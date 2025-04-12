

# Algorithmes de Graphes
Utilisés pour la navigation et la recherche de chemins dans les jeux.
- [**A***](details/Astar) : Permet de trouver le chemin le plus court entre deux points en utilisant une heuristique pour améliorer la performance par rapport à Dijkstra.
- [**Dijkstra**](details/Dijkstra) : Trouve le plus court chemin entre un nœud de départ et tous les autres nœuds dans un graphe, sans prendre en compte des heuristiques.
- [**Navigation Mesh**](details/NavigationMesh) : Utilisé pour les environnements complexes, permet une navigation plus flexible que les simples graphes de noeuds.

# Algorithmes de Physique
Simulent le comportement réaliste des objets et environnements.
- [**Physique**](details/Physique) : Gère la gravité, la résistance de l'air, et autres forces de la nature.
- [**Collisions**](details/Collisions) : Détecte et gère les interactions entre objets dans le jeu.
- [**Dynamiques des fluides**](details/Dynamiquesdesfluides) : Simule le mouvement et l'interaction des fluides.
- [**Simulations basées sur les particules**](details/Simulationsbaséessurlesparticules) : Pour les effets avancés de destruction, de liquides et de vêtements.
- [**Calculs sur GPU**](details/CalculssurGPU) : Utilisation du GPU pour des simulations physiques plus complexes et performantes.

## Les moteurs de physiques
- [**Box2D**](details/Box2D) : Moteur 2D, utilisé pour des jeux nécessitant des simulations physiques réalistes.
- [**PhysX**](details/PhysX) : Moteur 3D de NVIDIA, supporte des calculs physiques complexes, y compris la simulation de tissus et de fluides.

# Algorithmes de rendu 3D
Créent des images 3D à partir de modèles 2D.
- [**Ray tracing**](details/Raytracing) : Simule le chemin de la lumière pour produire des images réalistes avec des effets de réflexion, réfraction, et ombres douces.
- [**Ray tracing en temps réel**](details/Raytracingentempsréel) : Pour un rendu plus réaliste grâce à des calculs de lumière avancés.
- [**Rasterisation améliorée**](details/Rasterisationaméliorée) : Techniques optimisées pour un rendu rapide sans sacrifier la qualité visuelle.
- [**Global Illumination**](details/GlobalIllumination) : Simule le comportement complexe de la lumière dans les scènes pour un réalisme accru.
- [**Culling**](details/Culling)
  - **Occlusion culling** : Ignore les objets non visibles par la caméra car bloqués par d'autres objets.
  - **Frustum culling** : Ignore les objets en dehors du champ de vision de la caméra.
- [**Shaders**](details/Shaders) : Scripts qui déterminent l'aspect visuel des surfaces dans le jeu, incluant les textures, l'éclairage, et les effets spéciaux.

# IA et Machine Learning
Améliorent le comportement des PNJ et l'expérience de jeu.
- [**Arbres de décision**](details/Arbresdedécision) : Modélisent les choix disponibles pour l'IA, permettant de prendre des décisions basées sur différentes conditions.
- [**Machine learning**](details/Machinelearning) : Permet aux PNJ d'apprendre et d'améliorer leur comportement au fil du temps.
- [**Réseaux de neurones**](details/Réseauxdeneurones) : Simulent le fonctionnement du cerveau humain pour permettre des décisions complexes et l'apprentissage profond.
- [**Apprentissage par renforcement**](details/Apprentissageparrenforcement) : Permet à l'IA d'apprendre de ses actions pour améliorer ses stratégies au fil du temps.
- [**Simulation de foule**](details/Simulationdefoule) : Algorithmes pour simuler le comportement de groupes importants de personnages.
- [**Procedural Content Generation via Machine Learning (PCGML)**](details/ProceduralContentGenerationviaMachineLearning(PCGML)) : Utilise le machine learning pour générer du contenu de jeu de manière plus sophistiquée et adaptative.


# Systèmes de particules
Génèrent et contrôlent des effets visuels complexes comme le feu, la fumée, ou les explosions grâce à la simulation de grandes quantités de petites particules.
- [**Simulation de fluides et de gaz**](details/Simulationdefluidesetdegaz) : Techniques avancées pour la simulation de mouvements et interactions de fluides.
- [**VFX graphiques sur shaders**](details/VFXgraphiquessurshaders) : Création de visuels complexes directement dans les shaders pour plus d'efficacité.


# LOD (Level of Detail)
Optimise les performances en ajustant la complexité des modèles 3D en fonction de leur distance à la caméra pour maintenir une haute performance sans sacrifier la qualité visuelle.
- [**Streaming de contenu basé sur la position**](details/Streamingdecontenubasésurlaposition) : Chargement dynamique des assets en fonction de la position du joueur pour permettre de vastes mondes ouverts.
- [**LOD adaptatif**](details/LODadaptatif) : Ajustement en temps réel du niveau de détail selon la charge système et les critères visuels.


# Optimisation et Scalabilité
- [**Data-Oriented Design**](details/Data-OrientedDesign) : Approche de conception et de développement qui met l'accent sur l'organisation et l'accès aux données pour optimiser les performances et l'utilisation de la mémoire.
- [**Moteurs de jeu modulaires**](details/Moteursdejeumodulaires) : Architectures permettant une plus grande flexibilitante une plus grande flexibilité et adaptabilité dans le développement de jeux.


# Réseaux et Multi-joueurs
Gèrent la communication et la synchronisation entre joueurs dans les jeux en ligne.
- [**Prédiction**](details/Prédiction) : Anticipe les actions des joueurs pour réduire le décalage perçu dû à la latence.
- [**Interpolation**](details/Interpolation) : Lisse les mouvements des objets entre les mises à jour reçues pour éviter les saccades.
- [**Rollback Netcode**](details/RollbackNetcode) : Pour améliorer l'expérience en multijoueur, en particulier dans les jeux de combat, en réduisant la latence perçue.
- [**Synchronisation d'état déterministe**](details/Synchronisationd'étatdéterministe) : Assure une expérience multijoueur cohérente même avec des latences réseau variables.

# Culling et optimisation spatiale
Améliorent les performances en traitant uniquement les objets visibles ou pertinents.
- [**Quad-trees**](details/Quad-trees) : Divisent un espace 2D en quatre quadrants pour une gestion efficace des objets spatiaux.
- [**Octrees**](details/Octrees) : Extension des quad-trees dans un espace 3D, divisant l'espace en huit octants.

# Génération procédurale
Crée du contenu de manière algorithmique pour offrir une expérience unique à chaque partie.
- [**Bruit de Perlin**](details/BruitdePerlin) : Génère des textures, des terrains, et d'autres éléments de manière naturelle et aléatoire.
- [**Machine Learning pour PCG**](details/MachineLearningpourPCG) : Utilisation du machine learning pour créer des algorithmes de génération procédurale qui s'adaptent et apprennent de préférences des joueurs.
- [**Génération de monde infini**](details/Générationdemondeinfini) : Techniques permettant de créer des mondes qui se génèrent dynamiquement et infiniment en explorant.

