# m1-web-project

## Introduction

Ce README documente l'ensemble du processus de développement du projet, en tenant compte des retours reçus concernant la documentation et l'utilisation de l'IA.

### Processus de Documentation

**Contexte :** Suite aux retours reçus, ce README a été restructuré pour :
- Documenter précisément toutes les fonctionnalités réellement implémentées (sans mentionner des fonctionnalités inexistantes)
- Expliquer clairement comment l'IA a été utilisée dans le développement
- Suivre l'évolution du projet de manière transparente

**Méthodologie :** 
- Chaque demande faite à l'IA est documentée dans la section "Historique des Modifications"
- Pour chaque demande, on indique : la demande initiale, puis un résumé des modifications apportées
- À chaque commit, une section "Fonctionnalités Ajoutées" liste uniquement les nouvelles fonctionnalités depuis le dernier commit
- Ce processus est automatisé via un fichier de configuration (voir `.cursorrules` ou instructions dans le projet), que j'ai choisi volontairement de laisser dans le repo afin qu'il puisse être examiné

**Note importante :** Ce README est généré et mis à jour automatiquement par l'IA à chaque interaction, garantissant une documentation à jour et précise.

### Fonctionnalités à Venir *(partie non généré via IA)*

*PS : A savoir que certaines fonctionnalités ont déjà été ajouté par rapport aux projets que je vous ai rendu avec uniquement backend + sampler. Notemment la mise en place du backend sur render.com et la creation du projet angular. J'ai aussi décidé de bien séparé le projet en 3 parties, (comme expliqué plus tard, tout seul) en mettant en submodule github chacun des projets pour plus de cohérence. Le commit initial du projet tel qui l'est avant les "fonctionnalités à venir" : https://github.com/deliasTheo/m1-web-project/tree/a04caf23f95e68b29000cfb5ad316a7682eb1dc1.*

Voici les fonctionnalités prévues pour améliorer le projet :

1. **Guide.md à revoir** - Amélioration de la documentation utilisateur
2. **Support clavier AZERTY/QWERTY** - Adapter les raccourcis clavier pour fonctionner avec les deux layouts
3. **Upload audio à revoir** - Actuellement les uploads sont uniquement en mémoire. À décider : garder cette fonctionnalité ou la gérer uniquement via Angular
4. **Base de données cloud pour les presets** - Sauvegarder les objets JSON des presets (pas les fichiers audio) dans une base de données cloud et adapter le back-end
5. **Application front-end Angular** - Créer une application front-end séparée du sampler et du back-end qui :
   - Affiche au minimum une page avec la liste des presets
   - Communique avec le même back-end que le sampler
   - Permet de lister les presets et de les renommer
6. **Gestion des presets** - Ajouter des fonctionnalités (Angular) :
   - Suppression d'un preset
   - Création d'un nouveau preset depuis la page Angular (nom + liste des URLs des sons)
   - (Amélioration) Possibilité d'uploader des fichiers de son lors de la création d'un nouveau preset

---

## Structure du Projet

Le projet est composé de trois parties principales :

- **m1-web-backend/** - Serveur REST Node.js/Express pour servir les presets et fichiers audio
- **m1-web-sampler/** - Application web de sampler audio avec interface utilisateur
- **m1-web-frontend-angular/** - Application front-end Angular (en développement)

---

## Historique des Modifications

### Demande : Correction du support clavier AZERTY

**Date :** 19/01/2026

**Demande initiale :**

Corrigons d'abord une fonctionnalité dont j'ai parler dans le @README.md : 
- Support clavier AZERTY/QWERTY - Adapter les raccourcis clavier pour fonctionner avec les deux layouts
Le probleme, c'est qu'actuellement ce n'est pas les bonnes touches qui sont associé au pad. Dans un premier temps, on va corriger ca pour que ca corresponde a un clavier azerty.

Dans l'ideal j'aimerais que ce soit comme ca : 

pod 1 | pod 2 | pod 3 | pod 4 

pod a | pod z | pod e | pod r

pod q | pod s | pod d | pod f

pod w | pod x | pod c | pod v

Attention, sur mac 1/2/3/4 c'est les touches & é " '
Ce n'est pas le cas pour windows. Fait en sorte que ca marche aussi bien sur mac que sur windows (car je perle bien des touche 1/2/3/4, pas ceux du pavé numerique).

**Modifications apportées :**
1. Modification du fichier `m1-web-sampler/js/KeyboardHandler.js` pour utiliser `event.code` au lieu de `event.key` afin de détecter la position physique des touches (compatible Mac et Windows)
2. Mise à jour du mapping des touches pour correspondre au layout AZERTY :
   - Ligne du haut (pads 12-15) : touches 1, 2, 3, 4 (Digit1, Digit2, Digit3, Digit4)
   - Deuxième ligne (pads 8-11) : a, z, e, r (KeyA, KeyZ, KeyE, KeyR)
   - Troisième ligne (pads 4-7) : q, s, d, f (KeyQ, KeyS, KeyD, KeyF)
   - Ligne du bas (pads 0-3) : w, x, c, v (KeyW, KeyX, KeyC, KeyV)
3. Ajout d'un support supplémentaire pour les caractères produits sur Mac AZERTY (&, é, ", ') afin d'assurer la compatibilité complète

**Commentaire fait par moi-même**:
L'IA a fait à peux près ce que je voulais, mais il a mal compris que je voulais que la touche 1 soit le pod 0 et non le pod 12. J'ai donc modifié ca. De plus, j'ai remarqué qu'elle a mis en place les KeyA/Z/E sauf que si je laisse comme ca, ca prends en compte le clavier qwerty et non azerty. Je vais donc modifié ca pour m'adapter au clavier AZERT.

---

## Fonctionnalités Ajoutées par Commit

### Commit e2dd6c4 (19/01/2026) : Correction du mapping clavier AZERTY

- Correction du mapping clavier AZERTY pour les pads du sampler
- Utilisation de `event.key` au lieu de `event.code` pour les touches lettres afin de supporter correctement le layout AZERTY
- Correction de l'ordre des pads : pad 0 correspond maintenant à la touche 1
- Support maintenu pour les touches 1-4 via `event.code` (Digit1-4) et `event.key` pour Mac AZERTY (&, é, ", ')

---

---

## Notes de Développement

### Utilisation de l'IA

Ce projet utilise l'IA (via Cursor) pour le développement. Chaque interaction est documentée dans la section "Historique des Modifications" ci-dessus, garantissant la transparence sur l'utilisation de l'IA et les modifications apportées.

### État Actuel du Projet

- ✅ Backend fonctionnel avec serveur REST pour les presets
- ✅ Sampler web fonctionnel avec interface utilisateur
- 🚧 Frontend Angular en cours de développement
- 📋 Fonctionnalités à venir listées dans l'introduction