# Avoir son code et son git au propre

## Husky

### Installation

```
$ npm i -D husky
$ npx husky init
```

### Configuration

```
// package.json
{
    "scripts": {
        "prepare": "husky init"
    }
}
```

```
// .gitignore
.husky/_
```

## pre-commit

Par exemple, vous pouvez vérifier si le code est bien formaté ou que le code ne comporte pas d'erreur avant que le commit ne soit créé.\
Pour cela, il faut créer un fichier `pre-commit`, dans le dossier `.husky`, qui portera la ou les commandes de vérification du  :

### Validation du formatage de code

#### Prérequis

```
$ npm i -D prettier
```

#### Configuration husky

```
$ echo "npx prettier --check ." > .husky/pre-commit
```

### Validation des commits

#### Prérequis

```
$ npm i -D git-precommit-checks
```

#### Configuration git-precommit-checks

```js
// git-precommit-checks.config.js
module.exports = {
    display: {
        // Utilise les notifications système pour nous signaler qu’un problème est détecté.
        notifications: true,
        // Affiche les chemins des fichiers et numéros de lignes ainsi que les contenus défaillants.
        // Pratique pour ouvrir via un "Ctrl + clic" le fichier au bon emplacement directement dans l'éditeur.
        offendingContent: true,
        // Si jamais on souhaite obtenir l’affiche dans le terminal du détail des règles en place.
        rulesSummary: false,
        // Si on veut afficher des statistiques simplifiées (exemple : "1 'error', 1 'warning'").
        shortStats: true,
        // Pour afficher le détail de chaque action exécutée, les fichiers analysés, le résumé des opérations.
        verbose: false,
    },
    rules: [
        // Règles globales, appliquées sur tous les contenus ajoutés
        {
            // On renseigne le message qui doit nous être affiché en cas de problème.
            message: 'Aurais-tu oublié de terminer certaines tâches ?',
            // Ici, on indique qu’on veut juste une alerte, sans stopper le commit. Par défaut, c'est renseigné à "false".
            nonBlocking: true,
            // On passe sous forme de texte ou d’expression rationnelle les contenus à rechercher.
            regex: /(?:FIXME|TODO)/,
        },
        {
            message: 'Tu as des marqueurs de conflits qui traînent',
            regex: /^[<>|=]{4,}/m,
        },
        {
            message:
                'Arrêt du commit : tu as renseigné des choses qui ne doivent pas être commitées !',
            regex: /do not commit/i,
        },
        // Ensuite, on peut spécifier des fichiers ou motifs particuliers pour appliquer nos règles,
        // ça se fait avec la propriété "filter".
        {
            // Là encore, on peut utiliser une expression rationnelle
            filter: /\.js$/,
            message: '🤔 Hum ! N’as-tu pas oublié de retirer du "console.log(…)" ?',
            nonBlocking: true,
            regex: /^\s*console\.log/,
        },
        // Spécifique à Ruby/Rails
        {
            filter: /_spec\.rb$/,
            message: 'Tu as laissé traîner un "focus" dans tes tests RSpec',
            regex: /(?:focus: true|:focus => true)/,
        },
        {
            filter: /\.rb$/,
            message:
                'Ça sent l’oubli après un debug manuel : regarde ce `binding.pry` qui traîne',
            regex: /^[^#]*\bbinding\.pry/,
        },
    ],
}
```

#### Configuration husky

```
$ echo "npx --no-install git-precommit-checks" > .husky/pre-commit
```

## commit-msg

On peut également vérifier le contenu du message d'un commit pour s'assurer qu'il répond aux normes git (ou les votres).

### Validation des messages de commit

#### Prérequis

```
$ npm i -D @commitlint/cli @commitlint/config-conventional
```

#### Configuration commitlint

```js
// commitlint.config.js
module.exports = {
  extends: ['@commitlint/config-conventional'],
}
```

#### Configuration husky

```
$ echo "npx --no-install commitlint --edit $1" > .husky/commit-msg 
```

## pre-push

Si vous souhaitez vérifier que le nom de votre branche est cohérent par rapport aux normes git (ou aux votres), vous pouvez passer par l'évènement `pre-push` et une librairie `validate-branch-name`.

### Configuration

#### Installation validate-branch-name

```
$ npm i -D validate-branch-name
```

#### Configuration validate-branch-name

```js
// validate-branch-namerc.config.js
module.exports = {
    pattern: '^(main|develop)$|^(feat|fix|tech|rel(?:ease)?)/.+$',
    errorMsg: 'La branche ne respecte pas nos conventions de nommage….,
}
```

#### Configuration husky pour validation la branche

```
$ echo "npx --no-install validate-branch-name" > .husky/pre-push
```
