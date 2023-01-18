**Übung 6**: Wir erstellen Zertifikate

Erstelle die Resource Certificate und nutze die Methoden 
create, store, show und destroy 
und gib bei jeder Action einen kurzen Text wieder. 

Benenne die create-Action mit dem Namen certify.

**Hinweis:**

Routen werden von Hand gecodet,
Resource Controller können mit artisan erstellt werden!

Eine neue Klasse mit vorgegebenen Standard Methoden(alle leer!) wird erstellt,
die Methoden müssen dann von Hand gecodet werden !

// ohne jegliche Methode (leer!)

php artisan make:controller TestController

// ein Resource Controller mit leeren Standard-Methoden

php artisan make:controller ControllerName --resource 

**Lösung:**

1. wenn der Controller noch NICHT EXISTIERT!!!

mit artisan einen Resource Controller erstellen:

php artisan make:Controller CertificateController --resource


2. es entsteht die Datei:
App\Http\Controllers\CertificateController.php

```
<?php
/*
    uebung_06
	
	dieser Controller wurde mit 
	
	php artisan make:controller CertificateController --resource
	
	erstellt!
*/	
	
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class CertificateController extends Controller
{
    public function index()
    {
        //
    }

    public function create()
    {
        // uebung_06
        return "Zertifikat erstellen";
    }

   
    public function store(Request $request)
    {
        //
    }

    public function show($id)
    {
        // uebung_06
        return "Zertifikat mit ID: ".$id;
    }

    public function edit($id)
    {
        //
    }
  
    public function update(Request $request, $id)
    {
        //
    }
    
    public function destroy($id)
    {
        //
    }
   
}

```

3. mehrere Methoden des Controllers sollen Texte ausgeben(return)!

4. in web.php, im routing, sollen die erlaubten Methoden angegeben werden! mit except()

/routes/web.php
```
/* 
	uebung_06
	
	zuerst den Controller mit:

	php artisan make:controller CertificateController --resource
	
	erstellen!
	
	dann muessen die beiden Methoden im Controller nach Wunsch auscodiert werden!
	
	dann die routen setzen, alle auf einen Schlag, mit Ausnahmen und mit alias fuer 'create'
	
	php artisan route:list
	
	URL:
			http://routinglaravel.test/certificates/create 
			http://routinglaravel.test/certificates/123      show mit einer id kann auch text sein!?  
			http://routinglaravel.test/certificates/abc
	*/ 
	
Route::resource('certificates','CertificateController')->except(['index','edit','update'
])->names(['create' => 'certifikates.certify']);
```



**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/certificates/create 

http://routinglaravel.test/certificates/123      
show mit einer id kann auch text sein!?  

http://routinglaravel.test/certificates/abc
