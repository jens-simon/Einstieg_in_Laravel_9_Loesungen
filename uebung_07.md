
**Übung 7**: Der Query-String entscheidet über den Ausgang der Anfrage

Erstelle eine Closure Route, die die URI routinglaravel.test/question handhabt. Abhängig von Parametern im Query-String soll eine Ausgabe wiedergegeben werden. Die entsprechenden Anforderungen habe ich dir aufgelistet.

Packe das Bild Success.png in deinem Laravel-Projekt in den Pfad ./public/assets/image/Success.png



  1. Wenn keine »id« vorhanden ist oder die »id« null ist, soll eine Fehlermeldung mit einem HTTP-Statuscode 404 zurückgegeben werden.
  
  2. Wenn der Parameter »file« true ist, also nicht null oder false, soll das Bild Success.png heruntergeladen werden. Der Name der Datei soll der Wert des »id«-Parameters + die Endung .png sein. Die Parameter »question« und »id« dürfen ebenfalls nicht null sein.
    
  3. Wenn die »question« nicht vorhanden ist, soll auf die Seite der Akademie "https://www.webmasters-fernakademie.de/" weitergeleitet werden. Die »id« soll aber vorhanden sein.
    
  4. Wenn die »question« sowie die »id« vorhanden sind, soll ein kleiner individueller Text wiedergegeben werden. Dieser soll bestätigen, dass die Frage gespeichert wurde. Der Statuscode soll 200 sein.

Prüfe mit den nachfolgenden URLs, ob deine erwartete Ausgabe wiedergegeben wird.

    http://routinglaravel.test/question?question=Warum%20ist%20die%20Erde%20rund?&id=3&file=false
    
    http://routinglaravel.test/question?question=Warum%20ist%20die%20Erde%20rund?
    
    http://routinglaravel.test/question?question=Warum%20ist%20die%20Erde%20rund?&id=3&file=true
    
    http://routinglaravel.test/question?id=3&file=false
    

**Hinweis:**

Das Bild befindet sich im Download-Link im Tutorial/WBT!
Es muss in den Ordner:
/public/assets/image/Success.png


**Lösung:**




1. in web.php

/routes/web.php
```

/* 
	uebung_07
	
*/ 
use Symfony\Component\HttpFoundation\Response;
use Illuminate\Http\Request;

Route::get('question', function (Request $request) {

  if (!$request->filled('id')) { // keine id! url 1.
	  
    return response('Ein Fehler ist aufgetreten, da keine id übergeben wurde', Response::HTTP_NOT_FOUND);
  
  } elseif ($request->filled(['id', 'question']) && $request->file === "true") { // id, questeion file=true url 2.
  
    $id = $request->id;
    $newname = $id . ".png";
	
    return response()->download('assets/image/Success.png', $newname);
 
 } elseif ($request->has('id') && !$request->filled('question')) { // id, keine question url 3.

	return redirect()->away('https://www.webmasters-fernakademie.de');

 } elseif ($request->filled(['id', 'question']) && $request->file !== "true") { // id,question, file=false url 4.

	return "Ihre Frage wurde erfolgreich gespeichert.";	
 }	
 
});

```



**Test:**


// routen anschauen:

php artisan route:list

// urls aufrufen:

Prüfe mit den nachfolgenden URLs, ob deine erwartete Ausgabe wiedergegeben wird.

http://routinglaravel.test/question?question=Warum%20ist%20die%20Erde%20rund?

http://routinglaravel.test/question?question=Warum%20ist%20die%20Erde%20rund?&id=3&file=true
	
http://routinglaravel.test/question?id=3&file=false

http://routinglaravel.test/question?question=Warum%20ist%20die%20Erde%20rund?&id=3&file=false
