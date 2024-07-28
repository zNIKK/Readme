# O que é

é um conjunto de classes em css que são padronizadas em todo projeto, alem de melhorar a produtividade.
# instalação

Para instalar o Tailwind precisa instalar `tailwindcss` e criar automaticamente um arquivo `tailwind.config.js` com o comando `npx tailwindcss init`

```shell
npm install -D tailwindcss
npx tailwindcss init
```

# Classes importantes

- `h-scream` - ocupar o height toda da tela
```css
.h-screen {  
  height: 100vh;  
}
```

- `space-y-1` | `space-x-1` - Fazer o espaçamento entre os elementos verticais ou horizontais usando um calculo do padding top e bottom
```css
.space-y-1 > :not([hidden]) ~ :not([hidden]) {  
  --tw-space-y-reverse: 0;  
  margin-top: 
    calc(0.25rem/* 4px */ * calc(1 - var(--tw-space-y-reverse)));  
  margin-bottom: 
    calc(0.25rem/* 4px */ * var(--tw-space-y-reverse));  
}
```

- `gap-1` - espaçamentos entre elementos.
```css
.gap-4 {  
  gap: 1rem/* 16px */;  
}
```

- `rounded` - colocar bordas arrendondadas
```css
.rounded {  
  border-radius: 0.25rem/* 4px */;  
}
```

## flex

- `flex-1` - Crescer o container para ocupar um tamanho que se adapta a tela

```css
.flex-1 {  
  flex: 1 1 0%;
}
```


# Tailwind CSS IntelliSense

Uma extensão oficial do VSCode que permite autocompletar classes, realce de sintaxe e linting.

- **Autocompletar** - A extensão dará sugestões de nomes de classes
- **Linting** - destaca erros e bugs em potencial.
- **Pre visualizações de prévias** - Veja o CSS completo de uma classe passando o mouse por ele
- **Realce de sintaxe** - Fornece definições de sintaxes para que os recursos do tailwind sejam destacados corretamente