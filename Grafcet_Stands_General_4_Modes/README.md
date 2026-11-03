# GRAFCET général Stands — quatre branches en parallèle

Une seule page Visio réunit les quatre appels du dernier export TIA Portal fourni, avec **176 étapes uniques**, 434 cas de transition et 370 variantes de messages dans 332 encarts.

## Fichiers

- [Visio 2013 modifiable (.vsdx)](Grafcet_Stands_General_4_Modes.vsdx)
- [Aperçu du diagramme (.pdf)](Grafcet_Stands_General_4_Modes.pdf)
- [Format Visio XML alternatif (.vdx)](Grafcet_Stands_General_4_Modes_editable.vdx)
- [Guide de lecture et d’édition (.pdf)](Lire_le_Grafcet_General.pdf)
- [Archive contenant tous les fichiers (.zip)](Grafcet_Stands_General_4_Modes.zip)

## Disposition et couleurs

De gauche à droite : **bleu = remplissage**, **vert = dépotage**, **orange = dépotage à l’évent**, **violet = analyse Trailer**. Chaque branche conserve l’ordre numérique de ses étapes.

Les étapes communes 0 et 10 sont uniques en haut ; 480, 490, 500, 999 et la sortie 99 affichée **9999** sont uniques en bas. Les collecteurs communs sont gris. Cette disposition représente les choix OU du programme ; elle n’ajoute aucune synchronisation ET ni priorité entre demandes simultanées.

Les traits sont des connecteurs Visio collés à des points de connexion. Les parties communes sont regroupées dans les gouttières et rails. Les commentaires de réseaux, conditions et messages SPV/IHM sont conservés. Utiliser le zoom pour lire cette grande planche vectorielle.

Pour décaler une étape horizontalement dans Visio : Pointeur (Ctrl+1), sélectionner son carré et déplacer avec les flèches. Ses annotations et raccordements suivent ; les collecteurs restent fixes.

## Contrôles

Graphe, messages, couleurs, contenu ZIP/XML, collage des extrémités et géométrie contrôlés ; 352 simulations de déplacement sur les 176 étapes réussies. VSDX et VDX ouverts par une bibliothèque indépendante en lecture seule, puis importés et rendus en PDF dans LibreOffice. Microsoft Visio n’a pas été exécuté dans cet environnement.

Les deux retours mémoire 306/316 sont développés en cas conditionnels des valeurs écrites par le programme, sans inventer un retour fixe. Le corps du FC Isii_G7 et les messages du bloc analyseur externe ne sont pas inclus dans cet export ; ces limites figurent dans le guide.

Les quatre fichiers de modes séparés restent disponibles dans le dossier voisin `Grafcets_Stands_4_Modes`.
