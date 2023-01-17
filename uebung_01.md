**Übung 1**: Hallo Welt wie geht es dir?

Erstelle eine Route für die URL http://routinglaravel.test/helloworld

und gib beim Aufruf den Text "Hallo Welt wie geht es Dir?" wieder.

Dazu musst du in der Datei web.php eine neue Route mit der Methode get hinzufügen.

**Lösung:**

In routes/web.php eine Closure-Route einfuegen:

```
/* 
	uebung_01

	eine GET-Route 
	URL: http://routinglaravel.test/helloworld

*/ 
Route::get('/helloworld',function(){
    return "Hallo Welt, wie geht es Dir?";
});

```


**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/helloworld
