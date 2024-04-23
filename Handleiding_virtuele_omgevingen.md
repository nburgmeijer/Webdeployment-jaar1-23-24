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

4. Vervang de inhoud van config met het volgende, waarbij {X} je groepnummer is
```
Host group{X}-terminal.webdeployment.nl
ProxyCommand C:\Program Files (x86)\cloudflared\cloudflared.exe access ssh --hostname %h
```

5. Nu kan je een SSH connectie maken met de server met het volgende commando, waarbij {X} je groepnummer is
   - waarschijnlijk krijg je de melding dat de host nog niet bekend is en of je wil doorgaan met de aangegeven key fingerprint)
   - Type dan 'y' of ' yes'
   - Het standaard wachtwoord van de server is: 12345 
```
ssh ict@group{X}-terminal.webdeployment.nl
```

Nu zitten we in de zogenaamde shell van de linux server. 

![image](https://github.com/nburgmeijer/Webdeployment-jaar1-23-24/assets/31646458/2f360baa-bdcb-41f7-9f7d-9392847aba0c)

6. Om er voor te zorgen dat niet iedereen toegang heeft tot jullie server, gaan we het wachtwoord veranderen. Met het volgende commando in de shell
   Sla dit wachtwoord ergens veilig op!!!
```sh
passwd
```
