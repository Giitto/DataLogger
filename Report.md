# DataLogger

## Context

Ce projet a été proposé dans le cadre d'un stage à l'Université Paris 13 par Aomar OSMANI et Massinissa HAMIDI. Le but de celui-ci est l'extension de l'étude faite par Sussex-Huawei Locomotion Dataset. Il s'agit de connecter l'application DataLogger sur Android avec une plateforme IoT afin de permettre l'envoi en continue des données récoltées par les capteurs.

--------------------------------------------------------------------------------

## L'application Android : DataLogger

### Où la trouver ?

<https://github.com/Mohaabenz/DataLogger>

### Comment ça marche ?

Grâce aux capteurs des téléphones portables où l'application est éxecutée, les données sont envoyées toute les x temps à la plateforme IoT (Qu'on a hébéergé localement sur un PC) Puis sont affiché dans une interface personnalisable.

### Notre travail

Le travail a nécessité des recherches au préalable sur trois parties complémentaires les unes des autres.

#### 1\. Capteurs

Une compréhension du fonctionnement des capteurs disponible sur les smartphones utilisée ainsi que leurs données produites. Ces recherches ont abouti à la conclusion qu'un smartphones de nos jours possèdes tout les capteurs nécessaires à notre sujet d'étude.

#### 2\. Protocoles

Une vision globale des principaux protocoles utilisé par le DataLogger nous à guidé sur le choix du protocoles HTTP pour effectuer un envoi en continue. Le protocole MQTT a été envisagé mais présente des erreurs lors de l'éxécution et qui sont en cours de correction.

#### 3\. Platforme IOT

Nous avons utilisé ThingsBoard comme plateforme car il s'agit d'un outil open-source, facilement implémentable avec un système de rules (ou règles) qui permettent la configuration, la gestion des alarmes, la création d'interface de visualisation de données à l'aide de widgets et le trie des données.

## Configuration de l'application

![App1]()

Tout d'abord, il faut spécifier l'adresse de la plateforme IoT directement dans le code source de l'application mobile, pour l'instant on n'a pas supprimer l'envoi des données à un serveur avec l'utilisation du script PHP. Au lancement de l'application sur un mobile, il faut appareiller les téléphones en BT à partir des réglages des téléphones avant de les connecter avec l'application. Ceci n'est pas indiqué dans la documentation de l'application. Par la suite, il faut activer la Data collection et le Label annotation.

### Mot de passe

Le mot de passe par défaut est `0000`. Il est modifiable dans le fichier `Constants.java`.

### Adresse plateforme IoT & Access Token

Nous avons créer une nouvelle classe SendData.java qui permet d'envoyer les données automatiquement sur la plateforme IoT et celle-ci est utilisée dans la classe LoggerHelper.java. Dans LoggerHelper.java, une fonction readFile a été implémentée pour la lecture des fichiers afin de les envoyer au format String à SendData. L'adresse de la plateforme IoT ainsi que l'access Token se trouvent dans le fichier `SendData.java`.

### Fichier upload.php

Le fichier upload.php de base ne fonctionnait pas, on a dû en recréer un pour qu'il soit fonctionnel.

### Plateforme IoT

![TB1](https://sourceforge.net/images/icon_linux.gif)

#### Mise en place

<https://thingsboard.io/docs/user-guide/install/docker/>

#### Les rules

On a pu survoler un peu les rules mais ils n'ont pas pu être implémentée. Ce fichier, qui provient du GIT de la plateforme, montre un peu comment manipuler les rules en java : [AbstractRuleEngineLifecycleIntegrationTest.java](https://github.com/thingsboard/thingsboard/blob/master/application/src/test/java/org/thingsboard/server/rules/lifecycle/AbstractRuleEngineLifecycleIntegrationTest.java)

#### Communication

La plateforme accepte 2 protocoles : HTTP et MQTT. Avec le protocole HTTP, il faut faire une requete POST avec des paramètres au format JSON. 2 scripts Python sont disponibles pour montrer comment faire une requête.

#### Widgets

Le Dashboard est géré grâce à des widgets. On peut créer un seul dashboard et puis changer l'objet ou les objets connectées à visualiser.

--------------------------------------------------------------------------------

## Perspectives

Utiliser MQTT (Plus léger et moins d'énergie) Réseau de neuronne à part dans un serveur (Apprentissage dynamique et en continue de l'activité humaine) Un 2e réseau de neuronne pour générer des rules automatiquement Détection et résolution automatique des pannes. Gestion automatique des nouveaux devices<.. Suppression des fichiers après chaque envoi réussi (stockage dans une file d'attente pour un renvoi)(méthode .delete()) Désactivation de l'upload vers le serveur spécifié dans les paramètres.
