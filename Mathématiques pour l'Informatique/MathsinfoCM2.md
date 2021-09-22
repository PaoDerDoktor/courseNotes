# Comment l'aléatoire intervient en Informatique

## Définitions

le hasard est un concept exprimant l'impossibilité de prévoir avec certitude un fait quelconque :
- **Imprévisibilité** : quel résultat va-t-on avoir ?
- **Imprédictibilité** : est-ce qu'un événement `x` a se produire ?
  
Un **Aléa** est une tournure imprévisible que peut prendre un évènement

Une **Expérience aléatoire** est une expérience :
- Dont on ne peut pas prévoir le résultat à l'avance
- Qui s'oppose au **déterminisme**.
  
Un **cadre déterministe** (/le déterminisme) est un cadre qui permet de connaître *absolument toutes* les données d'une expérience, et donc d'en connaître le résultat àl'avance. En pratique, c'est rarement le cas même en laboratoire, où l'on réduit le nombre de données au maximum.

## L'aléatoire : bon ou mauvais ?

Au début, l'aléatoire était combattu car l'imprévisibilité et l'imprédictibilité sont considérées gênantes :
- Erreurs dans les programmes
- Cas à traiter imprévus
- Résultats différents d'une fois à l'autre
- ...

Aujourd'hui, on *recherche* et *développe* l'aléatoire pour différentes raisons :
- L'imprévisibilité est bonne pour les simulations
  - Tests de programmes, logiciels
  - Jeux-vidéos
  - Prévisions météo
  - Modélisations (catastrophes, accidents...)
  - ...
- L'imprédictibilité est bonne pour la cryptographie
  - On évite le *rejeu* dans une transaction sécurisé
  - Les données échangées ressemblent à de l'aléatoire (moins de risques de fuite)
  - ...
- ...

## Les trois aléatoires de Jean-Paul Delahaye

**Il n'ya pas de *mauvais* aléatoire, *tout* aléatoire peut trouver son utilisation**.

Jea-Paul Delahaye distingue 3 niveaux de hasard :

1. Aléatoire faible pour la simulation
   - Complètement déterministe (on peut connaître le résultat à l'avance)
   - mixte (déterministe et aléa)
2. Aléatoire moyen pour la cryptographie
   - Chiffrement
   - Signature
3. Aléatoire fort pour l'informatique théorique
   - Calculabilité, complexité
   - Théorie de l'information
  
## Obtenir de l'aléatoire

- Générateurs pseudo-aléatoire
  - Générateurs congruentiels linéaires (Randu, Pascal, ``rand()``...)
  - Mersenne twister (Utilisé dans les langages Python R, PHP...)
  - ``dev/random`` et ``dev/urandom`` (sur linux)
- Phénomènes physiques
  - Bruit atmosphérique
  - Bruit d'un convertisseur analogique-numérique dans un microcontrôleur
  - Bruit thermique
- Aléatoire de données
  - Données biométriques
  - Données géographiques, biologiques, chimiques
  - Données textuelles, données sur internet
- Acheter de l'aléatoire
  - [Random.org](https://random.org), le site utilise une mesure du bruit atmosphérique

# Comment mesurer la qualité de l'aléatoire ?

Le fondement est **l'équiprobabilité**. L'idée est que plus un générateur est aléatoire, plus il a *autant de chances* de générer n'importe quel résultat, aussi différents les uns des autres soient ils. Par exemple; un générateur aléatoire de séquences de 8 bits, s'il respecte l'équiprobabilité, a autant de chances de générer chacune des séquences suivantes :
- ``00000000``
- ``11111111``
- ``11010010``

**Comment la tester ?**

## Démarche empirique -- Tests statistiques

Ils ont été formalisés par **Donald Knuth** et **[normalisés par NIST](https://csrc.nist.gov/groups/ST/toolkit/rng/stats_tests.html)**

Les outils sont :
- Les *combinatoires* et les *probabilités*
- Les méta-tests :
  - Le *test du ``\chi_2``*est celui qu'n utilisera en cours

### L'entropie de Shannon

La quantité d'informations contenues ou délivrées par une source d'informations est mesurée par l'entropie de Shannon tel que :

```
H(X) = \sigma_(S_i \in S) - p_i log_b(p_i)
```

Avec ``p_i`` la probabilité que la source émette le symbole ``s_i``;

L'entropie est pertinente en théorie de l'information.

## Démarche théorique -- la complexité de Kolmogorov

La complexité de Kolmogorov est la taille du plus petitprogramme pouvant générer une suite ``s = s_1, s_2, ..., s_n`` fixée en entrée.

Par exemple, voici quelques suites de bits :
- ``00000000`` = *``0`` répété `8` fois*
- ``01010101`` = *``01`` répété `4` fois*

La complexité de Kolmogorov est plus proche de ce aue l'être humain entends par "aléatoire" que l'entropie de Shannon, mais elle est plus difficile a mettre en place a cause, notamment, du besoin d'énumérer tous les programmes possibles pour trouver le plus petit.

# Aspects psychologiques

Les humains ne sont pas très doués pour générer de l'aléatoire. Naturellement, les humains vont faire plusieurs erreurs. Appliquées au binaire, les erreurs les plus communes sont les suivantes :
1. **Flips** : nombre trop élevé de *flips* (passage de `0` à `1` ou inversement)
2. **Runs** : nombre trop élevé de *runs* (nombre de `1` ou `0` consécutifs trop faible)

La détection de ces erreurs est fortement facilitée par l'utilisation de tests statistiques. Il faut choisir les tests *adaptés*.

Mais inversement, les tests statistiques sont mauvais pour détecter certaines constructions que l'humain *peut* détecter , surtout lorsqu'elles ne sont pas locales
1. Séquence répétée deux fois
2. Palindromes

# La génération uniforme

## Les différents types de données aléatoires

On peut distinguer deux grands types de données :
- Les données discrètes
  - l'espace de probabilité est **fini** ou **dénombrable**
- Les données continues
  - L'espace de probabilité n'est **__pas__ dénombrable**

<!-- À compléter un peu avec des formules et exemples -->

## Exemple de génération uniforme avec Python

- L'initialisation du **germe** (*seed*)
  - Avec ``random`` :
    ```python
    import random as r
    import time

    r.seed(time.time()) # On initialise le germe avec le temps
    r.random()
    ```
  - Avec ``Numpy`` :
    ```python
    import numpy as np
    import time
    np.random.seed(time.time())
    np.random.random()
    ```

## Méthode dite "de l'urne" ou "du sac"

On mets tous les objets dans un même sac (ensemble, tableau), et on tire les objets un par un.

On peut vérifier expérimentalement que l'on a :

```
Pr(a = c) = 1/A
```

avec `c` l'objet attendu, `a` l'objet tiré et `A` le "sac".

### Implémentation de la méthode du sac

**Méthodologie :**
1. On choisit la bonne structure de données pour nos objets
2. On stocke tous les objets dans le tableau
3. On effectue un tirage uniforme sur l'indice du tableau

**Inconvénient :** cette méthode n'est plus possible quand `A` devient trop grand :
- Le *nombre de mots* sur l'alphabet de longueur `16` (``26^15 = 4.36x10^22``)
- Le *nombre de graphes orientés* avec `10` sommets

## Tirage uniforme avec rejet (méthode de Monte Carlo)

**Méthodologie :**
1. On définit un ensemble ``B`` dans lequel il est facile de tirer des objets, et un ensemble `A` contenu dans `B` où il est plus compliqué de tirer (par exemple, `B` un carré et `A` un cercle dans ce carré).
2. On tire un objet `b` dans `B`
3. On vérifie si `b \in A`. Si oui, on garde `b`, sinon, on recommence.

**Inconvénient** :

La méthode n'est pas efficace lorsque `A` est trop petit par rapport à `B`. On peut mesurer le rapport `p` avec une méthode **de Bernouilli**