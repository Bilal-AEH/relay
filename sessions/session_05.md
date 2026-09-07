# Session 05 — La mémoire des chemins

## Ce qu'on observe chez les humains

Aucun individu ne peut connaître une ville entière par cœur. Mais n'importe qui peut se déplacer dans une grande ville parce que la connaissance des chemins est distribuée — elle est dans les panneaux, les apps, les passants, les chauffeurs de taxi, les livreurs. Chaque nœud du réseau humain connaît les chemins depuis là où il est.

Cette connaissance est également dynamique. Un embouteillage se forme — les informations remontent, les GPS recalculent, les conducteurs se redistribuent sur d'autres routes. La mémoire des chemins n'est pas figée. Elle est mise à jour en permanence, par l'expérience collective.

Il y a une économie dans cette mémoire. Vous ne retracez pas l'itinéraire depuis zéro à chaque fois que vous allez au même endroit. Vous gardez en tête les chemins que vous avez déjà empruntés. La mémoire réduit le coût de chaque déplacement futur.

Et la mémoire a une durée de vie. Un chemin appris il y a dix ans peut ne plus exister. Une route fermée, un bâtiment démoli, une ville qui a changé — la mémoire périmée est parfois pire que l'absence de mémoire, parce qu'elle conduit avec confiance vers une impasse.

## Ce que les réseaux en ont fait

Les **tables de routage** sont la mémoire des chemins des routeurs. Chaque routeur sait, pour chaque plage d'adresses de destination, par quelle interface envoyer le paquet. Il ne trace pas le chemin complet — il décide juste du prochain saut. Et le routeur suivant fait de même. C'est une intelligence distribuée, exactement comme la connaissance humaine des rues.

```
Réseau destination    Interface de sortie   Prochain saut
10.0.0.0/8           eth0                  192.168.1.1
192.168.2.0/24       eth1                  192.168.2.254
0.0.0.0/0            eth0                  192.168.1.254  (route par défaut)
```

Ces tables sont construites et mises à jour par des protocoles de routage. **OSPF** (Open Shortest Path First) fait converger les routeurs d'un même réseau vers une vision commune de la topologie — chaque routeur inonde le réseau avec ce qu'il sait, et tous calculent les chemins optimaux. **BGP** (Border Gateway Protocol) fait la même chose à l'échelle d'Internet : chaque système autonome (AS) annonce les préfixes d'adresses qu'il peut atteindre, et les routeurs de frontière construisent leur table à partir de ces annonces.

Le **cache DNS** est une autre forme de cette mémoire : quand vous avez déjà résolu `example.com` récemment, votre machine garde la réponse en cache pendant un temps défini (le TTL — Time To Live). Elle ne refait pas la requête DNS à chaque connexion. C'est de l'économie de ressources — exactement comme la mémoire humaine des chemins.

## Le problème de la mémoire périmée

Une table de routage mal à jour envoie des paquets vers des destinations qui ont changé. Un cache DNS périmé retourne une IP qui ne correspond plus au bon serveur. Dans les deux cas, la confiance dans une mémoire ancienne crée une erreur silencieuse — le chemin semble correct jusqu'au moment où ça ne fonctionne pas.

**BGP hijacking** exploite directement cette dynamique : un acteur malveillant annonce faussement être le chemin optimal vers un ensemble de préfixes. Les routeurs mettent à jour leurs tables, et une portion du trafic Internet est redirigée. Ça s'est produit plusieurs fois à grande échelle — des incidents qui ont révélé à quel point la mémoire collective des chemins est vulnérable à une fausse mise à jour.

Les humains ont le même problème avec les rumeurs structurées : si quelqu'un de bien positionné répand une fausse information sur les chemins disponibles, le groupe entier adapte son comportement à cette fausse carte.

## Référence

- `docs/routage.md` — Tables de routage, OSPF, BGP, cache DNS, TTL
