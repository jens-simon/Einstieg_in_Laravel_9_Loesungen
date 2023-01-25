
**Übung 19**: Die Posts und der Query Builder

Langsam geht es ans Eingemachte!
Wir werden die Daten und Tabellen aus der vorherigen Übung jetzt richtig bearbeiten.

Du sollst die Aufgabe möglichst effizient und mit der passendsten Methode lösen. Ein wichtiger Punkt ist dabei: 
Es gibt bei den meisten Aufgaben nicht die eine perfekte Lösung, manche Lösungen sind aber eleganter. Viele Wege führen nach Rom. Solange die Abfragen bei dir das erwünschte Resultat erfüllen, gilt die Aufgabe als bestanden. 

Probiere ruhig aus. Falls du alle Daten löschst oder die Tabelle crasht, kannst du mit php artisan migrate:fresh und dem Code der vorherigen Aufgabe den alten Stand wiederherstellen.

Versuche möglichst alle Aufgaben zu lösen. 
Lasse dir die Variablen mit 

var_dump() , 
dd() oder 
ddd() ausgeben

und prüfe das Ergebnis.

1. Erstelle eine Abfrage, die alle Posts auswählt. Speichere diese Abfrage in einer Variable, sodass wir diese mehrfach verwenden können. Diese Variable werden wir für die anderen Aufgaben nutzen, um den Code nicht immer neu zu schreiben (Query Chaining).

2. Gib die Gesamtzahl der Posts aus.

3. Füge einen beliebigen Post mit dem Query Builder hinzu.

4. Aktualisiere den Text eines Posts, dessen »id« zwischen 6 und 10 ist und keine »interest_id« hat, auf "neuer Text".

5. Gib für den Post mit der »id« 1 das Erstelldatum aus.

6. Frage alle Posts ab und sortiere die »id« absteigend. Die Posts ohne »text« und ohne »interest_id« sollen nicht ausgegeben werden.

7. Lösche alle Posts, die keine »interest_id« oder »text« haben.

**Lösung:**

In einer Closure-Route in web.php

```


/* 
	uebung_19
	
	Verschiedenen Unteraufgaben durchführen:


	nicht im InterestController das ist unschön ;-)
*/
Route::get('uebung_19', function() {
	
	//Aufgabe 1
	$posts = DB::table('posts');

	//Aufgabe 2
	$count_posts = $posts->count();
	var_dump($count_posts);

	//Aufgabe 3
	DB::insert('insert into posts (title, text) value (?,?)', ['uebungsaufgabe', 'das ist schoen']);

	//Aufgabe 4
	$update = $posts->whereBetween('id', [6, 10])->whereNull('interest_id')->update(['text' => 'neuer Text']);
	var_dump($update);

	//Aufgabe 5
	$created = $posts->whereId(1)->value('created_at');
	var_dump($created);

	//Aufgabe 6
	$order_posts = $posts->whereNotNull(['text', 'interest_id'])->orderBy('id', 'desc')->get();
	var_dump($order_posts);

	//Aufgabe 7
	$deleted = $posts->whereNull('text')->orWhereNull('interest_id')->delete();
	var_dump($deleted);
});

```



**Test:**

http://routinglaravel.test/uebung_19

```
int(11)
int(1)
NULL
object(Illuminate\Support\Collection)#1343 (1) {
  ["items":protected]=>
  array(0) {
  }
}
int(1)

```
prüfe die beiden Tabellen posts und interests, fällt dir etwas auf?
```
mysql> SELECT * FROM posts;

mysql> SELECT * FROM interests;
```
