**Übung 22**: Tags, verschlüsselte Likes und jede Menge Beziehungen

Erstelle ein Model sowie eine Migration für die Tags. 

Erstelle dann eine Many-To-Many-Beziehung zwischen den Interessen und den Artikeln 
sowie eine One-To-Many-Beziehung zwischen den Artikeln und den Tags. 

Jeder Tag soll bei Abruf aus der Datenbank großgeschrieben werden. 

Die Like-Anzahl der Artikel soll verschlüsselt in der Datenbank gespeichert werden. 

Das machen wir natürlich nur zu Übungszwecken. 

Im produktiven Einsatz würde man dies nicht machen, da die Like-Anzahl nicht sicherheitsrelevant ist. 

Außerdem sollen beim Abruf eines Artikels gleich alle Tags mitgeladen werden.

**Hinweis:**
Die Migrations und Models finden sich auf Niklas' Github-Repository

https://gist.github.com/Cosnavel/57bd108e9a65637258146a1ce739f680

**Vorsicht! Ein kleiner Fehler in Niklas' interests - Migration !!!**

Da 'use SoftDeletes;' im Model Interest definiert wurde, muss auch in der Tabelle interests ein solches deleted_at Attribut drin sein.

Also entweder 'use SoftDeletes;' entfernen/auskommentieren oder die migration muss so aussehen:
```
//interests migration 
Schema::create('interests', function (Blueprint $table) {
    $table->increments('id');
    $table->string('text', 30);
    $table->softDeletes(); // hinzufügen!!!!!
    $table->timestamps();
});

```


**Lösung:**

Ausprobieren mit Tinker !!

```
	php artisan tinker
```


a) Artikel erstellen (DIREKT IN DIE DATENBANK!)

<-- Tinker direkt Befehle: -->

```
$article = App\Article::create(['title' => 'eloquent', 'text' => 'likes müssen verschluesselt sein', 'likes' => 0]);


/* Ergebnis sollte sein:
=> App\Article {#4401
     title: "eloquent",
     text: "likes mssen verschluesselt sein",
     likes: "eyJpdiI6IjI3UmduUXhYUC9nQmhLYW05UEZqL1E9PSIsInZhbHVlIjoiYXM2SXhhNFVmSU9PNWhsWVk3OFFhdz09IiwibWFjIjoiNDBjYjc1NThmZjE4YTk4MzFhOGIxMTVlOTNlMDY1OTA4YTUxOTM5NmYzNWI5N2QzNGI0MDEyYzRjMDUxNTNmZSIsInRhZyI6IiJ9",
     updated_at: "2021-08-25 10:33:54",
     created_at: "2021-08-25 10:33:54",
     id: 1,
   }
   
in mysql oder phpMyAdmin prüfen!
*/
```   

b) Tags erstellen	

```
$article->tags()->create(['title' => 'geheim']);
/*
Ergebnis sollte sein:
=> App\Tag {#4403
     title: "geheim",
     article_id: 1,
     updated_at: "2021-08-25 10:49:18",
     created_at: "2021-08-25 10:49:18",
     id: 1,
}
in mysql oder phpMyAdmin prüfen!
*/
```
	
c) Artikel löschen, Tag wird automatisch geloescht!

```

$article->delete();
/*
in mysql oder phpMyAdmin prüfen!

*/
```


**Tests:**

alle Schritte in mysql oder phpMyAdmin prüfen!


**Alternative Befehle zum üben für die many-to-many und one-to-many Beziehungen als Route in der web.php**
```
use App\Article;
use Illuminate\Support\Facades\Route;
use Illuminate\Support\Facades\DB;
use App\Interest;
use App\Page;
use App\Post;
use App\Tag;


Route::get('test_m_n', function () {

	$article = Article::create(
		[
			'title' => 'Bilderrahmen',
			'text' => ' Dies ist ein schöner Bilderrahmen'
		],
	);

	$interest = Interest::create(
		[
			'text' => 'Malen',
		],
	);

	$article->interests()->attach($interest); // Beziehung in der pivot-Tavelle herstellen
	//$article->interests()->detach($interest); // Beziehung in der pivot-Tavelle loeschen
	
	echo "<h2>Artikel 1 und alle Interessen</h2>";
	$article = Article::first();
	dump($article);
	foreach ($article->interests as $interest) {
		dump($interest);
	}

	// Tag
    	$article->tags()->create(['title' => 'geheim']);

	echo "<h2>Artikel 1 und alle Tags</h2>";
	
	//$article = Article::first(); // lazy loading
	$article = Article::with('tags')->first(); // eager loading
	
	dump($article);
	foreach ($article->tags as $tag) {
		dump($tag);
	}
});
```

**Tests:**

alle Schritte in mysql oder phpMyAdmin prüfen!

http://routinglaravel.test/test_m_n
