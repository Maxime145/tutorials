# Markdown

Ce document regroupe les fonctionnalités principales du Markdown. Chaque fonctionnalité suit le même principe :

- Son nom
- Sa syntaxe
- Et son résultat

## Titres

Syntaxe :

```markdown
# Titre niveau 1
## Titre niveau 2
### Titre niveau 3
#### Titre niveau 4
##### Titre niveau 5
###### Titre niveau 6
```

Résultat :

# Titre niveau 1
## Titre niveau 2
### Titre niveau 3
#### Titre niveau 4
##### Titre niveau 5
###### Titre niveau 6

## Commentaires / Citations

Syntaxe :

```markdown
> Mon commentaire
```

Résultat :

> Mon commentaire

## Mise en forme du texte

### Gras

Syntaxe :

```markdown
**Texte en gras**
__Texte en gras__
```

Résultat :

**Texte en gras**  
__Texte en gras__

### Italique

Syntaxe :

```markdown
*Texte en italique*
_Texte en italique_
```

Résultat :

*Texte en italique*  
_Texte en italique_

### Gras et italique

Syntaxe :

```markdown
***Texte important***
```

Résultat :

***Texte important***

### Texte barré

Syntaxe :

```markdown
~~Texte barré~~
```

Résultat :

~~Texte barré~~

## Liens

### Lien simple

Syntaxe :

```markdown
[My Link](https://github.com/)
```

Résultat :

[My Link](https://github.com/)

### Lien référencé

Syntaxe :

```markdown
// Pour appeler le lien dans le fichier
[Markdown]

// Pour déclarer le lien (généralement en bas du fichier)
// Automatiquement caché
[Markdown]: <https://guides.github.com/features/mastering-markdown/>
```

Résultat :

[Markdown]

> Utile pour alléger la lecture du code.

## Images

### Image fixe ou GIF

Syntaxe :

```markdown
[![Nom du lien](Lien_de_l_image)](Lien_de_redirection)
```

Résultat :

[![Home](https://image4.owler.com/logo/web-savvy-marketing_owler_20160228_232231_large.png)](https://github.com/)

### Vidéo YouTube via image

Syntaxe :

```markdown
[![Nom](http://img.youtube.com/vi/ID_VIDEO/0.jpg)]
(https://www.youtube.com/watch?v=ID_VIDEO "Titre")
```

Résultat :

[![](http://img.youtube.com/vi/o77MzDQT1cg/0.jpg)](https://www.youtube.com/watch?v=o77MzDQT1cg "Super vidéo de Hytale")

## Listes

### Liste non ordonnée

Syntaxe :

```markdown
- Item 1
  - Item 1.1
    - Item 1.1.1
- Item 2
```

Résultat :

- Item 1
  - Item 1.1
    - Item 1.1.1
- Item 2

> Deux espaces sont nécessaires pour chaque sous-niveau

### Liste ordonnée

Syntaxe :

```markdown
1. Premier
2. Deuxième
3. Troisième
```

Résultat :

1. Premier
2. Deuxième
3. Troisième

### Liste de tâches

Syntaxe :

```markdown
- [x] Tâche terminée
- [ ] Tâche à faire
```

Résultat :

- [x] Tâche terminée
- [ ] Tâche à faire

## Code

### Code en ligne

Syntaxe :

```markdown
Voici du `code inline`
```

Résultat :

Voici du `code inline`

### Bloc de code

Syntaxe :

````markdown
```js
function hello() {
  console.log("Hello World");
}
```
````

Résultat :

```js
function hello() {
  console.log("Hello World");
}
```

## Spoiler / Contenu repliable

Syntaxe :

```markdown
<details>
  <summary>Titre</summary>

  Contenu caché
</details>
```

Résultat :

<details>
  <summary>Titre</summary>

  Contenu caché
</details>

## Tableaux

Syntaxe :

```markdown
| Nom  | Valeur  |
| ---- | ------- |
| Nom1 | Valeur1 |
| Nom2 | Valeur2 |
```

Résultat :

| Nom  | Valeur  |
| ---- | ------- |
| Nom1 | Valeur1 |
| Nom2 | Valeur2 |

## Ligne de séparation

Syntaxe :

```markdown
---
```

Résultat :

---

## Échappement de caractères

Syntaxe :

```markdown
\*Texte non interprété\*
```

Résultat :

\*Texte non interprété\*

## HTML dans Markdown

Syntaxe :

```markdown
<p style="color:red;">Texte rouge</p>
```

Résultat :

<p style="color:red;">Texte rouge</p>

## Notes de bas de page

Syntaxe :

```mardown
Texte avec une note[^1]

// Elle va apparaitre à la fin du fichier
[^1]: Contenu de la note
```

Résultat :

Texte avec une note[^1]

[^1]: Contenu de la note

## Liens de référence
> Les liens suivants sont bien invisibles !

[Markdown]: <https://guides.github.com/features/mastering-markdown/>
[embed youtube]: <http://embedyoutube.org/>
