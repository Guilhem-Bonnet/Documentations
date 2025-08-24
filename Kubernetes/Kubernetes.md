---
title: Kubernetes
---
# Kubernetes

## 1. Introduction


### Qu'est ce que Kubernetes ?


Kubernetes est composé de clusters.

- Un `cluster` contient plusieurs `nodes` (nœuds)
- Les `nodes` sont des machines virtuelles (VM) ou des serveurs physiques
- Un node est soit un `control plane` (aussi appelé "Master"), soit un `Worker`


### Control Plane
Le control plane est en charge de la gestion du cluster. Il peut être distribué sur plusieurs nœuds pour la haute disponibilité.
Il fait tourner des composants tels que :
- l'API Server (API)
- le Controller Manager (c-m)
- le Scheduler (planificateur)
- etcd (base de données clé-valeur)

Ces composants fonctionnent ensemble pour la gestion et l'orchestration des applications dans le cluster.


### Les Nodes Worker
Les nodes Worker mettent leurs ressources à disposition pour faire tourner des pods.


### Pods
Un Pod est un groupe de conteneurs qui partagent une pile réseau et du stockage.
- Une application va tourner dans un ou plusieurs Pods
- Un pod a un ou plusieurs conteneurs


**Un Pod peut utiliser ou référencer d'autres ressources :**
- `ConfigMap` 
- `Secret` 
- `Persistent Volume Claim (PVC)` / `Persistent Volume (PV)`

Pour accéder à un pod, il faut une ressource de type Service.


### Ressources
Une ressource est un élément de haut niveau qui permet de créer ou de gérer des pods et d'autres objets dans Kubernetes.

Les catégories de ressources :
- **Workload** : *Création de pods, lancement d'applications*
    - `DaemonSet` : Un agent déployé sur chaque node (exemple : agent de monitoring). Il y a 1 pod de DaemonSet par node.
    - `Job / CronJob` : Lance des pods pour des applications de type batch ou planifiées.
    - `Deployment` : S'assure qu'on a un nombre constant de pods en fonctionnement.
    - `StatefulSet` : Permet de mettre en place, par exemple, un cluster de base de données avec un Master et plusieurs Slaves.
- **Configuration**
    - `Secret` : Gestion des données sensibles.
    - `ConfigMap` : Gestion des données de configuration.
- **Stockage**
    - `Persistent Volume (PV)` : Volume de stockage persistant.
    - `Persistent Volume Claim (PVC)` : Requête de stockage persistant.
    - `Storage Class` : Définit les classes de stockage disponibles.
- **Réseau**
    - `Service (svc)` : Abstraction réseau permettant d'accéder aux pods. Il existe plusieurs types de services (ClusterIP, NodePort, LoadBalancer). Un service permet de faire du load balancing et d'exposer les applications.
    - `Ingress (ing)` : Utilisé pour configurer un reverse-proxy appelé Ingress Controller. L'Ingress permet d'exposer des services HTTP/HTTPS en dehors du cluster via des règles de routage.

### Une application dans kubernetes
Une application est un ensemble de ressources.


Quand on déploie une application, elle va exister dans un namespace. Un namespace est une séparation logique du cluster, permettant de découper et d'organiser les ressources.

*Bonne pratique : créer un namespace par application.*

⚠️ Attention : par défaut, il n'y a pas de cloisonnement fort entre namespaces.
- Il faudra configurer le namespace avec des ressources dédiées si l'on souhaite les isoler les uns des autres, notamment au niveau réseau (par exemple avec des NetworkPolicies).

### Créer une ressource

Pour créer une ressource (pod ou autre) :
- Il faut définir un fichier YAML décrivant la ressource.
- Utiliser le binaire `kubectl` pour l'envoyer à l'API Server.

Exemple de fichier www.yaml basique :

```yml
apiVersion: v1 # pour un pod la valeur est V1
kind: Pod # type de ressource
metadata: # définir au minimum un name
    name: www 
spec: # spec va contenir au minimum container et sa définition
    containers:
    - name: www
    image: nginx:1.24
```
commande de lancement
```bash
kubectl apply -f www.yaml
``` 
