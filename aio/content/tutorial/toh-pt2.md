# Afficher une liste de sélection

Ce tutoriel vous montre comment:

* Etendre l'application Tour of Heroes pour afficher une liste de héros.
* Permettre aux utilisateurs de sélectionner un héros et d'afficher les détails de ce héros.

<div class="alert is-helpful">

Pour l'exemple d'application que cette page décrit, voir le <live-example></live-example>.

</div>

## Créer des héros mockés

La première étape consiste à créer des héros à afficher.

Créez un fichier appelé `mock-heroes.ts` dans le répertoire `src/app/`.
Définissez une constante de `HEROES` comme un ensemble de dix héros et exportez-le.
Le fichier doit ressembler à ceci.

<code-example header="src/app/mock-heroes.ts" path="toh-pt2/src/app/mock-heroes.ts"></code-example>

## Affichage des héros

Ouvrez le fichier de classe `HeroesComponent` et importez les mocks de `HEROES`.

<code-example header="src/app/heroes/heroes.component.ts (import HEROES)" path="toh-pt2/src/app/heroes/heroes.component.ts" region="import-heroes"></code-example>

Dans la classe `HeroesComponent`, définir une propriété de composant appelée `heroes` pour exposer le tableau `HEROES`.

<code-example header="src/app/heroes/heroes.component.ts" path="toh-pt2/src/app/heroes/heroes.component.ts" region="component"></code-example>

### Liste des héros avec `*ngFor`

Ouvrez le fichier de template `HeroesComponent`et faire les changements suivants:

1.  Ajoutez un `<h2>` en haut du fichier.
2.  Sous le `<h2>`, ajoutez un élément `<ul>`.
3.  Dans l'élément `<ul>`, insérez un `<li>`.
4.  Mettre un `<button>` dans `<li>` qui affiche les propriétés d'un `hero` à l'intérieur d'un élément `<span>`.
5.  Ajoutez des classes CSS pour styliser le composant.

Pour ressembler à ceci:

<code-example header="heroes.component.html (heroes template)" path="toh-pt2/src/app/heroes/heroes.component.1.html" region="list"></code-example>

Cela affiche une erreur car la propriété `hero` n'existe pas.
Pour avoir accès à chaque héros individuel et les énumérer tous, ajoutez un `*ngFor` dans `<li>` pour itérer dans la liste des héros:

<code-example path="toh-pt2/src/app/heroes/heroes.component.1.html" region="li"></code-example>

Le [`*ngFor`](guide/built-in-directives#ngFor) est une directive *repeater* dans Angular.
Il répète l'élément hôte pour chaque élément d'une liste.

La syntaxe de cet exemple est la suivante:

| Syntaxe   | Détails |
|:---      |:---     |
| `<li>`   | L'élément hôte.                                                                  |
| `heroes` | Terne la liste des héros mockés de la classe `HeroesComponent`, la liste des héros mockés. |
| `hero`   | Termine l'objet héros actuel pour chaque itération via la liste.            |

<div class="alert is-important">

N'oubliez pas de mettre l'astérisque `*` devant de `ngFor`.
C'est une partie importante de la syntaxe.

</div>

Après que le navigateur ait rafraîchi, la liste des héros apparaît.

<div class="callout is-helpful">

<header>Éléments interactifs</header>

A l'intérieur de l'élément `<li>`,ajoutez un élément `<button>` pour envelopper les détails du héros, puis rendre le héros cliquable. Pour améliorer l'accessibilité, utilisez des éléments HTML qui sont intrinsèquement interactifs au lieu d'ajouter un écouteur d'événements à un élément non interactif. Dans ce cas, l'élément interactif `<button>` est utilisé au lieu d'ajouter un événement à l'élément `<li>`.

Pour plus de détails sur l'accessibilité, voir [Accessibilité dans Angular](guide/accessibility).

</div>

<a id="styles"></a>

### Styliser les héros

La liste des héros doit être attrayante et doit répondre visuellement pour les utilisateurs qui veulent 
sélectionner un héros dans la liste.

Dans le [premier tutoriel](tutorial/toh-pt0#app-wide-styles), vous définissez les styles de base de l'ensemble de l'application dans `styles.css`.
Cette feuille de style n'incluait pas les styles pour cette liste de héros.

Vous pouvez ajouter plus de styles dans `styles.css` et continuez à développer cette feuille de style lorsque vous ajoutez des composants.

Vous préférez peut-être plutôt définir des styles privés pour un composant spécifique. Cela maintient tout ce dont un composant a besoin, comme le code, le HTML et le CSS, ensemble en un seul endroit.

Cette approche facilite la réutilisabilité du composant ailleurs et livrer l'apparence prévue du composant même si les styles globaux sont différents.

Vous définissez des styles privés en ligne dans le tableau `@Component.styles` ou comme fichiers de feuille de style identifiés dans le tableau `@Component.styleUrls`.

Quand `ng generate` a créé `HeroesComponent`, il a créé une feuille de style vide `heroes.component.css` pour `HeroesComponent` et l'a pointé dans `@Component.styleUrls` comme ça.

<code-example header="src/app/heroes/heroes.component.ts (@Component)" path="toh-pt2/src/app/heroes/heroes.component.ts" region="metadata"></code-example>

Ouvrez le fichier `heroes.component.css`et collez dans les styles CSS privés pour le `HeroesComponent` de l'[examen du code final](#final-code-review).

<div class="alert is-important">

Les styles et les feuilles de style identifiés dans les métadonnées `@Composant` sont étendus pour ce composant spécifique.
Le style `heroes.component.css` agit uniquement sur `HeroesComponent` et n'affectent pas le HTML extérieur ou le HTML dans tout autre composant.

</div>

## Affichage des détails

Lorsque l'utilisateur clique sur un héros dans la liste, le composant doit afficher les détails du héros sélectionné en bas de la page.

Le code de cette section écoute l'événement de l'élément de héros et affiche/met à jour les détails du héros.

### Ajouter une liaison d'événement de clics

Ajoutez une liaison d'événement de clic au `<button>` dans le `<li>` comme ça:

<code-example header="heroes.component.html (template excerpt)" path="toh-pt2/src/app/heroes/heroes.component.1.html" region="selectedHero-click"></code-example>

Ceci est un exemple de la syntaxe pour les [liaisons d'evenements](guide/event-binding) avec Angular.

Les parenthèses autour de `click` dit à Angular d'écouter les évenements `click`  provenant du `<button>`
Quand l'utilisateur clique sur le `<button>`, Angular exécute l'expression `onSelect(hero)`.

Dans la section suivante, vous définirez une méthode `onSelect()` dans `HeroesComponent` pour afficher le héros qui a été défini dans l'expression `*ngFor`.

### Ajouter le gestionnaire d'événements de clics

Renommez la propriété `hero` par `selectedHero` mais ne lui attribuez aucune valeur car il n'y a pas de *héros sélectionné* au début de l'application.

Ajoutez la méthode suivante `onSelect()`, qui attribue le héros cliqué dans le template du composant via `selectedHero`.

<code-example header="src/app/heroes/heroes.component.ts (onSelect)" path="toh-pt2/src/app/heroes/heroes.component.ts" region="on-select"></code-example>

### Ajouter une section de détails

Actuellement, vous avez une liste dans le template du composant.
Pour afficher des détails sur un héros lorsque vous cliquez sur leur nom dans la liste, ajoutez une section
dans le template qui affiche leurs détails.
Ajouter ce qui suit à `heroes.component.html` sous la section liste:

<code-example header="heroes.component.html (selected hero details)" path="toh-pt2/src/app/heroes/heroes.component.html" region="selectedHero-details"></code-example>

Les détails du héros ne doivent être affichés que lorsqu'un héros est sélectionné. Lorsqu'un composant est créé initialement, il n'y a pas de héros sélectionné. Ajoutez la directive `*ngIf` dans la `<div>` qui entoure les détails du héros. Cette directive dit à Angular de rendre la section uniquement quand `selectedHero` est défini après sa sélection en cliquant sur un héros.

<div class="alert is-important">

N'oubliez pas l'astérisque `*` devant de `ngIf`.
C'est une partie essentielle de la syntaxes.

</div>

### Stylisez le héros sélectionné

Pour aider à identifier le héros sélectionné, vous pouvez utiliser la classe CSS `.selected` dans le [style que vous avez ajouté précédement](#styles).
Pour appliquer la classe `.selected` dans `<li>` quand l'utilisateur clique dessus, il faut utiliser la liaison de classe.

<div class="lightbox">

<img alt="Selected hero with dark background and light text that differentiates it from unselected list items" src="generated/images/guide/toh/heroes-list-selected.png">

</div>

[La liaison de classe](guide/class-binding) dans Angular peut ajouter et supprimer une classe CSS conditionnellement.
Ajoutez `[class.some-css-class]="some-condition"` à l'élément que vous souhaitez styliser.

Ajoutez `[class.selected]` dans le `<button>` dans le template `HeroesComponent`:

<code-example header="heroes.component.html (toggle the 'selected' CSS class)" path="toh-pt2/src/app/heroes/heroes.component.1.html" region="class-selected"></code-example>

Lorsque le héros de la ligne est le même que le `selectedHero`, Angular ajoute la classe CSS `selected`.
Lorsque les deux héros sont différents, Angular supprime la classe.

Le `<li>` final ressemble à ça:

<code-example header="heroes.component.html (list item hero)" path="toh-pt2/src/app/heroes/heroes.component.html" region="li"></code-example>

<a id="final-code-review"></a>

## Revue du code final

Voici les fichiers de code discutés sur cette page, y compris les styles du `HeroesComponent`.

<code-tabs>
    <code-pane header="src/app/mock-heroes.ts" path="toh-pt2/src/app/mock-heroes.ts"></code-pane>
    <code-pane header="src/app/heroes/heroes.component.ts" path="toh-pt2/src/app/heroes/heroes.component.ts"></code-pane>
    <code-pane header="src/app/heroes/heroes.component.html" path="toh-pt2/src/app/heroes/heroes.component.html"></code-pane>
    <code-pane header="src/app/heroes/heroes.component.css" path="toh-pt2/src/app/heroes/heroes.component.css"></code-pane>
</code-tabs>

## Sommaire

*   L'application Tour of Heroes affiche une liste de héros avec une vue détaillée.
*   L'utilisateur peut sélectionner un héros et voir les détails de ce héros.
*   Vous avez utilisé `*ngFor` pour afficher une liste.
*   Vous avez utilisé `*ngIf` pour inclure ou exclure conditionnellement un bloc de HTML.
*   Vous pouvez mettre ou enlever une classe de style CSS avec une liaison `classe`.

@reviewed 2022-05-23
