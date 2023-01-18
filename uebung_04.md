**Übung 4**: Auch der Controller möchte die Welt begrüßen

Erstelle einen Controller mit dem Namen TestController sowie der Action printMessage() und verknüpfe diese Methode als Callback-Funktion mit der zuvor erstellten Route /helloworld. 

Gib im Controller den Text "Hallo Welt wie geht es dir?" wieder.

**Hinweis:**

Routen werden von Hand gecodet,
Controller können mit artisan erstellt werden!
Eine leere neue Klasse wird erstellt, die Methoden müssen wieder von Hand gecodet werden !

**Lösung:**

1. mit artisan einen Controller erstellen:

```

php artisan make:Controller TestController

```

**Hinweis:**

Bezeichnung von Controllern

Namen für Controller im Singular und großgeschrieben, sie enthalten keine Leerzeichen und enden auf Controller.

Beispiel: UserController, AuthController, RoleController, InterestConroller, PostController, usw. 

Diese Schreibweise nennt man Pascal Case.



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
	  // uebung_04
    
    // diese Methode muss von Hand gecodet werden, Teil der eigentlichen Aufgabe
    public function printMessage(){
        return "Hallo Welt, wie geht es Dir? Diesmal aus dem TestController ;-)";
    }
}

```

3. in web.php eine route erstellen, die den Controller benutzt:

/routes/web.php
```
/* 
	// uebung_04
	
	zuerst muss der Controller erstellt werden, erst dann kann die route diesen benutzen!

	eine GET-Route 
	URL: http://routinglaravel.test/helloworld
	
	Der Output kommt nun nicht mehr aus einer Closure von dieser Datei (function(){ return 'output';}
	
	Sondern ueber eine Umleitung zur Methode des Controllers!

	
	php artisan route:list

	
	*/ 
	
Route::get('/helloworld','TestController@printMessage');
```



**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/helloworld
