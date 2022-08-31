# Patrones de render y composiciones de componentes

- ⭐️ Cuando los componentes nietos de App no solo son nietos, sino también componentes hijos, podemos pasarles props directamente y mejorar su comunicación. Casi siempre que llamamos a un componente… pos lo llamamos y ya. 😅

```js
function App() {
  return (
    <TodoHeader />
  );
}

function TodoHeader() {
  return (
    <TodoCounter />
  );
}
```

- Esto implica que para compartir el estado debemos pasar props y props y props por cada componente intermedio entre App y los componentes que realmente necesiten esas props en cualquier lugar de la jerarquía. 😓

```js
function App() {
  const [state, setState] = React.setState(initialState);

  return (
    <TodoHeader state={state} setState={setState} />
  );
}

function TodoHeader({ state, setState }) {
  return (
    <header>
      <TodoCounter state={state} setState={setState} />
    </header>
  );
}

function TodoCounter({ state, setState }){
    ...
}
```

- Pero otra forma de trabajar es que App no solo llame a sus componentes directamente hijos, sino que también llamen a los siguientes componentes en la jerarquía de la aplicación. 😮

```js
function App() {
  return (
    <TodoHeader>
      <TodoCounter />
    </TodoHeader>
  );
}

function TodoHeader({ children }) {
  return (
    <header>
      {children}
    </header>
  );
}
```

- Y esta nueva forma de trabajar implica que ya no tenemos que pasar props y props y props entre App y el resto de componentes para compartir el estado, sino que App puede comunicarse directamente con el componente que realmente necesita ese estado. 🤩

```js
function App() {
  const [state, setState] = React.setState(initialState);

  return (
    <TodoHeader>
      <TodoCounter state={state} setState={setState} />
    </TodoHeader>
  );
}
```

💚 Esta es la magia de la composición de componentes.