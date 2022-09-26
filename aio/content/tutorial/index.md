# Tutoriel pour l'application : Tour des héros

<div class="callout is-helpful">

<header>Pour commencer</header>

Dans ce tutoriel, vous allez construire votre propre application à partir de zéro.
C'est un bon moyen de découvrir un processus de développement typique en apprenant les concepts, les outils et la terminologie de conception d'applications Angular.

Si vous êtes complètement débutant avec Angular, vous devrez dans un premier temps essayer le [**Try it now**](start) guide de démarrage rapide.
**Try it now** est basé sur un projet prêt à l'emploi partiellement achevé.
Vous pouvez modifier l'application dans StackBlitz et voir les résultats en temps réel.

**Try it now** couvre les mêmes sujets principaux &mdash;composants, syntaxe de modèle, routage, services et accès aux données via HTTP&mdash; dans un format condensé, conformément aux meilleures pratiques.

</div>

Ce tutoriel *Tour of Heroes* fournit une introduction aux principes fondamentaux d'Angular et vous montre comment :

* Mettre en place votre environnement de développement Angular.
* Utiliser la [Angular CLI](cli "CLI command reference") pour développer une application.

L'application *Tour of Heroes* que vous créez aide une agence de recrutement à gérer sa ligue de héros.
L'application possède de nombreuses fonctionnalités que vous vous attendez à trouver dans n'importe quelle application basée sur les données.

L'application finie:

* Avoir une liste de héros
* Afficher les héros dans une liste
* Editer les détails d'un héros séléctionné
* Navigue entre différentes vues de données des héros


À la fin de ce tutoriel, vous serez en mesure de faire ce qui suit :

*   Utiliser les [directives](guide/glossary#directive "Directives definition") présentes dans Angular pour afficher et masquer des éléments, et afficher les listes des héros.
*   Créer des [composants](guide/glossary#component "Components definition") Angular pour afficher les détails de chaque héros et afficher un tableau de héros.
*   Utiliser le one-way [data binding](guide/glossary#data-binding "Data binding definition") pour les données en lecture seule.
*   Ajouter des champs modifiables pour mettre à jour un modèle avec le two-way data binding.
*   Lier les méthodes des composants aux événements de l'utilisateur, comme les touches et les clics.
*   Permettre aux utilisateurs de sélectionner un héros depuis la liste principale et éditer ce héros dans une vue détaillée.
*   Formater les données avec des [pipes](guide/glossary#pipe "Pipe definition").
*   Créer un [service](guide/glossary#service "Service definition") partagé pour centraliser les héros.
*   Utiliser le [routing](guide/glossary#router "Router definition") pour naviguer entre les différentes vues et leurs composants.


<div class="callout is-helpful">

<header>Solution</header>

Après avoir terminé toutes les étapes du tutoriel, l'application finale ressemblera à ceci:

<live-example name="toh-pt6"></live-example>.

</div>

## Concevez votre nouvelle application

Voici une image de l'application de ce tutoriel, montrant la vue Tableau de bord et les héros les plus héroïques :

<div class="lightbox">

<img alt="Output of heroes dashboard" src="generated/images/guide/toh/heroes-dashboard-1.png">

</div>

Vous pouvez cliquer sur les liens **Tableau de bord** et **Héros** dans le tableau de bord pour naviguer entre les vues.

Si vous cliquez sur le héros "Magneta" présent dans le tableau de bord, le routeur ouvre une vue "Détails du héros" dans laquelle vous pouvez modifier le nom du héros.

<div class="lightbox">

<img alt="Details of hero in application" src="generated/images/guide/toh/hero-details-1.png">

</div>

Cliquer sur le bouton "Retour" vous ramène au tableau de bord.
Les liens en haut vous amènent à l'une des vues principales.
Si vous cliquez sur "Héros", l'application affiche la vue de liste "Héros".

<div class="lightbox">

<img alt="Output of heroes list application" src="generated/images/guide/toh/heroes-list-2.png">

</div>

Lorsque vous cliquez sur un nom de héros différent, le mini-détail sous la liste reflète le nouveau choix.

Vous pouvez cliquer sur le bouton "Afficher les détails" pour accéder aux détails modifiables du héros sélectionné.

Le diagramme suivant illustre les options de navigation.
<div class="lightbox">

<img alt="View navigations" src="generated/images/guide/toh/nav-diagram.png">

</div>

Ici l'application en action:

<div class="lightbox">

<img alt="Tour of Heroes in Action" src="generated/images/guide/toh/toh-anim.gif">

</div>

@reviewed 2022-05-16
