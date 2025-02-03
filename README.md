# À propos de Wordpress
 
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
> -
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



# Installation locale
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
- Microsoft VC++ packages (Si ils sont manquants, vous pouvez les télécharger facilement)
- D'une plate-forme de développement Web contenant un serveur Apache 2.4, du PHP, une base de données MySQL et/ou MariaDB et PHPMyAdmin. Le logiciel utilisé ici est [WAMP](https://www.wampserver.com/) (utilisable pour windows)