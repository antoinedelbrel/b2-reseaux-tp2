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

* 