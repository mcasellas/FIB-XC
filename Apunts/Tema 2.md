# T2. Other supporting protocols and services.

## ARP:
**Address Resolution Protocol**

Viatja sota IP -> Trama.

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

> *IP Privada -> Internet*


## DNS:
**Domain Name System**
