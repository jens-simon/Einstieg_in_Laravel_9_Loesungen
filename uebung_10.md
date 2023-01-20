
**Übung 10**: Weg von unschönem PHP, hin zu Blade Shortcuts

Baue den Code der Namensliste aus der Übung  9 des View-Abschnitts so um, 
dass du die Schleife mit Blade-Shortcuts realisierst und nur fünf Iterationen durchgeführt werden. 

http://routinglaravel.test/names

BASIERT AUF ÜBUNG 9!!!!

**Lösung:**

in resources/views

show_names.blade.php , die Datei erweitern aus Übung 9!

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
      
      <h1>Namen Übung 10</h1>
		  
      <ul>
		  @foreach($names as $name)  
			  @if ($loop->iteration > 5) 
				  @break;
			  @endif
			  <li>{{$name}}</li>   
		  @endforeach
		
      </ul>
    
    </body>

</html>

```


**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/names

