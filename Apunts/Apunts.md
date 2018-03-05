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

---
# T1. Internet Protocol

## Direcció IP:

Ex: 10.1.1.0/24 *[Direcció de xarxa]*

`8 bits | 8 bits | 8 bits | 8 bits`

Adreces de `32 bits` -> Màscara de `24 bits`, alhesores: `8` últims de host. Valen 0.

## Direcció de màscara:
10.1.1.0/24 = 255.255.255.0 -> Mateixa subxarxa.

> Tot 1's. -> 255.255.255.0

[]()
> 0.0.0.0 `Xarxa`
>
> 1.1.1.1  `Broadcast`
>
> 127.0.0.1 `Localhost`
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

## Direccionament:
#### Públic:

#### Privat:
**Classes de direccions:**

Classe | Inici | Network bits | Host bits
:-:|:-:|:-:|:-:
A | 10.**0.0.0 - 10.255.255.255** | 8 `[0 .. <-7->]` | 24
B | 172.**16.0.0** - 172.**31.255.255** | 16 `[10 .. <-14->]` | 16
C | 192.168.**1.1** - 192.168.**255.255** | 24 `[110 .. <-21->]` | 8

##### A:
0 | X | X | X | X | X | X | X
-|-|-|-|-|-|-|-


##### B:
1 | 0 | X | X | X | X | X | X
-|-|-|-|-|-|-|-


##### C:
1 | 1 | 0 | X | X | X | X | X
-|-|-|-|-|-|-|-


#### *Exemple exàmen:*
```
220.10.0.0/25

2^(32-25) -> 7 bits.
2^7 = 128, tinc 94 màquines // OK
128 -2 -Routers
```
***Distribució d’adreces públiques més adient:***

Xarxa | Nº direccions | Nº bits host
:-:|:-:|:-:
N4 | 50 + 1(R) + 2(X+B) = 53 | 64 -> `6 bits`
N1 | 20 + 1 + 2 = 23 | 32 -> `5 bits`
N2 | 12 + 1 + 2 = 15 | 16 -> `4 bits`
N3 | 10 + 1 + 2 = 13 | 16 -> `4 bits`

***Adreces IP decidides per a cada xarxa:***

Xarxa | Màscara | Adreça IP | Bit a bit
:-:|:-:|:-:|:-:
Adreça contractada | /25 | **220.10.0.0/25**
N4 | /26 | **220.10.0.0/26** (subconjunt de l'anterior) | 00XXXXXX
N1 | /27 | **220.10.0.64/27** (subconjunt de l'anterior) | 01XXXXXX
N2 | /28 | **220.10.0.96/28** (subconjunt de l'anterior) | 010XXXXX
N3 | /28 | **220.10.0.112/28** (subconjunt de l'anterior) | 011XXXXX

***Volem unir les xarxes N3 i N2:***

15+13 = 28 -> `5 bits`

> Retrocedim un bit.

Xarxa | IP | Màscara
-|-|-
N2+N3|  220.10.0.96 | /27

## Enrutament:

#### *Exercici:*

`Exercici 1`

*Xarxa destí* | *Màscara* | Gateway | Interfície
:-:|:-:|:-:|:-:
200.200.200.0 | /27 | 200.200.200.65 (RI) | e0
200.200.200.32 | /27 | 200.200.200.66 (R1) | e0
200.200.200.64 | /27 | Directe | e0
200.200.200.0 | ... |  |
Resta 0.0.0.0 | 0.0.0.0 | 200.200.200.66 (R1) | e0

## Fregmentació:

Enviament de paquets amb una mida màxima.

`MTU` Maximum Transfer Unit -> Data

Datagrama IP amb **MTU de 1020**
- Dades Transport (1000 Bytes)
- Cabeçera IP (20 Bytes)

*Així puc dividir en blocs de 1000.*

> Si IP fragmenta i algun paquet es perd no el recupera.
>
> **Els hauriem de fer a l'aplicació** perquè Transport->IP no fragmenti.

***Opcions:***
- Que reconstueixi la màquina final
- Que els routers intermitjos reconsturixin i tornin a fragmentar.

***Necessito per reconstruïr la fragmentació:***
- Identificacor
- Offset
- Mida

Necessito un ordre i saber de quin orígen pertanyen. Però... ***i si les MTU són diferents?***

`MTU 1020 -> MTU 420` Per encabir: [20+400]+[20+400]+[20+200]

`MTU 420 -> MTU 220` Per encabir: [20+200]+[20+200]

***Per identificar-los amb les fragmentacions?***

*Offset del byte:* Identifica els octets.

1000Bytes -> byte a byte -> `[0...999]` -> `[0..399][400..799][800..999]`

> **DF:** Don't Fragment

> **MF:** More Fragments

> > `MF = 0:` Ja no queden fragments per enviar.

> > `MF = 1:` Encara falten per enviar.

***Quants bits per l'offset?***

1000 bytes -> 2^10 -> 10 bits

> **Exemple 1:**

> Establim una mida mínima. Ex: Si la capçalera és de 20 bytes, no faré fragmentacions de 1 byte.

```
Blocs de `8 bytes` 2^3 = 8 -> M'estalvio 3 bits.

10+3 = 13 bits
```


[]()
> **Exemple 2:**

> MTU = 520 -> 500 de Dades.

> *Arrodonim al múltiple de 8 menor.*

```
Dades de 496 -> Ha de ser múltiple de 8
```
