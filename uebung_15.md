
**Übung 15**: Die Posts sollen mithilfe von Interessen kategorisiert werden

Füge eine Migration mit dem Tabellennamen interests hinzu.

Diese Migration soll eine Spalte mit dem Namen "id" samt Autoincrement erstellen sowie eine Spalte mit dem Namen "text", in der eine Zeichenfolge mit mindestens 30 Zeichen gespeichert werden kann.

Es sollen außerdem die Timestamps für on_create und on_update gesichert werden können. 

Eine interest repräsentiert ein Interesse. 

Betrachte die Interessen einfach als Kategorien. 

Der Nutzer kann z. B. einen Post zu einem leckeren Rezept hinzufügen und diesen dem Interesse Kochen zuordnen. 

Zu dieser Beziehung kommen wir aber an späterer Stelle. 



**Lösung:**

```

php artisan make:migration create_interests_table

```


im Ordner /database/migrations wird eine neue Datei mit Zeitstempel angelegt!

Diese muss nun der Aufgabe entsprechend angepasst werden!!!

```

    public function up()
    {
        Schema::create('interests', function (Blueprint $table) {
			// uebung_15
            $table->id();
            $table->string('text',30);
            $table->timestamps();
            /*  // alternative 
            	$table->timestamp('created_at')->useCurrent();
            	$table->timestamp('updated_at')->useCurrent();
	    */
        });
    }

```


**Test:**

im Ordner /database/migrations wird eine Datei mit dem Namen

202y_mm_dd_hhmmss_create_interests_table.php 

angelegt.






