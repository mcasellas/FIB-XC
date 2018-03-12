# T2. Other supporting protocols and services.

## ARP:
**Address Resolution Protocol**

Viatja sota IP -> Trama de subxarxa.

*Quina és la direcció d'enllaç de la IP xyz?*

> Broadcast a tota la subnet. S'envia la direcció d'enllaç pròpia per poder ser contestat.
>
> **L'involucrat contesta amb la seva direcció d'enllaç.**

`Taula ARP (caché):` Guardar les parelles [@IP, @enllaç] (+ refrescar la taula)

## ICMP:
**Internet Control Message Protocol**

Viatge sobre IP.

#### Preguntes (Fer solicituds):
  - Echo (Ping)
    - Request
    - Reply
  - Timestamp
    - Request
    - Reply

#### Gestionar errors:
  - Serveis
    - Source quench (relentizació d'origen)
    - Redirect
  - Errors
    - Destí inabastable
      - Xarxa
      - Host
      - Protocol
      - Port
    - Temps excedit (Temps de vida s'ha acabat -> Informo l'emissor)

## DHCP:
**Dynamic Host Configuration Protocol**

*Funciona sobre UDP*

- Direcció IP
- Mascara
- Nom (domini)
- Gateway
- Mascara

>mycomputer.ac.upc.edu

```
-(0.0.0.0)-> DHCP Discover
<-255.255.255.255- DHCP Offer
-> DHCP Request
<-(Dir IP Servei DHCP)- DHCP Pack
```

## NAT:
**Network Address Translation**

*IP Privada -> Internet*

> Servei al router.
>
> Taula de NAT: @Privada i @Públiques (mapejades)

@Privada | @Pública
-|-


Estàtiques i dinàmiques

`NAPT o PAT` -> NAT per ports**

`DNAT` -> Comunicació comença per fora

@Privada | Local port | @Pública | External Port
-|-|-|-

## DNS:
**Domain Name System**

*Identificar les màquines per noms* i obtenir l'adreça IP.

Existeix una jerarquia: `myhost.ac.upc.edu`

`.edu` **Top Level Domain**

- `.edu` Gestiona els següents: `upc`
  - `upc` Gestiona els següents: `ac`
    - `ac` Gestiona els següents.
      - `myhost`

> Existeix servidor de noms local de `ac.upc.edu`.

*Necessito la IP del servidor de noms* -> **La pregunto a upc.edu** -> **La pregunto a .edu**


*Protocol:*
```
Pregunto al meu DNS.


DNS -> Pregunta a /
/ -> Respon la IP de .org
DNS -> Pregunta a .org
.org -> Respon la IP de foo.org
DNS -> Pregunta a foo.org
foo.org -> Retorna la IP que vull

El meu DNS em retorna la IP.
```

> Pot estar a la xarxa local o externament.
