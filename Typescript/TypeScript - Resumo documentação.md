
### Introdução

O TypeScript é um superconjunto tipado do JavaScript que adiciona recursos de tipagem estática ao JavaScript. Ele é projetado para desenvolvimento em larga escala e oferece vantagens como autocompletar, detecção de erros durante a compilação e refatoração de código mais segura.

### Instalação

Para começar a usar o TypeScript, você pode instalá-lo através do npm (Node Package Manager) com o seguinte comando:

`npm install -g typescript`

### Configuração do Projeto

O TypeScript usa um arquivo de configuração chamado `tsconfig.json` para definir as opções de compilação do projeto. Aqui estão algumas opções comuns que podem ser configuradas no arquivo `tsconfig.json`:


```json
{   
	"compilerOptions": {     
		"target": "es6",
		"module": "commonjs",
		"outDir": "dist"
		},   
	"include": [
	"src/**/*"
	] 
}
```

### Tipos Básicos

O TypeScript oferece suporte a vários tipos básicos, incluindo `number`, `string`, `boolean`, `null`, `undefined`, `object`, `symbol` e `void`. Aqui estão alguns exemplos de declaração de tipos básicos:

```ts

const numero: number = 10;
const texto: string = "Olá, mundo!";
const ativo: boolean = true;
const nulo: null = null;
const indefinido: undefined = undefined;
const desconhecido: unknown;
const vazio: void = undefined;
const funcao: () => string
const array: Array<String> = ["valor"];
const array: string[] = ["valor"];

const tupla: [number, string?, ...string[]] = [1, "valor", "valores..."];

const objeto: object = { chave: "valor" };
const objeto: {
	chaveA: string;
	chaveB?: string;
	[key: string]: unknown; 
	// serve para deixar aberto o objeto, ou seja adicionar quantos índices eu quiser
} = { chaveA: "valorA", 
	 chaveB: "valorB", 
	 chaveC: string
}

enum Cores {
	VERMELHO, // 0
	AZUL = 100, // 100
	AMARELO = 'ROXO', // 300
}

const simbolo: symbol = Symbol("chave");
const nunca: never = throw new Error('Erro');
```

#### Ressalvas

1. __Any(qualquer)__
	- Esse tipo que você não vai querer ter nos seus códigos, ele representa uma falta de tipo.
2. __Void(Vazio)__
	- Indicado quando uma função ou valor não retorna nada, ou seja retorna undefined.
3. __Tuple(Tupla)__
	- Array com tipos específicos para cada índice .
4. __Enum(Enumeração)__
	- Uma estrutura de dados não ordenado, é utilizado quando tem mais de uma opção para uma mesma coisa.
5. __Unknown(Desconhecido)__
	- Ele se comporta como um any mais seguro, porque ele vai te força fazer a checagem de tipos antes de você fazer qualquer operação.

### Anotações de Tipo(Type-Annotation)

O TypeScript permite adicionar anotações de tipo a variáveis, parâmetros de função, retornos de função e muito mais. Aqui estão alguns exemplos:

```ts
let numero: number; 

numero = 1;
```

### Anotações de Asserção(Type-Assertions)

É um tipo de técnica que informa ao compilador sobre o tipo daquela variável   ```
```ts
let str: unknown = "valor";
console.log(str);

let len: number = (str as string).length;
console.log(len);

```

retorno:
```ts
valor
5
```

>Dica: Também pode ser usado como um elemento para tipar um elemento HTML, só recomendado se você ter absoluta certeza que aquele elemento existe. 

>Exemplo:
```ts
// container pode não vai existir
const container = document.querySelector('.container');
if (container) container.style.background = 'red';

// body sempre vai existir
const body = document.querySelector('body') as HTMLBodyElement;
body.style.background = 'red';
```

### Interfaces

As interfaces são usadas para definir a estrutura de um objeto. Elas podem conter propriedades e métodos, e são amplamente utilizadas para definir contratos em TypeScript. Aqui está um exemplo de interface

- Geralmente quando queremos modelar objetos usamos interface, quando não for usamos Type Alias.
- As interfaces só podem ser usadas para declarar as formas dos objetos, mas não para renomear tipos primitivos.

```ts
interface Pessoa {   
	nome: string;
	idade: number;
	adulto?: boolean, // ? - significa que pode ser omitida
	saudacao(): void;
}
```

#### Declaration merging

Essa funcionalidade está presente apenas nas **interfaces**, que basicamente permite que o Typescript misture duas ou mais interfaces que possuem o mesmo nome em apenas uma declaração.

```ts
interface User {
  nome: string
}

interface User {
  lastName: string
}

const user1: user = {
  name = "Mario",
  lastName = "Teste"
}
```

### Type Alias

É a mesma coisa de interface porem **interfaces são abertas e Type Alias são fechados**. Isso significa não podendo fazer "declaration merging" que você pode estender interfaces declarando uma segunda vez.

- Geralmente quando queremos modelar objetos usamos interface, quando não for usamos Type Alias.

```ts
type Pessoa = {   
	nome: string;
	idade: number;
	adulto?: boolean, // ? - significa que pode ser omitida
	saudacao(): void;
}
```

#### Union e Intersection

```ts
// É um numero ou string 
const unionTypes: string | number = "1" // or

type Nome = {
	nome: string
}

type Idade = {
	idade: number
}

// É Nome e Idade 
const IntersectionTypes = string & number; // and
// IntersectionTypes = { nome: string, idade: number }
```

### Classes

As classes permitem definir objetos com comportamentos e propriedades específicos. Elas podem herdar de outras classes e implementar interfaces. Aqui está um exemplo de classe:

```ts
class Animal {
  nome: string;

  constructor(nome: string) {
    this.nome = nome;
  }

  emitirSom(): void {
    console.log("O animal está emitindo um som.");
  }
}

```

## Extends e implements

No Typescript podemos utilizar o extends e o implements nas **interfaces**, algo que não é possível ao utilizar o type, ou seja, as interfaces em TypeScript podem **extender** as classes, este é um conceito muito interessante que ajuda muito ao utilizarmos uma programação mais orientada a objetos ou quando queremos reaproveitar propriedades de tags **HTML** em componentes **JSX**.

- Por exemplo, imaginemos que temos uma classe chamada Carro e uma interface chamada **NewCar**, podemos facilmente extender esta classe usando uma interface:

```ts
class Car {
  printCar = () => {
    console.log("this is my car")
  }
};

interface NewCar extends Car {
  name: string;
};

class NewestCar implements NewCar {
  name: "Car";
  constructor(engine:string) {
    this.name = name
  }
  printCar = () => {
    console.log("this is my car")
  }
};
```

## Decorators

Para usar os decorators é necessário estar habilitado a opção em ``tsconfig.json`` :

```json
{
	"experimentalDecorators": true,
	"emitDecoratorMetadata": true,
}
```

Um decorador é uma função que finge ser sua classe ou objeto para fazer outra função. uma declaração especial para adicionar funcionalidades extras a uma declaração de classe, método, acessador, propriedade ou parâmetro.

- Toda vez que eu chamar ``Animal`` ele primeiro executara minha função ``decorator`` que nela por sua vez inverte o primeiro argumento e o segundo.

```ts
interface Constructor {
	new (...args: any[]): any
}
// decorator decora partindo de base da class original usando argumentos dela
function inverteNomeECor(target: Constructor) {
  return class extends target {
    cor: string;
    nome: string;
    constructor(...args: any[]) {
      super(...args);
      // Executa função para inverter argumentos
      this.nome = this.inverte(args[0]);
      this.cor = this.inverte(args[1]);
    }
    
    inverte(valor: string): string {
      return valor.split('').reverse().join('');
    }
  };
}

@inverteNomeECor
export class Animal {
  constructor(public name: string, public cor: string) {}
}

// é a mesma coisa de @decorator:
// const AnimalDecorated = decorator(Animal);
const animal = new Animal('Luiz', 'roxo');
// { nome: 'ziuL', cor: 'oxor' }
```

### Parâmetros dentro de decoradores

``Decorators`` podem receber parâmetros em seu corpo.

```ts
@inverteNomeECor('valor1', 'valor2')
export class Animal {
  constructor(public name: string, public cor: string) {}
}
```

```ts
interface Constructor {
	new (...args: any[]): any
}
// Usamos uma função que retorna um decorator para usar parametros
export function inverteNomeECor(param1: string, param2: string) {
	function (target: Constructor) {
	  return class extends target {
	    cor: string;
	    nome: string;
	    constructor(...args: any[]) {
	      super(...args);
	      // Executa função para inverter argumentos
	      this.nome = this.inverte(args[0]);
	      this.cor = this.inverte(args[1]);
	    }
	    
	    inverte(valor: string): string {
	      return valor.split('').reverse().join('')
	      // Usando parametros
	      + ' ' + param1 ' ' + param2;
	    }
	  };
	}
}

@inverteNomeECor('valor1', 'valor2')
export class Animal {
  constructor(public name: string, public cor: string) {}
}

// é a mesma coisa de @decorator:
// const AnimalDecorated = decorator(Animal);
const animal = new Animal('Luiz', 'roxo');
// { nome: 'ziuL valor1 valor2', cor: 'oxor valor1 valor2' }
```
 
### Decoradores de métodos (method decorator)

Serve para decorar um método, como mudar se ele pode ser modificado, enumerável e até mudar o próprio valor dele:

```ts
@decorator
metodo(msg: string): string {
	return `${this.nome} ${this.sobrenome}: ${msg}`;
}
```

```ts
function decorator(
	classPrototype: any,
	nomeMetodo: string,
	descriptor: PropertyDescriptor,
): PropertyDescriptor | void {
	console.log(
	classPrototype, // UmaPessoa
	nomeMetodo, // metodo
	descriptor, /*
	{	
		value: [Function: metodo],
		writable: true,
		enumerable: false,
		configurable: true,
	}
	*/
	);
	return {
		// Coloca o primeiro argumento da mensagem do metodo em maiúsculas
		value: function (...args: string[]) {
			return args[0].toUpperCase();
		},
		// writable: false,
		// enumerable: false,
		// configurable: false,
	};
}

export class UmaPessoa {
	nome: string;
	sobrenome: string;
	
	constructor(nome: string, sobrenome: string) {
		this.nome = nome;
		this.sobrenome = sobrenome;
	}
	
	@decorator
	metodo(msg: string): string {
		return `${this.nome} ${this.sobrenome}: ${msg}`;
	}
	
}

const pessoa = new UmaPessoa('Luiz', 'Otavio');

const metodo = pessoa.metodo('Olá mundo')
console.log(metodo); // OLÁ MUNDO
```

### Decoradores de parâmetros (parameter decorator)

Serve para decorar um parâmetro, porem só serve para espiar o parâmetro não modifica-lo:

```ts
metodo(@decorator msg: string): string {
	return `${this.nome} ${this.sobrenome}: ${msg}`;
}
```

```ts
function decorator(
	classPrototype: any,
	nomeMetodo: string | symbol,
	index: number,
): any {
	console.log(
	classPrototype, // UmaPessoa
	nomeParametro, // msg
	index, // 0
	);
}

export class UmaPessoa {
	nome: string;
	sobrenome: string;
	
	constructor(nome: string, sobrenome: string) {
		this.nome = nome;
		this.sobrenome = sobrenome;
	}
	
	metodo(@decorator msg: string): string {
		return `${this.nome} ${this.sobrenome}: ${msg}`;
	}

}

const pessoa = new UmaPessoa('Luiz', 'Otavio');

const metodo = pessoa.metodo('Olá mundo');
console.log(metodo);
```

### Decoradores de propriedade (property decorators)

Serve para decorar uma propriedade, como mudar se ele pode ser modificado, enumerável e até mudar o próprio valor dele, e além disso posso adicionar getters e setters:

```ts
export class UmaPessoa {
	@decorador
	nome: string;
	@decorador
	sobrenome: string;
	// ...
```

```ts
function decorator(
	classPrototype: any,
	nomeMetodo: string | symbol,

): any {
	console.log(
	classPrototype, // UmaPessoa
	nomePropriedade, // nome
	);
	let valorPropriedade: any;
	return {
		// getters e setters
		get: () => valorPropriedade,
		set: (valor: any) => {
			valorPropriedade = valor.split('').reverse().join();
		},
		// writable: false,
		// enumerable: false,
		// configurable: false,
	}
}

export class UmaPessoa {
	@decorador
	nome: string;
	@decorador
	sobrenome: string;
	
	constructor(nome: string, sobrenome: string) {
		this.nome = nome;
		this.sobrenome = sobrenome;
	}
	
	metodo(@decorator msg: string): string {
		return `${this.nome} ${this.sobrenome}: ${msg}`;
	}
}

const pessoa = new UmaPessoa('Luiz', 'Otávio');

const metodo = pessoa.metodo('Olá mundo');
console.log(metodo); // ziuL oivátO: Olá mundo

```


<img align="right" width="120" height="120" src="https://media.giphy.com/media/6Fy1SaMmEBNTEjN8CB/giphy.gif">    







<div align="center"> 
  <a href="https://www.youtube.com/channel/UCNApxbcgWHv-aS9n-WDhRLA" target="_blank"><img src="https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white" target="_blank"></a>
  <a href="https://www.instagram.com/niickinn/" target="_blank"><img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-badge&logo=instagram&logoColor=white" target="_blank"></a>
 	<a href="https://www.twitch.tv/z_nikk" target="_blank"><img src="https://img.shields.io/badge/Twitch-9146FF?style=for-the-badge&logo=twitch&logoColor=white" target="_blank"></a>
 <a href="https://discord.com/channels/Nikk#4239" target="_blank"><img src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white" target="_blank"></a> 
  <a href = "https://mail.google.com/mail/u/2/#inbox"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
</div>