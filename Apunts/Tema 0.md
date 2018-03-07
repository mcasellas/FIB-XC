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


-|-|-|-|-|-
-|-|-|-|-|-
DL-H | IP-H | T-H | A-H | **Application data** | DL-T
DL-H | IP-H | T-H | **Transport Data** | **Transport Data** | DL-T
DL-H | IP-H | **IP Data** | **IP Data** | **IP Data** | DL-T
DL-H | **Frame Data** | **Frame Data** | **Frame Data** | **Frame Data** | DL-T
