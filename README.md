# Formation Docker
## CheatSheet


| quoi                                 | comment                                        |
|:-------------------------------------|-----------------------------------------------:|
|Chercher une image                    | docker search <string>                         |
|Telecharger une image                 | docker pull <repo/image:tag>                   |
|Lancer une image                      | docker run -t <repo/image:tag>                 |
|build un image a partir d'un dockerfile| docker build -t <nom_de_l_image>  .            |
|Voirs les conteneurs de lancer        | docker ps                                      |
|Voir les containeurs qui existe       | docker ps -a                                   |
|Lancer un programme dans un conteneur | docker exec -t <conteneur> <programme>         |
|Lister les volumes :                  | docker volume ls                               |
|Creer un volume                       | docker volume create <name>                    |
|Detruire les disque inutiliser        | docker volume prune                            |
|Plus d'info sur le volume             | docker volume inspect <id>                     |
|Detruire le volume en question        | docker volume rm <name>                        |
|Lister les reseau                     | docker network ls                              |
|Creer un reseau                       | docker network create -d <type> <networkName>  |
|Plus d'information sur le reseau      | docker network inspect <id>                    |
|Detruire les reseau inutile           | docker network prune                           |
|Detruire un reseau                    | docker network rm <name>                       |
|Nettoyer tout le system               | docker system prune                            |

## Exercice 1
* chercher une image
* télécharger l'image 
* lancer l'image
* afficher les containers qui tournent
* accèder a un container et le modifier
* kill le container 
* relancer l'image
* se rendre compte que les modifications ont disparues


## Exercice 2
* créer un fichier et le nommé Dockerfile
* coller le contenu suivant
```
FROM scratch
COPY hello /
CMD ["/hello"]
```
* build l'image
* run et voir que seul le binaire a été run et  exit
* modifier le Dockerfile pour qu'il resemble à ça 
```
FROM alpine
RUN  apk --update add htop \
     rm -rf /var/cache/apk/*
#ENTRYPOINT ["htop"]
CMD htop
```
* se rendre compte que c'est /bin/bash -c "htop"
* modifier le Dockerfile pour qu'il resemble à ça 
```
FROM alpine
RUN  apk --update add htop \
     rm -rf /var/cache/apk/*
ENTRYPOINT ["htop"]
#CMD htop
```
* se rendre compte que la c'est /bin/htop 


## Exercice 3
* créer un fichier et le nommé Dockerfile 
* Mettre un From ubuntu dans le Dockerfile
* ajouter une ligne ENV DEBIAN_FRONTEND=noninteractive
* Ajouter un RUN apt-get update && apt install -y apache2 apache2-utils php php-mysql libapache2-mod-php && apt-get clean
* Ajouter un EXPOSE 80
* Puis ajouter CMD ["apachectl", "-D", "FOREGROUND"]
* Build l'image : docker build -t <myCustomImageName> .
* Faire tourner l'image docker run <myCustomImageName>
* Vérifier quel tourne avec docker ps
* faire un docker inspect <container_id> et lancer curl <ipaddress>:<port>
* Supprimer l'images et le container


## Exercice 4
* reprendre le Dockerfile de l'exercice precedant
* ajourer un COPY ./dossierOuJaiMoncode /var/www/html
* build l'image
* run l'image

## Exercice 5
* faire un fichier docker compose de l'exercice precedent

## Exercice 6
* reprendre le docker compose de l'ex5
* rajouter une instance mariadb
* créer un volume nommé pour le code du site web 
* créer un volume nommé pour les données de mysql
* créer un réseau pour connecter les deux conteneurs
* copier le contenue du volume et faire en sorte que ca se connecte

## Exercice 7
* ecrire un Helloworld en golang
* faire son dockerfile en mode multistage

## Exercice 8

* chercher les volumes
* trouver leur locations
* supprimer les volumes inutiles
* supprimer les network inutiles
* docker system prune 
