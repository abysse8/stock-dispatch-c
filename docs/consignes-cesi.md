# Consignes CESI et preuves attendues

Source consultée : copie locale du parcours « Outils de programmation – Langage C », module A3 FISA S3E 2026–2027, dans `Documents/cesi/scenari/OUTILS_DE_PROGRAMMATION_-_LANGAGE_C/module.md`. La consultation de cette copie ne confirme pas une éventuelle modification ultérieure du cours.

## Obligations vérifiées dans la copie du cours

| Exigence | Réponse prévue | Preuve à fournir au rendu |
| --- | --- | --- |
| Groupe de 3 à 4 ; tâches explicites et contributions équilibrées | Quatre membres avec responsabilités techniques propres | Répartition adoptée, code et commits de chacun |
| Sujet libre validé avant démarrage | Proposition inventaire/stock | Accord de l'enseignant à obtenir |
| Application cohérente et fonctionnelle | Cycle article → mouvement → comptage → sauvegarde | Démonstration complète |
| Structures adaptées, manipulation par référence | `Article`, `Mouvement`, `Inventaire` | Types et fonctions utilisant leurs adresses |
| Pointeurs sur variables, tableaux, structures ou fonctions | Paramètres de structures et parcours de tableaux | Code expliqué en soutenance ; pointeurs sur fonctions non imposés |
| `malloc/free` si nécessaire | Tableaux bornés proposés | Limites vérifiées ; mémoire libérée si extension dynamique |
| Lecture et écriture de fichiers | Fichier local versionné | Aller-retour et vérification du contenu |
| Erreurs d'ouverture et de fermeture | Propagation des erreurs de persistance | Cas d'erreur et messages compréhensibles |
| Fonctionnalité avancée, exemples IHM/embarqué/réseau | IHM ncurses avec navigation et filtres | Acceptation de cette proposition puis démonstration |
| Fonctions claires, conventions, commentaires pertinents | Modules à responsabilités limitées | Relecture croisée et architecture documentée |
| Absence d'erreurs à la compilation et à l'exécution | Compilation avec avertissements, tests et essai interactif | Résultats effectivement exécutés à consigner |
| Git/GitHub tout au long du projet, commits explicites | Branches par lot et intégration progressive | Historique réel du développement |
| README : sujet, objectifs, architecture, compilation, exécution, dépendances | README initial à actualiser à mesure du développement | Commandes utilisables sur un clone neuf |
| Soutenance : démonstration, architecture, choix, questions | Scénario du README et présentation par chacun | Application fonctionnelle et explications personnelles |

Le cours confirme deux séances en autonomie. Il ne précise pas dans ce texte la date de rendu ni la durée de la soutenance. Les huit heures évoquées par l'équipe sont une hypothèse de préparation, pas une durée explicitement inscrite dans cette source.

## Retour de l'ancien projet

Le fil de courriel « Projet Main robotisee » du 28 octobre 2026 contient le lien du dépôt pan-tilt et des notes de ChatGPT transmises par Julien : risque d'inégalité entre missions, dépendance au matériel et importance des interfaces testables séparément. Ces notes sont un retour de réflexion, pas des consignes de l'enseignant.

La décision de quitter ce projet parce qu'il ne convenait pas au travail séparé a été confirmée par Julien dans la présente préparation. Les courriels ne sont pas reproduits dans le dépôt. Le nouveau découpage prévoit des données en mémoire pour chaque lot et une intégration précoce.

## Points encore à décider

- Accord enseignant sur le sujet et sur l'IHM terminal comme fonctionnalité avancée.
- Adoption des affectations proposées par les quatre membres.
- Sens métier éventuel du « dispatch » ; il n'ajoute aucune fonctionnalité au minimum tant que ce besoin n'est pas précisé.
- Dates, modalités de soutenance et règles éventuelles sur l'assistance par IA. La copie consultée ne fixe pas de règle sur cette assistance.
