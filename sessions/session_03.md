# Session 03 — Le gardien

## Ce qu'on observe chez les humains

Dans tout groupe qui dure, il y a un gardien. Pas toujours un individu — parfois une règle, parfois une procédure, parfois une porte avec un badge. Mais la fonction existe toujours.

Le gardien ne se justifie pas par la méfiance. Il se justifie par la définition. Un groupe sans frontière n'est pas un groupe — c'est un espace ouvert. La frontière crée l'appartenance, et le gardien fait vivre la frontière.

Ce qui varie, c'est la granularité du contrôle. Dans un club très fermé, on contrôle l'entrée et la sortie. Dans une entreprise, on contrôle l'accès pièce par pièce — le stagiaire accède à l'espace de travail, pas à la salle des serveurs. Dans un État, on contrôle les frontières mais pas les déplacements internes. Plus l'enjeu est élevé, plus les règles d'accès sont fines.

Ce que le gardien décide n'est pas arbitraire quand le système fonctionne bien. Il applique des règles définies en amont par ceux qui ont la légitimité de les définir. Le videur applique la politique du club. Le secrétaire applique les consignes du directeur. La règle précède le gardien — le gardien l'exécute.

## Ce que les réseaux en ont fait

Le **firewall** est le gardien du réseau. Il examine chaque paquet qui entre ou sort et décide, selon des règles prédéfinies, s'il passe ou non.

Ces règles sont des **ACL** (Access Control Lists) — des listes qui spécifient : quelle source, quelle destination, quel protocole, quel port. Un paquet TCP entrant sur le port 22 (SSH) depuis une adresse inconnue ? Bloqué. Un paquet HTTP depuis l'intérieur vers un serveur externe ? Autorisé.

```
Règle 1 :  TCP  192.168.1.0/24 → *         port 80, 443   ALLOW
Règle 2 :  TCP  *              → 10.0.0.5  port 22        DENY
Règle 3 :  *    *              → *         *              DENY (par défaut)
```

La dernière règle est la plus importante. En sécurité réseau, le principe de base est celui du **refus par défaut** — tout ce qui n'est pas explicitement autorisé est interdit. C'est l'inverse du monde social quotidien, où la plupart des espaces publics fonctionnent sur l'autorisation par défaut (tu peux entrer sauf interdiction explicite). Les réseaux critiques choisissent la posture inverse, parce que le coût d'une intrusion dépasse le coût de la restriction.

Les **VLANs** jouent aussi ce rôle : ils séparent physiquement les flux sur le même matériel. Un paquet dans le VLAN comptabilité ne voit pas le VLAN développement, même s'ils partagent le même switch. Le gardien n'est plus à l'entrée du bâtiment — il est à l'intérieur, à chaque couloir.

## La décision qui précède la règle

Un firewall mal configuré est soit trop permissif (tout passe), soit trop restrictif (rien ne fonctionne). Dans les deux cas, la cause n'est pas technique — c'est qu'on n'a pas clairement défini ce qu'on voulait protéger et de qui.

C'est le même problème que dans les organisations humaines où les règles d'accès n'ont jamais été formalisées. Tout le monde improvise, et personne ne sait vraiment qui a le droit de quoi.

La sécurité réseau commence par une politique. La politique commence par une décision organisationnelle.

## Référence

- `docs/acces.md` — Firewall, ACL, VLAN, politique de sécurité
