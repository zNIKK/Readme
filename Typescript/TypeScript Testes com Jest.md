
Este resumo abordará o uso do framework de testes Jest em conjunto com TypeScript. O Jest é uma ferramenta popular para testar código JavaScript e TypeScript, e é conhecido por sua simplicidade e facilidade de uso.

## Configuração inicial

Antes de começar a escrever testes, é necessário configurar um ambiente de teste com o Jest.

1. Instale o Jest e as dependências relacionadas em seu projeto:
```shell
npm install --save-dev jest ts-jest @types/jest
```

2. Configure o Jest criando um arquivo `jest.config.js` na raiz do seu projeto:

```json
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'node',
  moduleFileExtensions: ['ts', 'js'],
  transform: {
    '^.+\\.(ts|tsx)$': 'ts-jest',
  },
  testMatch: ['**/__tests__/**/*.+(ts|js)'],
};
```

3. Certifique-se de que seu arquivo `tsconfig.json` esteja configurado corretamente para o TypeScript.

4. Crie um arquivo para fazer teste. Exemplos 
	- ``index.test.ts``
	- ``index.spec.ts``

## Escrevendo testes básicos

Agora que a configuração está pronta, vamos começar a escrever nossos primeiros testes.

1. Crie um arquivo de teste com a extensão `.test.ts`. Por exemplo, `example.test.ts`.
    
2. Importe o módulo ou classe que deseja testar:
    
```ts
import { sum } from './example';
```
    
3. Escreva um teste utilizando a função `test` do Jest:
    
```ts
test('soma dois números corretamente', () => {   expect(sum(2, 3)).toBe(5); });
```

ou:

```ts
it('soma dois números corretamente', () => {   expect(sum(2, 3)).toBe(5); });
```

Neste exemplo, estamos testando a função `sum` para garantir que ela some corretamente dois números.

4. Execute os testes com o comando:

```shell
npx jest
```

O __Jest__ irá buscar e executar todos os arquivos de teste no diretório.

## O que SUT

- Geralmente quando queremos chamar a classe que está sendo testada usamos o termo __SUT__ (System Under Test).

```ts
const sut = new Classe();
```
## Utilizando Describe

Para cada tipo de test pode existir uma descrição geral de uma função, classe ou do que ela faz, contendo vários testes:

```ts
describe('Numeros', () => {
	it('soma dois números corretamente', () => {   
		expect(sum(2, 3)).toBe(5); 
	});
})
```

## Utilizando Matchers

Os matchers são funções que nos permitem realizar verificações em nossos testes. O Jest oferece uma variedade de matchers úteis para diferentes tipos de testes.

1. Igualdade: `toBe` verifica se dois valores são estritamente iguais.

```ts
it('dois mais dois é igual a quatro', () => {   
	expect(2 + 2).toBe(4); 
});
```

2. Verdadeiro/Falso: `toBeTruthy` verifica se um valor é verdadeiro.

```ts
test('verifica se um número é maior que zero', () => {   
	expect(10).toBeTruthy(); 
});
```

3. Comparação de arrays e objetos: `toEqual` verifica se dois arrays ou objetos são iguais em termos de valores.

```ts
test('verifica se dois objetos são iguais', () => {   
	const obj1 = { name: 'John', age: 25 };   
	const obj2 = { name: 'John', age: 25 };   
	expect(obj1).toEqual(obj2); 
});
```

4. E muitos outros matchers estão disponíveis no Jest.

```ts
it('should test jest assertions', () => {
    const number = 10;
    expect(number).toBeGreaterThan(9) // maior que 9
    expect(number).toBeGreaterThanOrEqual(9) // maior ou igual a 9
    expect(number).toBeLessThan(9) // menor que nove

    expect(number).toBeCloseTo(10.001) // esteja perto de 10
    expect(number).toBeCloseTo(9.996) // esteja perto de 10
  
    expect(number).not.toBeNull(); // não seja nulo

    expect(number).toHaveProperty('toString') // checar se existe a propriedade "toString" dentro de number
    expect(number).toHaveBeenCalledTimes(1) // checar quantas vezes o metodo foi chamado
  })
```

## Configurando mocks e stubs

__Mocks__ e __stubs__ são recursos úteis para testar unidades isoladas de código, especialmente quando há dependências externas.

- No teste abaixo, a SUT ``shoppingCart`` precisa da classe ``Discount`` pra funcionar, então criamos um __mock__:
```ts
import { Discount } from './discount';

describe('ShoppingCart' () => {
	// MOCKS = um bloco de codigo que serve para fingir uma dependência de uma classe
	it('should be a mock') {
		class DiscountMock extends Discount {}
		
		const sut  = new ShoppingCart(new DiscountMock());
	});
})
```

### Diferenças

Usamos o **mock** quando queremos saber se uma função vai ser chamada corretamente, quantas vezes ela vai ser chamada, se os parâmetros esperados são os corretos, já o **stub** vai nos dizer se o resultado do código retorna de acordo com os parâmetros passado, se retorna sucesso, erro ou exceção por exemplo, é previsível.

### Jest.fn()

É usado para criar uma função simulada (mock function) que pode ser passada como argumento para outras funções durante os testes.

### Jest.spyOn()

**É usado para criar uma mock function que espiona (spy) uma função existente**. Isso significa que a função original é executada normalmente, mas podemos verificar se ela foi chamada corretamente ou quantas vezes foi chamada, e também podemos modificar seu comportamento para atender às necessidades do teste.

### Jest.mock()

É usado para substituir uma dependência de um módulo por uma mock function. 

Isso é útil quando queremos testar um módulo que depende de outros módulos externos, como uma API ou banco de dados, e não queremos que os testes sejam afetados por alterações nessas dependências.

## Testando funções assíncronas

O Jest oferece suporte a testes de funções assíncronas usando as keywords `async/await` ou retornando uma Promise.

1. Testando uma função assíncrona com `async/await`:

```ts
import { fetchDataAsync } from './example';  

test('testa uma função assíncrona', async () => {   
   const result = await fetchDataAsync();   
   expect(result).toBe('data'); 
});
```

Aqui, estamos usando a keyword `await` para aguardar o resultado da função assíncrona e, em seguida, realizamos a asserção.

2. Testando uma função assíncrona retornando uma Promise:

```ts
import { fetchDataPromise } from './example';  

test('testa uma função assíncrona com Promise', () => {   
	return fetchDataPromise().then((result) => {     
		expect(result).toBe('data');   
	}); 
});
```

Neste exemplo, retornamos a Promise e utilizamos o método `.then()` para verificar o resultado.

## Testando funções de uma classe

O jest é como um testador de possibilidades, e em um classe isso não é diferente. Ele irá testar cada retorno da classe, desde funções a construtores da própria.

classe para ser testada:

```ts
export class MandarMsg {
  msg(): void {
    console.log('mensagem mandada com sucesso...');
  }
}
```

em ``mandarMsg.spec.ts``:

```ts
import { MandarMsg } from './mandarMsg';

describe('Persistency', () => {
	// limpar as instâncias desse método em cada mock
	afterEach(() => jest.clearAllMocks()); 
	
	// o metodo pode retorna undefined
	it('should return undefined', () => {
		// SUT:
		const sut = new MandarMsg();
		expect(sut.msg()).toBeUndefined();
	})
	
	// o metodo tem que chamar console.log uma vez
	it('should call console.log once', () => {
		const sut = new Persistency();
		const consoleSpy = jest.spyOn(console, 'log');
		sut.msg(); // chamar metodo
		expect(consoleSpy).toHaveBeenCalledTimes(1); // foi chamado 1 vez
	})
	// o método tem que chamar console.log com "Pedido salvo com secesso..."
	it('should call console.log with "Pedido salvo com secesso..."', () => {
		const sut = new MandarMsg();
		const consoleSpy = jest.spyOn(console, 'log');
		sut.msg();
		expect(consoleSpy).toHaveBeenCalledWith('Pedido salvo com sucesso...'); // espera ser chamado com essa string
	})
})
```

- No primeiro teste avisaremos ao jest que o método foi chamado 1 vez, assim devemos usar ``jest.spyOn()`` que observará esse objeto.

- No segundo teste o método ``msg()`` foi chamado 2 vezes, então não passara no teste. Isso é um problema do primeiro mock que chama o método 1 vez. Então para limpar as instâncias desse método em cada mock usaremos ``jest.clearAllMocks()``.

- No terceiro teste o método ``msg()`` tem que garantir que o ``console.log`` vai retorna a string "Pedido salvo com secesso..."

## Cobertura de código

O Jest fornece ferramentas para medir a cobertura de código dos testes, ou seja, a porcentagem de código testado.

1. Adicione a flag `--coverage` ao executar os testes:

```shell
npx jest --coverage
```


Isso irá gerar um relatório de cobertura de código após a execução dos testes.

2. O relatório de cobertura de código mostrará a porcentagem de linhas, funções e branches (ramificações) cobertas pelos testes.

Utilize esse relatório para identificar partes do código que não foram cobertas pelos testes.

```shell
-|---------|----------|---------|---------|-------------------
 | % Stmts | % Branch | % Funcs | % Lines | Uncovered Line #s
-|---------|----------|---------|---------|-------------------
 |     100 |      100 |     100 |     100 |
  |     100 |      100 |     100 |     100 |
   |     100 |      100 |     100 |     100 |
   |     100 |      100 |     100 |     100 |
   |     100 |      100 |     100 |     100 |
   |     100 |      100 |     100 |     100 |
   |     100 |      100 |     100 |     100 |
  |     100 |      100 |     100 |     100 |
   |     100 |      100 |     100 |     100 |
   |     100 |      100 |     100 |     100 |
-|---------|----------|---------|---------|-------------------
```
