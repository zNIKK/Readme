
## Os Pilares da POO

### Abstração

Permite __isolar de um objeto somente os conceitos que são necessários__ para o funcionamento do programa. Abaixo eu estou abstraindo muitas coisas da pessoa, ou seja eu não preciso saber a altura, o peso dessa pessoa, porque não são importantes para o programa. 

```ts
export class pessoa {
	private nome: string;
	private sobrenome: string;

	constructor(nome: string, sobrenome: string) {
		this.nome = nome;
		this.sobrenome =sobrenome;
	}
}
```

### Encapsulamento

Visa __ocultar partes internas de um objeto__ e exibir apenas o necessário pra uso externo. Não preciso saber como funciona internamente, preciso apenas saber o necessário. 
```ts
export class RemoteControl {
	constructor(private powerStatus = false ) {}
	
	public turnOn(): void {
		this.powerStatus = true;
	}

	public turnOff(): void {
		this.powerStatus = false;
	}
	
	public getStatus(): boolean {
		return this.powerStatus;
	}
}
```

### Herança

Visa passar características de um objeto para outro.

```ts
export abstract class Animal {
	constructor(public name: string ) {}
	abstract makeNoise(): void;
}

export class Dog extends Animal {
	makeNoise(): void {
		console.log(`${this.name} está fazendo AU AU...`);
	};
}

export class Cat extends Animal {
	makeNoise(): void {
		console.log(`${this.name} está fazendo MIAU...`);
	};
}
```

### Polimorfismo

Algo que é polimorfo tem a habilidade de assumir diferentes formas.

```ts
class AnimalSounds {
	play playSound(animal: Animal): void {
		animal.makeNoise();
	};
}

const dog = new Dog('Tina');
const cat = new Dog('Suzy');
const animalSounds = new AnimalSounds();
animalSounds.play(dog); // Tina está fazendo AU AU...
animalSounds.play(cat); // Suzy está fazendo MIAU...
```

## Classes

formato básico de uma Classe:

```ts
export class Empresa {
	// Declarar variáveis
	public readonly nome: string; 
	private readonly colaboradores: Colaborador[] = [];
	protected readonly cnpj: string;
	
	// Constructor
	constructor(nome: string, cnpj: string) {
		this.nome = nome;
		this.cnpj = cnpj;
	}

	// metodos
	adcionaColaborador(colaborador: Colaborador): void {
		this.colaboradores.push(colaborador);
	}
	
	mostrarColaboradores(): void {
		for (const colaborador of this.colaboradores) {
		console.log(colaborador);
		}
	}
}
```

### Modificadores de acesso

São para controlar o comportamento de acesso externo a essas propriedades.

- Para ter esse controle, há os modificadores de acesso, são eles:

#### Public

Pode ser acessado tanto pela mesma classe, classes filhas e outras classes.

```ts
class Pessoa{
	nome: string = "valor";
	idade: number = 12
	estaVivo: boolean = true;
}

let pessoa = new Pessoa();
pessoa.nome = "Paulo";
// com o modificador public podemos acessar e alterar o valor da propriedade nome fora da classe

```

#### Private

Pode ser acessada somente pela própria classe.

```tsx
class Pessoa{
	private nome: string = "TreinaWeb";
	idade: number = 12
	estaVivo: boolean = true;
}

let pessoa = new Pessoa();
pessoa.nome = "Paulo"; 
// Utilizando private não podemos mais acessar desta forma
```

#### Protected

Pode ser acessado pela mesma classe e classes filhas, não pode ser acessado por outras classes.

```tsx
class Pessoa{
	nome: string;
	idade: number;
	protected estaVivo: boolean;

	constructor(
		nome: string, 
		idade: number, 
		estaVivo: boolean
	){
    	this.nome = nome;
    	this.idade = idade;
    	this.estaVivo = estaVivo;
	}
}

class PessoaFisica extends Pessoa{
  cnpj: number;

  constructor(
	  nome: string, 
	  idade: number, 
	  estaVivo: boolean, 
	  cnpj: number
  ){
	super(nome, idade, estaVivo); 
	// ao utilizar protected, podemos acessar por classes filhas e pela própria classe;
	this.cnpj = cnpj;
  }
}
 
```

## Super-Class

Uma classe super é uma classe que está acima na hierarquia das classes que estende elas.

### Super

Serve para pegar um método ou variável de uma ``sub-class`` para uma ``super-class``.

```ts
// Super-Class
class Pessoa{
	nome: string;
	idade: number;

	getNomeEIdade(): string {
		return this.nome + ' ' + this.idade;
	}
	
	constructor( nome: string, idade: number ){
    	this.nome = nome;
    	this.idade = idade;
	}
}

// Sub-Class
class Aluno extends Pessoa{
	constructor( 
		nome: string, 
		idade: number, 
		public cpf: string // criei um novo argumento na classe Aluno
	) {
		// super usado para pegar todos os argumentos da super
		super(nome, idade);
		this.cpf = cpf;
	}
	getNomeEIdade(): string {
		console.log('FAZENDO ALGO ANTES');
		const result = super.getNomeEIdade();
		// result = this.nome + ' ' + this.idade;
		return result + ' HEYYYYYYYYYY!'
	}
}
```

## Getters e Setters

São usados para proteger seus dados, especialmente na criação de classes. Para cada instância de variável, um método ``getter`` retorna seu valor, enquanto um método ``setter`` o define ou atualiza.

```ts
class Pessoa{
	private nome: string;
	private idade: number;
	
	constructor( 
		private nome: string, 
		private idade: number, 
		private cpf: string 
	){
    	this._nome = nome;
    	this._idade = idade;
    	this._cpf = cpf;
	}
	
	get nome(): string {
		return this.nome;
	}
		
	set idade(valor: string) {
		this.idade = valor;
	}
	
	get cpf(): number {
		this.cpf.replace(/\D/g, ''); // tira todos os simbolos
	}
}

// como nome é privado eu não consigo instânciar ele, mas com get eu consigo

const pessoa = new Pessoa("nome", 18, '000.000.000-00')
console.log(pessoa).nome) // ERRADO

console.log(pessoa).getNome // CERTO
// nome
console.log(pessoa).getCpf())
// 00000000000

pessoa.setIdade = 12;

console.log(pessoa)
```

## Static

É um método estático para sua classe e um modificador de acesso, pode ser acessado sem instanciar a classe.

- Métodos estáticos tem muitas funções uteis, desde __criar um clone de um objeto__, considerando que as propriedades estáticas __são úteis para caches__. Até __configurações fixas__, ou qualquer outra informação que não precisa ser replicada nas instâncias.

```ts
class Pessoa{
	static propriedadeEstatica = 'valor';
	
	static falaOi(): void {
		console.log('oi');
	}
}
// Só poderei chamar ele sem instaciar a classe
Pessoa.falaOi();
```

#### Private Constructor

você pode privar o construtor de uma classe assim não podendo usar mais a palavra ``new`` antes da classe. Serve para impor regras de criação de objetos.

- Sempre que declarar um ``private constructor``, não se pode criar múltiplas instâncias de um ``class``.
- Declara um campo privado e estático chamado ``instance`` no qual terá o tipo ``Singleton``. Depois declara um método estático chamado ``getInstance()`` no qual irá checar se uma instância da classe ``Singleton`` foi criada. Se não foi criada ele instanciará o objeto.

```ts
class Singleton {
  private static instance: Singleton;

  private constructor(public name: string) {}

  static getInstance(name: string): Singleton {
    if (this.instance) return this.instance;
    this.instance = new Singleton(name);
    return this.instance;
  }
}
// com o private constructor isso não poderá ser feito:
let singleton1 = new Singleton(); 
let singleton2 = new Singleton(); 

console.log(singleton1 === singleton2) // false

// Chamar "getInstance()" múltiplas vezes não irá criar uma nova instância.
let singleton1 = Singleton.getInstance();
let singleton2 = Singleton.getInstance();

console.log(singleton1 === singleton2) // true

```

## Abstract

As classes abstratas são principalmente para herança, onde outras classes podem derivar delas. Não podemos criar uma instância de uma classe abstrata.

```ts
// essa classe é só um contrato para que outras classes herdam ela
export abstract class Personagem {
	constructor (
		protected nome: string,
		protected ataque: string,				
	) {}

	atacar(personagem: Personagem): void {
		personagem.perderVida(this.ataque);
	}
	// todas as classes herdadas teram esse método
	abstract bordao(): void;
}

export class Guerreira extends Personagem {
	bordao(): void {
		console.log('Guereira atacando!')
	}
}

export class Guerreira extends Personagem {
	bordao(): void {
		console.log('Monstro atacando!')
	}
}
```

## Tipos Avançados

### Type Guard

Uma maneira de checar se o tipo existe ou não em uma classe. Exemplo:

```ts
type Pessoa = { tipo: 'pessoa', nome: string };
type Animal = { tipo: 'animal', cor: string };

type PessoaOuAnimal = Pessoa | Animal;

export class Aluno implements Pessoa {
	constructor(public nome: string) {}
}

function monstraNome(obj: PessoaOuAnimal): void {
	// 1º maneira:
	// "Type guard" para checar se a chave nome existe no objeto 
	if ('nome' in obj) console.log(obj.nome);
	// 2º maneira:
	// instanceof = verifica se o "obj" está presente em "Aluno"
	if (obj instanceof Aluno) console.log(obj.nome);
	// 3º maneira:
	switch(obj.tipo) {
		case 'pessoa':
			console.log(obj.nome);
			return;
		case 'animal':
			console.log('Esse objeto não tem nome');
			return;	
	}
}

monstraNome(new Aluno('joão')); // joão
```

### Keyof e Typeof

você pode usar em um contexto de tipo para se referir ao tipo de uma variável ou propriedade.
```ts
type CoresType = {
	vermelho: string;
	verde: string;
	azul: string;
};

const coresObj: CoresType = {
	vermelho: 'red',
	verde: 'green',
	azul: 'blue',
}

function traduzirCor(
		cor: 'vermelho' | 'verde' | 'azul', 
		cores: CoresObj
	) {
	// ...
}
```

- Não precisa usar ``type alias`` para colocar um tipo que já foi atribuído no ``coresObj``, além de que eu não ficarei limitado a usar só três tipos de cores. Código usando typeof e keyof:

```ts
const coresObj = {
	vermelho: 'red', // vermelho: string;
	verde: 'green', // verde: string
	azul: 'blue', // azul: string
	// com o keyof eu posso criar quantas chaves quiser
	roxo: 'purple', 
}

function traduzirCor(
		cor: keyof CoresObj,
		// 'vermelho' | 'verde' | 'azul'
		// tipo do objeto
		cores: typeof CoresObj
	) {
	return cores[cor]
}
```

### Chaves de tipos

ajuda a manter seu código limpo, e previne que você se repita no seu código.
- Quero espelhar os dois tipos primeiros do ``type Veiculo`` para um outro ``type`` :
```ts
type Veiculo = {
	marca: string;
	// se eu trocar o ano ele não irá trocar o year no "type Car" 
	ano: number
}
// maneira errada:
type Car = {
	brand: string;
	year: string;
	name: string
}
// maneira certa:
type Car = {
	brand: Veiculo['marca'];
	year: Veiculo['ano'];
	name: string
}
```

### This Polimórfico

Ajuda a fazer uma função em cadeia. Exemplo:

```ts
export class Calculadora {
	constructor(public numero: number) {}
	
	// retorna this
	sum(n: number): this {
		this.numero += n;
		return this;
	};
	
	sub(n: number): this {
		this.numero -= n;
		return this;
	};

	div(n: number): this {
		this.numero /= n;
		return this;
	};
}

const calculadora = new Calculadora(10);
// função em cadeia só é possível porque estou retornando this
calculadora.sum(10).div(2).sub(3); // 10 + 10 / 2 - 3 = 7

```

### Overload de funções

Você pode ter múltiplas funções com o mesmo nome mas com diferentes parâmetros Baseado nos parâmetros que minha função receber a função se comportará de maneira diferente.

- define uma overload de funções no ``type Adder``. Na função ``adder`` se for mais argumentos que X e Y ele irá adicionar numa array que ira reduzir e somar as chaves dela, junto com os argumentos X e Y. a função retornara a soma de X e Y
```ts
// Overload

// a função "adder" pode receber:
// só X,
// X e Y,
// X e Y e outros argumentos...
type Adder = {
	(x: number) => number;
	(x: number, y: number) => number;
	(...arg: number[]): number;
}

const adder: Adder = (x: number, y?: number, ...args: number[]) => {
	if (args.length > 0) {
		return args.reduce((s, v) => s + v, 0) + x + (y || 0);
	}
	
	return x + (y || 0);
};

adder(1) // 1
adder(1, 2) // 3
adder(1, 2, 3) // 6
```

### Encadeamento opcional e Coalescência nula

evita em ter vários ``if`` no seu código:

- Encadeamento opcional(?): Pode não existir data no documento.

- Coalescência nula(??): Se existir ``data.toDateString`` ele irá exibir a data, se não existir ele vai exibir "Não existe data". A Coalescência nula só é mostrada se o tipo for ``undefined``, ``null``, ``false`` e ``0``

```ts
type Documento = {
	titulo: string;
	texto: string;
	data?: Date;
};

const documento: Documento = {
	titulo: "O título",
	texto: "O texto",
	// data: new Date(),
}

// jeito errado:
documento.data.toDateString() 

// jeito certo:
documento.data?.toDateString() ?? 'Não existe data'
```

