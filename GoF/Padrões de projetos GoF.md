
# Padrões de projeto de criação (creational)

Os padrões de projeto de criação são padrões que abstraem o processo de instanciação e criação de objetos. Eles ajudam a tornar um sistema independente de como seus objetos são representados, criados e compostos. Geralmente, atingem este objetivo delegando tarefas para outros objetos.

Esses padrões dão muita flexibilidade ao sistema, porque encapsulam o conhecimento sobre quais classes concretas são usadas. Além disso, ocultam o modo como as instâncias são criadas e compostas. O foco é eliminar conhecimento do cliente sobre o _QUE_, _COMO_ e _QUANDO_ está sendo criado e _QUEM_ faz parte do processo de criação. 

## Padrões e intenções

Os padrões de projeto de criação originais da GoF são (nome e intenção):

- ***Singleton*** - Garantir que uma classe tenha somente uma instância e fornecer um ponto global de acesso para ela.

- ***Builder*** - Separar a construção de um objeto complexo de sua representação, de modo que o mesmo processo de construção possa criar diferentes representações;

- ***Prototype*** - Especificar os tipos de objetos a serem criados usando uma instância prototípica e criar novos objetos copiando este protótipo;

- ***Factory Method*** - Definir uma interface para criar um objeto,  mas deixar as subclasses decidirem qual classe a ser instanciada. O Factory Method permite a uma classe postergar (defer) a instanciação às subclasses;

- ***Abstract Factory*** - Fornecer uma interface para criação de famílias de objetos relacionados ou dependentes sem especificar suas classes concretas;

## Singleton

### Intenção oficial

Garantir que uma classe tenha **somente uma instância** e **fornecer um ponto global de acesso para ela.**

### Visão Geral

-  Geralmente usado para _acesso a recursos compartilhados_, como acesso à base de dados, interfaces gráficas, sistema de arquivos, servidores de impressão, logger e outros.

-  Também usado para _substituir variáves globais_ como em casos de uso de objetos de configuração do sistema como um todo.


### Diagrama
![[Singleton.png]]
```ts
export class Singleton {
	private static _instance: Singleton | null = null;
	
	private constructor() {
	}
	// metodo que se comporta como um atributo
	static get instance(): Singleton {
		if(Single._instance === null) {
			// O new é usado somente uma vez na aplicação
			Singleton._instance = new Singleton()
		}
		return Singleton._instance;
	}
}

const instance1 = Singleton.instance;
const instance2 = Singleton.instance;

console.log(instance1 === instance2) // true
```

### Aplicabilidade

- Use o singleton quando uma classe precisa ter somente uma instância disponível em todo o seu programa.

- Use o singleton quando perceber que está usando variáveis globais para manter partes importantes do programa, com variáveis de configuração que são usadas por toda a aplicação.

### Vantagens

-  Você pode _permitir acesso global ao Singleton_ em toda sua aplicação, assim como fazíamos (ou fazemos com variáveis globais).

-  Uma vantagem do singleton é que podemos _proteger a instância com encapsulamento_ evitando que outro código sobrescreva seu valor.

### Desvantagens

- É mais difícil de testar

- Viola o principio da responsabilidade única

- Requer tratamento especial em casos de concorrência

- Erich Gamma (autor) descreveu que este seria o único padrão que ele removeria se fosse refratora o livro.
 
## Builder

### Intenção oficial

**Separar a construção de um objeto complexo de sua representação**, de modo que o mesmo processo de construção possa criar diferentes representações

### Visão geral

- O padrão sugere a separação do código que cria, e o código que usa o objeto.

- Trata da criação de objetos complexos (complexos de verdade).
	1. Construtores muito complexos.
	2. Composição de vários objetos (composite).
	3. Algoritmo de criação do objeto complexo.

- Permite a criação de um objeto em etapas.

- Permite method chaining.

- O objeto final pode variar de acordo com a necessidade.

- É um padrão complexo.

### Diagrama

![[Builder.png]]

```ts

// O Builder serve para usar em objetos complexos!!
// Esse tipo de código não é para usar Builder. É só um exemplo!

export class Person {
	constructor(public name?: string, public age?: number) {}
}

export class PersonBuilder {
	private person = new Person();
	
	newPerson(): void {
		this.person = new Person();
	}
	
	setName(name: string): this {
		this.person.name = name;
		return this;
	}
	
	setAge(age: number): this {
		this.person.age = age;
		return this;
	}
	
	getResult(): Person {
		return this.person;
	}
}

const personBuilder = new PersonBuilder();

const person1 = personBuilder
	.setName('Luiz')
	.setAge(30)
	.getResult();
personBuilder.newPerson();

const person2 = personBuilder
	.setName('Maria')
	.setAge(50)
	.getResult()

```

### Vantagens

- Separa criação de utilização;

- O cliente não precisa criar objetos diretamente;

- O mesmo código pode construir objetos diferentes;

- Ajuda na aplicação princípios SRP e OCP (S.O.L.I.D).

### Desvantagens

- O código final se tornar muito complexos.

## Prototype

### Intenção oficial

**Especificar os tipos de objetos a serem criados usando uma instância prototípica e criar novos objetos copiando este protótipo;**

- JavaScript é uma linguagem baseada em prototypes.

- Objetos estão diretamente ligados a outros objetos.

- Você pode literalmente fazer um objeto "herdar" de outro.

- A "herança" é obtida via __delegação__ (um objeto delega algo para seu protótipo).

- Uma das maneiras mais simples para manipular o protótipo de um objeto é usando: ``Object.create(prototypeObject)``;

- Também temos o costume de usar classes ou funções construtoras para manipulação de protótipos (isso faz com que JS/TS pareçam estar usando o padrão orientado a objetos clássico)

### Visão geral

- O tipo de objeto a ser criado é determinado pelo objeto protótipo;

- É tipicamente usado para evitar a recriação de objetos "caros";

- Ajudar evitar a explosão de subclasses;

- Pode (ou não) manter um registro de objetos protótipo em um objeto separado;

- Geralmente é criado apenas com um método "clone" dentrp do objeto protótipo;

- O método clone pode gerar uma "shallow" ou "deep" copy do objeto protótipo;

- Evita que o cliente conheça as classes que criam objetos.

### Diagrama 

![[Prototype.png]]

```ts
interface Prototype {
	clone(): Prototype;
}

class Person implements Prototype {
	constructor(public name: string, public age: number) {}

	clone(): this {
		// Isso não é um clone!
		// Estamos apenas criando um novo objeto
		// que tem este objeto como protótipo
		const newPerson = Object.create(this);
		return newPerson;
	}
}

const person1 = new Person('Luiz', 30);
const person2 = person1.clone();

console.log(person1.name); // Luiz
console.log(person2.name); // Luiz
```

### Aplicabilidade

- Use o padrão quando que seu código *não dependa de classes concretas para a criação de novos códigos;*

- Use o padrão quando *quiser evitar explosão de subclasses para objetos muito similares;*

- Use o padrão para *evitar a recriação de objetos "caros".*

### Vantagens

- Oculta classes concretas do código cliente;

- Ajuda na criação de objetos caros ou complexos;

- Evita a explosão de subclasses.

### Desvantagens

- Clonar objetos que tem referências para outros objetos pode ser super complexo.

## Factory Method

### Intenção oficial

**Definir uma interface para criar um objeto, mas deixar as subclasses decidirem que classe instanciar.** O Factory Method permite adiar a instanciação para as subclasses

- Factory (Fábricas) - são simplesmente operações que cria, objetos.

### Diagrama

![[Factory-Method.png]]

```ts
type Car = { model: string; engine: string };
type CarPrototype = { showDetails(): void };

const carPrototype: CarPrototype = {
	showDetails(): void {
	console.log(this);
	},
};

const carFactory = (model: string, engine: string): Car & carPrototype => {
	// declara id aleatório de 1 a 1000
	const idAsPrivateMember = Math.floor(Math.random() * 1000 );
	// coloca "carPrototype" no prototype de "carFactory" 
	const carObj = Object.create(carPrototype);
	// retorna um objeto que uni o "carObj" com o "id", "model" e "engine"
	return Object.assign(carObj, { id: idAsAPrivateMember, model, engine });
};

const car1 = carFactory('Fusca', 'V8');
car1.showDetails(); // { id: 930, model: 'Fusca', engine: 'V8'}
const car2 = carFactory('Celta', 'ABDD1233');
car2.showDetails(); // { id: 672, model: 'Celta', engine: 'ABDD1233'}

```

### Vantagens

- Lida com a criação de objetos;

- Oculta a lógica de instancia do código cliente.

- É obtido através de herança. 

- Permite a criação de novas factories sem a necessidade de alterar código já escrito (OCP);

- Pode usar parâmetros para determinar o tipo dos objetos a serem criados ou os parâmetros enviados aos objetos sendo criados.

- Outro exemplo:

```ts
interface Product {
	sayHi(): void;
}

class ConcreteProduct implements Product {
	sayHi(): void {
		console.log('Hi')
	}
}


abstract class Creator {
	abstract factoryMethod(): Product;
	
	createAndShow(): void {
		const product = this.factoryMethod();
		console.log(product);
	}
}

class ConcreteCreator extends Creator {
	factoryMethod(): Product {
		return new ConcreteProduct();
	}
}

const creator = new ConcreteCreator();
const product = creator.factoryMethod();
product.sayHi(); // Hi
create.createAndShow(); // ConcreteProduct{}

```

### Desvantagens

- Se usado sem necessidade, pode causar uma explosão de subclasses. Será necessário uma classe ``ConcreteCreator`` para cada ``ConcreteProduct``

### Aplicabilidade

__Use o Factory method:__

1. _Quando não souber com certeza_ quais os tipos de objetos o seu código vai precisar;

2. Para _permitir a extensão de suas factories_ para criação de novos objetos (isso ajuda a aplicar o Open/Closed Principle);

3. Para _desaclopar o código que cria o código_ que usa as classes (Single Responsibility Principle);

4. Dar um hook (gancho) às subclasses para _permitir que elas decidam a lógica de criação de objetos._


## Abstract Factory

### Intenção oficial

**Fornecer uma interface para criação de famílias de objetos relacionados ou dependentes sem especificar suas classes concretas.**

No exemplo abaixo o botão pode ser criado de dois tipos para linux e para windows, porem tanto um quanto o outro tem singularidades. Assim devemos criar uma classe que abrange um maior tipo de variedade. criando o ``UIElementFactory`` eu consigo especificar com precisão para que tipo de botão eu preciso naquele momento:

### Diagrama

![[Abstract-Factory-Example-0.png]]

```ts
// interface de botão genérica
interface Button {
	name: string;
	submit?: boolean
}

// interface para criar o botão
interface UIElementFactory {
	createButton(
		nameButton: string, 
		submit?: boolean,
	): Button;
}

// classe que implementa um botão para windows
class ButtonWindows implements Button {
	// defino um valor padrão para o submit
	submit?: boolean | undefined = false;
	
	constructor(public name: string) {}
	
	status(): void {
		console.log(
			`text: ${this.name} / submit: ${this.submit}`
		)
	}
}

// classe que implementa um botão para linux
class ButtonLinux implements Button {
	constructor(
		public name: string,
		public submit: boolean
	) {}

	status(): void {
		console.log(
			`text: ${this.name} / submit: ${this.submit}`
		)
	}
}

// nessa classe há uma divisão de elementos para windows
class UIElementFactoryWindows implements UIElementFactory {
	createButton(windowsNameButton: string): Button {
		return new ButtonWindows(WindowsNameButton);
	};
}
// nessa classe há uma divisão de elementos para linux
class UIElementFactoryLinux implements UIElementFactory {
	createButton(
		linuxNameButton: string, 
		submit: boolean
	): Button {
		return new ButtonLinux(linuxNameButton, submit);
	};
}

const windowsButton = new UIElementFactoryWindows();
const linuxButton = new UIElementFactoryLinux();

windowsButton.createButton('submit');
linuxButton.createButton('submit', true);

button1.status(); // text: submit / submit status: false
button2.status(); // text: submit / submit status: true
```

### Aplicabilidade

__Use o Abstract Factory quando:__

1. Um _sistema deve ser independente_ de como seus produtos são criados, compostos ou representados;

2. Um sistema deve ser configurado com uma família _produtos que podem (ou não) trabalhar juntos_;

3. Uma família de objetos for projetada para ser usada em _conjunto e você necessita garantir essa restrição_;

4. Você _quer fornecer uma biblioteca de classes de produtos_ e _quer revelar somente suas interfaces_, não suas implementações.

### Vantagens


- Lida com criação de objetos;

- É uma fábrica, assim como o Factory Method e geralmente _é composto por múltiplos Factory Methods_;

- Visa _agrupar famílias de produtos compatíveis_ criando uma fábrica concreta por grupo de objetos compatíveis;

- _Separa o código que cria do código_ que usa os objetos (SRP)

- Permite _fácil implementação de novas familías de objetos_ (OCP);

- Toda a programação fica _focada nas interfaces_ e não em implementações.

### Desvantagens

- Muitas classes e maior complexidade será introduzida no código.

# Padrões de projeto estruturais (structural)

Os padrões estruturais (structural) se preocupam com a forma como os objetos são compostos para formar estruturas maiores.

## Padrões e intenções

Os padrões de projeto estruturais originais da GoF são:

- ***Adapter*** - **converte a interface de uma classe em outra interface esperada pelos clientes.** O Adapter permite que certas classes trabalhem em conjunto, pois de outra forma seria impossível por causa de suas interfaces incompatíveis.
    
- ***Bridge*** - **separa uma abstração da sua implementação**, de modo que as duas possam variar independentemente.
    
- ***Composite*** - **compor objetos em estruturas de árvore para representarem hierarquias partes/todo.** Composite permite aos cliente tratarem de maneira uniforme objetos individuais e composições de objetos.
    
- ***Decorator*** - atribui responsabilidades adicionais a um objeto dinamicamente. Os Decorators **fornecem uma alternativa flexível à subclasses para extensão da funcionalidade.**
    
- ***Façade*** - **fornece uma interface unifica para um conjunto de interfaces em um subsistema.** O Façade define uma interface de nível mais alto que torna o subsistema mais fácil de usar.
    
- ***Flyweight*** - **usa compartilhamento para suportar grandes quantidades de objetos de granularidade fina**, de maneira eficiente.
    
- ***Proxy*** - fornece um objeto representante (surrogate), ou **um marcador de outro objeto para controlar o acesso ao mesmo.**

## Composite

### Intenção oficial

Compor objetos em estruturas de árvore para representar hierarquias partes/todo. ``Composite`` permite aos clientes tratarem de maneira uniforme objetos.

### Visão geral
- Faz mais sentido em estruturas que podem ser tratadas hierarquicamente (como árvores)

- Pode se uma solução para estruturas complexas que podem ser tratadas de maneira uniforme.

- Prioriza composição ao invés de herança

- Exemplo: em um grupo de produtos queremos saber o total do valor, devemos pegar um produto dentro daquele grupo de produtos e multiplicar com quantos produtos existem naquele grupo para contabilizar o total.

### Diagrama 

![[Composite.png]]

**Component (Raiz):**
```ts
export abstract class ProductComponent {
	abstract getPrice(): number;
	add(product: ProductComponent): void {}
	remove(product: ProductComponent): void {}
}
```

**Composite:**
```ts
export class ProductComposite extends ProductComponent {
	private children: ProductComponent[] = [];

	// método para adicionar produtos em lista
	add(...products: ProductComponent[]): void {	
		products.forEach(
			(product) => this.children.push(product)
		);
	}

	// método para remover produtos por index
	remove(product: ProductComponent): void {
		const productIndex = this.children.indexOf(product);
		if (productIndex !== -1) {
			this.children.splice(productIndex, 1);
		} 
	}

	// método para mostrar uma soma de todos os elementos
	getPrice(): number {
		return this.children.reduce(
			(sum, child) => sum + child.getPrice(), 0
		);
	}
}
```

**Leaf (folha):**
```ts
export class ProductLeaf extends ProductComponent {
	constructor(public name: string, public price: number) {
		super();
	}
	
	getPrice(): number {
		return this.price;
	}

}
```

```ts
// Client-code
const pen = new ProductLeaf('pen', 1);
const smartphone = new ProductLeaf('smartphone', 1_000);
const tshirt = new ProductLeaf('tshirt', 40);

const productBox = new ProductComposite();
productBox.add(pen, smartphone, tshirt);

console.log(productBox);
console.log(productBox.getPrice());
```

**Retorno:**
```shell
ProductComposite {
  children: [
    ProductLeaf { name: 'pen', price: 1 },
    ProductLeaf { name: 'smartphone', price: 1000 },
    ProductLeaf { name: 'tshirt', price: 40 }
  ]
}

1041
```
### Aplicabilidade

**Use o padrão Composite quando:**

- sua estrutura de objetos possa ser representada hierarquicamente, como por exemplo, estrutura tipo árvore.

- você quiser que o código cliente trate objetos compostos e objetos simples da mesma maneira.

### Vantagens

- É muito fácil criar objetos complexos por composição;

- É fácil gerar um hierarquia de objetos;

- É fácil usar polimorfismo e recursão;

- É fácil adicionar novos tipos de elementos na estrutura (OCP).

### Desvantagens

- Dependendo da estrutura, pode quebrar o princípio da segregação de interface (ISP). Objetos do tipo "Leaf" (folha) tendem a ter métodos que usam ou não fazem nada.

## Adapter

### Intenção oficial

***Converter a interface de uma classe em outra interface esperada pelos clientes*. O adapter permite que certas classes trabalhem em conjunto, pois de outra forma seria impossível por causa de suas interfaces incompatíveis.

### Visão geral
- É um padrão da categoria estrutural (strutural);

- Faz exatamente o que um adaptador da vida real faz (pense em um adaptador de tomados de um formato para outro);

- É muito usado para definir limites dentro de camadas da aplicação;

- Também pode ser usado para adaptar interface de códigos legado para um novo código;

- Exemplo uma classe que só válida Email e que para isso ela usa `isEmail` de uma biblioteca externa como `validator`

### Diagrama

![[Adapter-Class.png]]

```ts
// EmailValidatorProtocol
export interface EmailValidatorProtocol {
	isEmail: EmailValidatorFnProtocol;
}

export interface EmailValidatorFnProtocol {
	(value: string): boolean;
}

// EmailValidatorClassAdapter
import isEmail from 'validator/lib/isEmail';
import { EmailValidatorProtocol } from './email-validator-protocol';

// CLASSE ADAPTER - classe usada para adaptar a blibioteca "validator"
export class EmailValidatorClassAdapter implements EmailValidatorProtocol {
	isEmail(value: string): boolean {
		return isEmail(value);
	}
}

// função para validar de fato o email
function validaEmailClass(
	emailValidator: EmailValidatorProtocol,
	email: string,
): void {
	if (emailValidator.isEmail(email)) {
		console.log('Email é válido');
	} else {
		console.log('Email é inválido');
	}
}

validaEmailClass(
	new EmailValidatorClassAdapter(),     
	'nicolas.gandolfi11@gmail.com'
); 
// Email é válido
```

### Aplicabilidade

__Use o padrão Adapter quando:__

1. Você não quiser que seu código dependa diretamente de código de terceiros ou legado;


2. você quiser usar uma classe existente mas sua interface for incompatível com a interface que seu código ou domínio precisam

3. você quiser reutilizar várias subclasses que não possuam determinada funcionalidade mas for impraticável estender o código de cada uma apenas para adicionar a funcionalidade desejada (o Decorator também faz isso)

### Vantagens

- Desacopla o código da aplicação de códigos de terceiros;

- Aplica o SRP ao separar a conversão de interfaces da lógica da aplicação;

- Aplica o OCP ao permitir introduzir novos Adapters para código existente.

### Desvantagens

- Aumenta a complexidade da aplicação (Por outro lado, qual outra solução deveria ser aplicada?).

## Bridge

### Intenção oficial

Bridge é um padrão de projeto estrutural que tem a intenção de **desaclopar uma *abstração* da sua *implementação*, de modo que  as duas possam variar e evoluir independentemente**

> ***Abstração*** - É um código de alto nível que geralmente delega ações para outro objeto.

> ***Implementação*** - É um código que realmente faz o trabalho. geralmente uma classe que estende uma abstração

### Diferenças entre Bridge e Adapter

- (GOF pág. 208) A diferença chave entre esses padrões está nas suas intenções... O padrão Adapter faz as coisas funcionarem APÓS elas terem sido projetadas; o Bridge as faz funcionar ANTES QUE existam...

### Diagrama

![[bridge.png]]

- Device Implementation:
```ts
// interface de Protocolo padrão 
export interface DeviceImplementation {
	setVolume(volume: number): void;
	getVolume(): number;
}
```

- Remote Control:

```ts
// classe do controle remoto aonde o construtor é "DeviceImplementation"
export class RemoteControl {
	constructor(protected device: DeviceImplementation) {}
}
```

- Remote Control com volume:

```ts
// a mesma coisa do "RemoteControl" porem com metodos adcionais como "volumeUp" e "volumeDown"
export class RemoteControlWithVolume extends RemoteControl {
	volumeUp(): void {
		const oldVolume = this.device.getVolume();
		this.device.setVolume(this.device.getVolume() + 10);
		
		console.log(`
			${this.device.getName()} tinha o volume 
			${oldVolume} agora tem 
			${this.device.getVolume()}
		`);
	
	}

	volumeDown(): void {
		const oldVolume = this.device.getVolume();
		this.device.setVolume(this.device.getVolume() - 10);
		
		console.log(`
			${this.device.getName()} tinha o volume 
			${oldVolume} agora tem 
			${this.device.getVolume()}
			`);
	}
}
```

- Devices (dispositivos):

```ts
// o dispositivo "Radio" 
export class Radio implements DeviceImplementation {
	private volume = 10;
	
	setVolume(volume: number): void {
		if (volume < 0 || volume > 100) return;
		this.volume = volume;
	}
	
	getVolume(): number {
		return this.volume;
	}
}
```

```ts
// o dispositivo "Tv" 
export class Tv implements DeviceImplementation {
	private volume = 10;
	private power = false;
	
	setVolume(volume: number): void {
		if (volume < 0 || volume > 100) return;
		this.volume = volume;
	}
	
	getVolume(): number {
		return this.volume;
	}
}
```

- Client code:
```ts
export function clientCode(
  abstraction: RemoteControl | RemoteControlWithVolume,
): void {
	abstraction.togglePower(); // true
	
	if (!('volumeUp' in abstraction)) return;
	abstraction.volumeUp(); // 20
	abstraction.volumeUp(); // 30
	abstraction.volumeDown(); // 20
}

const tv = new Tv();
const radio = new Radio();
const radioRemoteControl = new RemoteControl(radio);
clientCode(radioRemoteControl);
const tvRemoteControl = new RemoteControlWithVolume(tv);
clientCode(tvRemoteControl);
```

- Retorno:
```powershell
Radio power status: true
Radio tinha o volume 10 agora tem 20
Radio tinha o volume 20 agora tem 30
Radio tinha o volume 30 agora tem 40
```
### Aplicabilidade

__Use o padrão Bridge quando:__

1. Você souber que sua estrutura terá abstrações(código de alto nível) e implementações dessa abstração (detalhes que possam variar de maneira independente);

2. você souber que o Adapter poderia ser aplicado naquela estrutura (você já conhece a estrutura);

3. Você quiser dividir uma classe que possa ter diversas variantes (como em produtos e suas variações de cores ``CanetaAzul``, ``CanetaVermelha``, ``CamisaAzul``, ``CamisetaVermelha``, etc....);

4. você quer trocar as implementações em tempo de execução.

### Vantagens

- Desacopla o código da abstração de códigos da implementação (SRP);

- Implementa o OCP ao permitir novas abstrações e/ou implementações para código existente;

- Tem as mesmas vantagens do Adapter.

### Desvantagens

- Aumenta a complexidade da aplicação quando implementado em locais incorretos.

## Decorators

### Intenção oficial

Agregar responsabilidades adicionais a um objeto dinamicamente. Os Decorators **fornecem uma alternativa flexível ao uso de subclasses para extensão de funcionalidades.**

### Visão geral

- Usa a composição ao invés da herança (sempre prefira composição ao invés de herança)

- É muito parecido com o "Composite" porém tem a intenção diferente;

- É usado para adicionar funcionalidades a objetos em tempo de execução;

- Finge ser o objeto sendo decorado, porém repassa chamadas dos métodos do objeto decorado;

- Pode executar ações antes e depois das chamadas dos métodos do objeto decorado;

- Pode manipular dados antes do retorno.

### Diagrama

![[Decorator.png]]

```ts
// Interface
export interface ProductProtocol {
	getPrice(): number;
	getName(): string;
}


// TShirt (Camiseta)
export class TShirt implements ProductProtocol {
	private name = 'Camiseta';	
	private price = 49.9;
	
	getPrice(): number {
		return this.price;
	}
	
	getName(): string {
		return this.name;
	}
}

// Decorator
export class ProductDecorator implements ProductProtocol {
	constructor(protected product: ProductProtocol) {}
	
	getPrice(): number {
		return this.product.getPrice();
	}
	
	getName(): string {
		return this.product.getName();
	}
}

// Decorator de estampas
export class ProductStampDecorator 
	extends ProductDecorator {
	
	getPrice(): number {
	// com decorator posso usar o preço original mais 10 reais de estampa
		return this.product.getPrice() + 10;
	}
	
	getName(): string {
		return this.product.getName() + ' (Estampada)';
	}

}
// main

const tShirt = new TShirt();
const tShirtWithStamp = new ProductStampDecorator(tShirt);

console.log(tShirt.getPrice(), tShirt.getName());
console.log(
		tShirtWithStamp.getPrice(), 
		tShirtWithStamp.getName()
	);
```

- Retorno:
```powershell
49.9 Camiseta
59.9 Camiseta (Estampada)
```

### Aplicabilidade

__Use o padrão Decorator quando:__

1. você precisa adicionar funcionalidades em objetos sem quebrar ou alterar o código existente

2. você quiser usar composição ao invés de herança

3. você percebe que pode ocorrer uma explosão de subclasses em determinada estrutura



### Vantagens

- Composição sempre é melhor que herança e, grande maioria dos casos

- É fácil adicionar ou remover comportamento de objeto sem tocar em código (OCP);

- É possivel decorar um objeto já decorado, adicionando ainda mais funcionalidades (camada)

### Desvantagens

- Quanto mais decorators em camadas, mais complexo seu código se torna

## Façade (Fachada)

### Intenção oficial

Façade (Fachada) é um padrão de projeto estrutural que **tem a intenção de fornecer uma interface unificada para um conjunto de interfaces em um subsistema.** Façade define uma interface de nível mais alto torna o subsistema mais fácil de ser usado

### Visão geral

- O Façade é o padrão mais simples de todos;

- Ele tem a intenção de facilitar a vida do código cliente ao criar um objeto de fachada para um sistema mais complexo;

- Instanciar vários métodos ou executar algoritmos apenas para todo esse código;

- Ele visa fornecer uma interface muito mais simples e unificada em um objeto que o cliente pode simplesmente chamar métodos e obter o comportamento desejado.

### Diagrama

![[Façade.png]]

```ts
// Façade
export class BuilderFacade {
	// Essa é a fachada para o projeto "BUILDER"
	private mainDishBuilder = new MainDishBuilder();
	private veganDishBuilder = new VeganDishBuilder();
	
	makeMeal1(): void {
		this.mainDishBuilder.makeMeal().makeDessert();
		
		console.log(this.mainDishBuilder.getMeal());
		console.log('Total: ', this
			.mainDishBuilder
			.getPrice());
	}
	
	makeMeal2(): void {
		this.mainDishBuilder.reset();
		
		const meal2 = this.mainDishBuilder
			.makeBeverage()
			.getMeal();
			
		console.log(meal2);
	}

	makeMeal3(): void {
		const veganMeal = this.veganDishBuilder
			.makeMeal()
			.getMeal();
			
		console.log(veganMeal);
		console.log('Total: ', veganMeal.getPrice());
	}
}

// client code (código cliente)

const builderFacade = new BuilderFacade();

builderFacade.makeMeal1();
builderFacade.makeMeal2();
builderFacade.makeMeal3();
```

- Retorno:
```powershell
MealBox {
  _children: [
    Rice { name: 'Arroz', price: 5 },
    Beans { name: 'Feijão', price: 10 },
    Meat { name: 'Carne', price: 20 },
    Dessert { name: 'Bebida', price: 7 }
  ]
}
42
MealBox { _children: [ Beverage { name: 'Bebida', price: 7 } ] }
MealBox {
  _children: [
    Rice { name: 'Arroz', price: 5 },
    Beans { name: 'Feijão', price: 10 }
  ]
}
15
```

### Aplicabilidade

__Use o padrão  Façade quando:__

1. Você quer disponibilizar um interface mais simples para um sistema complexo.

2. você quer criar pontos de entrada para determinadas partes do sistema, como determinadas partes do código.  

### Vantagens

- Simplifica o código complexo do código cliente;

- Facilita o uso do sistema;

- Cria pontos de entrada para camadas da aplicação e serviços de terceiros.

### Desvantagens

- O objeto façade se torna facilmente uma "God class" (use fachadas adicionais se perceber que isso está ocorrendo no seu código)


## Proxy

### Intenção oficial

Proxy é um padrão de projeto que tem a intenção de **fornecer um substituto ou marcador de localização para outro objeto para controlar o acesso a esse objeto.**

### Visão geral

- Usa composição, portanto tem a estrutura muito semelhante ao "Composite" e "Decorator" (as intenções são completamente diferentes);

- Usa um objeto "proxy" que finge ser o objeto real;

- É usado para controle de acesso, logs, cache, lazy instantiation e lazy evaluation distribuição de serviços e mais;

- Pode escolher como e quando repassar chamadas de métodos do objeto real;

- Tem várias variações: proxy virtual, proxy remoto, proxy de proteção, proxy inteligente...

#### Variações de proxy

1. **Proxy Virtual**: controla acesso a recursos que podem ser caros para criação ou utilização;

2. **Proxy Remoto**: controla acesso a recursos que estão em servidores remotos;

3. **Proxy de Proteção**: controla acesso a recursos que possam necessitar autenticação ou permissão;

4.  **Proxy Inteligente**: além de controlar acesso ao objeto real, também executa tarefas adicionais para saber quando executar determinadas ações;

### Diagrama

![[Proxy.png]]

```ts
export interface Subject {
	request(): void;
}

export classs RealSubject implements Subject {
	request(): void {
		console.log('Algo que meu objeot faz.')
	}
}

export class Proxy implements Subject {
	constructor(private subject: Subject) {}

	request(): void {
		console.log('Meu proxy faz algo.');
		this.subject.request(); // Chamada do objeto real
		console.log('Meu proxy pode fazer outra coisa.');
	}
}
```

### Aplicabilidade

__Use o padrão Proxy quando:__

1. Você tem um objeto caro para ser criado e não quer permitir acesso direto a esse objeto (proxy virtual);

2. você quer restringir acesso a partes da sua aplicação (proxy de proteção);

3. você quer um ligação entre seu sistema e um sistema remoto (proxy remoto);

4. você quer fazer cache de chamadas já realizadas (proxy inteligente ou proxy de cache);

5. você quer interceptar quaisquer chamadas de métodos no objeto real por qualquer motivo (por exemplo, criar logs)

### Vantagens

- O código cliente nem precisa saber se está ou não usando um Proxy (ele finge ser o objeto real);

- Você pode adicionar novos Proxies sem mudar código já testado (OCP)

- O Proxy funciona mesmo se o objeto real não estiver operacional ou pronto para uso;
- Você pode controlar o ciclo de vida de objeto reais dentro do proxy

### Desvantagens

- Introduz mais classes ao sistemas isso torna mais complexo.

## Flyweight

### Intenção oficial

Flyweight é um padrão de projeto estrutural que tem a intenção de **usar compartilhamento para suportar eficientemente grandes quantidades de objetos de forma granular**

### Visão geral

- É um padrão de otimização (cuidado)

- Visa economizar memória RAM devido ao grande número de objetos na aplicação

- Resolve o problema de desempenho dividindo o estado de um objeto em "intrínseco" e "extrínseco":
	1. **Estado intrínseco** é um estado que geralmente *não muda ou que muda muito pouco*
	2. **Estado extrínseco** é um estado que *pode ser movido para fora do objeto por mudar frequentemente*

- Só deve ser usado se sua aplicação estiver com problemas de alto consumo de memória RAM.

### Diagrama

![[Flyweight.png]]

```ts
export class DeliveryLocation implements DeliveryLocation {
	constructor(private readonly intrinsicState: DeliveryLocationData) {}

	deliver(nome: string, number: string): void {

		console.log('Entrega para %s', nome);
		console.log('Em', 
			this.intrinsicState.street, 
			this.intrinsicState.city
		);
		console.log('Número:', number);
		console.log('###');
	}

}
```

```ts
export class DeliveryFactory {
	private locations: DeliveryLocationDictionary = {};
	
	// Metodo para criar uma key de objeto com o nome dado no construtor
	private createId(data: DeliveryLocationData): string {
		return Object.values(data)
		  .map((item) => 
		  item.replace(/\s+/, '')
		  .toLocaleLowerCase()
		  .join('_');
	} 
	
	makeLocation(intrinsicState: DeliveryLocationData): 
	DeliveryFlyweight {
		const key = this.createId(intrinsicState);
		if (key in this.locations) return 
		this.locations[key];
		this.locations[key] = 
		new DeliveryLocation(intrinsicState);
		
		return this.locations[key];

  }
  
	getLocations(): DeliveryLocationDictionary {
		return this.locations;
	}
}
```

```ts
const factory = new DeliveryFactory();
deliveryContext(factory, 'Luiz', '20A', 'Av Brasil', 'SP');
deliveryContext(factory, 'Helena', '502', 'Av Brasil', 'SP');
deliveryContext(factory, 'Joana', '2', 'Rua A', 'BH');
deliveryContext(factory, 'João', '501', 'Rua B', 'RJ');
console.log();
console.log(factory.getLocations());
```

- Retorno:
```powershell
Entrega para Luiz
Em Av Brasil SP
Número: 20A
###
Entrega para Helena
Em Av Brasil SP
Número: 502
###
Entrega para Joana
Em Rua A BH
Número: 2
###
Entrega para João
Em Rua B RJ
Número: 501
###

{
  avbrasil_sp: DeliveryLocation {
    intrinsicState: { street: 'Av Brasil', city: 'SP' }
  },
  ruaa_bh: DeliveryLocation { intrinsicState: { street: 'Rua A', city: 'BH' } },
  ruab_rj: DeliveryLocation { intrinsicState: { street: 'Rua B', city: 'RJ' } }
}
```

### Aplicabilidade

__Só use o Flyweight se TODAS as condições a seguir forem verdadeiras:__

1. Sua aplicação utiliza um grande quantidade de objetos;

2. os custos de armazenamento são altos por causa da grande quantidade de objetos;

3. a maioria dos estados de objetos podem se tornar extrínsecos;

4. muitos objetos podem ser substituídos por poucos objetos compartilhados;

5. a aplicação não depende da identidade dos objetos.

### Vantagens

- Pode economizar memória RAM.

### Desvantagens

- Muito complexo.

# Padrões de projeto comportamentais (behavioural)

Os padrões de projeto comportamentais se preocupam com os algoritmos e a atribuição de responsabilidades entre objetos. Os padrões comportamentais não descrevem apenas padrões de objetos ou classes, mas também os padrões de comunicação entre eles. Esses padrões caracterizam fluxos de controle difíceis de seguir em tempo de execução. Eles afastam o foco do fluxo de controle para permitir que você se concentre somente na maneira como os objetos são interconectados.

## Padrões e intenções

Os padrões de projeto comportamentais originais da GoF são:

- ***Chain of responsibility*** - evita o acoplamento do remetente de uma solicitação ao seu destinatário, dando a mais de um objeto a chance de tratar a solicitação. Encadeia os objetos receptores e passa a solicitação ao longo da cadeia até que um objeto a trate.
	
- ***Command*** - encapsula uma solicitação como um objeto, desta forma permitindo que você parametrize clientes com diferentes solicitações, enfileire ou registre (log) solicitações e suporte operações que podem ser desfeitas.
	
- ***Interpreter*** - dada uma linguagem, define um representação para sua gramática juntamente com um interpretador que usa a representação para interpretar sentenças nesta linguagem.
	
- ***Iterator*** - fornece uma maneira de acessar sequencialmente os elementos de um objeto agregado sem expor sua representação subjacente.
	
- ***Mediator*** - define um objeto que encapsula como um conjunto de objetos interage. O mediator promove o acoplamento fraco ao evitar que os objetos se refiram explicitamente uns aos outros, permitindo que você varie suas interações independentemente.
	
- ***Memento*** - sem violar a encapsulação, captura e externaliza um estado interno de um objeto, de modo que o mesmo possa posteriormente ser restaurado para este estado.
	
- ***Observer*** - define uma dependência um para muitos entre objetos, de modo que, quando um objeto muda de estado, todos os seus dependentes são automaticamente notificados e atualizados.
	
- ***State*** - permite que um objeto altere seu comportamento quando seu estado interno muda. O objeto parecerá ter mudado sua classe.
	
- ***Strategy*** - Define uma família de algoritmos, encapsular cada um deles e fazê-los intercambiáveis. O strategy permite que o algoritmo varie independentemente dos clientes que o utilizam.
	
- ***Template method*** - define o esqueleto de um algoritmo em uma operação, postergando a definição de alguns passos para subclasses. O template method permite que as subclasses redefinam certos passos de um algoritmo sem mudar sua estrutura.
	
- ***Visitor*** - representa uma operação a ser executada sobre os elementos da estrutura de um objeto. O visitor permite que você defina uma nova operação sem mudar as classes dos elementos sobre os quais opera.

## Strategy
### Intenção oficial

Definir uma família de algoritmos, encapsular cada um deles e fazê-los intercambiáveis. O strategy permite que o algoritmo varie independentemente dos clientes que utilizam. 

### Visão geral

- Separa a regra de negócio de variações de algoritmos que possam existir;

- Define uma família de algoritmos cada uma variação diferente;

- Usa composição para permitir a troca de algoritmos em tempo de execução;

- Permite a criação de vários algoritmos sem a necessidade de condicionais.

### Diagrama

![[Strategy.png]]

### Aplicabilidade

__Use o Strategy quando:__

1. Você tiver variantes de um mesmo algoritmo e precisa trocar esses algoritmos em tempo de execução;

2. você precisa isolar a regra de negócio do algoritmo que deve ser aplicado (aplicando o princípio de responsabilidade única)

3. você perceber que está usando condicionais apenas para trocar resultado final de um algoritmo

### Vantagens

- Troca herança por composição

- Separa a regra de negócio de algoritmos complexos

- Aplica os princípios do aberto/fechado e da responsabilidade única

### Desvantagens

- Pode ser complexo criar toda um hierarquia de classe para aplicar novos algoritmos;

- Você pode obter o mesmo resultado com funções caso a linguagem de programação permitir;

- O código cliente precisa conhecer as estratégias que vai usar;

## Command

### Intenção oficial

Encapsular uma solicitação como um objeto, desta forma permitindo que você parametrize clientes com diferentes solicitações, enfileire ou registre (log) solicitações e suporte operações que podem ser desfeitas

### Visão geral

- Transforma uma solicitação (um comando) em um objeto com toda a informação necessária para execução;

- É a versão orientada a objetos para funções de callback

- Permite que comandos possam ser enfileirados, armazenados ou desfeitos;

- Permite registro de alterações para que possam ser replicadas quando necessário;

- Permite que você crie comandos compostos;

- Desacopla o código do objeto que faz solicitação com o objeto que recebe a solicitação;

- Usa composição ao invés de herança. 

### Diagrama

![[Command.png]]

- [Exemplo](https://github.com/zNIKK/JS/blob/main/typescript/src/GoF/src/behavioral/command/smart-house-app.ts):
```ts
// SmartHouseApp
export class SmartHouseApp {
	// command = objeto que contêm uma chave personalizada pelo usuário
	private commands: { [k: string]: SmartHouseCommand } = {};

	// Para adicionar um novo command precisa de "key" e o "command"  
	addCommand(key: string, command: SmartHouseCommand): void {
		this.commands[key] = command;
	}
	
	executeCommand(key: string): void {
		this.commands[key].execute();
	}


	undoCommand(key: string): void {
		this.commands[key].undo();
	}
}
```

```ts
//Receiver
const bedroomLight = new SmartHouseLight('Luz Quarto');

// Command
// Classe para desligar e ligar a luz
const bedroomLightPowerCommand = new LightPowerCommand(bedroomLight);

// Classe para aumentar e diminuir a luz
const bedroomIntensityCommand = new LightIntensityCommand(bedroomLight);

// Controle - invoker
const smartHouseApp = new SmartHouseApp();
// adicionar o comando com o nome da key 'btn-1' e o comando "bedroomLightPowerCommand"
smartHouseApp.addCommand('btn-1', bedroomLightPowerCommand);
smartHouseApp.addCommand('btn-2', bedroomLightPowerCommand);

smartHouseApp.addCommand('btn-3', bedroomIntensityCommand);
smartHouseApp.addCommand('btn-4', bedroomIntensityCommand);

smartHouseApp.executeCommand('btn-1'); // True
smartHouseApp.undoCommand('btn-1'); // False

smartHouseApp.executeCommand('btn-3'); // +1
smartHouseApp.undoCommand('btn-4'); // -1

```

### Aplicabilidade

__Use o Command quando:__

1. você quer desacoplar objeto que envia a solicitação do objeto que a receberá

2. você quer tratar um comando como um objeto (com a possibilidade de armazenar, agendar, enfileirar, fazer log, agendar execuções, ou fazer qualquer coisa que pode ser feita com um objeto)

3. você quer permitir que solicitações possam ser feitas e desfeitas

### Vantagens

- Você pode criar comandos simples e complexos (ou até compostos de outro comandos);

- você pode implementar fazer e desfazer

- comandos são objetos normais, portanto podem fazer tudo que objetos normais fazem.

### Desvantagens

- Muitas classes podem tornar o sistema mais complexo.

## Memento

### Intenção oficial

Sem violar o encapsulamento, captura e externaliza um estado interno de um objeto, de modo que o mesmo possa posteriormente ser restaurado para este estado.

### Visão geral

- Praticamente todas as aplicações o implementam com a função "desfazer" (CTRL + Z);

- Desacopla a responsabilidade da classe originadora de tomar conta dos seus backups;

- Garante o encapsulamento e consistência nos backups.

### Diagrama

![[Memento.png]]

- [Exemplo](https://github.com/zNIKK/JS/blob/main/typescript/src/GoF/src/behavioral/memento/main.ts): 

```ts
const imageEditor = new ImageEditor('/media/image.jpg', 'jpg');

const backupManager = new ImageEditorBackupManager(imageEditor);

// salva um array de formatos que foram usados exemplo:
backupManager.backup();
// ['jpg']
// fileFormat: 'jpg'

// como o nome diz converte o formato para "gif"
imageEditor.convertFormatTo('gif');
backupManager.backup();
// ['jpg', 'gif']
// fileFormat: 'gif'
imageEditor.convertFormatTo('bmp');
backupManager.backup();
// ['jpg', 'gif', 'bmp']
// fileFormat: 'bmp'

console.log(imageEditor);
// tira o ultimo formato do array e usa o penultimo formato que foi feito o backup (como se fosse um CTRL + Z)
backupManager.undo();
// ['jpg', 'gif']
// fileFormat: 'gif'
console.log(imageEditor);
```

```powershell
ImageEditor { filePath: '/media/imagem.jpg', fileFormat: 'jpg' }
BACKUP: salvando o estado de ImageEditor
BACKUP: salvando o estado de ImageEditor
ImageEditor { filePath: '/media/image.bmp', fileFormat: 'bmp' }
BACKUP: 2023-08-15T23:15:57.671Z foi restaurado com sucesso.
ImageEditor { filePath: '/media/image.gif', fileFormat: 'gif' }
```
### Aplicabilidade

__Só use o Memento quando:__

1. você deseja ter a possibilidade de salvar e restaurar o estado atual de um objeto sem violar o encapsulamento;

2. você deseja implementar função "desfazer" no seu sistema;

3. você deseja fazer backups de estado de determinadas classes no seu sistema.

### Vantagens

- Desacopla a responsabilidade de tomar conta do backup da classe original;

- é fácil salvar e restaurar um backup de uma classe.

### Desvantagens

- quanto mais backups, maior o consumo de memória de sua aplicação;

- as classes zeladoras precisam acompanhar as mudanças nas classes originadoras;

- pode ser desafiador garantir o encapsulamento em algumas linguagens de programação.

## State

### Intenção oficial

Permite que um objeto altere seu comportamento quando seu estado interno muda. O objeto parecerá ter mudado sua classe

### Visão geral

- Evita condicionais quando contexto muda de comportamento dependendo do seu estado

- Desacopla o estado de um objeto contexto e seus métodos em objetos de estado separados

- Facilita a adição de novos estados sem a necessidade de alterar estados anteriores

### Diagrama

![[State_2.png]]

- [Exemplo:]
```ts
const order = new ShoppingOrder(); // Pendente
// States são como se fossem condicionais(if/else)
order.approvePayment(); // Aprovado
order.waitPayment(); // Pendente
order.shipOrder(); // enviar pedido (recusado)
order.rejectPayment(); // Rejeitado

// o pagamento já foi recusado
order.approvePayment(); // Recusado
order.waitPayment(); // Recusado
order.shipOrder(); // Recusado
```

- Retorno:

```
O estado do pedido agora é OrderApproved
O estado do pedido agora é OrderPending
Não posso enviar o pedido com pagamento pendente.
O estado do pedido agora é OrderRejected
Não posso aprovar o pagamento porque o pedido foi recusado.
Não posso mover para pendente porque o pedido foi recusado.
Não posso enviar um pedido com pagamento recusado.
```

### Aplicabilidade

__Use o State quando:__

1. O seu objeto pode se comportar de maneira diferente dependendo do seu estado atual

2. Você quer evitar o uso de condicionais que alteram o comportamento da classe de acordo com valores dos seus campos

### Vantagens

- Desacopla a lógica de um estado da classe de contexto

- permite a criação de novos estados apenas adicionais complexas da classe de contexto

### Desvantagens

- Se você tem apenas poucas condicionais simples, aplicar este padrão pode deixar o seu código mais complexo do que o necessário.

## Mediator

### Intenção oficial

Define um objeto que encapsula como um conjunto de objetos interage. O mediator promove o acoplamento fraco ao evitar que os objetos se refiram explicitamente uns aos outros, permitindo que você varie suas intenções

### Visão geral

- Você quer diminuir ou extinguir o acoplamento direto entre as classes que poderiam estar diretamente acopladas;

- você quer simplificar comunicações de muitos-para-muitos para comunicações de um-para-um.

### Diagrama

![[Mediator.png]]

- [Exemplo]:

```ts
// Objeto central que faz a comunicação entre o comprador e o vendedor
const mediator = new Mediator();
// Objeto vendedor 1
const seller1 = new Seller();
// o vendedor 1 adiciona um produto "Camiseta" na sua loja
seller1.addProduct({ id: '1', name: 'Camiseta', price: 49.9 });
// o vendedor 1 adiciona um produto "Caneta" na sua loja
seller1.addProduct({ id: '2', name: 'Caneta', price: 9.9 });

// Objeto vendedor 2
const seller2 = new Seller();

// o vendedor 2 adiciona um produto "Carro" na sua loja
seller2.addProduct({ id: '3', name: 'Carro', price: 49000.9 });
// o vendedor 2 adiciona um produto "Lápis" na sua loja
seller2.addProduct({ id: '4', name: 'Lápis', price: 1.9 });

// adicina no array os vendedores
mediator.addSeller(seller1, seller2);

// objeto comprador
const buyer = new Buyer(mediator);

// o buyer recebe as MESMAS funções do Mediador
buyer.viewProducts();

buyer.buy('2'); // compra o produto 2
buyer.buy('3'); // compra o produto 3

buyer.viewProducts();
```

- Retorno:

```
1 Camiseta 49.9
2 Caneta 9.9
3 Carro 49000.9
4 Lápis 1.9
Aqui está 2 Caneta 9.9
Aqui está 3 Carro 49000.9
1 Camiseta 49.9
4 Lápis 1.9
```

### Aplicabilidade

__Só use o Memento quando:__

1. O seu objeto pode se comportar de maneira diferente dependendo do seu estado atual

2. Você quer evitar o uso de condicionais que alteram o comportamento da classe de acordo com valores dos seus campos

### Vantagens

- Desacopla objetos que poderiam estar firmemente acoplados

- facilita a reutilização de objetos

- facilita a adição ne novos mediadores e classes participantes na comunicação

- encapsula a comunicação entre objetos

### Desvantagens

- É fácil criar um mediador "faz tudo" (god class)

## Chain of responsibility

### Intenção oficial

Evita o acoplamento do remetente de uma solicitação ao seu destinatário, dando a mais de um objeto a chance de tratar a solicitação. Encadeia os objetos receptores e passa a solicitação ao longo da cadeia até que um objeto a trate.

### Visão geral

- É usado quando uma requisição precisa passar por uma sequência de operações até ser totalmente tratada;

- Desacopla quem envia de quem vai tratar a requisição;

- É muito usado com requisições HTTP;

- É a base para outros padrões de projeto conhecidos (como Middleware usado no express);

- Permite que objeto TRATE a requisição e chame o PRÓXIMO objeto da cadeia;

- Permite que objeto NÃO TRATE a requisição e chame o PRÓXIMO objeto da cadeia;

- Permite que objeto TRATE a requisição e FINALIZE a cadeia;

- Permite que objeto NÃO TRATE a requisição e FINALIZE a cadeia;

- O cliente pode iniciar a requisição de qualquer objeto caso necessário.

### Diagrama

![[Chain of responsibility.png]]

- Exemplo:

```ts
// Orçamento inicial do criente é 1000
const customerBudget = new CustomerBudget(1001);

// trata o orçamento SE o orçamento for menor que 1000
const seller = new SellerBudgetHandler();

seller
	// trata o proximo orçamento SE o orçamento for maior que 5000
  .setNextHandler(new ManagerBudgetHandler())
  	// trata o proximo orçamento SE o orçamento for maior que 50000
  .setNextHandler(new DirectorBudgetHandler())
    // trata o proximo orçamento INDEPENDENTE do valor 
  .setNextHandler(new CEOBudgetHandler());

seller.handle(customerBudget);
```

- Retorno:

```
O diretor tratou o orçamento
```

### Aplicabilidade

__Só use o Chain of responsibility quando:__

1. Seu sistema precisa processar uma requisição em várias etapas diferentes e você não quer criar rígida para o processamento. O chain of responsability permite que você altere a ordem dos objetos na cadeia facilmente (mesmo assim, mantendo uma ordem específica).
2. você quer aplicar o princípio da responsabilidade única para tratamento de dados da requisição. Cada objeto fica responsável por tratar apenas a parte que lhe couber
3. você quer permitir que os objetos responsáveis pelo tratamento de requisição possam variar em tempo de execução

### Vantagens

- Aplica o princípio da responsabilidade única (SRP);

- Aplica o princípio do aberto e fechado (OCP);

- Permite que você altere a cadeia de objetos e a ordem das chamadas facilmente

### Desvantagens

- É comum uma requisição passar por toda a cadeia e não ser tratada

## Template Method

### Intenção oficial

Define o esqueleto de um algoritmo em um operação, postergando a definição de alguns passos para subclasses. O template method permite que as subclasses redefinam certos passos de um algoritmo sem mudar sua estrutura. 

### Visão geral

- Mantém a ordem de chamada de métodos no algoritmo;

- Evita a duplicação de código dentro da classe base;

- Substitui condicionais por polimorfismo;

- Permite a adição de hooks para que as subclasses utilizem em pontos estratégicos do algoritmo.

### Diagrama

![[Template-Method.png]]

- [Exemplo]:

```ts
export abstract class TemplateMethodBaseClass {
	// este é o Template method (final)
	readonly templateMethod = (): void => {
		this.stepA();
		this.hook();
		this.stepB();
	};

	abstract stepA(): void; // As classes concretas devem definir
	abstract stepB(): void; // As classes concretas devem definir
	hook(): void {}; // As classes concretas podem usar
}

export class ConcreteTemplateMethod extends TemplateMethodBaseClass {
	stepA(): void {
		console.log('A - stepA')
	}
	
	stepB(): void {
		console.log('A - stepB')
	}

	hook(): void {
		console.log('A - Hook used')
	}
}

const concrete = new ConcreteTemplateMethod();
concrete.templateMethod()
```

- Retorno:

```powershell
A - stepA
A - Hook used
A - stepB
```

### Aplicabilidade

__Só use o Template Method quando:__

1. Você precisa de variações de um mesmo algoritmo sem mudar a ordem de execução dos métodos

2. Você percebe que esta usando herança para alterar apenas pequenos trechos de código de um algoritmo 

### Vantagens

- Evita duplicação de código

- Permite fácil alteração de algoritmos

- Aplica o OCP e SRP

### Desvantagens

- em alguns casos pode violar o LSP ao alterar o comportamento de métodos nas subclasses

## Observer

### Intenção oficial

Define uma dependência um para muitos entre objetos, de modo que, quando um objeto muda de estado, todos os seus dependentes são automaticamente notificados e atualizados.

### Visão geral

- Implementado com dois tipos de objetos: objetos observáveis (Observable) e objetos observadores (Observer);

- Objetos observáveis (Observable) têm uma referência para todos os seus observadores.

- Isso torna possível adicionar, remover e notificar todos observadores quando seu estado muda

- Objetos observadores (Observer) devem ter meios de receber notificação de seus Observáveis. Geralmente isso é feito com apenas um método.

### Diagrama

![[Observer.png]]

- [Exemplo]:

```ts
// função que faz um input 
function makeInput(): HTMLInputElement {
	const input = document.createElement('input');
	document.body.appendChild(input);
	return input;
}

// função que faz um paragrafo 
function makeParagraph(): HTMLParagraphElement {
	const p = document.createElement('p');
	document.body.appendChild(p);
	p.innerText = 'Texto inicial (Hardcoded)';
	return p;
}

// Concrete Observer do input
const input = new InputObservable(makeInput());
// Concrete Observer do paragrafo
const p1 = new ParagraphObserver(makeParagraph());
const p2 = new ParagraphObserver(makeParagraph());

// coloca o input em uma rede de paragrafos aonde se o valor do input mudar o  paragrafo também muda 
input.subscribe(p1, p2);

input.element.addEventListener('keyup', function () {
  input.notify();
});
```

- Retorno:

```powershell
A - stepA
A - Hook used
A - stepB
```

### Aplicabilidade

__Só use o Observer quando:__

1. Você precisa notificar vários objetos sobre a mudança de estado de outro(s) objeto(s);

### Vantagens

- Usa o SRP e OCP

- Facilita a comunicação entre objetos em **tempo de execução**

> **tempo de execução** = no código cliente é possível fazer edições sem ter que editar a classe fonte

### Desvantagens

- Pode ser complexo ou impossível manter a ordem em que as notificações são enviadas.

## Iterator

### Intenção oficial

Fornece uma maneira de acessar sequencialmente os elementos de um objeto agregado sem expor sua representação subjacente

### Visão geral

- Desacopla a intenção principal do objeto do modo como a sua iteração é realizada (delega a iteração para outro objeto)

- Permite vários tipos de iterators, facilitando a implementação de novos modos de travessia na mesma coleção

- Encapsula os detalhes e monitora toda a travessia

- Permite que a coleção troque de iterador em **tempo de execução**

- Geralmente a linguagem de programação disponibiliza maneiras para trabalhar com iteradores


### Diagrama

![[Iterator.png]]

- [Exemplo]():

```ts
export class Counter {
	public current = 0;
	public last = 5;
	
	[Symbol.iterator](): CounterIteratorForward {
		return this.resetIterator();
	}
	
	resetIterator(): CounterIteratorForward {
		return new CounterIteratorForward(this)
	}
}

export class CounterItaratorForward {
	private current = this.counter.current;
	private last = this.counter.last;
	constructor(private counter: Counter) {}

	next(): { value: number; done: boolean } {
		return { value: ++this.current, done: this.current > this.last };
	}
}

const counter = new Counter();
const [one, two, ...rest] = [...counter];
console.log(one, two, rest); // 1 2 [3, 4, 5]
for (const count of counter) console.log(count) // 1 2 3 4 5
```

### Aplicabilidade

__Só use o Iterator quando:__

1. Você precisa remover a complexidade de travessia de dentro da coleção principal. Isso permite que sua coleção foque apenas em armazenar dados de maneira eficiente

2. Sua coleção pode ter vários modos de travessia, como crescente, decrescente, pelo menor número de saltos, pulando de dois em dois, ou como preferir

3. Você quer disponibilizar protocolos de travessia para diferentes tipos de coleções

### Vantagens

- É possível pausar a travessia e continuar posteriormente

- É possível atravessar várias vezes a mesma coleção em paralelo usando outro objeto iterador

- É fácil adicionar com algoritmos de travessia completamente diferentes

- Não polui o código do objeto principal com vários métodos e algoritmos de travessia diferentes

### Desvantagens

- Este padrão só é útil se sua coleção realmente precisar de um travessia complexa. Do contrário é apenas complexidade a mais.

## Visitor

### Intenção oficial

Representa uma operação a ser executada sobre os elementos da estrutura de um objeto. **O Visitor permite que você separe um algoritmo dos elementos sobre os quais opera.**

### Visão geral

- 

### Diagrama



- [Exemplo]():

```ts

```

### Aplicabilidade

__Só use o Visitor quando:__

1. Você precisa executar um algoritmo em todos os elementos de uma estrutura mais complexa (como uma estrutura criada com o padrão Composite)

2. Você quer separar uma lógica complexa em objetos auxiliares

### Vantagens

- Limpa o código da regra de negócio

- Separa algoritmos complexos em objetos auxiliares

- Aplica SRP e OCP

### Desvantagens

- Se um novo objeto for adicionado à estrutura, você precisará atualizar os objetos visitantes

- Objetos visitantes podem não ter acesso a todos os membros dos objetos em que operam