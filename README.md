# b2-reseaux-tp2 

## I. Simplest setup

* Les VPCS sont configurés avec les bonnes Ips.

```
PC-1> ping 10.2.1.2
84 bytes from 10.2.1.2 icmp_seq=1 ttl=64 time=0.962 ms
84 bytes from 10.2.1.2 icmp_seq=2 ttl=64 time=1.973 ms
84 bytes from 10.2.1.2 icmp_seq=3 ttl=64 time=2.008 ms
```
* Le ping fonctionne.

* Sur la table wireshark on obtient :   
`29	47.627398	Private_66:68:01	Private_66:68:00	ARP	64	10.2.1.2 is at 00:50:79:66:68:01`

* Lorsqu'on fait un ping de PC2 a PC1 pour la première fois, la table ARP de PC2 ne connait pas encore l'adresse mac de PC1 donc il y aura une requete ARP sur sa broadcast. On peut voir ensuite une réponse à la requête pour indiquer à quelle adresse MAC appartient l'adresse IP demandé par le ping.  

* Le switch n'a pas besoin d'ip car il ne communique pas via le protocole IP mais via le protocole ethernet.

* Elles ont besoin d'une IP pour se ping car pour pouvoir ping une autre machine, la machine en question a besoin d'une adresse mac et grace a l'ip elle pourra connaitre l'adresse mac.  

## II. More switches  

```
PC-3> ping 10.2.2.1
84 bytes from 10.2.2.1 icmp_seq=1 ttl=64 time=2.126 ms

PC-3> ping 10.2.2.2
84 bytes from 10.2.2.2 icmp_seq=1 ttl=64 time=37.044 ms
84 bytes from 10.2.2.2 icmp_seq=2 ttl=64 time=5.078 ms
```  
Les PCs se ping bien.  

```
IOU1#show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----
   1    0050.7966.6801    DYNAMIC     Et0/1
   1    0050.7966.6802    DYNAMIC     Et0/0
   1    aabb.cc00.0120    DYNAMIC     Et0/0
   1    aabb.cc00.0310    DYNAMIC     Et0/2
   1    aabb.cc00.0320    DYNAMIC     Et0/0
Total Mac Addresses for this criterion: 5
```  
Voila ce qu'on obtient en faisant un `show mac address-table`.  
* Chaque adresse MAC est relié a des ports différends, les ports ET0/1 ... correspondent au protocole ethernet de chaque switch.  


``` 
Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Desg FWD 100       128.1    Shr
Et0/1               Desg FWD 100       128.2    Shr
Et0/2               Desg FWD 100       128.3    Shr
Et0/3               Desg FWD 100       128.4    Shr
Et1/0               Desg FWD 100       128.5    Shr
Et1/1               Desg FWD 100       128.6    Shr
Et1/2               Desg FWD 100       128.7    Shr
Et1/3               Desg FWD 100       128.8    Shr
```

Le switch 2 est donc le root bridges.

``` 

Interface           Role Sts Cost      Prio.Nbr Type
------------------- ---- --- --------- -------- --------------------------------
Et0/0               Desg FWD 100       128.1    Shr
Et0/1               Altn BLK 100       128.2    Shr
Et0/2               Root FWD 100       128.3    Shr
Et0/3               Desg FWD 100       128.4    Shr
Et1/0               Desg FWD 100       128.5    Shr
Et1/1               Desg FWD 100       128.6    Shr
Et1/2               Desg FWD 100       128.7    Shr
```

Le switch a un port bloquer pour éviter une storm broadcast.
