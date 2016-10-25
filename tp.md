# ARX
Fait par Axel Lheureux et Théo Plockyn

- - - 

Introduction - Budgetisation
=============

## Equipements 
Les noms d'équipements sont cliquables.  

- Switch [**TP-Link TL-SG1024D**](https://www.amazon.fr/TP-Link-TL-SG1024D-Gigabit-Rackable-Bo%C3%AEtier/dp/B003UWXFM0/ref=sr_1_1?ie=UTF8&qid=1476177479&sr=8-1) 96.99€ * 2  
- Routeur [**Cisco rv320**](http://www.ldlc-pro.com/fiche/PB00149718.html) 158.29€ 

## Abonnement internet
- Orange fibre intense 65€ HT/mois * 2

## Total
482.27€

![Architecture du réseau](./arx.png "Schéma d'architecture du réseau")

\newpage

### Explications

La plage d'adresse est en /24.  
Le routeur est configuré par défaut sur l'adresse 192.168.1.1
Le serveur sera en 192.168.1.2, les postes branchés sur le switch 1 seront sur la plage d'adresse à partir de 192.168.1.100, sur le switch 2 sur la plage à partir de 192.168.1.200 pour faciliter, lors d'un problème, la recherche physique de la machine fautive.  
Le routeur possédant une interface de gestion web, il est très aisé de la configurer.

Les requêtes entrantes sur le port 80 sont redirigées vers le serveur web. 



Les communications provenant des machines de l'entreprise comme d'Internet sont gérées par le routeur Cisco rv320.

\newpage

### Load Balance

Le routeur Cisco rv320 possède deux ports WAN et fait le load-balancing automatiquement, il suffit d'activer l'option dans l'interface d'administration

![Interface de gestion du dual WAN](./dual_wan.png "Dual WAN")

1. Cliquer sur le bouton radio correspondant au load-balancing.  

![Activation du load-balancing](./load_balancing.png "Load balancing")

2. Cliquer sur "Save". Le load-balancing est activé.

- - - 

### Configuration DHCP/DNS:

        client-router#configure terminal  
        client-router(config)#ip dhcp pool CLIENT_LAN  
        client-router(dhcp-config)#network 192.168.1.0 255.255.255.0  
        client-router(dhcp-config)#default-router 192.168.1.1  
        client-router(dhcp-config)#ip dns-server  
        client-router(dhcp-config)#ip domain-lookup  
        client-router(dhcp-config)#ip host www.localsite.com 192.168.1.2  
        client-router(dhcp-config)#ip name-server 8.8.8.8  



Pour les connexions extérieures, cela est géré lorsqu'on réserve le nom de domaine. ( Pour une configuration où on possède un seul fournisseur. Pour deux fournisseurs, nous n'avons pas trouvé la solution pour le moment )

\newpage
### Sources:
[**Lien vers IT-Connect pour DHCP/DNS**](http://www.it-connect.fr/configurer-le-service-dhcp-sur-un-routeur-cisco/)



