# Configuration GitHub pour le monorepo

Comment configurer GitHub pour bloquer les merges si les checks échouent ?

## Fichiers créés

Trois fichiers ont été créés dans `.github/` :

```
.github/
|-- workflows/
|   |-- lint.yml           # Vérifie ESLint et Prettier
│   |-- test.yml           # Lance les tests et l'audit de sécurité
|-- dependabot.yml         # Config Dependabot
```

## Étape 1 : Activer la protection de branche (IMPORTANT)

Pour **bloquer les merges** si les checks échouent, vous devez configurer la protection de branche sur GitHub :

### Sur GitHub.com :

1. Allez dans **Settings** → **Branches** (dans le menu de gauche)

2. Sous **Branch protection rules**, cliquez sur **Add rule**

3. Configurez comme suit :
   - **Branch name pattern** : `master` (ou `develop` si vous l'utilisez)
   - **Require a pull request before merging**
     - Require approvals: 1 (optionnel)
   - **Require status checks to pass before merging**
     - Require branches to be up to date before merging
     - Dans la recherche, ajoutez ces checks (ils apparaîtront après le premier run) :
       - `ESLint Check`
       - `Prettier Check`
       - `Run Tests`
       - `Security Audit`

   - **Do not allow bypassing the above settings** (recommandé)

4. Cliquez sur **Create** / **Save changes**

## Déroulement des évènements

### Sur chaque Pull Request :

1. **ESLint Check** s'exécute
   - Passe si le code respecte les règles ESLint
   - Échoue sinon → **Merge bloqué**

2. **Prettier Check** s'exécute
   - Passe si le code est bien formaté
   - Échoue sinon → **Merge bloqué**

3. **Run Tests** s'exécute
   - Passe si tous les tests réussissent
   - Échoue sinon → **Merge bloqué**

4. **Security Audit** s'exécute
   - Passe si aucune vulnérabilité >= moderate
   - Échoue sinon → **Merge bloqué**

5. **Dependabot** crée des PRs automatiques
   - Chaque lundi à 9h
   - Met à jour les dépendances obsolètes
   - Crée max 5 PRs à la fois

## Configuration du package.json racine

Pour que les workflows fonctionnent, ajoutez ces scripts dans votre `package.json` racine :

```json
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "format": "prettier --write \"**/*.{js,ts,json,md,yml,yaml}\"",
    "format:check": "prettier --check \"**/*.{js,ts,json,md,yml,yaml}\"",
    "test": "npm test --workspaces --if-present"
  }
}
```

## Configuration ESLint à la racine

Créez un fichier `eslint.config.js` à la racine pour linter le monorepo lui-même :

```javascript
import js from '@eslint/js';

export default [
  js.configs.recommended,
  {
    files: ['**/*.js'],
    languageOptions: {
      ecmaVersion: 2025,
      sourceType: 'module',
      globals: {
        process: 'readonly',
        console: 'readonly',
        __dirname: 'readonly',
      },
    },
    rules: {
      'no-console': 'off', // Autorisé dans les scripts
    },
  },
  {
    ignores: ['**/node_modules/**', '**/dist/**', '**/build/**'],
  },
];
```

## Tester la configuration

### Test 1 : Vérifier que les workflows sont bien configurés

1. Créez une branche de test :

   ```bash
   git checkout -b test/github-actions
   ```

2. Faites un changement et pushez :

   ```bash
   echo "// test" >> packages/utils/index.js
   git add .
   git commit -m "test: verify GitHub Actions"
   git push origin test/github-actions
   ```

3. Créez une Pull Request sur GitHub

4. Vérifiez que les 4 checks s'exécutent :
   - ESLint Check
   - Prettier Check
   - Run Tests
   - Security Audit

### Test 2 : Vérifier que le merge est bloqué en cas d'erreur

1. Dans votre branche, ajoutez du code mal formaté :

   ```javascript
   // packages/utils/test.js
   const test = 'mal formaté'; // Espaces en trop
   ```

2. Commitez et pushez :

   ```bash
   git add .
   git commit -m "test: bad formatting"
   git push
   ```

3. Sur la PR, vous devriez voir :
   - Prettier Check échoué
   - Bouton "Merge" désactivé

4. Corrigez et pushez à nouveau :

   ```bash
   npx prettier --write packages/utils/test.js
   git add .
   git commit -m "fix: formatting"
   git push
   ```

5. Les checks repassent au vert

## Badge de statut (optionnel)

Ajoutez un badge dans votre README.md pour afficher le statut des checks :

```markdown
[![Lint & Format](https://github.com/VOTRE-USERNAME/linting-monorepo/actions/workflows/lint.yml/badge.svg)](https://github.com/VOTRE-USERNAME/linting-monorepo/actions/workflows/lint.yml)
[![Tests](https://github.com/VOTRE-USERNAME/linting-monorepo/actions/workflows/test.yml/badge.svg)](https://github.com/VOTRE-USERNAME/linting-monorepo/actions/workflows/test.yml)
```

Remplacez `VOTRE-USERNAME` par votre nom d'utilisateur GitHub.

## Personnalisation de Dependabot

Dans `.github/dependabot.yml`, modifiez cette ligne :

```yaml
reviewers:
  - 'Maxime145' # Ajoutez ou remplacez par votre username
```

Vous pouvez aussi ajuster :

- La fréquence : `daily`, `weekly`, `monthly`
- Le nombre max de PRs : `open-pull-requests-limit`
- Les labels appliqués

## Commandes utiles en local

Avant de pusher, testez en local :

```bash
# Vérifier ESLint
npm run lint

# Auto-fix ESLint
npm run lint:fix

# Vérifier le formatage
npm run format:check

# Auto-formater
npm run format

# Lancer les tests
npm test

# Audit de sécurité
npm audit
```

## Ressources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Branch Protection Rules](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
- [Dependabot Documentation](https://docs.github.com/en/code-security/dependabot)

**Votre monorepo est maintenant protégé par CI/CD !**

