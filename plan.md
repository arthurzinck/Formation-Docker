# Plan de formation Docker 

* la conteneurisation c'est vieux
  * 1979: chroot
  * 2000: FreeBsd Jails
  * 2004: Solaris containers
  * 2005: OpenVZ
  * 2008: LXC
  * 2013: Docker

* Qu'est-ce que Docker ?
  * Technologie de containerisation
  * Entreprise fournie un api de ligne de commande
  * historique : 
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
      * [Solomon Hykes quitte Docker] (https://www.silicon.fr/solomon-hykes-quitte-docker-la-societe-quil-a-fondee-204943.html?inf_by=5b6e9742671db8113a8b4952)

  * concurence : 
    * CRI-O
    * ContainerD
    * Rkt
* L'Open Container Initiative à pour but de mettre en place les standards techniques autour des formats des conteneurs, des images et des runtime les exécutants.
* Google et la Fondation Linux ont créé la Cloud Native Computing Fundation ou CNCF.
* De nombreux membres : AT&T, Box, Cisco, Cloud Foundry Foundation, CoreOS, Cycle Computing, Docker, eBay, Goldman Sachs, Google, Huawei, IBM, Intel, Joyent, Kismatic, Mesosphere, Red Hat, Twitter, Univa, VMware et
Weaveworks ...

* La CNCF a pour vocation de s’assurer de la bonne exécution des applications dans des environnements Cloud.

* Plusieurs graduations de projets, Kubernetes fait partie des projets les mieux "géré" : [Projets CNCF] (https://www.cncf.io/projects/)

* Architecture :
  * Daemon
  * API
  * CLI
  
  * Qu'est-ce qu'une image ?
    * un binaire immutable
    * contient toute les étapes
    * créée sur un Dockerfile
 
  * Qu'est-ce qu'un conteneur ?
    * créée a partir d'une image
    * un process dans un cgroup et dans un namespaces


* Différence avec une VM ?
  * Pas d'émulation et pas d'emulateur
  * Réutilisation du kernel, des binaires et des libs
  * Technologie utilisé: (https://www.nginx.com/blog/what-are-namespaces-cgroups-how-do-they-work/)
    * Namespaces: fonction du Kernel pour controler la vision du process
    * Control Groups: fonction du Kernel pour controler les resources du process


* Pourquoi utilisé des conteneurs ?
  * replicabilité de l'environement
  * autonomie des équipes
  * mise a l'echelle

* Où récuperer les images ?
  * docker pull
  * docker search
  * DockerHub
  * Quay
  * création d'un registry

* Comment faire tourner un container ?
  * Docker run

* Comment acceder à un container ?
  * docker exec
  
* Comment faire une image custom ?
  * docker commit
  * Dockerfile:
    * FROM <image>
    * RUN <command>
    * CMD <arg>
    * COPY <fichier> <endroit_ou_copier>
    * ADD <fichier> <endroit_ou_copier> 
    * WORKDIR <endroit>
    * ENV <CLEFS>=<VALEUR>
    * ENTRYPOINT </chemin/bin>
    * EXPOSE <port>/<protocol>
    * Best Pratices

* Comment fonctionnent les volumes ?
  * bind 
  * anonyme
  * nommé

* Les commandes sont un peu longues ? 
  * docker-compose.yml
  * a utiliser que pour du dev surtout pas en prod.

* Comment faire pour que les containers travaillent ensembles ?
  * Depends_on
  * réseaux: 
    * bridge
    * overlay
    * none
  * Links
    

* Les bonnes pratiques pour la production
	* ne pas utiliser de docker ni de docker-compose ! 
    * ne pas utiliser pas de docker swarm
    * utiliser Kubernetes  



