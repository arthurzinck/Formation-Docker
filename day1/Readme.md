
# Day 1

## Historique
### Conteneurisation
* la conteneurisation c'est vieux
  * 1979: chroot
  * 2000: FreeBsd Jails
  * 2004: Solaris containers
  * 2005: OpenVZ
  * 2008: LXC
  * 2013: Docker

### Docker

* Qu'est-ce que Docker ?
  * Technologie de containerisation
  * Entreprise fournie un api de ligne de commande

#### Historique

* 2008 : Solomon Hykes, issu d'Epitech crée la société dotCloud
* 2010 : impossibilité de lever des fonds dans l’Hexagone, fermeture de dotCloud en France et incubation aux Etats-Unis via Ycombinator
* 2011 : libération du code sourde de dotCloud
* 2013 : naissance officielle de Docker, réécriture complète en OpenSource de dotCloud dans le langage Go
* 2014 :
  * intégration de Docker chez AWS 
  * partenariat avec IBM Cloud
  * version 0.9 libcontainer remplace LXC
  * annonce de Microsoft d'intégration de Docker à Windows 2016
* 2015: de plus en plus de projet se lance avec docker et c'est est un des projets qui à le plus d'étoiles sur GitHub
* 2016: 
  * les contributeurs principaux de la *Docker Team* : Cisco,Google, Microsoft, IBM, RedHat, Huawei
  * intégration dans Windows 10 avec Docker for Windows
* 2017:
  * Docker téléchargé plus de 13 milliards de fois 
  * changement dans le numération versions Docker CE et Docker EE
* 2018 :
  * intégration de Kubernetes
  * intégrations des plateformes Container As A Service et Container without Server
  * Docker EE 2.0
  * [Solomon Hykes quitte Docker](https://www.silicon.fr/solomon-hykes-quitte-docker-la-societe-quil-a-fondee-204943.html?inf_by=5b6e9742671db8113a8b4952)

#### Concurence 
* CRI-O
* ContainerD
* Rkt

### Autour de Docker 

* L'Open Container Initiative à pour but de mettre en place les standards techniques autour des formats des conteneurs, des images et des runtime les exécutants.

* Google et la Fondation Linux ont créé la Cloud Native Computing Fundation ou CNCF.

* De nombreux membres : AT&T, Box, Cisco, Cloud Foundry Foundation, CoreOS, Cycle Computing, Docker, eBay, Goldman Sachs, Google, Huawei, IBM, Intel, Joyent, Kismatic, Mesosphere, Red Hat, Twitter, Univa, VMware et
Weaveworks ...

* La CNCF a pour vocation de s’assurer de la bonne exécution des applications dans des environnements Cloud.

* Plusieurs graduations de projets, Kubernetes fait partie des projets les mieux "géré" : [Projets CNCF](https://www.cncf.io/projects/)

## Docker

### Architecture :
  * Daemon: tourne en arriere plan et fait tourner les conteneur gere les images
  * CLI: contacte l'api pour demander au Daemon de faire des actions
  
## Qu'est-ce qu'une image ?
* un binaire immutable
* contient toute les étapes dans des couches successive
* créée a partir d'un Dockerfile
 
## Qu'est-ce qu'un conteneur ?
* créée a partir d'une image
* un process dans un cgroup et dans un namespaces

## Différence avec une VM ?
* Pas d'émulation et pas d'emulateur
* Réutilisation du kernel, des binaires et des libs
* Technologie utilisé: [Pour en savoir plus](https://www.nginx.com/blog/what-are-namespaces-cgroups-how-do-they-work/)
  * Namespaces: fonction du Kernel pour controler la vision du process
  * Control Groups: fonction du Kernel pour controler les resources du process


## Pourquoi utilisé des conteneurs ?
* replicabilité de l'environement, portabilité
* autonomie des équipes
* mise a l'echelle

## Où récuperer les images ?
* DockerHub
* Quay
* création d'un registry
 Attention penser bien a prendre des images officiel, les image docker sont des vecteur d'attaque puissant pour faire rentrer des malware au coeur des entreprises !


* Comment lancer un container ?
  * Docker run <parametres>  -t <image>

* Comment acceder à un container ?
  * docker exec -it <conteneur> <programme>
  
* Comment faire une image custom ?
  * docker commit
  * Dockerfile:
    * FROM image:version
    * RUN command
    * CMD ["arg","arg"]
    * COPY fichier endroit_ou_copier
    * ADD <fichier> <endroit_ou_copier> 
    * WORKDIR <endroit>
    * ENV <CLEFS>=<VALEUR>
    * ENTRYPOINT </chemin/bin>
    * EXPOSE <port>/<protocol>
    * Best Pratices

## Installation

[Doc d'installation](https://docs.docker.com/get-docker/)

## Exercice 1
* chercher une image
* télécharger l'image 
* creer un conteneur a partir de l'image
* afficher les containers qui tournent
* accèder a un container et le modifier
* kill le container 
* redemarrer le conteneur
* se rendre compte que les modifications ont disparues


## Exercice 2
* Créer un fichier et le nommé Dockerfile et l'on va definir les etape de creation de notre image
* Faire demarrer l'image a partir d'une image Ubuntu en version Jammy
* Definir une variable d'environement DEBIAN_FRONTEND=noninteractive
* Definir une etape où l'on mets a jour la liste de paquet et apres on install tous ces paquet `apache2 apache2-utils php php-mysql libapache2-mod-php`
* Exposer le port 80 du container
* Pour terminer ce Dockerfile ajouter une etape ou il faut lancer Apache `["apachectl", "-D", "FOREGROUND"]`
* Creer l'image et donner lui le nom exo1 
* Creer un conteneur a partir de l'image exo1
* Vérifier dans quel etat elle est en affichant les conteneur docker
* Afficher les informations sur le conteneur et trouver son Ip, y acceder
* Supprimer l'images et le container


## Exercice 3
* reprendre le Dockerfile de l'exercice precedant
* faire une page HTML bidon ou prendre un projet de site web static
* Copier le dossier ou il y a le code dans `/var/www/html`
* build l'image
* run l'image

## Exercice 4
* afficher les images
* detruire une image
* nettoyer toutes les resource docker

## Exercice 5
### Preparation
L'idée dans cet exercice et de faire une image multi-stage build,
Voici le code d'un programme faisant un `helloworld` en Golang, copiez le dans un fichier nommé `main.go`.
```go
package main

import "fmt"

func main() {
    fmt.Println("hello world")
}
```
Puis créer un autre fichier nommé `go.mod` avec ce contenue:
```go
module github.com/arthurzinck/Formation-Docker/day1/exo5

go 1.21.3
```
### Etape 1 :
Pour faire une image multi-stage build, on fait commencer l'image avec un `FROM` d'une image qui nous intérresse pour créer l'image mais pas pour la faire tourner.
Ici on va prendre l'image : `golang:1.21.3` et on va la nommer avec `AS Builder`.
Puis on va definir notre chemin de travail à `/go/src` dans l'image.
On va copier l'ensembles des fichiers présent dans le repertoire locale dans le dossier de travail.
Puis on va installer les dépendances et compiler le binaire avec l'instruction : 
```bash
RUN go get -d . && CGO_ENABLED=0 GOOS=linux go build -o /go/bin/helloworld .
```

### Etape 2 :
Pour la deuxième étape de build, dans le meme `Dockerfile`, il faut mettre une autre image de début, ici `scratch`. 
Puis on va copier le binaire (le code compilé plus haut), dans notre nouvelle image, avec l'instruction : `COPY --from=Builder /go/bin/helloworld /helloworld`
Puis on va faire en sorte de lancer le binaire au lancement du conteneurs.


## Etape 3: 
On build l'image: 
```bash
docker build -t exo5:v1
```
On constate qu'il y a bien plusieurs stage : 
```
Step 1/7 : FROM golang:1.21.3 AS Builder
1.21.3: Pulling from library/golang
8457fd5474e7: Already exists 
13baa2029dde: Already exists 
325c5bf4c2f2: Already exists 
c185020e1367: Already exists 
16418b73e8ce: Pull complete 
d0b897dfffc2: Pull complete 
Digest: sha256:b113af1e8b06f06a18ad41a6b331646dff587d7a4cf740f4852d16c49ed8ad73
Status: Downloaded newer image for golang:1.21.3
 ---> 16ac1e9944a2
Step 2/7 : WORKDIR /go/src
 ---> Running in 3249692e4194
Removing intermediate container 3249692e4194
 ---> 0768417d6790
Step 3/7 : COPY . .
 ---> 64d00dc2c3ce
Step 4/7 : RUN go get -d . && CGO_ENABLED=0 GOOS=linux go build -o /go/bin/helloworld .
 ---> Running in 9c14b1720162
Removing intermediate container 9c14b1720162
 ---> 0c3caee8b48d
Step 5/7 : FROM scratch
 ---> 
Step 6/7 : COPY --from=Builder /go/bin/helloworld /helloworld
 ---> 8770862fe647
Step 7/7 : CMD ["/helloworld"]
 ---> Running in 7f5c90fc4083
Removing intermediate container 7f5c90fc4083
 ---> 8ceb106f1d11
Successfully built 8ceb106f1d11
Successfully tagged exo5:v1
```
Et cette image ne pesent rien du tout, contrairement a la v2 que j'ai faite sans le multi-stage build : 
```bash
> docker images            
REPOSITORY                                            TAG                IMAGE ID       CREATED         SIZE
exo5                                                  v2                 39fa4abf0d69   3 seconds ago   842MB
exo5                                                  v1                 8ceb106f1d11   3 minutes ago   1.8MB
```
