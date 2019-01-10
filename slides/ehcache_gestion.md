## ehcache et la gestion des caches

-@@-

## gestion des caches

*Permettre une invalidation des caches à la demande*

ehCache est une implémentation de la JSR107 <!-- .element class="fragment" -->

-@@-

## gestion des caches

Injection du `CacheManager`

```java
private final CacheManager cacheManager;
```

-@@-

## gestion des caches

Récupération d'un cache

```java
Cache cache = this.cacheManager.getCache(cacheName);
```

-@@-

## gestion des caches

Récupération de tous les caches

```java
this.cacheManager.getCacheNames().forEach(
  cacheName -> {
      this.cacheManager.getCache(cacheName)...
  }
);
```

-@@-

## gestion des caches

Invalidation de tout un cache

```java
((JCacheCache)
  this.cacheManager
    .getCache(cacheName)
).getNativeCache().clear()
```

-@@-

## gestion des caches

Suppression d'une valeur

```java
this.cacheManager.getCache(cacheName).evict(...)
```

-@@-

## gestion des caches

A voir dans les branches ehCache : 

```org.shipstone.....app.service.CacheService```
