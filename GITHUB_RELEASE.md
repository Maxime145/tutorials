# Guide de Release

Ce guide explique comment créer des releases automatiques avec tarballs sur GitHub.

## Fonctionnement automatique

Le workflow `.github/workflows/release.yml` se déclenche **automatiquement** quand :

1. Vous pushez sur la branche `master`
2. Des fichiers dans `packages/` ou `package.json` ont changé

**Ce qu'il fait** :
1. Lit la version depuis `package.json` racine
2. Vérifie si le tag existe déjà
3. Sinon, génère les tarballs (`.tgz`) de tous les packages
4. Crée un tag Git (`v1.0.0`, `v1.1.0`, etc.)
5. Crée une GitHub Release avec les tarballs attachés
6. Génère automatiquement les commandes d'installation

## Créer une nouvelle release

### Étape 1 : Incrémenter la version

Modifiez la version dans `package.json` **à la racine** :

```json
{
  "name": "linting-monorepo",
  "version": "1.0.1"
}
```

### Étape 2 : Committer et pusher

```bash
git add package.json
git commit -m "chore: bump version to 1.0.1"
git push origin main
```

### Étape 3 : Attendre

Le workflow se lance automatiquement ! Rendez-vous sur :
- **Actions** → Voir le workflow en cours
- **Releases** → La nouvelle release apparaît quelques minutes après

## Installation par les utilisateurs

Une fois la release créée, vous pouvez installer les packages comme ceci :

### Angular
```bash
npm i -D https://github.com/Maxime145/linting-monorepo/releases/download/v1.0.0/linting-monorepo-eslint-config-angular-1.0.0.tgz

# Puis
npx install-linter-angular
```

### React
```bash
npm i -D https://github.com/Maxime145/linting-monorepo/releases/download/v1.0.0/linting-monorepo-eslint-config-react-1.0.0.tgz

# Puis
npx install-linter-react
```

### Vue
```bash
npm i -D https://github.com/Maxime145/linting-monorepo/releases/download/v1.0.0/linting-monorepo-eslint-config-vue-1.0.0.tgz

# Puis
npx install-linter-vue
```

> **Note** : Les commandes d'installation sont générées automatiquement dans la description de chaque release !

## Déclencher manuellement

Vous pouvez aussi déclencher le workflow manuellement :

1. Allez sur **Actions** dans GitHub
2. Sélectionnez **Create Release with Tarballs**
3. Cliquez sur **Run workflow**
4. Sélectionnez la branche `master`
5. Cliquez sur **Run workflow**

## Versionning recommandé

Suivez le [Semantic Versioning](https://semver.org/) :

- **1.0.0** → **1.0.1** : Bug fix, petit changement
- **1.0.0** → **1.1.0** : Nouvelle fonctionnalité (backward compatible)
- **1.0.0** → **2.0.0** : Breaking change (non-backward compatible)

### Exemples

```bash
# Bug fix
"version": "1.0.1"
git commit -m "fix: correct import path in utils"

# Nouvelle fonctionnalité
"version": "1.1.0"
git commit -m "feat: add support for Stylelint v17"

# Breaking change
"version": "2.0.0"
git commit -m "feat!: migrate to ESLint v10 (BREAKING CHANGE)"
```

## Vérifier une release

### Sur GitHub

1. Allez dans **Releases**
2. Vérifiez que la release `v1.0.x` existe
3. Vérifiez que les 5 fichiers `.tgz` sont attachés :
    - `linting-monorepo-utils-1.0.x.tgz`
    - `linting-monorepo-eslint-config-base-1.0.x.tgz`
    - `linting-monorepo-eslint-config-angular-1.0.x.tgz`
    - `linting-monorepo-eslint-config-react-1.0.x.tgz`
    - `linting-monorepo-eslint-config-vue-1.0.x.tgz`

### En local (tester l'installation)

```bash
# Installez depuis la release
npm i -D https://github.com/Maxime145/linting-monorepo/releases/download/v1.0.0/linting-monorepo-eslint-config-react-1.0.0.tgz

# Vérifiez que c'est installé
npm list @linting-monorepo/eslint-config-react

# Testez le script d'installation
npx install-linter-react

# Vérifiez les fichiers créés
ls -la eslint.config.js prettier.config.js stylelint.config.js
```

## Problèmes rencontrés

À faire évoluer au besoin

## Mettre à jour un package existant

```bash
# Désinstaller l'ancienne version
npm uninstall @linting-monorepo/eslint-config-react

# Installer la nouvelle version
npm i -D https://github.com/Maxime145/linting-monorepo/releases/download/v1.1.0/linting-monorepo-eslint-config-react-1.1.0.tgz
```

## Documentation à mettre à jour

Pensez à mettre à jour dans **README.md** :

```bash
# Remplacez v1.0.0 par la dernière version
npm i -D https://github.com/Maxime145/linting-monorepo/releases/download/v1.0.0/linting-monorepo-eslint-config-react-1.0.0.tgz
```
