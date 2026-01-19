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
- Ce processus est automatisé via un fichier de configuration (voir `.cursorrules` ou instructions dans le projet)

**Note importante :** Ce README est généré et mis à jour automatiquement par l'IA à chaque interaction, garantissant une documentation à jour et précise.

### Fonctionnalités à Venir

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


**Modifications apportées :**


---

## Fonctionnalités Ajoutées par Commit

### [À compléter lors du prochain commit]

Cette section sera mise à jour automatiquement à chaque commit pour lister uniquement les nouvelles fonctionnalités ajoutées depuis le commit précédent.

---

## Notes de Développement

### Utilisation de l'IA

Ce projet utilise l'IA (via Cursor) pour le développement. Chaque interaction est documentée dans la section "Historique des Modifications" ci-dessus, garantissant la transparence sur l'utilisation de l'IA et les modifications apportées.

### État Actuel du Projet

- ✅ Backend fonctionnel avec serveur REST pour les presets
- ✅ Sampler web fonctionnel avec interface utilisateur
- 🚧 Frontend Angular en cours de développement
- 📋 Fonctionnalités à venir listées dans l'introduction