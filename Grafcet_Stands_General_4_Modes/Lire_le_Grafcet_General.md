# GRAFCET général Stands — quatre branches en parallèle

176 étapes uniques, 434 cas de transition dessinés, 370 messages dans 332 encarts.

- Remplissage : #23649A, lancement 10 → 20
- Dépotage : #16804A, lancement 10 → 25
- Dépotage à l’évent : #A85C00, lancement 10 → 26
- Analyse Trailer : #7B4BA4, lancement 10 → 21
- Commun : gris #596778 ; 0, 10, 99, 480, 490, 500, 999.

Une seule page, quatre colonnes parallèles dans cet ordre : remplissage, dépotage, évent et analyse Trailer. Chaque colonne conserve son ordre numérique. Les états 0/10 sont partagés en haut ; 480/490/500/999 et la sortie 99 affichée 9999 sont regroupés en bas. Aucune étape n’est dupliquée.

À 10, les quatre lancements colorés et les deux sorties communes vers 500/999 sont conservés. La disposition parallèle est une sélection OU, pas une synchronisation ET.

Les arrivées colorées sont regroupées dans les collecteurs locaux de chaque colonne, puis dans quatre rails horizontaux vers 0/480/500/999 et des collecteurs finaux gris. Le retour 0 est en haut ; les autres fusions se trouvent sous les branches. Les numéros décalés, conditions et messages du XML sont conservés.

Le manifeste parallèle contient : 5 400 formes, 52 collecteurs verticaux locaux, 4 collecteurs finaux communs, 4 rails horizontaux et 37 pistes de routage. 

Utiliser le zoom pour cette grande planche. Déplacement horizontal : Pointeur Ctrl+1, sélectionner le carré et décaler avec les flèches ; ses éléments et connecteurs suivent.

Le PDF joint décrit les retours mémoire, les messages externes et les contrôles. Les fichiers séparés précédents restent disponibles.

Source SHA256 : e7a4883f9c238457dafd0da759189fc370766387277755437b718b65bd1cd7b8
