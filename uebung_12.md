
**Übung 12**: Mithilfe von Blade Templates und Semantic UI sorgst du für eine hübschere Namensliste

Jetzt sollst du dein erstes Template erstellen. Dazu nutzen wir die View aus Übung 11 sowie die Controller Action und die registrierte Route.

Erstelle ein Layout mit dem Namen app.blade.php. In dieses Layout importierst du im Head-Abschnitt Semantic UI. Dafür kopierst du folgende zwei Tags: 

```
<link

  rel="stylesheet"

  href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.css"

  integrity="sha256-9mbkOfVho3ZPXfM7W8sV2SndrGDuh7wuyLjtsWeTI1Q="

  crossorigin="anonymous"

/>

<script

  src="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.js"

  integrity="sha256-t8GepnyPmw9t+foMh3mKNvcorqNHamSKtKRxxpUEgFI="

  crossorigin="anonymous"

></script>

```


Anschließend legst du eine Section fest, in der unser Inhalt der Nutzerdaten angezeigt wird. 

Zudem erstellst du eine View mit einem Header und bindest diesen im Layout ein. 

Die Schleife mit den Bedingungen kannst du übrigens entfernen. 

Deine View aus Übung 11 soll das erstellte Layout erweitern. 

Die Nutzerdaten gibst du in schönerer Darstellung aus.


Damit du den gesamten Inhalt schöner darstellen kannst, empfehle ich dir, das gerade eingebundene Semantic UI zu nutzen. Semantic UI ist ähnlich wie Bootstrap ein UI Framework. Mithilfe dessen lassen sich Nutzerinterfaces ziemlich schnell erstellen, ohne viel CSS schreiben zu müssen. Die einzelnen Komponten können über ihre Klassen genutzt werden. Die verfügbaren Komponenten sowie verschiedene Klassen kannst du der Dokumentation entnehmen. Diese ist unter folgendem Link aufrufbar: https://semantic-ui.com/introduction/getting-started.html


BASIERT AUF ÜBUNG 11!!!!

**Lösung:**

1. in resources/views

show_user.blade.php , die Datei verändern aus Übung 11!

```
@extends('layouts.app')

@section('content')
	<div class="ui grid">
	@foreach($users as $user)
		<div class="four wide column">
			<div class="ui card"> 
				<div class="content"> 
					<p class="header">{{$user['name']}} </p>
					<div class="description"> {{$user['email']}} <br> Alter: {{$user['age']}}
					</div>
					@isset($user['phone'])
					<div class="extra content">
						<a>
							<i class="phone icon"></i>
							{{$user['phone']}}
						</a>
					</div>
					@endisset
				</div>
			</div>
		</div>
	@endforeach
	</div>
@endsection	

```

2. in resources/views/layouts, den Ordner layouts bitte von Hand anlegen!

app.blade.php , die Datei neu erstellen!

```

<html>
	<head>
		<title>Blade Templates</title>
		<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.css"
			  integrity="sha256-9mbkOfVho3ZPXfM7W8sV2SndrGDuh7wuyLjtsWeTI1Q="
			  crossorigin="anonymous" />

		<script src="https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.js"
				integrity="sha256-t8GepnyPmw9t+foMh3mKNvcorqNHamSKtKRxxpUEgFI="
				crossorigin="anonymous"	>
		</script>

	</head>
	
	<body>
		@include('layouts.header')
		
		<div class="ui container">
			@yield('content')
		</div>
		
	</body>
</html>

```

2. in resources/views/layouts, den Ordner layouts bitte von Hand anlegen!

header.blade.php , die Datei neu erstellen!

```

<div class="ui secondary menu">
	<a class="item">Blade Templates</a>
</div>

<div class="ui divider">

</div>

```

**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/users

