# Handleiding virtuele omgevingen
##### Webdeployment HBO-ICT jaar 1 2023-2024

## Inleiding.

Voor het project Webdeployment krijgt iedere groep een eigen virtuele linux omgeving (hierna genoemd server) waar de web applicatie die ontwikkeld wordt als docker container deployed kan worden. 
Deze omgeving is van buitenaf bereikbaar en bevat de volgende standaardapplicaties:

-	Een MySql server
-	Een webbased Filebrowser om files vanuit een webbrowser over te kunnen zetten naar de server
-	Een webbased database administratie tool voor visuele administratie van de MySql server


## Secure Shell

Om toegang te krijgen tot de CLI(command line interface) van de server gaan we een SSH(secure shell) connectie maken met de server.
Doorloop de volgende stappen om vanaf het internet een SSH connectie te kunnen maken.

##### WINDOWS

1. Start bij voorkeur Powershell. En anders command prompt(cmd.exe)
2. Installeer de cloudflare connector. Deze zorgt ervoor dat je de connectie van buitenaf met de server kan maken
```sh
winget install --id cloudflare.cloudflared
```

2. Ga naar de .shh directory
```sh
cd .ssh
```

3. Voor het volgende uit om notepad te openen voor de file config 
```sh
notepad config
```

4. Vervang de inhoud van config met het volgende, waarbij {x} je groepnummer is
```shell
Host group4-terminal.webdeployment.nl
ProxyCommand C:\Program Files (x86)\cloudflared\cloudflared.exe access ssh --hostname %h
```