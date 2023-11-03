---
layout: page
title: Architecture - Building blocks  (Draft)
permalink: /arch-building-blocks-draft/
---


```mermaid
graph LR
    subgraph Auth["Authentication"]
        direction LR
        fauth>Federated authentication]
        localauth>Local authentication]
        oidcproxy>OIDC Proxy ?]
    end
    subgraph Storage["Storage"]
        direction LR
        rdb>Relational database]
        nosql>NoSQL]
        s3>"S3 (Archiving)"]
    end
    Auth  --> EPF((ePortfolio)) --> Storage
    
    Cache[Cache] --> EPF --> IAM["Identity & Access Management (IAM)"]
    Logs["Logging & Monitoring"] --> EPF --> Stats["Statistics"]
    APIM["API Manager (APIM)"] --> EPF    
    linkStyle default stroke-width:2px,fill:none,stroke:#505050,marker-end:none;
    
```

