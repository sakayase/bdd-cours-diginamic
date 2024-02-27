# DOCKER

Docker est une plateforme qui permet de créer des **conteneurs** dans lesquelles tourne une **image**.

Un **conteneur** est un environnement d'execution isolé du reste du systeme.

Une **image** est une configuration du systeme.

## Installation Windows

Pour l'installer sur Windows, il est necessaire d'avoir **WSL2** d'installé.
On peut ensuite installer **Docker Desktop** à l'aide de winget.

## Generalités
Le volume docker est contenu dans le volume WSL.  
Quitter un conteneur avec 'exit' eteint le conteneur, pour sortir sans l'eteindre il faut utiliser **CTRL + P + Q**.  
On peut identifier les conteneurs par **CONTAINER ID** (*docker ps -a* pour les avoir).  
Créer un volume permet d'avoir une **persistance des données** entre les conteneurs sur un meme volume, et donc aussi d'isoler certains conteneurs d'autres.  
Les volumes sont stockés dans */var/lib/docker/volumes/*  
Supprimer un conteneur (par exemple avec une BDD) d'un volume ne **supprimera pas la BDD contenue sur ce volume**.  

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
    ----
    docker run -ti --name alpine0 -v test:/aa alpine 
    ----
    docker run -d --name serversql -v courssql:/var/lib/mysql --env MARIADB_ROOT_PASSWORD=1234 mariadb
    ```

    *--name 'nom du container'*  
    *-ti mode interactif*  
    *alpine = nom d'une image d'une distribution linux*  
    *simon/mysqlclient:1.0 = nom d'une image*  
    *-dti mode détaché du conteneur*  
    *-env permet de configurer une variable d'environnement*  
    *-v pour preciser le volume, :/aa permet d'indiquer de travailler dans un dossier nommé 'aa'*  
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
    ```
    docker rm mariadbserver
    ```
    <br>

- docker inspect 'nom du container'  
    Permet d'obtenir la configuration du container (entre autre pour savoir l'adresse ip du conteneur)
    ```
    docker inspect mariadbserver
    ```
    <br>

- docker volume ls  
    Permet de lister les volumes
    <br>
    
- docker volume create 'nom du volume'  
    Permet de créer un volume
    ```
    docker volume create courssql
    ```
    <br>

- docker volume rm 'nom du volume'  
    Permet de supprimer un volume
    ```
    docker volume rm courssql
    ```
    <br>

- docker volume inspect 'nom du volume'  
    Permet d'inspecter un volume
    ```
    docker volume inspect courssql
    ```
    <br>

- docker network create 'nom du reseau'  
    Permet de créer un reseau
    ```
     docker network create courssql
    ```
    <br>

- docker network inspect 'nom du reseau'  
    Permet d'inspecter un reseau (pour avoir sa plage d'ips (*subnet*))
    ```
    docker network inspect courssql
    ```
    <br>

- docker network ls  
    Voir tous les reseaux dockers
    ```
    docker network ls
    ```
    <br>

- docker network connect 'nom du reseau' 'nom du conteneur'  
    Permet de connecter le conteneur au reseau
    ```
    docker network connect courssql serversql
    ```
    <br>

- docker network disconnect 'nom du reseau' 'nom du conteneur'  
    Permet de deconnecter le conteneur du reseau 
    ```
    docker network disconnect bridge serversql
    ```

## Raccourcis

- **CTRL + P + Q** : Permet de sortir d'un conteneur attaché sans l'eteindre

## Network

Créer un reseau permet de beneficier de la résolution DNS sur les conteneurs.

