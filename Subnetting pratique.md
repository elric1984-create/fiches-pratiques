[Subnetting pratique.md](https://github.com/user-attachments/files/32555323/Subnetting.pratique.md)
Subnetting pratique

  --------------- ------------ ----------- ----------- ----------- ---------- ---------- --------- ---------
  Puissance       2\^7         2\^6        2\^5        2\^4        2\^3       2\^2       2\^1      2\^0
  N° d\'address   128          64          32          16          8          4          2         1
  N° poste        126 postes   62 postes   30 postes   14 postes   6 postes   2 postes   1 poste   0 poste
  Broadcast       127          63          31          15          7          3          1         0
  Masque          .128         .192        .224        .240        .248       .252       .254      .255
  --------------- ------------ ----------- ----------- ----------- ---------- ---------- --------- ---------

  ------ ----- ---- ---- ---- --- --- ---- ---
  Bits   128   64   32   16   8   4   2    1
  .128   1     0    0    0    0   0   0    0
  .192   1     1    0    0    0   0   0    0
  .224   1     1    1    0    0   0   0    0
  .240   1     1    1    1    0   0   0    0
  ------ ----- ---- ---- ---- --- --- ---- ---

  ------ ----- ---- ---- ---- --- --- ---- ---
  Bits   128   64   32   16   8   4   2    1
  .128   1     0    0    0    0   0   0    0
  .192   1     1    0    0    0   0   0    0
  .224   1     1    1    0    0   0   0    0
  .240   1     1    1    1    0   0   0    0
  ------ ----- ---- ---- ---- --- --- ---- ---

\
Le masque appartient au réseau

Broadcast = mettre a 1 les bits étant a 0 après (a droite) les bits du
masque

Séparer un réseau

10.0.0.0/16 divisé en 60 égaux\
emprunter 6 bits

Pour diviser un réseau en tranches égales, voir le nombre de postes
requis, choisir le bit correspondant (exemple 120 postes \> bit 128 \>
emprunt des 7 bits suivants)

broadcast dernier octet impairs et réseau en pair

10,0,0,0/22

Divisions en sous réseaux egaux

raisonement

on divise en x réseaux\
on commence par chercher le nombre de bits empruntés

N est le nombre de réseaux

2^x^≥N

Nouveau CIDR = ancien CIDR+N

Nombre réel de réseaux = 2^N^

Nombre d'adresse du bloc (réseau+host+broadcast)=2^(32-nouveau\ CIDR)^

**🎯 MÉTHODE RAPIDE : \"LE BON BLOC\"**

**Principe**

Pour trouver l\'adresse réseau avec un CIDR non classique (ex: /27, /17,
/21), il faut trouver le **\"bloc\"** dans lequel se trouve l\'IP.

**Technique en 3 étapes**

**ÉTAPE 1 : Identifier l\'octet concerné**

-   /8 à /16 → 2ème octet
-   /16 à /24 → 3ème octet
-   /24 à /32 → 4ème octet

**ÉTAPE 2 : Calculer la taille du bloc**

**Formule rapide** : Bloc = 256 - valeur du masque dans l\'octet
concerné

**ÉTAPE 3 : Trouver le multiple**

Diviser la valeur de l\'octet par la taille du bloc, prendre la partie
entière, multiplier par le bloc.

**ÉTAPE 4 : Trouver le broacast**
ajouter le wildcard a l'adresse réseau, attention ajouter la valeur du premier octet broadcast au dernier octet de la partie réseau

  ---------- ----------------- ------------ ------------ ------------------------------- ----------------
  **CIDR**   **Masque**        **Bloc**     **Hôtes**    **Binaire (derniers octets)**   Wildcard
  /8         255.0.0.0         16 777 216   16 777 214   00000000.00000000.00000000      0.255.255.255
  /9         255.128.0.0       8 388 608    8 388 606    10000000.00000000.00000000      0.127.255.255
  /10        255.192.0.0       4 194 304    4 194 302    11000000.00000000.00000000      0.63.255.255
  /11        255.224.0.0       2 097 152    2 097 150    11100000.00000000.00000000      0.31.255.255
  /12        255.240.0.0       1 048 576    1 048 574    11110000.00000000.00000000      0.15.255.255
  /13        255.248.0.0       524 288      524 286      11111000.00000000.00000000      0.7.255.255
  /14        255.252.0.0       262 144      262 142      11111100.00000000.00000000      0.3.255.255
  /15        255.254.0.0       131 072      131 070      11111110.00000000.00000000      0.0.255.255
  /16        255.255.0.0       65 536       65 534       11111111.00000000.00000000      0.0.255.255
  /17        255.255.128.0     32 768       32 766       11111111.10000000.00000000      0.0.127.255
  /18        255.255.192.0     16 384       16 382       11111111.11000000.00000000      0.0.63.255
  /19        255.255.224.0     8 192        8 190        11111111.11100000.00000000      0.0.31.255
  /20        255.255.240.0     4 096        4 094        11111111.11110000.00000000      0.0.15.255
  /21        255.255.248.0     2 048        2 046        11111111.11111000.00000000      0.0.7.255
  /22        255.255.252.0     1 024        1 022        11111111.11111100.00000000      0.0.3.255
  /23        255.255.254.0     512          510          11111111.11111110.00000000      0.0.1.255
  /24        255.255.255.0     256          254          11111111.11111111.00000000      0.0.0.255
  /25        255.255.255.128   128          126          11111111.11111111.10000000      0.0.0.127
  /26        255.255.255.192   64           62           11111111.11111111.11000000      0.0.0.63
  /27        255.255.255.224   32           30           11111111.11111111.11100000      0.0.0.31
  /28        255.255.255.240   16           14           11111111.11111111.11110000      0.0.0.15
  /29        255.255.255.248   8            6            11111111.11111111.11111000      0.0.0.7
  /30        255.255.255.252   4            2            11111111.11111111.11111100      0.0.0.3
  /31        255.255.255.254   2            2\*          11111111.11111111.11111110      0.0.0.1
  /32        255.255.255.255   1            0            11111111.11111111.11111111      0.0.0.0
                                                                                         
                                                                                         
                                                                                         
                                                                                         
  ---------- ----------------- ------------ ------------ ------------------------------- ----------------
