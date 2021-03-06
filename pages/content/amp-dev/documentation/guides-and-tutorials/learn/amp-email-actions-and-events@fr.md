---
'$title': Actions et événements dans les e-mails AMP
$order: 0
formats:
  - email
teaser:
  text: '[tip type="note"]'
---

<!--
This file is imported from https://github.com/ampproject/amphtml/blob/main/docs/spec/amp-email-actions-and-events.md.
Please do not change this file.
If you have found a bug or an issue please
have a look and request a pull request there.
-->

<!---
Copyright 2020 The AMP HTML Authors. All Rights Reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS-IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->

[tip type="note"] Cette documentation couvre les actions et événements pour le format d'e-mail AMP. Lisez la section [Actions et événements](https://github.com/ampproject/amphtml/blob/main/docs/spec/amp-actions-and-events.md) pour les sites Web, les stories et les annonces AMP. [/tip]

L'attribut `on` est utilisé pour installer des gestionnaires d'événements sur les éléments. Les événements pris en charge dépendent de l'élément.

La valeur de la syntaxe est un langage simple spécifique au domaine du formulaire:

[sourcecode:javascript]
eventName:targetId[.methodName[(arg1=value, arg2=value)]][/sourcecode]

Consultez le tableau ci-dessous pour une description de chaque partie de la syntaxe.

<table>
  <tr>
    <th width="30%">Syntaxe</th>
    <th width="18%">Requis?</th>
    <th width="42%">Description</th>
  </tr>
  <tr>
    <td><code>eventName</code></td>
    <td>oui</td>
    <td>C'est le nom de l'événement qu'un élément expose.</td>
  </tr>
  <tr>
    <td><code>targetId</code></td>
    <td>oui</td>
    <td>C'est l'identifiant du DOM de l'élément ou une <a href="#special-targets">cible spéciale</a> prédéfinie sur laquelle vous souhaitez exécuter une action en réponse à l'événement. Dans l'exemple suivant, <code>targetId</code> représente l'identifiant du DOM de la cible <code>amp-lightbox</code>, <code>photo-slides</code>.     <pre>&lt;amp-lightbox id="photo-slides">&lt;/amp-lightbox>
&lt;button on="tap:photo-slides">Show Images&lt;/button></pre>
</td>
  </tr>
  <tr>
    <td><code>methodName</code></td>
    <td>non</td>
    <td>Pour les éléments qui ont des actions par défaut. <p>C'est la méthode que l'élément cible (référencé par <code>targetId</code>) expose et que vous souhaitez exécuter lorsque l'événement est déclenché.</p>
<p>AMP possède un concept d'action par défaut que les éléments peuvent implémenter. Ainsi, en omettant le <code>methodName</code>, AMP exécutera cette méthode par défaut.</p>
</td>
  </tr>
  <tr>
    <td><code>arg=value</code></td>
    <td>non</td>
    <td>Certaines actions, si elles sont documentées, peuvent accepter des arguments. Les arguments sont définis entre parenthèses dans la notation <code>key=value</code> . Les valeurs acceptées sont: <ul>
<li> chaînes simples sans guillemets: <code>simple-value</code> </li>
<li> chaînes entre guillemets: <code>"string value"</code> ou <code>'string value'</code> </li>
<li> valeurs booléennes: <code>true</code> ou <code>false</code> </li>
<li> nombres: <code>11</code> ou <code>1.1</code> </li>
<li> référence de syntaxe de point aux données d'événement: <code>event.someDataVariableName</code> </li>
</ul>
</td>
  </tr>
</table>

## Gérer plusieurs événements <a name="handling-multiple-events"></a>

Vous pouvez écouter plusieurs événements sur un élément en séparant les événements par un point-virgule `;`.

Exemple: `on="submit-success:lightbox1;submit-error:lightbox2"`

## Plusieurs actions pour un événement <a name="multiple-actions-for-one-event"></a>

Vous pouvez exécuter plusieurs actions en séquence pour le même événement en séparant les actions par une virgule « , ».

Exemple: `on="tap:target1.actionA,target2.actionB"`

## Événements et actions définis de manière globale <a name="globally-defined-events-and-actions"></a>

AMP définit globalement un événement `tap` que vous pouvez écouter sur n'importe quel élément HTML (y compris les éléments AMP).

AMP définit également globalement les actions `hide` , `show` et `toggleVisibility` que vous pouvez déclencher sur n'importe quel élément HTML.

[tip type="note"]

Un élément ne peut être affiché que s'il était d'abord masqué par une action `hide` ou `toggleVisibility`, ou à l'aide de l'attribut [`hidden`](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/hidden). L'action `show` ne prend pas en charge les éléments masqués par l'attribut `display:none` de CSS ou l'attribut `layout=nodisplay` d'AMP.

L'exemple suivant est possible dans AMP:

[sourcecode:html]

<div id="warning-message">Warning...</div>

<button on="tap:warning-message.hide">Cool, thanks!</button>
[/sourcecode]

[/tip]

## Événements spécifiques aux éléments <a name="element-specific-events"></a>

### \* - tous les éléments <a name="---all-elements"></a>

<table>
  <tr>
    <th>Événement</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>tap</code></td>
    <td>Se déclenche lorsque vous cliquez ou appuyez sur l'élément.</td>
  </tr>
</table>

### Éléments d'entrée <a name="input-elements"></a>

<table>
  <tr>
    <th width="20%">Événement</th>
    <th width="30%">Description</th>
    <th width="40%">Éléments</th>
    <th>Données</th>
  </tr>
  <tr>
    <td rowspan="3"><code>change</code></td>
    <td rowspan="3">Se déclenche lorsque la valeur de l'élément est modifié et envoyée. <p> Les propriétés des données les reflètent dans <a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement#Properties">HTMLInputElement</a> et <a href="https://developer.mozilla.org/en-US/docs/Web/API/HTMLSelectElement#Properties">HTMLSelectElement</a>.</p>
</td>
    <td><code>input</code></td>
    <td>
      <pre>event.min<br>event.max<br>event.value<br>event.valueAsNumber</pre>
    </td>
  </tr>
  <tr>
    <td> <code>input[type="radio"]</code>,<br><code>input[type="checkbox"]</code>
</td>
    <td>
      <code>event.checked</code>
    </td>
  </tr>
  <tr>
    <td><code>select</code></td>
    <td>
      <pre>event.min<br>event.max<br>event.value</pre>
    </td>
  </tr>
  <tr>
    <td><code>input-debounced</code></td>
    <td>Se déclenche lorsque la valeur de l'élément est modifiée. Il est similaire à l'événement <code>change</code> standard, mais il ne se déclenche que lorsque 300ms se sont écoulés après la fin de la modification de la valeur de l'entrée.</td>
    <td>Éléments qui déclenchent l'événement <code>input</code>.</td>
    <td>Identiques aux données  de l'événement <code>change</code>.</td>
  </tr>
  <tr>
    <td><code>input-throttled</code></td>
    <td>Se déclenche lorsque la valeur de l'élément est modifiée. Il est similaire à l'événement <code>change</code> standard, mais il est limité à se déclencher au plus une fois toutes les 100ms pendant la modification de la valeur de l'entrée.</td>
    <td>Éléments qui déclenchent l'événement <code>input</code>.</td>
    <td>	Identiques aux données de l'événement <code>change</code>.</td>
  </tr>
</table>

### amp-accordion > section <a name="amp-accordion"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td><code>expand</code></td>
    <td>Se déclenche lorsqu'une section d'accordéon se développe.</td>
    <td>Aucune.</td>
  </tr>
  <tr>
    <td><code>collapse</code></td>
    <td>Se déclenche lorsqu'une section d'accordéon se réduit.</td>
    <td>Aucune.</td>
  </tr>
</table>

### amp-carousel[type="slides"] <a name="amp-carouseltypeslides-1"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td><code>slideChange</code></td>
    <td>Se déclenche lorsque la diapositive actuelle du carrousel change.</td>
    <td><pre>// Slide number.<br>event.index</pre></td>
  </tr>
</table>

### amp-lightbox <a name="amp-lightbox-1"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td><code>lightboxOpen</code></td>
    <td>Se déclenche lorsque la lightbox est entièrement visible.</td>
    <td>Aucune</td>
  </tr>
  <tr>
    <td><code>lightboxClose</code></td>
    <td>Se déclenche lorsque la lightbox est complètement fermée.</td>
    <td>Aucune</td>
  </tr>
</table>

### amp-list <a name="amp-list-1"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td>	<code>fetch-error</code> (confiance basse)</td>
    <td>Se déclenche lorsque la récupération des données échoue.</td>
    <td>Aucune</td>
  </tr>
</table>

### amp-selector <a name="amp-selector-1"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td><code>select</code></td>
    <td>Se déclenche lorsqu'une option est sélectionnée ou désélectionnée.</td>
    <td><pre>// Target element's "option" attribute value.<br>event.targetOption<br>// Array of "option" attribute values of all selected elements.<br>event.selectedOptions</pre></td>
  </tr>
</table>

### amp-sidebar <a name="amp-sidebar-1"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td><code>sidebarOpen</code></td>
    <td>Se déclenche lorsque la barre latérale est complètement ouverte après la fin de la transition.</td>
    <td>Aucune</td>
  </tr>
  <tr>
    <td><code>sidebarClose</code></td>
    <td>Se déclenche lorsque la barre latérale est complètement fermée après la fin de la transition.</td>
    <td>Aucune</td>
  </tr>
</table>

### amp-state <a name="amp-state"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td>	<code>fetch-error</code> (confiance basse)</td>
    <td>Se déclenche lorsque la récupération des données échoue.</td>
    <td>Aucune</td>
  </tr>
</table>

### form <a name="form"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td><code>submit</code></td>
    <td>Se déclenche lorsque le formulaire est soumis.</td>
    <td></td>
  </tr>
  <tr>
    <td><code>submit-success</code></td>
    <td>Se déclenche lorsque le formulaire affiche une réponse d'envoi réussie.</td>
    <td><pre>// Response JSON.<br>event.response</pre></td>
  </tr>
  <tr>
    <td><code>submit-error</code></td>
    <td>Se déclenche lorsque le formulaire marque une erreur d'envoi.</td>
    <td><pre>// Response JSON.<br>event.response</pre></td>
  </tr>
  <tr>
    <td><code>valid</code></td>
    <td>Se déclenche lorsque le formulaire est valide.</td>
    <td></td>
  </tr>
  <tr>
    <td><code>invalid</code></td>
    <td>Se déclenche lorsque le formulaire n'est pas valide.</td>
    <td></td>
  </tr>
</table>

## Actions spécifiques aux éléments <a name="element-specific-actions"></a>

### \* (tous les éléments) <a name="-all-elements"></a>

<table>
  <tr>
    <th width="40%">Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>hide</code></td>
    <td>Masque l'élément cible.</td>
  </tr>
  <tr>
    <td><code>show</code></td>
    <td>Affiche l'élément cible. Si un élément <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#autofocus">élément de <code>autofocus</code></a> devient visible en conséquence, il obtient la mise au point.</td>
  </tr>
  <tr>
    <td><code>toggleVisibility</code></td>
    <td>Active / désactive la visibilité de l'élément cible. Si un <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#autofocus">élément de <code>autofocus</code></a> devient visible en conséquence, il obtient la mise au point.</td>
  </tr>
  <tr>
    <td><code>toggleClass(class=STRING, force=BOOLEAN)</code></td>
    <td>Change la classe de l'élément cible. L'élément <code>force</code> est facultatif, et si défini, il garantit que la classe sera uniquement ajoutée et pas supprimée si elle est définie sur <code>true</code>, et inversement si elle est définie sur <code>false</code>.</td>
  </tr>
  <tr>
    <td><code>focus</code></td>
    <td>Rend l'élément cible gagnant le focus. Pour perdre le focus, <code>focus</code> sur un autre élément (généralement l'élément parent). Nous déconseillons fortement de perdre le focus en nous concentrant sur <code>body</code> / <code>documentElement</code> pour des raisons d'accessibilité.</td>
  </tr>
</table>

### amp-accordion <a name="amp-accordion-1"></a>

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>toggle(section=STRING)</code></td>
    <td>Change les états <code>expanded</code> et <code>collapsed</code> des sections <code>amp-accordion</code>. Lorsque l'action est appelée sans argument, elle fait basculer toutes les sections de l'accordéon. Déclenchez sur une section spécifique en fournissant l'ID de section: <code>on="tap:myAccordion.toggle(section='section-id')"</code>.</td>
</tr>
  <tr>
    <td><code>expand(section=STRING)</code></td>
    <td>Développe les sections de l'accordéon. Si une section est déjà développée, elle reste développée. Lorsque l'action est appelée sans argument, elle développe toutes les sections de l'accordéon. Déclenchez sur une section spécifique en fournissant l'ID de section: <code>on="tap:myAccordion.expand(section='section-id')"</code>.</td>
  </tr>
  <tr>
    <td><code>collapse(section=STRING)</code></td>
    <td>Réduit les sections de l'accordéon. Si une section est déjà réduite, elle reste réduite. Lorsque l'action est appelée sans argument, elle réduit toutes les sections de l'accordéon. Déclenchez une section spécifique en fournissant l'ID de section: <code>on="tap:myAccordion.collapse(section='section-id')"</code>.</td>
  </tr>
</table>

### amp-carousel[type="slides"] <a name="amp-carouseltypeslides"></a>

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>goToSlide(index=INTEGER)</code></td>
    <td>Fait avancer le carrousel jusqu'à un index de diapositive spécifié.</td>
  </tr>
</table>

### amp-image-lightbox <a name="amp-image-lightbox"></a>

<table>
  <tr>
    <th width="40%">Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>open (default)</code></td>
    <td>Ouvre la lightbox d'image avec l'image source étant celle qui a déclenché l'action.</td>
  </tr>
</table>

### amp-lightbox <a name="amp-lightbox"></a>

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>open (default)</code></td>
    <td>Ouvre la lightbox.</td>
  </tr>
  <tr>
    <td><code>close</code></td>
    <td>Ferme la lightbox.</td>
  </tr>
</table>

### amp-list <a name="amp-list"></a>

<table>
  <tr>
    <th width="25%">Événement</th>
    <th width="35%">Description</th>
    <th width="40%">Données</th>
  </tr>
  <tr>
    <td><code>changeToLayoutContainer</code></td>
    <td>Met à jour la mise en page de <code>amp-list</code> vers <code>layout="CONTAINTER"</code> pour permettre <a href="https://github.com/ampproject/amphtml/blob/main/docs/spec/../extensions/amp-list/amp-list.md#dynamic-resizing">le redimensionnement dynamique</a>.</td>
  </tr>
  <tr>
    <td>	<code>fetch-error</code> (confiance basse)</td>
    <td>Se déclenche lorsque la récupération des données échoue.</td>
    <td>Aucune</td>
  </tr>
</table>

### amp-selector <a name="amp-selector"></a>

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>clear</code></td>
    <td>Efface toutes les sélections d'un <code>amp-selector</code> défini.</td>
  </tr>
  <tr>
    <td><code>selectUp(delta=INTEGER)</code></td>
    <td>Déplace la sélection vers le haut, à la valeur de `delta`. La valeur `delta` par défaut est définie sur -1. Si aucune option n'est sélectionnée, l'état sélectionné deviendra la valeur de la dernière option.</td>
  </tr>
  <tr>
    <td><code>selectDown(delta=INTEGER)</code></td>
    <td>Déplace la sélection vers le bas, à la valeur de `delta`. La valeur `delta` par défaut est définie sur 1. Si aucune option n'est sélectionnée, l'état sélectionné deviendra la valeur de la première option.</td>
  </tr>
  <tr>
    <td><code>toggle(index=INTEGER, value=BOOLEAN)</code></td>
    <td>Change l'application de `selected`. Si l'attribut de sélection est absent, cette action l'ajoute. Si l'attribut de sélection est présent, cette action le supprime. Vous pouvez forcer la conservation d'un ajout ou d'une suppression en incluant une valeur booléenne dans l'argument `value`. Une valeur `true` forcera l'ajout de l'attribut `selected` et ne le supprimera pas s'il est déjà présent. Une valeur de `false` supprimera l'attribut, mais ne l'ajoutera pas s'il est absent.</td>
  </tr>
</table>

### amp-sidebar <a name="amp-sidebar"></a>

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>open (default)</code></td>
    <td>Ouvre la barre latérale.</td>
  </tr>
  <tr>
    <td><code>close</code></td>
    <td>Ferme la barre latérale.</td>
  </tr>
  <tr>
    <td><code>toggle</code></td>
    <td>Change l'état de la barre latérale.</td>
  </tr>
</table>

### form <a name="form-1"></a>

<table>
  <tr>
    <th>Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>clear</code></td>
    <td>Efface toutes les valeurs dans les entrées du formulaire.</td>
  </tr>
  <tr>
    <td><code>submit</code></td>
    <td>Envoie le formulaire.</td>
  </tr>
</table>

## Cibles spéciales <a name="special-targets"></a>

Les cibles suivantes sont fournies par le système AMP et ont des exigences particulières:

### Cible: AMP <a name="target-amp"></a>

La cible `AMP` est fournie par le runtime AMP et implémente des actions de niveau supérieur qui s'appliquent à l'ensemble du document.

<table>
  <tr>
    <th width="40%">Action</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>
<code>setState({foo: 'bar'})</code><sup>1</sup>
</td>
    <td>
      <p>Nécessite <a href="https://amp.dev/documentation/components/amp-bind.html#updating-state-with-ampsetstate">amp-bind</a>.</p>
      <p>Fusionne un littéral d'objet dans l'état pouvant être lié.</p>
      <p></p>
    </td>
  </tr>
</table>

<sup>1</sup> Lorsqu'elles sont utilisées avec <a href="#multiple-actions-for-one-event">plusieurs actions</a>, les actions suivantes attendront la fin de <code>setState()</code> avant l'appel. Une seule action <code>setState()</code> est autorisée par événement.
