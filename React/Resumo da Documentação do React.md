---
sticker: ""
---

## Introdução ao React

- O React é uma biblioteca JavaScript para __construir interfaces de usuário.__

- Permite criar __componentes reutilizáveis e gerenciar o estado da aplicação__ de forma eficiente.

## Instalação

Primeiramente devemos instalar o React 

`npm install react --save`

Para aplicar o React no seu projeto devemos usar:

`npx create-react-app meu-app`

## Componentes

- Os componentes são a unidade fundamental no React.

- Podem ser criados como funções (Componentes Funcionais) ou classes (Componentes de Classe).

- Permitem o reuso de código e a construção de interfaces modulares.

- Exemplos:

1. em `components/myDiv.js`:

```jsx
	export function MyDiv() {
		return <div> Olá mundo </div>
	}
```

2. em `App.js` usa-se um componente `<Mydiv />`:

```jsx
import MyDiv from "components/myDiv"
function App() {
  return (
    <div className='App'>
	    <Mydiv />
    </div>
  );

}
```

## JSX

- JSX é uma sintaxe que combina HTML e JavaScript.

- Permite escrever estruturas de componentes de forma declarativa.

- Facilita a criação de elementos e sua renderização no DOM.

  

## Estado e Ciclo de Vida

- O estado é um objeto que armazena informações mutáveis ​​relacionadas a um componente.

- O ciclo de vida do componente descreve os diferentes estágios pelos quais ele passa, desde a criação até a destruição.

- Métodos de ciclo de vida, como `componentDidMount` e `componentWillUnmount`, permitem executar ações em momentos específicos.

  

## Renderização Condicional

- A renderização condicional permite mostrar diferentes elementos com base em uma condição.

- Pode ser feita usando operadores lógicos, operadores ternários ou estruturas de controle, como `if` e `switch`.

  

## Manipulação de Eventos

- Os eventos são tratados de maneira semelhante aos eventos DOM tradicionais.

- Permitem que os componentes respondam a ações do usuário, como cliques e digitação.

  

## Comunicação entre Componentes

- A comunicação entre componentes pode ser feita através de props (propriedades) ou por meio de um gerenciamento de estado compartilhado, como o Redux.

  

## Reconciliação e Chaves

- A reconciliação é o processo em que o React atualiza a árvore de elementos para refletir as mudanças no estado ou nas props.

- O uso de chaves (keys) ajuda o React a identificar de forma eficiente os elementos da lista que foram alterados, adicionados ou removidos.

  

## Hooks

- Os hooks são funções especiais que permitem usar recursos do React em componentes funcionais.

- Permitem adicionar estado, lidar com efeitos colaterais e muito mais, sem precisar escrever uma classe.

### UseState

- Uma variável de estado, declarada no topo do seu componente. Define um valor padrão para uma variável e usa-o entre o componente.

- Exemplos:
```js
const [state, setState] = useState(initialState); 
```

 1. `setState` serve para redefinir o valor do ``state`` alterando-a.

### UseEffect

- Permite que use um efeito paralelo no seu componente a cada vez que aquela variável de estado for alterada.
- Exemplos:
```js
const [count, setCount] = useState(0);

  useEffect(() => {
    setTimeout(() => {
      setCount(count + 1);
    }, 1000);
  }, [count]);
```
- Eu defini um state chamado ``count`` que começa com 0, usando o ``useEffect`` dentro da função ``setTimeout``(função para colocar um intervalo). A cada 1 segundo ele executa o ``setCount`` definindo + 1 ao variável count. Porem ai entra o useEffect, como count foi é alterado ele irá executar denovo e denovo.

### UseReduce

- Permite você adicionar um reducer no seu componente

#### O que é um Reducer?

- Componentes com muitas mudanças de estados podem se espalhar por muitos eventos, podendo ficar muito pesado e sendo difícil de ler.

```jsx
const [tasks, setTasks] = useState(initialTasks);

function handleAddTask(text) {
	// código para adicionar tarefas na lista
	setTasks(...)
}

function handleChangeTask(task) {
	// código para mudar tarefas na lista
	setTasks(...)
}

function handleDeleteTask(taskId) {
	// codigo para deletar tarefas na lista
	setTasks(...)
}

```
- A cada evento que esta chamando ``setTasks`` o componente cresce ainda mais. Para reduzir essa complexidade mantenha toda lógica em um local de fácil acesso. Você pode mover todo esse código dentro de um componente chamado ``reducer``
- Reducer são uma maneira diferente de states. Você pode migrar um ``useState``
para um ``useReducer`` em 3 passos.
	1. **Mova** de um ``state`` para uma ação de ``dispatching`` 
	2. **Escreva** uma função reducer
	3. **Use** o reducer em seu componente

- Exemplos:

##### Passo 1. Dispatching

```jsx
const [tasks, setTasks] = useState(initialTasks);

function handleAddTask(text) {
	// código para adicionar tarefas na lista
	dispatch(
	// "action" object:
	{
		type: 'added',
		id: nextId++,
		text: text,
	})
}

function handleChangeTask(task) {
	// código para mudar tarefas na lista
	dispatch({
		type: 'changed',
		text: text,
	})
}

function handleDeleteTask(taskId) {
	// código para deletar tarefas na lista
	dispatch({
		type: 'deleted',
		id: taskId,
	})
}

```
- O objeto que você passa é chamado de ação(action)

##### Passo 2. Escrever um reducer

1. Declare um estado atual (`tasks`) como o primeiro argumento.
2. Declare um objeto `action` como o segundo argumento.
3. Retorna o proximo state de um reducer (which React will set the state to).
```jsx
function yourReducer(state, action) {  
	if (action.type === 'added') {
		// código para adicionar tarefas na lista
	} else if (action.type === 'changed') {  
		// código para mudar tarefas na lista
	} else if (action.type === 'deleted') {
		// código para deletar tarefas na lista
	}
```
> Dica:
> Também pode ser usado com o switch:
```jsx
function yourReducer(state, action) {
	switch (action.type) {  
		case 'added': {
				// código para adicionar tarefas na lista
			}
		case 'changed': {  
				// código para mudar tarefas na lista
			}    
		case 'deleted': {  
				// código para deletar tarefas na lista	
			}  
	
	}
}
```

##### Passo 3. Usar um reducer

- Para usar esse reducer você precisa usar o ``useReducer``
- Então você deve trocar o useState:
```jsx
const [tasks, setTasks] = useState(initialTasks)
```
- Pelo useReducer com 2 argumentos:
	1. A função reducer no caso ``yourReducer``;
	2. O valor inicial.
```jsx
const [tasks, dispatch] = useReducer(yourReducer, initialTasks);
```

### UseContext

#### O que é um Context?

- O Contexto permite compartilhar dados entre componentes sem precisar passar manualmente as props através de todos os níveis da árvore de componentes.

- Exemplo:
```jsx
function MyComponent() {  
	const theme = useContext(ThemeContext);
}
```
- Para passar o contexto para o painel, envolva-o um dos seus componentes parentes dentro de um correspondente. 

- A função ``MyPage`` retorna um context ``ThemeContext`` carregando um valor com uma string "dark". Assim o valor recebido pelo componente ``Panel`` é usado com ``useContext`` na classe da div. Se o checkbox estiver "checked" o valor do theme se tornara "dark", se não ele se tornara light.

```jsx
function MyPage() {  
	return (
		<ThemeContext.Provider value="dark">  
			<Panel>
				<input 
				type="checkbox" 
				onChange={(e) => {
		              setTheme(e.target.checked ? 'dark' : 'light')
		        }>Set Dark mode</button>
			</Painel>  
		</ThemeContext.Provider>  
	);  
}

function Panel({ children }) {
  const theme = useContext(ThemeContext);

  return (
	// className="dark" || "light"
    <div className={theme}>
    // children = serve para envolver outras tags e componentes
      {children}
    </div>
  )
}

```
- Você pode passar também objetos e funções no value, em pequenos aplicativos isso não é problemático, porem em um projeto grande esse contexto irá re-renderizar muitas vezes.

- `<AuthContext.Provider value={currentUser, login}>`
- Para fazer com que o Context não se re-renderize muitas vezes você tem que envolver a função com os hooks ``useCallback`` e envolver o objeto em um ``useMemo``.

```jsx
function MyApp() {  
	const [currentUser, setCurrentUser] = useState(null);
	
	// "useCallback" retorna uma função memorizada.
	const login = useCallback((response) => {  
		storeCredentials(response.credentials);  
		setCurrentUser(response.user);  
	}, []);  
	// "useMemo" retorna um valor memorizado 
	const contextValue = useMemo(() => ({  
		currentUser,  
		login  
	}), [currentUser, login]);  
	
	return (  
		<AuthContext.Provider value={contextValue}>  
			<Page />  
		</AuthContext.Provider>  
	
	);
}
```

### UseCallback

-  Permite armazenar em memoria (armazena sua saída para que na próxima vez seja chamada com a mesma entrada) uma definição de função entre re-renderizações.
- Limitando a função para rodar só quando uma das dependências mudar. Como ``useEffect``.
- Uma das razões para usar-lo, é prevenir o componente seja renderizado novamente, a menos que seus props tenham mudado.

``const cachedFn = useCallback(fn, dependencies)``

### UseMemo

- A mesma coisa do useCallback porem usados com valores como objetos, arrays.

``const cachedValue = useMemo(calculateValue, dependencies)``

### UseRef

- Referência um valor que não precisa ser renderizado.
- Ref são perfeitos para guardar informações que não é afetado na saída visual do seu componente, por exemplo, se você precisa guardar.
- Ele também fornece um jeito de acessar o DOM.
- Exemplo:
```jsx
function App () {
	return (
		<div>
			<input type='text'/>
			<button>Foco no input</button>
		</div>
	)
}
```
- Eu preciso quando eu apertar o botão eu aplicar um focus no input e o melhor jeito de acessar é usando o ``useRef``
```jsx
function App () {
	const ref = useRef()
	console.log(ref.current) // <input type='text' ref={ref}/>
	
	function handleClick() {
		 ref.current.focus();
	} 
	return (
		<div>
			<input type='text' ref={ref}/>
			<button onClick={handleClick}>Foco no input</button>
		</div>
	)
}
```
- Outro exemplo:
```jsx
function App () {
	const [count, setCount] = useState(0)

	let count = 0 
	// em vez de usar uma variavel no corpo do componente use: 
	const ref = useRef(0)
	
	function handleClick() {
		console.log("count = " + count)
		// em vez de:
		count++;
		// use:
		ref.current++
	} 
	return (
		<div>
			<input type='text'/>
			<button onClick={handleClick}>incrementar count</button>
			<h1>{counter}</h1>
			<button onClick={() => setCounter(c => c + 1)}>
				+1
			</button>
		</div>
	)
}
```
- Quando eu clicar no botão __incrementar count__ ele vai contar normalmente.
- Retorno:
```js
// clico 3 vezes no "count"
count = 1
count = 2
count = 3

// clico 1 vez no +1 do useState() e depois clico 1 vez no "count"
count = 1
```

- Porem quando eu clico no botão +1 o count vai perder seu valor e voltara ao seu estado padrão. Isso acontece porque quando eu atualizo um valor do useState ele ira re-renderizar todo componente.

## Referências

- [Documentação oficial do React](https://reactjs.org/docs/getting-started.html)