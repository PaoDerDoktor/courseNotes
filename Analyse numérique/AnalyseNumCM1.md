NOTE : Le cours a 0 orga ça va être sympa

# Analyse numérique, CM/TD 1

## Présentation rapide

### Image continue

``u : \Omega \includes R^2 --> R`` est une application.
Type: ``(x, y) --> u(x, y)``

Qu'est-ce que le gradient de `u` ?  --> Dans les deux cas on utilise le calcul différentiel
Qu'est-ce que le laplacien de `u` ? -|

### Image discrète

Une image discrète est tout simplement une matrice.

### Motivation

#### Problème (1)

Étant donnée une fonction contenue sur ``[a, b]``, on cherche une fonction ``u(x)`` vérifiant :

```maths
{ - u''(x) + u(x) = f(x)
{            u(a) = u(b) = 0
```

(1) peut être résolu explicitement; mais c'est un exemple simple pour illustrer la méthode de résolution


Le problème (2) sera une version du problème (1) en dimension 2 : 

#### Problème (2)

étant donné une fonction `f` contenue sur ``[a, b]*[a, b] = \omega``, on cherche une fonction continue vérifiant :

```maths
{ - \delta u(x) + u(x) = f(x)    | sur \omega
{                 u(x) = 0       | sur \drond \omega (bord de \omega)
```

(2) ne peut pas être résolu explicitement, on cherche une solution approchée.

#### Conclusion sur les problèmes

- __Analyse fonctionnelle__ : ensemble de solutions de problèmes continus
- __Analyse numérique__ : ensemble de solutions de problèmes discrets

## Analyse numérique

### Chapitre I : Fonctions de plusieurs variables

#### 1) Produit scalaire

##### Définition :

Soient `x` et `y` deux vecteurs de `R^n` :

```maths
    +-   -+        +-   -+
    | x_1 |        | y_1 |
    | x_2 |        | y_2 |
    |  .  |        |  .  |
x = |  .  |    y = |  .  |
    |  .  |        |  .  |
    | x_n |        | y_n |
    +-   -+        +-   -+
```
Le __produit scalaire__ de `x` et `y` est noté ``(x/y)``.Il est défini par :

```maths

                                         +-   -+  
                                         | y_1 |  
                                         | y_2 |  
                                         |  .  |  
(x, y) = x^(T)*y = (x_1, x_2, ... x_n) * |  .  |  
                                         |  .  |  
                                         | y_n |  
                                         +-   -+

    = x_1*y_1 + x_2*y_2 + ... + x_n*y_n \in R
```

##### Exemple :

```maths
    +-   -+      +-   -+
    |  1  |      |  0  |
x = | -1  |  y = |  1  |
    |  2  |      |  2  |
    +-   -+      +-   -+
```
<!-- A CoMPLETER -->

##### Propriétés

(1)
```maths
\forall x, y z \in R^n, \forall \lambda \in R``:
(x + (\lambda y / z) = (x/z) + \lambda (y, z))
(x / y+\lambda z)
```

<!-- A COMPLETER AUSSI PUTAIN -->

#### Norme sur ``R^n``

##### Définition

On appelle __norme__ sur ``R^n`` toute application ``N : R^n --> R`` vérifiant les propriétés suivantes:
- ``\forall x \in R^n``, ``N(x) >= 0`` et ``N(x) = 0 <=> x=0``
- ``N(x+y) <= N(x) + N(y)``
- ``N(\lambda x) = (\lambda) N(x), \forall \lambda \in R``

##### Exemples

```maths
    +-   -+  
    | x_1 |  
    | x_2 |  
    |  .  |  
x = |  .  |    x \in R^n
    |  .  |  
    | x_n |  
    +-   -+  

||x||_2 = (\sigma^(n)_(i=1) x_(i)^2)^(1/2)   (norme euclidienne)
||x||_1 = \sigma^(n)_(i=1) |x_i|
||x||_\infinity = sup{|x_i| ; i = 1 ; .. n} <-- littéralement ce qui est au tableau
```

Soit :

```maths
    +---    ---+  
    | \sqrt(2) |  
    |     1    |  
x = |     0    |
    |    -1    |
    +---    ---+ 

||x||_2 = \sqrt((\sqrt(2))^2 + 1^2 + 0^2 + (-1)^2) = \sqrt(4) = 2
||x||_1 = \sqrt(2) + 1 + 0 = & = 2 + \sqrt(2)
||x||_\infinity = \sqrt(2)
```

#### Dérivées partielles

On a :
```maths
u : \omega \includes R^n --> R
                       x --> u(x)
```

Le **gradient** de `u` au point `x` est un __vecteur__ noté ``\grad f(x)`` :

```maths
             +----                      ----+  
             | (\drond f(x)) / (\drond x_1) |  
             | (\drond f(x)) / (\drond x_2) |  
             |               .              |  
\grad f(x) = |               .              |  
             |               .              |  
             | (\drond f(x)) / (\drond x_n) |  
             +----                      ----+  
```

C'est donc un vecteur de **dérivées partielles**.

##### Exemple

```maths
f : R^2 --> R

    +-   -+
    | x_1 |
x = |     | => 3x_(1)^(2) + 2x_(2)^(2) - 4x_(1)x_(2) + x_(1) - 6
    | x_2 |
    +-   -+
```

Calculer ``\grad f(x)`` et ``||\grad f(-1)||_(2)`` :
   
```maths
             +----                          ----+   +----
             |  (\drond f(x)) / (\drond x_(1))  |   |  6x_(1) + 0 - 4x_(2) + 1
\grad f(x) = |                                  | = |
             |  (\drond f(x)) / (\drond x_(2))  |   |  0 + 4x_(2) - 4x_(1) + 0 + 0 
             +----                          ----+   +----
6x_(1) - 4x_(2) + 1
4x_(2) - 4x_(1)

                 +----    ----+   +-   -+
                 | -6 + 4 + 1 |   | -1  |
\grad f(-1, 1) = |            | = |     |
                 |   -4 + 4   |   |  0  |
                 +----    ----+   +-   -+

||\grad f(-1, 1)||_(2) = (\sqrt((-1)^2)+0^2)^2 = 1
```

<!-- A COMPLETER ENCORE BORDEL --->

Cas d'une fonction de `R^n` dans `R^m` :

```maths
f : \omega \includes R^n --> R^m
                       x --> (f_1(x), f_2(x), f_m(x))
```

f'(x) est une matrice de `m`  lignes et `n` colonnes dite __matrice Jacobienne_, notée ``J_(f(x))``

```maths
+----                                                                                               ----+
|  (\drond f_1(x))/(\drond x_1)    (\drond f_1(x))/(\drond x_2)    ...    (\drond f_1(x))/(\drond x_n)  |
|                 .                               .                 .                    .              |
|                 .                               .                 .                    .              |
|                 .                               .                 .                    .              |
|  (\drond f_m(x))/(\drond x_1)    (\drond f_m(x))/(\drond x_2)    ...    (\drond f_m(x))/(\drond x_n)  |
+----                                                                                               ----+
```

##### Exemple

```maths
        f : R^3 --> R^2
(x_1, x_2, x_3) --> (3x_1 x_3 + x_2^2 ; 6x_1 x_2 x_3^2)
```

*Quelle matrice jacobienne peut-on associer à cette fonction ?*

```maths
+----                                                  ----+
|  3x_3 + 0 + 2x_2         0 + 2x_2            3x_1 + 0    |
|    6 x_1 x_3^2          6x_1 x_3^2        12x_1 x_2 x_3  |
+----                                                  ----+

   +----           ----+
   |  0     -2      3  |
 = |  0      0      0  |
   +----           ----+
```
#### Le Laplacien


```maths
f: \omega \includes R^n --> R
                      x --> f(x)
```

Le **Laplacien** de f est un __scalaire__ noté \delta f est défini par :
```maths
\delta f(x) = \sigma^(n)_(i=1) ((\drond^2 f(x))/(\drond x_i^2))
```

##### Exemple

```maths
f : R^2     --> R
(x_1, x_2)  --> 3x_1 x_2^2 + x_1 x_2


(\drond f(x)) / (\drond x_1) = 3x_2^2 + x_2
(\drond^2 f(x)) / (\drond x_1^2) = ((\drond)/(\drond x_1))*((\drond f(x))/(\drond x_1)) = 0

(\drond f(x)) / (\drond x_2) = 6x_1 x_2 + x_1
(\drond^2 f(x)) / (\drond x_2) = ((\drond)/(\drond x_2))*((\drond f(x))/(\drond x_2)) = 6x_1

\delta f(x) = 0 + 6x_1 = 6x_1
```

#### Divergence

Soit `V` un vecteur :

```maths
    +---    ---+
    |  P_1(x)  |
    |    .     |
V = |    .     |
    |    .     |
    |  P_n(m)  |
    +---    ---+
```

La **divergence** de V, notée ``div(V)``, vaut ``\sigma^(n)_(i=1) ((\drond f_i(x))/(\drond x_i))``

##### Exemples

(1)

```maths
f : R^2 --> R
      x --> f(x)
```

Calculer ``div(\grad f(x))`` :

<!-- ..... A completer hein (photo dans mon tel) --->

(2)

```maths
C : R^2 --> R
u : R^2 --> R
```

Calculer ``div(C(x)\grad u(x))``

```maths
             +---                          ---+
             |  (\drond u(x)) / (\drond x_1)  |
\grad u(x) = |                                |
             |  (\drond u(x)) / (\drond x_2)  |
             +---                          ---+

                  +---                               ---+
                  |  C(x) (\drond u(x)) / (\drond x_1)  |
C(x) \grad u(x) = |                                     |
                  |  C(x) (\drond u(x)) / (\drond x_2)  |
                  +---                               ---+

div(C(x) \grad u(x)) =  (\drond / (\drond x_1)) * (C(x) ((\drond u(x)) / (\drond x_1))) 
                      + (\drond / (\drond x_2)) * (C(x) ((\drond u(x)) / (\drond x_2)))

                     =  (\grad C(x) / \grad u(x)) + C(x) \delta u(x)

```