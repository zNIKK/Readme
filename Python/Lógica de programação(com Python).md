
## Pegar os índices de uma lista dinamicamente

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

## Pegar dois índices separados em A e B

```python
lista = ['Maria', 'Helena', 'Luiz']

for item in enumerate(lista):
	a, b = item
	print(item)
```