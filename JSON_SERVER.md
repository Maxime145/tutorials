# Configurer un json server avec Faker

## `package.json` -> packages essentiels

```json
// index.js

{
  "name": "json-faker-server",
  "version": "1.0.0",
  "author": "Maxime Vaudon",
  "main": "index.js",
  "private": "true",
  "scripts": {
    "prepare": "npm run faker",
    "faker": "node index.js",
    "start": "npm run faker && json-server --watch db.json"
  },
  "dependencies": {
    "@faker-js/faker": "10.1.0",
    "json-server": "0.17.4"
  },
  "engines": {
    "node": ">=24.0.2",
    "npm": ">=11.3.0"
  }
}
```

## `index.js` -> Script de création de données

```js
const fs = require('fs');
const { faker } = require('@faker-js/faker');

// https://fakerjs.dev/api/

const db = {
    array: [...Array(5)].map((_value, index) => ({
        id: index + 1,
        name: faker.commerce.productName(),
        description: faker.lorem.paragraph(),
        isActive: faker.datatype.boolean(),
        sub_array: [...Array(5)].map(() => (
            faker.lorem.word()
        )),
        image: faker.image.avatar()
    })),
    object: {
        id: faker.number.int({ min: 0, max: 2 }),
        letter: faker.string.alpha({ length: 1 })
    }
};

fs.writeFile('./db.json', JSON.stringify(db, null, 4), {}, () => {
    console.warn('Database was created !');
});
```

## `.gitignore` -> à ajouter au votre

```text
db.json
```


