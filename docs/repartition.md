# Répartition et travail séparé

Les affectations nominatives ci-dessous sont proposées au groupe. Tous les membres ont du code, des vérifications et une explication technique à présenter.

## Chahid — catalogue

Possède `src/catalog.c`, `include/catalog.h` et `tests/test_catalog.c`. Développe l'ajout, la recherche par identifiant et désignation et la modification des métadonnées. Quantité initiale nulle, aucun doublon, longueurs et capacité contrôlées. Les identifiants restent stables.

Travaille avec un inventaire construit en mémoire. Son test compile uniquement avec le modèle commun et le catalogue. Livrable : montrer un ajout, une recherche réussie, un identifiant absent et le refus d'un doublon sans changement de l'état.

Relecture proposée : Boubacar.

## Boubacar — mouvements et comptage physique

Possède `src/movement.c`, `include/movement.h` et `tests/test_movement.c`. Développe entrées, sorties, correction d'inventaire et consultation de l'historique. Garantit que quantité et historique changent ensemble et que toutes les erreurs préservent l'état.

Crée directement les articles de ses tests, sans appeler le catalogue ni le lecteur de fichiers. Livrable : stock 0 → 10 → 7 → 2, sortie impossible refusée, historique plein et débordement numérique traités.

Relecture proposée : Chahid.

## Diouma — fichiers et intégrité

Possède `src/storage.c`, `include/storage.h`, `tests/test_storage.c` et `tests/fixtures/`. Définit le format versionné, écrit le parseur, vérifie les données chargées et sauvegarde sans écraser prématurément la version précédente. Son lot inclut les erreurs d'ouverture, lecture, écriture et fermeture.

Construit un inventaire cohérent dans son test pour vérifier un aller-retour. Aucun appel aux modules catalogue ou mouvements n'est requis. Livrable : état identique après sauvegarde/rechargement ; données malformées et incohérentes rejetées avec conservation de l'état actif.

Relecture proposée : Julien.

## Julien — interface et bilan

Possède `src/ui.c`, `src/report.c`, `include/ui.h`, `tests/test_report.c` et l'orchestrateur `src/main.c`. Développe tableau navigable, recherche/filtre, formulaires, messages d'erreur, liste sous seuil et choix de sauvegarde avant sortie. Les calculs du bilan restent indépendants de ncurses.

Commence avec un inventaire et des résultats d'actions simulés : il peut présenter l'IHM avant que les autres modules soient terminés. Son test du bilan ne dépend ni de ncurses ni des fichiers. Livrable : navigation et filtrage visibles, seuil correctement traité, saisie invalide conservant le programme utilisable.

Relecture proposée : Diouma.

## Travail commun et équilibre

Définir ensemble `model.h`, les signatures et les codes de résultat au début. Construire ensemble le `Makefile` et ses cibles séparées. Toute modification d'un en-tête partagé est annoncée aux personnes concernées avant fusion. Chacun documente son module et participe à une première intégration pendant la première séance.

Diouma ne récupère pas toutes les tâches de documentation et Julien ne devient pas le seul responsable des erreurs des autres modules. Si la persistance ou l'IHM dépasse le temps disponible, simplifier collectivement le périmètre plutôt que déplacer tout le travail restant vers une personne. Les bonus attendent que le scénario commun fonctionne.

## Déroulement proposé

Le cours prévoit deux séances en autonomie. Une enveloppe de huit heures est l'hypothèse de travail reprise des échanges précédents, à confirmer.

| Moment | Résultat attendu |
| --- | --- |
| Avant le développement | Validation du sujet et de l'IHM avancée par l'enseignant ; choix des responsabilités par le groupe |
| Début de première séance | Types, signatures, format des erreurs et commandes de test définis ensemble |
| Première séance | Quatre démonstrations partielles sur données d'essai ; première compilation commune avant la fin |
| Seconde séance | Scénario complet, erreurs, sauvegarde/rechargement, relecture et préparation de la démonstration |

Une branche par lot, des commits réguliers et une pull request courte par étape. Intégrer tôt ; ne pas attendre que tous les lots soient terminés pour assembler l'application. Chacun doit pouvoir expliquer ses choix et montrer son historique de travail.
