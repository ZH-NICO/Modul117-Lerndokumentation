# Theorie-Factsheet - Tag 2

## Thema

**Übersicht:** Unterrichtsblock 2 – Evaluation von PC-Arbeitsplätzen und Planung der Ethernetverkabelung (Challenge «ARISTA-LAN»): logisches Layout, Verkabelungsplan und Stückliste

## Kernkonzepte

### 1. Logisches Layout

**Erklärung:** Das logische Layout zeigt, welche Geräte (PCs, Drucker, Switches, Router) wie miteinander verbunden sind. Pro Netzwerkverbindung wird eine eigene, unterscheidbare Linie gezeichnet, ohne Loops. Es dient dem Netzwerktechniker als Arbeitspapier und enthält Hostnamen sowie IP-Adressen.

### 2. Verkabelungsplan

**Erklärung:** Der Verkabelungsplan wird auf dem Gebäudegrundriss erstellt und zeigt die physische Verkabelung. UGV-Kabel (fest verlegt) werden blau dargestellt, Patchkabel rot. Die Kabel laufen sauber in Aufputzkabelkanälen von RJ45-Steckdose zu RJ45-Steckdose – keine «Lianen», keine Bohrungen im Sanitärbereich.

### 3. Stückliste

**Erklärung:** Die Stückliste ist der Einkaufszettel mit allem benötigten Material: Geräte, Anzahl Switches, Portanzahl inkl. Reserve, berechnete Meter UGV-Kabel, Patchkabel, RJ45-Steckdosen und Kabelkanäle – mit Position, Anzahl, Bezeichnung, Eigenschaften und Preis.

## Wichtige Begriffe

| Begriff | Definition |
|---------|-----------|
| Logisches Layout | Schematische Darstellung der Netzwerkverbindungen zwischen den Geräten |
| Verkabelungsplan | Plan der physischen Verkabelung auf dem Gebäudegrundriss |
| UGV-Kabel | Universelle Gebäudeverkabelung – fest verlegtes Kabel (im Plan blau) |
| Patchkabel | Flexibles Anschlusskabel von Steckdose zu Gerät/Switch (im Plan rot) |
| L2-Switch | Unmanaged Layer-2-Switch, verbindet Geräte auf MAC-Ebene (keine IP) |
| WAN-Router | Verbindet das LAN WAN-seitig mit dem ISP/Internet, LAN-seitig mit einem Switch |
| RJ-45 | Standard-Steckverbinder für Ethernet (8-polig) |
| Subnetzmaske | Legt fest, welcher Teil der IP-Adresse Netz und welcher Host ist |

## Zusammenfassung

- Erst planen (logisches Layout), dann physisch verkabeln (Verkabelungsplan), dann beschaffen (Stückliste)
- UGV = fest verlegt (blau), Patch = flexibel zum Gerät (rot)
- IP-Adresse/Subnetzmaske nur bei PCs, Druckern und Router – nicht bei L2-Switches
- WAN-Router trennt LAN und Internet; LAN-seitig genügt ein einziger Switch, kein Subnetting
- Ziel: so wenig Kabel wie möglich, keine Loops, saubere Gebäudeverkabelung
