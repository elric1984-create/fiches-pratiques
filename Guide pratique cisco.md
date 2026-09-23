[parametrage switch.md](https://github.com/user-attachments/files/32555710/parametrage.switch.md)
Parametrage vlan

On a stick

# paramétrage sur le switch

##  Numérotation et nommage des vlan

1.  1.  En
    2.  conf t
    3.  vlan (numéro de vlan)
    4.  name (nom de vlan)
    5.  exit

A répéter autant de fois qu'il y a de vlan (penser a la vlan de service)

##  Assignation des vlan a leur interfaces 

1.  int (interface du vlan)
2.  sw mode access
3.  sw acces vlan (numéro de vlan)

A répéter autant de fois que nécessaire

## Mise en place du lien entre vlan et routeur

1.  Int (interface vers routeur)
2.  sw mode trunk
3.  sw trunk allowed vlan (numéros de vlan séparés par des virgules)

# Paramétrage routeur

1.  En
2.  int G0/0.numéro vlan
3.  encapsulation dot1Q numéro de vlan
4.  ip address (gateway de vlan)
5.  ip helper-address (ip serveur dns)
6.  exit
7.  reproduire aussi souvent que nécéssaire
8.  int g0/0
9.  no shutdown
10. exit
11. ip routing

# Parametrage communication vlan routeur

##  Configuration Vlan de service

1.  Conf T
2.  int vlan(numéro du vlan de service)
3.  ip address (ip dispo sur vlan de service) masque sous réseau
4.  no shutdown
5.  exit
6.  ip default-gateway (gateway du vlan de service)

paramétrage svi (switch type 3)

**

# *Création de la table de routage*

******Switch(config)**********\#**********ip routing**

******Switch(config)#******exit**

******Switch#******show ip route**

(configurer les ip des postes cliens selon la table préalablement
établie)

# Création de vlan

Se pratique comme pour une config on a swtich

# Création des interfaces svi

******Switch********\#**** conf t**

******Switch(config********)#**** int vlan **(N° de la première vlan)**

******Switch(config-if)********\#**** ip address **(ip masque)**

******Switch(config-if)********\#**** int vlan **(N° de la seconde
Vlan)**

******Switch(config-if)********\#**** ip address **(ip masque)**
