### Multi node ?

![](images/multi-node-inmem-01.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-02.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-03.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-04.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-05.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-06.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-07.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-08.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-09.png)

-@@-

### Multi node ?

![](images/multi-node-inmem-10.png)

-@@-

## Inconsistance des données

-@@-

## Solution ?

1. synchroniser les caches

-@- 

### Synchronisation des caches

Impossibilité de gérer simplement la suppression<!-- .element style="color: crimson;" -->

La mutiplication des noeuds réduit l'efficacité du cache<!-- .element style="color: crimson;" -->

> Synchronisation seulement pour l'invalidation des / d'un cache (ou d'une valeur)

-@@- 

### Synchronisation des caches

Obligation de persistance des message d'invalidation de cache<!-- .element style="color: crimson;" -->

> Gestion alternative
> (code supplémentaire)

-@@-

### Synchronisation des caches

C'est la solution actuelle d'AVISé et de l'éditique

> mais ce n'est pas satisfaisant<!-- .element class="fragment" style="color: crimson;" -->


