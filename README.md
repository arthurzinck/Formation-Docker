# Formation Docker

## CheatSheet

| quoi                                 | comment                                        |
|:-------------------------------------|-----------------------------------------------:|
|Chercher une image                    | docker search <string>                         |
|Telecharger une image                 | docker pull <repo/image:tag>                   |
|Lancer une image                      | docker run -t <repo/image:tag>                 |
|build un image a partir d'un dockerfile| docker build -t <nom_de_l_image>  .           |
|Affiche les images                     | docker images                                 |
|Detruire une ou plusieurs image        |docker rmi Image Image...                      |
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


* [Day 1](day1/Readme.md)
* [Day 2](day2/Readme.md)
* [Day 3](day3/Readme.md)
