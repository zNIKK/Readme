
# Uso

- em vez de usar **ANY**
```ts
function generic(value = any): any { 
	return value 
}
```

- você usa o Tipo Genérico Type ou T

```ts
function generic<T>(value = T): T { 
	return value 
}
```

- assim quando for chamá-la você tem duas maneiras:

```ts
generic<string>('myString')
// ou
generic('myString')
```

# Extends

- quando eu quero obter uma chave em um objeto que seja genérico

  `type ObterChaveFn = <O, K>(objeto: O, chave: K) => O[K]`

- não podemos pegar a chave K do tipo O, porque ele é genérico demais

- por causa disso devemos usar extends para dizer para o Typescript que o tipo K é no máximo uma chave do tipo O

```ts
type ObterChaveFn = <O, K extends keyof O>(objeto: O, chave: K) => O[K]
```

# Intersection

- se eu unir elementos e quero que os tipos se unem junto eu uso o &
```ts
function unirObjetos<T, U>(obj1: T, obj2: U): T & U
```

# Predicate

- usamos o ``value is number``, sempre que ele retornar o valor **true** no ``typeof``, assim ele vai se tornar um numero.

```ts
function isNumber(value: unknown): value is number {
	return typeof value === 'number'
}
```

# Dicas

- Posso usar valores padrões como:

 ```ts
 interface PessoaProtocolo<T = string> {nome: T}
 ```

  ou seja eu posso omitir o valor do tipo do objeto

  ```ts
  const aluno: PessoaProtocolo = {nome: 'Luiz'}
  ```