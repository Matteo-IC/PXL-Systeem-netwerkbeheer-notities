# Containers en container images

## Podman commando's

```
$ podman login <registry>       # Inloggen bij een container registry
         pull <image>           # Download een container image
         
         images                 # Toon alle gedownloade images
         ps                     # Toon alle draaiende containers
         ps -a                  # Toon alle containers (ook gestopte)
         
         run <image>            # Start een container van een image
         run -d <image>         # Start een container in de achtergrond
         run -it <image>        # Start een container in interactieve modus
         exec <container> <cmd> # Doe commando in actieve container
         exec -it <container> <cmd> # Doe commando in actieve container
                                      en interactieve modus

         start <container>      # Start een gestopte container
         stop <container>       # Stop een draaiende container
         rm <container>         # Verwijder een gestopte container
         
         load -i <file> <image> # Laad een image vanuit een tar-bestand
         save -o <file> <image> # Sla een image op als een tar-bestand
         
         logs <container>       # Toon de logs van een container
         image inspect <image>  # Toon informatie van een image
```
