# Xarxes de computadors:

# T0. Introducció:

## Internet models:

En els ordinadors:
- Application
- Presentation
- Sesion
- Transport


A la xarxa i als ordinadors/servidors:
- Network
- Data Link
- Physical

> Cadascún parla amb els del seu nivell, i el superior i inferior: Comunicació horitzontal i vertical.
>
> `TCP -> IP`

Direcció del transport identifica l'aplicació.

> ***CLIENT:*** Aplicació demana transport.
>
> ***SERVER:*** Transport demana la peticio a l'applicació.

## Communication:

Endpoint A | | Endpoint B
:-|:-:|-:
Aplication Layer | ***Application Layer Protocol*** | Application Layer
Presentation Layer | ***Presentation Layer Protocol*** | Presentation Layer
Session Layer | ***Session Layer Protocol*** | Session Layer
Transport Layer | ***Transport Layer Protocol*** | Transport Layer
Network Layer | ***Network Layer Protocol*** (router) | Network Layer
Data Link Layer | ***Data Link Layer Protocol***  (router) | Data Link Layer
Physical Layer | ***Physical Layer Protocol***  (router) |  Physical Layer

**Router:**
Pot tenir dues targetes de xarxa.
> Puja per: la physical -> data link -> network protocol -> datalink -> physical

## Protocol data units:

||||||
-|-|-|-|-|-
DL-H | IP-H | T-H | A-H | **Application data** | DL-T
DL-H | IP-H | T-H | **Transport Data** | **Transport Data** | DL-T
DL-H | IP-H | **IP Data** | **IP Data** | **IP Data** | DL-T
DL-H | **Frame Data** | **Frame Data** | **Frame Data** | **Frame Data** | DL-T

# T1. Internet Protocol

## Direcció IP:

Ex: 10.1.1.0/24 *[Direcció de xarxa]*

`8 bits | 8 bits | 8 bits | 8 bits`

Adreces de `32 bits` -> Màscara de `24 bits`, alhesores: `8` últims de host. Valen 0.

## Direcció de màscara:
10.1.1.0/24 = 255.255.255.0 -> Mateixa subxarxa.

> Tot 1's. -> 255.255.255.0

[]()
> 0..0 `Xarxa`
>
>1..1  `Broadcast`
>
> Com a mínim he de reservar una pel router.

#### Exemples:
```
10.1.3.0/25

32-25 = 27 - 1 de xarxa - 1 de broadcast - 1 pel router = 25
```

```
Vull 50 hosts

2^6 = 64 // OK -> Necessito 6 bits.
2^5 = 32 // NO
```

## Direccionament
#### Públic:

#### Privat:
**Classes de direccions:**

Classe | Inici | Network bits | Host bits
:-:|:-:|:-:|:-:
A | 10.0.0.0 - 10.255.255.255 | 8 `[0 .. <-7->]` | 24
B | 172.16.0.0 - 172.31.255.255 | 16 `[10 .. <-14->]` | 16
C | 192.168.1.1 - 192.168.255.255 | 24 `[110 .. <-21->]` | 8

##### A:
0 | X | X | X | X | X | X | X
-|-|-|-|-|-|-|-


##### B:
1 | 0 | X | X | X | X | X | X
-|-|-|-|-|-|-|-


##### C:
1 | 1 | 0 | X | X | X | X | X
-|-|-|-|-|-|-|-

```
220.10.0.0/25

2^(32-25) -2 -Routers
```
