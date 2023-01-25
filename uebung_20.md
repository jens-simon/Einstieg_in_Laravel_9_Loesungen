**Übung 20**: Erstelle Model für Artikel und Interessen - Eloquent Model keine Fashionmodel

Du wirst zu Anfang dieser Lektion die CRUD-Operationen mit Eloquent lernen und diese üben. 

Erstelle dazu ein Model mit dem Namen Article sowie eine zugehörige Migration. 

Die bereits vorhandene Tabelle interests soll ebenfalls als Model verfügbar sein. Erstelle in der Migration für die Articles folgende Spalten:

    interest_id
    title
    text

Die ID sowie die Timestamps sollten schon vorhanden sein. 

Du brauchst diese also nicht neu hinzuzufügen. 

Die Spaltentypen sowie Indexe und Attribute kannst du selbstständig setzen.


**Lösung:**

1. Zur interests-Migration ein Modell erstellen:

```
    php artisan make:model Interest
    
```
es entsteht im Ordner app die Datei Interest.php

**Hinweis:**

Bezeichnung von Models

Namen für Models im Singular und großgeschrieben, sie enthalten keine Leerzeichen und enden NICHT auf Model.

Beispiel: User, Interest, Post, usw. 

Diese Schreibweise nennt man Pascal Case.


2. ein Model 'Article' und die dazugehörige Migration 'articles' erstellen:
```

    php artisan make:Model Article -m
    
```

-m erstellt die dazugehoerige Migrationsdatei!


3. in der Migrationsdatei für die articles im database/migrations Ordner die up()-Methode anpassen:

```
public function up()
		{
			Schema::create('articles', function (Blueprint $table) {
				$table->bigIncrements('id');
				$table->string("title");
				$table->text('text');
				$table->integer('interest_id')->nullable();
				$table->timestamps();
			});
		}
```    

4. alles migirieren mir dem artisan
```
	php artisan migrate
    
    oder
    
	php artisan migrate:fresh    
```

**Test:**

mit phpMyAdmin oder mysql nachschauen, ob die beiden Tabellen
articles und interests da sind und entsprechend aufgebaut sind.
