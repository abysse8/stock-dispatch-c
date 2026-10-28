# Tâches à reprendre dans GitHub

Ces fiches sont prêtes à servir de descriptions d'issues. Elles ne correspondent pas encore à des issues créées ou à des comptes GitHub assignés. Propriétaires proposés, à confirmer par l'équipe.

## T0 — Validation et contrat commun — tous

- Obtenir la validation du sujet et de l'IHM avancée.
- Choisir les affectations ; figer types, bornes, signatures et codes de résultat.
- Créer le Makefile avec cibles indépendantes ; convenir d'un format de fichier versionné.
- Critère d'acceptation : chacun sait construire ses données en mémoire et compiler son lot sans attendre les autres.

## T1 — Catalogue — Chahid

- Implémenter ajout, recherches et modification des métadonnées.
- Vérifier identifiant, doublons, longueurs et capacité.
- Critère : ajout et recherche réussis ; erreur sur doublon, article absent et capacité atteinte ; aucun changement en cas d'erreur.
- Cible prévue : `make test-catalog`.

## T2 — Stock, comptage et historique — Boubacar

- Implémenter entrées, sorties et corrections avec motif.
- Maintenir la cohérence stock/historique et refuser les dépassements.
- Critère : scénario 0 → 10 → 7 → 2 ; sortie de 8 depuis 7 refusée ; quantité négative, débordement et historique plein sans modification partielle.
- Cible prévue : `make test-movement`.

## T3 — Persistance — Diouma

- Décrire le format et fournir des fichiers valides/invalides dans `tests/fixtures/`.
- Charger dans un état temporaire et sauvegarder avant remplacement du fichier précédent.
- Critère : aller-retour identique ; fichier absent, tronqué, version inconnue, doublons, référence absente et historique incohérent signalés ; erreur d'écriture laissant l'ancien fichier intact.
- Cible prévue : `make test-storage`.

## T4 — IHM et alertes — Julien

- Développer une interface ncurses avec tableau navigable, filtre et formulaire.
- Afficher les articles sous seuil et l'historique ; rendre les erreurs visibles.
- Proposer de sauvegarder avant de quitter ; conserver l'état si la sauvegarde échoue.
- Critère : essai interactif sur données simulées puis réelles ; seuil strict vérifié automatiquement hors IHM ; annulation d'une saisie sans mouvement.
- Cible prévue : `make test-report` et essai manuel de l'IHM.

## T5 — Intégration et démonstration — tous

- Réaliser une première intégration pendant la première séance.
- Exécuter le scénario du README, puis fermer/recharger et comparer.
- Compiler depuis un clone neuf ; corriger le README selon les commandes réelles.
- Critère : tests des quatre lots réussis, scénario commun reproductible, limitations documentées et chaque membre capable de présenter sa partie.

## Extensions, après le minimum

Choisir une seule extension utile si le temps le permet : export d'un bilan, tri supplémentaire, ou affectation de sorties à une personne/projet si ce besoin est confirmé. Chaque extension doit avoir son responsable, son critère de réussite et un coût compatible avec l'intégration. Aucun de ces bonus ne remplace l'IHM avancée sans accord de l'enseignant.
