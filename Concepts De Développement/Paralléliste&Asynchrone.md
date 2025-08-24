---
title: Concurrence, Parallélisme et Asynchrone en .NET
---

# Documentation technique – Concurrence, Parallélisme et Asynchrone en .NET

## 1. Introduction étendue

### Objectif
Fournir une vision claire et professionnelle des différents **modèles d'exécution concurrente et asynchrone** en .NET, leurs **usages respectifs**, **différences fondamentales**, et **choix techniques** à adopter selon les cas.

---

## 2. Partie 1 – Concepts fondamentaux

### 2.1 Concurrence vs Parallélisme

| Concept        | Définition                                                                 |
|----------------|----------------------------------------------------------------------------|
| **Concurrence**| Capacité d’un programme à gérer plusieurs tâches *simultanément* (même si exécutées en alternance sur un seul cœur). |
| **Parallélisme**| Exécution de plusieurs tâches en **même temps** sur **plusieurs cœurs** de processeur.                    |

> ⚠ Concurrence ≠ Parallélisme (mais l’un peut impliquer l’autre)

---

## 3. Partie 2 – Panorama des outils .NET

### 3.1 `Thread`

- Objet bas niveau pour lancer une exécution parallèle.
- Lourd à créer (stack dédiée, appel système).
- Peu utilisé directement sauf cas spécifiques (longue vie, priorité, accès natif).

### 3.2 `ThreadPool`

- Pool interne de threads réutilisables.
- Géré automatiquement par .NET.
- Utilisé par `Task`, `Timer`, `BeginInvoke`, etc.

### 3.3 `Task` et `Task<T>`

- Abstraction de travail **asynchrone ou parallèle**.
- Peut s’exécuter via `ThreadPool`, mais pas nécessairement.
- Associé au modèle **async/await**.

```csharp
Task.Run(() => { /* code parallèle */ });
await Task.Delay(1000); // code asynchrone
```

### 3.4 `async` / `await`

- Modèle **asynchrone non-bloquant**.
- Libère le thread pendant l’attente (E/S, temporisation).
- Reprend l'exécution après complétion de la tâche.

```csharp
public async Task<string> LoadDataAsync()
{
    var response = await httpClient.GetAsync("https://api.com");
    return await response.Content.ReadAsStringAsync();
}
```

### 3.5 `Parallel` (TPL)

- Exécution parallèle **data-centric**.
- Utilise le `ThreadPool`.
- Permet d’exécuter des boucles `for`, `foreach` ou des actions en parallèle.

```csharp
Parallel.For(0, 10, i =>
{
    Console.WriteLine($"Processing item {i}");
});
```

### 3.6 `PLINQ` (Parallel LINQ)

- Version parallèle de LINQ.
- Traitement de collections avec parallélisme automatique.

```csharp
var results = data.AsParallel()
                  .Where(x => x.IsValid())
                  .Select(x => x.Compute())
                  .ToList();
```

---

## 🔧 Partie 3 – Bas niveau : ce qui se passe sous le capot

### 1. `async/await`

- **Compilation** transforme le code en **machine à états (state machine)**.
- Le `await` insère un point de **suspension** ; le code est fractionné avant/après.
- Pas de thread bloqué : il est libéré jusqu’à la complétion.
- Le résultat est **repris via le SynchronizationContext** (ex: UI thread) ou via un `TaskScheduler`.

### 2. `Task.Run`

- Planifie le travail dans le `ThreadPool`.
- Peut créer une `Task` chaude (démarre immédiatement) ou froide (déclenchée plus tard).

### 3. `Parallel` et `PLINQ`

- Utilisent des **work-stealing schedulers**.
- Le runtime optimise la répartition sur les **cœurs logiques disponibles**.

---

## 4. Partie 4 – Comparaison & stratégies de choix

| Objectif                                 | Recommandation                  | Commentaire |
|------------------------------------------|----------------------------------|-------------|
| Attente d'I/O (fichier, réseau, base)    | `async/await` + `Task`          | Très efficace, non-bloquant |
| Travail CPU-bound                        | `Parallel` / `Task.Run`         | Optimisation multicoeurs     |
| Exécution manuelle bas niveau            | `Thread`                        | Cas très spécifiques         |
| Pipeline de traitement parallèle         | `PLINQ`, `Dataflow`, `Channel`  | Optimisé pour transformation de données |
| UI responsive (WinForms, WPF, MAUI)      | `async/await` avec `SynchronizationContext` | Évite de bloquer le thread UI |

---

## 5. Partie 5 – Bonnes pratiques & erreurs courantes

### Bonnes pratiques
- **Préférer `async/await`** dès que possible pour tout ce qui est I/O.
- Utiliser `ConfigureAwait(false)` en **code bibliothèque** pour éviter de capturer le contexte.
- Ne **jamais `Task.Wait()` ou `.Result`** → risque de deadlock.
- Mesurer et profiler avant de paralléliser du code CPU.

### Erreurs fréquentes
- Mélanger `async/await` avec `Thread.Sleep` ou `Task.Wait`.
- Mal gérer les exceptions dans les `Task` (toujours utiliser `await` pour propager l’erreur).
- Abuser du parallélisme : risque de contention, surchauffe CPU.

---

## 6. Annexe – Approfondissements et histoire

### Historique .NET
| Époque | Évolution |
|--------|-----------|
| .NET 1.0 | `Thread`, `ThreadPool`, `Monitor` |
| .NET 4.0 (2010) | `Task`, TPL, `Parallel` |
| C# 5 / .NET 4.5 (2012) | `async` / `await` |
| .NET Core / .NET 5+ | `ValueTask`, channels, `IAsyncEnumerable` |

### Outils avancés
- `Channel<T>` (producteur/consommateur thread-safe)
- `AsyncLock`, `SemaphoreSlim`
- `IAsyncEnumerable<T>` + `await foreach`

---

## Fiche récapitulative

### Glossaire
- **Thread** : Exécution parallèle manuelle.
- **Task** : Abstraction de travail (parallèle ou asynchrone).
- **async/await** : Syntaxe pour la programmation asynchrone.
- **TPL** : Task Parallel Library.
- **PLINQ** : LINQ exécuté en parallèle.
- **Thread-safe** : Résistant aux accès concurrents.
- **SynchronizationContext** : Contexte d'exécution de continuation.

### Check-list choix d’implémentation

| Situation                                      | Outil recommandé          |
|-----------------------------------------------|----------------------------|
| I/O long (HTTP, fichiers)                     | `async` / `await`          |
| Boucle CPU-intensive                          | `Parallel.For`, `Task.Run` |
| Production/consommation concurrente           | `Channel<T>`, `BlockingCollection` |
| UI responsive (WPF, WinForms, MAUI)           | `async/await`, `Dispatcher.Invoke` |
| Traitement par lot / transformation de données| `PLINQ`, `Dataflow`        |
