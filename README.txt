*******************TUTORIEL AFIN D'INJECTER UNE BASE DE DONNEES SUR UN SITE WEB DE TYPE TOMCAT AVEC DOCKER********************


Création des Dockerfiles

1er Dockerfile ==> FROM postgres:9.5
		   VOLUME /var/lib/postgresql/data
		   COPY ./init-db.sql /docker-entrypoint-initdb.d/

2e Dockerfile ==> FROM tomcat:8-jre8
		  RUN apt-get update && apt-get install -y postgresql-9.5
		  COPY ./dbproject.war /usr/local/tomcat/webapps/

Création des Images 

A partir du 1er Dockerfile ==> build -t <<Nom de l'image>> <<Dossier contenant le 1er Dockerfile>>
A partir du 2e Dockerfile ==> build -t <<Nom de l'image>> <<Dossier contenant le 2e Dockerfile>>

Lancement des Images

1ere image ==> docker run -d -v <<Tag du volume>>:/var/lib/postgresql/data --name db(nom du container) <<Nom de la 1ere image>>
2eme image ==> docker run -d --name mytomcat(nom du container) --link db -p 9090:8080 <<Nom de la 2eme image>>

Entrer sur le site web de cette manière ==> http://addresse-ip:9090/dbproject/accueil.jsp