# BaseApp

## Situatie

Je werkt voor ACME. Ze hebben onlangs een todo-applicatie ontwikkeld. 
Je wordt gevraagd om een DevOps pipeline uit te werken. Hiervoor zal je op een remote Linux machine werken.

Er zijn twee onderdelen: Back-end en Front-end. Er is geen authenticatie.

De back-end is een NodeJs applicatie die de API host. De back-end luistert op poort 3000. 
De back-end draait standaard in-memory. Met andere woorden, de taken worden enkel opgeslagen in geheugen, niet op disk. 
De back-end kan ook een connectie maken naar een mysql databank. Die stel je in met volgende environment variabelen:

* STORAGE=mysql
* MYSQL_HOST=<hostname>
* MYSQL_USER=<username>
* MYSQL_PWD=$mysqlpwd 
* MYSQL_DB=$mysqldb

De Front-end is een HTML5 statische applicatie en luistert op poort 80. 
Via AJAX calls wordt de API aangeroepen. De front-end en de API moeten op dezelfde host draaien. 
De API draait in een subfolder /api.

## Architectuur

![Architectuur](./netwerkschema.jpeg)

## Opdracht:

1. Clone deze repository.
1. Bouw een image voor de back-end. De back-end draait op NodeJS. Je maakt gebruik van de node:23-bullseye base image. Een container op basis van deze image kan je op zichzelf uittesten.
1. Bouw een image voor de front-end. De front-end draait op Nginx. Je maakt gebruik van de nginx:1.27.2-alpine base image. De configuratie voor nginx vind je in de code repository. Een container op basis hiervan kan je pas uitvoeren na een kleine aanpassing in het configuratiebestand.
1. Maak een Docker Compose file aan die deze containers refereert. Expose je front-end op poort 80.
1. Voer Docker Compose uit en kijk of je de website kan opstarten.
1. Voeg MySQL toe aan je netwerk d.m.v. een Docker container. Je maakt gebruik van de mysql:8.4.3 base image. Voeg bind mounts toe zodat je data bewaard blijft.
1. De repository bevat een bestand init.sql. Zorg dat dit wordt uitgevoerd bij de start van de Mysql container. Check hiervoor de uitleg op Docker Hub rond het opstarten van een nieuwe instantie.
1. Configureer de API zodat die deze MySql databank gebruikt.
