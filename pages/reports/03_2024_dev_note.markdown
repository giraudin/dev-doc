---
layout: page
title: Avenirs ePortfolio - Travaux de développement - Point d'étape 03/2024
is_menu_entry: false
---



# Contexte, expérimentations et premières orientations
Le projet s'appuie sur une démarche de co-construction dont les travaux sont en cours. <br/>
Le cahier des charges ainsi que la modélisation des données ne sont pas encore définis, mais certains besoins sont déjà identifiés : authentification, gestion des API, stockage, indexation, notifications, etc.<br/>
 L'idée est d'effectuer les travaux préparatoires pour être rapidement en ordre de marche lorsque l'équipe de développement sera complétée et les fonctionnalités attendues précisées :
<ul class=spaced>
    <li> <b>Expérimentations autour d'outils :</b> API manager, Bokers.</li>
    <li> <b>Environnement de développement intégré : </b>Mise en œuvre d'un environnement de développement avec un ensemble des services. Ces services sont paramétrés pour dialoguer entre eux. Le déploiement se réalise très facilement sur un seveur de test ou en local pour le développement. De nouveaux services peuvent être ajoutés facilement en fonction des besoins.</li>
    <li> <b>Authentification et intégration OpenId Connect : </b> l'intégration OIDC a été testée de bout en bout et s'articule entre l'interface utilisateur, l'API manager et l'API ePortfolio qui a été initiée.</li>
    <li> <b>Interface utilisateur :</b> le choix du framework n'est pas encore arrêté mais des travaux ont été réalisés autour des fonctionnalités temps réel, pour les notifications, et des web components pour la réutilisabilité des éléments d'interface utilisateur :  
    <a href="https://github.com/avenirs-esr/authentication-webcomp" target ="_blank">https://github.com/avenirs-esr/authentication-webcomp</a></li>
    <li> <b>Site développeurs : </b> un site de documentation, essentiellement à destination des developpeurs a été développé, basé sur Github pages. Il contient les notes de synthèse concernant les éxpérimentations menée et des pistes de réflexion.<br/>
     Il précise également les éléments permettant de fixer un cadre de développement : versionnage, gestion des commits, workflow, etc.<br/>
     <a href="https://avenirs-esr.github.io/dev-doc/" target ="_blank">https://avenirs-esr.github.io/dev-doc/</a>
 </li>
    <li><b>API ePortfolio :</b>Développement d'une première brique de l'API, basée sur Spring boot, Kafka, Apache Apisix et OIDC.<br/> 
       <a href="https://github.com/avenirs-esr/avenirs-api" target ="_blank">https://github.com/avenirs-esr/avenirs-api</a>
    </li>
    </ul>  

# Prospection autour des API managers 
L'interropérabilité et au c&oelig;ur du projet Avenirs ePortfolio. La mise a disposition et les interactions avec des API sont donc un élément central. <br/><br/>
Cela  implique des besoins en terme de :
 - Gestion du trafic.
 - Monitoring, alertes.
 - Autorisation/Authentification, sécurisation des web services.
 - Gestion des déploiements, par exemple avec une stratégie de canary release qui permet de tester les nouvelles fonctionnalités sur une population restreinte.
 
  Pour traiter ces problématiques, une possibilité est d'utiliser un logiciel spécialisé : un API manager.  les API managers s'interfacent en amont des API développées et apportent les fonctionalité nécessaires au traitement de flux entrants ou sortants. <br/>
  Les principaux outils du marché on été expérimentés : <a href="https://avenirs-esr.github.io/dev-doc/apim-list/" target="_blank">https://avenirs-esr.github.io/dev-doc/apim-list/</a><br/>Parmis ces outils Gravitee et Apache Apisix se sont démarqués. Des contacts ont été pris avec les commerciaux de ces deux produits et des tests plus poussés ont été réalisés autour de l'intégration OIDC pour l'authentification. Les coûts de licence donnent plutôt l'avantage à Apache Apisix mais une licence éducation est en cours d'élaboration du côté de Gravitee.<br/><br/>
  Les API manager ne sont pas encore courants dans les établissements mais la problématique est identifiée et leur intérêt semble faire consensus. Nous avons pu échanger sur ce sujet avec l'Université de Loraine qui utilise Gravitee pour gérer ses API.

# Environnement de développement 
L'objectif de ce projet est de constituer un environnement autonome et intégré : <a href="https://github.com/avenirs-esr/srv-dev" target="_blank">https://github.com/avenirs-esr/srv-dev</a> <br/>
Il permet de déployer très rapidement, dans des conteneurs, l'ensemble des services sur un serveur de test ou localement pour les développeurs ou contributeurs. <br/>
Il est basé sur docker et docker-compose et actuellement, la liste des services déployés est la suivante :
<ul class="spaced">
    <li> <b>Authentification/OIDC :</b> CAS et OpenLdap.</li>
    <li> <b>Reverse proxy/serveur web :</b> Apache. La partie serveur web héberge les pages d'exemples et d'expérimentation.</li>
    <li> <b>API Manager : Apache Apisix, 4 conteneurs :</b> passerelle, dashboard, collecte et visualisation des métriques.</li>
    <li> <b>Broker :</b> Apache Kafka, 3 conteneurs : API, interface utilisateur, paramétrage et coordination distribués.</li>
    <li> <b>API ePortfolio :</b> version java basée sur Spring Boot, et une version initiale, basée sur NodeJs.</li>
</ul>

# Architecture
Les bases de l'architectures ont commencé à être posées. Outre une séparation classique entre interfaces utilisateurs (frontend) et les APIs (backend), les principaux modules sont identifiés avec un découpage basé sur les grand domaines fonctionnels :<br/>
<a href="https://avenirs-esr.github.io/dev-doc/arch-main-modules/" target="_blank">https://avenirs-esr.github.io/dev-doc/arch-main-modules/</a><br/>
<a href="https://avenirs-esr.github.io/dev-doc/arch-building-blocks-draft/" target="_blank">https://avenirs-esr.github.io/dev-doc/arch-building-blocks-draft/</a>
<br/><br/>
Nous avons pu échanger avec l'équipe technique PC-scol qui nous a recommendé de privilégier une architecture simple. Ils nous ont déconseillé de mettre en place une architecture de type micro services car cela complexifie considérablement les traitements en introduisant des problématiques de synchronisation de données. 

# Perspectives 

Parmis la listes de travaux à mener ou initier à court terme un certain nombre de points ressortent prioritairement :
<ul class="spaced">
<li><b>Interfaces utilisateurs :</b>Commencer à définir les interfaces utilisateur, éventuellement en mode fil de fer, la cinématique et les cas d'usage. L'ergonomie, l'accessiblité, et d'un manière générale l'expérience utilisateur sont des élements essentiels et doivent être pris en compte le plus tôt possible dans la vie du projet. Cela permettrait également de commencer à travailler sur la notion de rôles utilisateurs.</li>

<li><b>Stockage/ indexation / cyle de vie des données :</b> le stockage des traces, leur exploitation et conservation représentent un point central en termes fonctionnel et complexe d'un point de vue technique avec des contraintes liées au volume de données. Une modélisation, même partielle des objets manipulés est nécessaire pour pouvoir initier les travaux de ce module.</li>

<li><b>Log / Monitoring / collecte des usages : </b> c'est également un point essentiel, en terme d'exploitation, afin de garantir un fonctionnement nominal de la plateforme. Il s'agit d'u module transversal à intégrer au développement des autres modules.</li>
</ul>




