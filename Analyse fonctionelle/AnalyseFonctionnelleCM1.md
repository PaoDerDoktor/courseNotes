# Analyse fonctionnelle, CM/TD 1

`f` et `g` de classe ``C^1`` sur ``[a, b]`` et leurs dérivées sont continues.

## Rappel : intégration par parties

### Exemple

```maths
  +-- b                                   +-- b
  |     (         )                b      |     (          )
  |     (f'(x)g(x)) dx = [f(x)g(x)]   -   |     (f(x) g'(x)) dx
  |     (         )                a      |     (          )
--+   a                                 --+   a

                                                 +-- b
                                                 |     (         )
                       = f(b)g(b) - f(a)g(a) -   |     (f(x)g'(x)) dx
                                                 |     (         )
                                               --+   a
```
<!-- completer éventuellement avec la photo de ju -->

``f \in C([a, b])`` donnés, on cherche `u` vérifiant

```maths
{ - u''(x) + u(x) = f(x)
{            u(a) = u(b) = 0
```
<!-- Pour la colorisation des parenthèses : }}-->

```
  +-- b                            +-- b                       +-- b
  |     (                 )        |     (            )        |     (            )
  |     (-(u'(x))' \phi(x)) dx +   |     (u(x) \phi(x)) dx =   |     (f(x) \phi(x)) dx
  |     (                 )        |     (            )        |     (            )
--+   a                          --+   a                     --+   a
```

```maths
  +-- b                         +-- b                                           +-- b
  |     (              )        |     (            )                     b      |     (            )
  |     (u'(x) \phi'(x)) dx +   |     (u(x) \phi(x)) dx - [u'(x) \phi(x)]   =   |     (f(x) \phi(x)) dx
  |     (              )        |     (            )                     a      |     (            )
--+   a                       --+   a                                         --+   a
```

<!-- J'ai aucune idée de ce qu'il est en train de baragouiner au tableau c'est monstrueux -->
<!-- Bon apparemment le système et les intégrales sont "le même problème" -->

__**La base de l'analyse fonctionnelle**__ : le système vu plus haut est un problème fort, dont il est compliqué de trouver une solution, tandis que l'intégrale est le même problème en version faible <!--(???)-->, plus facile à résoudre

Bon grosso modo en vrai


❓


![aled](https://c.tenor.com/8lNAs5b-03sAAAAd/lol-mia-league-of-legends.gif)


## Distribution

\omega est un *ouvert* de ``R^2``

### Rappel ouvert/fermé

``[a, b]`` est un intervalle fermé de `R`.
``]a, b[`` est un intervalle fermé de `R`. <!--Pour le coloring des parentheses : ]-->

Le disque est un **compact** de `R`
La boule fermée est un **compact** de ``R^2``

Le support de `\phi` noté ``sup(\phi)`` ou ``supp(\phi)`` vaut ``{x \in \omega | \phi(x) !=0}``.

### Reprise sur la distribution

``D(\omega)`` est un ensemble des fonctions indéfiniment dérivables sur \omega et à *support compact*.

``D(\omega)`` est un espace de distribution, un espace de fonctions linéaires et continues sur \omega.

#### Exemple

On pose :

```maths
{ h(x) = 1 si x >= 0
{ h(x) = 0 si x <  0
```
`h` n'est pas dérivable <==> `h'` n'existe pas.

<!-- pour la colorisation des parenthèses : }} -->

```maths
                    +-- +\infinity
                    |     (            )
(h(x), \phi(x)) =   |     (h(x) \phi(x)) dx      | \forall \phi \in D(\omega)
                    |     (            )
                  --+   -\infinity
                 
                    +-- +\infinity
                    |     (       )
                =   |     (\phi(x)) dx
                    |     (       )
                  --+   0



(h'(x), \phi)   = - (h, \phi')

                    +-- +\infinity
                    |     (        )
                =   |     (\phi'(x)) dx
                    |     (        )
                  --+   0
```

``(h',\phi)`` dérivée de `h` au sens des distributions <!-- ??????? -->

## Chapitre I : Les espaces fonctionnels

## Les espaces L^1 et L^2

\omega un ouvert borné e ``R^n`` (``n=2`` pour une image)

``L^1(\omega)`` espace de fonctions **intégrable** sur à valeurs dans ``R``

``u \in L^1(\omega)`` signifie qu'il existe:

```maths
  +--
  |     (    )
  |     (u(x)) dx
  |     (    )
--+   \omega
```

``||u||_(L^1(\omega))`` vaut :

```maths
  +--
  |     (      )
  |     (|u(x)|) dx      --> Norme L^1
  |     (      )
--+   \omega
```

``L^2(\omega)`` espace de fonctions carré intégrables sur `R`

``u \in L^2(\omega)`` implique qu'il existe :

```maths
  +--
  |     (        )
  |     ((u(x))^2) dx
  |     (        )
--+   \omega
```