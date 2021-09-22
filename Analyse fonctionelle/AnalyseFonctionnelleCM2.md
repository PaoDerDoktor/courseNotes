# Analyse fonctionnelle, CM/TD 2

## Suite du cours

On rappelle que ``L^(1)(\omega)``, ``L^(2)(\omega)``.

### Exemple

```maths
\omega = [1, +\infinity[        u(x) = 1/x
```

On cherche :

```maths
u \in L^(1)(\omega) ?

  +-- +\infinity                    +-- a
  |     (    )                      |     (   )
  |     (u(x)) dx = lim             |     (1/x) dx
  |     (    )      a->+\infinity   |     (   )
--+   1                           --+   1


  +-- a
  |     (   )
  |     (1/x) dx = ln(a) - ln(1) = ln(a)
  |     (   )
--+   1


  +-- +\infinity
  |     (   )
  |     (1/x) dx = lim            ln(a) = +\infinity
  |     (   )      a->+\infinity
--+  1
```
<!-- Pour la colorisation des parenthèses : ]] -->

On peut en conclure qu'on a ``u \notin L^(1)(\omega)``.

On cherche donc encore :
```maths
u \in L^(2)(Omega) ?

  +-- +\infinity                      +-- a
  |     (  1  )                       |     (   1   )
  |     (-----) dx  = lim             |     (-------) dx
  |     ( x^2 )       a->+\infinity   |     (  x^2  )
--+   1                             --+   1             

                                    (  +-- a             )
                                    (  |     (      )    )
                    = lim           (  |     (x^(-2)) dx )
                      a->+\infinity (  |     (      )    )
                                    (--+   1             )

                                    (                a)
                                    ([  1           ] )
                    = lim           ([----- x^(-2+1)] )
                      a->+\infinity ([-2+1          ] )
                                    (                1)

                                             a
                                    [    1  ]
                    = lim           [- -----]  = lim            -y_a + 1 = 1
                      a->+\infinity [    x  ]    a->+\infinity
                                             1
```

On peut montrer que

```maths
L^(2)(\omega) \includes L^(1)(\omega)
```

## Chapitre 2 : Les espaces de Hilbert

### Définition

Soit `H` un espace vectoriel. Un produit scalaire ``(u, v)`` est une __forme bilinéaire__ de ``H*H`` dans `R`, symétrique, définie positive. cio (???) : ``(u, v) >= 0`` et ``\forall u \in H (u, u) > 0`` si ``u != 0``.

Un produit scalaire vérifie l'inégalité de **__Cauchy-Schwartz__** :

```maths
|(u, v)| <= (u, u)^(1/2) * (u, u)^(1/2) \forall u, v \in H
```

Un espace de **__Hilbert__** est un espace vectoriel muni d'un produit scalaire ``(u, v)`` aui **__Complet__** (??????) pour la norme ``(u, u)^(1/2) = ||u||_H``.

``L^(2)(\omega)`` muni du produit scalaire suivant :

```maths
           +--
           |     (         )
(u, v) =   |     (u(x) v(x)) dx
           |     (         )
         --+   \omega
```
 est un espace de Hilbert.

#### Remarque

``v \in L^(2)(\omega)``, on peut définir ses dérivées partielles (``(\drond v)/(\drond x_i)``, etc.)

``(\drond v) / (\drond x_i) \notin L^(2)(\omega)``

<!-- Note : rien compris -->

<!-- Note : j'i l'impression qu'il est parti sur un autre sujet sans nous dire, faut que je revoie l'organisation du cours ici, plus tard -->

``H^(1)(\omega)``espace de **__Sokolev__** d'ordre `1`.

```maths
 1           /        2             \drond v         2
H (\omega)= <  v \in L (\omega), -------------- \in L (\omega), 0 <= i <= n
             \                     \drond x_i
```

On munit ``H'(\omega)`` du produit scalaire suivant:

```maths
                       +--
                       |     (        n      \drond u          \drond v   )
(u, v) H' (\omega) =   |     (uv + \sigma --------------  * --------------) dx
                       |     (       i=1    \drond x_i        \drond x_i  )
                     --+   \omega
```

On note :

```maths
||u||_(H'(\omega)) = (u, v)_(H)^(1/2)

xH_(0)^(1) (\omega) = {v \in H'(\omega)   |   v = 0 si et seulement si \drond \omega}
```

### Formule de Green

`u` et `v` des fonctions de ``H'(\omega)``

```maths
  +--                                 +--                                  +--
  |     (  \drond u(x)       )        |     (       \drond v(x)   )        |     (              )
  |     (--------------- v(x)) dx =   |     (u(x) --------------- ) dx +   |     (\gamma u v x_i) d\gamma
  |     (  \drond x_i        )        |     (        \drond x_i   )        |     (              )
--+   \omega                        --+   \omega                         --+ \gamma\omega
```

- ``v_i`` ième normale à \drond\omega dirigée vers l'extérieur de \omega
- \gamma l'application trace


```maths
 2           /                      \drond v
H (\omega)= < v \in H'(\omega), ---------------- \in H'(\omega), 0 <= i <= n
             \                     \drond x_i
```