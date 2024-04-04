---
layout: page
title: Code, Frameworks & Tools
permalink: /code-frameworks-tools/
is_menu_entry: true
position: left
order: 30
---


## Git webfflow
The selected git flow is [GitHub Flow.](https://docs.github.com/en/get-started/quickstart/github-flow){:target="_blank"}

## Versioning (SemVer)
The versioning strategy is [Semantic Versioning.](https://semver.org/#semantic-versioning-200){:target="_blank"}

>   Given a version number MAJOR.MINOR.PATCH, increment the:
>
>    MAJOR version when you make incompatible API changes\
>    MINOR version when you add functionality in a backward compatible manner\
>    PATCH version when you make backward compatible bug fixes

## Conventional commits
The commit messages should respect the [Conventional Commits specification.](https://www.conventionalcommits.org/en/v1.0.0/){:target="_blank"}\
This specification defines at least 2 types of messages, feat, fix and the notion of Breaking change. \
This allow to automate the SemVer management :
     
    fix             -> patch
    feat            -> minor
    Breaking change -> major

### Commitlint & husky
In order to facilitate the commit with command line, [commitlint](https://github.com/conventional-changelog/commitlint){:target="_blank"} can be used in conjunction to [husky](https://typicode.github.io/husky/){:target="_blank"} (client side git hooks).    

## API 

### API Manager
- [API Management tools](../apim-list/)

## Storage 

- [PostegreSQL](../storage-posgresql/)

#### Tests & POC

- [Gravitee](../apim-gravitee/)
- [Apache APISIX](../apim-apisix/)
- [Kong](../apim-kong/)

## Docker & Docker-compose
- [Docker & Docker-compose installation notes](../docker-install/)