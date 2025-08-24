### Corrigé Type : Connaissance des Moteurs de Jeu

#### **1. Quel moteur de jeu utilises-tu le plus souvent et pourquoi ?**

J'utilise principalement **Unreal Engine 5** pour mes projets de développement de jeux 3D. Ce choix s'explique par plusieurs raisons.```markdown
D'abord, Unreal Engine est reconnu pour ses capacités graphiques de pointe, notamment grâce à des technologies comme **Lumen** (pour l'éclairage global dynamique) et **Nanite** (pour la gestion des géométries complexes). Ces fonctionnalités permettent de créer des environnements extrêmement détaillés et réalistes, tout en maintenant des performances élevées.

De plus, Unreal Engine 5 offre un écosystème complet avec des outils intégrés pour l'animation, la physique, l'intelligence artificielle, et plus encore. Cela me permet de gérer tous les aspects de la création d'un jeu à partir d'une seule plateforme. La programmation en **C++** dans Unreal est puissante, bien que plus complexe que d'autres langages comme C#. Cependant, les **Blueprints** d'Unreal permettent de prototyper rapidement des fonctionnalités sans avoir besoin de coder directement, ce qui est un atout majeur pour la rapidité de développement.

J'utilise également **Godot 4** pour des projets plus modestes ou pour des jeux 2D. La raison principale est sa nature open-source et la rapidité avec laquelle je peux développer et déployer des projets simples. Godot est aussi très léger et flexible, ce qui est parfait pour des projets indépendants ou expérimentaux. Avec la version 4, Godot a amélioré ses capacités 3D, ce qui me permet de l'utiliser dans des contextes plus variés.

#### **2. Explique comment tu structurerais un projet de jeu dans ce moteur (scènes, assets, scripts).**

Dans **Unreal Engine 5**, structurer un projet de manière organisée est crucial, surtout pour des jeux complexes. Voici comment je m'y prends :

- **Dossier "Content"** : C'est le dossier racine où tous les assets sont stockés. Je divise ce dossier en sous-dossiers pour chaque type d'asset, par exemple, `Characters`, `Environments`, `UI`, `Audio`, `Animations`, etc.
  
- **Dossier "Levels"** : Je crée un dossier spécifique pour chaque niveau du jeu ou scène, contenant les objets, acteurs, et géométries spécifiques à ce niveau. Cela aide à garder les scènes isolées les unes des autres, facilitant ainsi les modifications et les tests.

- **Blueprints vs C++** : J'utilise les Blueprints pour prototyper rapidement des fonctionnalités et pour des interactions simples, tandis que le C++ est réservé aux systèmes critiques qui nécessitent des performances optimales ou des logiques complexes. Je sépare les scripts en différents dossiers selon leur fonction : `PlayerController`, `AI`, `UI`, etc.

- **Références croisées** : Pour éviter les dépendances circulaires, je veille à ce que les Blueprints et C++ soient bien séparés, en gardant les références croisées minimales et bien documentées.

#### **3. Comment gères-tu l'optimisation des performances dans ce moteur ?**

Dans Unreal Engine 5, l'optimisation est un aspect central du développement, surtout pour des jeux 3D ambitieux. Voici ma méthode :

- **Lumen et Nanite** : J'utilise **Lumen** pour gérer l'éclairage global de manière dynamique sans avoir besoin de baking complexe, ce qui permet d'économiser du temps et d'améliorer la qualité visuelle. **Nanite** est utilisé pour gérer les géométries complexes sans impact majeur sur les performances, en optimisant automatiquement les LOD (Level of Detail).

- **Profiling** : J'utilise régulièrement des outils de profiling comme le **Unreal Insights** pour surveiller les performances en temps réel, identifier les goulots d'étranglement, et ajuster les paramètres en conséquence.

- **Culling et LODs** : Le **frustum culling** et le **distance culling** sont configurés pour éviter de rendre des objets non visibles, et les LODs sont soigneusement définis pour les objets 3D afin de réduire le nombre de polygones affichés à distance.

- **Optimisation du code** : En C++, je m'assure que le code est optimisé en minimisant l'usage de l'allocation dynamique et en utilisant des structures de données adaptées. Les fonctions critiques sont profilées et optimisées pour réduire leur impact sur le CPU.

- **Textures et Materials** : Les textures sont compressées et optimisées en utilisant des formats comme **DXT1/5**, et les materials sont créés pour être aussi simples que possible, en utilisant des shaders personnalisés seulement lorsque nécessaire.

#### **4. Quelle est ta méthode pour gérer les transitions de scènes et l'implémentation de systèmes de sauvegarde ?**

Pour les **transitions de scènes**, j'utilise souvent une approche basée sur les **seamless loading screens** dans Unreal Engine. Cela implique de charger la prochaine scène en arrière-plan tout en affichant un écran de transition animé. Une technique courante est de précharger les données critiques avant d'effectuer la transition réelle, en utilisant des **streaming levels** pour gérer de grandes scènes de manière modulaire, ce qui permet de maintenir une expérience fluide sans interruptions.

Concernant les **systèmes de sauvegarde**, j'utilise un système basé sur les **SaveGame classes** d'Unreal. Ce système permet de sauvegarder et de charger des données de jeu complexes, telles que l'état du joueur, l'inventaire, et la progression du jeu, en sérialisant les données directement dans des fichiers binaires. J'implémente aussi un système de sauvegarde automatique qui enregistre les checkpoints critiques et permet aux joueurs de reprendre là où ils se sont arrêtés.

#### **Exercice : Décris un système de gameplay complexe que tu as implémenté dans un moteur de jeu. Explique les choix techniques que tu as faits et les défis que tu as rencontrés.**

Un des systèmes de gameplay les plus complexes que j'ai implémenté était un **système de gestion de groupe d'IA** dans un jeu de stratégie en temps réel développé sous Unreal Engine 5. Le défi principal était de permettre à des groupes d'unités contrôlés par l'IA de se comporter de manière coordonnée tout en réagissant dynamiquement aux actions du joueur.

**Choix techniques :**
- J'ai utilisé des **Behavior Trees** pour gérer les décisions des unités individuelles, avec des services et des tâches personnalisées pour assurer la communication entre les unités d'un même groupe.
- Un **système de perception** avancé a été intégré pour que les unités puissent détecter des ennemis, calculer des chemins d'évitement ou de poursuite, et coordonner leurs attaques en fonction des priorités du groupe.
- L'**optimisation des performances** a été un défi majeur, car le jeu devait gérer des centaines d'unités en temps réel. Pour cela, j'ai utilisé le **culling** pour les unités hors de l'écran et j'ai réduit la fréquence des mises à jour des unités éloignées du joueur.

**Défis rencontrés :**
- L'un des plus grands défis a été d'assurer une transition fluide entre les niveaux de décision (individuelle vs. de groupe) sans surcharger le CPU. J'ai dû itérer plusieurs fois sur les algorithmes de prise de décision pour équilibrer les performances et la réactivité.
- Un autre défi a été de synchroniser les animations avec les décisions prises par l'IA, notamment dans des scénarios complexes où plusieurs actions doivent se dérouler simultanément.

---

### **Évaluation de ce Cas Type :**

Ce corrigé type montre une excellente maîtrise des moteurs de jeu, en particulier **Unreal Engine 5**, avec un accent fort sur l'optimisation des performances et la gestion des systèmes complexes. Les réponses et l'exercice démontrent une capacité à travailler sur des projets de grande envergure, en utilisant des techniques avancées pour résoudre des problèmes spécifiques au développement de jeux.

### **Note pour cette section : 18/20**

**Commentaires :**  
Les réponses montrent une solide expertise technique et une capacité à adapter les méthodes en fonction des besoins du projet. L'approche structurée pour l'organisation des projets, couplée à une attention particulière aux détails techniques, est impressionnante. Le développeur pourrait encore améliorer son travail en explorant davantage l'intégration artistique et sonore, mais dans l'ensemble, il s'agit d'un travail très bien réalisé.

---

### **Amélioration des Systèmes de Sauvegarde :**

Pour améliorer l'intégration de systèmes de sauvegarde plus avancés, voici quelques exemples de ce que tu pourrais explorer :

### **1. Sauvegarde en Cloud :**
   - **Intégration Cloud :** Implémente des systèmes de sauvegarde en cloud, comme l'intégration avec des services tels que **Firebase** ou **AWS GameLift**. Cela permet aux joueurs de sauvegarder leurs données de jeu sur des serveurs distants, ce qui leur permet de récupérer leur progression sur différents appareils.
   - **Synchronisation Multiplateforme :** Assure la synchronisation des sauvegardes entre différentes plateformes (PC, console, mobile) afin que les joueurs puissent continuer leur progression d'un appareil à un autre sans interruption.

### **2. Systèmes de Sauvegarde Incrémentale :**
   - **Sauvegarde Incrémentale :** Implémente un système où seules les données modifiées depuis la dernière sauvegarde sont stockées, ce qui réduit la quantité de données à sauvegarder et accélère le processus. Cela est particulièrement utile pour les jeux avec de grandes quantités de données, comme les RPG ou les jeux de gestion.
   - **Historique des Sauvegardes :** Permet de garder un historique des sauvegardes pour que les joueurs puissent revenir à un```markdown
état antérieur du jeu en cas de problème ou s'ils souhaitent essayer différentes décisions sans perdre leur progression principale.

### **3. Chiffrement des Données de Sauvegarde :**
   - **Sécurité des Sauvegardes :** Implémente le chiffrement des données de sauvegarde pour protéger la progression des joueurs contre la corruption des données, les attaques externes, ou la triche. Des algorithmes comme **AES** peuvent être utilisés pour sécuriser les fichiers de sauvegarde.

### **4. Sauvegardes en Temps Réel :**
   - **Sauvegardes en Temps Réel :** Intègre un système de sauvegarde qui enregistre les données critiques en temps réel ou à intervalles réguliers sans interrompre l'expérience de jeu, minimisant ainsi les risques de perte de progression en cas de crash ou d'arrêt inattendu du jeu.
   - **Système de Checkpoints Automatiques :** Mets en place des checkpoints automatiques qui sauvegardent la progression du joueur à des moments critiques (par exemple, après avoir battu un boss ou terminé une mission), en plus des sauvegardes manuelles.

### **5. Gestion Avancée des États de Jeu :**
   - **Snapshotting :** Implémente une fonctionnalité de snapshot qui permet de capturer l'état complet du jeu à un instant donné, y compris les états intermédiaires des systèmes dynamiques, pour un retour en arrière précis en cas de besoin.
   - **Versioning des Sauvegardes :** Gère différentes versions de sauvegardes compatibles avec les mises à jour du jeu, ce qui permet de maintenir la compatibilité des sauvegardes même après des modifications significatives du gameplay ou des systèmes.

### **6. Intégration Sociale :**
   - **Partage de Sauvegardes :** Permets aux joueurs de partager leurs fichiers de sauvegarde avec d'autres, par exemple pour montrer leurs succès ou pour que des amis puissent continuer une partie commencée ensemble.
   - **Sauvegardes Collectives :** Implémente un système où plusieurs joueurs peuvent contribuer à une même sauvegarde dans un jeu coopératif ou multijoueur, permettant une progression collective et synchronisée.

### **7. Interface Utilisateur pour la Gestion des Sauvegardes :**
   - **Interface Avancée :** Crée une interface utilisateur permettant aux joueurs de gérer leurs sauvegardes de manière intuitive, y compris la possibilité de nommer, trier, et sélectionner des sauvegardes spécifiques, ainsi que d'afficher des métadonnées (date, heure, niveau atteint, etc.).
   - **Visualisation des Sauvegardes :** Ajoute des aperçus visuels (par exemple, captures d'écran associées à chaque sauvegarde) pour que les joueurs puissent facilement identifier et choisir la sauvegarde qu'ils souhaitent charger.

En explorant et en intégrant certaines de ces fonctionnalités avancées, tu pourrais grandement améliorer l'expérience utilisateur en termes de sauvegarde dans tes jeux, tout en assurant la sécurité, la flexibilité, et l'accessibilité des données de progression.
