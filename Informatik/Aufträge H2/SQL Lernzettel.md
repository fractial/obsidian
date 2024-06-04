## Grundlagen von SQL
- **SQL** steht für **Structured Query Language** (strukturierte Abfragesprache).
- SQL wird verwendet, um Daten aus Datenbanken zu lesen und zu manipulieren.

## Hauptbefehle
1. **SELECT**: Gibt an, welche Spalten ausgegeben werden sollen.
2. **FROM**: Gibt die Tabelle an, aus der die Daten stammen.
3. **WHERE**: Gibt die Bedingung an, unter der die Datensätze ausgewählt werden.

### Beispielabfrage
```sql
SELECT Saison, Fahrerweltmeister, KonstrukteursWM
FROM WMTitel
WHERE Fahrerweltmeister = 'Michael Schumacher';
```

## Platzhalter und Zeichenketten
- Alle Spalten anzeigen: `SELECT * FROM WMTitel;`
- Zeichenketten in einfache Anführungszeichen setzen: `'Michael Schumacher'`

## Vergleichsoperatoren
- `<`, `<=`, `=`, `<>`, `>=`, `>`
- Beispiel: Weltmeister mit mindestens 100 WM-Punkten
```sql
SELECT Fahrerweltmeister, WM_Punkte
FROM WMTitel
WHERE WM_Punkte >= 100;
```

## Logische Operatoren
- **AND**, **OR**, **NOT**
- Beispiel: Michael Schumacher mit mehr als 100 WM-Punkten
```sql
SELECT Saison, Fahrerweltmeister, WM_Punkte
FROM WMTitel
WHERE Fahrerweltmeister = 'Michael Schumacher'
AND WM_Punkte > 100;
```

## Bereichsoperator
- **BETWEEN** für Bereichsvergleiche
- Beispiel: Weltmeister mit Punkten zwischen 80 und 110
```sql
SELECT Saison, Fahrerweltmeister, WM_Punkte
FROM WMTitel
WHERE WM_Punkte BETWEEN 80 AND 110;
```

## Mustervergleich
- **LIKE** für Mustervergleiche (`%` für beliebige Zeichenfolge, `_` für ein einzelnes beliebiges Zeichen)
- Beispiel: Konstrukteursweltmeister Renault
```sql
SELECT Saison, KonstrukteursWM
FROM WMTitel
WHERE KonstrukteursWM LIKE '%Renault%';
```

## Listenoperator
- **IN** für eine Liste von Kriterien
- Beispiel: Ayrton Senna, Alain Prost oder Damon Hill als Weltmeister
```sql
SELECT Saison, Fahrerweltmeister
FROM WMTitel
WHERE Fahrerweltmeister IN ('Ayrton Senna', 'Alain Prost', 'Damon Hill');
```

## Umgang mit NULL-Werten
- **IS NULL** für NULL-Werte
- Beispiel: Jahre ohne Team_Punkte
```sql
SELECT *
FROM WMTitel
WHERE Team_Punkte IS NULL;
```

## Einzigartige Einträge
- **DISTINCT** für einzigartige Einträge
- Beispiel: Einmalige Namen der Weltmeister
```sql
SELECT DISTINCT Fahrerweltmeister
FROM WMTitel;
```

## Berechnungen und Alias
- Grundrechenarten (+, -, *, /) und **AS** für Spaltenbezeichnungen
- Beispiel: Prozentuale Ausbeute der WM-Punkte
```sql
SELECT Fahrerweltmeister, WM_Punkte/160*100 AS Ausbeute
FROM WMTitel;
```

## Sortieren von Ergebnissen
- **ORDER BY** für sortierte Ausgaben (Standard: aufsteigend, `DESC` für absteigend)
- Beispiel: Sortierte Ausbeute der WM-Punkte
```sql
SELECT Fahrerweltmeister, WM_Punkte/160*100 AS Ausbeute
FROM WMTitel
ORDER BY Ausbeute DESC;
```

## Limitierung der Ausgabe
- **LIMIT** für Begrenzung der Anzahl der ausgegebenen Datensätze
- Beispiel: Nur die Plätze 5 bis 7 der WM-Punkte-Ausbeute
```sql
SELECT Fahrerweltmeister, WM_Punkte/160*100 AS Ausbeute
FROM WMTitel
ORDER BY Ausbeute DESC, Fahrerweltmeister
LIMIT 4, 3;
```

Mit diesen grundlegenden SQL-Befehlen und Operatoren kannst du effektiv Daten aus einer Datenbank abfragen und manipulieren.

## Aggregatfunktionen
Mit Aggregatfunktionen kannst du statistische Auswertungen numerischer Daten in einer Datenbank vornehmen. Jede Aggregatfunktion wird auf ein Attribut einer Tabelle angewendet und liefert als Ergebnis einen Zahlenwert zurück.

### SUM()
- **SUM** (Summe): Zählt die numerischen Werte einer Spalte zusammen.
- Beispiel: Gesamtpunktzahl aller Weltmeister
```sql
SELECT SUM(WM_Punkte) AS Gesamtpunktzahl
FROM WMTitel;
```
- Tipp: Mit `AS` kannst du der Ergebnisspalte einen neuen Namen geben.

### COUNT()
- **COUNT** (Anzahl): Zählt die Anzahl der von NULL verschiedenen Werte einer Spalte.
- Beispiel: Anzahl der WM-Titel von Michael Schumacher
```sql
SELECT COUNT(Fahrerweltmeister) AS Anzahl_der_WM_Titel
FROM WMTitel
WHERE Fahrerweltmeister = 'Michael Schumacher';
```
- Hinweis: `COUNT(*)` zählt alle Datensätze, `COUNT(DISTINCT Spaltenname)` zählt nur die verschiedenen Werte einer Spalte.

### MIN() & MAX()
- **MIN** (Minimum): Gibt den kleinsten Wert einer Spalte zurück.
- **MAX** (Maximum): Gibt den größten Wert einer Spalte zurück.
- Beispiel: Höchste und niedrigste WM-Punkte
```sql
SELECT MAX(WM_Punkte) AS Max_WM_Punkte
FROM WMTitel;
```
```sql
SELECT MIN(WM_Punkte) AS Min_WM_Punkte
FROM WMTitel;
```

### AVG()
- **AVG** (Durchschnitt): Gibt den Durchschnitt aller Zahlenwerte einer Spalte.
- Beispiel: Durchschnittliche WM-Punkte der Weltmeister
```sql
SELECT AVG(WM_Punkte) AS Durchschnitt
FROM WMTitel;
```
- Alternativ (zum besseren Verständnis):
```sql
SELECT SUM(WM_Punkte) / COUNT(WM_Punkte) AS Durchschnitt
FROM WMTitel;
```
- Erklärung: `AVG(WM_Punkte) = SUM(WM_Punkte) / COUNT(WM_Punkte)`

## Hinweis zu Aggregatfunktionen
- Ohne die **GROUP BY**-Klausel kannst du Aggregatfunktionen und die Auswahl von Attributen nicht mischen.
- Die folgende `SELECT`-Anweisung liefert einen Fehler:
```sql
SELECT Fahrerweltmeister, SUM(WM_Punkte)
FROM WMTitel;
```
- Richtig wäre:
```sql
SELECT Fahrerweltmeister, SUM(WM_Punkte)
FROM WMTitel
GROUP BY Fahrerweltmeister;
```

Mit diesen Aggregatfunktionen kannst du effektive statistische Auswertungen in SQL vornehmen.

## Was ist ein Join?
Ein Join in SQL wird verwendet, um Daten aus mehreren Tabellen basierend auf einer logischen Beziehung zwischen diesen Tabellen zusammenzuführen. Joins nutzen Primär- und Fremdschlüssel, um Datensätze zu verknüpfen.

### Grundlegendes Beispiel: 1:n-Beziehung zwischen Fahrer und Fahrt
- Tabellenstruktur:
  - **Fahrer** (PersonalNr, Name, Vorname, StraßeNr, PLZ, Ort, Telefon)
  - **Fahrt** (FahrtNr, ↑PersonalNr, Kennzeichen, Datum, Preis, Dauer, Reisestart, Reiseziel)
- Die PersonalNr ist Primärschlüssel in der Tabelle Fahrer und Fremdschlüssel in der Tabelle Fahrt.

### Syntax für Joins
- **Klassische Syntax**:
  ```sql
  SELECT *
  FROM Fahrer, Fahrt
  WHERE Fahrer.PersonalNr = Fahrt.PersonalNr;
  ```

- **Inner Join Syntax**:
  ```sql
  SELECT *
  FROM Fahrer
  INNER JOIN Fahrt ON Fahrer.PersonalNr = Fahrt.PersonalNr;
  ```

### Ergebnis eines Joins
Die resultierende Tabelle enthält die kombinierten Daten aus beiden Tabellen, wobei Datensätze nur dann kombiniert werden, wenn die Werte der verknüpfenden Schlüssel übereinstimmen.

### Beispiel: 1:n-Beziehung zwischen Fahrt und Bus
- Tabellenstruktur:
  - **Fahrt** (FahrtNr, ↑Kennzeichen, ↑PersonalNr, Datum, Preis, Dauer, Reisestart, Reiseziel)
  - **Bus** (Kennzeichen, Bustyp, Baujahr, Sitzplätze)

- SQL-Abfrage:
  ```sql
  SELECT FahrtNr, Datum, Reiseziel
  FROM Fahrt
  INNER JOIN Bus ON Fahrt.Kennzeichen = Bus.Kennzeichen
  WHERE Sitzplätze > 50;
  ```

### Doppel-Join
Hier werden drei Tabellen verknüpft: Fahrer, Fahrt und Bus.
- SQL-Abfrage:
  ```sql
  SELECT Fahrer.PersonalNr, Name, Vorname, FahrtNr, Bus.Kennzeichen, Datum, Preis, Dauer, Reisestart, Reiseziel, Bustyp
  FROM Fahrer
  INNER JOIN Fahrt ON Fahrer.PersonalNr = Fahrt.PersonalNr
  INNER JOIN Bus ON Fahrt.Kennzeichen = Bus.Kennzeichen;
  ```

### Alias-Namen zur Vereinfachung
- Alias-Namen für Tabellen:
  ```sql
  SELECT *
  FROM Fahrer D
  INNER JOIN Fahrt F ON D.PersonalNr = F.PersonalNr
  INNER JOIN Bus B ON F.Kennzeichen = B.Kennzeichen;
  ```

### Triple-Join
Verknüpfung von vier Tabellen: Fahrt, Kunde, Bus und Bucht.
- SQL-Abfrage:
  ```sql
  SELECT Nachname, Vorname, GebuchtePlätze, Baujahr
  FROM Kunde K
  INNER JOIN Bucht O ON O.KundenNr = K.KundenNr
  INNER JOIN Fahrt F ON F.FahrtNr = O.FahrtNr
  INNER JOIN Bus B ON F.Kennzeichen = B.Kennzeichen
  WHERE Baujahr < 2000
  ORDER BY Nachname;
  ```

## Zusammenfassung
- **Inner Join**: Verknüpft Tabellen basierend auf übereinstimmenden Schlüsselwerten.
- **Alias-Namen**: Vereinfachen die Schreibweise und Lesbarkeit der Abfrage.
- **Mehrfach-Joins**: Ermöglichen das Verknüpfen von mehr als zwei Tabellen.
- **Bedingungen in Joins**: Filtern die resultierenden Datensätze basierend auf spezifischen Kriterien.