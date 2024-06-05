#### S. 307, 3.
1. In der Tabelle "Qualifikationsspiele" lässt sich alleinig das Attribut "Datum" als Slüssel definieren, da jeder Wert (bspw.: "07.09.12") nur einmal vorkommt. Alle anderen Attribute haben Werte die mehrmals vorkommen z. B. beim Attribut "Gegner" "Österreich" und "Heimspiel/Auswärtsspiel" "HS"/"AS". Doch selbst bei "Datum" können in Zukunft Probleme auftreten, falls mehrere Spiele am selben Tag gehalten werden.
2. `SELECT * FROM Qualifikationsspiele WHERE Heimspiel/Auswärtsspiel = "HS";`
   `SELECT Datum FROM Qualifikationsspiele WHERE Gegner = "Österreich";`
   `SELECT DISTINCT Gegner FROM Qualifikationsspiele;`

#### S. 308, 4.
Types (in rs notation)
`u32` | `String` | `Option<Vec<String>>` | `Option<Vec<u32>>`

Schüler:

| <u>SID</u> | Name   | Attribute | KID |
| ---------- | ------ | --------- | --- |
| 001        | Kevin  | null      | 784 |
| 002        | Thomas | null      | 784 |
| 003        | Alan   | null      | 784 |

Kurse:

| <u>KID</u> | Fach               | Lehrer    | Raum  |
| ---------- | ------------------ | --------- | ----- |
| 784        | Sozialwissenschaft | Mr. White | C 204 |
Alle Schüler im Kurs "784": `SELECT * FROM Schüler WHERE KID = "784"`
Der Lehrer von Kevins Sozialwissenschafts Kurs: `SELECT * FROM Schüler INNER JOIN Kurse ON Schüler.KID = Kurse.KID WHERE Name = "Kevin"`
Alle Kurse die belegt werden: `SELECT DISTINCT Fach FROM Schüler INNER JOIN Kurse ON Schüler.KID = Kurse.KID`