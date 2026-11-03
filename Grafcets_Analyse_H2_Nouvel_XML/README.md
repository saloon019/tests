# Analyse H2 — trois vues Visio 2013

Le **nouveau Fct_Shelter_Analyse_H2_FB.xml joint** est représenté dans trois fichiers indépendants, chacun sur une page. Les trois VSDX sont marqués V2 pour les distinguer de la livraison issue de l’ancien XML.

| Vue | Visio modifiable | Aperçu PDF | Étapes | Transitions |
| --- | --- | --- | ---: | ---: |
| Général complet | [VSDX](Grafcet_Analyse_H2_General_V2.vsdx) | [PDF](Grafcet_Analyse_H2_General_V2.pdf) | 34 | 76 |
| Analyse Trailer | [VSDX](Grafcet_Analyse_H2_Trailer_V2.vsdx) | [PDF](Grafcet_Analyse_H2_Trailer_V2.pdf) | 26 | 54 |
| Début / Milieu / Fin ensemble | [VSDX](Grafcet_Analyse_H2_Debut_Milieu_Fin_V2.vsdx) | [PDF](Grafcet_Analyse_H2_Debut_Milieu_Fin_V2.pdf) | 21 | 45 |

**Bleu = Trailer ; vert = Début/Milieu/Fin ; gris = commun.** Le général dispose les préparations en parallèle, l’analyse et ses résultats au centre, puis les replis et la fin commune. Chaque état source reste unique. Les vues de famille gardent une colonne numérique et les retours réels du programme.

- [Guide de lecture et d’édition](Lire_les_Grafcets_Analyse_H2.pdf)
- [Archive complète avec les trois VSDX, PDF et VDX alternatifs](Grafcets_Analyse_H2_Nouvel_XML.zip)
- [Rapport des contrôles](Validation_Grafcets_Analyse_H2.json)

Les commentaires de réseaux, les messages conditionnels IHM/SPV et les actions accompagnent les étapes. Les connecteurs sont collés à des points de connexion. Les trajets communs sont regroupés. La sortie source 99 est affichée 9999 et placée en bas.

Milieu et Fin rejoignent directement 500 ; Début possède la préparation 100 à 120. Les appels proviennent de `Ech_Stand_Analyse.Stands`, à l’étape 5. Le général conserve aussi le cas spécial stand 8. Les vues de famille excluent cet appel dédié ; elles gardent la sortie conditionnelle 500→550 du stand 8. La réceptivité originale complète de T004 est préservée dans les métadonnées du diagramme Début/Milieu/Fin.

Les conditions de 500 vers 501/502/503 restent celles du XML, avec leurs recouvrements. Aucune priorité ni exclusivité de demandes n’est ajoutée. Le reset global R61 et les actions R64/R65 sont conservés. Les conditions R50 utilisent bien `Tempo_Analyse_Q` du nouvel XML ; les six mémorisations de seuil R49 utilisent `Tempo_Stab_Analyse_Q`.

162 simulations de déplacement horizontal réussies. Textes, propriétés, couleurs, formules et connexions sont préservés dans les VDX. Lecture indépendante en bibliothèque et rendus LibreOffice des six fichiers Visio validés. Microsoft Visio n’a pas été exécuté dans cet environnement. Le corps du FC Isii_G7 n’est pas fourni dans l’export.

Utiliser le zoom pour ces grandes planches. Dans Visio, Pointeur (Ctrl+1), sélectionner le carré et utiliser les flèches gauche/droite : ses annotations et liaisons suivent, les collecteurs restent fixes.
