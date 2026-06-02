# Theorie-Factsheet - Tag 3

## Thema

**Übersicht:** Unterrichtsblock 3 – Netzwerkadressierung Grundlagen: IPv4-Adressen, Subnetzmasken, Standardgateway, Subnetting, DHCP/APIPA, Loopback und Windows-Kommandos zur Netzwerkanalyse

## Kernkonzepte

### 1. Netzwerkparameter

**Erklärung:** Damit ein Host in einem Netzwerk kommunizieren kann, braucht er mehrere Parameter. Die IP-Adresse identifiziert den Host logisch, die Subnetzmaske bestimmt den Netz- und Hostanteil, das Standardgateway verbindet das lokale Netz mit anderen Netzen und DNS übersetzt Namen in IP-Adressen. Die MAC-Adresse ist die feste Hardwareadresse der Netzwerkkarte und wird innerhalb des lokalen Netzes verwendet.

### 2. Subnetting

**Erklärung:** Beim Subnetting wird ein grösseres Netzwerk in kleinere Teilnetze aufgeteilt. In M117 werden hauptsächlich `/8`, `/16` und `/24` verwendet. Bei einem `/24`-Netz wie `172.20.10.0/24` ist `172.20.10.0` die Netzwerkadresse, `172.20.10.255` die Broadcastadresse und die nutzbaren Hostadressen liegen dazwischen.

### 3. Adresszuweisung und Fehlersuche

**Erklärung:** IP-Adressen können statisch oder dynamisch per DHCP vergeben werden. Statische Adressen eignen sich für Router, Server, Drucker und geplante kleine Netze. Wenn DHCP nicht funktioniert, kann Windows automatisch eine APIPA-Adresse aus `169.254.0.0/16` vergeben. Mit `ping`, `ipconfig`, `arp` und `netstat` kann man die Konfiguration und Verbindungen prüfen.

## Wichtige Begriffe

| Begriff | Definition |
|---------|-----------|
| IPv4-Adresse | Logische Adresse eines Hosts, z.B. `172.20.10.11` |
| Subnetzmaske | Legt fest, welcher Teil der IP-Adresse zum Netz und welcher zum Host gehört |
| CIDR | Kurzschreibweise der Subnetzmaske, z.B. `/24` für `255.255.255.0` |
| Standardgateway | Router-Adresse, über die andere Netzwerke oder das Internet erreicht werden |
| Netzwerkadresse | Erste Adresse eines Subnetzes; identifiziert das Netz und wird keinem Host vergeben |
| Broadcastadresse | Letzte Adresse eines Subnetzes; Nachricht an alle Hosts im Subnetz |
| DHCP | Dienst zur automatischen Zuweisung von IP-Adresse, Maske, Gateway und DNS |
| APIPA | Automatische Ersatzadresse aus `169.254.0.0/16`, wenn DHCP nicht erreichbar ist |
| Loopback | Adresse `127.0.0.1` zum Testen des eigenen Hosts |
| CSMA/CD | Zugriffsverfahren für alte Halbduplex-Ethernet-Netze zur Kollisionserkennung |

## Zusammenfassung

- Hosts brauchen IP-Adresse, Subnetzmaske, Gateway und meistens DNS für die Kommunikation
- Die Subnetzmaske trennt Netz-ID und Host-ID
- Netzwerkadresse und Broadcastadresse dürfen nicht als Hostadressen verwendet werden
- Private IPv4-Bereiche nach RFC 1918 sind `10.0.0.0/8`, `172.16.0.0/12` und `192.168.0.0/16`
- DHCP vergibt Netzwerkparameter automatisch; APIPA weist auf ein DHCP-Problem hin
- `ipconfig`, `ping`, `arp` und `netstat` helfen bei der Fehlersuche im Netzwerk
