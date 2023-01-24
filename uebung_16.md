
**Übung 16**: Migriere deine Migrations

Führe die Migration in deiner Vagrant Box aus. 



**Lösung:**

```

php artisan migrate

```



**Test:**

im MySql Server des Linux(Vagrant)-Systems gibt es nun einige Tabellen in der routinglaravel Datenbank: 

```

vagrant ssh

mysql -u homestead
secret

USE routinglaravel;

SHOW TABLES;

DESCRIBE posts;

DESCRIBE interests;

```

Vorsicht: eventuell gab es einen Fehler in der .env Datei!
