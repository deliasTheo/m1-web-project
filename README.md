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

### Demande : Création du frontend Angular avec composant homePage

**Date :** 20/01/2026

**Demande initiale :**

Je dois réaliser un front end en angular dans le dossier @m1-web-frontend-angular/.
Dans ce projet je veux : 
- Un composant homePage, qui me permet d'avoir la liste des presets disponible sur notre backend (pour l'instant utilise une liste vide via un service, on fera ensuite les modif necessaire directement depuis le service pour le connecter a mon backend) On affichera uniquement leur nom. Puis avec des chevrons, on fera en sorte de pouvoir "dérouler" et d'avoir tout les nom d'un preset. ON trouvera aussi un mini bouton pour modifié le nom du preset ou d'un son. Pour ca, il faudra valider avec un autre bouton pour etre sur que l'utilisateur soit OK avec ca.
- le model d'un preset : - un nom, un type et des sons. Chaque son possede un url et un nom. 
- Tu pourra aussi créer un bouton ajouter, que nous feront par la suite pour ajouter un preset ou un son (ajouter un son a un preset existant, ou un nouveau preset). Je te dis ca pas pour que tu le fasse, mais pour que tu saches ce qu'on va faire pas la suite pour que le code soit près a acceuillir cette fonctionnalité. 

Oublie pas de créer un liste de preset deja faite dans le service directement, afin que on soit près par la suite pour lié ca aux backend

**Modifications apportées :**
1. Création des modèles TypeScript `Preset` et `Son` dans le dossier `models/` :
   - `Preset` : contient un nom (string), un type (string) et une liste de sons (Son[])
   - `Son` : contient un nom (string) et une url (string)
2. Création du service `PresetService` dans le dossier `services/` :
   - Liste vide de presets initialisée (prête pour la connexion au backend)
   - Méthodes pour récupérer les presets, mettre à jour les noms de presets et de sons
   - Méthodes préparées pour l'ajout futur de presets et de sons (`addPreset`, `addSonToPreset`)
3. Création du composant `HomePage` dans le dossier `components/home-page/` :
   - Affichage de la liste des presets avec leurs noms uniquement
   - Système de chevrons pour dérouler/réduire chaque preset et afficher ses sons
   - Boutons d'édition pour modifier le nom des presets et des sons avec validation (boutons ✓ et ✕)
   - Bouton "Ajouter un preset" préparé pour les fonctionnalités futures
   - Interface utilisateur moderne avec styles CSS
4. Configuration des routes Angular :
   - Route par défaut (`''`) et route `/home` pointant vers le composant `HomePage`
   - Simplification du template `app.html` pour n'afficher que le `<router-outlet />`

**Commentaire apporté par moi-même :**
Cursor m'a ajouter les fonctionnalités que je voulais avec un front end assez sobre et qui ressemblait a ce que je voulais. Il a juste oublié de me créer des exemples, la liste est vide, ducoup j'ai ajouter des variables d'exemple en dur pour tester. Niveau architechture il a respecté ce que j'ai demandé. Avant de faire appel au backend, il faudra que je le prépare pour le rename, puis pour l'ajout et la suppression plus tard de chaque preset ou son. Je vais quand même lui demander de préparer ses fonctionnalité en créant les boutons et les methodes dans le service.

---

### Demande : Ajout des fonctionnalités de suppression et d'ajout de presets/sons

**Date :** 20/01/2026

**Demande initiale :**

Très bien. Ajoute maintenant les boutons et les methode nécéssaire (même si elle sont vide pour l'instant car le backend n'est pas près) pour : 
- Suppression d'un son (dans un preset) ou d'un preset entier. Il fautdra demander la validation pour etre sur que l'utilisateur est ok avec ca
- Ajout d'un son, dans un preset existant
- L'ajout d'un preset, sera un forms, crée un nouveau composant pour ca, mais il faut l'utiliser comme une "box" au dessus de la page qui peux etre fermé a tout moment si l'utilisateur veux annulé l'ajout. Il faudra donner un nom, un type. Il ne sera pas obligé d'ajouter des son, mais tu mettra un bouton + pour ajouter un son a ce preset qu'on est en train de créer. Oublie pas de bien sérarer avec un service afin que l'utilisation du backend soit facile des qu'il sera près. Ducoup la tu ajoutera un preset a la liste qu'on a deja créer. Ne pense tu pas qu'il est utile que cet liste soit un observable ? Si plus tard on passe par des requette backend ? Si tu pense que c'est pas nécassaire, ne fait pas

**Modifications apportées :**
1. Conversion du service `PresetService` pour utiliser un `BehaviorSubject` et un `Observable` :
   - La liste des presets est maintenant un `Observable<Preset[]>` accessible via `presets$`
   - Méthode `getPresets()` retourne l'Observable
   - Méthode `getPresetsValue()` pour accéder à la valeur synchrone si nécessaire
   - Toutes les méthodes du service mettent à jour le BehaviorSubject pour notifier les abonnés
2. Ajout des méthodes de suppression dans le service :
   - `deletePreset(presetIndex)` : supprime un preset
   - `deleteSonFromPreset(presetIndex, sonIndex)` : supprime un son d'un preset
   - Toutes les méthodes sont préparées avec des commentaires TODO pour les appels backend futurs
3. Ajout de la méthode pour ajouter un son dans un preset existant :
   - `addSonToPreset(presetIndex, son)` : ajoute un son à un preset existant
4. Création du composant modal `AddPresetModal` :
   - Formulaire pour créer un nouveau preset avec nom et type (champs obligatoires)
   - Bouton "+ Ajouter un son" pour ajouter dynamiquement des sons au preset en cours de création
   - Possibilité de supprimer des sons avant la sauvegarde
   - Bouton de fermeture (✕) et possibilité de fermer en cliquant sur l'overlay
   - Bouton "Annuler" et "Enregistrer" (désactivé si nom ou type vide)
5. Mise à jour du composant `HomePage` :
   - Utilisation de l'Observable avec `subscribe` et gestion de la désinscription dans `ngOnDestroy`
   - Ajout des boutons de suppression (🗑️) pour les presets et les sons avec confirmation
   - Ajout des boîtes de confirmation pour valider les suppressions (overlay avec message d'avertissement)
   - Ajout du bouton "+ Ajouter un son" dans chaque preset déroulé
   - Formulaire inline pour ajouter un son dans un preset existant (nom et URL)
   - Intégration du modal pour ajouter un preset
   - Gestion de la réindexation des presets déroulés après suppression
6. Styles CSS ajoutés :
   - Styles pour les boutons de suppression
   - Styles pour les boîtes de confirmation (overlay + modal)
   - Styles pour le formulaire d'ajout de son inline
   - Styles pour les actions groupées (preset-actions, son-actions)

**Commentaire apporté par moi-même :**
Pas vraiment de commentaire. Cursor a fait ce qu'il fallait, autant niveau architechture que fonctionnellement. Je vais pouvoir passer a la partie backend afin qu'elle accepte ces nouvelles fonctionnalités

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