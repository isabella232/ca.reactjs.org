---
id: tutorial
title: "Tutorial: Introducció a React"
layout: tutorial
sectionid: tutorial
permalink: tutorial/tutorial.html
redirect_from:
  - "docs/tutorial.html"
  - "docs/why-react.html"
  - "docs/tutorial-ja-JP.html"
  - "docs/tutorial-ko-KR.html"
  - "docs/tutorial-zh-CN.html"
---

Aquest tutorial no assumeix cap coneixement previ sobre React.

## Abans de començar el tutorial {#before-we-start-the-tutorial}

Anem a construir un petit joc durant aquest tutorial. **Hauràs estar temptat a obviar-perquè tu no estàs construint jocs en el dia a dia, però dóna-li una oportunitat.** Les tècniques que aprendràs en el tutorial són fonamentals per a construir qualsevol aplicació de React, i dominar-et donarà una entesa profunda de React.

>Tip
>
>Aquest tutorial està dissenyat per a persones que prefereixen **aprendre fent**. Si tu prefereixes aprendre els conceptes des del principi, revisa la nostra [guia pas a pas](/docs/hello-world.html). Podries trobar aquest tutorial i la guia, complementàries entre si.

Aquest tutorial està dividit en diverses seccions:

* [Configuració per a l'tutorial](#setup-for-the-tutorial) et donarà un punt de partida per seguir el tutorial.
* [Visió general](#overview) t'ensenyarà **els fonaments** de React: components, props i estat.
* [Completant el joc](#completing-the-game) t'ensenyarà **les tècniques més comuns** en desenvolupament de React.
* [Afegint viatge en el temps](#adding-time-travel) et donarà una **visió més profunda** de les fortaleses úniques de React.

No has de completar totes les seccions alhora per obtenir el valor d'aquest tutorial. Prova arribar tan lluny com puguis, fins i tot si és una o dues seccions.

### Què estem construint? {#what-are-we-building}

En aquest tutorial, et mostrarem com construir un joc de tic-tac-toe interactiu amb React.

Pots veure el que construirem aquí: **[Resultat Final](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**. Si el codi no et fa sentit, o si no estàs familiaritzat amb la sintaxi de codi, no et preocupis! L'objectiu d'aquest tutorial és ajudar-te a entendre React i la seva sintaxi.

Recomanem que revisis el joc de tic-tac-toe abans de continuar amb el tutorial. Una de les característiques que notaràs és que hi ha una llista enumerada a la dreta del tauler del jugador. Aquesta llista dóna una història de tots els moviments que han ocorregut en el joc, i es va actualitzant conforme el joc progressa.

Pots tancar el joc de tic-tac-toe una vegada que et familiarizaste amb ell. Començarem des d'una plantilla més simple en aquest tutorial. El nostre següent pas és configurar de tal manera que puguis començar a construir el joc.

### Prerequisits {#prerequisites}

Assumim que tens certa familiaritat amb HTML i javaScript, però hauries de ser capaç de seguir endavant fins i tot si véns d'un llenguatge de programació diferent. També suposem que estàs familiaritzat amb conceptes de programació com a funcions, objectes, arrays, i en menor mesura, classes.

Si necessites revisar javaScript, et recomanem llegir [aquesta guia](https://developer.mozilla.org/ca/docs/Web/JavaScript/A_re-introduction_to_javaScript). Tingues en compte que també fem servir algunes característiques de ES6, una versió recent de javaScript. En aquest tutorial, estem fent servir [funcions fletxa](https://developer.mozilla.org/ca/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [classes](https://developer.mozilla.org/ca/docs/Web/JavaScript/Reference/Classes), sentències [`let`](https://developer.mozilla.org/ca/docs/Web/JavaScript/Reference/Statements/let) i [`const`](https://developer.mozilla.org/ca/docs/Web/JavaScript/Reference/Statements/const). Pots fer servir el [Babel REPL](babel://ES5-syntax-example) per revisar a quin codi compila ES6.

## Configuració per a l'tutorial {#setup-for-the-tutorial}

Hi ha dues maneres de completar aquest tutorial: pots escriure el codi al teu navegador, o pots configurar el teu entorn de desenvolupament local en el teu ordinador.

### Opció de configuració 1: Escriu codi al navegador {#setup-option-1-write-code-in-the-browser}

Aquesta és la forma més ràpida de començar!

Primer, obre aquest **[codi inicial](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)** en una nova pestanya. La nova pestanya haurà de mostrar un tauler buit del joc de tic-tac-toe i codi de React. Estarem editant el codi d'React en aquest tutorial.

Ara pots saltar a la segona opció de configuració o anar a la secció de [visió general](#overview) per obtenir una idea general de React.

### Opció de configuració 2: Entorn de desenvolupament local {#setup-option-2-local-development-environment}

Aquesta és completament opcional i no és requerida per aquest tutorial!

<br>

<setails>

<summary><b>Opcional: Instruccions per seguir endavant localment utilitzant el teu editor de text preferit</b></summary>

Aquesta configuració requereix més feina però et permet completar el tutorial usant un editor de la teva elecció. Aquí els passos a seguir:

1. Assegura't de tenir una versió recent de [NODE.JS](https://nodejs.org/en/) instal·lada.
2. Segueix les [instruccions d'instal·lació de Create React App](/docs/create-a-new-react-app.html#create-react-app) per fer un nou projecte.

```bash
npx create-react-app mi-app
```

3. Elimina tots els arxius a la carpeta `src/` del nou projecte.

> Nota:
>
> **No eliminis la carpeta `src` per complet, només els arxius de codi font originals dins d'ella**. Reemplaçarem els arxius de codi font per defecte amb exemples per a aquest projecte en el següent pas.

```bash
cd my-app
cd src

# Si fas servir Mac o Linux:
rm -f *

# O, si fas servir Windows:
del *

# Després, torna a la carpeta del projecte
cd ..
```

4. Afegeix un fitxer anomenat `index.css` a la carpeta `src/` amb [aquest codi CSS](https://codepen.io/gaearon/pen/oWWQNa?editors=0100).

5. Afegeix un fitxer anomenat `index.js` a la carpeta `src/` amb [aquest codi JS](https://codepen.io/gaearon/pen/oWWQNa?editors=0010).

6. Afegeix aquestes 3 línies a la part superior de l'arxiu `index.js` a la carpeta `src/`:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
```

Ara, si el teu executes `npm start` a la carpeta del projecte i obres `http://localhost:3000` al navegador, hauries de veure un camp de tic-tac-toe buit.

Recomanem seguir [aquestes instruccions](https://babeljs.io/docs/editors/) per configurar el ressaltat de sintaxi per al teu editor.

</details>

### Ajuda, estic encallat! {#help-im-stuck}

Si et atoras, revisa els [recursos de suport de la comunitat](/community/support.html). En particular, [xat de Reactiflux](https://discord.gg/0ZcbPKXt5bZjGY5n) és una gran manera d'obtenir ajuda ràpidament. Si no reps una resposta, o segueixes encallat, si us plau crea 1 issue, i t'ajudarem.

## Visió general {#overview}

Ara que està el teu entorn configurat, anem a obtenir una visió general de React!

### Què és React? {#what-is-react}

React és una llibreria de javaScript declarativa, eficient i flexible per construir interfícies d'usuari. Permet compondre IUS complexes de petites i aïllades peces de codi anomenades "components".

React té pocs tipus diferents de components, però anem a començar amb la subclasse `React.Component`:

```javascript
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Llista de compres per {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Ús d'exemple: <ShoppingList name="Mark" />
```

Anem a veure les etiquetes divertides que semblen XML aviat. Fem servir components per dir-li a React el que volem que es vegi a la pantalla. Quan els nostres dades canvien, React actualitzarà eficientment i tornarà a renderitzar (re-render) els nostres components.

Aquí, ShoppingList és una **classe de component de React**, o **tipus de component de React**. Un component accepta paràmetres, anomenats `props` (abreviatura de "propietats"), i retorna una jerarquia de vistes a mostrar a través del mètode` render`.

El mètode `render` retorna una *descripció* del que vols veure a la pantalla. React pren la descripció i mostra el resultat. En particular, `render` retorna 1 **element de React**, el quin és una lleugera descripció del que cal renderitzar. La majoria de desenvolupadors de React usen una sintaxi especial anomenada "JSX" que facilita l'escriptura d'aquestes estructures. La sintaxi `<div />` és transformada en temps de construcció a `React.createElement('div')`. L'exemple anterior és equivalent a:

```javascript
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

[Veure la versió completa estesa.](babel://tutorial-expanded-version)

Si tens curiositat, `createElement()` està descrit en més detall en la [referència de l'API](/docs/react-api.html#createelement), però no ho farem servir en aquest tutorial. En canvi, seguirem fent servir JSX.

JSX ve amb tot el poder de javaScript. Pots posar *qualsevol* expressió de javaScript en l'interior de les claus dins de JSX. Cada element d'React és un objecte de javaScript que pots emmagatzemar en una variable o passar al voltant del teu programa.

El component anterior `ShoppingList` només renderitza components pre-construïts de la DOM com `<div />` i `<li />`. Però, també pots compondre i renderitzar components personalitzats de React. Per exemple, ara podem referirmos al llistat de compres complet escrivint `<ShoppingList />`. Cada compoent de React està encapsulat i pot operar independentment; això et permet construir ius omplexes des de components simples.

## Inspeccionant el codi inicial {#inspecting-the-starter-code}

Si vas a treballar el tutorial **al navegador,** obre aquest codi en un nou tab: **[Codi inicial](https://codepen.io/gaearon/pen/oWWQNa?editors=0010)**. Si vas a treballar el tutorial **localment**, obre `src/index.js` a la carpeta del teu projecte (ja has tocat aquest arxiu durant la [configuració](#setup-option-2-local-development-environment)).

Aquest codi inicial és la base del que estàs construint. Ens han proveït els estils de CSS així que només necessites enfocar-te en aprendre React i programar el joc tic-tac-toe.

Inspeccionant el codi, notaràs que tenim 3 components de React:

* Square
* Board
* Game

El component Square renderitza un simple `<button>` i el Board renderitza 9 quadrats. El component Game renderitza 1 table amb valors de posició per defecte que modificarem després. Actualment no hi ha components interactius.

### Passant dades a través de props {#passing-data-through-props}

Només per embrutar-nos les mans, anem a passar una mica de dades del nostre component Board al nostre component Square.

Recomanem fermament escriure el codi a mà mentre segueixes el tutorial sense copiar i enganxar. Això t'ajudarà a desenvolupar una memòria muscular i una entesa més sòlid.

En el mètode `renderSquare` de Board, canvia el codi per a passar una prop anomenada` value` a Square:

```js{3}
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
```

Canvia el mètode `render` de Square per mostrar aquest valor, reemplaçant `{/* TODO */}` amb `{this.props.value}`:

```js{5}
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

abans:

![React Devtools Library](../images/tutorial/tictac-empty.png)

Després: Hauries de veure un número a cada quadrat del resultat renderitzat.

![React Devtools Library](../images/tutorial/tictac-numbers.png)

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/aWWQOG?editors=0010)**

Felicitats! Acabes de "passar un prop" d'un component pare Board a un component fill Square. Passant props és com la informació flueix en apps de React, de pares a fills.

### Fent un component interactiu {#making-an-interactive-component}

Anem a omplir el component de Square amb una "X" quan donem clic en ell.
Primer, canvia l'etiqueta button que és retornada del mètode `render()` del component Square a això:

```javascript{4}
class Square extends React.Component {
  render() {
    return (
      <button className="square" onClick={function() {alert('clic'); }}>
        {this.props.value}
      </button>
    );
  }
}
```

Si fas clic en un quadrat ara, hauries veure un avís al teu navegador.

> Nota
>
> Per continuar escrivint codi sense problemes i evitar el [confús comportament de `this`](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/), farem servir la [sintaxi de funcions fletxa](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Functions/Arrow_functions) per manejar esdeveniments aquí i més avall:
>
>```javascript{4}
>class Square extends React.Component {
>  render() {
>    return (
>      <button className="square" onClick={() => alert('clic')}>
>        {this.props.value}
>      </button>
>    );
>  }
>}
>```
>
> Tingues en compte com amb `onClick={() => alert('clic')}`, estem passant *una funció* com a valor del prop `onClick`. React només cridarà a aquesta funció després d'un clic. Oblidar `() =>` i escriure `onClick={alert('clic')}` és un error comú, i executaria l'alerta cada vegada que el component es re-renderitzi.

Com un següent pas, volem que el component Square "recordi" que va ser clickeado, i es ompli amb una marca de "X". Per a "recordar" coses, els component usen **estat**.

Els components de React poden tenir estat establint `this.state` en els seus constructors. `this.state` ha de ser considerat com privat per a un component de React en què és definit. Anem a emmagatzemar el valor actual d'un quadrat en `this.state`, i canviar-lo quan el quadrat és clickeado.

Primer, anem a afegir el constructor a la classe per inicialitzar l'estat:

```javascript{2-7}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button className="square" onClick={() => alert('click')}>
        {this.props.value}
      </button>
    );
  }
}
```

> Nota
>
> A les [classes de javaScript](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Classes), necessites sempre cridar `super` quan defineixes el constructor d'una subclasse. Totes les classes de components de React que tenen un `constructor` han de començar amb una crida a` super (props) `.

Ara canviarem el mètode `render` de Square per mostrar el valor de l'estat actual quan és clickeado:

* Reemplaça `this.props.value` per` this.state.value` dins de l'etiqueta `<button>`.
* Reemplaça el gestor d'esdeveniment `onClick={...}` per `onClick={() => this.setState ({value: 'X'})}`.
* Posa els props `className` i` onClick` en línies separades per millor llegibilitat.

Després d'aquests canvis, l'etiqueta `<button>` que és retornada del mètode `render` de Square es veu així:

```javascript{12-13,15}
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

Cridant a `this.setState` des del gestor` onClick` en el mètode `render` de Square, diem a React que re-renderitzi el quadrat sempre que la seva` <button> `és clickeado. Després de l'actualització, el `this.state.value` del quadrat serà` 'X'`, així que veurem `X` al tauler de joc. Si tu fas clic en qualsevol quadrat, un `X` hauria de mostrar en el mateix.

Quan crides `setState` en un component, React actualitza automàticament els components fills dins el mateix també.

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/VbbVLg?editors=0010)**

### Eines de desenvolupament {#developer-tools}

L'extensió de React Devtools Library per [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) i [Firefox](https://addons.mozilla.org/a-uS/firefox/addon/react-devtools/) et permet inspeccionar l'arbre de components de React amb les teves eines de desenvolupament del navegador.

<img src="../images/tutorial/devtools.png" alt="React Devtools Library" style="max-width: 100%">

React DevTools et permet revisar els props i l'estat de les teves components de React.

Després d'instal·lar React DevTools, pots fer clic dret en qualsevol element de la pàgina, clic a "Inspeccionar element" per obrir les eines de desenvolupament, i la pestanya de React apareixerà com l'última pestanya a la dreta.

**No obstant això, notar que hi ha uns quants passos extres per fer-lo funcionar amb CodePen:**

1. Entra o registra't i confirma la teva correu electrònic (requerit per prevenir spam).
2. Clic en el botó "Fork".
3. Click a "Change View" i després selecciona "Debug mode".
4. En la nova pestanya que s'obre, el DevTools hauria ara tenir una pestanya de React.

## Completant el joc {#completing-the-game}

Ara tenim els blocs de construcció bàsics per al nostre joc tic-tac-toe. Per completar el joc, necessitem alternar col·locant "X" i "O" en el tauler, i necessites una manera de determinar el guanyador.

### Elevant l'estat {#lifting-state-up}

Actualment, cada component Square manté l'estat del joc. Per determinar un guanyador, necessitem mantenir el valor de cada un dels 9 quadrats en un sol lloc.

Podem pensar que el tauler hauria només preguntar a cada quadrat pel seu estat. Encara que aquest enfocament és possible en React, et incentivem a que no ho facis servir perquè el codi es torna difícil de ententer, susceptible a errors, i difícil de refactorizar. En el seu lloc, el millor enfocament és emmagatzemar l'estat del joc en el component pare Board en comptes de cada component Square. El component Board pot dir-li a cada quadrat de mostrar passant-li 1 prop [tal qual vam fer quan vam passar un número a cada quadrat](#passing-data-through-props).

**Per recopilar dades de múltiples fills, o tenir dos components fills comunicats entre si, necessites declarar l'estat compartit en el seu component pare. El component pare pot passar l'estat cap als fills usant props; això manté els components fills sincronitzats entre ells i amb el seu component pare.**

Elevar l'estat al component pare és comú quan components de React són refactorizados, anem a prendre aquesta oportunitat per intentar-ho.

Afegeix un constructor al Board i estableix l'estat inicial de Board per contenir un arranjament amb 9 valors null. Aquests 9 nulls corresponen als 9 quadrats:

```javascript{2-7}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  renderSquare(i) {
    return <Square value={i} />;
  }
```

Quan omplim el tauler després, l'arranjament `this.state.squares` es veurà alguna cosa així:

```javascript
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

El mètode `renderSquare` del component Board actualment es veu així:

```javascript
  renderSquare(i) {
    return <Square value={i} />;
  }
```

Al principi, [passem el prop `value`](#passing-data-through-props) des del Board per mostrar els números de 0 a 8 en cada quadrat. En un pas previ, reemplacem els números amb una marca "X" [determinat per l'estat del propi Square](#making-an-interactive-component). Això és perquè el quadrat actualment ignora el prop `value` passat pel Board.

Ara farem servir el prop passant el mecanisme altra vegada. Modificarem el Board per instruir cada Square sobre el seu valor actual (`'X'`,`'O'`, o `null`). Ja tenim definit l'arranjament `squares` al constructor del Board, i modificarem el mètode` renderSquare` perquè el llegeixi des d'allà:

```javascript{2}
  renderSquare(i) {
    return <Square value={this.state.squares[i]} />;
  }
```

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/gWWQPY?editors=0010)**

Cada Square ara rebrà un prop `value` que serà `'X'`, `'O'`, o `null` per quadrats buits.

Després, ens cal canviar el que passa quan un quadrat és clickeado. El component Board ara manté què quadrats estan farcits. Necessitem crear un mètode perquè el quadrat actualitza l'estat del component Board. A causa de que l'estat és considerat privat al component que el defineix, no podem actualitzar l'estat de Board directament des Square.

En canvi, passarem una funció com prop des Board a Square i farem que Square truqui a aquesta funció quan un quadrat sigui clickeado. Canviarem el mètode `renderSquare` a Board a:

```javascript{5}
  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }
```

> Nota
>
> Dividim l'element retornat en múltiples línies per llegibilitat, i afegim parèntesi perquè javaScript no inseriu un punt i coma després del `return` i trenqui el nostre codi.

Ara estem passant dues props des Board a Square: `value` i `onClick`. El prop `onClick` és una funció que Square pot trucar quan sigui clickeado. Farem els següents canvis a Square:

* Substitueix `this.state.value` per `this.props.value` en el mètode `render` de Square
* Substituir `this.setState()` per `this.props.onClick()` en el mètode `render` de Square
* Eliminar el `constructor` de Square perquè el component ja no fa seguiment de l'estat del joc

Després d'aquests canvis, el component Square es veu alguna cosa així:

```javascript{1,2,6,8}
class Square extends React.Component {
  render() {
    return (
      <button
        className="square"
        onClick={() => this.props.onClick()}
      >
        {this.props.value}
      </button>
    );
  }
}
```

Quan un quadrat és clickeado, la funció `onClick` proveïda pel component Board és cridada. Aquí un repàs de com això va ser aconseguit:

1. El prop `onClick` en el component pre-construït del DOM` <button> `li diu a React per establir un escoltador de l'esdeveniment clic.
2. Quan el botó és clickeado, React trucarà al gestor d'esdeveniment `onClick` que està definit en el mètode` render() `de Square.
3. Aquest gestor d'esdeveniment crida a `this.props.onClick()`. El prop `onClick` del component Square va ser especificat pel component Board.
4. Com que el Board va passar `onClick={() => this.handleClick (i)}` a Square, el component Square crida a `this.handleClick (i)` quan és clickeado.
5. No tenim definit el mètode `handleClick()` tot, així que el nostre codi falla. Si fas clic ara veuràs una pantalla vermella d'error que diu alguna cosa com *"this.handleClick is not a function"* (this.handleClick no és una funció).

> Nota
>
> L'atribut `onClick` de l'element `<button> `del DOM té un significat especial per React perquè és un component pre-construït. Per components personalitzats com Square, la nomenclatura la decideixes tu. Podríem donar-li qualsevol nom al prop `onClick` de Square o al mètode` handleClick` de Board, i el codi funcionaria de la mateixa forma. En React, però, és una convenció usar els noms `on[Event]` per props que representen esdeveniments i `handle[Event]` per als mètodes que manegen els esdeveniments.

Quan intentem clicar un quadrat, hauríem d'obtenir un error perquè no hem definit `handleClick` encara. Anem ara a afegir `handleClick` a la classe Board:

```javascript{9-13}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = 'X';
    this.setState({squares: squares});
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/ybbQJX?editors=0010)**

Després d'aquests canvis, podem novament clicar en els quadrats per omplir-los de la mateixa manera que ho vam fer abans. No obstant això, ara l'estat està emmagatzemat en el component Board en lloc de cada component Square. Quan l'estat del Board canvia, els components Square es re-renderitza automàticament. Mantenir l'estat de tots els quadrats en el component Board ens permetrà determinar el guanyador en el futur.

A causa de que el component Square ara no manté estat, els components Square reben valors del component Board i informen al mateix quan són clickeados. En termes de React, els components Square ara són **components controlats**. El component Board té control complet sobre ells.

Notar com a `handleClick`, anomenem `.slice() `per crear una còpia de l'array de `squares` per modificar-lo en comptes de modificar l'array existent. Ara explicareomos per què crear una còpia de l'array `squares` en la següent secció.

### Per què és important la immutabilitat? {#why-immutability-is-important}

En l'exemple de codi anterior, vam suggerir que usessis el mètode `.slice()` per crear una còpia de l'array de `squares` per modificar-lo en comptes de modificar l'array existent. Ara discutirem la immutabilitat i per què és important aprendre-la.

Hi ha generalment dos enfocaments per canviar dades. El primer enfocament és * mutar * les dades directament canviant els seus valors. El segon enfocament és reemplaçar les dades amb una nova còpia que té els canvis desitjats.

#### Canvi de dades amb mutació {#data-change-with-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Ara `player` és {score: 2, name: 'Jeff'}
```

#### Canvi de dades sense mutació {#data-change-without-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};

var newPlayer = Object.assign({}, player, {score: 2});
// Ara `player` no ha canviat, però` newPlayer` és {score: 2, name: 'Jeff'}

// O si fas servir la sintaxi proposta de propagació d'objecte, pots escriure:
// var newPlayer={... player, score: 2};
```

El resultat final és el mateix, però al no mutar (o canviar les dades subjacents) directament, obtenim molts beneficis descrits a continuació

#### Funcionalitats complexes es tornen simples {#complex-features-become-simple}

La immutabilitat fa que funcionalitats complexes siguin molt més fàcil d'implementar. Després en aquest tutorial, implementarem una funcionalitat de "viatge en el temps" que ens permet repassar l'historial del joc tic-tac-toe i "tornar" a moviments previs. Aquesta funcionalitat no és específica de jocs, una habilitat de desfer i refer certes accions és un requeriment comú en aplicacions. Evitar la mutació de dades directament ens permet mantenir intacte versions prèvies de l'historial del joc, i reusar després.

#### Detectar canvis {#detecting-changes}

Detectar canvis en objectes mutables és difícil perquè són modificats directmante. Aquesta detecció requereix que els objectes mutables siguin comparats a la còpia prèvia del mateix i que l'arbre sencer de l'objecte sigui recorregut.

Detectar canvis en objectes immutables és considerablement més senzill. Si l'objecte immutable que està sent referenciat és diferent de l'anterior, vol dir que l'objecte ha canviat.

#### Determinar quan re-renderitzar en React {#determining-when-to-re-render-in-react}

El benefici principal d'immutabilitat és que t'ajuda a construir _componentes puros_ en React. Dades immutables poden determinar fàcilment si s'han realitzat canvis, que ajuda també a determinar quan un component requereix ser re-renderitzat.

Pots aprendre més sobre `shouldComponentUpdate()` i com pots construir *components purs* llegint [Optimitzant el rendiment](/docs/Optimizing-performance.html#examples).

### Components de funció {#function-components}

Ara canviarem el component Square a ser un **component de funció**.

En React, **components de funció** són una forma més simple d'escriure components que només contenen un mètode `render` i no té estat propi. En lloc de definir una classe que estén `React.Component`, podem escriure una funció que pren` props` com a paràmetres i retorna el que s'ha de renderitzar. Components de funció són menys tediosos d'escriure que classes, i molts components poden ser expressats d'aquesta manera.

Reemplaça la classe Square per aquesta funció:

```javascript
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

Hem canviat `this.props` a` props` en les dues vegades que apareix.

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/QvvJOv?editors=0010)**

> Nota
>
> Quan modifiquem el component Square a ser un component de funció, també vam canviar `onClick={() => this.props.onClick()}` a una més curta `onClick={props.onClick}` (notar la manca de parèntesi en *amdós* costats).

### Prenent torns {#taking-turns}

Ara ens cal corregir un defecte obvi en el nostre joc tic-tac-toe: les "O" no poden ser marcades al tauler.

Establirem el primer moviment a ser una "X" per defecte. Podem establir el valor per defecte modificant l'estat inicial en el nostre constructor del component Board:

```javascript{6}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }
```

Cada vegada que el jugador faci un moviment, `xIsNext` (un booleà) seran invertits per determinar quin jugador segueix i l'estat del joc serà desat. Actualitzarem la funció `handleClick` del component Board per invertir el valor de `xIsNext`:

```javascript{3,6}
  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Amb aquest canvi, "X"s i "O"s poden prendre torns. ¡Intenta-ho!

També canviarem el text de "status" al `render` del Board perquè mostri quin jugador té el següent torn:

```javascript{2}
  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      // la resta no ha canviat
```

Després d'aplicar aquests canvis, hauríem de tenir aquest component Board:

```javascript{6,11-16,29}
class Board extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      squares: Array(9).fill(null),
      xIsNext: true,
    };
  }

  handleClick(i) {
    const squares = this.state.squares.slice();
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.state.squares[i]}
        onClick={() => this.handleClick(i)}
      />
    );
  }

  render() {
    const status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

**[Veure el codi complert en aquest punt](https://codepen.io/gaearon/pen/KmmrBy?editors=0010)**

### Declarant un guanyador {#declaring-a-winner}

Ara que vam mostrar de quin jugador és el següent torn, també hem de mostrar quan algú va guanyar el joc i si no hi ha més moviments que fer. Còpia aquesta funció de suport i enganxa-al final de l'arxiu.

```javascript
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
```

Donat un arranjament de 9 quadrats, aquesta funció comprovarà si hi ha un guanyador i retornarà `'X'`, `'O'` o `null` segons correspongui.

Anomenarem a `calculateWinner (squares)` en el mètode `render` del component Board per revisar si un jugador ha guanyat. Si un jugador ha guanyat, podem mostrar un text com: "Winner: X" o "Winner: O". Reemplaçarem la declaració de l' `status` en el mètode` render` d'Board amb aquest codi:

```javascript{2-8}
  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      // la resta del codi no ha canviat
```

Ara podem canviar la funció `handleClick` del component Board per retornar ràpidament ignorant un clic si algú ha guanyat el joc o si un quadrat està ja emplenat:

```javascript{3-5}
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }
```

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/LyyXgK?editors=0010)**

Felicitats! Ara tens un joc tic-tac-toe funcionant. I també acabes d'aprendre el bàsic de React. Així que *ets* probablement el reial guanyador aquí.

## Afegint viatge en el temps {#adding-time-travel}

Com a exercici final, farem possible "retrocedir en el temps" al moviment previ al joc.

### Emmagatzemar un historial de moviments {#storing-a-history-of-moves}

Si mutamos l'array de `squares`, implementar viatge en el temps seria molt difícil.

No obstant això, fem servir `slice()` per crear una còpia nova de l'array de `squares` després de cada moviment, i [el tractem com immutable](#why-immutability-is-important). Això ens permet emmagatzemar cada versió prèvia de l'array de `squares`, i navegar entre els torns que ja han passat.

Emmagatzemarem els passats arrays de `squares` en un altre array anomenat `history`. La matriu `history` representa tots els estats del tauler, des del primer moviment fins a l'últim, i té una forma com aquesta:

```javascript
history = [
  // Abans del primer moviment
  {
    squares: [
      null, null, null,
      null, null, null,
      null, null, null,
    ]
  },
  // Després del primer moviment
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, null,
    ]
  },
  // Després del segon moviment
  {
    squares: [
      null, null, null,
      null, 'X', null,
      null, null, 'O',
    ]
  },
  // ...
]
```

Ara ens cal decidir quin component ha de ser l'amo de l'estat `history`.

### Elevant l'estat, una altra vegada {#lifting-state-up-again}

Volem que el component de nivell superior, Game, mostri una llista dels moviments passats. Us cal accés al `historial` per fer-ho, així que col·locarem l'estat` history` en el component Game.

Col·locant l'estat `history` en el component Game et permet eliminar l'estat` squares` del seu component fill Board. Tal com [ "elevem l'estat"](#lifting-state-up) del component Square al component Board, ara elevarem del Board al component Game. Això donarà al component Game complet control sobre les dades d'Board, i permetrà instruir el tauler que renderitzi els torns previs des del `history`.

Primer, anem a establir l'estat inicial per al component Game en el seu constructor:

```javascript{2-10}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      xIsNext: true,
    };
  }

  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}
```

Després, tenim que el component Board rep els props `squares` i `onClick` del component Game. Des que ara tenim un sol gestor de clic en Board per a molts Squares, necessitem passar la ubicació de cada Square al gestor `onClick` per indicar què quadrat va ser clickedo. Aquí hi ha els passos requerits per transformar el component Board:

* Eliminar el `constructor` en Board.
* Substituir `this.state.squares[i]` per `this.props.squares[i]` en el mètode `renderSquare` del component Board.
* Substituir `this.handleClick(i)` per `this.props.onClick(i)` en el mètode `renderSquare` del component Board.

El component Board ara es veu així:

```javascript{17,18}
class Board extends React.Component {
  handleClick(i) {
    const squares = this.state.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      squares: squares,
      xIsNext: !this.state.xIsNext,
    });
  }

  renderSquare(i) {
    return (
      <Square
        value={this.props.squares[i]}
        onClick={() => this.props.onClick(i)}
      />
    );
  }

  render() {
    const winner = calculateWinner(this.state.squares);
    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}
```

Actualitzarem el mètode `render` del component Game per utilitzar l'entrada més recent de l'historial per determinar i mostrar l'estat del joc:

```javascript{2-11,16-19,22}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
```

Atès que el component ara està renderitzant l'estat del joc, podem eliminar el codi corresponent del mètode `render` del Board. Després de refactorizar, el mètode `render` es veu així:

```js{1-4}
  render() {
    return (
      <div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
```

Finalment, ens cal moure el mètode `handleClick` del component Board al component Game. També encesitamos modificar `handleClick` perquè l'estat del component Game està estructurat diferent. En el mètode `handleClick` de Game, concatenamos la nova entrada de l'historial en `history`.

```javascript{2-4,10-12}
  handleClick(i) {
    const history = this.state.history;
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares,
      }]),
      xIsNext: !this.state.xIsNext,
    });
  }
```

> Nota
>
> A diferència del mètode `push()` dels arrays que has d'estar més familiaritzat, el mètode `concat()` no Mutal l'array original, per això ho preferim.

En aquest punt, el component Board només necessita els mètodes `renderSquare` i` render`. L'estat del joc i el mètode `handleClick` haurien d'estar en el component Game.

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/EmmOqJ?editors=0010)**

### Ara es mostren els moviments anteriors {#showing-the-past-moves}

Des que vam gravar l'historial del joc tic-tac-toe, ara podem mostrar-lo al jugador com una llista de moviments anteriors.

Vam aprendre abans que els elements de React són objectes de primera classe en javaScript; així que podem passar-ho al voltant de les nostres aplicacions. Per renderitzar múltiples elements en React, podem usar una matriu d'elements de React.

En javaScript, els arrays tenen un [mètode `map()`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/map) que és comunament usat per mapejar dades a altres dades, per exemple:

```js
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
```

Usant el mètode `map`, podem mapejar el nostre historial de moviments a elements de React representant botons a la pantalla, i mostrant una llista de potones per "saldar" a moviments anteriors.

Anem a `mapejar` sobre el` historial` en el mètode `render` del component Game:

```javascript{6-15,34}
  render() {
    const history = this.state.history;
    const current = history[history.length - 1];
    const winner = calculateWinner(current.squares);

    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });

    let status;
    if (winner) {
      status = 'Winner: ' + winner;
    } else {
      status = 'Next player: ' + (this.state.xIsNext ? 'X' : 'O');
    }

    return (
      <div className="game">
        <div className="game-board">
          <Board
            squares={current.squares}
            onClick={(i) => this.handleClick(i)}
          />
        </div>
        <div className="game-info">
          <div>{status}</div>
          <ol>{moves}</ol>
        </div>
      </div>
    );
  }
```

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/EmmGEa?editors=0010)**

Per cada moviment en l'historial del joc de tic-tac-toe, vam crear un element de llista `<li>` que conté un botó `<button>`. El botó té un gestor `onClick` que invoca un mètode anomenat` this.jumpTo()`. No hem implementat el mètode `jumpTo()` encara. Per ara, hem de veure una llista dels moviments que han ocorregut en el joc i un advertiment a la consola de les eines de desenvolupador que diu:

> Warning:
> Each child in an array or Iterator should have a unique "key" prop. Check the render method of "Game".

Anem a discutir que significa l'advertència anterior.

### Triant una key {#picking-a-key}

Quan renderizamos una llista, React emmagatzema informació sobre cada element de la llista renderitzat. Quan actualitzem una llista, React necessita determinar que ha canviat. Podríem haver afegit, eliminat, reacomodado, o actualitzat els elements de la llista.

Imagina canviar de

```html
<li>Alexa: 7 tasks left</li>
<li>Ben: 5 tasks left</li>
```

a

```html
<li>Ben: 9 tasks left</li>
<li>Claudia: 8 tasks left</li>
<li>Alexa: 5 tasks left</li>
```

A més dels comptadors actualitzats, un humà llegint això probablement diria que es van intercanviar l'ordre d'Alexa i Ben i van inserir Claudia entre ells. No obstant això, React és un programa d'ordinador i no sap el que intentem. Perquè React no pot saber les nostres intencions, ens cal especificar una propietat *key* per a cada element de la llista per diferenciar cada un dels seus germans. Una opció seria fer servir els strings `alexa`,` ben`, `claudia`. Si anéssim a mostrar dades d'una base de dades, els ids de base de dades d'Alexa, Ben i Claudia podrien ser usats com keys.

```html
<li key={user.id}>{user.name}: {user.taskCount} tasks left</li>
```

Quan una llista és re-renderitzada, React pren cada key l'element de la llista i busca l'element de la llista anterior que coincideixi l'key. Si la llista actual té un key que no existia abans, React crea un component. Si a la llista actual li cal un key que existia en la llista anterior, React destrueix el component previ. Si dos keys coincideixen, el component corresponent és mogut. Els keys li diuen a React sobre la identitat de cada component la qual cosa permet als React mantenir el seu estat entre re-renderitzats. Si l'key d'un component canvia, el component serà destruït i re-creat amb un nou estat.

`key` és una propietat especial i reservada a React (igual que amb` ref`, una característica més avançada). Quan un elementoes creat, React extreu la propietat `key` i l'emmagatzema directament en l'element retornat. Tot i que el `key` es pot veure que pertany a les `props`, `key` no pot ser referenciat usant `this.props.key`. React automàticament fa servir `key` per decidir quins components actualitzar. Un component no pot esbrinar sobre la seva `key`.

**Es recomana fortament que facis servir keys apropiat quan construeixis llistes dinàmiques**. Si no tens un key apropiat, potser vulguis considerar reestruturar les teves dades perquè puguis tenir-la.

Si la key no està especificat, React presentarà un advertiment i farà servir l'índex de l'array com a índex per defecte. Usant l'índex de l'array com un key és problemàtic quan intentes reordenar els elements d'una llista o inserir/eliminar elements de la llista. Passar explícitament `key={i}` silencia l'advertència però té els mateixos problemes que els índexs de l'array i no és recomanat en la majoria dels casos.

Els keys no necessiten ser globalment únics; només necessiten ser únics entre components i els seus germans.


### Implementant viatge en el temps {#implementing-time-travel}

En l'historial del joc de tic-tac-toe, cada moviment anterior té un ID únic associat; és el nombre seqüencial del moviment. Els moviments mai són reordenats, eliminats, o inserits en el medi, així que és segur usar els índexs del moviment com un key.

En el mètode `render` del component Game, podem afegir el key com `<li key={moure}` l'advertiment React hauria de desaparèixer:

```js{6}
    const moves = history.map((step, move) => {
      const desc = move ?
        'Go to move #' + move :
        'Go to game start';
      return (
        <li key={move}>
          <button onClick={() => this.jumpTo(move)}>{desc}</button>
        </li>
      );
    });
```

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/PmmXRE?editors=0010)**

Fent clic en qualsevol dels botons de la llista llança un error perquè el mètode `jumpTo` no està definit. Abans d'implementar `jumpTo`, afegirem `stepNumber` a l'estat del component Game per indicar quin pas estem veient actualment.

Primer, afegeix `stepNumber: 0` a l'estat inicial en el constructor de Game:

```js{8}
class Game extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      history: [{
        squares: Array(9).fill(null),
      }],
      stepNumber: 0,
      xIsNext: true,
    };
  }
```

Després, definirem el mètode `jumpTo` en el component Game per actualitzar el `stepNumber`. També establirem `xIsNext` a veritable si el nombre que estem canviant en` stepNumber` és parell:

```javascript{5-10}
  handleClick(i) {
    // aquest mètode no ha canviat
  }

  jumpTo(step) {
    this.setState({
      stepNumber: step,
      xIsNext: (step % 2) === 0,
    });
  }

  render() {
    // aquest mètode no ha canviat
  }
```

Ara farem uns petits canvis al mètode `handleClick` de Game, el quin es dispara quan fas clic en un quadrat.

L'estat `stepNumber` que hem afegit ara reflecteix el moviment mostrat a l'usuari. Després de fer un nou moviment, necessitem actualitzar `stepNumber` afegint` stepNumber: history.length` com a part de l'argument de `this.setState`. Això assegura que no ens estanquem mostrant el mateix moviment després d'un nou realitzat.

També reemplaçarem `this.state.history` per` this.state.history.slice (0, this.state.stepNumber + 1) `. Això assegura que si "tornem en el temps" i després fem un nou moviment des d'aquest punt, vam tirar tot la història "futura" que ara seria incorrecta.

```javascript{2,13}
  handleClick(i) {
    const history = this.state.history.slice(0, this.state.stepNumber + 1);
    const current = history[history.length - 1];
    const squares = current.squares.slice();
    if (calculateWinner(squares) || squares[i]) {
      return;
    }
    squares[i] = this.state.xIsNext ? 'X' : 'O';
    this.setState({
      history: history.concat([{
        squares: squares
      }]),
      stepNumber: history.length,
      xIsNext: !this.state.xIsNext,
    });
  }
```

Finalment, modificarem el mètode `render` del component Game de sempre renderitzar l'últim moviment a renderitzar el moviment seleccionat actualment d'acord a` stepNumber`:

```javascript{3}
  render() {
    const history = this.state.history;
    const current = history[this.state.stepNumber];
    const winner = calculateWinner(current.squares);

    // la resta no ha canviat
```

Si clickeamos en qualsevol pas de la història del joc, el tauler tic-tac-toe hauria d'actualitzar immediatament per mostrar el tauler com es veia després que el pas va ocórrer.

**[Veure el codi complet en aquest punt](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**

### En conclusió {#wrapping-up}

Felicitacions! Has creat un joc de tic-tac-toe que:

* Et permet jugar tic-tac-toe,
* Indica quan un jugador ha guanyat el joc,
* Emmagatzema l'historial del joc com va progressant,
* Permet als jugadors revisar l'historial del joc i veure versions anteriors del tauler de joc.

Bon treball! Esperem que ara et sentis que tens una entesa descente sobre com funciona React.

Revisa el resultat final aquí: **[Resultat final](https://codepen.io/gaearon/pen/gWWZgR?editors=0010)**.

Si tens un temps extra o vols practicar les teves noves habilitats de React, aquí algunes idees de millores que pots fer al joc de tic-tac-toe, les quals estan llistades en ordre de dificultat creixent:

1. Mostra la ubicació per a cada moviment en el format (columna, fila) a la llista de l'historial de moviments.
2. Converteix en negreta l'element actualment seleccionat a la llista de moviments.
3. Reescriu el Board per utilitzar 2 cicles per fer els quadrats en comptes d'escriure'ls a mà.
4. Afegeix un botó de switch que et permeti ordenar els moviments en ordre ascendent o descendent.
5. Quan algú guanya, ressalta els 3 quadrats que van fer que guanyi.
6. Quan ningú guanya, mostra un missatge sobre que el resultat és un empat.

Al llarg d'aquest tutorial, hem abordat conceptes de React incloent elements, components, props, i estat. Per a una explicació més detallada de cada un d'aquests temes, revisa [la resta de la documentació](/docs/hello-world.html). Per aprendre més sobre definir components, revisa la [referència de l'API de `React.Component`](/docs/react-component.html).