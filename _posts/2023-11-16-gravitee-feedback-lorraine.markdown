---
topic: Feedback of Lorraine University about Gravitee.
# attendees: Christian Daviau, Julien Gribonvald, Arnaud Deman.
author: Arnaud Deman
excerpt: Feedback from the University of Lorraine on Gravitee
main_actions_to_take: [
    Make a load test,
]
---
<br/><br/>
# Notes du RETEX Université Lorraine sur Gravitee

## Gravitee à 3 briques principales

* Brique API management en version Community
* Brique alert-engine de monitoring payant dans gravitee (4 800€/an tarif négocié)
* Brique sécurité access-management fonctionnel avec CAS, voir avec shib en version EE mais non utilisé

Premiers contacts en 2018.

## Points faibles

* la documentation
* les montées de versions difficiles à suivre (qualif à la main des màj liés aux features utilisées)

## Features utilisées

* Usage du dynamic routing
* "http callout"
* mock
* modification des headers pour forcer le passage par gravitee
* API-Docs peut remonter dans gravitee

## Autres infos

Utilisait WSO2 avant, mais périmètre trop large. Gravitee était plus simple. Comparaison avec kong, etc...

Se sont limité à une utilisation simple pour faciliter une migration éventuelle.

Peut d'empreinte en terme de charge.
-> préconise un test de charge sur l'outil avant adoption définitive.

En test avec kafka pour la gestion API asynchrone car gravitee ne le gère pas encore

gravitee va passer sur kubernetes, dans la roadmap.