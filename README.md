# Configurar-PostgreSQL-con-Docker-en-Windows-10-Tutorial-Labs-Estad-sticas-Editar-video

Este tutorial explica de manera breve y clara cómo instalar y configurar Docker para levantar imágenes de PostgreSQL y así poder manejar bases de datos de manera fácil y rápida en Windows 10:

[![Watch the video](https://img.youtube.com/vi/mQbU6kMyCec/maxresdefault.jpg)](https://youtu.be/mQbU6kMyCec)

### [Full Video](https://youtu.be/mQbU6kMyCec)

Estos son los comandos que se usan en las diferentes terminales del video. Además, dejaré el documento de configuración .yml para realizar correctamente la conexión con las bases de datos. Terminal de PowerShell:
  - docker pull postgres:15.3
  - docker pull dpage/pgadmin4
Terminal de Visual Studio Code:
  - docker compose up -d
docker-compose.yml:
version: '3'
services:
  myDB:
     image: postgres:15.3
     container_name: my-database
     restart: always
     ports:
          - 5432:5432
     environment:
          - POSTGRES_USER=alumno
          - POSTGRES_PASSWORD=123456
          - POSTGRES_DB=course-db
     volumes:
          - ./postgres:/var/lib/postgresql/data

  pdAdmin:
        image: dpage/pgadmin4
        container_name: pgadmin4
        restart: always
        depends_on:
           - myDB
        ports:
           - 8080:80
        environment:
           - PGADMIN_DEFAULT_EMAIL=alumno@gmail.com
           - PGADMIN_DEFAULT_PASSWORD=123456
        volumes:
           - ./pgadmin:/var/lib/pgadmin
           - ./pgadmin:/certs/server.certs
           - ./pgadmin:/certs/server.key
           - ./pgadmin:/pgadmin4/servers.json
