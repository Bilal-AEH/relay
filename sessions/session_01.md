# Session 01 — La confiance et l'inconnu

## Ce qu'on observe chez les humains

Vous rencontrez quelqu'un pour la première fois. Vous ne pouvez pas vérifier son identité directement — vous n'avez aucun historique commun, aucune expérience partagée. Pourtant, la décision de lui faire confiance ou non se prend en quelques secondes.

Sur quoi elle repose, cette décision ?

Rarement sur une vérification directe. Presque toujours sur des intermédiaires : il est ami avec quelqu'un que vous connaissez. Il travaille dans une institution que vous reconnaissez. Quelqu'un de fiable vous a dit du bien de lui. Vous ne validez pas la personne — vous validez la chaîne qui la relie à quelque chose de connu.

C'est ce que les sociologues appellent la confiance transitive. Elle se propage à travers des tiers. Et elle a une limite claire : elle est aussi solide que le maillon le plus faible de la chaîne.

Ce mécanisme est si profondément ancré qu'on le reproduit partout — dans les recommandations professionnelles, dans les systèmes de réputation en ligne, dans les lettres de motivation. On ne certifie jamais quelqu'un soi-même. On s'appuie sur quelqu'un qui s'appuie sur quelqu'un.

## Ce que les réseaux en ont fait

Quand votre navigateur ouvre une connexion vers un serveur qu'il n'a jamais vu, il est dans la même situation. Il ne peut pas vérifier l'identité du serveur directement. Il s'appuie sur une chaîne.

C'est le rôle d'une **Certificate Authority (CA)**. La CA est un tiers de confiance — une institution reconnue — qui a vérifié l'identité du serveur et signé numériquement un certificat pour l'attester. Votre navigateur, lui, connaît la CA (son certificat racine est installé dans votre système d'exploitation à la livraison). Il ne connaît pas le serveur, mais il connaît la CA qui le certifie.

```
Navigateur → CA (connue, racine installée)
CA → Serveur (certifié, signature vérifiable)
Navigateur → Serveur (confiance transitive)
```

La chaîne de certificats peut avoir plusieurs maillons : une CA racine certifie une CA intermédiaire qui certifie le serveur. C'est exactement la structure de confiance humaine — plus il y a d'intermédiaires, plus chaque maillon doit être solide.

## La limite commune

La confiance transitive a un problème que les humains connaissent bien : si un tiers de confiance est compromis, tout ce qu'il a certifié l'est aussi.

En réseau, ça s'appelle un **compromis de CA**. Si quelqu'un s'empare de la clé privée d'une CA, il peut signer de faux certificats et se faire passer pour n'importe quel serveur. Plusieurs incidents réels ont démontré l'impact.

Côté humain, c'est le cas où la personne qui vous a recommandé quelqu'un était elle-même malhonnête. La chaîne entière perd sa valeur.

Les ingénieurs qui ont conçu TLS ne l'ont pas inventé. Ils ont formalisé ce que les humains faisaient depuis toujours.

## Référence

- `docs/confiance.md` — PKI, certificats, chaîne de validation
- RFC 5280 — Internet X.509 Public Key Infrastructure
