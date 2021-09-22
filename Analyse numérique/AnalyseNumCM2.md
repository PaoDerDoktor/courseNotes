# Analyse numérique, CM/TD 2

## Chapitre I - suite

### Calculs Matriciels

`A` matrice d'ordre `n` (`n` lignes et `n` colonnes) à coefficients réels.

#### Valeurs propres, vecteurs propres

##### Définitions

``\lambda \in C`` est une __valeur propre__ de `A` si et seulement si il existe un `x` non nul tel que ``Ax = \lambda x``

On peut associer un __vecteur propre__ a une valeur propre :

On pose `\lambda` valeur propre de `A` <=> ``det(\lambda I_n - A) = 0`` avec I_n la matrice identité d'ordre `n`.

``det(\lambda I_n - A)`` est un polynôme de degré `n`, appelé __polynôme caractéristique__.

##### Exemple

Déterminer les valeurs propres de `A` tel que :

(1)
```maths
    +---    ---+     +---               ---+   +---    ---+   +---                    ---+
    |  2   -1  |     |  \lambda         0  |   |  2   -1  |   |  2-\lambda           -1  |
A = |          | ==> |                     | - |          | = |                          |
    | -1    2  |     |  0         \lambda  |   | -1    2  |   | -1            2-\lambda  |
    +---    ---+     +---               ---+   +---    ---+   +---                    ---+

det(\lambda I_2 - A) = (\lambda - 2) * (\lambda - 2) - (-1) * (-1)
                     = (\lambda - 2)^2 - 1^2
                     = (\lambda - 2 - 1) * (\lambda - 2 + 1)
                     = (\lambda - 3) * (\lambda - 1)
```

On peut trivialement déduire par al règle du produit nul que les valeurs propres de A sont `1` et `3`. Elles sont toutes deux strictement positives.

(2)
```maths
    +---         ---+     +---                            ---+   +---         ---+
    |  2   -1    0  |     |  \lambda        0          0     |   |  2   -1    0  |
A = | -1    2   -1  | ==> |  0           \lambda       0     | - | -1    2   -1  |
    |  0   -1    2  |     |  0              0       \lambda  |   |  0   -1    2  |
    +---         ---+     +---                            ---+   +---         ---+

                           +---                                       ---+
                           |  2 - \lambda         -1              0      |
                      ==>  |       -1        2 - \lambda         -1      |
                           |        0             -1        2 - \lambda  |
                           +---                                       ---+

                                           (+---                    ---+)      (+---            ---+)
                                           (|  \lambda-2       -1      |)      (| -1        0      |)
det (\lambda I_2 - A) = (\lambda - 2) * det(|                          |) + det(|                  |)
                                           (|      -1       \lambda-2  |)      (| -1    \lambda-2  |)
                                           (+---                    ---+)      (+---            ---+)

                      = (\lambda - 2) * (((\lambda-2)^2)-(-1)^2) - \lambda + 2
                      = (\lambda - 2) * ((\lambda-2)^2 - 1) - \lambda + 2
                      = 
```

<!-- Again, a completer --->

Les valeurs propres de `A` sont **strictement positives**.

##### Propriété

Une matrice `A` est **définie positive** si et seulement si **toutes ses valeurs propres** sont **strictement positives**

Toutes les matrices `A` vues précédemment ayant toutes leurs valeurs propres strictement supérieures à 0, elles sont toutes définies positives.

##### Théorème 1

Si `A` est une matrice symétrique et définie positive, alors `A` est inversible et `A^(-1)` est symétrique et définie positive.

##### Théorème 2

Si `A` est symétrique et définie positive, avec `A` d'ordre `n` et pour `x` et `y` appartenant à `R^n`, ``(Ax/y)`` définit un produit scalaire sur ``R^n``.