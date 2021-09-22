<!-- NOTE : les CMs précédents étaient des rappels du C++ -->

# Architecture II

## Définition

__Qu'est-ce qu'une architecture parallèle ?__
- Au moins 2PE (processeur élémentaire)
- Des bornes mémoires
- Réseau d'interconnection --> __Composant principal__

On peut acheter de l'architecture parallèle dans le commerce (AMD Ryzen, Intel Core, DDR4, DDR5, etc.)

## Histoire

Historiquement, les principaux clients de parallélisme étaient les militaires. A la fin de la guerre froide, les projets militaires s'arrêtent et a partir de là, les entreprises font faillites et se font racheter par d'autres pour leurs brevets.

Ceci explique qu'il n'y ait pas de grand "consortium" et standard de parallélisme, comme le web et le __W3C__ par exemple

## Classifications :

On peut notamment classifier les méthodes de parallélisme par :
- Modèle d'exécution
- Structure de la mémoire
- Classification *IDSM*

### Exemple par modèles d'exécution

- Classification de __Flynn__ (1972) [modèle séquentiel]
  - On généralise le système de __Von Neumann__
  - On a des séquences d'instructions simples ou multiples
  - On a des séquences de données, là aussi simples ou multiples

### L'*IDSM* :

```
                +-------------+
                |   Data (D)  |
                +-------------+
                |   S  |   M  |
+---------+-----+------+------+
| Instru- |  S  | SISD | SIMD |
| ctions  +-----+------+------+
|   (I)   |  M  | MISD | MIMD |
+---------+-----+------+------+

```

#### Classe *SISD* :

```
      ^
      | D
 I  +----+
--> | PE |
    +----+
      ^ 
      | D

```

seul représentant: Von Neumann

#### Classe *MISD*:

```

 D  +------+  D  +------+  D  +------+  D
--> | PE_1 | --> | PE_2 | --> | PE_n | -->
    +------+     +------+     +------+
       ^            ^            ^
       | I_1        | I_2        | I_n
```

Exemple d'application : on sait ce qu'n cherche dans un flux vidéo, et on essaie de savoir si cette chose cherchée est présente dans le flux. On applique une série de filtres

Trop peu d'applications correspondent au *MISD* --> Pas de représentant connu

#### Classe *SIMD*

```
 D_1  +------+
----> | PE_1 | ---->
      +------+
         ^
         | I
         |
 D_2  +------+
----> | PE_2 | ---->
      +------+
         ^
         | I
         |
 D_n  +------+
----> | PE_n | ---->
      +------+
         ^
         | I
         |
```

Chaque processeur execute les mêmes instructions que ses voisins au même instant (modèle synchrone) sur ses propres données.

**Synchrône != massivement parallèle**

__problème d'ingénieurie__ : comment synchroniser un grand nombre de composants ?

Le *SIMD* n'existe plus en tant que modèle d'exécution pour l'architecture parallèle, mais il est présent pour les processeurs de PC modernes ==> Les jeux d'instructions __vectoriels__

Exemple : on envoie la même instruction sur les quatres quarts d'un entier non-signé sur 32 bits qui est en fait un ensemble de 4 octets

__Schéma en little-endian :__
```
   | I  | I  | I  | I
   V    V    V    V
 +----+----+----+----+
 | d4 | d3 | d2 | d1 |
 +----+----+----+----+
31                   0
```

__Intrinsics__ --> Bibliothèque de fonctions (très élémentaires) pour travailler en *SIMD*

##### Exemple :

On a un `float` (`32` bits) en *SSE*/*SSE2*/.../*SSE4*. Les *SSE* et dérivés travaillent sur des **registres 128 bits**.
On travaille `4` float en même temps (``128/32 = 4``) -> On a un speedup de facteur **4** !

Le code *C++* pur :

```cpp
#define N (4*...)

float src[N], dest[N];

// -------------------------
for (int i!=0; i < N; i++) {
    dest[i] = src[i];
} // Forme canonique
``` 

On peut premièrement modifier la boucle comme ceci, en la déroulant, comme on sait par nature du float que N est divisible par `4` :

```cpp
for (int i!=0; i < N; i+=4) {
    dest[i]   = src[i];
    dest[i+1] = src[i+1];
    dest[i+2] = src[i+2];
    dest[i+3] = src[i+3];
} // Forme déroulée
```

Le code avec des fonctions *SSE2* :

```cpp
for (int i!=0; i < N; i+=4) {
    __mm_store(&dest[i], __mm_load(&src[i]));
} // Forme vectorisée
```

#### Classe *MIMD*

```
         | D_1      | D_2       | D_n
         V          |           |
 I_1  +------+      |           |
----> | PE_1 |      |           |
      +------+      |           |
         |          V           |
 I_2     |       +------+       |
---->----+-----> | PE_2 |       |
         |       +------+       |
         |          |           V
 I_n     |          |        +------+
---->----+----->----+------> | PE_n |
         |          |        +------+
         |          |           |
         |          |           |
         V          V           V
```

Chaque processeur exécute ses propres instructions sur ses propres données (modèle asynchrone). On peut évidemment faire des systèmes massivement parallèles avec ça, c'est même le modèle actuel.

__Contrepartie__ : la synchronisation est à la charge du programmeur.

### Classification par structure de mémoire

#### Mémoire partagée (1950 ~> 1990)

```
             +---+
             |   |
+------+     |   |      +-----+
| PE_1 | --> |   | <--> | B_1 | // Banc mémoire
+------+     | R |      +-----+
             | É |
+------+     | S |      +-----+
| PE_2 | --> | E | <--> | B_2 |
+------+     | A |      +-----+
             | U |
+------+     |   |      +-----+
| PE_n | --> |   | <--> | B_n |
+------+     |   |      +-----+
             |   |
             +---+
```

__Quel est le rôle du réseau d'interconnection ?__

Ici la mémoire est **partagée** : le *RSO* relie chaque *PE* à l'intégralité des bancs mémoire de la machine. Chaque *PE* peut adresser tous les bancs.

On utilise le modèle programmation *multithreading* (chaque processeur s'occupe d'un thread, chaque processus peut contenir plusieurs threads)

Le modèle de réseau est *dynamique* (les routes changent tout le temps au gré des besoins)

On a avec ce système un problème de **gestion des caches** :

```
+------------+-------+               +-------+        +-------+
|     PE     |       |               | cache |   +--> |yyyyyyy| banc mémoire
| +--------+ | cache |               |   L2  |   |    |       |
| |Registre| |   L1  |               |       |   |    |       |
| +--------+ |       |          +--> |xxxxxxx| --+    |       |
|            |xxxxxxx| -> bloc -+    |       |   ^    |       |
+------------+-------+          |    +-------+   |    +-------+
                                |   /!\ INCOHÉRENCE DE CACHE /!\
                                |
                                |
+------------+-------+          |
|     PE     |       |          |
| +--------+ | cache |          |
| |Registre| |   L1  |          | /!\ INCOHÉRENCE DE CACHE À CACHE /!\
| +--------+ |       |          |
|            |yyyyyyy| ---------+
+------------+-------+                                    
```

Seul le réseau peut signaler que les caches sont corrompus ("dirty") et rétablir la cohérence entre les caches ``L1`` (privé) et ``L2`` (partagé). Le mécanisme étant très complexe et lourd, on ne peut pas faire de massivement parallèle avec un tel système.

#### Mémoire distribuée (1990 ~> 2000)

```
              Couple 1
+----------------------------------+             +---+
| +------+------+   +------+-----+ |   Message   |   |
| | PE_1 | L1_1 |   | L2_1 | B_1 | | <---------> |   |
| +------+------+   +------+-----+ |             |   |
+----------------------------------+             |   |
                                                 |   |
                                                 |   |
              Couple 2                           | R |
+----------------------------------+             | É |
| +------+------+   +------+-----+ |   Message   | S |
| | PE_2 | L1_2 |   | L2_2 | B_2 | | <---------> | E |
| +------+------+   +------+-----+ |             | A |
+----------------------------------+             | U |
                                                 |   |
                                                 |   |
              Couple n                           |   |
+----------------------------------+             |   |
| +------+------+   +------+-----+ |   Message   |   |
| | PE_n | L1_n |   | L2_n | B_n | | <---------> |   |
| +------+------+   +------+-----+ |             |   |
+----------------------------------+             +---+
```

Le réseau relie des couples processeurs-bancs. Chaque banc est adressable par *son* processeur. Il transfère les données d'un couple à l'autre avec des messages.

On utilise le modèle de programmation *multi-processus*.

Le modèle réseau est *statique* (les routes sont figées).

On peut, comme on n'a pas de problème de gestion, faire du massivement parallèle.

##### Quelle topologie utiliser ?

On peut utiliser plusieurs topologie réseau, mais chacune a sa spécialité :
- Une grille (traitement d'image)
- Un arbre (traitement de données)
- Un anneau (bruteforce)
- ...

Avec ce système de mémoire distribuée, on a possiblement une topologie en *hypercube* : une topologie physique capable de se subdiviser en software (choix de processeur) en n'importe quelle autre topologie.

Le souci, c'est qu'un hypercube nécessiterait au minimum **2048 processeurs**. Ça fait beaucoup, et en 2000 c'est quasiment inatteignable (coût, matières premières, rendement) notamment à cause des récessions/bulles.

On crée alors des **hybrides** (clusters de *SMP*) parallèlement aux supercalculateurs.

#### Hybrides (2000 -> ...)

```
+---------+        +---+        +---------+
| SMP     | <----> | R | <----> | SMP     |
| (64 PE) |        | É |        | (64 PE) |
+---------+        | S |        +---------+
                   | E |                   
+---------+        | A |        +---------+
| SMP     | <----> | U | <----> | SMP     |
| (64 PE) |        |   |        | (64 PE) |
+---------+        +---+        +---------+
```

Le modèle est *hybride multiprocesseur/multithreading*. On insère des threads dans des processus (un processus est associé à un *SMP*).

La mémoire est *physiquement distribuée*, mais *logiquement partagée*.

