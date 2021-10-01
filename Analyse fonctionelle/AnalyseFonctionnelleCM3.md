# Analyse fonctionnelle, CM/TD 3

## Problèmes aux limites elliptiques

### 1) problème abstrait

Soit `V` un espace de Hilbert, ``(., .)_V`` produit scalaire sur `V`, ``||.||_V`` norme correspondante.

```maths
a : V * V ------> R         forme bilinéaire
   (u, v) ------>a(u, v)
```

__**Définition :**__ On dit que ``a`` est __continue__ sur `V` si et seulement si ``\exists n > 0 | |a(u, v)| <= M ||u|| ||v||``.

__**Définition :**__ On dit que `a` est __V-elliptique__ si et seulement si ``\exists \alpha > 0 | a(u, u) >=\alpha (||u||_V)^2``.

Considérons le problème abstrait.

Trouver ``u \in V`` solution de :

- `(1)` ``a(u, v) = f(v) \forall v \in V``

#### Théorème

Si la forme bilinéaire `a` est `V`-elliptique (__coersive__), alors le problème `(1)` admet une unique solution ``u \in V``.

#### Exemples

<!-- NOTE : Pour la colorisation des parenthèses : [ -->
```maths
  /
 / - u''(x) = f dans ]0, 1[
<
 \   u(0) = u(1) = 0
  \
```

On rappelle :

```maths
  +-- b                b     +-- b
  |     (   )      [  ]      |     (   )
  |     (f'g) dx = [fg]  -   |     (fg') dx
  |     (   )      [  ]      |     (   )
--+   a                a   --+   a

  +-- 1                    
  |     (              )   
  |     (- (u'(x))'v(x)) dx
  |     (              )   
--+   0                    

(On utilise ici la formule de Green (intégration par parties))

    +-- 1                                                 +-- 1                         b
    |     (        )                                      |     (          )      [    ]
=   |     (f(x)v(x)) dx \forall v \in (H_0)^1(\omega) +   |     (u'(x)v'(x)) dx - [v(x)]
    |     (        )                                      |     (          )      [    ]
  --+   0                                               --+   0                         a

    +-- 1                                    +-- 1
    |     (          )                       |     (        )
=   |     (u'(x)v'(x)) dx - (u'(1)*v(0)) =   |     (f(x)v(x)) dx \forall v \in (H_0)^1(\omega)
    |     (          )                       |     (        )
  --+   0                                  --+   0
```

On cherche ``u \in (H_0)^1(\omega) = { v \in H^1(\omega) v(0) = v(1) = 0 }``

Si on pose ``V = (H_0)^1(\omega)`` on a :

```maths
            +-- 1
            |     (           )
a(u, v) =   |     (u'(x)*v'(x)) dx
            |     (           )
          --+   0
```

et

```maths
         +-- 1
         |     (         )
F(v) =   |     (f(x)*v(x)) dx
         |     (         )
       --+   0
```

Notre problème s'écrit :

**__Trouver ``u \in v | a(u, u) = f(v) \forall v \in V``__**

On pose un autre problème :

#### Exercice

```maths
\omega = ]0, 1[, f donnée :

       /
      /  - u''(x) + u(x) = f(x) dans \omega
(P2) <
      \    u'(0) = u'(1) = 0
       \
```

Trouver la forme variationnelle de ``(P1)`` et montrer que ``(P2)`` admet une unique solution

```maths
            +-- 1               +-- 1
            |     (    )        |
a(u, v) =   |     (u'v') dx +   |     (uv) dx
            |     (    )        |
          --+   0             --+   0

         +-- 1
         |     (  )
F(v) =   |     (fv) dx
         |     (  )
       --+

V = H^1(\omega)
```

La forme variationnelle de ``(P1)`` :

```maths
       /
      /  Trouver u \in V |
(P3) <
      \          a(u, v) = F(v)
       \
```

a est une forme bilinéaire, symétrique

```maths
                         +-- 1                  +-- 1
                         |     (       )        |     (      )
\forall u != 0 a(u, u) = |     (u'(x)^2) dx +   |     (u(x)^2) dx > 0
                         |     (       )        |     (      )
                       --+   0                --+   0

a(u, u) = ||u||_(H^1(\omega)) > 0
```

Donc ``(P3)`` admet une seule unique solution

##### En dimension 2

On pose :

```maths
\omega = ]0, 1[ * ]0, 1[

                                  /
                                 /  -\delta u(x) = f(x) dans \omega
trouver u \in (H_0)^1(\omega) | <
                                 \  u = 0 sur \drond \omega
                                  \

x = (x_1, x_2)
```

