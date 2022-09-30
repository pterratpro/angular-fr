# Créer un nouveau projet

Utilisez la commande `ng new` pour commencer à créer votre application **Tour of Heroes**.

Ce tutoriel:

1. Configure votre environnement.
2. Crée un nouvel espace de travail et l'application initiale.
3. Lancer l'application.
4. Apporter des modifications à la nouvelle application.

<div class="alert is-helpful">

Pour afficher le code de l'application, voir le <live-example></live-example>.

</div>

## Configurez votre environnement

Pour configurer votre environnement de développement, suivez les instructions dans [Configuration d'un environnement local](guide/setup-local "Setting up for Local Development").

## Créer un nouvel espace de travail et une application initiale

Vous développez des applications dans le contexte Angular [espace de travail](guide/glossary#workspace).
Un _espace de travail_ contient les fichiers pour un ou plusieurs [projets](guide/glossary#project).
Un _projet_ est l'ensemble de fichiers qui composent une application ou une bibliothèque.

Pour créer un nouvel espace de travail et un projet initial:

1.  Assurez-vous que vous n'êtes pas déjà dans un répertoire d'espace de travail Angular.
    Par exemple, si vous êtes dans l'espace de travail de démarrage à partir d'un exercice antérieur, accédez à son parent.

2.  Exécutez `ng new` suivi du nom de l'application comme indiqué ici:

    <code-example format="shell" language="shell">

    ng new angular-tour-of-heroes

    </code-example>

3.  `ng new` Vous invite à des informations sur les fonctionnalités à inclure dans le projet initial.
    Acceptez les valeurs par défaut en appuyant sur la touche Entrée ou Retour.

`ng new` installe les packages `npm` et les autres dépendances dont Angular a besoin.
Cela peut prendre quelques minutes.

`ng new` Crée également l'espace de travail suivant et les fichiers de projet de démarrage:

*   Un nouvel espace de travail, avec un répertoire racine nommé `angular-tour-of-heroes`
*   Un projet d'application squelette initial dans le sous-répertoire `src/app`
*   Fichiers de configuration connexes

Le projet d'application initial contient une application simple prête à s'exécuter.

## Lancer l'application

Accédez au répertoire de l'espace de travail et lancez l'application.

<code-example format="shell" language="shell">

cd angular-tour-of-heroes
ng serve --open

</code-example>

<div class="alert is-helpful">

La commande `ng serve`:

* Construit l'application
* Démarre le serveur de développement
* Regarde les fichiers source
* Reconstruit l'application lorsque vous apportez des modifications

Le flag `--open` ouvre un navigateur à `http://localhost:4200`.

</div>

Vous devriez voir l'application s'exécuter dans votre navigateur.

## Composants Angular

La page que vous voyez est la *shell d'application*.
Le shell est contrôlé par un **composant** Angular nommé `AppComponent`.

Les *Composants* sont les éléments constitutifs fondamentaux des applications Angular.
Ils affichent des données à l'écran, écoutent l'entrée de l'utilisateur et prennent des mesures en fonction de cette entrée.

## Apporter des modifications à l'application

Ouvrez le projet dans votre éditeur ou IDE préféré. Accédez au dossier `src/app` pour modifier l'application de démarrage.
Dans l'IDE, localisez ces fichiers, qui constituent le `AppComponent` que vous venez de créer:

| Fichiers                | Details |
|:---                  |:---     |
| `app.component.ts`   | Le code de classe des composants, écrit en TypeScript. |
| `app.component.html` | Le template du composant, écrit en html.         |
| `app.component.css`  | Les styles CSS privés du composant.              |

<div class="alert is-important">

Lorsque vous exécutez `ng new`, Angular a créé des spécifications de test pour votre nouvelle application.
Cependant, apporter ces modifications casse vos spécifications nouvellement créées.

Ce ne sera pas un problème car les tests Angular sont en dehors de la portée de ce tutoriel et ne seront pas utilisés.

Pour en savoir plus sur les tests avec Angular, voir [Testing](guide/testing).

</div>

### Modifier le titre de l'application

Ouvrez le fichier `app.component.ts` et changez la valeur de la propriété `title` en 'Tour of Heroes'.

<code-example header="app.component.ts (class title property)" path="toh-pt0/src/app/app.component.ts" region="set-title"></code-example>

Ouvrez le fichier `app.component.html` et supprimez le template par défaut créé par `ng new`.
Remplacez-le par la ligne suivante.

<code-example header="app.component.html (template)" path="toh-pt0/src/app/app.component.html"></code-example>

Les doubles accolades permettent *l'interpolation* avec Angular.
Cette liaison d'interpolation présente la valeur de propriété `Title` du composant dans la balise d'en-tête HTML.

Le navigateur actualise et affiche le nouveau titre d'application.

<a id="app-wide-styles"></a>

### Ajouter des fichiers de styles dans application

La plupart des applications visent un look cohérent à travers l'application.
`ng new` a créé un fichier `styles.css` dans ce but.
Mettez vos styles à l'échelle de l'application.

Ouvrez `src/styles.css` et ajoutez le code ci-dessous dedans.

<code-example header="src/styles.css (excerpt)" path="toh-pt0/src/styles.1.css"></code-example>

## Revue du code final

Voici les fichiers de code discutés sur cette page.

<code-tabs>
    <code-pane header="src/app/app.component.ts" path="toh-pt0/src/app/app.component.ts"></code-pane>
    <code-pane header="src/app/app.component.html" path="toh-pt0/src/app/app.component.html"></code-pane>
    <code-pane header="src/styles.css (excerpt)" path="toh-pt0/src/styles.1.css"></code-pane>
</code-tabs>

## Sommaire

*   Vous avez créé la structure d'application initiale en utilisant `ng new`.
*   Vous avez appris que les composants Angular affichent des données
*   Vous avez utilisé les doubles accolades d'interpolation pour afficher le titre de l'application

@reviewed 2022-02-28
