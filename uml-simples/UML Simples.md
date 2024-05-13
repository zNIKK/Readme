## Herança

Uma classe que herda de outra classe, ou seja um carro que é um filho de automóvel. Exemplo:

```js
export class Automoveis {}

export class Carro extends Automoveis {}
```

![[Pasted image 20230821213304.png]]

## Agregação e Composição

- A **Agregação** é um caso particular, indica que uma das classes do relacionamento é uma parte, ou **está contida** em outra classe. Ou seja o carro **precisa** da classe motor para funcionar.

```js
export class Carro {
	// Agregação
	private motor: Motor;
	constructor(motor: Motor) {
	this.motor = motor
	}
}

export class Motor {}

// Composição
const motor = new Motor();
const carro = new Carro(motor);
```

- Agregação:

![[Pasted image 20230821213424.png]]

- Composição:

![[Pasted image 20230821213500.png]]

- Uma classe que está contida na outra "vive" e constitui a outra. Se o objeto da classe que contém for destruído, as classes da agregação de composição serão destruídas juntamente, já que as mesmas fazem parte da outra.

## Dependência

- Uma **dependência** indica a ocorrência de um relacionamento _semântico_ entre dois ou mais elementos do modelo, onde uma classe cliente é dependente de alguns serviços da classe fornecedora, mas não tem uma dependência estrutural interna com esse fornecedor. 
- O escritor depende da caneta para escrever.
```js
export class Escritor {
	Escrever(caneta: Caneta): void {
		console.log(`Escrevendo com ${caneta}`)
	}
}

export class Caneta {}
```

![[Pasted image 20230821213601.png]]

## Realização

- Uma classe que implementa uma interface ou uma interface estendendo outra interface.

```js
export interface ControleRemoto {
	play(): void;
	pause(): void;
}
// interface estendendo uma interface
export interface ControleSom extends ControleRemoto {
	mudarRadio(): void
}
// uma classe implementando uma interface
export class Bluray implements ControleRemoto {
	pause(): void {}
	play(): void {}
}
// uma classe implementando uma interface aonde essa interface foi estendida
export class Som implements ControleSom {
	mudarRadio(): void {}
	pause(): void {}
	play(): void {}
}
```

![[Pasted image 20230821213809.png]]

## Abstratos

- **É um tipo de classe especial que não pode ser instanciada, apenas herdada**

- Sendo assim, uma classe abstrata não pode ter um objeto criado a partir de sua instanciação. Essas classes são muito importantes quando não queremos criar um objeto a partir de uma classe “geral”, apenas de suas “subclasses”.

```js
export abstract class Animal {
	protected abstract gerarBarulho(): string;

	gerarSom(): void {
		console.log(this.makeNoise());
	}
}

export class Dog extends Animal {
	protected makeNoise(): string {
		return 'AU AU'
	}
}

const dog = new Dog();
dog.makeSound();
```
retorno:
```
AU AU
```

![[Pasted image 20230821214159.png]]


-  A classe ``Animal`` tem uma função abstrata ``gerarBarulho`` , nesse mesmo animal tenho uma função para fazer o animal gerar um som (qualquer um que seja). Assim, eu defini que a classe ``Dog`` estende a classe animal aonde temos a função  ``gerarBarulho``, só que colocando um retorno para essa função no caso ``AU AU``.
