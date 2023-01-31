**Übung 24**: Keine Doppelungen in deiner Collection

Gegeben sei ein Array mit folgenden Elementen: ['eloquent','laravel','laravel','collection','collection','model','migration','eloquent','collection','php','php','php']. 

Erstelle eine Collection und filtere alle Elemente, sodass jedes doppelte Element entfernt wird. 

Des Weiteren sollen alle Elemente vollständig großgeschrieben sein.

**Lösung:**

Lösung in tinker(live) oder in einer Closure-Route(web.php):


```


use Illuminate\Support\Collection;

$collect = collect(['eloquent','laravel','laravel','collection','collection','model','migration','eloquent','collection','php','php','php']);

var_dump($collect);

$ergebnis = $collect->unique()->map(function($item){ return strtoupper($item);}  ) ;  
var_dump($collect);

// Das Ergebnis entsteht in 2 Schritten:
//
// 1.Schritt: entfernen der doppleten Einträge(unique)
//
// 'eloquent','laravel','collection','model','migration','php'
//
// 2.Schritt: neue Zuordnung der verbliebenen Elemente mit map (update mit einer Zuordnungslogik)
// hier: ändere die verbliebenen Elemente mit strtoupper(), also GROSSBUCHSTABEN 
//
// das sind :

/*
Illuminate\Support\Collection {#4337
     all: [
       0 => "ELOQUENT",
       1 => "LARAVEL",
       3 => "COLLECTION",
       5 => "MODEL",
       6 => "MIGRATION",
       9 => "PHP",
     ],
   }
*/
```
