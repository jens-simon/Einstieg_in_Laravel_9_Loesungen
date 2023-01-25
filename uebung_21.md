**Übung 21**: Kreatives Ausprobieren von Eloquent

Erstelle einige Artikel 
sowie dazugehörige Interessen.

Probiere 
 - die CRUD-Methoden 
 - sowie Mass Assignment, 
 - Soft Deleting 
 - und Sub Queries aus.

Deiner Kreativität sind keine Grenzen gesetzt.

**Hinweis:**
Die Übung 20 MUSS VORHER ausgeführt worden sein!


**Lösung:**

1. Alle Migrationsdateien abarbeiten

```
  php artisan migrate:fresh
    
```

2. Routes fuer create/read article und create/read interest vorbereiten in der /routes/web.php
```
/*
	uebung_21
	
	URLs zum Eintragen der Datensätze:

	http://routinglaravel.test/interest/create/Programmieren
	http://routinglaravel.test/interest/create/Lesen
	http://routinglaravel.test/interest/create/Politik
	http://routinglaravel.test/interest/create/Sport
	http://routinglaravel.test/interest/create/Gaming

	http://routinglaravel.test/article/create/LaravelCRUD/CreateReadUpdateDelete/1
	http://routinglaravel.test/article/create/Politik/Umwelt ist toll Wirtschaft aber auch/3
	http://routinglaravel.test/article/create/Formel1/Autorennen macht viel Spa? beim Zusehen/4

	URLs zum Ansehen der Datensätze:

	http://routinglaravel.test/articles
	http://routinglaravel.test/interests

	
	
*/
use App\Interest; 
use App\Article; 

// Artikel erstellen
Route::get('article/create/{title}/{text}/{interest_id}/', function($title,$text,$interest_id){

    $article = new Article;

    $article->title = $title;
    $article->text = $text;
    $article->interest_id = $interest_id;

    $article->save();
});

// Interessen erstellen
Route::get('interest/create/{text}', function($text){
    $interest = new Interest;

    $interest->text = $text;
  
    $interest->save();
});

// Artikel anzeigen
Route::get('articles', function(){
	$articles = Article::all();

	dd($articles);	
});

// Interessen anzeigen
Route::get('interests', function(){

	
	$interests = Interest::all();
	var_dump($interests);	
	

	/*
    // suchen nach ID
    $interests = Interest::findOrFail(1); // wird gefunden!
    //$interests = Interest::findOrFail(3443543); // wird nicht gefunden! 404
    var_dump($interests);
    */

    /*
    // suchen nach exaktem Text 
    $interests = Interest::whereText("Politik")->get(); // wird gefunden!
    // oder nur erstes, wenn mehrere!
    //$interests = Interest::whereText("Politik")->first();
    var_dump($interests);
    */

    /*
    // suchen , finden und Text aendern
    $interest = Interest::whereText("Politik")->first(); // geht nur einmal!! dann Fehler!
    $interest->text="Chillen";
    $interest->save();
    var_dump($interest);
    */

    /*
    // suchen , finden und loeschen (dauerhaft!!!/ richtiges DELETE FROM ....)
    $interest = Interest::whereId(3)->first();
    $interest->delete();
    var_dump($interest);
    */
});
```

**Hinweis:**
In der interests - Route sind mehrere Beispiel auskommentiert, diese bei Bedarf wieder aktivieren!

**Tests bis hierhin:**
URLs zum Eintragen der Datensätze:

http://routinglaravel.test/interest/create/Programmieren
	
http://routinglaravel.test/interest/create/Lesen
	
http://routinglaravel.test/interest/create/Politik
	
http://routinglaravel.test/interest/create/Sport
	
http://routinglaravel.test/interest/create/Gaming
	

http://routinglaravel.test/article/create/LaravelCRUD/CreateReadUpdateDelete/1
	
http://routinglaravel.test/article/create/Politik/Umwelt%20ist%20toll%20Wirtschaft%20aber%20auch/3
	
http://routinglaravel.test/article/create/Formel1/Autorennen%20macht%20viel%20Spaß%20beim%20Zusehen/4
	

URLs zum Ansehen der Datensätze:

http://routinglaravel.test/articles
	
http://routinglaravel.test/interests
	


3. softdeletes

a)
in  app\Interest.php

```
namespace App;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes; // uebung_21

class Interest extends Model
{
    use SoftDeletes; // uebung_21
}

```

b)
in der Interests_Migrations Datei sind keine SoftDeletes drin, also einfügen, mit einem artisan befehl oder manuell:

```

  php artisan make:migration add_softdeletes_to_interests_table 

```

c)
im Ordner database\migrations ensteht die Datei 202x....add_softdeletes_to_interests_table.php

```

public function up() {
        Schema::table('interests', function (Blueprint $table) {
            //
            // uebung_21
            $table->softDeletes(); // hinzufügen!!!!!
        });
}

```

d)
in der routes/web.php folgende Route hinzufügen:

```

Route:get('interests)
    // suchen , finden und loeschen (dauerhaft!!!/ richtiges DELETE FROM ....)
    $interest = Interest::whereId(3)->first();
    $interest->delete(); // softdelete!
    var_dump($interest);
    
	
```

e) 
Migrationen durchführen
```

  php artisan migrate

```

f)
```
/*
	jetzt nochmal was loeschen und drauf achten, deleted NULL nicht NULL!
	
	http://routinglaravel.test/interest/delete/1 oder 2 oder ...
	
	
*/

Route::get('interest/delete/{id}', function($id){
	$interest = Interest::whereId($id)->first();
    $interest->delete();
    var_dump($interest);

});
```

**Tests bis hierhin:**

http://routinglaravel.test/interest/delete/1

http://routinglaravel.test/interest/delete/2

Prüfen im phpMyAdmin!


g)
withTrashed / mit den soft gelöschten

```
// http://routinglaravel.test/interests/with_trashed

Route::get('interests/with_trashed', function(){
	$interests_trashed = Interest::withTrashed()->get();
    var_dump($interests_trashed);

});
```

**Tests bis hierhin:**

http://routinglaravel.test/interests/with_trashed


h)
// onlyTrashed  // trashed()/ nur die soft gelöschten
```
// http://routinglaravel.test/interest/only_trashed
Route::get('interests/only_trashed', function(){
	$interest = Interest::onlyTrashed()->get();
    var_dump($interest);
	
});
```

**Tests bis hierhin:**

http://routinglaravel.test/interests/only_trashed

i)
// bist du ein getrashtes Element? hole mich aus dem papierkorb mit restore()
// mit mysql oder phpMyAdmin prüfen ;-)

```
// http://routinglaravel.test/interest/is_trashed_then_restore
Route::get('interest/is_trashed_then_restore', function(){
	$interest = Interest::onlyTrashed()->first();
    
	$isTrashed = $interest->trashed();
	var_dump($isTrashed);
	if ($isTrashed) $interest->restore();
});	
```

**Tests bis hierhin:**

http://routinglaravel.test/interests/is_trashed_then_restore


4. mass assignment

Standardmässig DEAKTIVIERT, aber sicherheitsrelevant!!!
Im Model muss entweder 
	$fillable=[]; WhiteList für Spalten der Tabelle
oder 
	$guarded=[]; Blacklist für Spalten der Tabelle
genutzt werden !

Am Beispiel des Model Articles:

app\Articles.php

```
class Article extends Model
{
	....
	// uebung_21: Mass Assignment
	protected $fillable =['title','text']; // für beide Spalten müssen Inhalte angegeben werden bei einem INSERT
}
```


Wofür das alles?
---------------
die Methoden:
create()
update()
firstOrCreate()
firstOrNew()
verlangen das zwingend!!



// Artikel erstellen mit create() - MASS ASSIGNMENt im Model zwingend
// id is nullable, daher nicht nötig, text hat keinen default also nötig! title auch!
// http://routinglaravel.test/article/create_ma/Neuer%20Artikel/Der%0Artikel%20kann%20was
```
Route::get('article/create_ma/{title}/{text}', function($title,$text){

    Article::create( ['title' => $title, 'text' => $text]);

});
```

**Test bis hierhin:**

http://routinglaravel.test/article/create_ma/Neuer%20Artikel/Der%0Artikel%20kann%20was

5)
SUBQUERY Beispiel aus Tutorial! im Video ab 20:42
// Subquery aus Tutorial
// http://routinglaravel.test/subquery

```
Route::get('subquery', function(){

	$articles = Article::addSelect(['interest' => Interest::select('text')->whereColumn('id', 'interest_id')->limit(1)])->get();  
	dd($articles);
});
```

**Test bis hierhin:**

http://routinglaravel.test/subquery
