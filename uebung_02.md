**Übung 2**: Was ist der Name?

Bitte füge eine Route für die URL routinglarave.test/name/nachname hinzu. Es sollen die Parameter $name und $nachname übergeben werden. Die beiden Parameter sollen notwendig und nicht optional sein. Anschließend sollen die beiden Parameter ausgegeben werden.

**Lösung:**

In routes/web.php eine Closure-Route einfuegen:

```
/* 
	uebung_02
	
	eine GET-Route 
	URL: http://routinglaravel.test/name/jens/nachname/simon
	URL: http://routinglaravel.test/name/kim/nachname/schmitz
	
*/ 
Route::get('/name/{name}/nachname/{nachname}',function($name,$nachname){
    return "Der übergebene Name lautet: ".$name." ".$nachname;
});

```


**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/name/jens/nachname/simon

http://routinglaravel.test/name/kim/nachname/schmitz

http://routinglaravel.test/name/nachname/schmitz

http://routinglaravel.test/name/jens/nachname


