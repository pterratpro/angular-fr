# Aperçu de l'interface CLI et référence des commandes

L'interface CLI d'Angular est un outil d'interface de ligne de commande que vous utilisez pour initialiser, développer, échafauder et maintenir des applications Angular directement à partir d'un shell de commande.

## Installation d'Angular CLI

Les versions principales d'Angular CLI suivent la version principale d'Angular supportée, mais les versions mineures peuvent être publiées séparément.

Installez le CLI en utilisant le gestionnaire de paquets `npm` :

<code-example format="shell" language="shell">

npm install -g &commat;angular/cli<aio-angular-dist-tag class="pln"></aio-angular-dist-tag>

</code-example>

Pour plus de détails sur les changements entre les versions, et des informations sur la mise à jour à partir de versions précédentes, voir l'onglet Releases sur GitHub : https://github.com/angular/angular-cli/releases

## Basic workflow

Appelez l'outil sur la ligne de commande via l'exécutable `ng`.
Une aide en ligne est disponible sur la ligne de commande.
Entrez la commande suivante pour lister les commandes ou les options d'une commande donnée (telle que [generate](cli/generate)\) avec une courte description.

<code-example format="shell" language="shell">

ng help
ng generate --help

</code-example>

Pour créer, construire et servir un nouveau projet Angular basique sur un serveur de développement, allez dans le répertoire parent de votre nouvel espace de travail et utilisez les commandes suivantes :

<code-example format="shell" language="shell">

ng new my-first-project
cd my-first-project
ng serve

</code-example>

Dans votre navigateur, ouvrez http://localhost:4200/ pour voir l'exécution de la nouvelle application.
Lorsque vous utilisez la commande [ng serve](cli/serve) pour construire une application localement, le serveur reconstruit automatiquement l'application et recharge la page lorsque vous modifiez l'un des fichiers source.

<div class="alert is-helpful">

Lorsque vous exécutez la commande `ng new my-first-project`, un nouveau dossier, nommé `my-first-project`, sera créé dans le répertoire de travail actuel.
Comme vous voulez pouvoir créer des fichiers dans ce dossier, assurez-vous d'avoir les droits suffisants dans le répertoire de travail actuel avant d'exécuter la commande.

Si le répertoire de travail actuel n'est pas le bon endroit pour votre projet, vous pouvez changer pour un répertoire plus approprié en exécutant `cd <path-to-other-directory>`.

</div>

## Workspaces and project files

La commande [ng new](cli/new) crée un dossier *Angular workspace* et génère un nouveau modèle d'application.
Un espace de travail peut contenir plusieurs applications et bibliothèques.
L'application initiale créée par la commande [ng new](cli/new) se trouve au niveau supérieur de l'espace de travail.
Lorsque vous générez une application ou une bibliothèque supplémentaire dans un espace de travail, elle est placée dans un sous-dossier `projects/`.

Une application nouvellement générée contient les fichiers sources d'un module racine, avec un composant racine et un modèle.
Chaque application possède un dossier `src` qui contient la logique, les données et les actifs.

Vous pouvez éditer les fichiers générés directement, ou les compléter et les modifier à l'aide des commandes CLI.
Utilisez la commande [ng generate](cli/generate) pour ajouter de nouveaux fichiers pour des composants et services supplémentaires, et du code pour des nouveaux pipes, directives, etc.
Les commandes telles que [add](cli/add) et [generate](cli/generate), qui créent ou opèrent sur des applications et des bibliothèques, doivent être exécutées depuis un espace de travail ou un dossier de projet.

* Pour en savoir plus sur La structure des fichiers de l'espace de travail [Workspace file structure](guide/file-structure).

### Configuration de l'espace de travail et du projet

Un seul fichier de configuration de l'espace de travail, `angular.json`, est créé au niveau supérieur de l'espace de travail.
C'est là que vous pouvez définir des valeurs par défaut par projet pour les options de commande CLI, et spécifier les configurations à utiliser lorsque le CLI construit un projet dans différents buts.

La commande [ng config](cli/config) vous permet de définir et de récupérer les valeurs de configuration à partir de la ligne de commande, ou vous pouvez modifier directement le fichier `angular.json`.

<div class="alert is-helpful">

**NOTE**: <br />
Les noms d'options dans le fichier de configuration doivent utiliser [camelCase](guide/glossary#case-types), alors que les noms d'options fournis aux commandes doivent utiliser des tirets.

</div>

*   Pour en savoir plus sur la configuration de l'espace de travail [Workspace Configuration](guide/workspace-config).

## Syntaxe du langage de commande CLI

La syntaxe des commandes est présentée comme suit :

`ng` *<command-name>* *<required-arg>* [*optional-arg*] `[options]`

*   La plupart des commandes, et certaines options, ont des alias.
    Les alias sont indiqués dans la déclaration syntaxique de chaque commande.

*   Les noms d'options sont préfixés par un double tiret \(`--`\).
    Les alias d'options sont préfixés par un simple tiret \(`-``).
    Les arguments ne sont pas préfixés.
    Par exemple :

    <code-example format="shell" language="shell">

    ng build my-app -c production

    </code-example>

*   Typiquement, le nom d'un artefact généré peut être donné comme argument à la commande ou spécifié avec l'option `--name`.

*   Les noms des arguments et des options doivent être donnés en [dash-case] (guide/glossary#case-types).
    Par exemple :`--my-option-name`

### Boolean options

Les options booléennes ont deux formes : `--this-option` met l'indicateur à `true`, `--no-this-option` le met à `false`.
Si aucune option n'est fournie, l'indicateur reste dans son état par défaut, comme indiqué dans la documentation de référence.

### Options des tableaux

Les options des tableaux peuvent être fournies sous deux formes : `--option value1 value2` ou `--option value1 --option value2`.

### Chemins relatifs

Les options qui spécifient des fichiers peuvent être données comme des chemins absolus, ou comme des chemins relatifs au répertoire de travail actuel, qui est généralement la racine de l'espace de travail ou du projet.

### Schémas

Les commandes [ng generate](cli/generate) et [ng add](cli/add) prennent, comme argument, l'artefact ou la bibliothèque à générer ou à ajouter au projet en cours.
En plus des options générales, chaque artefact ou bibliothèque définit ses propres options dans un *schéma*.
Les options schématiques sont fournies à la commande dans le même format que les options immédiates de la commande.

<!-- links -->

<!-- external links -->

<!-- end links -->

@reviewed 2022-02-28
