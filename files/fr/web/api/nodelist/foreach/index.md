---
title: NodeList.prototype.forEach()
slug: Web/API/NodeList/forEach
tags:
  - API
  - DOM
  - Liste
  - Méthodes
  - Noeuds
translation_of: Web/API/NodeList/forEach
---
{{APIRef("DOM")}}

La méthode **`forEach()`** de l'interface {{domxref("NodeList")}} appelle le rappel donné en paramètre une fois pour chaque paire de valeurs dans la liste, dans l'ordre d'insertion.

## Syntaxe

    nodeList.forEach(callback[, thisArg]);

### Paramètres

- `callback`

  - : Fonction à exécuter pour chaque élément, contenant éventuellement 3 arguments :

    - _`currentValue`_
      - : L'élément en cours de traitement dans la NodeList.
    - `currentIndex`
      - : L'index de l'élément en cours de traitement dans la NodeList.
    - _`listObj`_
      - : L'objet NodeList auquel `forEach()` est appliqué.

- ` thisArg`` {{Optional_inline}}  `
  - : Valeur à utiliser comme {{jsxref("this")}} lors de l'exécution du `callback` (_rappel_).

### Valeur retournée

{{jsxref('undefined')}} (_indéfini_).

## Exceptions

_Aucune_.

## Exemple

```js
var node = document.createElement("div");
var kid1 = document.createElement("p");
var kid2 = document.createTextNode("hey");
var kid3 = document.createElement("span");

node.appendChild(kid1);
node.appendChild(kid2);
node.appendChild(kid3);

var list = node.childNodes;

list.forEach(
  function(currentValue, currentIndex, listObj) {
    console.log(currentValue + ', ' + currentIndex + ', ' + this);
  },
  'myThisArg'
);
```

résultat :

    [object HTMLParagraphElement], 0, myThisArg
    [object Text], 1, myThisArg
    [object HTMLSpanElement], 2, myThisArg

## Polyfill

Ce {{Glossary("Polyfill","polyfill")}} ajoute une compatibilité à tous les navigateurs prenant en charge [ES5](https://caniuse.com/#search=es5) :

```js
if (window.NodeList && !NodeList.prototype.forEach) {
    NodeList.prototype.forEach = function (callback, thisArg) {
        thisArg = thisArg || window;
        for (var i = 0; i < this.length; i++) {
            callback.call(thisArg, this[i], i, this);
        }
    };
}
```

## Spécifications

| Spécification                                                                    | Statut                           | Commentaire                                                      |
| -------------------------------------------------------------------------------- | -------------------------------- | ---------------------------------------------------------------- |
| {{SpecName('DOM WHATWG', '#interface-nodelist', 'NodeList')}} | {{ Spec2('DOM WHATWG') }} | Définit `NodeList` comme `iterable<Node> `(_noeud itérable_)     |
| {{SpecName("WebIDL", "#es-forEach", "forEach")}}                 | {{Spec2("WebIDL")}}         | Définit `forEach` sur les déclarations `iterable` (_itératives_) |

## Compatibilité des navigateurs

{{Compat("api.NodeList.forEach")}}

## Voir aussi

- {{domxref("Node")}}
- {{domxref("NodeList")}}