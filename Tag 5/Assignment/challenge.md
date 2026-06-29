# Challenge 5 - Dateizugriffsrechte: Konzept

## Ziel

Fuer eine kleine Firma mit drei Abteilungen und zehn Mitarbeitenden wird eine klare Datenablage mit Benutzernamen, Gruppen, Ordnern, Besitzern und Zugriffsrechten erstellt. Die Rechte werden gruppenweise vergeben, damit die Administration einfach und nachvollziehbar bleibt.

## 1. Ausgangslage

Die Firma besteht aus drei Abteilungen:

| Abteilung | Zweck |
| --- | --- |
| Verwaltung | Personal, Finanzen und allgemeine Administration |
| Verkauf | Kundenkontakte, Angebote und Auftraege |
| IT | Support, Systeme und technische Dokumentation |

Die Daten werden zentral unter `D:\Firma` abgelegt. Jede Abteilung erhaelt ein eigenes Arbeitsverzeichnis. Zusaetzlich gibt es einen gemeinsamen Ordner fuer allgemeine Informationen.

## 2. Benutzernamenskonzept

Die Usernames werden klein geschrieben und bestehen aus dem ersten Buchstaben des Vornamens plus dem Nachnamen.

Beispiele:

- Anna Keller wird `akeller`
- Luca Baumann wird `lbaumann`
- Jonas Frei wird `jfrei`

Regeln:

- Alle Usernames werden klein geschrieben.
- Umlaute werden ersetzt: `ae`, `oe`, `ue`.
- Leerzeichen und Sonderzeichen werden nicht verwendet.
- Bei Namenskonflikten wird eine Zahl angehaengt, zum Beispiel `akeller2`.

Vorteile:

- Das Schema ist einfach lesbar und schnell verstaendlich.
- Usernames koennen automatisiert aus Vorname und Nachname erzeugt werden.
- Die Abteilung steht nicht im Namen, deshalb bleibt der Username bei einem Abteilungswechsel gleich.
- Neue Benutzer koennen ohne neue Namenslogik integriert werden.

## 3. Benutzer-Matrix

| Username | Vollstaendiger Name | Abteilung | Funktion | Initialpasswort |
| --- | --- | --- | --- | --- |
| `akeller` | Anna Keller | Verwaltung | Sachbearbeiterin | `Start-2026!01` |
| `vmeier` | Vanessa Meier | Verwaltung | Teamleitung | `Start-2026!02` |
| `rschmid` | Rafael Schmid | Verwaltung | Buchhaltung | `Start-2026!03` |
| `mlanger` | Marco Langer | Verwaltung | Geschaeftsleitung | `Start-2026!04` |
| `nkoenig` | Nora Koenig | Verkauf | Teamleitung | `Start-2026!05` |
| `lbaumann` | Luca Baumann | Verkauf | Verkauf Innendienst | `Start-2026!06` |
| `mmueller` | Mia Mueller | Verkauf | Verkauf Aussendienst | `Start-2026!07` |
| `jfrei` | Jonas Frei | IT | Support | `Start-2026!08` |
| `tleu` | Tim Leu | IT | Systembetreuung | `Start-2026!09` |
| `shuber` | Sara Huber | IT | Helpdesk | `Start-2026!10` |

Das Initialpasswort muss beim ersten Login geaendert werden. Dadurch ist das Startpasswort nur fuer die Erstanmeldung gedacht.

## 4. Gruppen und Mitgliedschaften

Rechte werden nicht direkt an einzelne Benutzer vergeben, sondern ueber Gruppen. Dadurch muessen neue Mitarbeitende nur der passenden Gruppe hinzugefuegt werden.

| Gruppe | Zweck | Mitglieder |
| --- | --- | --- |
| `grp-verwaltung` | Zugriff auf Verwaltungsdaten | `akeller`, `vmeier`, `rschmid`, `mlanger` |
| `grp-verkauf` | Zugriff auf Verkaufsdaten | `nkoenig`, `lbaumann`, `mmueller` |
| `grp-it` | Zugriff auf IT-Daten und Support-Leserechte | `jfrei`, `tleu`, `shuber` |

## 5. Verzeichnisstruktur

```text
D:\Firma
|-- 00_Allgemein
|-- 10_Verwaltung
|-- 20_Verkauf
|-- 30_IT
```

| Verzeichnis | Zweck | Owner |
| --- | --- | --- |
| `D:\Firma\00_Allgemein` | Allgemeine Informationen fuer alle Abteilungen | `mlanger` |
| `D:\Firma\10_Verwaltung` | Verwaltungs-, Personal- und Finanzdaten | `vmeier` |
| `D:\Firma\20_Verkauf` | Kunden-, Angebots- und Auftragsdaten | `nkoenig` |
| `D:\Firma\30_IT` | Technische Dokumentation und Supportdaten | `tleu` |

Die Nummerierung sorgt dafuer, dass die Ordner immer in einer logischen Reihenfolge angezeigt werden. `00_Allgemein` steht bewusst an erster Stelle, weil dieser Ordner fuer alle Abteilungen gedacht ist. Die Fachordner sind nach Abteilungen getrennt, damit sensible Daten nicht vermischt werden.

## 6. Rechte- und Owner-Matrix

Legende: `Kein Zugriff` = kein Zugriff, `Lesen` = Dateien ansehen/oeffnen, `Lesen+Schreiben` = Dateien erstellen, aendern und loeschen.

| Verzeichnis | Owner | `grp-verwaltung` | `grp-verkauf` | `grp-it` |
| --- | --- | --- | --- | --- |
| `D:\Firma\00_Allgemein` | `mlanger` | Lesen+Schreiben | Lesen+Schreiben | Lesen+Schreiben |
| `D:\Firma\10_Verwaltung` | `vmeier` | Lesen+Schreiben | Kein Zugriff | Lesen |
| `D:\Firma\20_Verkauf` | `nkoenig` | Lesen | Lesen+Schreiben | Lesen |
| `D:\Firma\30_IT` | `tleu` | Kein Zugriff | Kein Zugriff | Lesen+Schreiben |

## 7. Begruendung der Rechte

`00_Allgemein` ist fuer alle Abteilungen gedacht. Deshalb erhalten alle Gruppen Lesen+Schreiben, damit gemeinsame Informationen abgelegt und gepflegt werden koennen.

`10_Verwaltung` enthaelt sensible Personal- und Finanzdaten. Nur die Verwaltung darf schreiben. Die IT erhaelt Leserechte fuer Supportfaelle. Der Verkauf erhaelt keinen Zugriff, weil diese Daten fuer die Arbeit im Verkauf nicht notwendig sind.

`20_Verkauf` enthaelt Kunden- und Auftragsdaten. Der Verkauf darf schreiben, weil diese Daten dort gepflegt werden. Die Verwaltung darf lesen, damit Auftraege und Rechnungsinformationen nachvollzogen werden koennen. Die IT darf lesen, falls Support benoetigt wird.

`30_IT` enthaelt technische Informationen. Nur die IT darf schreiben. Verwaltung und Verkauf haben keinen Zugriff, weil technische Konfigurationen und interne Supportdaten nicht fuer alle sichtbar sein muessen.

## 8. Owner-Konzept

Der Owner ist jeweils die fachlich verantwortliche Person oder Teamleitung des Ordners.

| Owner | Begruendung |
| --- | --- |
| `mlanger` | Geschaeftsleitung, verantwortlich fuer allgemeine Firmeninformationen |
| `vmeier` | Teamleitung Verwaltung, verantwortlich fuer Verwaltungsdaten |
| `nkoenig` | Teamleitung Verkauf, verantwortlich fuer Verkaufsdaten |
| `tleu` | Systembetreuung IT, verantwortlich fuer technische Daten |

Owner werden nicht zufaellig gewaehlt. Sie muessen entscheiden koennen, welche Daten korrekt sind und wer fachlich Zugriff benoetigt.

## 9. Integration neuer Benutzer

Bei einem neuen Mitarbeitenden wird folgender Ablauf verwendet:

1. Vollstaendigen Namen und Abteilung erfassen.
2. Username nach Schema erzeugen.
3. Initialpasswort vergeben.
4. Benutzer der passenden Gruppe zuweisen.
5. Beim ersten Login Passwortwechsel verlangen.
6. Zugriff auf die Ordner testen.

Beispiel: Die neue Mitarbeiterin Lea Steiner beginnt im Verkauf. Ihr Username wird `lsteiner`. Sie wird der Gruppe `grp-verkauf` hinzugefuegt und erhaelt dadurch automatisch Schreibrechte auf `D:\Firma\20_Verkauf` und `D:\Firma\00_Allgemein`.

## 10. Risiken von zu weit gefassten Rechten

Zu breite Rechte sind ein Sicherheitsrisiko. Wenn alle Benutzer ueberall schreiben duerfen, koennen Daten versehentlich geloescht, ueberschrieben oder an falschen Orten gespeichert werden. Ausserdem koennen sensible Informationen sichtbar werden, obwohl sie fuer die Arbeit nicht benoetigt werden.

Darum gilt das Prinzip: Jeder Benutzer erhaelt nur die Rechte, die fuer seine Arbeit notwendig sind. Schreibrechte werden nur dort vergeben, wo die Gruppe Daten wirklich pflegen muss.

## 11. Ergebnis

Das Konzept erfuellt die Anforderungen der Challenge 5:

- Ein klares Benutzernamensschema ist definiert und begruendet.
- Zehn fiktive Benutzer mit Username, Name, Abteilung, Funktion und Initialpasswort sind dokumentiert.
- Drei Gruppen mit Mitgliedschaften sind definiert.
- Vier Verzeichnisse mit Ownern sind festgelegt.
- Eine Rechte-Matrix mit Kein Zugriff, Lesen und Lesen+Schreiben ist vorhanden.
- Die wichtigsten Entscheidungen sind so begruendet, dass sie in der Besprechung erklaert werden koennen.
