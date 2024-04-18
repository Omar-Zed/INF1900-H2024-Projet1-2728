## INF1900-H2024-Projet1-2728
Projet 1 de génie logiciel à Polytechnique Montréal pour le cours INF1900. Le repertoire contient les fichiers de laboratoire des deux équipes ainsi que les fichiers du projet final en plus d'un fichier LisezMoi.txt (très aproximatif).

# Objectif Principal du Projet Intégrateur
L'objectif principal de ce projet intégrateur est de concevoir et programmer deux robots capables de collaborer pour accomplir une série de tâches sur une table rectangulaire.

L'épreuve finale consiste en une série d'étapes où les robots doivent se déplacer, collecter des données, les échanger et afficher des informations sur un PC. L'accent est mis sur le respect des requis techniques et la qualité des techniques utilisées plutôt que sur la rapidité d'exécution. En cas d'erreur pendant l'épreuve, une seule reprise par robot est autorisée.


# Rôle Spécifique de Chaque Robot
Dans ce projet, chaque robot a un rôle spécifique bien défini :

## Robot 1
Le Robot 1 sera placé dans une boîte rectangulaire positionnée à l'extrémité gauche d'une table rectangulaire. La boîte possède une ouverture d'environ 10-15 cm permettant au robot, s'il est centré dans la boîte et face à l'ouverture, de faire face au centre de la table. Il sera positionné au centre de la largeur de la boîte, mais n'importe où le long de sa longueur.

Le premier objectif du Robot 1 est de localiser le centre de la boîte et de s'y déplacer. Ensuite, il doit s'orienter vers l'ouverture de la boîte en utilisant un capteur de distance.

## Robot 2
Le Robot 2 sera placé sur un parcours rectangulaire ou une bande sera collée, pointant vers la boîte du Robot 1. Pendant l'épreuve, des bandes supplémentaires seront ajoutées aux parties horizontales du parcours, pointant vers l'intérieur du parcours. Ces bandes auront des longueurs fixes de 4,5, 6,5 ou 8,5 pouces et seront espacées d'au moins 9 pouces.

Le Robot 2 sera positionné juste au-dessus de la bande extérieure du parcours, pointant vers la boîte du Robot 1. Son objectif est de parcourir le parcours en suivant le tracé des bandes. Une fois qu'il a parcouru toutes les bandes jusqu'à atteindre la bande extérieure, il doit se positionner dessus pour faire face au Robot 1 en utilisant un capteur de suivi de ligne.

Après que chaque robot est positionné, le Robot 2, équipé d'une LED infrarouge, doit transmettre les informations du parcours au Robot 1, qui dispose également d'un capteur d'ondes infrarouges. Le Robot 1 utilisera ces informations pour redessiner le parcours à l'aide de caractères Unicode et se dessiner lui-même à sa position initiale.


# Choix de l'Architecture à Base de Machines à États
Dans notre équipe, nous avons opté pour une architecture à base de machines à états pour la programmation des robots, notamment pour le Robot 2. Voici les raisons de ce choix :

  Précision de la Localisation : Une machine à états permet une distinction précise de la position du robot au moment où il traite les informations des capteurs. Le Robot 2 peut se trouver dans différentes situations tout en captant les mêmes informations avec ses capteurs. L'utilisation d'une machine à états nous permet de gérer ces situations de manière précise et adéquate.
  Gestion des Mesures : Le Robot 2 effectue des mesures tout au long du parcours en utilisant différents compteurs logiques sur le microprocesseur. Pour gérer efficacement ces mesures, il était nécessaire de répartir les étapes du parcours sur différentes parties de la machine à états du robot.

En résumé, l'utilisation d'une architecture à base de machines à états nous permet de gérer de manière précise et efficace les différentes situations rencontrées par le Robot 2 tout au long de son parcours, ainsi que de gérer les mesures effectuées pendant ce parcours de manière appropriée.


# Gestion des Interactions entre les Deux Robots
Pendant l'exécution du projet, les interactions entre les deux robots sont gérées en utilisant la communication infrarouge. Voici comment cela fonctionne :

  Protocole SIRC : Nous avons utilisé le protocole SIRC (Sony Infrared Remote Control) pour la communication entre les robots. Ce protocole consiste à générer une onde infrarouge à une fréquence spécifique, qui dans notre cas est de 38 KHz.
  Transmission des Données : Chaque donnée transmise commence par un signal de démarrage (start) qui consiste en une fréquence de 38 KHz pendant 2,4 millisecondes, suivi d'une période de 600 microsecondes pendant laquelle la LED infrarouge est éteinte. Ensuite, les données sont transmises sous forme de 7 bits binaires, suivies de leur CRC (Cyclic Redundancy Check) sur 5 bits. Le CRC permet de vérifier l'intégrité des données transmises.
  Encodage des Bits : Pour encoder les bits, le robot génère une fréquence infrarouge à 38 KHz pendant 1,2 millisecondes pour représenter un bit logique 1, et pendant 600 microsecondes pour représenter un bit logique 0. Lorsque le capteur infrarouge reçoit un signal à 38 KHz, il interprète cela comme un bit logique 0 pendant toute la durée de la fréquence.

En résumé, la communication entre les deux robots pendant l'exécution du projet est réalisée en utilisant le protocole SIRC avec une modulation infrarouge à 38 KHz. Cette méthode permet d'assurer une transmission fiable des données entre les robots tout en garantissant l'intégrité des informations transmises grâce au CRC.



# Principales Difficultés Rencontrées et Solutions Apportées
Le développement de ce projet a été confronté à plusieurs difficultés majeures, mais nous avons réussi à les résoudre grâce à différentes approches :

  Intégration des Parties du Projet : La principale difficulté résidait dans l'intégration des différentes parties du projet. Chaque composant fonctionnait individuellement, mais les faire fonctionner ensemble n'était pas trivial. Nous avons résolu ce problème en révisant attentivement chaque partie et en nous assurant que les différentes parties communiquaient correctement entre elles.
  Gestion des Compteurs Binaires : Nous avons rencontré des problèmes liés à l'utilisation des compteurs binaires dans différentes parties du projet. Parfois, les mêmes compteurs étaient utilisés plusieurs fois, ce qui entraînait des dysfonctionnements si les registres de contrôle n'étaient pas correctement réinitialisés. Pour résoudre ce problème, nous avons revu notre utilisation des compteurs et avons mis en place des procédures de réinitialisation rigoureuses.
  Variations des Conditions d'Essais : Les conditions d'essais pouvaient varier en fonction de l'emplacement du robot et de l'éclairage ambiant. Par exemple, la présence de néons dans certaines salles de laboratoire émettant de l'infrarouge pouvait fausser les résultats. Pour pallier cela, nous avons effectué des tests dans différentes conditions et avons ajusté nos algorithmes en conséquence.
  Problèmes Matériels : Les problèmes matériels étaient également fréquents, notamment au niveau des moteurs et des connexions électriques. Nous avons dû apporter des ajustements constants pour garantir le bon fonctionnement des moteurs et vérifier régulièrement l'état des câbles et des connexions. De plus, nous avons identifié que le niveau de charge des piles alimentant le pont en H pouvait affecter les performances du robot, et nous avons pris des mesures pour maintenir une alimentation stable.

En résumé, en surmontant les obstacles liés à l'intégration des différentes parties du projet, en améliorant la gestion des compteurs binaires, en adaptant nos algorithmes aux variations des conditions d'essais et en résolvant les problèmes matériels, nous avons réussi à développer un système fonctionnel et robuste pour notre projet intégrateur.


# Technologies de Communication Entre les Robots et le PC
La communication entre les robots et le PC repose principalement sur les technologies suivantes :

  Communication USB : Le PC communique avec les robots via une connexion USB. Cette connexion est utilisée exclusivement pour programmer la carte mère des robots en langage C/C++ à l'aide d'Avrdude. Cependant, il est à noter que l'utilisation d'Avrdude pour programmer les cartes Atmel n'est pas toujours optimale et a entraîné des dysfonctionnements chez certaines équipes, malgré les précautions prises.
Malgré les défis rencontrés avec Avrdude, cette méthode de programmation reste couramment utilisée pour sa compatibilité avec les microprocesseurs Atmel et sa facilité d'utilisation avec les systèmes de développement Arduino.

En résumé, la communication USB entre le PC et les robots est essentielle pour la programmation des microprocesseurs et constitue un élément clé du processus de développement du projet.


# Améliorations Futures et Réflexions Post-Projet
À ce stade, aucune amélioration future n'est envisagée pour le projet, car celui-ci est maintenant terminé et les robots ont présenté le comportement attendu. Actuellement, nous sommes le lendemain du projet, après avoir passé trois jours intenses à Poly (du lundi 15/04/2024 à 7h au mercredi 17/04/2024 à 10h, heure de passage).

Ces trois jours ont été mémorables, et malgré la fatigue, j'ai vécu des moments exceptionnels avec les autres étudiants. Nous avons partagé des moments d'entraide, de stress, de désespoir, de joie et de fatigue. Ce projet a été une expérience enrichissante qui m'a beaucoup appris sur le travail en ingénierie, sur les interactions humaines, sur le travail d'équipe et sur moi-même.

En seulement trois jours, nous avons acquis des enseignements précieux que plusieurs années pourraient difficilement transmettre. À présent, j'attends avec impatience les résultats du projet et j'espère recevoir le prix du meilleur parcours (je mettrai à jour cette information si je le reçois). En attendant, je retourne me concentrer sur la préparation de mes examens finaux.
