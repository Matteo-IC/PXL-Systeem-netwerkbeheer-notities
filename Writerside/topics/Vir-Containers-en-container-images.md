# Containers en container images

## Podman en Docker commando's

**Podman** en **Docker** gebruiken grotendeels **dezelfde commando's**.\
Hieronder een overzicht van de meest gebruikte commando's:

```
login <registry>       # Inloggen bij een container registry
pull <image>           # Download een container image

images                 # Toon alle gedownloade images
ps                     # Toon alle draaiende containers
ps -a                  # Toon alle containers (ook gestopte)

run <image>            # Start een container van een image
run -d <image>         # Start een container in de achtergrond
run -it <image>        # Start een container in interactieve modus
exec <container> <cmd> # Doe commando in actieve container
exec -it <container> <cmd> # Doe commando in actieve container en 
                             interactieve modus

start <container>      # Start een gestopte container
stop <container>       # Stop een draaiende container
rm <container>         # Verwijder een gestopte container

load -i <file> <image> # Laad een image vanuit een tar-bestand
save -o <file> <image> # Sla een image op als een tar-bestand
commit <container> <new_image> # Maak een nieuwe image van een container

logs <container>       # Toon de logs van een container
image inspect <image>  # Toon informatie van een image
```

## Terminologie

- **SIGTERM**:
  - Een signaal dat naar een proces wordt gestuurd en vraagt of die kan afsluiten.

- **SIGKILL**:
  - Een signaal dat een proces onmiddellijk stopt, het proces kan dan niet proper afsluiten.
    Wordt meestal gedaan als een proces niet reageert op SIGTERM.

### Verschil ubi10 en ubi10-init

- **ubi10:**
  - Bevat alleen de minimale benodigdheden om een container te draaien.
  - Start **geen init-proces**, dus processen in de container moeten zelf hun signalen afhandelen.
  - SIGTERM wordt vaak genegeerd.
- **ubi10-init:**
  - Bevat **een init-proces** dat als eerste wordt gestart in de container.
  - Dit init-proces zorgt ervoor dat processen in de container correct worden beheerd.
  - Het init-proces zorgt ervoor dat signalen zoals SIGTERM correct worden afgehandeld.

## Containerfiles

Een **Containerfile** (ook wel Dockerfile genoemd) is een **tekstbestand** dat **instructies bevat** om een **container image te bouwen**.

### Hoe gebruiken

1. **Maak een bestand** genaamd `Dockerfile` aan.
   1. Kan anders heten, maar dan moet je dat meegeven in volgende stappen.
2. **Schrijf de instructies** in het bestand.
3. **Bouw het image** met het commando.

### Instructies

- `FROM <image>`: **Bepaalt het basisimage** voor de container.
- `RUN <command>`: **Voert een commando uit** tijdens het bouwen van het image.
- `COPY <source> <destination>`: **Kopieert bestanden** van de **host naar de container**.
- `CMD ["executable", "param1", "param2"]`: Bepaalt het **standaardcommando** dat wordt **uitgevoerd wanneer een container wordt gestart**.
  - **Behalve wanneer een ander commando wordt opgegeven** bij het starten van de container.
- `ENTRYPOINT ["executable", "param1", "param2"]`: Bepaalt het **standaardcommando dat altijd wordt uitgevoerd** wanneer een container wordt gestart.
  - Extra parameters kunnen worden toegevoegd bij het starten van de container.





