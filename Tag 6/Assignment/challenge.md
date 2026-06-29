# Challenge 6 - ARISTA-PC: Umsetzungsplan

## Ziel

Die virtuelle Maschine `PCA` wird als Windows-10-Pro-System eingerichtet. Danach werden lokale Gruppen, Benutzer, Ordner, NTFS-Berechtigungen und eine Dateifreigabe exakt nach Auftrag umgesetzt und mit dem Auswertungsskript kontrolliert.

## 1. Virtuelle Maschine erstellen

| Punkt | Vorgabe |
| --- | --- |
| Betriebssystem | Windows 10 Pro, 64-bit, Deutsch |
| Virtualisierung | VMware |
| Netzwerkkarte waehrend Installation | Lokal |
| Erster Benutzer | `felix` |
| Vollstaendiger Name | Felix Muster |
| Passwort | `felix` |
| Rolle | Systemadministrator, Mitglied der Administratorengruppe |

Nach der Installation wird kontrolliert, ob `felix` wirklich Mitglied der lokalen Administratorengruppe ist.

## 2. Grundkonfiguration als Felix

Alle folgenden Arbeiten werden als `felix` ausgefuehrt.

| Einstellung | Wert |
| --- | --- |
| IP-Adresse | `10.0.1.1/24` |
| Hostname | `PCA` |
| Arbeitsgruppe | `GRA` |
| Router | `10.0.1.254` |
| DNS 1 | `10.0.1.254` |
| DNS 2 | `8.8.8.8` |

Das Tastaturlayout wird bei Bedarf auf Deutsch-Schweiz oder auf das Tastaturlayout des Notebooks angepasst.

## 3. Lokale Gruppen erstellen

Die automatisch vorhandenen Windows-Gruppen werden nicht geloescht.

| Gruppe | Beschreibung |
| --- | --- |
| `sales` | Marketing, Verkauf und Buchhaltung |
| `law` | Juristen, die Mandate bearbeiten |
| `archive` | Betreuer des Datenarchivs |

## 4. Lokale Benutzer erstellen

Die automatisch vorhandenen Windows-Benutzer werden nicht geloescht. Bei allen neuen Benutzern gilt: Das Kennwort muss bei der ersten Anmeldung nicht geaendert werden und laeuft nie ab. Jeder Account wird einmal angemeldet, damit das Homeverzeichnis erstellt wird.

| Username | Passwort | Vollstaendiger Name | Gruppen |
| --- | --- | --- | --- |
| `susi` | `susi` | Susi Wenger | `sales` |
| `alex` | `alex` | Alex Keller | `law` |
| `nina` | `nina` | Nina Burger | `sales`, `law`, `archive` |

## 5. Verzeichnisstruktur erstellen

Die Ordner werden unter `C:\daten` erstellt. Bei allen Ordnern wird die Vererbung deaktiviert, damit nur die im Auftrag definierten Rechte gelten.

```text
C:\daten
|-- sales
|-- law
|-- archive
|-- transfer
```

| Verzeichnis | Zweck |
| --- | --- |
| `C:\daten` | Daten-Toplevel-Verzeichnis |
| `C:\daten\sales` | Arbeitsverzeichnis der Gruppe `sales` |
| `C:\daten\law` | Arbeitsverzeichnis der Gruppe `law` |
| `C:\daten\archive` | Datenarchiv, betreut durch Gruppe `archive` |
| `C:\daten\transfer` | Datenaustausch und Dateifreigabe |

## 6. NTFS-Berechtigungen setzen

Legende: `F` = Vollzugriff, `R` = Lesen/Ausfuehren, `R/W` = Lesen und Schreiben/Aendern, leer = kein Zugriff.

| Verzeichnis | Owner | `felix` | Administratoren | SYSTEM | `law` | `sales` | `archive` |
| --- | --- | --- | --- | --- | --- | --- | --- |
| `C:\daten` | `felix` | F | F | F | R | R | R |
| `C:\daten\sales` | `sales` | F | F | F |  | R/W |  |
| `C:\daten\law` | `law` | F | F | F | R/W |  |  |
| `C:\daten\archive` | `archive` | F | F | F |  |  | R/W |
| `C:\daten\transfer` | `felix` | F | F | F | R/W | R/W | R/W |

Wichtig ist, dass Rechte ueber Gruppen vergeben werden und nicht direkt an einzelne Benutzer. Dadurch erhalten `susi`, `alex` und `nina` ihre Berechtigungen automatisch ueber ihre Gruppenzugehoerigkeit.

## 7. Dateifreigabe erstellen

| Punkt | Vorgabe |
| --- | --- |
| Freigabe-Verzeichnis | `C:\daten\transfer` |
| Freigabe-Name | `pcxch` |
| Freigabe-Berechtigung | `Jeder` darf aendern und lesen |

Die Freigabeberechtigung erlaubt den Zugriff grundsaetzlich. Die effektiven Rechte werden zusaetzlich durch die NTFS-Berechtigungen des Ordners `transfer` eingeschraenkt.

## 8. Kontrolle der Benutzer und Rechte

Nach der Einrichtung werden folgende Kontrollen durchgefuehrt:

- Als `susi`, `alex` und `nina` je einmal anmelden, damit die Homeverzeichnisse erstellt werden.
- Pruefen, ob `susi` in `C:\daten\sales` schreiben darf und keinen Zugriff auf `law` oder `archive` hat.
- Pruefen, ob `alex` in `C:\daten\law` schreiben darf und keinen Zugriff auf `sales` oder `archive` hat.
- Pruefen, ob `nina` in `sales`, `law`, `archive` und `transfer` die vorgesehenen Rechte hat.
- Pruefen, ob alle drei Benutzer in `C:\daten\transfer` schreiben duerfen.

## 9. Freigabe vom Notebook pruefen

Fuer die Freigabepruefung muessen VM und Notebook im gleichen Subnetz sein.

| Geraet | Beispiel-IP |
| --- | --- |
| VM `PCA` | `10.0.1.1/24` |
| Notebook | `10.0.1.2/24` |

Vorgehen:

- In VMware die Netzwerkkarte auf `Bridged: Connected directly to the physical network` umstellen.
- Im Virtual Network Editor `Bridged to: VirtualBox Host-Only Ethernet Adapter` setzen, falls dieser Adapter fuer die Verbindung zum Notebook verwendet wird.
- Auf dem Notebook den passenden Netzwerkadapter ebenfalls ins Subnetz `10.0.1.0/24` setzen.
- Verbindung mit `ping 10.0.1.1` pruefen, falls ICMP nicht durch die Firewall blockiert wird.
- Freigabe als Netzlaufwerk verbinden.

```cmd
net use Z: \\10.0.1.1\pcxch /user:susi susi
```

Danach wird im Explorer geprueft, ob Laufwerk `Z:` erreichbar ist und ob eine Testdatei erstellt, gelesen und geloescht werden kann.

Die Verbindung wird wieder getrennt mit:

```cmd
net use Z: /delete
```

Als Beweis werden sinnvolle Screenshots oder ein klares Testprotokoll abgelegt, zum Beispiel vom `net use`-Befehl, vom verbundenen Laufwerk `Z:` und von einer erfolgreichen Testdatei.

## 10. Automatische Auswertung

Zum Schluss wird das Auswertungsskript gemäss Auftrag ausgefuehrt.

1. `eval.zip` von `https://www.jarnold.ch/it/modul/117/eval.zip` herunterladen und entpacken.
2. `eval.ps1` nach `C:\Users` verschieben.
3. Windows PowerShell als Administrator starten, nicht die x86- oder ISE-Variante.
4. In `C:\Users` wechseln.
5. Ausfuehrungsrichtlinie temporaer erlauben und die Rueckfrage mit `J` bestaetigen.
6. Skript starten und `EVAL.txt` erzeugen.
7. `EVAL.txt` auf das Notebook kopieren und nicht bearbeiten.

```powershell
cd C:\Users
Set-ExecutionPolicy Unrestricted
Powershell.exe -command .\eval.ps1
```

## 11. Abgabe

Fuer die Abgabe werden mindestens folgende Dateien bereitgestellt:

- `EVAL.txt`, umbenannt nach den Familiennamen der Gruppenmitglieder.
- Beweis der Freigabepruefung vom Notebook aus.
- Diese Dokumentation als Plan fuer die Umsetzung der Challenge.

Bei der Besprechung muss erklaert werden koennen, wie das Benutzer- und Berechtigungskonzept umgesetzt wurde, wie die Freigabe getestet wurde, wie die Homeverzeichnisse entstanden sind und warum die Rechtevergabe funktioniert.
