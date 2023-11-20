---
layout: page
title: Docker & docker-compose installation note
permalink: /docker-install/
---

# Docker

Resource: [Install Docker Engine on Debian](https://docs.docker.com/engine/install/debian/){:target="_blank"}
<pre>
  sudo apt-get update
  sudo apt-get install ca-certificates curl gnupg
  sudo install -m 0755 -d /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  sudo chmod a+r /etc/apt/keyrings/docker.gpg


    echo   "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" |   sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
 </pre>  
N.B.: 
 - The repository may be adjusted if the Debian distribution is testing.
 - To use a Proxy adjust /usr/lib/systemd/system/docker.service
   <pre>
    (...)
    [Service]
        Environment="HTTP_PROXY=http://cache.univ-tln.fr:3128/"
        Environment="HTTPS_PROXY=http://cache.univ-tln.fr:3128/"
   </pre>

# Docker-compose

<pre>
sudo curl -sSL https://github.com/docker/compose/releases/download/v2.23.0/docker-compose-linux-x86_64 -o /usr/bin/docker-compose && sudo chmod +x /usr/bin/docker-compose
</pre>
  

