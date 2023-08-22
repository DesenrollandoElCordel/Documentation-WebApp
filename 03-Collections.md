# 3. Les collections

## 3.1. Étape 1 : La création des collections
Dans le dossier **data**, nous avons créé deux dossiers, correspondant aux collections que nous souhaitons afficher sur le site web : **Pliegos** et **Illustraciones**.

## 3.2. Étape 2 : La liste des collections (description_collection.html)
Pour afficher la liste des collections sur le site Web, nous n’avons pas suivi la [méthode](https://teipublisher.com/exist/apps/tei-publisher/doc/documentation.xml?odd=docbook&id=introduction&view=div#subcollections) par défaut proposée par *TEI-Publisher*. Nous avons créé notre propre template (**description_collection.html**), dans lequel les collections sont organisées sous la forme d’une table HTML.

En ce qui concerne les URL des collections *Moreno* et *Pliegos Varios*, contenus dans le dossier *Pliegos*, nous avons artificiellement créé des sous-collections afin de permettre à l’utilisateur de voir soit tous les documents, soit ceux imprimés par José María Moreno, soit le reste de la collection regroupée sous le nom de *pliegos varios*. Pour cela, nous attribuons à l’élément `<a>` un attribut `@href`, dont la valeur est l’URL de la collection *Pliegos* à laquelle est ajoutée une facette correspondant aux *pliegos Moreno* ou aux *pliegos Varios* :

```
index.html?collection=Pliegos&amp;facet-collection=Colleción+Moreno.
```

