# Lire les quatre GRAFCET Stands

FB modifié — livraison du 3 novembre 2026

Les quatre fichiers Visio décrivent le même export Fct_Stands_FB.xml, séparé selon ses quatre demandes de lancement. Ils conservent les étapes réellement utilisées par chaque mode, leurs sauts et les sorties communes. Aucune règle provenant de l’ancienne analyse fonctionnelle n’est ajoutée au nouveau programme.

## Demandes de lancement à l’étape 10

| Mode | Bit de la structure statique Parametres | Départ |
| --- | --- | --- |
| Remplissage | Parametres.Dde_Remplissage_Trailer | 10 → 20 |
| Dépotage | Parametres.Depotage.Dde_Depotage | 10 → 25 |
| Dépotage à l’évent | Parametres.Depotage_Event.Dde_Depotage_Event | 10 → 26 |
| Analyse Trailer | Parametres.Dde_Analyse_Trailer | 10 → 21 |

La supervision écrit ces demandes. Le réseau R8 contient ensuite quatre bobines RCoil qui remettent les demandes à FALSE sous la garde commune du réseau. Le mode ne doit donc pas être suivi en maintenant artificiellement un bit de demande à TRUE : ce sont les étapes décalées qui portent le parcours engagé.

Le dépotage et le dépotage à l’évent exigent également Num_Stand = 1 au lancement. Les gardes du réseau R8 ne rendent pas les quatre demandes mutuellement exclusives. Les graphiques n’ajoutent ni verrou d’exclusivité ni priorité entre des demandes simultanées.

## Contenu des quatre planches

| Mode | Étapes | Barres / chemins dessinés | Variantes de messages | Encarts |
| --- | --- | --- | --- | --- |
| Remplissage | 63 | 177 | 130 | 105 |
| Dépotage | 58 | 127 | 118 | 111 |
| Dépotage à l’évent | 62 | 134 | 118 | 112 |
| Analyse Trailer | 14 | 32 | 16 | 16 |

Le remplissage développe les deux destinations indirectes de reprise en plusieurs cas conditionnels ; son nombre de barres est expliqué page 3. Les messages strictement identiques pour une même étape et une même condition sont regroupés en un encart, en conservant leurs canaux et références.

## Étapes décalées et frontières entre modes

| Mode | Étapes du début propres au parcours |
| --- | --- |
| Remplissage | 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120, 130, 131, 132, 140 |
| Dépotage | 25, 35, 45, 55, 65, 75, 85, 95, 105, 115, 125, 133, 135, 137, 145 |
| Dépotage à l’évent | 26, 36, 46, 56, 66, 76, 86, 96, 106, 116, 126, 134, 136, 138, 146 |
| Analyse Trailer | 21, 31, 41, 51, 61, 71, 91 |

Ces listes sont numériques ; elles ne supposent pas que chaque étape rejoint automatiquement la suivante. Toutes les liaisons suivent les réceptivités et destinations réellement écrites dans le XML.

Les quatre partitions couvrent exactement les 176 étapes référencées : 169 n’appartiennent qu’à un mode, et 7 sont communes aux quatre : 0, 10, 99, 480, 490, 500 et 999. Les étapes communes figurent dans chacun des fichiers qui les utilise ; additionner les quatre tableaux ne donne donc pas le nombre d’étapes uniques du FB.

## Quelques sauts qui donnent le sens des parcours

| Saut / parcours | Lecture conservée |
| --- | --- |
| 140 → 150 | Fin du début commun du remplissage, puis séquence de remplissage. |
| 145 → 600 | Fin du début commun décalé du dépotage, puis séquence spécifique de dépotage. |
| 146 → 800 | Fin du début commun décalé de l’évent, puis séquence spécifique de dépotage à l’évent. |
| 71 → 91 | Analyse Trailer hors cycle de remplissage : appel de la séquence d’analyse sans importer les étapes de mise en teneur du remplissage. |
| Retour 0 / 10 | Une nouvelle demande correspond à un nouveau choix de mode. La recherche de parcours s’arrête à cette frontière ; elle ne déroule pas les trois autres lancements. |

## Lecture graphique et provenance

Chaque Visio contient une seule grande page en colonne, avec un carré par étape, les transitions et les collecteurs communs par destination. Les branches simples sont des OU. Les points pleins marquent les jonctions ; les croisements entourés de blanc ne sont pas reliés. Les barres et textes restent éditables.

Les numéros de mode sont conservés : par exemple 25, 35, 45… pour le dépotage et 26, 36, 46… pour l’évent. Comme dans les livraisons précédentes, la sortie source 99 est affichée 9999 tout en bas, avec son identité XML 99 conservée dans les données de la forme.

Un titre de réseau partagé peut citer plusieurs variantes d’étapes ou plusieurs modes. Il est conservé comme commentaire de provenance ; les carrés présents sur la planche sont ceux du mode sélectionné. Les étapes 133 et 134 sont bien présentes, même si le titre du réseau R23 ne cite que 130.

## Retours mémoire du remplissage : 306 et 316

Le réseau R59 écrit G7.G_X_New := G7_G_X_mem depuis 306 ou 316 sous validation IHM. Il ne s’agit pas d’un retour fixe vers 260. La mémoire est Int Retain ; elle n’est pas une mémoire de sélection entre les quatre modes.

Pour rendre les sauts visibles, chacun des deux MOVEs indirects est développé en onze branches conditionnelles. Chaque branche garde la réceptivité d’origine et ajoute le cas G7_G_X_mem = destination. Les destinations documentées sont :

0, 240, 250, 260, 270, 280, 290, 300, 305, 306, 310.

Les dix valeurs non nulles correspondent aux étapes déclarées dans la plage de sauvegarde 240…310 de R6. La valeur 0 est réellement écrite par R251. La garde du retour ne l’exclut pas. Son affichage est une projection documentaire, pas une preuve qu’une reprise vers zéro est atteignable dans un cycle complet.

Ainsi, le remplissage comporte 157 transitions agrégées dans l’audit abstrait ; remplacer 2 retours indirects par 22 cas donne 177 barres / chemins dessinés. Les lignes de ces cas sont regroupées dans une grille de trois transitions sous 306 et 316 pour garder la colonne lisible.

Le domaine complet n’est pas prouvé : une valeur retenue initiale ou une valeur d’étape non référencée dans la plage pourrait être différente de la liste affichée. Le corps du FC Isii_G7 n’est pas fourni et la garde du retour ne contrôle pas ce domaine. Cette vérification reste distincte de la restitution graphique.

## Messages popups et données des formes

L’extraction couvre 242 écrivains Message Ladder et 370 variantes conditionnelles locales : 185 IHM et 185 SPV. Elle reprend les SCL préparatoires, les concaténations Ladder et leurs ajouts successifs. Les cas de pression à 640, les compléments de messages à 650 et les temporisations 632/832 sont conservés.

Aux étapes 90, 91, 95 et 96, ce FB n’écrit pas de popup local propre à l’analyse. Le réseau R255 donne priorité aux messages du bloc analyseur externe. Le fichier Analyse Trailer représente ses 14 étapes de gestion dans le FB Stands ; il ne remplace pas le GRAFCET interne de l’analyseur et ne reprend pas les anciens messages Shelter comme s’ils venaient du nouveau XML.

Les données de forme conservent les réceptivités complètes, le réseau d’origine, les expressions sources, les textes intégraux et les conditions de chaque message. Les alias et la suppression de l’en-tête répétitif ne concernent que l’affichage. Les séquences de test spécifiques du nouveau code, dont 631–634 et 831–834, sont restituées telles quelles.

## Écarts entre titres et code conservés à la lecture

| Repère | Constat dans le nouvel export | Restitution |
| --- | --- | --- |
| R23 / 133–134 | Le titre de réseau ne mentionne que 130 ; les contacts et les statuts référencent aussi 133 et 134. | Les deux étapes décalées sont représentées. |
| 853 | Le titre annonce un saut vers 854, mais le MOVE écrit 860. | Liaison 853 → 860. |
| 870 | Le titre annonce 870, mais le MOVE écrit 871. | Liaison 870 → 871. |
| 860 | Le titre annonce une décision Salle de contrôle ; les choix vers 861/862 utilisent les réponses IHM %X0/%X1. | Les conditions IHM restent celles du XML. |

Ces différences sont signalées sans modifier le programme ni corriger silencieusement ses conditions ou ses destinations. La portée fonctionnelle de ces choix se vérifie dans le programme source.

## Déplacer une étape dans Visio

1. Activer l’outil Pointeur avec Ctrl+1.
2. Sélectionner le carré de l’étape, puis le décaler horizontalement, par exemple avec les flèches gauche/droite.
3. Les transitions, conditions, commentaires et encarts suivent le carré ; les connecteurs restent collés à leurs points. Les collecteurs partagés restent fixes.

Les quatre côtés des carrés possèdent des points de connexion. Le suivi repose sur des formules ShapeSheet natives, sans macro. Les parcours sont conservés ; il ne s’agit pas d’une redistribution automatique globale de toutes les formes autour d’un obstacle.

## Vérifications et identification de la source

| Mode | Déplacements simulés | Connecteurs contrôlés | Collecteurs fixes |
| --- | --- | --- | --- |
| Remplissage | 126 | 568 | 26 |
| Dépotage | 116 | 441 | 14 |
| Dépotage à l’évent | 124 | 467 | 14 |
| Analyse Trailer | 28 | 111 | 6 |

Total : 394 simulations, chaque carré déplacé de −0,5 puis +0,5 pouce. Les dépendances, points de collage, coudes orthogonaux et marques de croisement sont contrôlés par un évaluateur indépendant. Les VDX préservent les textes, propriétés, connexions et formules ; ils sont lus par Aspose Diagram en lecture seule, sans sauvegarde SDK.

Microsoft Visio n’a pas été exécuté dans cet environnement. Les vérifications des formules et de la structure du fichier ne sont pas une exécution du programme automate ni du FC Isii_G7.

Source : Fct_Stands_FB.xml, 256 réseaux (139 LAD / 117 SCL), 176 étapes référencées.
SHA-256 du fichier reçu :
e7a4883f9c238457dafd0da759189fc370766387277755437b718b65bd1cd7b8
