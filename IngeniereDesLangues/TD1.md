# TD 1

## I]

### 1)

#### a)

```maths
\sigma = {0, 1}
```

#### b)

```maths
\sigma = {a}
```

#### c)

```maths
\sigma = \void
```

### 2)

#### a)

```maths
\sigma = {o, h, u, c, g}
```

#### b)

```maths
\sigma = {r, a, p, l, e, 4, 7, 1}
```

#### c)

```maths
\sigma = {0, 1}
```

### 3)

#### a)

All binary strings including the empty string.
All binray strings.

#### b)

Any string containing nothing but `a`'s (as many time as needed), including the empty string.
All string with only `a`'s, but at least one.

#### c)

The language which contains only the empty string.
The language which contains only the empty string.

### 4)

#### a)

The strings with even number of characters (`a` and `b`), and a length of at least 2.

#### b)

The binary strings that only end in ``101``

#### c)

Strings that do **not** contain a `0` after the first `1`.

#### d)

The strings that end with an `a` or are empty.

### 5)

<!-- A COMPLETER AVEC LES DIAGRAMMES -->

### 6)

<!-- A COMPLETER AVEC LES DIAGRAMMES -->

### 7)

#### a)

|   |  0  |    1   |
|---|:---:|:------:|
| 1 | {1} | {1, 2} |
| 2 | {2} |   {2}  |
|   |     |        |

#### b)

|   |  0  |  1  |  ε  |
|---|:---:|:---:|:---:|
| 1 | {1} | {2} | {2} |
| 2 | {2} |     |     |
|   |     |     |     |

### 8)

<!-- A COMPLETER AVEC LES IMAGES -->

## II] RegExps

### 1)

#### a)

```regex
\b\w*[aeiouy]{4}\w*\b
```

#### b)

```regex
\b\w*q+\w*\b
```

#### c)

```regex
\b\w*er\w*er\w*er\w\b
```

#### d)

```regex
\b\w*([aeiouy]{3}w+){2}\w*\b
```

#### e)

```regex
\b[a-m]+[n-z]+\b
```

#### f)

```regex
\b[^aeiouy\s]{4}\w*\b
```

#### g)

```regex
\b\w*(ism)\b
```

#### h)

```regex
\b(\we){3}\b
```

#### i)

```regex
\b[aeiouy]+([^aeiouy\s]*[aeiouy])?\b
```

#### j)
```regex
\b\w*((sh\w*ch)|(ch\w*sh))\w*\b
```

#### k)

```regex
\b(?!(equ))\w*equ\w*\b
```

#### l)

```regex
\b\w*ent\\w*(?<!(ent))\b
```

### 2)

#### a)

```regex
\b\w\w*\1\b
```

#### b)

```regex
\b\w\w\2\1
```

## III]

### 1)

Q_1, Q_2, Q_2, Q_2, Q_2, Q_1, Q_1, Q_1

### 2)

Q_1, Q_2, Q_1, Q_3, Q_2

