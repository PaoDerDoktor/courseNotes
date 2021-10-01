# CM Calcul Parallèle et Distribué 5

## Sections parallèles

### Parallélisme imbriqué

```c++
#pragma omp parallel
{
    #pragma omp parallel
    {
        ...
    }
}
```

```c++
#pragma omp parallel
{
    #pragma omp section
    {
        #pragma omp section
        {
            f(left_path);
        }

        #pragma omp section
        {
            f(right_path);
        }
    }
}
```

Activation du 