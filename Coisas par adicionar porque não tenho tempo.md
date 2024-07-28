
# React

## `useFormStatus()`

Ele te da a informação de status do ultimo envio de formulário

```ts
const { pending, data, method, action } = useFormStatus();
```

### Disparar um status de "pending" durante o envio

```tsx
// 
function Submit() {
  const { pending } = useFormStatus();
  return (
    <button type="submit" disabled={pending}>
      {pending ? "Submitting..." : "Submit"}
    </button>
  );
}

//

export function Form() {
  function handleFormSubmit() {
    // função de delay
    await new Promise(resolve => setTimeout(resolve, 3000))
    
  }
  
  return (
    <form action={handleFormSubmit()}>
      <Submit />
    </form>
  );
}
```

# Next

## Configuração de segmento de rota

As configurações de segmento de rota permitem que você configure um comportamento de uma `page`, `Layout` ou um `Segmento de rota` diretamente exportando as seguintes variáveis:

- **`dynamic`** - Muda o comportamento para `static` ou `dynamic`.

- **`dynamicParams`** - Controla o que acontece quando um segmento dinâmico é visitado e não foi gerado com m `generateStaticParams`.

- **`revalidate`** - Define uma revalidação padrão. Essa opção não substitui o valor do `revalidate` definido por uma requisição individual de `fetch`.

- **`fetchCache`** - permite que você substitui a opção padrão de `cache` de todas as requisições `fetch`.

- **`runtime`** - É recomendado usar o runtime do Node.js para executar para renderizar suas aplicação, e usar o runtime do Edge.

- **`preferredRegion`** - O suporte para `preferredRegion` e as regiões suportadas dependem de sua plataforma de implementação.

- **`maxDuration`** - Por padrão o Next.js não tem limite de execução em logica em server side (renderizando uma página ou manipulando APIs). Plataformas de implantação podem usar `maxduration` de uma saída de build do Next.js para adicionar um limite de execução. 

Exemplo:

```ts layout.tsx | page.tsx | route.ts
export const fetchCache = 'auto'
```