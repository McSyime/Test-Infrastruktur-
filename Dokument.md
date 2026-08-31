# Mise en place d'une infrastructure de teste

## Einleitung 

Dans le cadre du projet demandé, Je souhaite élaborer un projet technique à mettre en place sur mon lieu de travail. Ce projet consiste à la mise en place d'une infrastructure de teste avec des appareils comme des serveurs et des Switchs dans une première phase. 

## Le besoin 

Ce besoin vient du fait, qu'au sein de mon équipe, nous manquons de connaissances sur notre réseau car il est simplement pas accessible pour nous. Tout ce qui concerne nos équipements serveurs et réseau passent par le BIT. Or nous avons au sein de cette équipe des compétence informatique largement suffisante pour développer nos systèmes. Avec cette infrastructure de teste, nous pourrions mettre en place un système de Monitoring spécifique à nos besoins. C'est à dire Monitoré les services, les ports et les protocoles qui nous intéressent en fonction de nos besoins. 

Il faut aussi prendre en compte que le BIT est là pour mettre en place des solutions définitives, mais ils ne sont malheureusement pas tout le temps à notre disposition pour résoudre nos problèmes et cela peut parfois prendre énormément de temps. Tellement de temps que certains projets finissent par être abandonnés. Avec cette initiative, nous pourrions étudier nos systèmes dans une infrastructure sécurisé sans risqué de compromettre la sécurité de notre réseau de travail. 

## Objectifs 

Pour rester simple, j'attribue 3 objectifs dans ce projet qui permettront d'évaluer mon idée : 

1. Définition de l'architecture réseau
2. Définition des éléments à surveiller
3. Prototypes d'automatisations de l'infrastructure

## Définition de l'infrastructure réseau 

Dans le schéma suivant, J'illustre l'infrastructure hardware minimale pour pouvoir effectué le Monitoring et les automatisations. Etant donné que nous n'avons pas accès aux règles Firewall, je n'en utiliserai pas dans ce prototype car il n'est pour l'instant pas relevant pour le Monitoring et l'automatisation de nos besoins. 

![Infrastruktur Schema](Infrastruktur_Schema.png)

Nous distinguons 4 réseaux différents basés sur l'adresse privée 192.168.x.x / 24. 

### Netzwerk 1

Le réseau 192.168.10.1 accueillera les solutions de Monitoring. Il peut communiquer avec le Netzwerk 2 par le router central ainsi qu'avec le ou les PC admin qui sont sur le réseau 192.168.40.1 /24. 

### Netzwerk 2 

Sur la même base que le réseau 1, il y a un Switch et deux serveurs de testes. Les serveurs de tests peuvent communiquer avec la passerelle ainsi que les PC admins. Cela est nécessaire pour l'automatisation ou l'envoi de logs au serveur Infra pour qu'il puisse faire ce qu'on va lui demander. Il y a également une PDU (Power Distribution Unit) qui n'est pas sur le même réseau que les deux serveurs de testes. Cela a été fait ainsi car dans notre exploitation, les deux types d'équipements ne sont pas sur le même réseau. Cette PDU a été intégrée au projet car il y a également des possibilités de Monitoring et d'automatisation pertinente. A noter que cela implique une configuration de port sur le Switch du réseau 2. LA PDU doit être atteignable uniquement depuis le réseau 1. 

### PC Admin 

Le PC admin a accès à tous les réseaux et tous les appareils qui s'y trouvent afin de pouvoir effectuer les configurations nécessaires. 

### Router 

Le Router intègre évidemment les 4 réseaux dont nous avons besoin. Je souhaite limiter au maximum les échange entre le réseau 1 et 2 afin de ne laisser passer que ce que je veux traiter. Il en va de même pour la PDU. Afin de définir ces règles, je souhaite configurer une machine Linux disposant de deux ports LAN pour y connecter les Switch des réseaux 1 et 2. De cette manière, les deux réseaux sont séparées physiquement et je pourrai par exemple mettre en place des règles ACL à l'aide de nftables et des tables de routages.












