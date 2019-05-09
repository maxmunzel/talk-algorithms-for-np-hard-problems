% Einführung und Definitionen 
% Caspar Nagy 
% 13. Mai 2019 

## Gliederung

* Motivation
* Definitionen

# Motivation 

## Motivation – Wo wir bei TGI stehen geblieben sind

Viele Interessante Probleme $\in NP$

  * Löungen für \textsc{Bar Fight Prevention} (aka \textsc{Vertex Cover}) schon für $n=1000$ sehr unhandlich
  * Laufzeit kann drastisch reduziert werden, wenn wir den Lösungsraum einschränken 

Frage: 

  * Für welche Problem/Parameter-Paare ist das möglich?
  * Welche Laufzeit kann man mit Parametriesierung erreichen?

# Definitionen

## Definitionen

Parametriesiertes Problem

* $(X,k) \in \Sigma^{*} \times \mathbb{N}$, wobei $X$ die Instanz unseres Problems und $k$ die unäre Kodierung unseres Parameters ist. $*$ 

FPT (Fixed Parameter Tractable)

* Menge der parametrierten Probleme, für die ein Algorithmus $\mathcal{A}$ existiert, der Instanzen in Zeit $f(k) \cdot |(x,k)|^{c}$ entscheidet.

XP (slice-wise polynomial) 

* Menge der parametrierten Probleme, für die ein Algorithmus $\mathcal{A}$ existiert, der Instanzen in Zeit $f(k) \cdot |(x,k)|^{g(k)}$ entscheidet.



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
