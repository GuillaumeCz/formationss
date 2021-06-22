# Docker

## 01/06/12

Why docker ? Avant c'etait 1 serveur physique pour une app. Ce qui n'est absolument pas optimisé en terme de ressource / espace / ...

L'utilisation de VM a été une première solution. La conteneurisation est LA solution. 

VM: 
- Hyperviseur qui pop des OS complets (utilisation d'un kernel virtuel)
- Assez lourd, peu d'optimisation de ressources

Conteneurisation:
- Partage de ressources avec l'hôte (utilisation de son kernel)
- Seulement l'app avec "Support file runtime"

Docker / Podman / LXC sont 3 technos qui permettent de manipuler des conteneurs.

Docker --> Develop (Build) -> Deploy (Ship) -> Run.

Utilisable aussi bien en prod que pour le dev.

Les plus:
- Deploiement portable 
- Tout le monde à le même setup, peu importe l'hote. (pas de "ça marche chez moi, pas chez toi")
- Centré sur app (on peut négliger les dependances)
- Construction automatique avec Dockerfile
- Partage facile (juste un dockerfile à passer, pas un OS ENTIER)
- Versionnement possible (il ne s'agit que d'un Dockerfile)
- Ecosystème fournit --> Des tonnes de docker préconfigurés avec tout et n'importe quoi.

IMAGE !== CONTAINER

### Archi

Commandes principales:
- `docker build <dockerfile>` --> Créé image
- `docker pull <repoName>` --> Chope image existante d'un registre (DockerHub / Harbour / ...), sorte de catalogue d'images.
- `docker run <image>` --> Fait tourner une image existante

Docker engine: 
- App client / serveur
- Daemon docker
- CLI
- API pour interaction w/ daemon

Docker Desktop:
- Pour Windows / MacOS
- Sort de grosse VM GNU qui fait tourner docker engine
- Plus un ensemble de services à dispo

Docker compose:
- Boite à outils pour lancer de multiples container (Ex: Pop un container pour app, un autre pour bdd...)
- Tout en YAML

Docker SWARM --> Orchestrateur de container (gestion automatique / manuel de container genre pop / kill / run si down / ...) === Kubernetes en moins populaire.

Docker hub:
- Github du container, tout plein d'images (officielles ou non)
- Team / Organisations

### Quelques commandes

- `docker run <name>` --> Si image <name> existe localement, il la démarre, sinon la pull et la démarre. 
- `docker run -d -p 8080:80 <name>` --> `-d` pour daemon, `-p` pour forward (host: 8080 -> container: 80). `localhost:8080` permet de taper sur port 80 de container.
- `docker ps` --> List les container qui tournent (`-a` pour afficher ceux qui sont arretés).
- `docker stop <name>` --> Stop un/des containers.
- `docker rm <name>` --> Supprime un/des containers.
- `docker exec -it  <name> bash` --> ouvre un terminal (`-i: interactive, -t: tty`) sur un container puis lance bash.
- `docker run -it <name> bash` --> pop et ouvre terminal + bash.
- `docker run -v <chemin> ...` --> permet de monter un dossier hote en tant que volume du container (les données du container ne sont PAS PERSISTANTES).

### A savoir / bonnes pratiques

Un container peut avoir 3 états:
- Run
- Stop
- n'existe pas

Pour `pull` de la meilleur manière possible, il faut préciser la version + le hash de l'image (comme ça on est sur). Prendre `latest`  peut provoquer des surprises.
- `docker pull <img>:<tag>@<hash>`

Qu'est-ce qu'une image ?
- Un fichier immutable
- Se compose de plusieurs layers
- dockerfile
- passage de image à container avec `docker build`
- S'appuie sur un `Union file system` (ensemble de layers préexistant, idée d'héritage entre image)

| Layer | APP | Container |
| Layer | Apache | I|
| Layer | EMACS | M |
| Layer | Kernel | G |

Ce dessus, Apache / Emacs / Kernel représentent une image. ça correspondrait à:
```
From debian:buster

Run apt update && apt install EMACS
Run apt update && apt install apache 2

CMD <Start apache>
```

Il y a 4 commandes principales (de dockerfile): 
- FROM --> Chope une image de départ, idée d'héritage
- RUN --> Exec commande sur image (ajouter layer)
- COPY --> Copie de host à container
- CMD --> Exec commande sans ajouter de layer (ex: lancer un service)


Dockerfile -`build`-> Image -`run`-> Container

Conseils:
- utiliser un linter lors de la redaction du dockerfile
- utiliser un `makefile` pour les commandes complexes (avec des kilometres de redirections de ports et tout...)
- utiliser le "build pattern" pour fragmenter des parties de build et les réutiliser
- Ne pas lancer une app dans un container en `root` 
- Utiliser `ENTRYPOINT` pour set de variables d'environement juste avant d'utiliser CMD.

### Builder pattern

```
From ... as builder

// ajout de layers
// Compilation

From ...

// recup de l'execution de `builder`
// Faire tourner une app sans tout ce qui est en rapport avec compilation (genre les compilateurs + spécificités du langage ...)
```
