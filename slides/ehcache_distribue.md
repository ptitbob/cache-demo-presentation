## ehCache distribué

Serveur OSS<!-- .element class="fragment" -->

-@@-

## ehCache distribué

Serveur OSS

* Dockerisable
* Configurable via l'application
* Compatible JSR107
* Clusterisable

-@@-

## ehCache distribué

```xml
<dependency>
    <groupId>org.ehcache</groupId>
    <artifactId>ehcache</artifactId>
</dependency>



.
```

Activation...

-@@-

## ehCache distribué

```xml
<dependency>
    <groupId>org.ehcache</groupId>
    <artifactId>ehcache</artifactId>
</dependency>
<dependency>
    <groupId>org.ehcache</groupId>
    <artifactId>ehcache-clustered</artifactId>
</dependency>
```

... par l'ajout d'une dépendance

-@@-

## configuration

1. Ajout de la gestion en mode cluster

-@@-

```xml
<config
  ...
  xmlns:tc="http://www.ehcache.org/v3/clustered"
>
</config>
```

-@@-

## configuration

1. Ajout de la gestion en mode cluster
2. Configuration de l'accès au serveur

-@@-

```xml
<config...>
  <service>
    <tc:cluster>
      <tc:connection
          url="terracotta://ehcache:9410/demo-cache"
      />
      <tc:server-side-config auto-create="true">
        <tc:default-resource from="primary-server-resource"/>
      </tc:server-side-config>
    </tc:cluster>
  </service>
...
</config>
```

-@@-

## configuration

1. Ajout de la gestion en mode cluster
2. Configuration de l'accès au serveur
3. Définition d'une ressource cache cluster

-@@-

```xml
<config...>
  <service>...</service>
  <cache-template name="app-default">
    <expiry>
      <ttl unit="seconds">30</ttl>
    </expiry>
    <resources>
      <heap>10</heap>
      <offheap unit="MB">1</offheap>
      <tc:clustered-dedicated unit="MB">10
      </tc:clustered-dedicated>
    </resources>
    <tc:clustered-store consistency="strong"/>
  </cache-template>
</config>
```

-@@-

## ehCache et docker

docker compose : 

```yaml
ehcache:
  hostname: ehcache
  image: terracotta/terracotta-server-oss:5.5.1
  container_name: ehcache
  environment:
    - OFFHEAP_RESOURCE1_SIZE=256
    - OFFHEAP_RESOURCE1_UNIT=MB
    - OFFHEAP_RESOURCE1_NAME=primary-server-resource
  ports:
    - 9410:9410
  networks:
    - cache_net
```

-@@-

<!-- .slide: data-background="./images/bunny_03.png" data-background-size="20%" data-background-position="right 2.5em bottom 1em" -->

## ehCache easy !<!-- .element style="font-family: 'Sedgwick Ave', cursive; "--> 