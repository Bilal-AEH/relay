# Session 06 — La résilience

## Ce qu'on observe chez les humains

Certains groupes s'effondrent quand ils perdent un membre clé. D'autres absorbent le choc et continuent. La différence n'est pas la taille — elle est dans la structure.

Un groupe organisé autour d'une figure centrale — le fondateur, l'expert unique, le seul à connaître le processus — est fragile par construction. Toute la connaissance, toutes les décisions, tous les flux passent par ce point. Quand ce point disparaît, le groupe perd sa cohérence.

Un groupe qui a distribué sa connaissance et ses responsabilités est différemment vulnérable. Il peut perdre un nœud sans perdre la capacité à fonctionner, parce que d'autres nœuds savent faire ce que faisait le nœud perdu — ou peuvent trouver un chemin autour de lui.

C'est un choix de conception, pas un hasard. Les organisations résilientes ont souvent été construites avec cette intention : documenter, former plusieurs personnes aux mêmes tâches critiques, maintenir des redondances. C'est plus coûteux à construire. C'est bien moins coûteux à maintenir en cas de crise.

La résilience a aussi une limite : plus un système est distribué, plus il est difficile à coordonner. Un groupe décentralisé prend plus de temps à prendre une décision qu'un groupe hiérarchique. La résilience et la vitesse de décision sont souvent en tension.

## Ce que les réseaux en ont fait

La topologie **en étoile** place un équipement central — un switch ou un hub — au cœur de toutes les connexions. Toutes les machines le traversent pour communiquer. C'est simple à déployer, simple à gérer. Et c'est un **single point of failure** : si l'équipement central tombe, le réseau entier cesse de fonctionner.

```
Machine A ─┐
Machine B ─┼─ Switch central ─ Machine D
Machine C ─┘
```

La topologie **maillée (mesh)** connecte chaque nœud à plusieurs autres. Si un chemin est coupé, le trafic emprunte un autre. Pas de point central, pas d'effondrement central.

```
Machine A ── Machine B
    │    ╲  ╱    │
    │     ╲╱     │
    │     ╱╲     │
Machine D ── Machine C
```

Internet a été conçu autour de ce principe. Le réseau ARPANET — précurseur d'Internet — devait pouvoir survivre à la destruction de n'importe quel nœud, y compris plusieurs simultanément. **BGP** reflète cette intention : quand un chemin disparaît, les routeurs convergent vers un chemin alternatif. Le réseau se reconfigure autour de la perte.

La **redondance** dans les datacenters traduit le même raisonnement : doubles alimentations électriques, connexions réseau multiples vers plusieurs FAI, serveurs en cluster. Chaque composant critique a un doublon prêt à prendre le relais. Le coût de la redondance est calculé contre le coût de l'indisponibilité.

## Ce que ça révèle sur les deux systèmes

Les réseaux ont formalisé et résolu en quelques décennies un problème que les organisations humaines gèrent depuis des millénaires : comment préserver la capacité à fonctionner face à la défaillance d'un composant.

La différence, c'est la vitesse de convergence. Un réseau BGP reconverge en quelques minutes après une panne. Une organisation humaine qui perd son expert unique peut mettre des mois à retrouver son niveau de fonctionnement — le temps de former, de recruter, de reconstruire la connaissance perdue.

La résilience coûte. Les deux systèmes paient ce coût différemment.

## Référence

- `docs/topologie.md` — Étoile, mesh, redondance, single point of failure, BGP convergence
