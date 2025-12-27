# Markdown

Ce document regroupe les fonctionnalités principales du Markdown (GitHub Flavored Markdown).
Chaque fonctionnalité suit le même principe :
- Son nom
- Sa syntaxe
- Et son résultat

---

## Titres

Syntaxe :

    # Titre niveau 1
    ## Titre niveau 2
    ### Titre niveau 3
    #### Titre niveau 4
    ##### Titre niveau 5
    ###### Titre niveau 6

Résultat :

# Titre niveau 1
## Titre niveau 2
### Titre niveau 3
#### Titre niveau 4
##### Titre niveau 5
###### Titre niveau 6

---

## Commentaires / Citations

Syntaxe :

    > Mon commentaire

Résultat :

> Mon commentaire

---

## Mise en forme du texte

### Gras

Syntaxe :

    **Texte en gras**
    __Texte en gras__

Résultat :

**Texte en gras**  
__Texte en gras__

### Italique

Syntaxe :

    *Texte en italique*
    _Texte en italique_

Résultat :

*Texte en italique*  
_Texte en italique_

### Gras et italique

Syntaxe :

    ***Texte important***

Résultat :

***Texte important***

### Texte barré

Syntaxe :

    ~~Texte barré~~

Résultat :

~~Texte barré~~

---

## Liens

### Lien simple

Syntaxe :

    [My Link](https://github.com/)

Résultat :

[My Link](https://github.com/)

### Lien référencé

Syntaxe :

    [Markdown]

Déclaration du lien (en bas de fichier) :

    [Markdown]: https://guides.github.com/features/mastering-markdown/

Résultat :

[Markdown]

> Utile pour alléger le contenu du document

---

## Images

### Image fixe ou GIF

Syntaxe :

    [![Nom du lien](Lien_de_l_image)](Lien_de_redirection)

Résultat :

[![Home](https://image4.owler.com/logo/web-savvy-marketing_owler_20160228_232231_large.png)](https://github.com/)

---

### Vidéo YouTube via image

Syntaxe :

    [![Nom](http://img.youtube.com/vi/ID_VIDEO/0.jpg)]
    (https://www.youtube.com/watch?v=ID_VIDEO "Titre")

Résultat :

[![](http://img.youtube.com/vi/o77MzDQT1cg/0.jpg)](https://www.youtube.com/watch?v=o77MzDQT1cg "Super vidéo de Hytale")

---

## Listes

### Liste non ordonnée

Syntaxe :

    - Item 1
      - Item 1.1
        - Item 1.1.1
    - Item 2

Résultat :

- Item 1
  - Item 1.1
    - Item 1.1.1
- Item 2

> Deux espaces sont nécessaires pour chaque sous-niveau

---

### Liste ordonnée

Syntaxe :

    1. Premier
    2. Deuxième
    3. Troisième

Résultat :

1. Premier
2. Deuxième
3. Troisième

---

### Liste de tâches

Syntaxe :

    - [x] Tâche terminée
    - [ ] Tâche à faire

Résultat :

- [x] Tâche terminée
- [ ] Tâche à faire

---

## Code

### Code en ligne

Syntaxe :

    Voici du `code inline`

Résultat :

Voici du `code inline`

---

### Bloc de code

Syntaxe :

        function hello() {
          console.log("Hello World");
        }

Résultat :

    function hello() {
      console.log("Hello World");
    }

---

## Spoiler / Contenu repliable

Syntaxe :

    <details>
      <summary>Titre</summary>

      Contenu caché
    </details>

Résultat :

<details>
  <summary>Titre</summary>

  Contenu caché
</details>

---

## Tableaux

Syntaxe :

    | Nom  | Valeur  |
    | ---- | ------- |
    | Nom1 | Valeur1 |
    | Nom2 | Valeur2 |

Résultat :

| Nom  | Valeur  |
| ---- | ------- |
| Nom1 | Valeur1 |
| Nom2 | Valeur2 |

---

## Ligne de séparation

Syntaxe :

    ---

Résultat :

---

---

## Échappement de caractères

Syntaxe :

    \*Texte non interprété\*

Résultat :

\*Texte non interprété\*

---

## HTML dans Markdown

Syntaxe :

    <p style="color:red;">Texte rouge</p>

Résultat :

<p style="color:red;">Texte rouge</p>

---

## Notes de bas de page

Syntaxe :

    Texte avec une note[^1]

    [^1]: Contenu de la note

Résultat :

Texte avec une note[^1]

[^1]: Contenu de la note

---

## Liens de référence

    [Markdown]: https://guides.github.com/features/mastering-markdown/
    [embed youtube]: http://embedyoutube.org/

---
