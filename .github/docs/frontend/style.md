# OS Job-Project

# Ajout et/ou modification de fichiers .scss

1.  ## Choisir le bon dossier

    -   `base/` : ici on ajoute les fichiers qui servent de base au style du site. Par exemple les fichiers:

        -   `_reset.scss` permet de réinitialiser les comportements liés aux navigateurs ; box-sizing, margin, padding, scroll-behavior etc...
        -   `_typography.scss` contient tout ce qui concerne le texte

    -   `components/`: Ce dossier est utilisé pour les petits components réutilisables tels que des boutons, des inputs, des icones etc...

    -   `layouts/`: Les éléments réutilisables plus large : header, footer, formulaires, grid...

    -   `pages/`: on stock ici le style utile à chaque page et qui n'est pas utilisé ailleurs : `_home.scss`, `_blog.scss`...

    -   `themes/`: Ici sont rangés les fichiers thématiques, c'est a dire les fichiers pour le dark mode, pour la utilisateur et un autre pour la partie admin si les deux n'ont pas le même thême.

    -   `vendors/`: Ressources tiers comme Bootstrap par exemple

2.  ## Nommer son fichier

Excepter le fichier index.scss principal, tous les fichiers commence par un underscore suivi d'une minuscule: `_footer.scss`;

Dès que votre fichier est créé, il faut l'importer dans le fichier `_index.scss` en utiliser la commande suivante : `@forward 'footer.scss';`.

3.  ## Importer et utiliser les variables, mixins ou autres utils

    -   **Variables** :

    Pour pourvoir utiliser une variable, il faut l'importer en haut du fichier avec @use:

    ```
    @use '../utils/variables' as v;
    ```

    Ensuite, on l'appelle dans notre code en notant v. avant:

    ```
    .div {
            colors: v.$primary-color;
    }
    ```

    -   **Mixins** :

    Pour les mixins, même principe :

    ```
    @use '../utils/mixins' as m;
    ```

    cependant pour les utiliser on les appelle avec `@include` :

    ```
    .div {
        @include m.font($color: v.$color, $size: v.$fontSize-normal);
    }
    ```

    -   **Fonctions** :

    ```
    @use 'functions' as f;

    .div {
        f.invert(v.primary-color, 80%);
    }
    ```

# Nommenclature BEM

Pour ce projet, pour une question de lisibilité, on va utiliser la nommenclature **BEM : Block - Element - Modifier**

Pour se faire chaque bloc aura une classe, son élément enfant contiendra la classe du parent suivi de \_\_<nomduchild>.

Si un élément spécifique est modifié sa classe finie par --<nomdumodifier>.

Exemple :

```
<header className="header">
    <img className="header__logo" src="../assets/logo.webp" />
    <nav className="header__nav">
        <ul className="header__list">
            <li className="header__item"><a href="#" className="header__link">Home</a></li>
            <li className="header__item"><a href="/annonces" className="header__link">Annonces</a></li>
            <li className="header__item"><a href="/articles" className="header__link">Articles</a></li>
        </ul>
        <ul className="header__list--small">
            <li className="header__item"><a href="/suivi" className="header__link">Suivi</a></li>
            <li className="header__item header__item--last"><a href="/connexion" className="header__link">Connexion</a></li>
        </ul>
    </nav>
</header>
```

---

**_Comme vous l'avez remarqué on évite le nesting de plus de 2 éléments, les classes ne sont pas : `header__nav__item__link` mais `header__nav`, `header__link`, etc..._**
**_Pour le nommage des classes, on réfléchi si la classe parent est ou peut-être utilisée ailleurs :_**
**_Nommer une balise <li> `nav__item` peut poser problème puisqu'on peut avoir plusieurs menus de navigation: dans le header, dans le footer, sur le côté etc..._**
