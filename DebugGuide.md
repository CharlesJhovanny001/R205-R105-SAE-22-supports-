# Commande Linux
## Guide Debug Sous Linux
 ### 1. Vérifier l'état de sa carte réseau


```
    sudo mii-tool enp0s31f6

```

``mii-tool`` permet de vérifier si il existe un line avec la carte réseau.
si il n'y en n'a pas le teminal affichera ceci : 


```
    sudo mii-tool enp0s31f6
enp0s31f6: no link
```
l'état de notre carte réseau est **DOWN**
ainsi la commande suivante permetra de la rendre ip dans l'état **UP** :
```
    ip link set UP enp0s31f6

```
### 2. Configuration IP
On peut maintenant vérifier si il existe une adresse ip sur notre carte réseau :
```
    ip address 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s31f6: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether b0:7b:25:26:9b:88 brd ff:ff:ff:ff:ff:ff

```
Si il existe déja une address ip on peut la supprimer grâce à : 

```
    ip adress flush dev enp0s31f6
```

Ajoutons maintenant une adresse Ip et un masque correspond a l'adresse du réseau ici le réseau sera `10.202.0.0/24` 

```
    ip addr add 10.202.8.1/24 dev enp0s31f6
 ```

### 3. Configuration Table De Routage

Vérifions si il existe une route par default : 

```
   ip route 
   
```
De même si il existe déja une route par default ou même une autre route on peut la supprimer grâce à : 

```
ip route flush dev enp0s31f6

```

Ajoutons maintenant une route par défault  _Cette route permet de ne pas ajouter chaque route à la main c'est à dire si notre pc ne connait pas l'adresse de destination il passera par cette route automatiquement ainsi on peut communiquer avec tous les pc si l'on ajoute l'adresse de la passerelle_




















## Comparaison Commandes Linux,Windows
|Sous Linux|Sous Windows|
|--------|--------|
| `ip addr show`   |`ipconfig`   | 
|`ip address add dev ` **eno1** |    D    |
|`ip address flush dev`  **eno1** |    `ipconfig /release interface`   |
 `ping`  **Ip**    |     `ping`  **Ip**    |
| `ip route`  |    `route`    |
|`traceroute`  **IP**  |    `tracert`  **Ip**   |
|    ` cat /etc/resolv.conf` |    `ipfconfig /all`    |
|    `nslookup` |       `nslookup` |
|       `ip link show` |    B    |
|    C    |    D    |
|    A    |    B    |
|    C    |    D    |
|    A    |    B    |
|    C    |    D    |
|    A    |    B    |
|    C    |    D    |
|    A    |    B    |
|    C    |    D    |
|    A    |    B    |
|    C    |    D    |
|    A    |    B    |
|    C    |    D    |
|    A    |    B    |
|    C    |    D    |

