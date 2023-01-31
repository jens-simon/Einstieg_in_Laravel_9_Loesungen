**Übung 26**: Sinnfreie Übungsfactory

Erstelle eine Factory für die Artikel. Der Titel soll ein Stadtname und der Text eine IBAN sein. Ja ich weiß, das macht inhaltlich wenig Sinn.


**Lösung:**

1.

Factory für Artikel erstellen mit 

Stadtname und IBAN


```

php artisan make:factory ArticleFactory 

```

in database/factories/ wird ArticleFactory.php angelegt!


2. Die return Werte anpassen:

```
$factory->define(App\Article::class, function (Faker $faker) {
    return [
        //
        'title'=> $this->faker->city() ,
        'text' => $this->faker->iban() ,
        
    ];
});
``` 

3.

in tinker (php artisan tinker) fake-Daten erzeugen:

```

factory(App\Article::class, 5)->create();

```

**Test:**
in der Datenbank die erzeugten Adressen ansehen (mysql oder phpMyAdmin)

EIn Beispiel mit dem Seeder

4.

```

php artisan make:seeder MeinTestSeeder


```

eine Seeder Class in in databases/seeders/MeinTestSeeder.php entsteht!

5.

hierin die run()-Methode anpassen:

```

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Str;

class MeinTestSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        //
        DB::table('articles')->insert([
            'title' => Str::random(10),
            'text' => Str::random(50),
        ]);
    }
}

```

6.
und mit dem artisan Befehl ausprobieren:

```

php artisan db:seed MeinTestSeeder

```

**Test:**

```

Vollständige Texte 	id	title	text	interest_id	created_at	updated_at 	
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	1 	LaravelCRUD 	CreatReadUpdateDelete 	1 	2021-08-09 12:11:22 	2021-08-09 12:11:22
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	2 	Politik 	Umwelt ist toll Wirtschaft aber auch 	2 	2021-08-09 12:11:41 	2021-08-09 12:11:41
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	3 	LaravelCRUD 	CreatReadUpdateDelete 	4 	2021-08-09 12:11:53 	2021-08-09 12:11:53
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	4 	gyvwjgqZIX 	U5TtNNiacBUBYG534gSvm5Dwsb8x7jRXWTscTb1HwVEXfGmBH0 	NULL 	NULL 	NULL
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	5 	31AeZ0X02E 	0fPhI0zL7FRBdaRxjLfjSW9Iq4rzBaq4eCPfjFtK6VsO4amKdJ 	NULL 	NULL 	NULL
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	6 	fRR1RBF1b3 	dQmo6BRrnKJ8zb1XiBXTcPVMh2HIBqa71YNN6CjNDA2ok83xsq 	NULL 	NULL 	NULL
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	7 	uNxBOh8Mrz 	yphoTeqHXev7H3euoP4OG5GKstYXDw034C5NgKLxrs9F6tF8lO 	NULL 	NULL 	NULL
	Bearbeiten Bearbeiten 	Kopieren Kopieren 	Löschen Löschen 	8 	qx0d2aoO7G 	2NrNPNigUWoqvCFrltMJtNg9nEqZ5828cXNLxGtNQ0xcIF2rLf 	NULL 	NULL 	NULL 

```
