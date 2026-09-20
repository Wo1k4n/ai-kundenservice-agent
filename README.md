# KI-Kundenservice-Agent

Viertes und bisher komplexestes Projekt. Ein Mini-Shop, bei dem Bestellungen 
in einer Datenbank landen, und ein KI-Agent, der Kunden eigenständig 
Auskunft über ihre Bestellung geben kann.

## Was das System macht

Auf der Shop-Seite wählt man ein Produkt, füllt Name und Email aus und 
bestellt. Die Bestellung landet automatisch in einer Supabase-Datenbank 
(PostgreSQL). Über die Chat-Seite kann man danach einen KI-Agenten fragen, 
z.B. "wo ist meine Bestellung" - der Agent durchsucht selber die 
Datenbank nach dem passenden Eintrag und antwortet mit den echten Daten.

Der Agent hat auch ein Gedächtnis: er merkt sich den bisherigen 
Gesprächsverlauf, man muss z.B. seinen Namen nicht in jeder Nachricht 
wiederholen.

Technisch ist das mein erstes Projekt mit n8n's AI Agent Node statt 
manuellen HTTP-Requests an die KI. Der Agent entscheidet selbst, wann er 
die Datenbank durchsucht (Tool-Use), statt dass ich das mit IF-Nodes 
fest vorgebe.

## Aufbau

Zwei n8n-Workflows:
- **Bestellung entgegennehmen** - nimmt Bestellungen vom Shop-Formular 
  entgegen und speichert sie in Supabase
- **Erster AI Agent Test** - der Chat-Agent mit Zugriff auf die Datenbank

Zwei Frontend-Seiten:
- **shop-bestellung.html** - Produktauswahl und Bestellformular
- **kundenservice-chat.html** - Chat mit dem KI-Agenten

## Verwendet

- n8n (inkl. AI Agent, Memory, Tool-Nutzung)
- Groq API (openai/gpt-oss-120b)
- Supabase (PostgreSQL-Datenbank)

## Zum Ausprobieren

Beide Workflows lassen sich in eine eigene n8n-Instanz importieren. Braucht 
einen eigenen Groq API-Key und eine eigene Supabase-Datenbank mit einer 
Tabelle "Bestellungen" (Spalten: kunde_name, email, produkt, status). 
In den HTML-Dateien müssen die jeweiligen Webhook-URLs angepasst werden.

## Was noch nicht so gut ist

- Der Agent kann Bestellungen nur nachschlagen, nicht ändern oder stornieren
- Keine Validierung im Bestellformular (z.B. ob die Email echt aussieht)
- RLS in Supabase ist aktiv, aber ohne eingerichtete Policies - funktioniert 
  nur, weil n8n über den Service Role Key zugreift

Mein bisher fortgeschrittenstes Projekt.
