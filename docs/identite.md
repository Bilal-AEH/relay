# Identité réseau — DNS, ARP, usurpation

## Les couches d'identité

Un équipement réseau a plusieurs identités superposées :

```
Nom de domaine  →  github.com          (lisible, mémorisable)
Adresse IP      →  140.82.121.4        (logique, peut changer)
Adresse MAC     →  aa:bb:cc:dd:ee:ff   (physique, gravée en usine)
```

Chaque couche traduit la précédente.

## DNS — résolution de noms

```
Client → Résolveur local → Serveur DNS récursif → Serveur autoritaire
```

```python
import socket
ip = socket.gethostbyname("github.com")
print(ip)  # 140.82.121.4
```

Le résolveur cache les réponses pendant la durée du TTL (Time To Live) défini par le serveur autoritaire.

## ARP — résolution d'adresses physiques

Sur un réseau local, IP ne suffit pas. Il faut l'adresse MAC pour encapsuler la trame Ethernet.

```
Machine A :  "Qui a l'IP 192.168.1.10 ?"  →  broadcast
Machine B :  "C'est moi — ma MAC est xx:xx:xx:xx:xx:xx"
Machine A :  enregistre dans son cache ARP, envoie la trame
```

Aucune authentification dans ce protocole — n'importe qui peut répondre à une requête ARP.

## Attaques sur l'identité

**DNS poisoning** : corrompre le cache d'un résolveur DNS pour retourner une fausse IP. Le nom est correct, la destination ne l'est pas.

**ARP spoofing** : envoyer des réponses ARP falsifiées pour associer sa propre MAC à l'IP d'une autre machine. Tout le trafic destiné à la victime transite par l'attaquant.

```
Normal   :  192.168.1.1  →  MAC du routeur
Après ARP spoof :  192.168.1.1  →  MAC de l'attaquant
```

C'est le vecteur classique d'une attaque man-in-the-middle sur un réseau local.

**DNSSEC** signe cryptographiquement les réponses DNS — une réponse non signée ou mal signée est rejetée. Solution partielle : DNSSEC n'est pas déployé partout.

## Voir dans le projet

- Session 04 : identité, réputation, et le problème de la confiance dans l'annuaire
