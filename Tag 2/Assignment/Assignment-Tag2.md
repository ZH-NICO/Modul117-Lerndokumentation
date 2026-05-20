# Assignment - Tag 2

## Aufgabe

**Beschreibung:** Unterrichtsblock 2 – Challenge 2 «ARISTA-LAN». Evaluation von PC-Arbeitsplätzen inklusive Planung der Ethernetverkabelung. Für die Firma Arista GmbH (Office-Dienstleistungen, 10 Mitarbeiter) sollen die alten PCs und Drucker ersetzt und die Büroräume neu mit Ethernet verkabelt werden. Dazu sind ein logisches Layout, ein Verkabelungsplan und eine Stückliste zu erstellen. Diese Challenge zählt doppelt und wird im Lerntandem bearbeitet.

## Anforderungen

- Logisches Layout (JPG) gemäss Vorlage: Icons verwenden, pro Netzwerkverbindung eine unterscheidbare Linie, keine Loops, so wenig Kabel wie möglich
- L2-Switches korrekt anschliessen: jeder PC, Drucker, Router und Switch an einen RJ-45-Port; Hostnamen für PCs, Switches und Router
- Private IP-Adresse/Subnetzmaske nur bei PCs, Druckern und Router – nicht bei Switches
- WAN-Router korrekt: WAN-seitig zum ISP/WWW, LAN-seitig an einen einzigen Switch, kein Subnetting
- Verkabelungsplan (JPG) gemäss Grundriss: UGV blau, Patch rot, vorgegebene Icons, saubere Gebäudeverkabelung in Aufputzkanälen, keine Bohrungen im Sanitärbereich
- Stückliste (PDF) als Einkaufszettel: alle Komponenten, Switch-Portanzahl inkl. Reserve, berechnete (nicht geschätzte) Meter UGV-Kabel, Patchkabel, RJ45-Steckdosen, Kabelkanäle und Produktinfos
- Beschaffung: 10x Office-PC (WIN11-Pro, CH-Tastatur, Maus, Screen), 3x B/W-Laserdrucker, 1x Color-Laserdrucker, benötigte Anzahl Unmanaged L2-Switches + Kabel-/Montagezubehör

## Umsetzung

**Vorgehen:** Bürogrundriss analysiert und Arbeitsplätze pro Büro gezählt (A:1, B:3, C:3, D:1, E:Sitzungszimmer ohne Arbeitsplatz, F:2 = 10 PCs). Mit dem IPERKA-Modell geplant: ein Subnetz mit privatem Adressbereich (z.B. 192.168.1.0/24), WAN-Router → zentraler Switch → weitere L2-Switches in den Bürobereichen. Logisches Layout mit den vorgegebenen Icons gezeichnet, danach den Verkabelungsplan auf dem Grundriss erstellt (UGV blau von RJ45-Steckdose zu RJ45-Steckdose durch Aufputzkanäle, Patchkabel rot zu den Geräten). Drucker bedarfsgerecht auf die Büros verteilt. Kabellängen anhand des Grundrisses berechnet und in die Stückliste übernommen.

**Ergebnis:** Logisches Layout (JPG), Verkabelungsplan (JPG) und Stückliste (PDF) erstellt und im Lerntandem auf dem Teams-Chat abgegeben. Enthalten: 10 Office-PCs, 3 B/W-Laserdrucker, 1 Color-Laserdrucker, die benötigte Anzahl Unmanaged L2-Switches sowie Patch-/UGV-Kabel, Kabelkanäle und RJ45-Steckdosen. Logisches Layout und Verkabelungsplan stimmen bei Komponenten, Verbindungen und Hostnamen überein.

## Erkenntnisse

- Eine saubere Planung (logisches Layout) vor der Verkabelung verhindert Rückfragen und Fehler beim Elektroinstallateur
- UGV-Kabel (fest verlegt, blau) und Patchkabel (zu den Geräten, rot) müssen klar unterschieden werden – die Farbcodierung macht den Plan lesbar
- IP-Adressen werden nur bei PCs, Druckern und Router vergeben, nicht bei Switches, da ein L2-Switch auf MAC-Ebene arbeitet
- Der WAN-Router trennt das LAN vom Internet; LAN-seitig genügt ein einziger Switch, kein Subnetting nötig
- Bautechnische Auflagen (keine Bohrungen im Sanitärbereich, Aufputzkanäle) beeinflussen die Kabelführung direkt
