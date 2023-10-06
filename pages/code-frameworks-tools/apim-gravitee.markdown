---
layout: page
title: Gravitee
permalink: /apim-gravitee/
---


## Resources

- [gravitee.io](https://documentation.gravitee.io/apim/overview/readme){:target="_blank"}



## Instalation notes

The installation method used is [Custom Install with Docker Compose](https://documentation.gravitee.io/apim/getting-started/install-guides/install-on-docker/custom-install-with-docker-compose){:target="_blank"}.
In this installation mode a directory structure has to be created. It is not mentionned in the doc bu uUnder debian like distros, the owner/groups of some folders have to be adjusted (this could probably done via the docker file too).

<pre>
/gravitee
 ├── docker-compose-apim.yaml
 ├── apim-gateway     
 │    ├── logs                   graviteeio (user defined in the image with the uid 1000)
 │    └── plugins
 ├── apim-management-api
 │    ├── logs                   systemd-resolve systemd-journal
 │    └── plugins
 ├── apim-management-ui
 │    └── logs
 ├── apim-portal-ui
 │    └── logs                   systemd-resolve systemd-journal
 ├── elasticsearch
 │    └── data
 └── mongodb                     
     └── data                    systemd-coredump systemd-coredump

</pre>
