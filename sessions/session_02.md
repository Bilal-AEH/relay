# Session 02 — La rumeur

## Ce qu'on observe chez les humains

Une information entre dans un groupe. Personne ne l'a planifiée, personne ne contrôle sa diffusion. En quelques heures, tout le monde est au courant — mais la version que chacun a entendue diffère légèrement de la précédente.

Ce phénomène n'est pas un bug de la communication humaine. C'est un mode de fonctionnement. Les groupes humains diffusent l'information sans permission parce que c'est efficace — ça permet à un groupe de réagir vite à une menace, de partager une découverte, de coordonner sans organisation centrale.

Le problème, c'est que ce mode de diffusion ne discrimine pas. La vraie nouvelle et la fausse nouvelle se propagent exactement de la même façon. Et plus un groupe est grand, plus le bruit l'emporte sur le signal.

Les sociétés qui ont grandi ont toutes développé des mécanismes pour contrôler ça : des canaux officiels (la presse, le journal d'entreprise, l'annonce en réunion), des filtres (les gatekeepers — éditeurs, chefs, modérateurs), des segmentations (tu sais ça si tu es dans ce service, pas si tu es ailleurs). La diffusion libre reste utile dans les petits groupes. À grande échelle, elle devient ingérable.

## Ce que les réseaux en ont fait

Le **broadcast** est la version réseau de la rumeur. Une machine envoie un paquet à toutes les machines du réseau simultanément, sans demander si elles en ont besoin. Le protocole ARP fonctionne ainsi : quand une machine cherche l'adresse physique correspondant à une adresse IP, elle crie dans le vide — et tous les équipements entendent.

C'est efficace dans un réseau petit. Dans un réseau de plusieurs centaines de machines, un broadcast permanent sature le canal. C'est ce qu'on appelle un **broadcast storm** — chaque machine répond, ce qui génère d'autres broadcasts, jusqu'à ce que le réseau soit inutilisable.

La solution est la même que dans les groupes humains : la segmentation.

Les **VLANs** (Virtual Local Area Networks) découpent un réseau physique en sous-réseaux logiques isolés. Un broadcast envoyé dans un VLAN ne sort pas de ce VLAN. Chaque segment a sa propre sphère d'information — exactement comme les services dans une entreprise qui n'ont accès qu'à ce qui les concerne.

```
Sans segmentation :  Machine A crie → tout le monde entend
Avec VLAN        :  Machine A crie → seulement son segment entend
```

Le **multicast** affine encore plus : une machine envoie un paquet à un groupe d'abonnés qui ont explicitement demandé à recevoir ce flux. Ni à tout le monde (broadcast), ni à un seul (unicast) — à ceux qui ont manifesté un intérêt. C'est la liste de diffusion versus le mailing général.

## La dynamique commune

Ce qui est fascinant, c'est que la décision de segmenter n'est jamais technique en premier. Elle est sociale. On segmente parce qu'on a décidé que certaines informations appartiennent à certains groupes. Le VLAN est la formalisation d'une décision organisationnelle.

Et les deux systèmes — humain et réseau — partagent la même vulnérabilité : si la segmentation est mal configurée, l'information fuit. En réseau, c'est un VLAN hopping. Dans une organisation, c'est une fuite interne.

## Référence

- `docs/propagation.md` — Broadcast, multicast, VLAN, segmentation
