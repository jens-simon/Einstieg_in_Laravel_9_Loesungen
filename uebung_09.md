
**Übung 9**: Eine Namensliste in deiner View wiedergeben

Erstelle eine Custom Action in unserem CertificateController.

Diese Action soll nameList() heißen.

Weise der Custom Action eine Route zu. 

Im Controller soll ein Array mit mindestens zehn Namen erstellt werden. 

Erstelle eine View mit einem beliebigen Namen und gib die Variable des Arrays an die View weiter. 

In der View erstellst du einen foreach loop und gibst die Namen in einer unordered list (ul) aus.

**Lösung:**

1. im Certificates Controller in app/Http/Controllers aus Übung 6 und 8

```
public function create()
{

/*
    // uebung_06
    return "Zertifikat erstellen";
*/

    // uebung_08
    return view('create_certificate'); // hier wird die View gerendert!!! die muss auch so heissen
  
}

// uebung_09
public function nameList() {
    $names = ['Andrea','Ben', 'Charlie', 'Kyle', 'Bob', 'Ryan', 'Nick', 'Moritz', 'Lisa', 'Amanda', 'Chris'];

    return view('show_names', compact('names')); 
}

```

2. in der web.php

```

/* uebung_09
  sollte vor der resource-Route-Methode kommen!!!
*/
Route::get('names','CertificateController@nameList');

```


3. in resources/views

show_names.blade.php VON HAND anlegen!!!

```
<html>
    <head>
 
    </head>

    <body>

      <h1>Namen Übung_09</h1>

      <ul>
      <?php
      foreach($names as $name)  {
        echo '<li>'.$name.'</li>';
      }    
      ?>    
      </ul>
    </body>

</html>

```


**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/names

