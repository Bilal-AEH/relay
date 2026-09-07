# Contrôle d'accès — Firewall, ACL, politique

## Le principe

Tout trafic réseau est autorisé ou refusé selon des règles. La règle par défaut définit la posture de sécurité :

- **Tout autoriser sauf interdiction explicite** — posture permissive, risquée
- **Tout interdire sauf autorisation explicite** — posture restrictive, recommandée

## Firewall

Un firewall inspecte les paquets et applique des règles. Deux types principaux :

**Stateless (sans état)** — évalue chaque paquet indépendamment. Rapide, limité. Ne connaît pas le contexte d'une connexion.

**Stateful** — maintient une table des connexions actives. Un paquet de retour correspondant à une connexion établie est automatiquement autorisé. Plus intelligent, plus coûteux.

## ACL (Access Control Lists)

Une ACL est une liste ordonnée de règles. La première règle qui correspond s'applique — les suivantes sont ignorées.

```
# Syntaxe simplifiée
permit tcp 192.168.1.0/24 any eq 443    # HTTPS depuis réseau interne : OK
permit tcp 192.168.1.0/24 any eq 80     # HTTP depuis réseau interne : OK
deny   tcp any            any eq 22     # SSH depuis partout : refusé
permit ip  any            any           # Reste : autorisé
```

L'ordre compte. Une règle `permit any any` en haut annule tout ce qui suit.

## Zones réseau

Un découpage classique en trois zones :

```
Internet → [ Firewall ] → DMZ → [ Firewall ] → LAN
```

- **DMZ (Demilitarized Zone)** : serveurs exposés (web, mail). Accessibles depuis Internet, isolés du LAN.
- **LAN** : réseau interne. Inaccessible depuis Internet directement.
- **Internet** : non fiable par défaut.

## La politique précède la technique

Un firewall sans politique de sécurité définie est soit inutile (tout autoriser), soit un obstacle (tout bloquer). La politique répond à des questions organisationnelles : qui a besoin d'accéder à quoi, depuis où, pour quels usages ?

La règle technique n'est que la traduction de cette décision.

## Voir dans le projet

- Session 03 : le gardien, la règle sociale, et le refus par défaut
