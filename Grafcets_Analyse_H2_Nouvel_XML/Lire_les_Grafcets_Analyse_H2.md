# Lire les GRAFCETs Analyse H2

Trois fichiers Visio 2013 éditables représentent le bloc Fct_Shelter_Analyse_H2_FB à partir du nouvel export XML fourni. Chaque diagramme tient sur une seule grande page, avec les transitions, les liaisons regroupées et les messages près des étapes.

| Vue | Étapes | Transitions | Variantes de message | Encarts |
| --- | ---: | ---: | ---: | ---: |
| Général complet | 34 | 76 | 56 | 48 |
| Trailer | 26 | 54 | 38 | 33 |
| Début / Milieu / Fin | 21 | 45 | 26 | 20 |

## Choisir la vue

Le général montre toutes les possibilités du bloc. Les deux vues par famille isolent l’analyse Trailer et l’ensemble Début/Milieu/Fin. Les nombres de messages comptent les variantes conditionnelles IHM et SPV ; plusieurs variantes peuvent partager un encart.

## Suivre le général par phases

Les étapes 0 et 5 sont en haut. La préparation Trailer 10 à 40 est en bleu à gauche ; la préparation Début 100 à 120 est en vert à droite. Elles rejoignent l’analyse commune 500 à 508, en gris au centre. Les retours de résultat repartent vers le repli Trailer 50 à 90 à gauche, ou vers 130 à droite pour Début/Milieu/Fin. La fin 550, le défaut 999 et la sortie 9999 sont au centre en bas. Chaque étape source apparaît une seule fois.

## Couleurs et symboles

Bleu = famille Trailer ; vert = famille Début/Milieu/Fin ; gris = commun. Les étapes communes restent grises dans les trois fichiers. Les liaisons portent la couleur de leur famille et rejoignent des collecteurs partagés gris. Carré = étape ; barre = transition ; branche simple = OU. La disposition en parallèle n’ajoute aucune synchronisation ET. Les points pleins marquent les jonctions ; un croisement avec un blanc ne relie pas les traits.

## Lire et déplacer dans Visio

Les deux vues par famille suivent une colonne en ordre numérique ; les retours ascendants restent dessinés. Les titres de réseaux et les popups conditionnels accompagnent les étapes. La sortie affichée 9999 correspond à l’étape source 99, conservée dans les données. Utiliser le zoom. Pour décaler une étape horizontalement : outil Pointeur (Ctrl+1), sélectionner le carré puis flèches gauche/droite. Les annotations et raccordements locaux suivent ; les collecteurs restent fixes.

## Appels et parcours réels

La sélection est à l’étape 5, dans Ech_Stand_Analyse.Stands : H2_Trailer lance 10 ; H2.Debut lance 100 ; H2.Milieu et H2.fin lancent directement 500. Milieu et Fin n’ont aucune étape exclusive. Sous Synchro_OK, chacun des résultats 505/506/507/508 renvoie vers 50 si Trailer, ou vers 130 si Début/Milieu/Fin. Les demandes ne viennent pas de la structure Parametres du bloc Stands.

## Périmètre des vues et cas stand 8

Le général conserve les 76 transitions locales et T004 complète : 5→500 sous Milieu, Fin, ou Fct.State_Run ET Num_stand = 8 ET NON Dde_Analyse. La vue Trailer exclut les appels Début, Milieu/Fin et l’appel spécial stand 8. La vue Début/Milieu/Fin exclut l’appel Trailer et restreint T004 aux deux clauses Milieu/Fin ; la condition complète reste dans condition_source. Les trois vues gardent la sortie T051 : 500→550 sous Fct.State_Run ET Num_stand = 8 ET Dde_Analyse. Les transitions vers les étapes de l’autre famille sont exclues des vues filtrées.

## Conditions, messages et actions préservés

En R50, les branches 500→501/502/503 ne sont pas rendues artificiellement exclusives : aucune priorité de fonctionnement n’est inventée. La règle globale de retour à 0 de R61 est conservée intégralement. Les actions de R64 sur les résultats 505 à 508 et de R65 sur Cde_60XVx04 et FinAnalyse restent présentes. À 503, le général conserve les quatre messages ; chaque vue de famille garde ses deux variantes IHM/SPV. Les autres messages des étapes retenues gardent leurs conditions et textes source. La nouvelle version utilise Tempo_Analyse_Q en R50 et Tempo_Stab_Analyse_Q pour les six seuils de R49.

## Source et contrôles

La logique vient du nouveau XML joint Fct_Shelter_Analyse_H2_FB.xml, dont l’empreinte SHA-256 a été vérifiée. Les modèles, connexions et déplacements horizontaux sont contrôlés ; la lecture indépendante et le rendu LibreOffice ont été validés. Microsoft Visio n’a pas été exécuté dans cet environnement. Les fichiers VDX alternatifs et les aperçus PDF accompagnent les VSDX.

## Source XML — SHA-256

`afd04bcdf513eb9935f635555ed7d8cf57a9d924697ccca7d0a76f890b0fcfbd`
