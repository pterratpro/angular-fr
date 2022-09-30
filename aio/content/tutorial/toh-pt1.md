# L'éditeur de héros

L'application a désormais un titre.
Ensuite, créez un nouveau composant pour afficher les informations du héros et placer ce composant dans le shell d'application.

<div class="alert is-helpful">

Pour l'exemple d'application que cette page décrit, voir le <live-example></live-example>.

</div>

## Créez le composant Heroes

Utilisez `ng generate` pour créer un nouveau composant nommé `heroes`.

<code-example format="shell" language="shell">

ng generate component heroes

</code-example>

`ng generate` crée un nouveau répertoire, `src/app/heroes/`, et génère les trois fichiers de `HeroesComponent` avec un fichier de test.

Le fichier classe `HeroesComponent` est comme suit:

<code-example header="app/heroes/heroes.component.ts (initial version)" path="toh-pt1/src/app/heroes/heroes.component.ts" region="v1"></code-example>

Vous importez toujours le symbole `Component` de la bibliothèque Core Angular et annotez la classe de composants avec `@Component`.

`@Component` est une fonction de decorator qui spécifie les métadonnées Angular pour le composant.

`ng generate` créé trois propriétés de métadonnées:

| Propriétés    | Détails                                            |
| :------------ | :------------------------------------------------- |
| `selector`    | Le sélecteur d'éléments CSS du composant.          |
| `templateUrl` | L'emplacement du fichier de template du composant. |
| `styleUrls`   | L'emplacement des styles CSS privés du composant.  |

<a id="selector"></a>

Le [sélécteur de l'élément CSS](https://developer.mozilla.org/docs/Web/CSS/Type_selectors), `'app-heroes'`, correspond au nom de l'élément HTML qui identifie ce composant dans le template d'un composant parent.

Le `ngOnInit()` est un [hook de cycle de vie](guide/lifecycle-hooks#oninit).
Angular appelle `ngOnInit()` peu de temps après la création d'un composant.
C'est un bon endroit pour mettre la logique d'initialisation.

Toujours `export` la classe de composants pour que vous puissiez l'`import` partout ailleurs &hellip; comme dans `AppModule`.

### Ajoutez une propriété `hero`

Ajoutez une propriété `hero` dans le `HeroesComponent` pour un héros nommé `Windstorm`.

<code-example header="heroes.component.ts (hero property)" path="toh-pt1/src/app/heroes/heroes.component.ts" region="add-hero"></code-example>

### Afficher le héros

Ouvrez le fichier de template `heroes.component.html`.
Supprimez le texte par défault qui a été créé par `ng generate` et le remplacer par une liaison de données à la nouvelle propriété `hero`.

<code-example header="heroes.component.html" path="toh-pt1/src/app/heroes/heroes.component.1.html" region="show-hero-1"></code-example>

## Afficher la vue `HeroesComponent`

Pour afficher `HeroesComponent`, vous devez l'ajouter au template du shell `AppComponent`.

Souvenez-vous que `app-heroes` est le [sélécteur d'élément](#selector) pour `HeroesComponent`.
Ajoutez un élément `<app-heroes>` Dans le fichier de template `AppComponent`, juste en dessous du titre.

<code-example header="src/app/app.component.html" path="toh-pt1/src/app/app.component.html"></code-example>

Si `ng serve` est encore entrain de fonctionner,
le navigateur doit actualiser et afficher à la fois le titre d'application et le nom du héros.

## Créez une interface `Hero`

Un vrai héros est plus qu'un nom.

Créez une interface `Hero` dans son propre fichier dans le répertoire `src/app`.
Donnez lui les propriétés `id` et `name`.

<code-example path="toh-pt1/src/app/hero.ts"  header="src/app/hero.ts"></code-example>

Retournez dans la classe `HeroesComponent` et importez l'interface `Hero`.

Refactorisez la propriété `hero` du composant pour être de type `Hero`.
Initialisez-le avec un `id` de `1` et le nom `Windstorm`.

Le fichier de classe révisé `HeroesComponent` devrait ressembler à ça:

<code-example header="src/app/heroes/heroes.component.ts" path="toh-pt1/src/app/heroes/heroes.component.ts"></code-example>

La page ne s'affiche plus correctement car vous avez changé le héros d'une string en un objet.

## Affichez l'objet hero

Mettez à jour la liaison dans le template pour annoncer le nom du héros et afficher à la fois `id` et` name` dans un affichage de détails comme ceci:

<code-example header="heroes.component.html (HeroesComponent template)" path="toh-pt1/src/app/heroes/heroes.component.1.html" region="show-hero-2"></code-example>

Le navigateur rafraîchit et affiche les informations du héros.

## Formatez avec le `UppercasePipe`

Editez la liaison `hero.name` comme suit:

<code-example header="src/app/heroes/heroes.component.html" path="toh-pt1/src/app/heroes/heroes.component.html" region="pipe"></code-example>

Le navigateur se rafraîchit et maintenant le nom du héros est affiché en majuscules.

Le mot `uppercase` dans la liaison d'interpolation après le pipe <code>&verbar;</code>, active `UppercasePipe`.

[Pipes](guide/pipes) sont un bon moyen de formater les strings, les devises, les dates et autres données d'affichage.
Angular a plusieurs pipes par défault, vous pouvez créer le votre également.

## Modifier le héros

Les utilisateurs devraient pouvoir modifier le nom du héros dans un `<input>`.

L'input texte doit à la fois _afficher_ la propriété `name` du héros et _modifier_ cette propriété.
Cela signifie que les données circulent de la classe de composants vers l'interface et de l'interface vers la classe.

Pour automatiser ce flux de données, configurez le two-way binding entre l'élément `<input>` et la propriété `hero.name`.

### Two-way binding

Refactorisez la zone détails du template `HeroesComponent` pour que cela ressemble à ceci:

<code-example header="src/app/heroes/heroes.component.html (HeroesComponent's template)" path="toh-pt1/src/app/heroes/heroes.component.1.html" region="name-input"></code-example>

`[(ngModel)]` est la syntaxe Angular pour le two-way data binding.

Ici, il lie la propriété `hero.name` à la zone de texte HTML afin que les données puissent _circuler_ dans les deux _directions_.
Les données peuvent circuler de la propriété `hero.name` à la zone de texte et de la zone de texte vers le` hero.name`.

### Le module manquant `FormsModule`

Notez que l'application a cessé de fonctionner lorsque vous avez ajouté `[(ngModel)]`.

Pour voir l'erreur, ouvrez les outils de développement du navigateur et regardez dans la console
pour un message comme

<code-example format="output" hideCopy language="shell">

Erreurs d'analyse du template:
Ne peut pas se lier à 'ngModel' car il n'est pas une propriété connue 'd'input'.

</code-example>

Bien que `ngModel` soit une directive Angular valide, elle n'est pas disponible par défaut.

Il est dans `FormsModule` et vous devez l'importer pour l'utiliser.
## `AppModule`

Angular doit savoir comment les éléments de votre application s'imbriquent et quels autres fichiers et libraries dont l'application a besoin.
Cette information est appelée _metadata_.

Certaines metadata se trouvent dans le décorateur `@Component` que vous avez ajouté à vos classes de composants.
D'autres métadonnées essentielles se trouvent les décorateurs [`@NgModule`](guide/ngmodules).

Le décorateur le plus important `@NgModule` annote la classe de niveau supérieur **AppModule**.

`ng new` a créé une classe `AppModule` dans `src/app/app.module.ts` quand il a créé le projet.
C'est l'endroit où est le `FormsModule`.

### Importez `FormsModule`

Ouvrez `app.module.ts`  et importez `FormsModule` qui provient de la librarie `@angular/forms`.

<code-example path="toh-pt1/src/app/app.module.ts" header="app.module.ts (FormsModule symbol import)"
 region="formsmodule-js-import"></code-example>

Ajoutez `FormsModule` dans le tableau `imports` dans `@NgModule`.
Le tableau `imports` contient la liste des modules externes dont l'application a besoin.

<code-example header="app.module.ts (@NgModule imports)" path="toh-pt1/src/app/app.module.ts" region="ng-imports"></code-example>

Lorsque le navigateur se rafraîchit, l'application doit à nouveau fonctionner.
Vous pouvez modifier le nom du héros et voir les modifications immédiatement dans le `<h2>` au-dessus de la zone de texte.

### Déclarez `HeroesComponent`

Chaque composant doit être déclaré exactement une fois dans le [NgModule](guide/ngmodules).

Vous n'avez pas déclaré `HeroesComponent`.
Pourquoi l'application fonctionne-t-elle?

Cela marche car `ng generate` a déclaré `HeroesComponent` dans `AppModule` quand il a créé ce composant.

Ouvrez `src/app/app.module.ts` et vous trouverez `HeroesComponent` qui a été importé en haut du fichier.

<code-example path="toh-pt1/src/app/app.module.ts" header="src/app/app.module.ts" region="heroes-import" ></code-example>

`HeroesComponent` est déclaré dans le tableau `@NgModule.declarations`.

<code-example header="src/app/app.module.ts" path="toh-pt1/src/app/app.module.ts" region="declarations"></code-example>

<div class="alert is-helpful">

`AppModule` déclare deux composants, `AppComponent` et `HeroesComponent`.

</div>

## Revue de code final

Voici les fichiers de code de cette page.

<code-tabs>
    <code-pane header="src/app/heroes/heroes.component.ts" path="toh-pt1/src/app/heroes/heroes.component.ts"></code-pane>
    <code-pane header="src/app/heroes/heroes.component.html" path="toh-pt1/src/app/heroes/heroes.component.html"></code-pane>
    <code-pane header="src/app/app.module.ts" path="toh-pt1/src/app/app.module.ts"></code-pane>
    <code-pane header="src/app/app.component.ts" path="toh-pt1/src/app/app.component.ts"></code-pane>
    <code-pane header="src/app/app.component.html" path="toh-pt1/src/app/app.component.html"></code-pane>
    <code-pane header="src/app/hero.ts" path="toh-pt1/src/app/hero.ts"></code-pane>
</code-tabs>

## Sommaire

- Vous avez utilisé `ng generate` pour créer un second `HeroesComponent`.
- Vous avez affiché `HeroesComponent` par ajout dans le shell `AppComponent`.
- Vous avez appliqué `UppercasePipe` pour formater le nom.
- Vous avez utilisé le two-way data binding avec la directive `ngModel`.
- Vous avez appris ce qu'était `AppModule`.
- Vous avez importé `FormsModule` dans `AppModule` pour qu'Angular reconnaisse et applique la directive `ngModel`.
- Vous avez appris l'importance de déclarer les composants dans le `AppModule`.

@reviewed 2022-02-28
