
# Programação básica

## `if`/`elif`/`else` (Condicionais)

- O famoso "Se/Se não se/Se não" usado para tomar decisões entre um ou outro.

- Só pode chegar condições `True` e `false` 

```python
entrada = input('quer entrar no sistema(sim/não): ')

if entrada == 'sim': ## Se for 'sim', execute:
	print('Você entrou no sistema')
elif entrada == 'não': ## Se não for 'sim' execute:
	print('Você não entrou no sistema')
else: ## Se não for nenhuma dessas opções, execute:
	print('Sem permissão para entrar')
```

### Operação ternária (condicional de uma linha)

Uma forma de simplificar uma condicional. Exemplo:

```python
print('valor' if True else 'Outro valor')
## Execute esse valor se a condição for verdadeira. 
## Se não execute outro valor

digito = 10
novo_digito = digito if digito <= 9 else 0 ## 10
```

### Operadores de comparação

-  Usado para checagem de tipos e números. Por exemplo checar se um um número é maior que o outro `1 > 2` ou se `'a' == 'a'`;

Eles são:
- `>` Maior que
- `<` Menor que
- `>=` Maior ou igual
- `<=` Menor ou igual
- `==` Igual
- `!=` Diferente

### Operadores lógicos

- Usado para checar uma condição com outra condição. Por exemplo checar duas opções ao mesmo tempo `if 1 and 2 == true`

- São considerados `false` valores como `0`/`0.0`/`''`

Eles são:

- `and`(e) - Todas as opções devem ser verdadeiras para retornar `true`
- `or`(ou) - qualquer uma das opções deve ser verdadeira para retornar `true`
- `not`(não) - Usado para inverter expressões, exemplo `not true = false`
- `in`(entre) `not in` - Usado para determinar se algo está ou não entre uma array.
- `is`(é) `is not` - Usado para retorna se algo é determinado tipo, como se fosse o `==`. Exemplo: `if var is None:`

```python
nome = Otávio

print('á' in nome) ## "á está entre nome?"
## true
```

## `try`/`except`(Exceções)

Quando uma exceção(erro) ocorre. O Python normalmente para e gera uma mensagem de erro.

Essas exceções podem ser manipuladas usando o `try`/`except`

```python
try:
	print(x)
except:
	print('uma exceção ocorreu!')
```

## `while`(Repetições infinitas)

Executa uma ação **enquanto** uma condição for verdadeira.

- Geralmente usado para laços que você **não sabe** o final dele
```python
condicao = True

while condicao: ## Looping infinito
	nome = input('Qual o seu nome: ')
	print(f'Seu nome é {nome}')
	
## Retorno:
"""
Qual o seu nome: Nicolas
Seu nome é Nicolas
Qual o seu nome: Bruna 
Seu nome é Bruna
Qual o seu nome: Otávio
Seu nome é Otávio
...
"""
```

### Operadores de atribuição

Operadores que atribuem um numero a uma variável, eles são operações resumida. ou seja `variavel += 1` e igual a `variavel = variavel + 1`

Eles são:

- `=`(igual)
- `+=`(mais)
- `-=`(menos)
- `*=`(vezes)
- `/=`(divisão) - Pode retorna um número de ponto flutuante
- `//=`(divisão inteira) - Retorna um número inteiro
- `**=`(potenciação)
- `%=`(módulo)

### Break

acaba com o seu laço de repetição independente do valor da condição

```python
condicao = True

while condicao:
	nome = input('Qual o seu nome: ')
	print(f'Seu nome é {nome}')

	if nome == 'sair':
		break
print('acabou')

## Retorno:
"""
Qual o seu nome: Nicolas
Seu nome é Nicolas
Qual o seu nome: Bruna 
Seu nome é Bruna
Qual o seu nome: sair
acabou
"""
```

### Continue

Quando usado volta o seu laço para o começo dele.

```python
contador = 0

while contador < 10:
	contador += 1 
	if contador == 6:
		print('')
		continue ## voltou do começo

	print(contador)

## Retorno
"""
1
2
3
4
5

7
8
9
10
"""
```

### while + while

Posso fazer quantos laços eu quiser dentro de outros laços. Exemplo: ele irá executar o segundo `while` até que acabe, depois ele executa o primeiro laço

```python
qtd_linhas = 3
qtd_colunas = 3

linha = 1
while linha <= qtd_linhas:
	coluna = 1
	while coluna <= qtd_colunas:
		print(f'{linha=} {coluna=}')
		coluna += 1
	linha += 1

print('Acabou')

## Retorno
"""
linha=1 coluna=1
linha=1 coluna=2
linha=1 coluna=3
linha=2 coluna=1
linha=2 coluna=2
linha=2 coluna=3
linha=3 coluna=1
linha=3 coluna=2
linha=3 coluna=3
Acabou
"""
```

### while + else

Quando o laço `while` for executado completamente execute o `else`. É como se o código executasse fora do código.

```python
string = 'ABC'
i = 0

while i < len(string):
	letra = string[i]

	print(letra)	
	i += 1
	else:
		print('O else foi executado')

print('Fora do While')

## Retorno
"""
A
B
C
O else foi executado
Fora do While
"""
```

> Quando o seu laço `while` ter um `break`, o `else` não irá executar. O `else` só executará quando `while` for até o final

## `for`/`in` (Repetições finitas)

Executa um laço de repetições **para cada** variáveis **dentro de** um iterável.

- Geralmente usado para laços que você **sabe** o final dele

```python
texto = 'Python'
novo_texto = ''
for letra in texto: ## Para cada "letra" dentro de "texto" execute:
	novo_texto += f'*{letra}'

novo_texto += '*'
print(novo_texto)

## Retorno
"""
*P*y*t*h*o*n*
"""
```

### `range(start, stop, step)`

Uma função que percorre números, aonde tem um começo um final e de quantos a quantos passos.

```python
for numero in range(5, 10, 2): 
	print(numero)

## Retorno
"""
5
7
9
"""
```

### `continue`/`break`/`else`

Como no `while` podemos usar esses métodos no `for` também. Resumindo:

- `continue` - Volta para o começo do laço.
- `break` - Quebra o laço completamente.
- `else` - Depois de executar tudo do laço, execute-o.

```python
for i in range(5):
    if i == 2:
        print('i é 2, pulando...')
        continue

    if i == 4:
        print('i é 4, seu else não executará')
        break

    for j in range(1, 3):
        print(i, j)
else:
    print('For completo com sucesso!')

## Retorno
"""
0 1
0 2
1 1
1 2
i é 2, pulando...
3 1
3 2
i é 4, seu else não executará
"""
```

## Lista (Dado mutável)

Você pode listar **qualquer tipo** de item ordenando eles em index por index, como uma lista de mercado

- Suporta vários valores de qualquer tipo inclusive outra lista
```python
print(lista[1]) ## True
print(lista[-1]) ## []
```

### Métodos úteis

#### Alterar valores

```python
lista = ['a', 'b', 'c']

lista[2] = 'nicolas' ## ['a', 'nicolas', 'c']
```

#### `del` (deletar valores)

```python
lista = ['a', 'b', 'c']

del lista[2] ## ['a', 'c']
```

##### `pop()`

Remove o ultimo elemento da lista

```python
lista = ['a', 'b', 'c']

lista.pop() ## ['a', 'b']
```

#### `append()`(adicionar valores)


```python
lista = ['a', 'b', 'c']

lista.append('d') ## ['a', 'b', 'c', 'e']
```

##### `insert(indice, valor)`

Adiciona um item em um índice escolhido

#### `clear`(Limpar valores)


```python
lista = ['a', 'b', 'c']

lista.clear() ## []
```

#### Juntar listas

concatena as listas

```python
lista_a = [1, 2, 3]
lista_b = [4, 5, 6]
lista_c = lista_a + lista_b ## [1, 2, 3, 4, 5, 6]
```

##### `extend()`

estende uma lista usando outra lista, esse método não pode ser armazenada em uma variável.

```python
lista_a = [1, 2, 3]
lista_b = [4, 5, 6]
lista_a.extend(lista_b) ## [1, 2, 3, 4, 5, 6]
```

#### `copy(lista)`

Copia uma lista mutável

```python
lista_a = [1, 2, 3]
lista_b = lista_a.copy()

lista_a[0] = 'Qualquer coisa'
## "lista_b" diferente da "lista_a"
print(lista_b) ## [1, 2, 3]
```

#### `index(nome)`

Indica o index do nome atribuído

```python
lista = ['Maria', 'Helena', 'Luiz']

for i in lista:
print(lista.index(i), i)

## Retorno
"""
0 Maria
1 Helena
2 Luiz
"""
```
 
#### `enumerate(lista)`

Permite que acompanhe números de iterações em um loop, esse `enumerate` contém um contador.

- O `enumarate()` só é possível usar uma vez a lista até o final, depois ficará vazia
- Essa função poderá começar em qualquer numero de indice que quiser, adicione `enumerate(lista, start=5)` para 

```python
lista = ['Maria', 'Helena', 'Luiz']
lista_enumerada = enumerate(lista)

for i in lista_enumerada:
	print(i)

print(list(enumerate(lista, start=5))) 
## [(5, 'Maria'), (6, 'Helena'), (7, 'Luiz')]

## Retorno
"""
(0, 'Maria')
(1, 'Helena')
(2, 'Luiz')

"""
```

##### Dicas

-  Pegar dois índices separados em A e B por um `for`

```python
lista = ['Maria', 'Helena', 'Luiz']

for indice, nome in enumerate(lista):
	print(indice, nome)
```
> Output
```shell
0 Maria
1 Helena
2 Luiz
```

### Desempacotamento

Armazena cada valor em cada variável

```python
nome1, nome2, nome3 = ['Maria', 'Helena', 'Luiz']
print(nome2) ## Helena
```

- Posso também desempacotar o primeiro valor e jogar o "resto" em uma lista
- Também posso desempacotar o ultimo item da lista

```python
primeiro, *resto, ultimo = ['Maria', 'Helena', 'Luiz', 'Marcos']
print(primeiro, resto, ultimo) ## Maria ['Helena', 'Luiz']
```

#### Dicas

- Em vez de usar o `for` para listar itens em fileira, eu posso usar o `desempacotamento`

- ele vai passar por todos os itens da lista e desempacotar cada item dela

```python
lista = ['Maria', 'Helena', 'Luiz']
string = 'ABCD'

print(*lista) ## Maria Helena Luiz
print(*string) ## A B C D
```

### Tupla

É uma lista imutável, é feita do mesmo jeito da lista mas substituindo os colchetes  pelos parenteses ou tirar os colchetes 

```python
nomes = 'Maria', 'Helena', 'Luiz' ## 
print(nomes) ## ('Maria', 'Helena', 'Luiz')
```

### Dicas

- Pegar os índices de uma lista dinamicamente

```python
lista = ['Maria', 'Helena', 'Luiz']
indices = range(len(lista)) ## range(0, 2)

for indice in indices:
	print(indice, lista[indice])
```
> Output
```terminal
0 Maria
1 Helena
2 Luiz
```

## Objetos

### Métodos do python

#### `__iter__()`

Cria um objeto **iterável** com funções próprias.

```python
texto = 'luiz'.__iter__()

## Retono
"""
<str_ascii_iterator object at 0x7f21603d7790>
"""
```

> Posso chamar o método `__iter__()` com a função `iter('variavel')`

#### `__next__()`

Avança para o **próximo item** de um método iterável. Até que o iterável chegue no final assim levantando uma exceção chamada `StopIteration`

```python
texto = 'luiz'.__iter__()

print(texto.__next__())
print(texto.__next__())
print(texto.__next__())
print(texto.__next__())
print(texto.__next__())
## Retono
"""
l
u
i
z
Traceback (most recent call last):
  File "/mnt/Media/Linguagens/Back-end/Python/python_review/main.py", line 7, in <module>
    print(texto.__next__())
          ^^^^^^^^^^^^^^^^
StopIteration
"""
```

> Posso chamar o método `__next__()` com a função `next(texto)`

# Funções básicas

## Comentários

Existem dois tipos de comentários em python

1. `# qualquer texto`

- Não interpretado pelo Python.
- Pode comentar em só uma linha.

2. `""" qualquer texto """`

-  Chamado de **DocString** e Interpretado pelo Python
- Pode comentar em várias linhas.

## `print()`

- Mostra argumentos no terminal.
- pode separar argumentos com a virgula. exemplo: `print(1, 2)`

### Argumentos especiais

#### `sep=""`

- Define um separador de cada argumento. Por padrão é um espaço

Usado:
```python
print(1, 2, 3, sep="-")

# Retorno
"""
1-2-3
"""
```

#### `end=""`

- Define no final do print qualquer tipo de caractere. Por padrão (dependendo do seu sistema operacional) `\r\n` ou `\n`

```python
print(1, 2, 3, end="##")
print("teste")

# Retorno
"""
1 2 3##teste
"""
```

## `input()`

- Coleta dados do usuário. Passar um tipo de argumento sempre retornará o mesmo tipo.

```python
nome = input('qual o seu nome?')
print(nome)

## Retorno
"""
Qual o seu nome? João
João
"""
```

## `type()`

- É uma classe que mostra o tipo de um argumento

```python
<class 'str'>
```

## Classe de conversão


### `int()`

- converte qualquer argumento em um número inteiro;

### `float`

- converte um número em float (números decimais)

### `bool()`

- Interpreta qualquer argumento para boolean(true ou false)

## `len()`

Conta quantos caracteres tem em uma string

```python
variavel = 'Olá mundo'

print(len(variavel)) ## 9
```


# Tipos embutidos(built-in)

## String

String é um tipo de texto, usado envelopando os caracteres em `""`
### `\`

- Usado para usar uma tecla de **escape** (tecla que cancela a função dela própria). Exemplo: 

```python
print("nome qualquer: \"nicolas\"")

# Retorno
"""
nome qualquer: "nicolas"
"""
```

> Usado também para quebrar linhas em códigos, quando ela precisa de continuação 

```python
if local_carro >= (LOCAL_1 - RADAR_RANGE) and \
		local_carro <= (LOCAL_1 + RADAR_RANGE):
	print('teste')
```
### `r""`(Raw strings)

- Usado para ignorar todos os caracteres de **escape** em toda string
- Mais usado para **Regex**

```python
print(r"nome qualquer: \"nicolas\"")

# Retorno
"""
nome qualquer: \"nicolas\"
"""
```
### `f""` (F-strings)

- É uma formatação de string usado junto com variáveis.

```python
print(f'{nome} tem {altura} de altura')

### Retorno
"""
matheus tem 1.706134213523 de altura
"""
```

#### {variavel=}

A variável ficará com o nome e o valor juntos. Exemplo:

```python
print(f'{nome=} tem {altura=} de altura')

## Retorno
"""
nome=matheus tem altura=1.706134213523 de altura
"""
```

### `%`(Interpolação básica de strings)

- `%s` - Strings
- `%d` e `%i` - números inteiros
- `%f` - números float (decimais)
- `%x` e `%X` - Hexadecimal (ABCDEF0123456789)

```python
nome = 'Luiz'
preco = 1000.958943

variavel = '%s, o preço é R$%.2f' % (nome, preco)
print() ## Luiz, o preço é R$1000.92
```

#### `%01x`

```python
print('O hexadecimal de %d é %08X' % (1500, 1500))
## O hexadecimal de 1500 é 000005DC
```

### Formatação básica de strings

Eles são:

- `s` - string
- `d` - int
- `f` - float
- `x` ou `X` - Hexadecimal
- `=` - Força um número aparecer antes dos zeros

#### `:c>1`(Padding)

Adiciona um padding(espaçamento) qualquer direção

- `(caractere)>(quantidade)` - padding para a direita 
- `(caractere)<(quantidade)` - padding para a esquerda
- `(caractere)^(quantidade)` - padding no centro

```python
variavel = 'ABC'
print(f'{variavel:|>10}') ## |||||||ABC
print(f'{variavel:|<10}') ## ABC|||||||
print(f'{variavel:|^10}') ## |||ABC||||
```

#### `:.nf` (Números decimais)

Você pode especificar quantas casas decimais pode ser mostrado.

- `:.(quantidade)f` - quantidade de números mostrados depois da vírgula


```python
altura = 1.704135623421

print(f'{altura:.2f}') ## 1.70
```

> Você pode usar `:+.1f` para especificar um numero positivo. Exemplo: `+10000000`

> Você pode usar `:,.2f` para usar virgula a cada 3 números. Exemplo: `100,000.00`


### `[i:f:p]`(Fatiamento de strings)

Uma string é um array aonde cada caractere é um Índice desse array.

- Para pegar de trás para frente usa o índice negativo `variavel[-1]`

- O fatiamento é especificar aonde começa, termina e de quantos passos `[inicio:final:passos]`

```python
variavel = 'Olá mundo'

print(variavel[4]) ## m
print(variavel[0:5:2]) ## Oám
print(variavel[4:]) ## mundo
```

> Você pode omitir o inicio ou o final `variavel[4:]`

### Métodos de Strings

Strings implementam todas as operações comuns de sequências, juntamente com os métodos adicionais mais usados.

Aqui estão todos os [Métodos de string](https://docs.python.org/pt-br/3/library/stdtypes.html#string-methods "Link to this heading")

#### `.capitalize()`

Retorna uma cópia da string com o seu primeiro caractere em maiúsculo e o restante em minúsculo.

#### `.split()`

Divide uma string para lista, por padrão ele divide a cada espaço em branco

- Posso quebrar a frase depois de um carácter especifico. `.split(caracter)`

```python
frase = 'Olha só que, coisa interessante'

lista_palavras = frase.split()
## ['Olha', 'só', 'que,', 'coisa', 'interessante']
lista_palavras = frase.split(',')
## ['Olha só que', ' coisa interessante']

```

#### `.strip()`

Tira os espaços de uma string no final dela e no começo.

- `.rstrip` corta os espaços da direita(final)
- `.lstrip` corta os espaços da esquerda(começo)

```python
frase = '        Olha só que, coisa interessante         '

lista_palavras = frase.strip()
## Olha só que, coisa interessante
```

#### `.join()`

junta iteráveis com caracteres no meio de cada

```python
frase = ['Olha só que', 'coisa interessante']

frases_unidas = '_'.join(frase) 
## Olha só que_coisa interessante
```


#### `.lower()`

Retorna uma cópia da string com todos os caracteres que permitem maiúsculo E minúsculo convertidos para letras minúsculas.

#### `.replace(old, new[, count])`

Retorna uma cópia da string com todas as ocorrências da substring **old** substituídas por **new**. Se o argumento opcional **count** é fornecido, apenas as primeiras **count** ocorrências são substituídas.

#### `.isalpha()`

Retorna `True` se todos os caracteres na string são alfabéticos e existe pelo menos um caractere, `False` caso contrário.

#### `.isascii()`

Retorna `True` se a string é vazia ou se todos os caracteres na string são ASCII, `False` caso contrário.

#### `.isdecimal()`

Retorna `True` se todos os caracteres na string são caracteres decimais e existe pelo menos um caractere, `False` caso contrário.

#### `.isdigit()`

Retorna `True` se todos os caracteres na string são dígitos e existe pelo menos um caractere, `False` caso contrário.

#### `.islower()`

Retorna `True` se todos os caracteres em caixa (que possuem maiúsculo e minúsculo) na string são minúsculos e existe pelo menos um caractere em caixa, `False` caso contrário.

#### `.isnumeric()`

Retorna `True` se todos os caracteres na string são caracteres numéricos

#### `.isspace()`

Retorna `True` se existem apenas caracteres de espaço em branco na string e existe pelo menos um caractere, `False` caso contrário.

## Int

Int é um tipo de numero inteiro

## Float

Int é um tipo de numero decimal

#### Aritmética de ponto flutuante

Existe uma imprecisão em números de pontos flutuantes quando são calculados, há muitas maneiras de resolver esse problema.

- Usar `fStrings`
- Usar a função `round()`- arrendonda as casas finais
- Importar uma classe `decimal`

```python
import decimal

numero_1 = 0.1
numero_2 = 0.7
numero_3 = numero_1 + numero_2
print(numero_3) ## 0.7999999999999
## fStrings
print(f'{numero_3:.2f}') ## 0.80
## round()
print(round(numero_3, 2)) ## 0.80
## decimal
numero_1 = decimal.Decimal(0.1)
numero_2 = decimal.Decimal(0.7)

print(numero_1 + numero_2)
```

## Bool

Bool ou Boolean é um tipo de 0 ou 1, True ou False

## None

É um dado que representa a ausência de um valor ou um valor null

- Usado geralmente para determinar ou chamar uma variável que não existe em certos blocos de códigos como um placeholder
```python
passou = None ## passou foi chamado antes

if False:
	passou = True ## passou tem seu valor mudado nesse bloco
	print('faça algo')
else:
	print('Não faça algo')

print(passou) ## None
```

# Dicas

## Variáveis

 - No Python não existem variáveis constantes então por convenção geral quando uma variável é constante usamos letra maiúsculas.                         Exemplo: `VARIAVEL_1 = 60`


### `id()` 

É um código de identificação por variável, se o valor da variável for igual o id também vai ser.

```python
v1 = 'a'
v2 = 'a'
v3 = 'b'
print(id(v1)) ## 4372210416
print(id(v2)) ## 4372210416
print(id(v3)) ## 4371992752
```

## `...` (Elipses)

- É um placeholder, usado para códigos inacabados para que não gere erros

```python
if variavel:
	...
```

## `;`(quebra de linha)

- Representa uma quebra de linha. Muito usado para códigos que precisão de uma linha unica para funcionar. Exemplo: `print('Oi');print(1+1)`

## Dados

### Imutáveis 

Copia o valor

```python
nome = 'Luiz'
outro_nome = nome
nome = 'João'
print(nome) ## João
print(outro_nome) ## Luiz
```

### Mutáveis

aponta para o mesmo valor na memória

```python
lista_a = ['Luiz', 'Maria']
lista_b = lista_a

lista_a[0] = 'Qualquer coisa'
print(lista_b)
```

## The Zen of Python, por Tim Peters

- Bonito é melhor que feio.
- Explícito é melhor que implícito.
- Simples é melhor que complexo.
- Complexo é melhor que complicado.
- Plano é melhor que aglomerado.
- Esparso é melhor que denso.
- Legibilidade conta.
- Casos especiais não são especiais o bastante para quebrar as regras.
- Embora a praticidade vença a pureza.
- Erros nunca devem passar silenciosamente.
- A menos que sejam explicitamente silenciados.
- Diante da ambiguidade, recuse a tentação de adivinhar.
- Deve haver um -- e só um -- modo óbvio para fazer algo.
- Embora esse modo possa não ser óbvio à primeira vista a menos que você seja holandês.
- Agora é melhor que nunca.
- Embora nunca frequentemente seja melhor que *exatamente* agora.
- Se a implementação é difícil de explicar, é uma má ideia.
- Se a implementação é fácil de explicar, pode ser uma boa ideia.
- Namespaces são uma grande ideia -- vamos fazer mais dessas!

# Comandos

## `python`

### `python`

- Executa no modo interativo do python. O que possibilita fazer qualquer código e retorna na mesma hora.

### `python -i <arquivo.py>`

- Carrega um arquivo `.py` com o modo interativo daquele arquivo

### `python --version`

- indica versão do Python

> pode ser resumido por `python -V`

```bash
Python 3.11.8
```

### `python <arquivo.py>`

- Abre um arquivo `.py`

### `python -i <arquivo.py>`

- Abre o shell interativo com um arquivo .py

### `which python`

- Para onde o python está apontando, caminho em que foi instalado

```bash
/mnt/Media/Linguagens/Back-end/Python/python_review/venv/bin/python
```

### `python -u <arquivo.py>`(unbuffered)

- geralmente o python salva o código em um buffer antes de mostrar na tela. Esse comando evita isso.

### `python -m <modulo> <exe>`

- Executa uma biblioteca como script e cria um ambiente virtual. Exemplo: `python -m venv `

### `python -c <comando>`

- Executa um comando em python aonde mostrará um retorno

## `venv`


### `python -m venv venv`

- Cria pasta **venv** como um ambiente virtual.

### `source venv/bin/activate`

- Entra no ambiente de virtual **venv** do python

### `deactivate`

- Sai do ambiente virtual **venv**

## `pip`

### `pip install <package>`

- Instala um pacote de python

### `python -m pip install pip --upgrade`

- Atualiza o pip

## `pyenv`

Gerenciador de versões do python

### Instalação

```bash
curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
```

Depois cole as propriedades mostradas no terminal no final do arquivo em 
`nano ~/.zshrc`, algo parecido com isso:

```bash
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

### Comandos

#### `pyenv update`

- Atualiza pyenv

#### `pyenv install -l`

- Lista todas as versões do Python

> Dica: O Python completo está nas versões sem nenhuma especificação exemplo: 0.0.0

#### `pyenv install <0.0.0>`

- Instala uma versão

#### `pyenv global <0.0.0>`

- Para definir o python instalado pelo pyenv em vez do python já instalado, use esse comando

