# DOCKER

Docker est une plateforme qui permet de créer des **conteneurs** dans lesquelles tourne une **image**.

Un **conteneur** est un environnement d'execution isolé du reste du systeme.

Une **image** est une configuration du systeme.

## Installation Windows

Pour l'installer sur Windows, il est necessaire d'avoir **WSL2** d'installé.
On peut ensuite installer **Docker Desktop** à l'aide de winget.

## Commandes

- docker ps *(-a)*
    Lister tous les conteneurs actifs *(et inactif avec -a)*
    <br>

- docker run 
    Créer un conteneur en s'attachant au terminal du container
    ``` 
    docker run --name mysqlclient -ti alpine
    ----
    docker run -dti --name mysqlclient simon/mysqlclient:1.0
    ----
    docker run -d --env MARIADB_ROOT_PASSWORD=1234 --name mariadbserver mariadb
    ```

    *--name 'nom du container'*
    *-ti s'attache au conteneur*
    *alpine = nom d'une image d'une distribution linux*
    *simon/mysqlclient:1.0 = nom d'une image*
    *-dti mode détaché du conteneur*
    *-env permet de configurer une variable d'environnement*
    <br>

- docker attach 'nom du container'
    Permet d'ouvrir le terminal sur le container
    ```
    docker attach mysqlclient
    ```
    <br>

- docker commit 'nom du container' 'nom du repository:tag(num de version)'
    Permet de créer une image à partir du container nommé.
    (Répository = nom du proprio / nom de l'image)   
    ```
    docker commit mysqlclient simon/mysqlclient:1.0 
    ```
    <br>

- docker images
    Lister toutes les images dispo sur la machine
    <br>

- docker rm 'nom du container'
    Supprimer le conteneur nommé
    <br>

- docker inspect 'nom du container'
    Permet d'obtenir la configuration du container (entre autre pour savoir l'adresse ip du containeur)
    ```
    docker inspect mariadbserver
    ```


