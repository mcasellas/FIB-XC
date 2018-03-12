# T3. Routing Algorithms:

*Com completar les taules d'enrutament de manera eficient.*

**Mètriques:**
- Salts
- Congestió
- Cost
- Prohibició

> Diferència entre **interiors** i exteriors.
>
> Procès dinàmic d'actualització de taules de routing.

## RIP (Routing Information Protocol):

`RIP Update:` Actualització de taules.

Envio per totes les interfícies un multicast (a tots els routers als que estan connectats).

> Temps d'enviar un paquet **~ 30s**
>
> Si no ha arribat res als 30s [Caigut/Retrassat]? **~ 180s**

`Mètrica:` Número de salts necessito per arribar al destí.

1. **Al arrancar un router:** Només veig les subxarxes de les meves interfícies, no els routers. Amb gateway *

```
R1 ->
      N1 1
      N2 1

R5 -> N5 1 -> R4  N5  R5 2
      N6 1        N6  R5 2
```

2.
