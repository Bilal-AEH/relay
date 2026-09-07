# Propagation — Broadcast, Multicast, VLAN

## Les trois modes de diffusion

| Mode      | Destinataire              | Exemple              |
|-----------|---------------------------|----------------------|
| Unicast   | Une machine               | HTTP, SSH, TLS       |
| Broadcast | Toutes les machines       | ARP request, DHCP    |
| Multicast | Un groupe d'abonnés       | Streaming vidéo, OSPF|

## Broadcast

Un paquet broadcast a pour adresse de destination `255.255.255.255` (IPv4) ou `ff:ff:ff:ff:ff:ff` (MAC). Toutes les interfaces du segment l'acceptent.

```python
import socket

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
sock.setsockopt(socket.SOL_SOCKET, socket.SO_BROADCAST, 1)
sock.sendto(b"qui est la ?", ("255.255.255.255", 9999))
```

Le broadcast ne franchit pas les routeurs. Il est limité au segment réseau local (domaine de broadcast).

## VLAN — segmentation logique

Un VLAN (Virtual LAN) crée des domaines de broadcast séparés sur le même équipement physique. Les trames sont taguées avec un identifiant VLAN (802.1Q).

```
Switch physique unique :
  VLAN 10 → Comptabilité  (les broadcasts restent dans ce VLAN)
  VLAN 20 → Développement (isolé du VLAN 10)
  VLAN 30 → Direction
```

Communication inter-VLAN : nécessite un routeur ou un switch de niveau 3.

## Multicast

Une machine s'abonne à un groupe multicast (adresse `224.0.0.0/4`). Elle reçoit les flux destinés à ce groupe, pas les autres.

OSPF utilise `224.0.0.5` et `224.0.0.6` — les routeurs s'abonnent à ces groupes pour recevoir les annonces de routage.

## Voir dans le projet

- Session 02 : la rumeur, la segmentation, et pourquoi le contrôle de la diffusion est toujours une décision organisationnelle
