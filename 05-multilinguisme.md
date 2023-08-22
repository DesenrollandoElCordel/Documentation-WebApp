# 5. Le multilinguisme
L’interface par défaut de *TEI-Publisher* est traduite automatiquement à l’aide d’attributs `@data-i18n` ou du web-component `<pb-i18n>`.

Les traductions supplémentaires sont définies dans le dossier **resources/i18n/app**, sous la forme de fichiers .json (un pour chaque langue : **en.json**, **es.json** et **fr.json**). Le dossier i18n contient également un fichier **languages.json**, qui permet de sélectionner les langues de l’interface. Parmi les langues proposées par *TEI-Publisher*, nous avons sélectionné le français, l’espagnol et l’anglais.

<img src="images/05-I18n-Config.png" width="200" alt="Sélection des langues de l’interface dans languages.json"/>

Pour inclure des traductions personnalisées dans les templates, il faut ajouter au web-component `<pb-page>` l’attribut  `@locales`, avec pour valeur `resources/i18n/{{ns}}/{{lng}}.json`.

<img src="images/05-I18n-PbPage.png" width="800" alt="Lien vers les traductions personnalisées"/>

Par exemple, pour traduire le label des facettes, dans chaque fichier .json, il faut choisir une clé unique qui identifie chaque label, et lui associer une traduction

<img src="images/05-I18n-JsonEnglish.png" width="300" alt="Traduction en anglais du nom des facettes"/>

Cette clé est ensuite reprise dans le fichier **config.xqm** (variable `$config:facets` : Voir 4.2.2. Configuration de l’affichage) de la manière suivante : facets.[cle_unique]. Par exemple, pour afficher les traductions du label de la facette “Collection”, il faut utiliser `facets.collection`.
La clé “more” est utilisée avec le web-component `<pb-i18n>` dans le fichier facets.xql (`fonction facets:display`, Figure 51).

<img src="images/05-I18n-More.png" width="800" alt="Exemple de traduction d’une portion de texte"/>
