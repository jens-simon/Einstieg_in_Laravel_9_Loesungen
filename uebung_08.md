
**Übung 8**: Deine erste View

Erstelle für unsere Action create im CertificateController eine View mit beliebigem Namen und stelle den Text "Zertifikat erstellen" schöner dar.

BASIERT AUF Übung 6!!!!

**Lösung:**

1. im Certificates Controller in app/Http/COntrollers aus Übung 6

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
```

2. in resources/views

create_certificate.blade.php VON HAND anlegen!!!

```
<html>

    <head>
        <title>Zertifikat erstellen</title>
    </head>

    <body>

        <h1 style="color:blue">Zertifikat erstellen</h1>
	     
        <p style="color:green">hier kannst du ein Zertifikat erstellen</>
    
    </body>

</html>

```


**Test:**


// routen anschauen:

php artisan route:list

// url aufrufen:

http://routinglaravel.test/certificates/create

