**Übung 25**: 

Zensur in deiner Applikation. Wir erlauben nur Laravel-Artikel

Um die Validerung kennenzulernen, erstelle eine View und nutze diese in deinem ArticleController als Wiedergabewert der Action create. 

In dieser View soll ein Formular vorhanden sein. 

Erstelle für das Formular eine Validierung. Erstelle eine neue Validierungsregel. 
Diese Regel soll validieren, ob der Titel des Artikels das Wort »Laravel« enthält. 
Beachte bei der Validierung das Error Handling. 

Wenn kein Fehler auftritt, kannst du in der store Action einen neuen Artikel erstellen.


**Lösung:**

0.a)

Vorarbeiten laut Skript Kapitel 18 Formulare

```

php artisan make:Controller ArticleController --resource

```

0.b)
im routing, web.php

```

// uebung_25 
// article Controller existiert jetzt alle routen erlauben!
Route::resource('article', 'ArticleController');

``` 

**Test:**
```
php artisan route:list
```
da sind sie!!!


1.
eine View für Artikel erstellen (als Datei von Hand!!)

article.blade.php

```
@if ($errors->any())

@foreach($errors->all() as $error)

{{$error}}

@endforeach

@endif

<form action="{{ route('article.store')}}" method="POST">
    @csrf 

    <input name="title" placeholder="Titel des Artikels" required >
    <input name="text" placeholder="Text für den Artikel" required >
    <input type="submit">

</form>
```
**Hinweis:**
Das Formular hat kein HTML-Grundgrüst, dieses wird aber vom Browser dynamisch ergänzt!
Es funktioniert also, aber ein gerüst um den Formular-Code wäre optimal!


2.
im ArticleController:

```
public function create()
 {
    // uebung_25
	return view('article');
 }
```

3. 
in web.php

```
// uebung_25
Route::resource('article','ArticleController');
```
**Test:**

http://routinglaravel.test/article/create


4. DIE VALIDIERUNG!!

Mit Webtools beide required Felder mal leern. dann abschicken!!!!
Jetzt kommt leerer Inhalt zum Server, der muss erkannt werden!!!!!!!

Im ArticleController.php:

```
	public function store(Request $request)
	{
        // uebung_25
		
		/* // simple Variante, hier deaktiviert
		 $request->validate(
		 [
            'title' => 'required',
            'text' => 'required'

        ]
		
		); */
		
		// komplexere Variante, hier aktiv!
		$request->validate([
			'title' => [ 
				'required',
				function($attribute, $value, $fail) {
					if (strpos($value,'Laravel') === false) {
						$fail($attribute.' enthält nicht den Text Laravel');
					}
				}
			],
			'text' => 'required'
		]);	
		
		Article::create($request->all());
		
		return "success - alles OK!";
		
		
    }
	
```


5. im Article.php Model:

```

<?php
namespace App;

use Illuminate\Database\Eloquent\Model;

class Article extends Model
{
    protected $fillable = ['title','text'];
}


```

6. noch verbessern mit einem ArticleRequest

```

   php artisan make:request ArticleRequest

```

in App\Http\Requests\ liegt nun ArticleRequest.php:

```
 public function authorize()
    {
        return true; //false;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            'title' => [ 
				'required',
				function($attribute, $value, $fail) {
					if (strpos($value,'Laravel') === false) {
						$fail($attribute.' enthält nicht den Text Laravel');
					}
				}
			],
			'text' => 'required'
            //
        ];
    }

```


Im ArticleController.php:

```
public function store(Request $request)
	
	use App\Http\Requests\ArticleRequest;
	
    public function store(ArticleRequest $request)
    {
        // uebung_25
		Article::create($request->all());
		
		return "success - alles OK!";
		
		
    }
```	
