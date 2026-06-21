# Assignment - Tag 5

## Aufgabe

**Beschreibung:** Unterrichtsblock 5 - Dateizugriffsrechte. Für eine kleine Firma mit drei Abteilungen und zehn Mitarbeitenden wird ein Konzept für Benutzernamen, Gruppen, Verzeichnisstruktur, Besitzer und Zugriffsrechte erstellt.

## Anforderungen

- Benutzernamenskonzept definieren und begründen
- Zehn fiktive Benutzer mit Username, vollständigem Namen, Abteilung und Initialpasswort erfassen
- Gruppen definieren und Benutzer den passenden Gruppen zuordnen
- Verzeichnisstruktur mit vier Ordnern festlegen
- Rechte-Matrix erstellen: Kein Zugriff, Lesen, Lesen+Schreiben
- Besitzer der Ordner definieren und begründen

## Umsetzung

**Vorgehen:** Zuerst wurden drei Abteilungen festgelegt: Verwaltung, Verkauf und IT. Danach wurde ein einheitliches Benutzernamensschema gewählt. Die Berechtigungen werden nicht direkt auf einzelne Benutzer vergeben, sondern über Abteilungsgruppen. So bleibt die Administration einfacher und neue Mitarbeitende können schnell integriert werden.

### Benutzernamenskonzept

Usernames werden klein geschrieben und bestehen aus dem ersten Buchstaben des Vornamens plus Nachname. Umlaute werden ersetzt (`ä` -> `ae`, `ö` -> `oe`, `ü` -> `ue`). Beispiel: Anna Keller wird zu `akeller`.

Vorteile:

- Einfach zu verstehen und gut lesbar
- Automatisierbar, weil der Username aus Vor- und Nachname generiert werden kann
- Keine Abteilungsnamen im Username, dadurch bleibt der Account bei Abteilungswechsel gültig
- Bei Namenskonflikten kann eine Zahl ergänzt werden, z.B. `akeller2`

### Benutzer-Matrix

| Username | Vollständiger Name | Abteilung | Rolle | Initialpasswort |
| --- | --- | --- | --- | --- |
| `akeller` | Anna Keller | Verwaltung | Sachbearbeiterin | `Start-2026!01` |
| `vmeier` | Vanessa Meier | Verwaltung | Teamleitung | `Start-2026!02` |
| `rschmid` | Rafael Schmid | Verwaltung | Buchhaltung | `Start-2026!03` |
| `nkoenig` | Nora König | Verkauf | Teamleitung | `Start-2026!04` |
| `lbaumann` | Luca Baumann | Verkauf | Verkauf Innendienst | `Start-2026!05` |
| `mmueller` | Mia Müller | Verkauf | Verkauf Aussendienst | `Start-2026!06` |
| `jfrei` | Jonas Frei | IT | Support | `Start-2026!07` |
| `tleu` | Tim Leu | IT | Systembetreuung | `Start-2026!08` |
| `shuber` | Sara Huber | IT | Helpdesk | `Start-2026!09` |
| `mlanger` | Marco Langer | Verwaltung | Geschäftsleitung | `Start-2026!10` |

Hinweis: Das Initialpasswort muss beim ersten Login geändert werden.

### Gruppen und Mitgliedschaften

| Gruppe | Zweck | Mitglieder |
| --- | --- | --- |
| `grp-verwaltung` | Zugriff auf Verwaltungsdaten | `akeller`, `vmeier`, `rschmid`, `mlanger` |
| `grp-verkauf` | Zugriff auf Verkaufsdaten | `nkoenig`, `lbaumann`, `mmueller` |
| `grp-it` | Zugriff auf IT-Daten und technische Ablage | `jfrei`, `tleu`, `shuber` |

### Verzeichnisstruktur

```text
D:\Firma
|-- 00_Allgemein
|-- 10_Verwaltung
|-- 20_Verkauf
|-- 30_IT
```

Die Nummerierung sorgt dafür, dass die Ordner immer in der gleichen Reihenfolge sortiert werden. Gemeinsame Informationen liegen in `00_Allgemein`, abteilungsspezifische Daten in eigenen Ordnern.

### Rechte- und Owner-Matrix

| Verzeichnis | Owner | `grp-verwaltung` | `grp-verkauf` | `grp-it` |
| --- | --- | --- | --- | --- |
| `D:\Firma\00_Allgemein` | `mlanger` | Lesen+Schreiben | Lesen+Schreiben | Lesen+Schreiben |
| `D:\Firma\10_Verwaltung` | `vmeier` | Lesen+Schreiben | Kein Zugriff | Lesen |
| `D:\Firma\20_Verkauf` | `nkoenig` | Lesen | Lesen+Schreiben | Lesen |
| `D:\Firma\30_IT` | `tleu` | Kein Zugriff | Kein Zugriff | Lesen+Schreiben |

Die Owner sind jeweils die verantwortlichen Personen der Abteilung. Sie sind fachlich zuständig und können beurteilen, wer Zugriff benötigt. IT erhält auf Fachordner nur Leserechte im normalen Betrieb, damit Support möglich ist, aber keine unnötigen Schreibrechte entstehen.

**Ergebnis:** Es entstand ein klares Benutzer-, Gruppen- und Berechtigungskonzept für eine kleine Firma. Neue Benutzer werden mit dem definierten Namensschema erstellt und danach nur noch der passenden Gruppe zugewiesen. Dadurch erhalten sie automatisch die richtigen Rechte auf die Ordnerstruktur.

## Erkenntnisse

- Gruppenrechte sind übersichtlicher und sicherer als Einzelberechtigungen pro Benutzer
- Zu weit gefasste Rechte erhöhen das Risiko von Datenverlust oder ungewollten Änderungen
- Ein klarer Verzeichnisbaum hilft, Daten schnell zu finden und Verantwortlichkeiten zu erkennen
- Owner sollten fachlich verantwortlich sein, nicht zufällig gewählt werden
- Neue Mitarbeitende können mit einem festen Schema schneller und fehlerärmer eingerichtet werden
