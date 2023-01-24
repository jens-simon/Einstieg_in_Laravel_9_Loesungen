**Übung 17**: Interessen, Datenbank und Controller

Erstelle einen Controller, um unsere Tabelle interests mit Daten zu befüllen.

Erstelle eine Action, die mit einer Abfrage alle Interessen wiedergibt.

Erstelle eine Action samt Raw SQL Query, mit der sich Interessen anhand der Route-Parameter erstellen lassen.

Erstelle eine Action samt Raw SQL Query, um einzelne Interessen zu löschen.

Registriere die drei Actions in Routes.


BASIERT AUF den Übungen 15 und 16!!!!


**Wichtig:** Es muss vorher migriert worden sein, da die Tabelle sonst nicht verfügbar ist.




**Lösung:**

1. Den InterestController mit artisan erstellen lassen:

```

php artisan make:controller InterestController

```
**Hinweis:**

Bezeichnung von Controllern

Namen für Controller im Singular und großgeschrieben, sie enthalten keine Leerzeichen und enden auf Controller.

Beispiel: UserController, AuthController, RoleController, InterestConroller, PostController, usw. 

Diese Schreibweise nennt man Pascal Case.

2.
Die Routes erstellen in der /routes/web.php:

```

/* 
	uebung_17
	
	URL:
	http://routinglaravel.test/interests
	
	http://routinglaravel.test/interests/create/1/Programmieren
	http://routinglaravel.test/interests/create/2/Chillen
	
	http://routinglaravel.test/delete/2
*/	

Route::get('interests','InterestController@index');
Route::get('interests/create/{id}/{text}','InterestController@create');
Route::get('interests/delete/{id}','InterestController@delete');

```

3. im Controller die Methoden ausprogrammieren:

```

<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use Illuminate\Support\Facades\DB;


class InterestController extends Controller
{
    // uebung_17
    public function index() { 
        //dump(DB::table('interests')->dump());
        //dump(DB::table('interests')->dd());
	//dump(DB::table('interests')->toSql());
        
		$interests = DB::select('select * from interests '); 
		return var_dump($interests); 
	}
	
	public function create($id, $text)  {
		DB::insert('insert into interests (id, text) values (:id, :text)' , ['id' => $id, 'text' => $text]);
	} 
	
	public function delete($id) {
		$removed = DB::delete('delete from interests where id = ?', [$id]); 
		return dd($removed); 
	}	
}

```

**Test:**

http://routinglaravel.test/interests
	
http://routinglaravel.test/interests/create/1/Programmieren

http://routinglaravel.test/interests/create/2/Chillen
	
http://routinglaravel.test/interests/delete/2
