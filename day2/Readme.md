# Docker-compose
C'est un outils permetant de gerer le cycle de vie sur votre ordinateur de plusieurs conteneurs.
Par cycle de vie, est entendue, leur eventuele creation ou l'image utiliser, leur parametrage, leur capacité a travailler ensemble, et leur mort.

## Pourquoi
Utiliser Docker-compose permet de plus facilement gérer un environement ou une application qui se compose de plusieurs conteneurs.

Aussi cela permet de garder une trace des paramètres nécessaire pour lancer chacun des conteneurs vu que c'est écrit dans un fichier en YAML.

## Syntaxe 

* versions
* service
  * nom
    * image / build
    * container_name
    * depends_on
    * volumes
    * network
* volumes
* network


Exemple :
```yaml
version: "3.8"
services:
  web:
    build: .
    depends_on:
      - db
      - redis
  redis:
    image: redis
  db:
    image: postgres
```

[liste complete](https://docs.docker.com/compose/compose-file/compose-file-v3/#service-configuration-reference)

## Installation

[Documentation d'installation](https://docs.docker.com/compose/install/)

## Reseau
* Bridge(default): permet de comuniquer avec les autre container mais n'est pas accessible en dehors de votre pc
* Host: se lance sur l'interface de votre PC et est donc disponible au autres pc dans le reseau local
* overlay: permet une communication inter pc, c'est ultiliser avec SWARM
* none
* ipvlan 
* macvlan
* network plugins

## Volume

Plusieurs possibilitées :
* [les Bind](https://docs.docker.com/storage/bind-mounts/), une association de dossier sur votre machine vers un dossier dans votre container
* [les volumes](https://docs.docker.com/storage/volumes/) , un dossier managé et créer dans les dossiers systeme docker
* [les volumes driver](https://docs.docker.com/storage/volumes/#use-a-volume-driver), possibilité d'ecrire sur un serveur distant par exemple

## Security et Best Practice

* Utilisez les versions officiel des images
* Quand vous appelez une image il faut mettre sa version
* Evitez de mettre votre code ou de la config dans l'image, monter le en volume/bind dans le `docker-compose.yaml`
* Definissez un autre utilisateur que `root`
* chaque container doit avoir une fonction independante


## Exercice 1
créer un `docker-compose.yaml` pour lancer un conteneur avec une image nginx et monter un volume avec une page html dans `/usr/share/nginx/html`

## Exercice 2
Créer un `docker-compose.yaml` avec un conteneur nginx qui sert un fichier custom et un conteneur avec une base de donnée, les deux doivent avoir des volumes persistant. Le conteneur nginx doit attendre que la base de donnée soit prète avant de démarrer.

## Exercice 3 
Créer un volume docker, le trouver sur le filesystem, l'utiliser dans un `docker-compose.yaml`

## Exercice 4
* Créer une dossier `code`, dedans créer une fichier `app.py` :
```python
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

* Créer un fichier `requirements.txt` :
```
flask
redis
```

* Créer un `Dockerfile` pour l'application : 
```Dockerfile
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

* Créer un `docker-compose.yaml` pour lancer le conteneur python contenant l'app au dessus et un conteneur Redis
```yaml
services:
  web:
    build: .
    ports:
      - "8000:5000"
    volumes:
      - ./code:/code
  redis:
    image: "redis:alpine"

```
# Exercice 5
* Créer un fichier `docker-compose.yaml`
  * créer un service `web-backend` avec une image `nginx:1.25.3` ce service doit avoir access a la BDD mais pas a l'outils de gestion de BDD
  * créer un service `db` avec une image `postgres:16.0` ce service doit etre accessible par le `web-backend` et par `adminer`.
  * créer un service `adminer` avec une image `adminer:4.8.1-standalone` ce service doit etre accessible sur le port `8080` et doit pouvoir acceder a la BDD mais pas au `web-backend`
