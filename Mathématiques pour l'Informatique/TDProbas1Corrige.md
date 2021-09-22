# TD 1 - Exercices de bases et essais de Bernoulli ---- Correction

## Exercice I

### Question 1

L'espace de probabilité de l'expérience aléatoire (le lancer d'un dé à 6 faces classique) est ``D = {1, 2, 3, 4, 5,6}``.

Dans le cas de l'équiprobabilité, la distribution de probabilité est la distribution uniforme (chaque face a la même chance d'apparaître) : ``P(r = i) = 1/6`` (avec `r` le résultat, et pour tout ``i \in D``)

Évènement ``F \includes D``

```maths
"X = 5" = 6
= {i \in D | X(i) = 5}
"X = 1" = {4, 5}
"X = 1" = {1, 2, 3}
```

Rappels au tableau :
```maths
P(F) = ¨(r \in F) = (Card F) / (Card D)
``` 
Avec ``Card x`` le cardinal de l'ensemble `x`.

Une variable aléatoire est une fonction associant à un résultat d'expérience aléatoire une valeur. Exemple avec l'exemple du lancer de dé :

```maths
X : D -->  A = {-1, 1, 5}
    1  -> -1
    2  -> -1
    3  -> -1
    4  ->  1
    5  ->  1
    6  ->  5

        ===> P(X =  5) = 1/6
        ===> P(X =  1) = 2/6
        ===> P(X = -1) = 3/6 = P(r = 1) + P(r = 2) + P(r = 3)
```

Non, `X` ne dépends pas de la distribution de probabilité.

### Question 2

Calcul de l'**Espérance** de `X` :

```maths
E[X] = \sigma_(a \in A) a * P(X = a) = -1*(3/6) + 1*(2/6) + 5*(1/6) = 4/6 = 2/3
```

Calcul de la **Variance** de `X` :

```maths
E[X^2] = \sigma_(a \in A) a^2 * P(X = a) = (-1)^2 * (3/6) + 1^2 * (2/6) + 5^2 * (1/6) = 30/6 = 5

Var(X) = E[X^2] - (E[X])^2
       = 5 - (2/3)^2
       = 41/9
```

### Question 3

L'espace de probabilité de l'expérience aléatoire de trois lancers de dés a six faces classiques est ``E_3 = D*D*D = D^3``. On précise par souci de clarté :

```maths
E_3 = {(1, 1, 1), (1, 1, 2), ..., (6, 6, 6)}
Card(E_3) = Card(D)^3 = 6^3 = 216
```

Calculons la distribution de probabilité de cette expérience aléatoire. On note ``d = (d_1, d2, d_3)`` le résultat, et on pose ``i, j, k \in E`` :

```maths
P((d_1, d_2, d_3) = (i, j, k)) = P(d_1 = i   et d_2 = j   et d_3 = k)
                               = P(d_1 = i) * P(d_2 = j) * P(d_3 = k)
                               = (1/6)      * (1/6)      * (1/6)
                               = 1/216
```

On peut le dire comme on sait que les 3 lancers de dés sont indépendants (le résultat des uns n'influence aucunement celui des autres).

On reconnaît que ``P((d_1, d_2, d_3) = (i, j, k)) = 1/Card(E_3)``. On est donc dans le cas d'une distribution uniforme.

### Question 4

Calcul de l'**Espérance** de `Y` :

```maths
E[Y] = E[X_1] + E[X_2] + E[X_3]         (--> Linéarité de l'expérience toujours vraie)
     = 2/3    + 2/3    + 2/3
     = 6/3
     = 2
```

Calcul de la **Variance** de `Y` :

```maths
Var(Y) = Var(X_1) + Var(X_2) + Var(X_3)         (--> Car X_1, X_2 et X_3 sont indépendants)
       = 41/9     + 41/9     + 41/9
       = 123/9
```

## Exercice II

### Question 1

Ici l'expérience aléatoire est `i` lancer(s) de pièce de monnaie. Si on a Pile (`P`), on s'arrête. Sinon, on continue tant qu'on obtient Face (`F`).

Ainsi, on peut obtenir le résultat ``(P)`` ou le résultat ``(FP)``, mais pas le résultat ``(F)`` ou le résultat ``(PP)``.

Sachant cela, on pose ``E = {P, FP, FFP, FFFP, ...} = {F^i P | i \in N}`` l'espace de probabilité de l'expérience aléatoire.

On a :

```maths
P(r = P)      =  1/2
P(r = FP)     = (1/2) * (1/2) = 1/(2^2) = 1/4
P(r = F^(i)P) = 1/(2^(i+1))

\sigma_(i \in N) P(r  = F^(i)P) = 1/2 + 1/4 = 1/8 + ... = 1
```

### Question 2

On essaye de calculer l'espérance de `X` :

```
\sigma_(i \in N) 2^(i+1) * P(r = F^(i)P) = \sigma_(i \in N) 2^(i+1) 1/(2^(i+1)) = \sigma_(n \in N) 1
```

``E[X]`` n'est pas définie : la somme tends vers l'infinie


### Question 3

