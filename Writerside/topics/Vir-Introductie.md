# Introductie

**Waarom VM's** gebruiken?
- **Veiligheid**
    - Als één gehacked wordt is het lastiger om verder te geraken.
- **Meerdere services** op **één PC** draaien.
- Als één **VM crasht** gaat **niet alles plat**.

**VMs vs Containers:**
- **VM's:** Virtualizeren een hele machine, **insclusief hardware**. Draaien daarboven nog een OS.
- **Containers:** Virtualizeren **alleen** bijvoorbeeld een **service / applicatie**.

**Containers** zijn dus **meer lightweight** dan VM's.

## Podman vs Docker

**Allebei containertechnologie.**

**Voordelen van Podman:**
- **Daemonless**
    - Geen aparte daemon nodig om te runnen: meer lightweight en secure
- **Rootles** container
    - Docker runt als root
- Is **compatibel met docker**
- Podman biedt de mogelijkheid om **containers samen te laten werken**
    - kan bijvoorbeeld 2 of meer containers een netwerk laten delen
- **Integratie met systemd**
    - containers zijn services (en dus geen daemon nodig)

## Podman

**Image:** Voorgemaakte applicatie.

### Voorbeeld: nginx

Container image downloaden:
```
$ podman image pull docker.io/library/nginx:latest
```

Images listen
```
$ podman image ls
```

IP van container achterhalen
```
$ nmcli device show ens160 | grep 'IP4.ADDRESS’
```

Container met webserver starten
```
$ podman run -d --name web -p 8080:80 nginx
```

*Webserver zou nu moeten draaien.*

Webserver stoppen
```
$ podman stop web
```

Webserver starten
```
$ podman start web
```

### Voorbeeld: podman coderen

Je kan met vele programmeertalen met docker werken.\
Dit voorbeeld is met Bash.

Maak een directory aan voor het voorbeeld
```
$ mkdir docker-linux
```

Maak een containerfile aan
```
$ touch docker-linux/Dockerfile
```

Inhoud van containerfile er in zetten
```
$ nano docker-linux/Dockerfile  

# Gebruik een officiële Fedora image als basis  
FROM fedora:latest  
# Stel werkdirectory in  
WORKDIR /app  
# Schrijf een shell commando dat "Hello, World" print  
CMD ["echo", "Hello, World"]
```

Naar het dir met het Dockerfile gaan
```
$ cd docker-linux/
```

Bouw de podman image met de naam hallo-test
```
~/docker-linux$ podman build -t hallo-test .
```

Images opvragen
```
~/docker-linux$ podman images
```

Run de container, maakt niet uit in welk dir je zit
```
$ podman run hallo-test
Hello, World
```

## Kubernetes

**Veel containers tegelijk beheren is lastig.**\
Je kan dit gemakkelijker maken via:
1. **Kubernetes**
    1. Wordt in de industrie gebruikt
2. Docker Swarm

**Kubernetes** wordt gebruikt voor het **automatiseren van deployment, scaling en management van containers**.

**Kubernetes:**
- Runs en manages containers over verschillende machines.
- Zet automatisch containers aan of uit afhankelijk van de load.
- Herstart en vervangt kapotte containers.
- Doet aan load balancing, deelt het traffic over de containers
- updates de containers zonder downtime

**Belangrijke concepten:**
- **Pods:** een groep van één of meer containers
- **Nodes:** Machines waar pods op draaien
- **Clusters:** Groepen van nodes die samen beheerd worden
- **Services:** Zorgen dat pods netwerk resources hebben
- **Deployments:** Beheren hoe je containers worden deployed of geüpdate

## Legacy applicaties vs microservices

Vroeger moest een applicatie / service plat gelegd worden voor een update omdat de applicatie / service één groot executable is.

Tegenwoordig bestaat een applicatie / service uit meerdere kleine delen genaamd microservices. Zo moet maar een klein deel tijdelijk plat gelegd worden voor een update.
