# Architecture et contrats proposés

Ce document fixe un point de départ à valider ensemble. Les types et fonctions cités ne sont pas encore implémentés.

## État commun

| Type prévu | Champs essentiels | Propriétaire des modifications |
| --- | --- | --- |
| `Article` | Identifiant entier positif, désignation, catégorie, quantité, seuil minimal | Chahid : métadonnées ; Boubacar : quantité |
| `Mouvement` | Identifiant, article, type, quantité avant, quantité après, motif | Boubacar |
| `Inventaire` | Tableau d'articles et nombre utilisé, tableau de mouvements et nombre utilisé | Chaque module pour son opération |
| `Resultat` | Succès, argument invalide, introuvable, doublon, capacité atteinte, stock insuffisant, erreur fichier | Contrat commun |

Pour la première version, proposer des tableaux bornés : 256 articles, 2 048 mouvements, désignation de 63 octets maximum hors zéro terminal. Les autres tailles sont fixées dans `model.h` lors du démarrage. Le refus explicite d'une capacité atteinte est préférable à une allocation dynamique inutile dans ce périmètre. Une extension dynamique doit prévoir le traitement d'un échec d'allocation et la libération de la mémoire.

Les identifiants sont stables ; retirer un article n'est pas prévu. Un article est créé avec une quantité nulle : toute variation passe ensuite par un mouvement. Les chaînes sont terminées par zéro ; une saisie trop longue est refusée plutôt que tronquée silencieusement.

## Opérations par module

| Module | Entrées | Sorties et effets |
| --- | --- | --- |
| Catalogue | Inventaire, identifiant, métadonnées ou recherche | Ajout/modification/recherche, sans variation du stock |
| Mouvements | Inventaire, identifiant article, type et quantité ou comptage physique | Stock et historique modifiés ensemble, ou état strictement inchangé |
| Persistance | Chemin et inventaire | Sauvegarde ; chargement dans un état temporaire puis remplacement après validation complète |
| Bilan | Inventaire en lecture seule | Liste filtrée des articles sous seuil, sans modifier ni réordonner l'état partagé |
| IHM | Choix et saisies utilisateur | Validation de forme, appels des modules, affichage des résultats et gestion de l'état non sauvegardé |

Les signatures exactes seront regroupées dans les en-têtes avant de développer les modules. Aucune fonction métier ne lit `stdin`, n'affiche à l'écran ou ne termine le programme. Les tests appellent directement ces fonctions. Seul l'orchestrateur déclenche le chargement et la sauvegarde.

## Invariants et cas limites

- Identifiant d'article unique et positif. Seuil et quantité entiers entre 0 et `INT_MAX`.
- Entrée et sortie strictement positives. Vérifier le débordement avant une addition et le stock disponible avant une soustraction.
- Correction : fournir la quantité comptée, qui peut être zéro ; calculer et expliquer l'écart. Une quantité inchangée n'ajoute pas de mouvement.
- Préparer et valider le mouvement, y compris la place dans l'historique, avant de changer le stock. Une erreur ne doit jamais laisser une modification partielle.
- Chaque mouvement vise un article existant. Les identifiants de mouvements sont uniques et leur ordre est conservé.
- Pour chaque article, la chaîne des mouvements part de zéro ; chaque quantité « avant » égale la précédente quantité « après » ; le dernier résultat égale le stock courant. Un article sans mouvement a un stock nul.
- Une alerte signifie quantité strictement inférieure au seuil. Égalité au seuil : aucune alerte.
- Le programme propose de sauvegarder les changements avant de quitter. Une erreur de sauvegarde laisse les modifications en mémoire et signale qu'elles ne sont pas enregistrées.

## Fichier local unique

Format texte versionné proposé : première ligne `STOCK;1`, puis des lignes d'articles et de mouvements. Le format exact et un exemple complet seront livrés par Diouma avant l'intégration. Un fichier unique évite de devoir synchroniser séparément un fichier de stock et un fichier d'historique.

Le format doit préciser les champs, leurs limites et les règles de validation. Pour cette version, interdire les séparateurs et retours à la ligne dans les champs textuels ; ne pas annoncer la prise en charge générale des CSV avec guillemets. Utiliser des conversions numériques contrôlées, avec rejet d'un nombre hors plage, d'une fin de ligne tronquée ou de données supplémentaires non prévues.

Charger dans un état temporaire, vérifier références et cohérence des mouvements, puis remplacer l'état actif seulement en cas de succès. Un fichier absent au démarrage n'est pas assimilé silencieusement à un inventaire vide : offrir explicitement la création d'un nouvel inventaire.

Sauvegarder dans un fichier temporaire du même répertoire, vérifier les écritures et la fermeture, puis remplacer le fichier précédent par renommage. En cas d'erreur avant remplacement, conserver l'ancien fichier. Cela ne constitue pas une garantie de résistance à une coupure de courant. Une seule instance écrit le fichier ; le travail à quatre sur GitHub ne signifie pas quatre utilisateurs simultanés dans l'application.

## Développement indépendant

Chacun construit un petit inventaire directement en mémoire. Aucun test du catalogue, des mouvements ou du bilan ne dépend du lecteur de fichiers. Les tests de persistance construisent eux-mêmes un état valide. Les essais de l'IHM utilisent des réponses simulées dans un programme de démonstration séparé, sans remplacer les fichiers des autres membres.

En cas de tableaux volumineux, éviter de multiplier les copies sur la pile ; réserver l'état temporaire de chargement dans une zone de stockage adaptée. Les décisions sur l'emplacement de cet état sont prises lors de la définition des types.
