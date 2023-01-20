**Übung 11**: Anhand von Nutzerdaten entscheiden wir über die Farbigkeit der Nutzer in der Namensliste

Nutze die im Begleitmaterial enthaltenen vorgegebenen Nutzerdaten. Du kannst sie in deinen Controller kopieren. 

Erstelle dann eine neue Action in unserem Controller CertificateController 
und registriere die Action mit einer neuen Route.

Als Wiedergabewert der Action soll eine View genutzt werden. 
Die View musst du ebenfalls erstellen. 

Die Nutzerdaten sollen als Parameter an die View weitergegeben werden.

Erstelle eine Schleife, die über alle Elemente iteriert. 
Mithilfe einer Kontrollstruktur soll geprüft werden, 
ob die jeweilige Person älter oder jünger als 18 ist und ob sie eine Telefonnummer hat. 

Es soll als Wiedergabe immer der Name und die E-Mail-Adresse in der jeweiligen Farbe angezeigt werden.

    Alter < 18 und keine Telefonnummer => grün
    Alter =18 und keine Telefonnumer => blau
    Alter < 18 und Telefonnummer => rot
    Alter = 18 und Telefonnummer => magenta

```

<?php

$users = [

            [

            'name' => 'Cathy Gleichner',

            'email' => 'Cristobal_Volkman89@hotmail.com',

            'phone' => '1-102-339-0647 x06086',

            'age' => '14',

          ],

          [

            'name' => 'Rashad Bartoletti',

            'email' => 'Josephine70@gmail.com',

            'age' => '23',

          ],

          [

            'name' => 'Anabel Crooks',

            'email' => 'Lambert.Braun38@hotmail.com',

            'phone' => '1-455-074-9861 x97241',

            'age' => '56',

          ],

          [

            'name' => 'Ova Howe',

            'email' => 'Diego_Turner@yahoo.com',

            'age' => '4',

          ],

          [

            'name' => 'Loy Balistreri',

            'email' => 'Emily.Senger68@hotmail.com',

            'age' => '87',

          ],

          [

            'name' => 'Tamia Parisian',

            'email' => 'Arlie77@gmail.com',

            'phone' => '633.048.2602',

            'age' => '13',

          ],

          [

            'name' => 'Demario Boehm',

            'email' => 'Annie.MacGyver@yahoo.com',

            'phone' => '258.282.8669 x9776',

            'age' => '35',

          ],

          [

            'name' => 'Tianna Jacobi I',

            'email' => 'Elliot32@hotmail.com',

            'age' => '43',

          ],

          [

            'name' => 'Rosemary Heidenreich',

            'email' => 'Cornelius.King23@hotmail.com',

            'phone' => '638-129-2815 x184',

            'age' => '54',

          ],

          [

            'name' => 'Jonas Gaylord',

            'email' => 'Wilburn14@yahoo.com',

            'phone' => '(348) 253-3467 x129',

            'age' => '49',

          ],

          [

            'name' => 'Juanita Luettgen PhD',

            'email' => 'Kaelyn_Predovic@hotmail.com',

            'phone' => '(229) 085-6914',

            'age' => '27',

          ],

          [

            'name' => 'Ms. Dedrick Quigley',

            'email' => 'Brandi.Glover@gmail.com',

            'phone' => '184.536.7463 x687',

            'age' => '32',

          ],

          [

            'name' => 'Britney Upton',

            'email' => 'Lela_Labadie@hotmail.com',

            'phone' => '1-684-898-5084 x7777',

            'age' => '61',

          ],

          [

            'name' => 'Alysha Stamm',

            'email' => 'Jacinto.Langosh@gmail.com',

            'phone' => '559.743.3564',

            'age' => '36',

          ],

          [

            'name' => 'Jonas Cummings',

            'email' => 'Stephania.Ebert65@gmail.com',

            'phone' => '254-084-9491 x8652',

            'age' => '19',

          ],

          [

            'name' => 'Esther Tromp',

            'email' => 'Baylee22@yahoo.com',

            'phone' => '1-039-607-9412 x0385',

            'age' => '72',

          ],

          [

            'name' => 'Wilhelm Ullrich',

            'email' => 'Norene.Hartmann@hotmail.com',

            'phone' => '(559) 229-9496',

            'age' => '93',

          ],

        ];

?>

```

alternativer Link zu den Nutzerdaten:

https://gist.github.com/Cosnavel/9328849e064a8ca74bdfccabff6fb13a

BASIERT AUF ÜBUNG 10!!!!

VORSICHT: im Lösungsvideo hat der Autor kein vollständiges HTML-Grundgerüst in das Template gesetzt ,
das funktioniert natürlich trotzdem. Hier in der Lösung ist das Tempate vollständig (siehe unten)!

**Lösung:**

1. in routes/web.php eine neue Route anlegen:

```

// uebung_11
// http://routinglaravel.test/users
// sollte vor den resource-Route kommen!!!
Route::get('users','CertificateController@showUser');


```

2. im CertificateController

```
// uebung_11
    public function showUser() {
       
	   $users = [

            [

            'name' => 'Cathy Gleichner',

            'email' => 'Cristobal_Volkman89@hotmail.com',

            'phone' => '1-102-339-0647 x06086',

            'age' => '14',

          ],

          [

            'name' => 'Rashad Bartoletti',

            'email' => 'Josephine70@gmail.com',

            'age' => '23',

          ],

          [

            'name' => 'Anabel Crooks',

            'email' => 'Lambert.Braun38@hotmail.com',

            'phone' => '1-455-074-9861 x97241',

            'age' => '56',

          ],

          [

            'name' => 'Ova Howe',

            'email' => 'Diego_Turner@yahoo.com',

            'age' => '4',

          ],

          [

            'name' => 'Loy Balistreri',

            'email' => 'Emily.Senger68@hotmail.com',

            'age' => '87',

          ],

          [

            'name' => 'Tamia Parisian',

            'email' => 'Arlie77@gmail.com',

            'phone' => '633.048.2602',

            'age' => '13',

          ],

          [

            'name' => 'Demario Boehm',

            'email' => 'Annie.MacGyver@yahoo.com',

            'phone' => '258.282.8669 x9776',

            'age' => '35',

          ],

          [

            'name' => 'Tianna Jacobi I',

            'email' => 'Elliot32@hotmail.com',

            'age' => '43',

          ],

          [

            'name' => 'Rosemary Heidenreich',

            'email' => 'Cornelius.King23@hotmail.com',

            'phone' => '638-129-2815 x184',

            'age' => '54',

          ],

          [

            'name' => 'Jonas Gaylord',

            'email' => 'Wilburn14@yahoo.com',

            'phone' => '(348) 253-3467 x129',

            'age' => '49',

          ],

          [

            'name' => 'Juanita Luettgen PhD',

            'email' => 'Kaelyn_Predovic@hotmail.com',

            'phone' => '(229) 085-6914',

            'age' => '27',

          ],

          [

            'name' => 'Ms. Dedrick Quigley',

            'email' => 'Brandi.Glover@gmail.com',

            'phone' => '184.536.7463 x687',

            'age' => '32',

          ],

          [

            'name' => 'Britney Upton',

            'email' => 'Lela_Labadie@hotmail.com',

            'phone' => '1-684-898-5084 x7777',

            'age' => '61',

          ],

          [

            'name' => 'Alysha Stamm',

            'email' => 'Jacinto.Langosh@gmail.com',

            'phone' => '559.743.3564',

            'age' => '36',

          ],

          [

            'name' => 'Jonas Cummings',

            'email' => 'Stephania.Ebert65@gmail.com',

            'phone' => '254-084-9491 x8652',

            'age' => '19',

          ],

          [

            'name' => 'Esther Tromp',

            'email' => 'Baylee22@yahoo.com',

            'phone' => '1-039-607-9412 x0385',

            'age' => '72',

          ],

          [

            'name' => 'Wilhelm Ullrich',

            'email' => 'Norene.Hartmann@hotmail.com',

            'phone' => '(559) 229-9496',

            'age' => '93',

          ],

        ];
        
        return view('show_user', compact('users')); 

    }
```


3. in resources/views

show_user.blade.php , die Datei manuell anlegen!

```
<html>
    <head>
 
    </head>

    <body>

		<h1>Nutzer mit Alter and Telefon</h1> 
		<ul>
			@foreach ($users as $user) 

				@switch($user)

				@case( $user['age'] < 18 && !isset($user['phone']) )
					<li style="color: green">{{$user['name']}}  
						<small>{{$user['email']}}</small>
					</li> 
					@break

				@case( $user['age'] >= 18 && !isset($user['phone']) ) 
					<li style="color: blue">{{$user['name']}}  
						<small>{{$user['email']}}</small>
					</li> 
					@break
				
				@case( $user['age'] < 18 && isset($user['phone']) )
					<li style="color: brown">{{$user['name']}}
						<small>{{$user['email']}}</small>
					</li> 
					@break
				
				@case( $user['age'] >= 18 && isset($user['phone']) )
					<li style="color: magenta">{{$user['name']}} 
						<small>{{$user['email']}}</small>
					</li> 
					@break
			
				@endswitch 

			@endforeach 

		</ul> 

    </body>

    
</html>
/*@extends('layouts.app')

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
@endsection	*/

```


**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/users

