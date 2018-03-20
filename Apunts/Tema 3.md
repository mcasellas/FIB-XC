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

`RIP Update:` Actualització de taules via *UDP*.

Envio per totes les interfícies un multicast (a tots els routers als que estan connectats). **All RIPv2 routers -> 224.0.0.9**

> Temps d'enviar un paquet **~ 30s**
>
> Si no ha arribat res als 30s [Caigut/Retrassat]? **~ 180s**

`Mètrica:` Número de salts necessito per arribar al destí. `Mínim mètrica = 1`

- **Al arrancar un router:** Només veig les subxarxes de les meves interfícies, no els routers. Amb gateway *

*Exercici 2016t-c1-test:*

Si no el tinc l'afegeixo a la taula, i, en el cas que ja hi sigui, l'actualitzo si és millor.

Si no hi puc arribar: `(Mètrica infinit) = 16`

No retornen la informació que sels hi ha donat per la mateixa interfície

R1 |  | I/R | Mètrica
-|-|-|-
N1 | - | e0  | 1  
N2 | - | e1 | 1

R1 |  | I/R | Mètrica
-|-|-|-
N3 | - | e1  | 1  
N1 | R1 | e0 | 2
N2 | R1 | e1 | 2

 `Split Horizon`

```
R1 cap a -> R2,R3 -update-
      N1 1
      N2 1

R4 -> R2
      N5 1
      N4 1
      N6 2

R5 -> R4
      N6 1

R4 -> R5
      N4 1
      N3 2
      N2 3
      N1 3
      N6
```

## OSPF (Open Shortest Path First):

Més sofisticat -> S'envia un 'mapa' del seu voltant.

**Link state advertisements (LSA)** Inclou salts, bitrates, delays, percentatges d'error...

Viatja sobre IP -> 224.0.0.5 (flooding) i s'envia només quan s'actualitza.

`Protocol hello:` Protocol separat per saber si encara està viu.

## CIDR (Classless Inter-Domain Routing)

> Agregar rutes (entrades) a les taules de routing.
>
> Sumaritzar

Subxarxa | Gateway
-|-
200.200.0.0/24 | Rx
200.200.1.1/24 | Rx

Es pot compactar en una sola amb una màscara més petita: 200.200.0.0/23


# Prova de seguiment:

1. *Màscara de subxarxa més llarga:*
  ```
  80.84|.80.181

  80.84|.88.81

  0101|0000
  0101|1000
  ```

  Resposta: `/20`

2. *Quina màscara li correspon a 192.168.180.0 amb 100 màquines.*

  Necessito 7 bits.

  Resposta: `/25`

3. *Quants servidors poden haver-hi com a màxim?*

  eth1: **180.180.180.240/28** // eth2 **192.168.180.240/28**

  Màquina: 180.180.180.245 (pública) i 192.168.180.245 (privada)

  32 - 28 bits = 4 bits.

  2^4 = 16 - 3 (xarxa, broadcast i router) = `13 servidors`.

4. *Adreçament per les xarxes B i C. Consecutiu a la xarxa A:*

  A -> B -> C

  B: 300 hosts -> 9 bits **32-9 = 23 bits de màscara**

  C: 500 hosts -> 9 bits **23 bits de màscara**

  ```
  - A: 192.168.180.0/25
  - B: 192.168.180.128/23

    A : 1011010|0
    B : 1011011|0 --182.0/23--
    C : 1011100|0 --184.0/23--
  ```

5. *Interfícies del router que han de fer NAT:*
`eth0`
