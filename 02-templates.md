# 2. Les templates

## 2.1. La notice d’un pliego : page-pliegos.html
<img src="images/02-Page-Item.png" alt="Structure du template page-pliego.html" width="500">

*Figure 1 : Structure du template **page-pliego.html***

Ce template permet d’afficher la notice d’un document avec les métadonnées descriptives, le texte et le facsimilé. Il a été créé à partir du template **facsimile.html** proposé par défaut par *TEI-Publisher*.

La page (Figure 1) se compose (de haut en bas) d’un menu de navigation général appelé depuis le template **menu.html** ; d’une barre d’outil appelée depuis le template **toolbar.html** (excepté la génération des boutons) ; d’un espace de consultation des métadonnées et des images ; et d’un pied de page. Les métadonnées, le contenu de la table des matières, les informations sur les gravures et les options de téléchargement sont créés avec l’élément `<pb-drawer>`, qui se situe entre l’élément `<app-header>` et l’élément `<main>`.

Les métadonnées sont affichées en cliquant sur le bouton “Métadonnées”, qui fait glisser un panneau à gauche. Pour cela, nous avons repris et adapté le code utilisé pour afficher la table des matières. Ainsi, elles sont gérées par le web-component `<pb-drawer toogle="metadataToogle">` (Figure 2). Il contient un web-component `<pb-view>`, avec un attribut `@xpath` ciblant le `<teiHeader>`. Le web-component `<pb-param>` définit des paramètres (avec les attributs `@name` et `@value`), repris par l’ODD pour sélectionner les métadonnées à afficher, en utilisant le prédicat suivant lors de la création du *model sequence* : `$parameters?mode='commentary'`. Pour le choix des métadonnées, voir 1.9. Les métadonnées.

<img src="images/02-Page-item-Metadata.png" alt="Code permettant d'afficher les métadonnées" width="500">

*Figure 2 : Structure du web-component `pb-drawer` permettant d’afficher les métadonnées*

L’affichage des métadonnées concernant les gravures suit le même procédé (Figure 3), mais avec le paramètre suivant : `$parameters?mode='figures'`.

<img src="images/02-Page-item-Gravures.png" alt="Code permettant d'afficher les informations sur les gravures" width="500">

*Figure 3 : Structure du web-component `pb-drawer` permettant d’afficher la liste des gravures*

Nous avons ajouté un bouton “Télécharger”, permettant de télécharger le texte ou les images d’un document. Il est construit sur le même modèle que précédemment, avec un web-component `<pb-drawer>`. Pour l’export du texte en .pdf ou en .epub, nous utilisons les fonctions par défaut de *TEI-Publisher* avec le web-component `<pb-download>`.
En ce qui concerne le téléchargement du code source XML TEI et celui des images, nous avons développé des fonctions spécifiques qui renvoient l’utilisateur vers la plateforme Zenodo. Ces fonctions sont contenues dans le fichier **modules/custom-api.xql** (Figure 4). Le bouton “Comparer” est, quant à lui, directement affiché depuis le template **toolbar.html** (Voir 2.3. La barre d’outils).

<img src="images/02-Page-Item-fonction1.png" alt="Code permettant de télécharger des fichiers PDF" width="500">
<img src="images/02-Page-Item-fonction2.png" alt="Code permettant de télécharger des fichiers TEI" width="500"/>

*Figure 4 : Fonctions utilisées pour télécharger les PDF et les fichiers XML-TEI*

Le contenu principal de la page est défini avec l’élément `<main class="page-pliegos_ _content-body">`. La transcription est affichée avec un autre web-component `<pb-view>`, lequel est encadré par deux web-components `<pb-navigation>` permettant de changer de pages (Figure 5).

<img src="images/02-Page-Item-Transcription.png" alt="Code permettant d'afficher la transcription d'un document" width="500">

*Figure 5 : Affichage des transcriptions et des outils de navigation*

Le web-component `<pb-facsimile>` permet d’afficher les images du document via le protocole IIIF (Figure 6). L’URI de base est celle du serveur de l’Université de Genève : “https://iiif.unige.ch/iiif/2/”. À cette URI, est concaténé le nom le nom de l’image sur le serveur IIIF. Celui-ci est indiqué dans les fichiers TEI, avec l’élément `<pb/>` et son attribut `@facs`. Dans l’ODD, cet élément est transformé en web-component `<pb-facs-link>`, ce qui permet ainsi d’afficher les images dans `<pb-facsimile>` (Voir 1.3. Les changements de page `<pb/>`...).

<img src="images/02-Page-Item-Facsimile.png" alt="Code permettant d'afficher les images numérisées d'un document" width="500">

*Figure 6 : Affichage des transcriptions et des outils de navigation*

## 2.2. La notice d’une illustration (illustration.html)

*TEI-Publisher* permet de définir des templates spécifiques en fonction des collections. Dans le fichier **config.xqm**, il faut modifier la fonction `config:collection-config` (Figure 7). Si la collection s’appelle “Ilustraciones”, alors on applique le template **illustration.html**. Sinon, on applique le template par défaut défini dans le même fichier avec la fonction `config:default-template`.

[Figure 7]

La notice d’une gravure a une organisation plus simple que celle des pliegos (Figure 8).

<img src="images/02-Page-Illustration.png" alt="Structure de la page d'une gravure" width="500">

*Figure 8 : Structure de la page illustration.html*

Le fil d’ariane (ou breadcrumb) est créé à l’aide d’une fonction XQuery, qui se trouve dans le fichier **modules/custom-api.xml** et intégré dans chaque notice d’illustration avec `<div data-template="api:display-illustration"/>`.

L’identifiant et la date sont affichés avec l’élément `<app-toolbar>` (Figure 9). Le web-component `<pb-view>` cible l’élément `<fileDesc>` du `<teiHeader>`, tandis que `<pb-param>` définit des paramètres repris par l’ODD avec le prédicat `$parameters?mode='title'` (Voir 1.9. Les métadonnées, `<fileDesc>`).

<img src="images/02-Page-Illustration-Titre.png" alt="Code permettant d'afficher le titre d'une illustration" width="500">

*Figure 9 : Affichage du titre*

Sur le même modèle (Figure 10), les métadonnées descriptives sont affichées avec le web-component `<pb-param>`, qui définit des paramètres (avec les attributs `@name` et `@value`) repris par l’ODD avec le prédicat suivant : `$parameters?mode='illustration'` (Voir 1.9. Les métadonnées, <teiHeader>).

<img src="images/02-Page-Illustration-Metadata.png" alt="Code permettant d'afficher les métadonnées d'une illustration" width="500">

*Figure 10 : Affichage des métadonnées descriptives*

Enfin, l’image est affichée avec l’élément `<div data-template="api:display-illustration"/>`, qui fait appelle à la fonction `api:display-illustration`, contenue dans le fichier **modules/custom-api.xql** (Figure 11). Cette fonction récupère les coordonnées d’une gravure sur l’image de la page et les concatène avec l’URI de base du serveur IIIF de l’Université de Genève. Elle affiche ensuite cette URL dans un élément HTML `<img/>`.

<img src="images/02-Page-Illustration-Img.png" alt="Code permettant d'afficher une illustration sur la page illustration.html" width="500"/>

*Figure 11 : Fonction api:display-illustration*
