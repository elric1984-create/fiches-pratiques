[Opérations de bases sur Debian.md](https://github.com/user-attachments/files/32556123/Operations.de.bases.sur.Debian.md)
Opérations de bases sous Debian

# Précautions d'installation

Penser a activer ssh et autres services nécessaires selon l'usage (ainsi
qu'a désactiver les services inutiles)

# Installation et paramétrage sudo

1.  Su -
2.  apt install && apt upgrade -y
3.  apt install sudo

## ajouter l'utilisateur au sudoers

1.  Usermod -aG sudo username

NB : cette commande permet d'ajouter un utilisateur a un groupe (pas
forcement le groupe sudo)

1.  redemarrer

# Fixer une ip

1.  Sudo nano/etc/network/interfaces
2.  le fichier doit ressembler a

\# This file describes the network interfaces available on your system

#and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/\*

\# The loopback network interface

auto lo

iface lo inet loopback

\# The primary network interface

allow-hotplug ens33

iface ens33 inet static

address 172.16.82.10/24

gateway 172.16.82.2

dns-nameservers 1.1.1.1 8.8.8.8

## Editer le fichier resolv.conf

1.  Sudo nano /etc/resolv.conf
2.  ajouter « nameserver x.x.x.x » (8 ou 1 par sécurité sauf consigne
    contraire)

# modifier les permission d'un fichier

1.  Chmod « permission(a qui, modif,droit) » « nom de fichier »

2.  À qui s\'applique le changement rwx

    -   *u* (*******u******ser*, utilisateur) représente la catégorie
        \"propriétaire\" ;
    -   *g* (*******g******roup*, groupe) représente la catégorie
        \"groupe propriétaire\" ;
    -   *o* (*******o******thers*, autres) représente la catégorie
        \"reste du monde\" ;
    -   *a* (*******a******ll*, tous) représente l\'ensemble des trois
        catégories.

3.  La modification que l\'on veut faire

    -   *+* : ajouter
    -   *-* : supprimer
    -   *=* : affectation

4.  Le droit que l\'on veut modifier

    -   *r* : *******r******ead* → lecture

    -   *w* : *******w******rite* → écriture

    -   *x* : *e******x******ecute* → exécution

    -   *X* : *e******X******ecute* → exécution, concerne uniquement les
        répertoires (qu\'ils aient déjà une autorisation d\'exécution ou
        pas) et les fichiers qui ont déjà une autorisation d\'exécution
        pour l\'une des catégories d\'utilisateurs. Nous allons voir
        plus bas dans la partie des traitements récursifs l\'intérêt
        du *X*.

        1.  1.  1.  ##### []{#anchor}En octal

En [octal](https://fr.wikipedia.org/wiki/Systeme_octal), chaque «
groupement » de droits (pour *user*, *group* et *other*) sera représenté
par un chiffre et à chaque droit correspond une valeur :

-   *r* (*******r******ead*) = *4*
-   *w* (*******w******rite*) = *2*
-   *x* (*e******x******ecute*) = *1*
-   *-* = *0*

Par exemple,

-   Pour *rwx*, on aura : 4+2+1 = *7*
-   Pour *rw-*, on aura : 4+2+0 = *6*
-   Pour *r\--*, on aura : 4+0+0 = *4*

Ce qui permet de faire toutes les combinaisons :

-   *0* : *****\-\--***** (aucun droit)
-   *1* : *****\--x***** (exécution)
-   *2* : *****-w-***** (écriture)
-   *3* : *****-wx***** (écriture et exécution)
-   *4* : *****r\--***** (lecture seule)
-   *5* : *****r-x***** (lecture et exécution)
-   *6* : *****rw-***** (lecture et écriture)
-   *7* : *****rwx***** (lecture, écriture et exécution)

1.  
