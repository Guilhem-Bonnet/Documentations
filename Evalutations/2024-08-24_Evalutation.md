# Évaluation Poussée en Développement de Jeux Vidéo

Heure de début d'évaluation: 10:40

## 1. Connaissance des Moteurs de Jeu
**Objectif :** Évaluer ta maîtrise des moteurs de jeu (Unity, Godot, Unreal Engine, etc.).

### Questions :
- Quel moteur de jeu utilises-tu le plus souvent et pourquoi ?

J'utilisais jusqu'à présent le moteur de jeu Unity. Le choix c'est imposé à moi car l'entreprise dans laquelle j'étais entrée utilisé déjà ce moteur. Mais sa reste un bon choix de moteur selon moi, car il était le moteur prédestiné aux indépendant par sa communauté, ses ressources et son accécibilité. Sans parlé du C# qui est mon language phare et qui m'as permis de facilement me lancé sur le moteur.
Aujourd'hui, j'ai essayé pendant quelque temps l'unreal engine 5 et je compte peaufiné mon expérience et mon expertice le concernant.
Sinon je suis en train de me penché sérieusement sur Godot, qui est depuis récemment un moteur à forte croissance, due au problèmes récent dans l'actualité concernant Unity et demandant aux développeurs indépendant de regarder ailleur, notemment l'open source. GoDot depuis l'ors est en forte croissance avec une communauté de plus en plus grande. Bien que sa spécialisation 2D était acceptable, le moteur avait du mal à se mettre au niveau en 3D. Mais depuis la version 4 il propose des lumière très convenable.

Aujourd'hui si je devais choisir un moteur je dirais Godot.
Bien que unity ne soit pas mort et peut nous réservé des surprise l'engouement s'en ai détaché et l'open source ne risque pas du jour au lendemain de nous réservé de mauvaises surprises.

Si je souhaite par contre me penché sur un gros projet en 3D avec une équipe complète, je pencherais plus pour l'Unreal engine 5, qui à énormément à offrir autant en expérience qu'en opportunitée de carière dans l'industrie.


- Explique comment tu structurerais un projet de jeu dans ce moteur (scènes, assets, scripts).

Pour moi l'organisation d'un projet est primordial.
Si c'est un petit projet je ferais à l'essentiel.
un dossier Scène, un dossier script, un dossier assets
dans le dossier assets une partie Art (textures, 3D etc ..) dédié aux artistes.
Pour un plus gros projet j'aurais segmenté par niveau de jeu pour les artistes.

Le défis est d'avoir une zone d'éléments réutilisable pour permettre une optimisation avec la réutilisabilité exemple : les textures

Pour les scripts c'est une autre affaire. Certains scripts se voient généraliste, d'autres réutilisable, ou encore omniprésent. Dès qu'il est possible de les cathégorisé je créer un dossier pour les rangé ensemble. Sinon les généraux restent à la racine de Script

- Comment gères-tu l'optimisation des performances dans ce moteur ?

Pour cette question je vais parlé de Unity(4ans d'expérience), car j'ai encore trop peu d'expérience avec les autres moteur.
Avec unity je vais concevoir les scripts théorique en amond pour les logiques complexe, je parle ici des scripts qui necessites des design pattern par exemple. Je vais prendre le temps de créer un patron de conception et d'incorporé mes diagrames.
Pour les petits scripts je vise toujours à pensé optimisé et efficace. Je part du principe qu'un script de plus de 700 lignes à un problèmes de réflexion. J'utilise des outils de visualisation des ressources pour vérifié les performences et détecté de potentiels problèmes. J'utilise des outils et technologies permettant de fort gain de ressources: réutilisation des prefabs et textures, bonne taille de texture, LOD, Oclussion culling avancé, système de préloading, scène streaming, object pooling, réflexion sur les lights avec gestion des light bake/mixed/réal time, j'essaye toujours d'avoir le moins possible de lumière en temp réel sans pour autant avoir un impact sur l'expérience. Le shadow cascade aussi, en fonction de la distance la finesse des shadow. Et aussi l'optimisation du code via le build pour retiré tous commentaire ou éléments non necessaire au fonctionnement du jeu.


- Quelle est ta méthode pour gérer les transitions de scènes et l'implémentation de systèmes de sauvegarde ?

En général pour la transition je fais un fondu au noir fade in fade out avec soit une caméra en dont destroy on load (surtout pour la VR) ou alors je fais un préfab de la caméra avec le système fade in et fade out sur chacune des scènes. Evidemment je rajoute un système de chargement et en général j'essaye de joueur au mieux avec les threads pour éviter un gros pic de performence durant le chargement et par la même occasion créer une nausée en VR (écran figé)

Pour les sauvegarde, je n'ai pas eu l'occasion de faire énormément de choses.Mes expérience se limitent au playerpref et j'ai implémenter une fois du SQLITE en y mettant les objets d'une scènes qui avaient bougé avec leurs transform. Je reporté ensuite leur transform sur l'objet cible au chargement.

### Exercice :
- Décris un système de gameplay complexe que tu as implémenté dans un moteur de jeu. Explique les choix techniques que tu as faits et les défis que tu as rencontrés.

Le plus gros projet sur lequel j'ai travaillé était un flipper.
La complexité était que c'était un réel flipper avec sa structure physique et des composant comme un tire bille avec un potentiomètre ou un accéléromètre, de tout avec une couche de unity et couplé avec de la VR. L'écran de jeu était en 4k, un autre écran était un HD, et le casque vr était en 4K aussi (hp reverb pro G2). Et il fallait que le jeu tourne sans aucune latence en 90fps pour ne pas avoir d'effet bizarre en VR.
Le challenge était compliqué, l'optimisation devait être ardue avec un lumière convaincante.

Heure de fin : 11:26

## 2. Programmation et Scripting
**Objectif :** Évaluer ta compétence en programmation et scripting pour le développement de jeux.

### Questions :
- Quels langages de programmation utilises-tu pour développer des jeux, et pourquoi ?
- Explique comment tu gères l'architecture des scripts dans un projet de jeu pour assurer une bonne maintenabilité.
- Comment abordes-tu la gestion des événements (comme les entrées utilisateur ou les collisions) dans tes jeux ?

### Exercice :
- Écris un script en C# (pour Unity) ou GDScript (pour Godot) qui implémente un comportement d'IA simple pour un ennemi (par exemple, un ennemi qui suit le joueur lorsqu'il est à une certaine distance).

## 3. Conception de Gameplay et Balancing
**Objectif :** Évaluer ta capacité à concevoir des systèmes de gameplay équilibrés et intéressants.

### Questions :
- Comment t'assures-tu que les mécaniques de jeu restent équilibrées et intéressantes pour le joueur ?
- Peux-tu donner un exemple d'une mécanique de jeu que tu as dû ajuster après les retours des joueurs ?
- Comment gères-tu la difficulté et la progression dans un jeu ?

### Exercice :
- Conçois un système de progression pour un jeu de type rogue-like. Décris les éléments clés du système (ex. : augmentation des statistiques, acquisition d'items, etc.) et explique comment tu équilibrerais ce système.

## 4. Graphismes et Animation
**Objectif :** Évaluer ta capacité à intégrer et à gérer les aspects visuels d’un jeu vidéo.

### Questions :
- Comment abordes-tu l'intégration des assets graphiques dans tes projets de jeu ?
- Quel est ton processus pour travailler avec des animations (par exemple, spritesheets, animations 3D) ?
- Comment optimises-tu les performances graphiques, notamment en ce qui concerne les shaders et le rendu ?

### Exercice :
- Décris un pipeline typique pour intégrer un modèle 3D animé dans ton moteur de jeu de choix, en passant par l'importation, l'application de textures, et l'intégration dans le projet avec les animations.

## 5. Conception Sonore
**Objectif :** Évaluer ta capacité à gérer les aspects audio d’un jeu vidéo.

### Questions :
- Comment choisis-tu et intègres-tu les effets sonores et la musique dans un jeu ?
- Comment gères-tu l'implémentation de l'audio dynamique ou adaptatif (ex. : la musique change selon les actions du joueur) ?
- Quel est ton processus pour équilibrer les différents éléments sonores dans un jeu ?

### Exercice :
- Imagine un jeu avec plusieurs environnements distincts. Décris comment tu gérerais l'ambiance sonore de ces environnements pour qu'ils se sentent uniques et immersifs.

## 6. Tests et Débogage
**Objectif :** Évaluer tes pratiques en matière de tests et de débogage dans le développement de jeux.

### Questions :
- Quelle est ta méthodologie pour tester les fonctionnalités de ton jeu ?
- Comment abordes-tu le débogage des bugs complexes dans un jeu vidéo ?
- Comment gères-tu les tests de performance, notamment pour assurer un bon framerate ?

### Exercice :
- Décris un bug particulièrement difficile que tu as rencontré dans un projet de jeu, et explique comment tu l'as résolu.

## 7. Documentation et Collaboration
**Objectif :** Évaluer ta capacité à documenter ton code et à travailler en équipe.

### Questions :
- Comment documentes-tu ton code et tes systèmes dans un projet de jeu ?
- Quelle est ton approche pour collaborer avec d'autres développeurs ou artistes sur un projet de jeu ?
- Comment gères-tu les versions et la fusion de code dans des projets en équipe ?

### Exercice :
- Rédige un extrait de documentation pour une fonctionnalité clé que tu as implémentée dans un jeu. Inclue des exemples de code et des explications sur le fonctionnement et l'utilisation de cette fonctionnalité.

## 8. Innovation et Créativité
**Objectif :** Évaluer ta capacité à innover et à proposer des concepts de jeu originaux.

### Questions :
- Comment trouves-tu l'inspiration pour de nouvelles idées de jeu ?
- Peux-tu donner un exemple d'une mécanique ou d'un concept de jeu unique que tu as créé ?
- Comment t'assures-tu que tes idées innovantes restent accessibles et amusantes pour les joueurs ?

### Exercice :
- Propose un concept de jeu original. Décris les mécaniques principales, l'histoire, et le style visuel. Explique pourquoi tu penses que ce jeu serait à la fois innovant et attrayant pour les joueurs.
