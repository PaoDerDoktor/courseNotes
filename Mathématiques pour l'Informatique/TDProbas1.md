# TD 1 - Exercices de base et essais de Bernoulli

## Exercice 1

### Question 1

L'expérience aléatoire d'un jet d'un dé a six faces classique a pour espace de probabilités ``{1, 2, 3, 4, 5, 6}``

La variable aléatoire `X` a pour espace de probabilités ``{-1, 1, 5}``

Dans le cas où le dé respecte l'équiprobabilité (``1/6`` chances de tomber sur chacune des faces), La distribution de probabilité de la variable `X` est telle :

```maths
+-----+-----+-----+
| -1  |  1  |  5  |
+-----+-----+-----+
| 3/6 | 2/6 | 1/6 |
+-----+-----+-----+
```

La distribution de l'expérience aléatoire d'un jet de dé a six faces classique est :

```maths
+-----+-----+-----+-----+-----+-----+
|  1  |  2  |  3  |  4  |  5  |  6  |
+-----+-----+-----+-----+-----+-----+
| 1/6 | 1/6 | 1/6 | 1/6 | 1/6 | 1/6 |
+-----+-----+-----+-----+-----+-----+
```

`X` ne dépend pas de la distribution de probabilité.

### Question 2


Calcul de l'**Espérance** de `X` :

```maths
E[X] = -1 * P(X = -1) + 1 * P(X = 1) + 5 * P(X = 5)
E[X] = -(3/6) + 2/6 + 5/6
E[X] = 4/6
E[X] = 2/3
```
Calcul de la **Variance** de `X` :

```maths
Var(X) = E[(X - E[X])^2]
Var(X) = E[X^2] - (E[X])^2

E[X^2] = (-1)^2 * P(X = -1) + 1^2 * P(X = 1) + 5^2 * P(X = 5)
E[X^2] = 3/6 + 2/6 + 25/6
E[X^2] = 30/6
E[X^2] = 5

Var(X) = 30/6 - (4/6)^2 = 30/6 - 16/36
Var(X) = 164/36
Var(X) = 41/9
```

### Question 3

L'espace de