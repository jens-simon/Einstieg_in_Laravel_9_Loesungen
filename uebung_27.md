**Übung 27**: Daten in der Session speichern

Speichere einen Artikel, der mit der Action show aufgerufen wird, in der Session. Lies diesen aus, indem du in der Action index den zuletzt aufgerufenen Artikelnamen anzeigst.

**Lösung:**

1. 

in der bereits vorhanden view welcom.blade.php folgende Änderung einfügen:

```

  <h3>Letzer Artikel: {{$article}}</h3>

```


2. 
in der web.php die nachfolgende route anlegen bzw. ändern, wenn diese schon vorhanden ist, also **Vorsicht**, die darf nicht dopplet existieren!:


```

Route::get('/', function () {
    $article = session()->get('article',"----");
    return view('welcome',compact('article'));
});

``` 

3.

in der web.php die nachfolgende routes anlegen:


```
Route::get('article/create/{title}/{text}/', function($title,$text){

    $article = new Article;

    $article->title = $title;
    $article->text = $text;
   // $article->interest_id = $interest_id;

    $article->save();

    return "Artikel erstellt!";
});


Route::get('article/create/{title}/{text}/{interest_id}/', function($title,$text,$interest_id){

    $article = new Article;

    $article->title = $title;
    $article->text = $text;
    $article->interest_id = $interest_id;

    $article->save();

    return "Artikel erstellt!";
});

Route::get('article/show/{id}',function($id){
    $article = Article::find($id);
    dump($article->title);
    session(['article' => $article->title]);
	
	  dump(session()->get('article'));
	
    return $article;
});

```



**Test:**

Ale Artikel und Interessen vorher löschen(in der Datenbank)!

http://routinglaravel.test

http://routinglaravel.test/article/create/Titel/Bescheibung

http://routinglaravel.test/article/show/1

