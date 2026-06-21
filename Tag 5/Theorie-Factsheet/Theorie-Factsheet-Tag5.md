# Theorie-Factsheet - Tag 5

## Thema

**Übersicht:** Dateizugriffsrechte unter Windows und Linux, Benutzer- und Gruppenkonzepte, Dateifreigaben, UNC-Pfade und Grundlagen zu virtuellen Maschinen.

## Kernkonzepte

### 1. Benutzer, Gruppen und Zugriffsrechte

**Erklärung:** Benutzer sind einzelne Accounts, Gruppen fassen mehrere Benutzer zusammen. Rechte sollten möglichst über Gruppen vergeben werden, weil neue Benutzer dann nur noch der richtigen Gruppe hinzugefügt werden müssen. Die wichtigsten Grundrechte sind **Lesen**, **Schreiben** und **Ausführen**. Unter Linux werden diese Rechte klassisch als `rwx` für Owner, Group und Others dargestellt.

### 2. Windows-Berechtigungen und Dateifreigaben

**Erklärung:** Windows arbeitet mit ACLs (Access Control Lists). Dadurch können Rechte feiner gesetzt werden als nur mit `rwx`. Typische beschränkte Sicherheitseinstellungen sind z.B. Lesen, Ändern oder Vollzugriff. Rechte können von übergeordneten Ordnern vererbt werden. Eine Dateifreigabe macht einen Ordner im Netzwerk verfügbar. Der Zugriff erfolgt über einen UNC-Pfad wie `\\SERVER01\Daten`.

### 3. Virtuelle Maschinen

**Erklärung:** Eine virtuelle Maschine ist ein Computer, der als Software auf einem physischen Gerät läuft. CPU, RAM, Speicher und Netzwerk werden vom Host-System bereitgestellt und der VM zugewiesen. Gängige Tools sind VirtualBox, VMware Workstation und Hyper-V. Beim Netzwerkmodus unterscheidet man z.B. NAT, Bridged und Host-only.

## Wichtige Begriffe

| Begriff | Definition |
|---------|-----------|
| Benutzer | Einzelner Account, der sich am System anmelden kann |
| Gruppe | Sammlung von Benutzern zur einfacheren Rechtevergabe |
| Lesen | Dateien oder Ordner anzeigen und öffnen |
| Schreiben | Dateien oder Ordner erstellen, ändern oder löschen |
| Ausführen | Programme oder Skripte starten |
| Owner | Besitzer einer Datei oder eines Ordners |
| Rechtevererbung | Unterordner übernehmen automatisch die Rechte des übergeordneten Ordners |
| Dateifreigabe | Ordner wird über das Netzwerk für andere Geräte verfügbar gemacht |
| UNC-Pfad | Netzwerkpfad im Format `\\Server\Freigabe` |
| ACL | Access Control List, detaillierte Berechtigungsliste unter Windows |
| NAT | VM nutzt das Netzwerk des Hosts über eine Übersetzung |
| Bridged | VM ist wie ein eigenes Gerät direkt im Netzwerk sichtbar |
| Host-only | VM kommuniziert nur mit dem Host und anderen Host-only-VMs |

## Zusammenfassung

- Rechte sollten nicht einzeln pro Benutzer, sondern über Gruppen vergeben werden
- Lesen, Schreiben und Ausführen sind die wichtigsten Grundrechte
- Windows nutzt ACLs, Linux klassisch `rwx` für Owner, Group und Others
- Dateifreigaben werden über UNC-Pfade wie `\\Server\Freigabe` genutzt
- Virtuelle Maschinen abstrahieren Hardware und können mit NAT, Bridged oder Host-only vernetzt werden
