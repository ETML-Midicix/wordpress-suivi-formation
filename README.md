# Partie 1 : À propos de Wordpress

## Qu'est-ce que Wordpress ?

Wordpress est un **CMS** (Content Managment System), gratuit et libre. Écris en PHP, il donne accès à des bases de données en MySQL et MariaDB.

>[!NOTE]
> Un CMS est un programme informatique permettant de créer et travailler à plusieurs sur un site Internet, un blog ou encore un site e-commerce. Il est également adapté à tous (un utilisateur qui n'est pas un développeur peut faire un site web sans connaissances, mais sera plus limité)
> ex : Wordpress, Wix...

L'origine de Wordpress remonte en 2001. Créer par *Michel Valdrighi*, **b2** (de son ancien nom), voit le jour en tant que logiciel de publication de blog open-source.
Ce n'est que quelques années plus tard, en janvier 2003, que *Matthew Mullenweg* et *Mike Little*, reprennent ce projet, corriges des bugs, ajoutent des fonctionnalités et décidèrent de le renommer **B2evolution**, puis ensuite **Wordpress**.

En mai 2003, Wordpress v0.7 deviens le successeur officiel de **b2**, et son créateur *Michel Valdrighi* réintègre l'équipe de développement.

## Questions

> ### 1) WordPress est-il beaucoup utilisé ?
> D'après wikipedia "À la date du 19 janvier 2025, WordPress était utilisé par 43,5 % des sites web dans le monde", ce qui reviens à un taux se rapprochant de la moitié du marché. Les autres sites sont autour de ces chiffres là, environ 43,6%.

> ### 2) Combien coûte WordPress ?
>
> Il y a différents plans proposés par Wordpress **(tarifs /mois HT)**
>
> | Gratuit | Personnel | Premium | Business | Commerce | Entreprise |
>| :-- | :--: | :--: | :--: | :--: | :--: |
>| 0 CHF | 5 CHF | 10 CHF | 30 CHF | 54CHF | à partir de 25000 $ / an |
>||Faites votre nid sur le Web avec un nom de domaine personnalisé. |Construisez un site Web à votre image à l'aide de puissants outils de conception. |Libérez la puissance de WordPress avec la plateforme d’hébergement géré conçue par les spécialistes de WordPress. |Créez une boutique en ligne puissante avec des extensions premium intégrées. |L’aisance et la flexibilité de WordPress avec une évolutivité, une sécurité et des capacités basées sur les données sans pareilles. |
>
>Se référer au lien [ci-contre](https://wordpress.com/fr/pricing/)

> ### 3) Quelle est la différence entre wordpress.com et wordpress.org
>
> #### wordpress.com
>
> - différents plans
> - optimisation
> - sécurisation
> - supports
>
> #### wordpress.org
>
> - possibilité de télécharger le code source de wordpress
> - hébergement local ou hébergement externe (services d'hébergement de wordpress non inclus)
>
>Se référer au lien [ci-contre](https://wordpress.com/support/com-vs-org/)



# Partie 2 : Installation locale
## Processus et étapes d'installation sur Windows
[cf Hostinger](https://www.youtube.com/watch?v=bBR1sbEe3Vc&ab_channel=L%27Acad%C3%A9mieHostinger)

1. Rendez vous sur https://www.wampserver.com/ et cliquer sur **Télécharger**
1. Ensuite, installez-le sur votre appareil et il vous sera demandé de choisir le navigateur par défaut pour l'application, ainsi que son éditeur de texte.
1. Lancer PHPMyAdmin depuis WAMP
1. Connectez-vous avec l'identifiant root et sans mot de passe
1. Créez une base de donnée avec le nom "WordPress"
1. Rendez vous sur https://wordpress.org/ et cliquer en haut à droite sur **Get WordPress** (ce qui reviens à [ceci](https://wordpress.org/download/))
1. Ensuite, dezipper-le et déplacez-le dans le dossier "www" de WAMP, soit un chemin ressemblant à celui-ci **wamp64\www** avec wamp64 se situant dans le dossier sélectionné lors de l'installation.
1. Renommez le dossier dézipper, par exemple en testsite
1. Rendez vous sur http://localhost/testsite, dans le cas où vous avez renommez le dossier **testsite**, sinon, changez ceci par le nom de votre dossier.
1. Sélectionnez votre langue s'il vous la demande.
1. Cliquez ensuite sur **C'est parti!**
1. Compléter les informations de la base de données définies précédement ici sont les suivantes :
- nom de la base de données = WordPress
- identifiant = root
- mot de passe = *champ vide*
- adresse = localhost

Et voilà, vous avez installé WordPress en local sur Windows !

## De quoi WordPress a-t-il besoin pour fonctionner ?

Wordpress a besoin de plusieurs choses pour fonctionner :
- Un web Serveur (par exemple Apache 2.4)
- Un language de script (PHP)
- une base de données (MySQL et/ou MariaDB)

Le logiciel utilisé ici, afin de réunir ces 3 besoins, s'appelle [WAMP](https://www.wampserver.com/) (utilisable pour windows)

# Partie 3 : Installation distante

[Documentation Ubuntu](https://ubuntu.com/tutorials/install-and-configure-wordpress#1-overview)

## Installation des dépendances

Connectez-vous ä votre machine distante par ssh.

Ensuite, effectuez les commandes suivantes pour installer les dépendances

```shell
sudo apt update
```

```shell
sudo apt install apache2 \
                 ghostscript \
                 libapache2-mod-php \
                 mysql-server \
                 php \
                 php-bcmath \
                 php-curl \
                 php-imagick \
                 php-intl \
                 php-json \
                 php-mbstring \
                 php-mysql \
                 php-xml \
                 php-zip
```

## Installation de WordPress

Ici, nous téléchargeons **WordPress** à partir de la dernière release, plutòt que de le télécharger à partir de la commande *apt*

Création d'un dossier pour WordPress
```shell
sudo mkdir -p /srv/www
```

Défini l'utilisateur propriétaire du dossier (l'utilisateur d'apache)
```shell
sudo chown www-data: /srv/www
```

Télécharge la dernière release et le décompresse dans le dossier /srv/www
```shell
curl https://wordpress.org/latest.tar.gz | sudo -u www-data tar zx -C /srv/www
```

## Configuration d'apache pour WordPress

Cröer un fichier **/etc/apache2/sites-available/wordpress.conf**
```shell
sudo nano /etc/apache2/sites-available/wordpress.conf
```

 Écrire le contenu suivant dans le fichier
 ```shell
<VirtualHost *:80>
    DocumentRoot /srv/www/wordpress
    <Directory /srv/www/wordpress>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted
    </Directory>
    <Directory /srv/www/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
 ```

Activer le site
```shell
sudo a2ensite wordpress
```

Activer la réécriture d'url
```shell
sudo a2enmod rewrite
```

Désactiver le site par défaut d'apache "It Works"
```shell
sudo a2dissite 000-default
```

Recharger apache pour appliquer les changement effectués
```shell
sudo service apache2 reload
```


## Configuration de la base de données

Connexion à MySql
```shell
sudo mysql -uroot
```

Si vous souhaitez ajouter / changer de mot de passe (recommandé)
```shell
ALTER USER 'root'@'localhost' IDENTIFIED BY '<password>';
```

Cröer la base de donnée 'wordpress'
```shell
CREATE DATABASE wordpress;
```

Créer un utilisateur pour faire fonctionner wordpress (remplacer **<password\>** par le mot de passe souhaité)
```shell
CREATE USER wordpress@localhost IDENTIFIED BY '<password>';
```

Affecter les droits à l'utilisateur WordPress
```shell
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON wordpress.* TO wordpress@localhost;
```

Actualiser les privilèges utilisateurs.
```shell
FLUSH PRIVILEGES;
```

>[!NOTE]
> Pour quitter MySql, faire la commande **exit**

## Configuration de WordPress pour la connexion à la base de donnée

Copier la sample configuration dans le fichier **wp-config.php**
```shell
sudo -u www-data cp /srv/www/wordpress/wp-config-sample.php /srv/www/wordpress/wp-config.php
```

Remplacer le nom de la base de données par celle créée précédement
```shell
sudo -u www-data sed -i 's/database_name_here/wordpress/' /srv/www/wordpress/wp-config.php
```

Remplacer le nom d'utilisateur par celui créé précédement
```shell
sudo -u www-data sed -i 's/username_here/wordpress/' /srv/www/wordpress/wp-config.php
```

Remplacer le mot de passe par celui créé précédement
```shell
sudo -u www-data sed -i 's/password_here/<password>/' /srv/www/wordpress/wp-config.php
```

Ouvrir le fichier de configuration
```shell
sudo -u www-data nano /srv/www/wordpress/wp-config.php
```

Remplacer ceci
```
define( 'AUTH_KEY',         'put your unique phrase here' );
define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
define( 'NONCE_KEY',        'put your unique phrase here' );
define( 'AUTH_SALT',        'put your unique phrase here' );
define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
define( 'NONCE_SALT',       'put your unique phrase here' );
```

par ceux returné par ce lien : https://api.wordpress.org/secret-key/1.1/salt/

## Configuration WordPress

Ouvrir depuis votre machine locale wordpress : http://**<ip de votre machine distance\>**

Döfinissez la langue et les valeurs que vous souhaitez pour votre site

Et voilà, votre site WordPress est prêt.

# Partie 4 : Installation sur docker

## Qu'est-ce que docker ?

Docker est un outils permettant de lancer et d'empaqueter une applications et leurs dépendances dans des **conteneurs**.

### Différence entre `Conteneurisation`et `Virtualisation` ?

| | Conteneurisation | Virtualisation |
| :-- | :-- | :-- |
| **Explication** | Permet d'isoler une application au seins de conteneurs, qui encapsulent l'ensemble des dépendances nécessaires à leur fonctionnement. En tant que développeur, cela permet de travailler sur une application, avec le même environnement | Permet d'émuler un appareil informatique, tels qu'un ordinateur |
| **Avantages** | Beaucoup plus léger, demandant donc moins de ressources et plus rapide, plus portable car elles encapsulent touts ses dépendances et n'a pas besoin d'hyperviseur pour fonctionner | Environnement complet contenant un système d'exploitations, permettant de simuler un appareil entier, permettant donc également de prendre en compte les erreurs pouvant provenir de l'OS, plus sécurisé car OS indépendant |
| **Inconvénients** | Chaque conteneurs utilisent le même noyau d'OS, ce qui peut être une faille car si par exemple un conteneur obtiens un virus, les autres peuvent en être affecté  | Environnement demandant beaucoup plus de ressources donc moins performants |

### Dockerfile vs docker compose

> ### Dockerfile
>
>Fichier (Dockerfile) de script contenant des commandes, afin de build une image docker (pouvait être utilisé plus tard pour créer une application à conteneur unique)


> ### docker compose
>
>Fichier (*.yml) permettant de créer une application multi conteneurs, à partir d'images docker en ligne (dockerhub) ou provenant d'un Dockerfile local. Permet de faire communiquer plusieurs conteneurs différents ensemble.



### Ports, Volumes et Environnements

> ### Ports
>
> Permet d'exposer un port à la machine hôte, par un port aléatoire ou donné en paramètre

> ### Volumes
>
>Permet de lier des dossiers locaux avec des dossiers dans le conteneur

> ### Environnements
>
>Permet de définir les variables d'environnements du conteneur, qui seront utilisés afin de définir des valeurs tels que des identifiants




## Installation

### Installer docker

Installer docker et ces plugins
```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Pour tester si l'installation a fonctionnée

```shell
sudo docker run hello-world
```

> [!NOTE]
> Explication des différents packages installé
>
> | docker-ce | docker-ce-cli | containerd.io | docker-buildx-plugin | docker-compose-plugin |
>| :--: | :--: | :--: | :--: | :--: |
>| Version de docker qui supporte l'édition communautaire, d'où son nom (ce => Community Edition), *à besoin de **docker-ce-cli** | **docker-ce** version console | Contrôle tout ce que le conteneur pourrait faire, des transferts d'images et de stockage à l'exécution et la supervision du traffic réseau | Permet d'étendre les possibilité de build d'images, en utilisant le builder `BuildKit` | Permet d'effectuer des `docker compose`|

### Installer Wordpress

[source](https://medium.com/@richardevcom/wordpress-development-environment-with-docker-ba52427bdd65)

Reproduisez l'arborescence ci-dessous

```
wp-dev/
├─ wp-content/
├─ compose.yml
├─ .env
```

Vous pouvez créer les dossiers avec cette commande la faire avec cette commande

```shell
sudo mkdir wp-dev wp-dev/wp-content
```

Pour créer le ficher `.env`, faites les commandes ci-dessous

Se déplacer dans le dossier wp-dev
```shell
cd wp-dev
```

Créer et ouvrir le fichier `.env` en mode édition
```shell
sudo nano .env
```

Coller le contenu ci-dessous

.env
```shell
ROOT_PASSWORD=""
WORDPRESS_USERNAME=""
WORDPRESS_PASSWORD=""
```

>[!NOTE]
> Remplacer les champs de caractères vides par les données corespondantes à celles que vous souhaités


Créer et ouvrir le fichier `docker-compose.yml` en mode édition
```shell
sudo nano docker-compose.yml
```

Coller le contenu ci-dessous
```yml
#docker-compose.yml
version: "3.6"
services:
  wordpress:
    image: wordpress:latest
    container_name: wordpress
    volumes:
      - ./wp-content:/var/www/html/wp-content
    env_file: .env
    environment:
      - WORDPRESS_DB_NAME=wordpress
      - WORDPRESS_TABLE_PREFIX=wp_
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=$WORDPRESS_USERNAME
      - WORDPRESS_DB_PASSWORD=$WORDPRESS_PASSWORD
    depends_on:
      - db
      - phpmyadmin
    restart: always
    ports:
      - 8080:80

  db:
    image: mariadb:latest
    container_name: db
    volumes:
      - db_data:/var/lib/mysql
    env_file: .env
    environment:
      - MYSQL_ROOT_PASSWORD=$ROOT_PASSWORD
      - MYSQL_USER=$WORDPRESS_USERNAME
      - MYSQL_PASSWORD=$WORDPRESS_PASSWORD
      - MYSQL_DATABASE=wordpress
    restart: always

  phpmyadmin:
    depends_on:
      - db
    image: phpmyadmin/phpmyadmin:latest
    container_name: phpmyadmin
    restart: always
    ports:
      - 8180:80
    env_file: .env
    environment:
      PMA_HOST: db
      MYSQL_ROOT_PASSWORD: $ROOT_PASSWORD

volumes:
  db_data:

```

effectuez la commande pour créer l'application muti conteneur
```shell
docker compose up -d
```

Lancer http://localhost:8080

Configuré le site WordPress

Et voilà

`Schéma ERD (entity-relationship diagram) de la base de données WordPress`
![Screenshot from 2025-02-10 11-35-29](https://github.com/user-attachments/assets/bbc02a6a-af92-4174-b734-ab5b38b75a60)



### Commandes utiles à connaître

```shell
docker compuse up -d
```

```shell
docker ps -a
```

```shell
docker compose start wordpress
```

```shell
docker exec -it db sh
```
Obtenir les processus en cours à l'intérieur d'un conteneur (après la commande précédente)
```shell
ps -aux
```
