# BDD Relationnelles

Une bdd relationnelle est une base de donnée où les données sont stockées en **entitées primaires** (string, int, etc..).
Premiere BDD relationnelle par **IBM en 1970**.

Ces BDD gerent **l'acces concurent aux données**.

L'information est stockée dans des tableaux à deux dimensions appelées des **relations** ou **tables**.

- Lignes = enregistrements
- Colonnes = attributs

Le langage utilisé est appelé **SQL** (*Structured Query Language*).

Une BDD relationnel doit garantire l'intégrité des données :

- **A** : Atomicité = La mise à jour d'une donnée répartie sur plusieurs table se fait en totalité ou pas du tout.
- **C** : Coherence = À un instant T, tous les utilisateurs voient les mêmes données.
- **I** : Isolation = L'etat doit être stable, peut importe si des mises à jours se produisent simultanement ou les unes après les autres.
- **D** : Durabilité = Une fois la mise à jour validée (et non effectuée), la base de donnée est stable, meme si elle doit s'eteindre ou autre, la mise à jour se fera une fois la base de nouveau allumée.

## Scalabilité

Il existe deux types de scalabilité :

- Horizontal : Pour plus de ressources : Plus de machine
- Vertical : Pour plus de ressources : Augmenter les ressources de la machine

## Unicité

Pour garantir l'unicité, on met en place une **clé primaire** (**primary key**) qui permet d'identifier un enregistrement de manière unique. 
Ce n'est pas forcement un id, mais peut etre dérivé d'attributs de la table.

## Types d'attributs

- Numérique
    - Entiers : int
    - Décimaux : 
        - Decimal(5,2) -> -999.99 et 999.99
        - Decimal(5,4) -> -9.9999 et 9.9999
- Alphanumérique
    - Varchar : pour les attributs de type String (max : 9000octets)
- Temporel
    - Date : (AAAA-MM-JJ)
    - Time : (hh:mm:ss)
    - DateTime
    - etc...


## Requetes

- SHOW databases; *(voir toutes les bases de données de l'instance)*

- CREATE DATABASE 'nom de base'

- USE 'nom de table' *(Se mettre sur la table nommée)*

- CREATE TABLE 'nom de table' (
    ATTRIBUT type,
    ...
)

- INSERT INTO 'table' (ATTRIBUT1, ATTRIBUT2) values (attribut1 value, attribut2 value)  
*(ATTRIBUT1 et ATTRIBUT2 optionnel, uniquement si on ne veut pas peupler tout l'enregistrement)*

- SELECT 'attribut' FROM 'table'

- ALTER TABLE 'nom de table' ADD CONSTRAINT 'nom de la contrainte' \<primary, etc> 'nom du champ'

- DELETE from 'nom de table' *(delete tout le contenu de la table si pas de WHERE)*

- DROP 'nom de table' *(Supprime toute la table)*

## Foreign Keys

Les clés etrangeres permettent de croiser des données sur plusieurs tables
**Une clé étrangere réference une clé primaire d'une autre table**

## Jeux de caracteres

Historiquement, les caracteres etaient codés sur 7bits => 128 caractères possible. (**ASCII**)
8bits => 256 caractères (**ISO-8859**-x)
À present, on utilise la norme **UTF8**

## Interclassement (Collations en anglais)

Permet d'avoir une équivalence sur les caractères "**è**", "**à**", etc... avec "**e**", "**a**", etc... pour avoir un **ordre alphabetique** correct

_bin => b != B
_ci => b = B
_general => a = à

Ces collations sont **cumulables**

# Commandes

Se connecter au serveur :
```
mysql -u root -h 172.17.0.3 -p
```