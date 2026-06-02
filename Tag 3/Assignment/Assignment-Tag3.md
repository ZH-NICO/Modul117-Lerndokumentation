# Assignment - Tag 3

## Aufgabe

**Beschreibung:** Unterrichtsblock 3 – Netzwerkadressierung Grundlagen. Erarbeiten der wichtigsten Netzwerkparameter wie Hostname, MAC-Adresse, IPv4-Adresse, Subnetzmaske, Standardgateway und DNS. Zusätzlich wird ein Adresskonzept für eine kleine Firma mit drei Abteilungen zu je drei Mitarbeitern erstellt und in Cisco Packet Tracer umgesetzt.

## Anforderungen

- Zugriffsverfahren CSMA/CD in Bezug auf Halbduplex und Vollduplex erklären können
- Netzwerkparameter wie IP-Adresse, Subnetzmaske, Gateway und DNS-Server kennen und richtig einsetzen
- Ein privates IPv4-/16-Netz aus RFC 1918 verwenden und daraus drei /24-Subnetze planen
- Pro Abteilung ein eigenes Subnetz mit statischen Adressen erstellen
- Netzwerkadresse, nutzbare Hostadressen und Broadcastadresse pro Subnetz bestimmen
- Standardgateway für den Internetzugang einplanen
- Topologie in Cisco Packet Tracer umsetzen und mit Ping/IP-Konfiguration testen
- Windows-Befehle arp, ping, ipconfig und netstat zweckmässig einsetzen können

## Umsetzung

**Vorgehen:** Als privates Ausgangsnetz wurde `172.20.0.0/16` gewählt. Für die Firma wurden drei Abteilungen geplant: Verwaltung, Verkauf und Technik. Jede Abteilung erhält ein eigenes `/24`-Subnetz, damit die Bereiche logisch getrennt sind und später einfacher erweitert werden können. Die Adressen werden statisch vergeben. Pro Subnetz ist die `.1` als Standardgateway vorgesehen, die PCs erhalten die Adressen `.11` bis `.13`.

| Abteilung | Subnetz | Subnetzmaske | Netzwerkadresse | Gateway | Hosts | Broadcast |
| --- | --- | --- | --- | --- | --- | --- |
| Verwaltung | `172.20.10.0/24` | `255.255.255.0` | `172.20.10.0` | `172.20.10.1` | `172.20.10.11` - `172.20.10.13` | `172.20.10.255` |
| Verkauf | `172.20.20.0/24` | `255.255.255.0` | `172.20.20.0` | `172.20.20.1` | `172.20.20.11` - `172.20.20.13` | `172.20.20.255` |
| Technik | `172.20.30.0/24` | `255.255.255.0` | `172.20.30.0` | `172.20.30.1` | `172.20.30.11` - `172.20.30.13` | `172.20.30.255` |

**Ergebnis:** Das Adresskonzept ist vorbereitet. In Cisco Packet Tracer kann die Topologie mit einem Router als Standardgateway, einem Switch pro Abteilung und je drei PCs pro Abteilung umgesetzt werden. Jeder PC erhält eine statische IP-Adresse aus seinem Subnetz, die passende Subnetzmaske `255.255.255.0` und das Gateway seiner Abteilung. Der Router verbindet die drei Subnetze miteinander und stellt den Weg ins Internet bereit. Die Funktion wird mit `ping` zwischen PCs, zum Gateway und zum simulierten Internet getestet.

## Erkenntnisse

- Ein `/16`-Netz bietet viele Adressen und kann sauber in mehrere `/24`-Subnetze aufgeteilt werden
- Pro Subnetz dürfen Netzwerkadresse und Broadcastadresse nicht an Hosts vergeben werden
- Das Standardgateway ist nötig, damit Geräte andere Subnetze oder das Internet erreichen können
- Statische Adressen sind sinnvoll für kleine, geplante Umgebungen und wichtige Geräte wie Router, Server oder Drucker
- APIPA-Adressen zeigen, dass ein Gerät keine gültige Adresse per DHCP erhalten hat
- Mit `ipconfig`, `ping`, `arp` und `netstat` kann man die Netzwerkkonfiguration prüfen und Fehler eingrenzen
