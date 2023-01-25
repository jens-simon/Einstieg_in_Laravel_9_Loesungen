**Übung 18**: Interessen und Posts für die spätere Benutzung hinzufügen

In dieser Lektion werden wir mit einigen Daten arbeiten. 

Deshalb ist es notwendig, dass wir zwei Migrations durchführen und die Tabellen mit Daten befüllen.

Zum einen nutzen wir die create_interests_table-Migration. 
Diese sollte aus einer der vorherigen Übungen schon bei dir vorhanden sein.
    
Zum anderen nutzen wir die Migration create_posts_table. 
Ersetze zuerst die up-Funktion der create_posts_table mit folgendem Code:

```

public function up()

{

    Schema::create('posts', function (Blueprint $table) {

        $table->increments('id');

        $table->string('title');

        $table->text('text')->nullable();

        $table->integer('interest_id')->nullable();

        $table->timestamps();

    });

}
```


Nachdem du dies getan hast, führe den Befehl 


```
php artisan migrate:fresh 
```
aus. 
Damit wir mit den gleichen Daten in den Übungen arbeiten, wäre es sinnvoll, deine Tabelle mit den vorgegebenen Daten zu befüllen. Erstelle dazu eine Controller Action oder eine Closure Route. Füge dort den nachfolgenden Code ein. Der Code befüllt die Tabellen »interests« sowie »posts«. Wie du schon siehst, habe ich jeweils ein Array mit Daten erstellt. Über beide Arrays iteriere ich mit einer foreach-Schleife. Mit der Funktion (object) werden die jeweiligen Nested Arrays als stdClass-Objekte verfügbar. Dadurch kann ich wie bei gewöhnlichen Objekten auf die Array-Parameter zugreifen. Die beiden Spalten created_at und updated_at werden mit der timestamp()-Methode in der Migration erstellt. Die Carbon-Bibliothek wird seit Laravel-Version 5.8 offiziell unterstützt. Sie bietet uns Zugriff auf erweiterte Date/Time Funktionen. Wir behandeln diese später noch genauer. In Eloquent werden »created_at« und »updated_at« automatisch befüllt. Wenn wir jedoch den Query Builder verwenden, müssen wir die beiden Spalten manuell befüllen. Die Methode now() von Carbon gibt einen aktuellen Timestamp wieder. Diesen fügen wir in unsere beiden Spalten ein.

```

$interestdata = [

[

'id' => 1,

'text' => 'Coding',

],

[

'id' => 2,

'text' => 'Kochen',

],

[

'id' => 3,

'text' => 'Singen',

],

[

'id' => 4,

'text' => 'Fußball',

],

];



foreach ($interestdata as $interest) {

    $interest = (object) $interest;

    DB::table('interests')->insert(

        ['text' => $interest->text, 'id' => $interest->id]

    );

}



$postdata = [

[

'id' => 1,

'title' => 'Montag',

'text' => 'Montag ist schön zum Fußball spielen',

'interest_id' => 4,

],

[

'id' => 2,

'title' => 'jeder Tag',

'text' => null,

'interest_id' => 1,

],

[

'id' => 3,

'title' => 'Dienstag',

'text' => 'Dienstag koche ich.',

'interest_id' => 2,

],

[

'id' => 4,

'title' => 'Mittwoch',

'text' => 'Mittwoch singe ich',

'interest_id' => 3,

],

[

'id' => 5,

'title' => 'Mittwoch',

'text' => 'Mittwoch ist schlechtes Wetter',

'interest_id' => null,

],

[

'id' => 6,

'title' => 'Donnerstag',

'text' => 'Donnerstag lerne ich den Query Builder',

'interest_id' => 1,

],

[

'id' => 7,

'title' => 'Essen',

'text' => 'Ich bin hungrig.',

'interest_id' => null,

],

[

'id' => 8,

'title' => 'Freitag',

'text' => null,

'interest_id' => 1,

],

[

'id' => 9,

'title' => 'Samstag',

'text' => 'Samstag koche ich.',

'interest_id' => 2,

],

[

'id' => 10,

'title' => 'Fußball',

'text' => null,

'interest_id' => 4,

],

[

'id' => 11,

'title' => 'Coding',

'text' => 'Laravel macht Spaß',

'interest_id' => null,

],

];



foreach ($postdata as $post) {

    $post = (object) $post;



    DB::table('posts')->insert(

        [

    'id' => $post->id,

    'title' => $post->title,

    'text' => $post->text,

    'interest_id' => $post->interest_id,

    'created_at' => \Carbon\Carbon::now(),

    'updated_at' => \Carbon\Carbon::now(),

]

    );

}

```


Alternativer Link zu den Daten: https://gist.github.com/Cosnavel/885b58d1e43afb5838d02bbf24ea4611




**Lösung:**

```
Route::get('uebung_18', function() {
	$interestdata = [
[
'id' => 1,
'text' => 'Coding',
],
[
'id' => 2,
'text' => 'Kochen',
],
[
'id' => 3,
'text' => 'Singen',
],
[
'id' => 4,
'text' => 'Fußball',
],
];

foreach ($interestdata as $interest) {
    $interest = (object) $interest;
    DB::table('interests')->insert(
        ['text' => $interest->text, 'id' => $interest->id]
    );
}

$postdata = [
[
'id' => 1,
'title' => 'Montag',
'text' => 'Montag ist schön zum Fußball spielen',
'interest_id' => 4,
],
[
'id' => 2,
'title' => 'jeder Tag',
'text' => null,
'interest_id' => 1,
],
[
'id' => 3,
'title' => 'Dienstag',
'text' => 'Dienstag koche ich.',
'interest_id' => 2,
],
[
'id' => 4,
'title' => 'Mittwoch',
'text' => 'Mittwoch singe ich',
'interest_id' => 3,
],
[
'id' => 5,
'title' => 'Mittwoch',
'text' => 'Mittwoch ist schlechtes Wetter',
'interest_id' => null,
],
[
'id' => 6,
'title' => 'Donnerstag',
'text' => 'Donnerstag lerne ich den Query Builder',
'interest_id' => 1,
],
[
'id' => 7,
'title' => 'Essen',
'text' => 'Ich bin hungrig.',
'interest_id' => null,
],
[
'id' => 8,
'title' => 'Freitag',
'text' => null,
'interest_id' => 1,
],
[
'id' => 9,
'title' => 'Samstag',
'text' => 'Samstag koche ich.',
'interest_id' => 2,
],
[
'id' => 10,
'title' => 'Fußball',
'text' => null,
'interest_id' => 4,
],
[
'id' => 11,
'title' => 'Coding',
'text' => 'Laravel macht Spaß',
'interest_id' => null,
],
];

foreach ($postdata as $post) {
    $post = (object) $post;

    DB::table('posts')->insert(
        [
    'id' => $post->id,
    'title' => $post->title,
    'text' => $post->text,
    'interest_id' => $post->interest_id,
    'created_at' => \Carbon\Carbon::now(),
    'updated_at' => \Carbon\Carbon::now(),
]
    );
}
	return "Wenn keine Fehler aufgetaucht sind, sind die Tabellen jetzt gefüllt!";
});

```

**Test:**

http://routinglaravel.test/uebung_18
	
```
mysql> SELECT * FROM posts;
+----+------------+----------------------------------------+-------------+---------------------+---------------------+
| id | title      | text                                   | interest_id | created_at          | updated_at          |
+----+------------+----------------------------------------+-------------+---------------------+---------------------+
|  1 | Montag     | Montag ist schön zum Fußball spielen   |           4 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  2 | jeder Tag  | NULL                                   |           1 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  3 | Dienstag   | Dienstag koche ich.                    |           2 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  4 | Mittwoch   | Mittwoch singe ich                     |           3 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  5 | Mittwoch   | Mittwoch ist schlechtes Wetter         |        NULL | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  6 | Donnerstag | Donnerstag lerne ich den Query Builder |           1 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  7 | Essen      | Ich bin hungrig.                       |        NULL | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  8 | Freitag    | NULL                                   |           1 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
|  9 | Samstag    | Samstag koche ich.                     |           2 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
| 10 | Fußball    | NULL                                   |           4 | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
| 11 | Coding     | Laravel macht Spaß                     |        NULL | 2021-11-15 21:43:24 | 2021-11-15 21:43:24 |
+----+------------+----------------------------------------+-------------+---------------------+---------------------+
11 rows in set (0.00 sec)

mysql> SELECT * FROM interests;
+----+----------+------------+------------+
| id | text     | created_at | updated_at |
+----+----------+------------+------------+
|  1 | Coding   | NULL       | NULL       |
|  2 | Kochen   | NULL       | NULL       |
|  3 | Singen   | NULL       | NULL       |
|  4 | Fußball  | NULL       | NULL       |
+----+----------+------------+------------+
4 rows in set (0.00 sec)

mysql>
```

