## Exercice 1 :
créer un Dockerfile qui a partir de l'image ubuntu Jammy créer les variables d'environements suivantes :
 - NOM
 - PRENOM
 - EXERCICE
Mettez les bonnes valeurs a chaque fois. Puis faites en sorte que le conteneurs les affiches avec la commande `env` quand on le lance.

Pour vous notez je veux le Dockerfile.

## Exercice 2 :
* créer un fichier `index.html` contenant :
```html
 <p>Exercice2: Facile !<p>
```
* créer un Dockerfile a partir de l'image `nginx:1.25.3` dans lequels vous montez cet `index.html` dans `/usr/share/nginx/html`
* n'oublier pas d'exposer le port 80 pour que vous puisiez y avoir acces.
* Pour lancer nginx mettez cette instruction en fin de Dockerfile : `CMD [ "nginx","-g","daemon off;" ]`
* l'image doit s'apeller exo2:v1
* Quand vous lancez l'image elle doit etre exposé sur le port 8080 de votre localhost

Pour vous notez je veux : 
    - le Dockerfile
    - la commande que vous avez utilisé pour créer l'image
    - la commande que vous avez utilisé pour lancer le conteneur

## Exercice 3:
Voici un Dockerfile, optimisez le :
```
FROM golang:1.21.3
WORKDIR /go/src
COPY . .
RUN go get -d . && CGO_ENABLED=0 GOOS=linux go build -o /go/bin/helloworld .
CMD ["/go/bin/helloworld"]
```

## Exercice 4
Je veux un fichier `docker-compose.yaml` qui contienent deux services:
* un service appeler `wordpress` qui avec l'image `wordpress:6-apache` et les variables d'environement: WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD, WORDPRESS_DB_NAME pour se connecter a l'autre service
* un service appeler `mysql`  avec une image `mysql:5.6` et les variables d'environement : MYSQL_DATABASE, MYSQL_USER, MYSQL_PASSWORD, MYSQL_RANDOM_ROOT_PASSWORD pour configurer le service.
* chacun de ses service doit etre persistant


A envoyer a arthur@z3k.fr
