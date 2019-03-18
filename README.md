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

Vous devez voir ceci quand vous allez dans l'onglet ???DFU???

Ensuite vous devez choisir une BAUD de 9600 et non 57600 comme écrit dans la documentation. 8 bits /1 bits stop et pas de bits de parité.
Choisissez votre firmware et lancer la mis à jour. Ceci peut durer pendant plusieurs minutes il ne faut pas s'inquieter.


### Envoie des Paquet

### Pré-Requis : Minicom

Pour gerer votre port serial, il vous faut un logiciel de gestion de port serie, personellement j'utilise minicom qui est bien personalisable.

```
 $ sudo apt-get install minicom
```

Quand l'installation est terminé lancé :

```
 $ minicom -s
```

## Utiliser Minicom

Pour pouvoir dialoguer avec votre RN2483, vous devez configurer le port serie : donc allons dans l'onglet "Configuration du port serie"
Nous avons donc une fenetre comme ceci :

Mettre photo de minicom

![alt text](https://github.com/Saxito/MAJRN2483/Docs/minicom_config_serie.png)


### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With