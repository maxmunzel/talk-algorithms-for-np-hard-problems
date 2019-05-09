% Datenbanken I -- Einführung
% Michael Kofler
% September 2013

# Einführung

## Inhalt der Lehrveranstaltung

* Konzepte relationaler Datenbanksysteme
* Design von Datenbanken
* Daten mit SQL^[Standard Query Language] abfragen und verändern

Basis für alle Beispiele: MySQL

## Inhalt im Detail

* Einführung, Hello-World!-Beispiel, MySQL
* Datenbankmodellierung (semantisch, logisch, physisch)
* Entity-Relationship-Modelle
* Datentypen
* Relationships (1:1, 1:n, n:m, identifying vs. non-identifying)
* Primary Keys, Foreign Keys, Foreign Key Constraints
* Normalformen (1NF, 2NF, 3NF), De-Normalisierung
* SQL-Einführung (SELECT, INSERT, UPDATE, DELETE, CREATE/ALTER/DROP TABLE)
* Transaktionen, ACID
* viele praktische Beispiel

## Datenbanken versus Datenbanksysteme

\colA{6cm}

Datenbanken

* Adressen für Serienbriefe
* Patientenkartei einer Artzpraxis
* Warenbestand eines Lebensmitteldiskonters
* Facebook
* Telekom-Abrechnungssystem
* ...

\colB{6cm}

Datenbanksysteme

* IBM DB/2
* Microsoft Access
* Microsoft SQL Server
* MySQL
* Oracle
* PostgreSQL
* SAP MaxDB
* SQLite

\colEnd

\vspace{3mm}

PS: Ein Datenbanksystem ist genaugenommen ein *Datenbankmanagagementsystem*.\
**DBMS** = *Database Management System*.

## Wozu Datenbanksysteme?

* Sicherheit

    + Datenverluste vermeiden
    + steuern, wer welche Daten lesen/verändern darf
    + aufzeichnen, wer wann was verändert hat
    + Transaktionen
    + Backups
    + Hochverfügbarkeit

* Netzwerkzugriff
* Multi-User-Zugriff mit Zugriffskontrolle

## Client/Server-Modell

\includegraphics[width=0.8\textwidth]{bilder/client-server.png}

## Relationale Datenbanken

* Organisation aller Daten in Tabellen
* jede Tabelle für sich: ähnlich wie Excel-Tabellenblatt
* Tabellen sind miteinander verknüpft (Relationships)
* Verknüpfungen über ID-Spalten (Primary Key, Foreign Key)

## Relationale Datenbanken

\hbox{}\hspace*{-9mm}\includegraphics[width=1.17\textwidth]{bilder/schema-mylibrary.png}

## Standard Query Language = SQL

```sql
SELECT * FROM personen
    
SELECT * FROM personen ORDER BY nachname, vorname

SELECT id, nachname, vorname FROM personen

SELECT COUNT(*) FROM personen

SELECT COUNT(*) FROM personen WHERE geschlecht='f'
```

Link: <http://de.wikipedia.org/wiki/SQL>
