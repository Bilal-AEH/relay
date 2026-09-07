# Session 04 — L'identité et la réputation

## Ce qu'on observe chez les humains

Vous ne connaissez pas quelqu'un. Vous connaissez son nom, ce qu'il a fait, et ce que d'autres ont dit de lui.

L'identité humaine, dans un contexte social large, est presque entièrement construite par la réputation — c'est-à-dire par l'agrégation de ce que des tiers rapportent. Avant les bases de données, les villes fonctionnaient par le bouche-à-oreille. Avant les réseaux sociaux, la réputation professionnelle se transmettait par des lettres de recommandation, des références vérifiables, des annuaires.

Le nom est l'identifiant. Il ne change pas (ou rarement). Mais ce à quoi il renvoie — la réputation, l'historique, la localisation — évolue. Un nom suffit pour commencer à chercher. Mais le nom seul ne prouve rien : il peut être usurpé. C'est pour ça que la vérification d'identité a toujours besoin d'un ancrage supplémentaire — un document, une signature, un tiers qui confirme.

## Ce que les réseaux en ont fait

Les réseaux ont le même problème d'identité — et le même besoin d'annuaires.

**DNS (Domain Name System)** est l'annuaire d'Internet. Il fait correspondre un nom lisible (`github.com`) à une adresse IP numérique (`140.82.121.4`). Sans DNS, chaque connexion nécessiterait de connaître l'adresse IP par cœur — comme un monde sans annuaire où il faudrait mémoriser le numéro de téléphone de chaque personne.

```
Requête DNS :  "Quelle est l'adresse de github.com ?"
Réponse DNS :  "140.82.121.4"
```

**ARP (Address Resolution Protocol)** descend encore d'un niveau : il fait correspondre une adresse IP à une adresse physique (MAC address) — l'identifiant gravé dans la carte réseau à la fabrication. On passe du nom logique (IP, assigné dynamiquement) à l'identité physique (MAC, permanente).

```
IP  → adresse logique, peut changer, lisible
MAC → adresse physique, permanente, gravée dans le matériel
```

Le parallèle est précis : le nom de domaine est comme le nom social — lisible, mémorisable, mais abstrait. L'adresse IP est comme une adresse postale — assignée, peut changer. La MAC address est comme une empreinte digitale — physique, unique, permanente.

## La vulnérabilité de l'annuaire

Un annuaire central est une cible. Si quelqu'un peut contrôler ce que retourne le DNS, il peut rediriger le trafic vers n'importe quelle machine tout en conservant le nom d'origine. C'est ce qu'on appelle le **DNS poisoning** — empoisonner le cache d'un résolveur DNS pour que les requêtes légitimes pointent vers une machine malveillante.

Côté ARP, c'est l'**ARP spoofing** : envoyer de fausses réponses ARP pour associer sa propre MAC à l'IP d'une autre machine. Résultat : tout le trafic destiné à cette machine passe par l'attaquant en premier. C'est un vecteur classique d'attaque man-in-the-middle.

Dans les deux cas, la faille n'est pas dans le nom — elle est dans la confiance implicite accordée à l'annuaire. On suppose que les réponses sont correctes, parce que vérifier chaque réponse en temps réel était impossible à l'époque de leur conception.

La réputation humaine a le même problème. Un nom peut être usurpé. Un faux CV peut passer. Un faux avis peut circuler. La solution dans les deux cas est la même : ajouter une couche de vérification externe — DNSSEC pour le réseau, une vérification des références pour l'humain.

## Référence

- `docs/identite.md` — DNS, ARP, DNSSEC, usurpation d'identité réseau
