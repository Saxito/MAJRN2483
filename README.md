# Mise a Jour de la carte RN2483 et envoie des paquets avec minicom

Ceci est un tutoriel pour mettre a jour le firmware de la carte RN2483 avec le logiciel de lora et de Microship.
Nous expliquerons aussi comment envoyer des paquets sur le serveur CampusIOT avec Minicom.

## MAJ

Premierement vous devez installer le logiciel Lora "Development Suite" suivant votre OS :

https://www.microchip.com/wwwproducts/en/RN2483

Dans l'onglet Document/Software

### Installation 

Sur le même site vous devez aussi telecharger le firmware de votre choix (1.03, 1.04, 1.05)
Ensuite lancer Lora Development Suite :

Si votre device contient deja un firmware et que vous voulez mettre a jour, le logiciel doit le detecter automatiquement.
Si votre device n'as aucun firmwre vous devez cocher la case : Bootloader Mode.

Vous devez voir ceci quand vous allez dans l'onglet DFU

![alt text](https://github.com/Saxito/MAJRN2483/blob/master/Docs/lorasuite.png)

Ensuite vous devez choisir une BAUD à 9600 et non 57600 comme écrit dans la documentation. 8 bits de debis / 1 bits stop et pas de bits de parité.
Choisissez votre firmware et lancer la mis à jour. Ceci peut durer pendant plusieurs minutes il ne faut pas s'inquieter.


## Envoie des Paquets

### Pré-Requis : Minicom

Pour gerer votre port serial, il vous faut un logiciel de gestion de port serie, personellement j'utilise minicom qui est bien personalisable.

```
 $ sudo apt-get install minicom
```

Quand l'installation est terminé lancé :

```
 $ minicom -s
```

### Utiliser Minicom

Pour pouvoir dialoguer avec votre RN2483, vous devez configurer le port serie : donc allons dans l'onglet "Configuration du port serie"
Nous avons donc une fenetre comme ceci :

![alt text](https://github.com/Saxito/MAJRN2483/blob/master/Docs/minicom_config_serie.png)

Nous allons donc regarder quel port serie est notre carte en utilisant :

```
 $ dmesg
```
Par exemple pour moi c'est USB0 donc dans port serie il faut noter : /dev/ttyUSB0

Dans Débit/Parité/bits il faut mettre 57600 8N1

Contrôle du flux matériel :Non
Contrôle du flux logiciel : Non

Ensuite il faut sortir de minicom. Nous nous retrouvons sur un ecran noir. 

Nous allons donc acceder aux réglage avec CTRL+A - Z
Il faut activer "Local echo" avec la touche E qui permet de voir ce que nous ecrivons.
Il faut aussi activer  "Add carriage return" avec la touche U
et activer "Ajouter LF" avec la touche A 

### Envoie des paquets avec minicom

Dans ce tutoriel, il est supposé que vous avez deja ajouter ce device dans le serveur Lora ou d'autre plateforme. (si ce n'est pas le cas je vous invite a regarder le tuto suivant : https://github.com/CampusIoT/tutorial/blob/master/loraserver/README-app.md)

Il faut donc joindre le serveur IOT :

```
 $ mac join otaa
```
Appuyer ensuite sur la touche Entrée puis CTRL+J pour envoyer la commande. Normalement nous devons recevoir

```
 $ ok
 
 accepted
```

Si ce n'est pas le cas essayer la commande suivante et recommencer.

```
 $ mac set dr 0
```

Ensuite pour envoyer un paquet il faut executer :

```
 $ mac tx cnf/uncnf 1 "votre message en hexa"
```
Par exemple si je veux envoyer un paquet confirmer sur le port 2 et envoyer 123A 
```
 $ mac tx cnf 2 123A
```
et nous recevons :
```
 $ ok
 mac_tx_ok 
```