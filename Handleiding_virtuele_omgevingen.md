# Handleiding virtuele omgevingen
##### Webdeployment HBO-ICT jaar 1 2023-2024

## Inleiding.

Voor het project Webdeployment krijgt iedere groep een eigen virtuele linux omgeving (hierna genoemd server) waar de web applicatie die ontwikkeld wordt als docker container deployed kan worden. 
Deze omgeving is van buitenaf bereikbaar en bevat de volgende opties.

-	Een MySql server 
> intern bereikbaar op localhost:3306
-	Een webbased Filebrowser om files vanuit een webbrowser over te kunnen zetten naar de server
> group{x}-files.webdeployment.nl
-	Een webbased database administratie tool voor visuele administratie van de MySql server
> group{x}-database.webdeployment.nl
-  localhost:8080(intern andres van de webapplicaties straks) is te bereiken op
>group{x}.webdeployment.nl

\* {x} = je groupnummer

## Secure Shell

Om toegang te krijgen tot de CLI(command line interface) van de server gaan we een SSH(secure shell) connectie maken met de server.
Doorloop de volgende stappen om vanaf het internet een SSH connectie te kunnen maken.

##### WINDOWS

1. Start bij voorkeur Powershell. En anders command prompt(cmd.exe)
2. Installeer de cloudflare connector. Deze zorgt ervoor dat je de connectie van buitenaf met de server kan maken
```ps
winget install --id cloudflare.cloudflared
```

2. Ga naar de .shh directory
```ps
cd .ssh
```

3. Voor het volgende uit om notepad te openen voor de file config 
```ps
notepad config
```

4. Vervang de inhoud van config met het volgende, waarbij {x} je groepnummer is (bijvoorbeeld group12-terminal.webdeploy)
```
Host group{x}-terminal.webdeployment.nl
ProxyCommand C:\Program Files (x86)\cloudflared\cloudflared.exe access ssh --hostname %h
```

5. Nu kan je een SSH connectie maken met de server met het volgende commando, waarbij {x} je groepnummer is
   - waarschijnlijk krijg je de melding dat de host nog niet bekend is en of je wil doorgaan met de aangegeven key fingerprint)
   - Type dan 'y' of ' yes'
   - Het standaard wachtwoord van de server is: 12345 
```
ssh ict@group{x}-terminal.webdeployment.nl
```

Nu zitten we in de zogenaamde shell van de linux server. 

![image](https://github.com/nburgmeijer/Webdeployment-jaar1-23-24/assets/31646458/2f360baa-bdcb-41f7-9f7d-9392847aba0c)

6. Om er voor te zorgen dat niet iedereen toegang heeft tot jullie server, gaan we het wachtwoord veranderen. Met het volgende commando in de shell
   Sla dit wachtwoord ergens veilig op!!!
```sh
passwd
```
#### MacOs
>Volgt

<br/>

## Filebrowser

Mocht het nodig zijn om files over te zetten naar de server dan kan dit via de webbased filebrowser.
Deze kan je bereiken op het volgende adres, waarbij {x} je groepnummer is.
```
https://group{x}-files.webdeployment.nl
```

De standaar login is:
Username: admin
Password: admin

Het wachtwoord kan je aanpassen in de webinterface.

![alt text](image.png)

## MySql Server en phpMyAdmin

Op de server is een docker container actief met daarin een MySql server. Deze server is bereikbaar via localhost of 127.0.0.1 op poort 3306 (standaard poort voor database connecties)

#### ConnectionString
Maak gebruik van de volgende connectie string om vanuit C# Blazor connectie te maken:

```csharp
"Server=localhost;port=3306;Database={database naam};Uid=root;Pwd=Test@1234!"
```

#### phpMyAdmin
Je kan deze database server managen via een webbased adminstratietool genaamd phpMyAdmin.
Deze kan je bereiken op het volgende adres, waarbij {x} je groepnummer is
```
group{x}-database.webdeployment.nl
```

De standaard login voor de database is net zoals in periode 3:

Username: root
Password: Test@1234!

Je kan het wachtwoord veranderen door boven op de pagina op Server: 127.0.0.1 te klikken en dan op change password:

![alt text](image-2.png)

## Standaard docker containers

Voor het volgende commando uit in de shell van de server om te zien welke docker containers momenteel actief zijn

```
docker ps
```
![alt text](image-1.png)


##### We zien hier 3 containers n.l:

- nginx: Een webserver op poort 8080 die je kan bereiken op onderstaand adres, waarbij {x} je groepsnummer is:
(deze staat hier tijdelijk zodat je kan zien dat je webapplicatie straks bereikbaar is op poort 8080)
```
group{x}.webdeployment.nl 
```
- filebrowser: De filebrowser applicatie
- mysql: de mySql Server
- phpmyadmin: Database administratie tool

# Belanrijke informatie

- Tussen 2:00 uur en 2:30 uur 's nachts wordt van elke omgeving een backup gemaakt. De server wordt dan een paar minuten in een soort stop staat gezet. Op dat moment is de server niet beschikbaar.
- Laat de containers die draaiden toen je voor het eerst inlogde met rust! Met uitzondering van de nginx container. Deze wordt ook vervangen door een container met jullie webapplicatie
- Mocht er onverhoopt iets verkeerd gaan stuur dan een mail naar. 

nick.burgmeijer@nhlstenden.com


Mogelijkheden zijn:

    - wachtwoord vergeten, dan kan je een wachtwoord reset vragen
    - er is iets mis met de mysql, filebrowser of phpMyAdmin containers
    - je server is gecrashed

Dan is er de mogelijkheid om eventeel een verse omgeving aan te vragen of een eerder backup te herstellen (let op: de laatste 2 backups worden bewaard!)