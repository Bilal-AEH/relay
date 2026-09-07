# Session 07 — Le relais

## Une fonction, trois époques

Il existait un métier.

L'opératrice téléphonique travaillait dans une centrale. Elle portait un casque, assise devant un tableau de fiches et de câbles. Quand un abonné décrochait, elle répondait. Il lui donnait un nom ou un numéro. Elle savait où trouver la ligne correspondante dans l'annuaire — une connaissance construite par l'expérience, actualisée chaque jour. Elle tirait un câble, établissait la connexion, vérifiait que la ligne était libre. Si ce n'était pas le cas, elle cherchait une alternative. Elle était le point de contact, la mémoire du réseau, la voix entre deux inconnus.

Ce n'était pas un travail d'exécution mécanique. Elle gérait des priorités — les urgences passaient avant les conversations mondaines. Elle gérait des conflits — les lignes occupées, les demandes impossibles, les abonnés impatients. Elle connaissait les habitudes de son central, les heures de pointe, les pannes récurrentes. La fonction demandait du jugement.

---

Les autocommutateurs ont remplacé les câbles. Plus besoin de quelqu'un pour tirer la connexion — la machine le faisait automatiquement, en millisecondes, sans erreur de mémoire. Le travail de routage manuel est devenu du routage automatique.

Le routeur fait exactement ce que faisait l'opératrice : il reçoit un paquet, consulte sa table, décide du chemin, fait suivre. Il ne connaît ni l'expéditeur ni le destinataire. Il connaît les chemins. C'est tout ce qu'il lui faut.

```
Paquet reçu → consultation de la table → prochain saut → forward
```

La table, c'est la mémoire de l'opératrice. Le protocole de routage, c'est la formation continue — la mise à jour permanente de ce qu'elle savait sur les chemins disponibles.

---

Quelque chose a changé depuis.

Le routeur ne comprenait pas le contenu du paquet. Il voyait des adresses, des ports, des protocoles. Pas du sens. La conversation qu'il acheminait lui était opaque — et il n'avait pas à la comprendre pour faire son travail.

L'opératrice, elle, entendait parfois. Elle ne devait pas écouter — mais elle pouvait. Elle comprenait la langue, pouvait inférer l'urgence d'une voix, détecter une demande inhabituelle. Cette dimension humaine n'était pas dans le protocole. Elle était dans la personne.

---

Ce projet s'arrête ici.

Pas parce que la suite n'existe pas. Parce que la suite, vous la connaissez déjà — et la décrire explicitement ajouterait moins que de la laisser présente, visible dans la structure de ce qui précède.

## Référence

- Sessions 01 à 06 — le contexte complet
- `docs/` — les concepts techniques associés à chaque couche
