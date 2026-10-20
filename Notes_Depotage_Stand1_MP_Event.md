# Dépotage Stand 1 — notes fonctionnelles de revue

Version du 20 octobre 2026 · AF §§5.18.9 et 5.18.10 · compression MP / évent

Document fonctionnel à revoir. Les étapes nouvelles sont une proposition documentaire ; ce fichier ne constitue pas un programme PLC.

Le modèle comporte **63 étapes**, **137 transitions** et **77 variantes de messages** présentées dans **76 encarts**. La sortie XML 99 est affichée 9999 en bas de la planche.

## Origines et périmètre

Le tronc Stands comprend 17 étapes de 0 à 140, avec 131 et 132, 41 transitions sortantes et 28 messages. Titres, commentaires, actions locales, réceptivités et destinations sont conservés. Les étapes 480/490 et leur branche de purge sont également conservées.

Les conditions AF sont des libellés fonctionnels à implémenter. Elles ne sont pas présentées comme des adresses PLC existantes. Les numéros nouveaux n’impliquent pas l’exécution des anciens réseaux Stands portant le même numéro. Les commandes globales héritées sont recensées pour le tronc ; leur extension demande une adaptation.

La désactivation fonctionnelle du cycle de dépotage et Fct.State_Activate ne sont pas assimilées. Le forçage R100 hérité ne définit pas un retour automatique de l’extension AF avant son repli.

## Décisions utilisateur intégrées

### PV-01 — Test XML pression + débit confirmé

Décision utilisateur : conserver pression ET débit du XML, écarts absolus et égalité aux seuils acceptée. DeltaP := ABS(60PITx01 − Analyse_hist.P_etancheite), DeltaQ := ABS(60FITx01 − Analyse_hist.Q_etancheite). Comparaisons <= Delta_P_Max_etanch et <= Delta_Q_Max_etanch. Aucun pourcentage ni seuil de 10 % n’est utilisé. Activation du module à adapter à la nouvelle séquence, paramètres et critères repris du XML.

### PV-03 — Consignes MP à l’arrêt confirmées distinctes

Précision utilisateur : deux consignes distinctes, 79–84 barg au réglage initial et 75–84 barg dans la correction du détendeur. Aucun remplacement de l’une par l’autre.

## Règles d’arrêt et de surveillance

- **M1 — 14-PAH-001 OU 14-PAH-002** : Alarme immédiate, sans arrêt par ces seuls seuils.
- **M2 — 14-PAHH-001 OU perte de terre** : Arrêter le cycle MP et fermer 15-XSV-009 ; suite PV-07.
- **M3 — AU terrain ou supervision** : Fermer 15-XSV-009 et 60-XSV-008 ; suite PV-07. En évent, ces fermetures ne coupent pas le chemin manuel.
- **V1 — Perte terre pendant dépotage évent** : Alarme à l’opérateur uniquement ; aucune coupure du chemin manuel ajoutée. Surveillance maintenue pendant l’attente des fermetures de fin 810, avant désactivation 850.
- **V2 — AU du stand pendant évent** : Aucun effet d’arrêt de ce flux manuel selon l’AF ; pas de transition de coupure fictive.

Les étapes 430 et 440 ne disposent d’aucune sortie automatique. Les conditions de réarmement et de reprise restent PV-07. Le STOP déclaré du mode évent ne ferme aucune vanne manuelle.

## Mémo de pressions fourni par l’AF

| Mesure | Repères | HH | H | L | LL |
|---|---|---:|---:|---:|---:|
| Refoulement MP / PT104 | 13-PT-104-1/2/3/4 | 87 | 84 | 79 | — |
| Aspiration HP / PT102 | 15-PT-102-1/2/3 | 90 | 85 | 75 | 74 |

Toutes les valeurs sont en barg. Ce tableau constitue un mémo AF ; il ne crée aucun nouveau seuil de commande ou d’arrêt du GRAFCET.

## Interfaces et parcours particuliers

| Interface | Traitement | Origine / revue |
|---|---|---|
| 140 → 150 | La transition du XML est inchangée. Le nouveau pas 150 engage la fermeture 15-XSV-009 avant le test commun. | XML + AF .9.1/.10.1 |
| 90 → 480 → 490/500 | Rejet qualité et branche de purge du Stands conservés. Pas de renvoi autorisé 480 → 100. L’accès du trailer pollué à l’évent reste à préciser. | PV-02 |
| 10/40/50/60/70 → 500 | Annulations du préfixe vers le rapport d’origine. Les conditions et destinations sont conservées. | XML Stands |
| 230 → 140 | Après la purge de fuite, retour au raccordement du flexible, puis nouveau test. | AF .9.1/.10.1 |
| 420 → 300 | Reprise MP après décision SC et acquittement terrain, avec permissifs à définir ; retour au début de phase MP, sans nouveau test de fuite imposé. | AF .9.3 / PV-07 |
| 640 → 600 | Reprise évent après confirmations de fermeture, décision SC et acquittement terrain. Retour aux ouvertures manuelles. | AF .10.3 / PV-08 |
| 430 / 440 | États distincts de protection MP et d’AU, sans sortie automatique dans le modèle. Réarmement et arbitrage restent ouverts. | PV-07 |
| 800/810/820 → repli | Fin MP, fin évent et annulation rejoignent le repli avec les confirmations/points d’isolement propres au cas. | PV-05 / PV-06 |
| 950 → 0 | Clôture documentaire proposée. Un rapport incomplet émis à l’annulation n’est pas réémis. Le détail de cette interface reste à préciser. | PV-11 |
| R100 hérité → 0 | Le forçage du XML est présenté dans son périmètre de tronc. Son extension doit être adaptée ; elle ne doit pas court-circuiter le repli AF. | PV-11 |

## Points ouverts à valider

### PV-02 — Qualité H2 et accès au mode évent

Précision utilisateur : conserver à l’identique la branche de purge existante 90→480→490/500 ; sa suite reste à préciser pour ce cycle et pour les Stands. Aucun renvoi autorisé 480→100 n’est ajouté. L’accès d’un trailer non conforme au mode évent n’est donc pas défini par le tronc actuel. L’AF évent dit aussi « qualité conforme » malgré son titre pollué.

### PV-04 — État usine, référence MP et stabilité

Définir les informations d’état cohérentes production/compresseurs, les critères de stabilité et le traitement d’une référence 14-PIT-002 rendant la plage impossible. La référence est figée à la création du message, sans suivi continu.

### PV-05 — Fermetures de fin évent et repli

L’AF .10.5 cite trailer + 15-DB-028 alors que le débit évent traverse trailer + 60-HV-108 + 60-HR-102. Le repli commun ne ferme pas ces deux dernières vannes. Aucun remplacement silencieux ni fermeture automatique n’est supposé.

### PV-06 — Isolement MP avant repli

La fin normale exige trailer + 15-DB-028 fermées mais ne décrit pas la commande de 15-XSV-009. Confirmer l’isolement avant décompression ; aucune fermeture automatique de fin n’est ajoutée comme exigence acquise.

### PV-07 — Protections, AU et arbitrage

Réarmement/suite après PAHH ou perte MET et après AU non définis. Aucun retour automatique vers la reprise STOP. L’arbitrage de demandes simultanées reste à définir ; les commandes de fermeture prescrites sont rappelées indépendamment.

### PV-08 — Décisions opérateur et parallélisme

Après STOP évent, les demandes SC et terrain sont simultanées. Mémorisation d’un choix reçu tôt, changement de choix et priorité entre boutons simultanés à spécifier. La reprise nécessite les deux confirmations et un nouvel acquittement terrain.

### PV-09 — Repères de terre et correspondance Stand 1

L’AF mentionne 60-XSO-X01 puis 60-XSO-101 ; le tronc conserve MALT/60-XSO-x03 et les repères x du XML. Confirmer les correspondances sans réécrire le tronc importé.

### PV-10 — Pressions résiduelles et constats terrain

La cible résiduelle évent, les tolérances et durées de stabilité à zéro ne sont pas chiffrées. PG-104 est lu par l’opérateur : aucune mesure automatique de manomètre n’est créée. Le seuil <90 barg appartient seulement à la fin MP.

### PV-11 — Héritages chargement / clôture

Le préfixe conserve ses variables et messages de pression de remplissage. Confirmer leur emploi au dépotage, les commandes globales importées et la gestion des rapports/conditions de retour disponible. La clôture normale 950 est une proposition documentaire.

## Repérage des étapes nouvelles

| Étape | Intitulé | Partie | Origine | Points de revue |
|---:|---|---|---|---|
| 150 | Fermeture 15-XSV-009 avant test | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | — |
| 160 | Lignage avant test et ouverture 60-HV-109 | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | — |
| 170 | Légère ouverture trailer et stabilisation | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | — |
| 180 | Fermeture trailer — références du test | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | PV-01 |
| 190 | Test automatique pression + débit — temporisation | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | PV-01 |
| 210 | Résultat du test — critères absolus XML | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | PV-01 |
| 220 | Test NON CONFORME — séquence arrêtée | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | — |
| 230 | Purge du stand après fuite | Test d’étanchéité commun | 5.18.9.1 / 5.18.10.1 | PV-10 |
| 250 | Test conforme — confirmation du mode de dépotage | Sélection du mode | 5.18.9.1 / 5.18.10.1 | PV-02, PV-11 |
| 300 | Début de phase MP — ouverture 15-XSV-009 | Dépotage vers MP | 5.18.9.2 | — |
| 310 | Contexte production / compresseurs MP | Dépotage vers MP | 5.18.9.2 | PV-04 |
| 320 | Réglage initial — production et MP à l’arrêt | Dépotage vers MP | 5.18.9.2 | PV-03 |
| 330 | Réglage initial — compresseurs MP en fonctionnement | Dépotage vers MP | 5.18.9.2 | PV-04 |
| 340 | Pression >84 barg — préparation de correction | Dépotage vers MP | 5.18.9.2 | — |
| 344 | Préparer le message de réglage du détendeur | Dépotage vers MP | 5.18.9.2 | PV-03, PV-04 |
| 345 | Réglage du détendeur 60-PCV-103 en écoulement | Dépotage vers MP | 5.18.9.2 | PV-03 |
| 350 | Fermer les vannes de détente et confirmer la stabilité | Dépotage vers MP | 5.18.9.2 | — |
| 360 | Ouverture progressive 15-DB-028 | Dépotage vers MP | 5.18.9.2 | — |
| 370 | Absence de ralentissement — fermeture 15-DB-028 | Dépotage vers MP | 5.18.9.2 | — |
| 380 | Dépotage MP prêt / effectif | Dépotage vers MP | 5.18.9.2 | PV-10 |
| 410 | STOP MP — attente décision Salle de contrôle | Arrêts MP | 5.18.9.3 | — |
| 420 | Reprise MP décidée — information terrain | Arrêts MP | 5.18.9.3 | PV-07 |
| 430 | Arrêt de protection MP | Arrêts MP | 5.18.9.4 | PV-07, PV-09 |
| 440 | Arrêt d’urgence du Stand 1 — mode MP | Arrêts MP | 5.18.9.3 | PV-07 |
| 600 | Début de phase évent — ouvertures manuelles | Dépotage à l’évent | 5.18.10.2 | — |
| 610 | Dépotage à l’évent en cours | Dépotage à l’évent | 5.18.10.2 / 5.18.10.4 | PV-09, PV-10 |
| 620 | STOP évent déclaré — demandes en parallèle | Arrêt évent | 5.18.10.3 | PV-08 |
| 640 | Reprise évent décidée — information terrain | Arrêt évent | 5.18.10.3 | — |
| 800 | Fin MP — fermeture trailer et 15-DB-028 | Fin de dépotage | 5.18.9.5 | — |
| 810 | Fin évent — consigne de fermeture à valider | Fin de dépotage | 5.18.10.5 | PV-05, PV-10 |
| 820 | Annulation de l’opération | Fin de dépotage | 5.18.9.3 / 5.18.10.3 | — |
| 850 | Cycle désactivé — feu orange | Repli commun | 5.18.9.5 / 5.18.10.5 | — |
| 855 | Isolement avant repli — point à valider | Repli commun | 5.18.9.6 / 5.18.10.6 | PV-05, PV-06 |
| 860 | Décompression amont et aval 60-PCV-103 | Repli commun | 5.18.9.6 / 5.18.10.6 | PV-10 |
| 870 | Fermeture des vannes de repli | Repli commun | 5.18.9.6 / 5.18.10.6 | — |
| 880 | Déconnexion du flexible | Repli commun | 5.18.9.6 / 5.18.10.6 | — |
| 890 | Attente autorisation d’enlèvement SC | Enlèvement commun | 5.18.9.7 / 5.18.10.7 | — |
| 900 | Activation de la fonction d’enlèvement | Enlèvement commun | 5.18.9.7 / 5.18.10.7 | — |
| 910 | Déconnexion MET et attelage | Enlèvement commun | 5.18.9.7 / 5.18.10.7 | PV-09 |
| 920 | Feu vert — autorisation d’évacuation | Enlèvement commun | 5.18.9.7 / 5.18.10.7 | PV-09, PV-11 |
| 950 | Clôture du dossier de dépotage | Clôture | Synthèse / interface rapport | PV-11 |

## Couverture de l’analyse fonctionnelle

| Article | Étapes / règles | Représentation dans le modèle | Réserves / précisions |
|---|---|---|---|
| 5.18.9.1 / 5.18.10.1 | 150, 160, 170, 180, 190, 210, 220, 230, 250 | Fermeture XSV-009, lignage complet, préparation test, module pression + débit confirmé, résultat, purge/annulation et reprise 140. | PV-01 confirmé ; accès évent PV-02. |
| 5.18.9.2 | 300, 310, 320, 330, 340, 344, 345, 350, 360, 370, 380 | Ouverture XSV-009, contextes usine, référence MP figée, correction PCV-103, validation de pression, DB-028 et contrôle de ralentissement. | PV-03 confirmé ; PV-04. |
| 5.18.9.3 | 410, 420, 440, 820 ; règles STOP/AU | STOP ferme XSV-009 ; décision SC ; reprise acquittée ; annulation/rapport incomplet. Pause progressive manuelle documentée sans faux changement d’état BPCS. | PV-07 pour réarmements/arbitrage. |
| 5.18.9.4 | Règles M1/M2 ; 430 ; surveillance incluant 800 | PAH-001/002 : alarme seule. PAHH-001 ou perte MET : fermeture XSV-009 et arrêt de protection distinct. | PV-07 / PV-09. |
| 5.18.9.5 | 380 → 800 → 850 | Fin déclarée après constat terrain PG-104 <90 barg sans baisse ; fermeture trailer + DB-028 ; désactivation et orange. | PV-06 / PV-10. |
| 5.18.9.6 / 5.18.10.6 | 855, 860, 870, 880 | Isolement à confirmer, décompression PCV-103 amont/aval, constats zéro stable, fermetures puis déconnexion flexible. | PV-05 / PV-06 / PV-10. |
| 5.18.9.7 / 5.18.10.7 | 890, 900, 910, 920, 950 | Autorisation SC, activation terrain, déconnexion MET, attelage, feu vert et retour disponible/clôture. | PV-09 / PV-11. |
| 5.18.10.2 | 600, 610 | Ouvertures progressives trailer, HV-108 et HR-102 ; validation ; attente STOP non finalisé ou finalisé. | Chemin de débit entièrement manuel. |
| 5.18.10.3 | 620, 640, 820 | Demandes SC et terrain en parallèle ; trois fermetures confirmées ; reprise annoncée/acquittée ou annulation avec rapport incomplet. | PV-08 ; AU sans effet de coupure du flux évent. |
| 5.18.10.4 | Règle V1 ; messages 610 | Perte MET en mode évent : alarme opérateur uniquement. | Aucune transition de coupure automatique ajoutée. |
| 5.18.10.5 | 610 → 810 → 850 | Pression résiduelle constatée au PG-104, déclaration finalisée, consigne trailer + DB-028 conservée telle que fournie. | PV-05 / PV-10 avant validation de conception. |

## Contrôles de traçabilité effectués pour cette annexe

- 17 étapes de tronc : comparaison des titres, réseaux, commentaires, messages et actions locales au fichier Stands.
- 41 transitions sortantes du tronc : identités, conditions et cibles comparées à l’extraction XML.
- 28 messages du tronc conservés ; états et transitions de purge 480/490 comparés à la source.
- Absence de nouvelle transition 480→100 et de sortie automatique des états 430/440 vérifiée.
- Expressions SCL de pression/débit absolus et comparaisons <= retrouvées dans R35 ; tests logiques aux bornes effectués sans proposer de valeur de réglage opérationnelle.
- PV-01 et PV-03 confirmés ; neuf points restent ouverts.

Les contrôles graphiques, de collage et de déplacement de la planche Visio sont consignés séparément. Le corps du moteur Isii_G7 n’est pas fourni par l’export ; cette annexe ne simule pas son fonctionnement.

## Références documentaires

- AF fournie dans le message utilisateur : §§5.18.9 et 5.18.10, complétée par ses réponses sur le test et les consignes.
- Export Stands : Fct_Stands_FB.xml, tronc 0–140 et interfaces héritées identifiées.
- Modèle documentaire : extraction.json, block Depotage_Stand1_MP_Event.

Empreinte XML Stands : `2c87ed1b1c985625326edd7b7802fa9e4a7cd1e7ca18561241305103e7a89ce5`.

Empreinte interne du modèle : `533f2cf7dcac6a7ecf6846a0684efd1428dfa2ff072507308497558b729f2119`.
