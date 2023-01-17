**Übung 0: Installation Vagrant/Homestead/Laravel**

1.
VirtualBox - Installation

https://www.virtualbox.org/

Eventuell Neustart durchführen!

2.
Vagrant Installation

https://www.vagrantup.com/

Eventuell Neustart durchführen!

3.
Installation von Homestead im Homeverzeichnis von Windows (c:\users\student\) :

In einem Terminalfenster(Eingabeauforderung,CMD oder Powershell)
folgendes Command im **Homeverzeichnis** ausführen:

Anmerkung: sollte Git nicht installiert sein, dieses vorher installieren:


https://git-scm.com/download/win


```
git clone --branch v13.0.0 https://github.com/laravel/homestead.git Homestead
```


4.
Homestead initialisieren:

```
init.bat
```
oder in Powershell:
```
./init.bat
``` 

5.
Homestead.yaml bearbeiten

C:/Users/student mit dem eigenen Homeverzeichnis ersetzen

Die Sites und deren Benennungen gegebenenfalls anpassen!


```
---
ip: "192.168.10.10"
memory: 2048
cpus: 2
provider: virtualbox

authorize: C:/Users/student/.ssh/id_rsa.pub

keys:
    - C:/Users/student/.ssh/id_rsa

folders:
    - map: C:/Users/student/Homestead/code
      to: /home/vagrant/code

sites:
    - map: routinglaravel.test
      to: /home/vagrant/code/routinglaravel/public
         
databases:
    - routinglaravel

    
features:
    - mysql: true
    - mariadb: false
    - postgresql: false
    - ohmyzsh: false
    - webdriver: false

#services:
#    - enabled:
#        - "postgresql@12-main"
#    - disabled:
#        - "postgresql@11-main"

ports: 
#    - send: 4040
#      to: 4040
#    - send: 5432 # PostgreSQL
#      to: 54320
#    - send: 8025 # Mailhog
#      to: 8025
#    - send: 9600
#      to: 9600
#    - send: 27017
#      to: 27017
```

6. 
Den Unterordner code anlegen:

``` 
PS C:\Users\student\Homestead> mkdir code
```

7. 
Die ssh-Keys erstellen:

Führe in der CMD den folgenden Befehl aus: 

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Gib bei der Datei in der die Keys gespeichert werden sollen .ssh/id_rsa an.

Drücke bei der Aufforderung einen Passphrase anzugeben zwei mal Enter.

Der SSH Key sollte gespeichert worden sein. 


8.
Vagrant starten!

```
vagrant up
```

9.
Bei Änderungen in der .yaml Datei:

```
vagrant reload --provision
```

10.
In der Windows hosts Datei in c:\windows\system32\drivers\etc

diesen Eintrag hinzufügen:

```
192.168.10.10 routinglaravel.test
```

http://routinglaravel.test

geschafft!
