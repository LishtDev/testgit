# Guide de contribution à un projet GitHub

Ce document explique les commandes Git courantes pour contribuer à un projet hébergé sur GitHub.

## 1. Prérequis

- Installer [Git](https://git-scm.com/downloads).
- Avoir un compte [GitHub](https://github.com/).
- Avoir accès au dépôt, ou pouvoir le forker.

Vérifiez l’installation :

```bash
git --version
```

## 2. Récupérer le projet

### Cloner un dépôt auquel vous avez accès

```bash
git clone https://github.com/ORGANISATION/NOM-DU-DEPOT.git
cd NOM-DU-DEPOT
```

Remplacez `ORGANISATION` et `NOM-DU-DEPOT` par les bonnes valeurs.

### Contribuer via un fork

1. Sur GitHub, ouvrez le dépôt et cliquez sur **Fork**.
2. Clonez votre fork :

```bash
git clone https://github.com/VOTRE-UTILISATEUR/NOM-DU-DEPOT.git
cd NOM-DU-DEPOT
```

3. Ajoutez le dépôt original comme source amont (`upstream`) :

```bash
git remote add upstream https://github.com/ORGANISATION/NOM-DU-DEPOT.git
git remote -v
```

## 3. Créer une branche de travail

Récupérez les dernières modifications, puis créez une branche dédiée :

```bash
git switch main
git pull upstream main
git switch -c type/description-courte
```

Exemples de noms de branches :

- `feat/ajout-recherche`
- `fix/correction-connexion`
- `docs/maj-readme`

> Si vous contribuez directement au dépôt, utilisez `git pull origin main` au lieu de `git pull upstream main` si `origin` est le dépôt de référence.

## 4. Modifier et vérifier les fichiers

Après vos modifications, consultez l’état du dépôt :

```bash
git status
git diff
```

Pour ajouter des fichiers à l’index :

```bash
git add nom-du-fichier
```

Pour ajouter toutes les modifications suivies et les nouveaux fichiers non ignorés :

```bash
git add .
```

Vérifiez ce qui sera inclus dans le commit :

```bash
git diff --staged
```

## 5. Enregistrer les modifications (commit)

```bash
git commit -m "type: description claire"
```

Exemples :

```bash
git commit -m "feat: ajouter la recherche"
git commit -m "fix: corriger la validation du formulaire"
git commit -m "docs: mettre à jour le README"
```

Types courants : `feat` (fonctionnalité), `fix` (correction), `docs` (documentation), `test` (tests), `refactor` (refactorisation), `chore` (maintenance).

## 6. Synchroniser et envoyer la branche

Récupérez les dernières modifications du dépôt original si nécessaire :

```bash
git fetch upstream
git rebase upstream/main
```

Résolvez les éventuels conflits, puis envoyez votre branche vers votre fork :

```bash
git push -u origin type/description-courte
```

Adaptez le nom de branche à celui que vous avez créé. Pour une première publication, `-u` configure la branche distante de suivi.

## 7. Ouvrir une Pull Request (PR)

1. Allez sur GitHub et ouvrez votre fork.
2. Cliquez sur **Compare & pull request** (ou ouvrez une Pull Request depuis l’onglet **Pull requests**).
3. Vérifiez que la branche de base est `main` du dépôt original et que la branche de comparaison est votre branche.
4. Décrivez les changements, leur motivation et les tests effectués.
5. Envoyez la Pull Request et répondez aux retours de revue.

## 8. Mettre à jour sa branche après une revue

```bash
git fetch upstream
git rebase upstream/main
git push --force-with-lease
```

`--force-with-lease` peut être nécessaire après un rebase si la branche a déjà été poussée. Utilisez-le uniquement sur votre branche personnelle, jamais sur une branche partagée sans accord.

## 9. Commandes utiles

| Commande | Utilité |
|---|---|
| `git status` | Voir l’état du dépôt |
| `git branch` | Lister les branches locales |
| `git switch NOM-BRANCHE` | Changer de branche |
| `git switch -c NOM-BRANCHE` | Créer et utiliser une branche |
| `git log --oneline --graph --decorate -10` | Voir les derniers commits |
| `git diff` | Voir les modifications non indexées |
| `git diff --staged` | Voir les modifications indexées |
| `git stash` | Mettre temporairement ses changements de côté |
| `git stash pop` | Réappliquer les changements mis de côté |
| `git remote -v` | Afficher les dépôts distants |
| `git pull` | Récupérer et intégrer les changements distants |
| `git push` | Envoyer les commits vers le dépôt distant |

## 10. Bonnes pratiques

- Travaillez sur une branche dédiée, pas directement sur `main`.
- Faites des commits petits et explicites.
- Lancez les tests et les vérifications du projet avant d’ouvrir une PR.
- N’incluez jamais de mots de passe, clés API ou secrets dans vos commits.
- Suivez les conventions et le code de conduite du projet.
- Décrivez clairement le problème résolu et les changements apportés.

## Parcours rapide

Pour une contribution via un fork, après avoir configuré `upstream` :

```bash
git switch main
git pull upstream main
git switch -c feat/ma-contribution
# Modifiez les fichiers...
git status
git add .
git diff --staged
git commit -m "feat: décrire ma contribution"
git push -u origin feat/ma-contribution
```

Ensuite, ouvrez une Pull Request sur GitHub depuis votre branche vers `main` du dépôt original.
