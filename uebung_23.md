**Übung 23**: Collections mit Multiplikation und Division filtern und bearbeiten

Erstelle eine Collection aus dem Array [1,2,3,4,5,6,7,8,9] 

und multipliziere alle Werte, die durch drei teilbar sind mit 9. 

Das Ergebnis sollte folgendermaßen aussehen: [27,54,81]


**Lösung:**

Lösung in tinker(live) oder in einer Closure-Route(web.php):


```

use Illuminate\Support\Collection;

// Das Array wird in eine Collection überführt
$collect = collect([1,2,3,4,5,6,7,8,9]);
var_dump($collect);

// Die neue Ergbnis Collection wird in 2 Schritten gebildet:
//
// 1.Schritt: filter (where Bedingung)
// hier: wähle alle Elemente deren Modulus 3 Wert 0 ist.
//
// das sind : 3,6 und 9
//
// 2.Schritt: neue Zuordnung der verbliebenen Elemente mit map (update mit einer Zuordnungslogik)
// hier: ändere die verbliebenen Elemente mit *9
//
// das sind : 9,54 und 81
//

$ergebnis = $collect->filter(  

	function ($item) {
		return $item % 3 === 0;
	}

) ->map(


	function ($item) {
		return $item * 9;
	}

);

var_dump($ergebnis);
/*
object(Illuminate\Support\Collection)#3710 (1) {
  ["items":protected]=>
  array(3) {
    [2]=>
    int(27)
    [5]=>
    int(54)
    [8]=>
    int(81)
  }
}
*/

```
