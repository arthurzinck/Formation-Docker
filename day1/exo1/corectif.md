## Exercice 1
* chercher une image: `docker search <image>``
* télécharger l'image: `docker pull <image>`
* lancer l'image `docker run -t <image>` rajoutez -i pour que le conteneur soit interractif
* afficher les containers qui tournent: `docker ps`
* accèder a un container et le modifier: docker exe -it <conteneur_id> /bin/sh ou /bin/bash, creer un dossier teste
* kill le container: docker kill <conteneur_id>
* relancer l'image: docker container start <container_id>
* se rendre compte que les modifications ont disparues `docker exec -it <container_id> /bin/bash
