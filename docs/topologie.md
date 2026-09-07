# Topologie — Structures réseau et résilience

## Les topologies fondamentales

**Étoile** — tout passe par un point central.

```
A ─┐
B ─┼─ Switch ─ D
C ─┘
```

Simple à déployer, simple à déboguer. Single point of failure : si le switch tombe, plus rien ne communique.

**Anneau** — chaque machine est connectée aux deux suivantes. Une coupure suffit à isoler une portion du réseau. Utilisé dans certains réseaux industriels avec des mécanismes de redondance.

**Maillé (mesh)** — chaque nœud a plusieurs connexions vers d'autres nœuds. Plusieurs chemins disponibles entre deux points. Plus résilient, plus complexe à gérer.

**Hybride** — la réalité : un cœur de réseau maillé, des distributions en étoile vers les postes de travail.

## Single Point of Failure

Un SPOF (Single Point of Failure) est un composant dont la défaillance entraîne l'arrêt complet du service. L'identifier, c'est la première étape pour le résoudre.

Solutions classiques :
- **Redondance d'équipements** : deux switches en failover
- **Liaisons redondantes** : deux câbles entre deux équipements (agrégation de liens / LACP)
- **Plusieurs FAI** : deux connexions Internet indépendantes

## BGP et la convergence

BGP (Border Gateway Protocol) est le protocole de routage entre systèmes autonomes — entre les grandes entités qui composent Internet (FAI, entreprises, datacenters).

Quand un lien BGP tombe, les routeurs voisins retirent les préfixes annoncés par ce lien et propagent l'information. Les autres routeurs recalculent leurs chemins. La convergence prend de quelques secondes à quelques minutes selon la taille du réseau.

C'est pour cette raison qu'une panne d'un FAI n'éteint pas Internet. Les chemins se redistribuent.

**BGP hijacking** : annoncer faussement des préfixes qu'on ne possède pas. D'autres routeurs, croyant avoir trouvé un chemin optimal, redirigent le trafic. Ça s'est produit à l'échelle mondiale plusieurs fois.

## Spanning Tree Protocol (STP)

Dans une topologie avec des boucles physiques (pour la redondance), STP désactive logiquement les chemins redondants pour éviter les boucles réseau, et les réactive si le chemin principal tombe.

## Voir dans le projet

- Session 06 : résilience humaine et réseau, la tension entre distribution et coordination
