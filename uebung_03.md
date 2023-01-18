**Übung 3**: Auch Routes können Spitznamen haben

Erstelle eine Route und weise ihr einen optionalen Parameter sowie einen Nickname zu. 
Lass dir dann alle erstellten Routes anzeigen.


**Lösung:**

In routes/web.php eine Closure-Route einfuegen:

```
/* 
	uebung_03
	
	eine GET-Route 
	URL: http://routinglaravel.test/user
	URL: http://routinglaravel.test/user/jens
	
	das Fragezeichen hinter dem name-Parameter erlaubt diese auch wegzulassen (optional) ohne Fehlermeldung!!
	
	username ist ein interner nickname, den man per URL nicht ansprechen kann
	
	anzeige aller routes ueber das Terminal mit:
	
	php artisan route:list
*/ 
Route::get('/user/{name?}',function($name=null){
    return "Name=".$name;
})->name('username');

```


**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/user

http://routinglaravel.test/user/jens

http://routinglaravel.test/user/anne

