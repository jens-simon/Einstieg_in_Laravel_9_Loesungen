**Übung 5**: Von der Closure Route zur Controller Action

Wähle die Route /name/{name}/nachname/{nachname} und /user/{name?} aus und packe die jeweiligen Closures in Controller Actions.

Die Controller Actions kannst du beliebig benennen. 

Nutze die Controller Actions dann als Callback im Routing. 

Die Parameter sollten übergeben werden. 

Der Parameter $name in der Route /user/{name?} soll optional sein.

**Hinweis:**

Routen werden von Hand gecodet,
Controller können mit artisan erstellt werden!
Eine leere neue Klasse wird erstellt, die Methoden müssen wieder von Hand gecodet werden !

**Lösung:**

1. wenn der Controller noch NICHT EXISTIERT!!!

mit artisan einen Controller erstellen:

php artisan make:Controller TestController


2. es entsteht die Datei:
App\Http\Controllers\TestController.php

```
<?php
// diese Datei wurden mit:
// php artisan make:Controller TestController erstellt

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class TestController extends Controller
{
  // uebung_05
  
  public function showName($name,$nachname) {
        return "Der übergebene Name lautet: ".$name." ".$nachname;
  }
  
  public function showUserName($username=null) {
        return "Der username lautet: ".$username;
  }
}

```

3. in web.php 2 routes erstellen, die den Controller benutzen:

/routes/web.php
```
/* 
	uebung_05
	
	zuerst muessen die beiden Methoden im Controller erstellt werden, erst dann koennen die routes diese benutzen!
	
	php artisan route:list
	
	URL: http://routinglaravel.test/name/jens/nachname/simon
		 http://routinglaravel.test/name/kim/nachname/schmitz
		 http://routinglaravel.test/name/nachname/
		 http://routinglaravel.test/name/jens/nachname/
		 http://routinglaravel.test/name/jens/nachname
		 	 
		 
	URL: http://routinglaravel.test/user/jens
		 http://routinglaravel.test/user/
		 http://routinglaravel.test/user
*/ 

Route::get('/name/{name}/nachname/{nachname}','TestController@showName');	
Route::get('/user/{name?}','TestController@showUsername');
```



**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/name/jens/nachname/simon

http://routinglaravel.test/name/kim/nachname/schmitz

http://routinglaravel.test/name/nachname/

http://routinglaravel.test/name/jens/nachname/

http://routinglaravel.test/name/jens/nachname

		 	 
http://routinglaravel.test/user/jens

http://routinglaravel.test/user/

http://routinglaravel.test/user

