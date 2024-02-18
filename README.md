# Intro

L'ONU FS (XGS-ONU-25-20NI) a une limite de 17 VLAN mappable sur le bridge. Ceci peut donc poser problème dans le cas ou l'OLT remonte une quantité supérieur à 17 VLAN.

Cet ONU est trouvable ici : https://www.fs.com/fr/products/185594.html

Un ensemble de source sur l'ONU sont trouvable ici : https://hack-gpon.org/xgs/ont-fs-XGS-ONU-25-20NI/

Ceci n'est pas un tuto de comment faire une req DHCP avec prio 6 sur VLAN832. Les informations ne sont ici que pour configurer un ONU afin que celui puisse recevoir du trafique de l'OLT et émettre.

Vous briquez vos ONU ? J'en ai rien à faire, pas mon souci :p


# Explication du problème

L'ONU est bien limité à 17 VLAN rules. Aucunes des deux personnes ayant réussi à faire fonctionner l'ONU sur ce forum ont l'option TV.
L'option TV prend 6x 840VLAN rules + 3x 838VLAN rules.
Ceci explique la différence de quantité de VLAN rules. 13 VLAN rules pour eux, 22 pour moi (13 + 6 + 3 = 22).

Hors, les VLAN 838 et 840 sont envoyés par l'OLT avant le VLAN 832. Le VLAN 832 se retrouve donc non mappé sur le bridge car étant la 19ème règle envoyé (au delà de 17). Il devient donc impossible de passer des trams sur le vlan832.

> [!note]
> 95% des personnes avec une offre Orange sont donc concerné par ce souci. Le mod de l'ONU ayant été fini, celui-ci vous permettra d'avoir une ligne fonctionnel avec cet ONU


## Cas numéro 1 => vous n'avez pas l'option TV

Etant limité à environ 13 VLAN, vous ne devriez pas avoir le souci et donc une simple configuration du module sera suffisante.


## Cas numéro 2 => vous avez l'option TV

Etant fort probablement à plus de 22 VLAN, vous devriez avoir le souci et donc une simple configuration du module ne sera pas suffisante.
Il vous faudra donc faire un peu plus que de la simple configuration.


# Résolution du problème

~~Un mod + configuration de l'ONU ont/sont réalisé. Je donnerais plus d'info à ce sujet une fois stable.~~

Le mod est disponible et la marche à suivre renseigné ici.


# Bonne pratique

Changer directement les valeurs serial, vendor et hardware version sur l'ONU ne sont pas recommandé. En effet, dans le cas de RMA, il vous sera nécessaire de faire un revert.
De même, l'ONU possède un ensemble de fichiers de config qui permettent de remplacer dynamiquement ces valeurs, sans avoir à changer les valeurs par défaut. Cette méthode est donc grandement privilégié et conseillé.

Un ONU doit avoir un failsafe qui permet de retourner à l'état initial en cas de brick ou de mauvaise configuration. Le mod qui est utilisé pour configurer l'ONU permet de faire, via un double power cycle de moins de 30 à 120sec, une remise en état d'usine de l'ONU.
Ceci permet de limité énormément les bricks involontaire par mauvaises manipulations. Cela permet aussi de facilement remettre l'ONU en réglage usine (Il suffit de faire un double power cycle de moins de 120sec).
Ce failsafe est encore en court d'amélioration.


# Modification de l'ONU

## Liste des nécessaires

La version 1.1 du mod est disponible ici : [rssor mod v1.1](https://github.com/rssor/fs_xgspon_mod/releases/tag/v1.1)
Les explications (English) sont disponible ici : [readme](https://github.com/rssor/fs_xgspon_mod/tree/test_bruteforce_and_orange_support)

Il vous faudra connaitre le serial de l'ONU. Pour cela le plus simple est d'en faire la demande auprès de fs.com.
Dans le cas ou vous auriez oublié, il existe un sous module au mod qui permet de trouvé ce serial en une 20ene de seconde ([Récupération du serial](#r%C3%A9cup%C3%A9ration-du-serial-brut-force))

## Installation du mod

Vous assurez d'être sur une machine hôte de l'ONU. Vous aurez besoin d'une adresse sur le réseau `192.168.100.0/24`. Vous aurez aussi besoin d'avoir une règle firewall qui permet à l'ONU d'accéder au port 8172 sur l'adresse que vous aurez choisi sur le réseau `192.168.100.0/24`.
L'ONU est accessible sur l'IP `192.168.100.1`

Dans notre cas, ISP orange les commandes à faire sont les suivantes.


### Installation

> [!important]  
> => Dans le cas où vous n'êtes pas sûr d'avoir moins de 17 règles de vlan à mapper

```
./fs_xgspon_mod.py install GPONXXXXXXXX orange SMBSXXXXXXXX
```
> Ou `GPONXXXXXXXX` est le sérial d'origine de l'ONU fs.com et `SMBSXXXXXXXX` le serial de la livebox

> reboot de l'ONU (press enter)

> [!important]  
> => Dans le cas où vous êtes sûr d'avoir moins de 17 règles de vlan à mapper

```
./fs_xgspon_mod.py install GPONXXXXXXXX orange SMBSXXXXXXXX --vlan_rules ""
```
> Ou `GPONXXXXXXXX` est le sérial d'origine de l'ONU fs.com et `SMBSXXXXXXXX` le serial de la livebox

> reboot de l'ONU (press enter)


### Vérification

#### Vendor, serial, hardware version

```
./fs_xgspon_mod.py telnet SMBSXXXXXXXX
```
> Ou `SMBSXXXXXXXX` le serial de la livebox

puis

```
/s/m/show 256
/s/m/show 257
```
C'est deux commande devraient permettre d'afficher le serial, vendor et hardware version pour vérification des bonnes valeurs (en hexa).

#### Reg status

```
/traffic/pon/show onu
```
> ------------------------- ONU INFO --------------------------
>
> Onu id 26
>
> sdThreshold:   0
>
> sfThreshold:   0
>
> TO1:   80000
>
> TO2:   1
>
> eqd:   XXXXXXXX
>
> Serial Number(vendor code): SMBS
>
> Serial Number(sn):          XXXXXXX
>
> Password:                   XX XX XX XX XX XX XX XX XX XX
>
> Registration ID:           0xXXXXXXXXXXXXXXXX0000000000000000000000000000000000000000000000000000000000
>
> ------------------------- INFO END --------------------------

#### Status O5

```
/traffic/pon/show link
```
> ----------------- LINK STATE -----------------
>
> Operation State Machine: OPERATION (O5)
>
> ----------------- STATE  END -----------------

#### VLAN

```
/system/mib/show 506
```

> EntityID                  = 0x0101
>
> OuterPriFilter            = 15
>
> OuterVidFilter            = 4096
>
> OuterTPIDFilter           = 0
>
> InnerPriFilter            = 8
>
> InnerVidFilter            = 832
>
> InnerTPIDFilter           = 5
>
> EtherTypeFilter           = 0
>
> AniBriPortNum             = 2
>
> RmTagTreat                = 1
>
> OuterPriTreat             = 15
>
> OuterVidTreat             = 0
>
> OuterTPIDTreat            = 0
>
> InnerPriTreat             = 8
>
> InnerVidTreat             = 2800
>
> InnerTPIDTreat            = 2

> EntityID                  = 0x0101
>
> OuterPriFilter            = 15
>
> OuterVidFilter            = 4096
>
> OuterTPIDFilter           = 0
>
> InnerPriFilter            = 8
>
> InnerVidFilter            = 835
>
> InnerTPIDFilter           = 5
>
> EtherTypeFilter           = 0
>
> AniBriPortNum             = 6
>
> RmTagTreat                = 1
>
> OuterPriTreat             = 15
>
> OuterVidTreat             = 0
>
> OuterTPIDTreat            = 0
>
> InnerPriTreat             = 8
>
> InnerVidTreat             = 835
>
> InnerTPIDTreat            = 2

> ...

#### Mapping VLAN

```
/traffic/eth/show connect all
```

> US BRIDGE 65535
>
> ---------------------------------------------------------------
>
> INDEX = 0, SLOT = 1, PORT = 4, VLANFILTER = 832 PRIFILTER = 0x1
>
>     VLAN MATCH : MATCH
>
>     VLAN ACT   : REPLACE
>
>     OUT  VID   : 2800
>
>     OUT  PRI   : 0
>
>     TCI MAPPING:
>
>                 * PRI 0  -> FLOW 1
>
>                 * PRI 1  -> FLOW 0
>
>                 * PRI 2  -> FLOW 0
>
>                 * PRI 3  -> FLOW 0
>
>                 * PRI 4  -> FLOW 0
>
>                 * PRI 5  -> FLOW 0
>
>                 * PRI 6  -> FLOW 0
>
>                 * PRI 7  -> FLOW 0


### Persistance des modifications

> [!warning]
> A ne faire que si les étapes précédentes sont OK

```
./fs_xgspon_mod.py persist SMBSXXXXXXXX
```

> Ou `SMBSXXXXXXXX` le serial de la livebox


### Cron pour rearm

> [!warning]
> A ne faire que si les étapes précédentes sont OK

```
./fs_xgspon_mod.py rearm SMBSXXXXXXXX
```

> Ou `SMBSXXXXXXXX` le serial de la livebox

Il s'agit ici de mettre en place un job cron pour rearm l'ONU. Ceci à pour but de re-armer le mod en cas de failsafe (double coupure de courant, 2 reboot rapide successif, ...). Dans mon cas, ce job est fait via opnsense toutes les 5mins.


## Récupération du serial (brut force)

```
sudo ./fs_xgspon_mod.py discoverserial_cig
```


# Mise en pratique et matériel

OpnSense

X710-DA2 (l'ONU n'est accessible que lorsque la fibre est enfiché)

MC220L  (l'ONU est accessible avec/sans fibre enfiché)


# OpenSense

## Cron Job template
Ajout d'un template de tache cron pour rearm le module.
> `cd /usr/local/opnsense/service/conf/actions.d/`
>
> `nano actions_onu_rearm.conf`

```
[reload]
command:/opt/onu/fs_xgspon_mod.py
parameters:rearm %s
type:script_output
message:Rearm ONU (%s)
description:Rearm ONU
```

> `service configd restart`

Pour tester
> `configctl -d onu_rearm reload GPONXXXXXXXX`
>
> `tail -500f /var/log/configd/configd_YYYYMMDD.log`

## Cron job usage
Ajout d'une nouvelle tache cron dans opnsense.

![image](https://github.com/akhamar/orange-xgs-pon/assets/32886437/61dd5c21-74fe-4b95-94a7-cad5f631aba8)

La valeur a mettre est celle du serial d'origine GPONXXXXXXXX (et non SMBSXXXXXXXX comme sur la capture)
![image](https://github.com/akhamar/orange-xgs-pon/assets/32886437/2061ddff-481e-470e-872e-eef234fa24eb)


# Remerciements

- rss (rssor)
- lama

PS: je ne répond pas aux mails, aux messages privés et je ne fais pas la cuisine à votre place.
