
## O que é

O Next.js simplifica o desenvolvimento de aplicações React, oferecendo uma estrutura robusta e eficiente para a construção de aplicações web modernas. Explore a documentação completa para obter informações detalhadas e exemplos mais aprofundados.

## Instalação

Recomendamos começar um novo projeto em Next.js usando `create-next-app`, no qual define tudo automaticamente por você. Para criar um projeto, rode:

```powershell
npx create-next-app@latest
```

Na hora da instalação, irão ser mostradas os seguintes prompts:

```powershell
What is your project named? my-app
Would you like to use TypeScript? No / Yes
Would you like to use ESLint? No / Yes
Would you like to use Tailwind CSS? No / Yes
Would you like to use `src/` directory? No / Yes
Would you like to use App Router? (recommended) No / Yes
Would you like to customize the default import alias (@/*)? No / Yes
What import alias would you like configured? @/*
```

### Instalação manual

Para fazer uma instalação manual, precisará criar os pacotes requeridos:

```powershell
npm install next@latest react@latest react-dom@latest
```

abra seu arquivo `package.json` e adicione os seguintes scripts:

```json package.json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

Esses scripts remetem para diferentes estágios de modo de desenvolvimento

- `dev`: roda `next dev` para começar Next.js em modo desenvolvedor.

- `build`: roda `next build` para fazer build de sua aplicação para uso em produção.

- `start`: roda `next start` para começar uma produção de servidor Next.js.

- `lint`: roda `next lint` para definir a configuração ESLint integrada do Next.js.

## Estrutura de arquivos

A partir da criação dos arquivos no next.js a estrutura da pasta se aparentara com a imagem abaixo:

![[Prints/Pasted image 20240209194041.png]]

- `/app` Contêm todas as rotas, componentes, e logica da aplicação. É aonde você mais usará;

- `/app/lib` Contêm funções usadas em sua aplicação, como as funções de utilidade reutilizáveis e funções de busca de dados (data fetching functions);

- `/app/ui` Contêm todos os UI componentes da sia aplicação, como `cards`, `tables` e `forms`, para não perder tempo, o next.js já pre disponibilizou componentes estilizados;

- `public` Contêm todas as `assets` da aplicação, como as imagens;

- `scripts` Contêm os `seeding scripts` (um script que é colocado dados fictícios) usado para incrementar sua database;

## Fundamentos de Roteamento

### Estrutura

O next.js fornece vários tipos de rotas com um comportamento específicos entre elas.

- [layouts](<### Layouts>) - Uma UI (interface de usuário) compartilhada para um segmento e seus filhos;
- [page](<### Pages>) - Uma UI unica de uma rota publicamente acessível;
- [loading](<### Loading>) - Uma UI de carregamento
- [not-found](<### Not-found>) - Uma UI de erro 404
- [error](<### Error>) - Uma UI de erro
- [global-error](<### Global-Error>) - Uma UI de erro global
- [route](<### Route>) - Uma Server-side API endpoint
- [template](<### Template>) - Especializado em re-renderizar o UI layout
- [default](<### Default>) - Uma UI de fallback para Rotas paralelas 

### Hierarquia de Componentes

- `layout.js`
- `template.js`
- `error.js`
- `loading.js`
- `not-found.js`
- `page.js` ou [nested](<#### Nested routes>) `layout.js`

![[Prints/Hierarquia de Componentes.png]]

### Rotas

Em next.js uma rota é criada a partir de [arquivos aninhados (nested files)](<#### Nested routes>) resumidamente são arquivos dentro de outros.

Em especial, ``page.js`` que é usado para fazer um segmento de rota publicamente acessível.

![[Prints/Pasted image 20240209120852.png]]

No exemplo, o caminho de URL ``./dashboard/analytics`` não é publicamente acessível, porque não tem um arquivo ``page.js``, esse arquivo pode ser usado para armazenar componentes stylesheets, imagens, ou outros arquivos de [colocação](<#### Colocação>)

#### Dicas

Para desconsiderar rotas no Next.js usa-se `_` antes do nome da rota exemplo `_document.tsx` 

### Segmentos de rotas

Cada pasta em uma rota representa um ``route segment`` a cada ``segment`` é mapeado para um correspondente a uma **URL path**

![[Prints/Pasted image 20240209112437.png]]

exemplo os segmentos de `/dashboard/settings`

1. `/` (Segmento root)
2. ``dashboard`` (Segmento)
3. `settings` (Segmento Leaf)

#### Nested routes

Para criar uma ``Nested route``, coloque os arquivos dentro de outros. por exemplo, adicionando uma nova rota de `/dashboard/settings` aninhando duas novas pastas dentro do diretório do ``app``

#### Colocação

Tem a opção de colocar seus arquivos (componentes, estilos, testes, etc...) dentro de arquivos no diretório `app` sem que eles sejam roteáveis.

![[Prints/Pasted image 20240209114144.png]]


#### Criar uma UI (Interface de Usuário)

conversões de arquivos especiais são usadas para criar UI pra cada segmento de rota, a mais importante e comumente usada é a `pages` que mostra uma UI única para uma certa rota, ou até o ``layouts`` que mostra UI que é compartilhada através de múltiplas rotas.

##### Pages

É uma **rota unica**, geralmente a página principal, para criar sua primeira pagina, coloque um arquivo `page.js` dentro do diretório `app` e exporte um componente React 

```tsx /app/page.tsx
// `app/page.tsx` É a rota de `/`

export default function Page() {
  return <h1>Hello, Home page!</h1>
}
```

##### Dashboard pages

Cria um arquivo chamado `dashboard` dentro de `app`. Assim crie um novo arquivo `page.tsx` dentro de `dashboard` com o seguinte conteúdo:

```tsx /app/dashboard/page.tsx
export default function Page() {
  return <p>Dashboard Page</p>;
}
```

Assim criando uma rota em `http://localhost:3000/dashboard`, e assim você pode criar diferentes `pages` em vários arquivos diferentes.

##### Layouts

Um layout é um arquivo que se compartilha entre múltiplas rotas, layouts preserva o estado, permanece interativo, e não é re-renderizado.


```tsx /app/dashboard/layout.tsx
export default function DashboardLayout({

}: {
  children: React.ReactNode
}) {
  return (
    <section>
      {/* Inclua uma UI compartilhada. Ex: header ou sidebar */}
      <nav></nav>
 
      {children}
    </section>
  )
}
```

##### Root Layout

Qualquer UI que for adicionada ao layout raiz será compartilhada em todas as páginas do seu aplicativo e não restringe a um arquivo só.

Esse layout se aplica para todos os layouts. Esse layout é obrigatório e precisa conter tags `html` e `body`, possibilitando modificar o HMTL inicial retornada de um server

```tsx /app/layout.tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>
        {/* Layout UI */}
        <main>{children}</main>
      </body>
    </html>
  )
}
```

##### Document

O arquivo document é usado para atualizar as tags `<html>` e `<body>` são utilizadas para renderizar a `page`

#### Templates

Templates são similar aos layouts eles envolvem cada **child layout** ou **page**. 

Diferentes dos layouts que persistem através das rotas e conserva os states, templates cria uma nova instância pra cada um de seus filhos. 

Isso significa que quando um usuário navega entre rotas que compartilham um template, uma nova instância de um componente é montada, elementos DOM são recriados, mas os states não são preservados, e effects são re-sincronizados 

##### Aonde aplica

No caso aonde precisasse dos seguintes comportamentos, templates pode ser uma opção mais comportável do que layouts.

- Features que dependem de `useEffect` (ex: pagina de login) e `useState` (ex: um formulário de feedback por página)

- Para mudar um comportamento de framework padrão. por exemplo,**suspense Boundaries** dentro de layouts só mostrando os fallback da primeira vez que o layout é carregado e não quando trocado de página. Os fallback é mostrado a cada navegação.

Um template pode ser definido pelo exportamento de um componente React padrão vindo de um arquivo `template.js`. O componente aceita um `children` prop.

```tsx /app/tamplates.js
export default function Template(
{ children }: { 
	children: React.ReactNode 
}) {
  return <div>{children}</div>
}
```

### Linking e Navegação

Tem 4 maneiras para navegar entre rotas:

1. Usando o Componente `<Link>` 
2. Usando o hook `useRouter` ([Client Component](https://nextjs.org/docs/app/building-your-application/rendering/client-components))
3. Usando a função `redirect` ([Server Component](https://nextjs.org/docs/app/building-your-application/rendering/server-components))
4. Usando o [API Histórico](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#using-the-native-history-api) nativo

#### Componente `<Link>`

Para navegar entre páginas, tradicionalmente usa-se a tag `<a>` porem toda vez que esse link é carregada a página inteira é atualizada, esse comportamento não pode acontecer.

```tsx /app/ui/dashboard/nav-links.tsx
import Link from 'next/link';

export default function nav() {
	return (
		<Link href="/">home</Link>
	)
}
```

Assim para resolver esse problema usamos o componente `<Link>` para navegar entre páginas que permite você usar o `client side navigation`.

Diferente do tradicional SPA (Single-page application) do React aonde o navegador carrega todo o código da sua aplicação no primeiro carregamento, o Next.js divide o seu código automaticamente do seu aplicativo por segmentos de rota.

Dividir o código por rotas significa que as páginas se tornaram isoladas. Ou seja, se uma certa página retornar um erro o resto da sua aplicação ainda irá funcionar.

A partir do momento que o link for exibido na view port do navegador. O Next.js pre-busca o código que estará ligado a essa rota em segundo plano.

##### Linkando Segmentos dinâmicos

Quando se linka segmentos dinâmicos, você pode usar [template literals e interpolação](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Template_literals) para gerar uma lista de  links. Por exemplo:

```jsx app/blog/PostList.jsx
import Link from 'next/link'
 
export default function PostList({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <Link href={`/blog/${post.slug}`}>{post.title}</Link>
        </li>
      ))}
    </ul>
  )
}
```

##### Verificando links ativos

Você pode usar `usePathname()` para determinar se um link está ativo. Por exemplo, adicionar uma classe ao link ativo, você pode checar se o atual `pathname` combina com `href` link.

```tsx app/components/links.tsx
'use client'
 
import { usePathname } from 'next/navigation'
import Link from 'next/link'
 
export function Links() {
  const pathname = usePathname()
 
  return (
    <nav>
      <ul>
        <li>
          <Link className={`link ${pathname === '/' ? 'active' : ''}`} href="/">
            Home
          </Link>
        </li>
        <li>
          <Link
            className={`link ${pathname === '/about' ? 'active' : ''}`}
            href="/about"
          >
            About
          </Link>
        </li>
      </ul>
    </nav>
  )
}
```

##### Rolagem até o `id`

O comportamento padrão do App router Next.js é o scroll ate o topo da página de uma nova rota ou preservar o posição do scroll para navegação de trás para frente.

Se você gostaria de rolar para um especifico `id`, você pode juntar seu URL com um link hash `#` ou passar um link hash para a propriedade `href`. 

Isso será possível porque o `<Link>` renderiza em um elemento `<a>` 

```tsx
<Link href="/dashboard#settings">Settings</Link>
 
// Output
<a href="/dashboard#settings">Settings</a>
```

##### Desabilitando restauração de scroll

Se você gostaria de desabilitar esse comportamento, você pode colocar `scroll={false}` para o Componente `<Link>`, ou `scroll: false` para `router.push()` ou `router.replace()`.

```tsx
// next/link
<Link href="/dashboard" scroll={false}>
  Dashboard
</Link>
```

```tsx
// useRouter
import { useRouter } from 'next/navigation'
 
const router = useRouter()
 
router.push('/dashboard', { scroll: false })
```

#### Hook `useRouter()` 

O Hook `useRouter` permite que programaticamente mude rotas de [Componente de Cliente](https://nextjs.org/docs/app/building-your-application/rendering/client-components)

```tsx app/page.js
'use client'
 
import { useRouter } from 'next/navigation'
 
export default function Page() {
  const router = useRouter()
 
  return (
    <button type="button" onClick={() => router.push('/dashboard')}>
      Dashboard
    </button>
  )
}
```

Para mais especificações de `useRouter`, veja [API reference](https://nextjs.org/docs/app/api-reference/functions/use-router).

> **Recomendação**: Usa o Componente `<Link>` para navegar entre rotas a menos que você tenha um requerimento especifico para usar `useRouter`

#### Função `redirect`

Para o [Componente de Server](https://nextjs.org/docs/app/building-your-application/rendering/server-components), usa a função `redirect`.

```tsx app/team/[id]/page.tsx
import { redirect } from 'next/navigation'
 
async function fetchTeam(id: string) {
  const res = await fetch('https://...')
  if (!res.ok) return undefined
  return res.json()
}
 
export default async function Profile({ params }: { params: { id: string } }) {
  const team = await fetchTeam(params.id)
  if (!team) {
    redirect('/login')
  }
 
  // ...
}
```

> **Dicas**:
> - `redirect` retorna um código de status **307 (Temporary Redirect)** por padrão. Quando usado em uma Ação de Server, ele irá retorna um **303(See Other)**. No qual é comumente usado para redirecionamento para uma pagina bem sucedida como um request de POST.
> - `redirect` lança um erro então deve ser chamado fora dos blocos `try/catch`
> - `redirect` pode ser chamado em Componente de Cliente durante o processo de renderização mas não em Event Handlers(manipuladores de eventos). Use o Hook `useRouter`ao invés disso.
> - `redirect` só aceita URLs absolutas e pode ser usada para redirecionar a um link externo.
> - Se você gostaria de redirecionar antes do processo de renderizar, usa o `next.config.js` ou [Middleware](https://nextjs.org/docs/app/building-your-application/routing/redirecting#nextresponseredirect-in-middleware).

Veja [API de referência `redirect`](https://nextjs.org/docs/app/api-reference/functions/redirect) para mais informações.

#### Usando o histórico de API nativo.

Next.js permite usar o método nativo [`window.history.pushState`](https://developer.mozilla.org/en-US/docs/Web/API/History/pushState) e o [`window.history.replaceState`](https://developer.mozilla.org/en-US/docs/Web/API/History/replaceState) para atualizar a pilha de históricos do navegador sem recarregar a página

`pushState` e `replaceState` integram dentro do Next.js Router, permitindo sincronizar com `usePathname` e `useSearchParams`.

##### `window.history.pushState`

Usa-lo para adicionar uma nova entrada em sua pilha de histórico navegador. O usuário pode navegar de volta ao estado anterior. Por exemplo, organizar uma lista de produtos:

```tsx
'use client'
 
import { useSearchParams } from 'next/navigation'
 
export default function SortProducts() {
  const searchParams = useSearchParams()
 
  function updateSorting(sortOrder: string) {
    const params = new URLSearchParams(searchParams.toString())
    params.set('sort', sortOrder)
    window.history.pushState(null, '', `?${params.toString()}`)
  }
 
  return (
    <>
      <button onClick={() => updateSorting('asc')}>
	      Sort Ascending
      </button>
      <button onClick={() => updateSorting('desc')}>
	      Sort Descending
      </button>
    </>
  )
}
```

##### `window.history.replaceState`

Usa-lo para adicionar uma nova entrada em sua pilha de histórico navegador. O usuário não consegue navegar de volta ao estado anterior. Por exemplo, trocar o local da aplicação:

```tsx
'use client'
 
import { usePathname } from 'next/navigation'
 
export function LocaleSwitcher() {
  const pathname = usePathname()
 
  function switchLocale(locale: string) {
    // e.g. '/en/about' or '/fr/contact'
    const newPath = `/${locale}${pathname}`
    window.history.replaceState(null, '', newPath)
  }
 
  return (
    <>
      <button onClick={() => switchLocale('en')}>English</button>
      <button onClick={() => switchLocale('fr')}>French</button>
    </>
  )
}
```

### Modelos avançados de rotas

Modelos de rotas que usa-se para momentos específicos.

#### Rotas paralelas

Permite que mostre simultaneamente duas ou mais paginas na mesma visualização e podendo navegar independentemente. Exemplo: Dashboards 

#### Rotas interceptada

Permite que intercepte uma rota e mostre ela no contexto de outra rota. Exemplo: expandir uma foto no feed como um ``modal popup``

## Renderização

Uma renderização escreve o código que você escreve em uma interface de usuário.

### Componentes de Cliente

Usa-se `"use client"` no topo do arquivo.

Esses componentes permite que você escreva um UI interativo em client **opt-in**, significa que você tem que decidir explicitamente que o componente React deve ser renderizado no cliente.

#### Benefícios

- **interatividade**: Componentes Client pode usar states, effects e event listeners, significa que eles podem fornecer um feedback imediatamente para o usuário e atualizar a UI

- **Browser APIs**: Componentes Client tem acesso ao API de navegador, como geolocalização, ou até mesmo `localStorage`.

### Componentes de Servidores

São Componentes React que permitem escrever uma UI qye pode ser renderizada e opcionalmente armazenada em cache no servidor. em Next.js, o trabalho de renderização e dividido por rota
## Estilizando

### Como colocar fonts

Dentro de `/app/ui`, crie um arquivo chamado `fonts.ts`. 

importe a fonte, como exemplo a fonte `Inter` importe de `next/font/google`. Essa fonte será a sua fonte primária.

```ts /app/ui
import { Inter } from 'next/font/google';
// em subset é colocado qual o subconjunto deseja carregar
export const inter = Inter({ subsets: ['latin'] });
```

E por fim, coloque a fonte no elemento `<body>` em  `/app/layout.tsx`, ou em qualquer lugar que quiser.

```tsx /app/layout.tsx

import '@/app/ui/global.css';
import { inter } from '@/app/ui/fonts';
 
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={`${inter.className} antialiased`}>
	      {children}
      </body>
    </html>
  );
}
```

### Como colocar imagens

Isso servirá para mídias estáticas, como imagens.

em `/public`. Tudo que está dentro de public pode ser usado normalmente como assets.

```tsx 
<img
  src="/hero.png"
  alt="Screenshots of the dashboard project showing desktop version"
/>
```

Esse método usa a tag `<img>` que tem algumas vantagens:

- Garante que a sua imagem fique responsiva em diferentes tamanhos de telas;

- Evita mudanças de layout (layout shift), conforme as imagens forem carregadas;

- Carregamento lento de imagens que estão fora da visão de usuário;

O Next.js oferece um componente próprio para usar imagens chamado [`<image>`](<### `<image>`>)  

### `<image>`

o componente `<image>` é a extensão da tag `<img>`, que vem com um automático otimização de imagem:

- Evita mudança de layout automática quando as imagens são carregadas;

- Redimensiona as imagens o que evita o envio de imagens muito largas em dispositivos com view port menor;

- Carregamento lento de imagens por padrão (as imagens são carregas conforme entram na janela de visualização);

- Serve imagens em formatos modernos, como `WebP` ou `AVIF`, quando o navegador suportar.

##### Como adicionar

Iremos adicionar duas imagens no arquivo `/public`. Elas irão se adaptar ao tamanho da tela do usuário.

```tsx /app/page.tsx
import Image from 'next/image';
 
export default function Page() {
  return (
	<div>
      <Image
        src="/hero-desktop.png"
        width={1000}
        height={760}
        className="hidden md:block"
        alt=
        "Screenshots of the dashboard project showing desktop version"
      />
    </div>
  );
}
```

Esta definindo o `width` para `1000` e o `height` para `760` pixels. Assim definindo largura e altura previne o layout shift (mudança de layout), esses valores devem ter uma proporção idêntico a imagem fonte.

Também pode ser usado para classes `hidden` para remover uma imagem de um DOM e usado depois como em telas mobile.

## Adicionando Busca e Paginação

## Fetch datas

Depois de criar e plantar uma database. Existem várias opções para buscar dados (fetch data) para a sua aplicação.

### Camada de API

APIs são uma camada intermediária entre sua aplicação e a database. Existem alguns casos aonde você pode usar uma API:

- Se você está usando serviços em 3rd party que venha de uma API

- Se você está `fetching data` vindo de um client, você vai querer ter um API layer para rodar em server evitando a exposição da database secrets no client

Em Next.js, você pode criar API endpoints usando [Route Handlers](<### Route Handlers>).

### Database queries

Quando você está criando uma aplicação full-stack, as vezes precisará escrever uma lógica para interagir com a database. Como algumas databases como Postgres.

Você pode fazer isso com SQL, ou um ORM como o PRISMA.

Tem alguns casos aonde você pose escrever database queries:

- Quando você está criando seu API endpoints, você precisa escreve código que interaja com sua database.

- Se você está usando componentes de React Server (Procurando dados no server), você pode pular a camada de API, e questionar sua database diretamente sem riscos de expor seus database secrets no client.

### Componentes de Server

Por padrão, as aplicação em Next.js usam o componentes de React Server. procurar dados com um Server componente é relativamente uma abordagem nova e tem alguns benefícios usando eles:

- Server Componentes suporta promises, fornecendo uma solução mais simples para tarefas assíncronas como a busca de dados. Você pode usar a sintaxe `async/await` sem chegar a usar o `useEffect`, `useState` ou outras bibliotecas de buscadores de dados 

- Como mencionado antes, já que os server componentes são executados no servidor, você pode interrogar a database diretamente sem uma camada adicional de API

### SQL

Tem algumas razões para usar SQL em seus projetos:

- SQL é um padrão de industria de muitas databases relativas.

- Tendo o básico de entendimento de SQL ajuda a entender os fundamentos de databases relativas. Permitindo aplicar fundamentos para outras ferramentas.

- SQL é versátil. permitindo procurar e manipular dados especificas.

Para saber como implantar SQL Queries com `Vercel Postgres SDK` siga a página: 
https://nextjs.org/learn/dashboard-app/fetching-data#using-sql

### Requisição em Cascata

Uma "cascata" se refere a uma sequencia de requisições de rede que depende que requisições passadas sejam completadas. No caso da procura de dados, cada requisição poderá só começar quando a anterior for retornada

![[Prints/Pasted image 20240228191009.png]]

```ts /app/dashboard/page.tsx
const revenue = await fetchRevenue();
const latestInvoices = await fetchLatestInvoices(); 
// espere acabar o fetchRevenue()

const {
  numberOfInvoices,
  numberOfCustomers,
  totalPaidInvoices,
  totalPendingInvoices,
} = await fetchCardData(); // wait for fetchLatestInvoices() to finish
```

### Requisição em Paralela

Um jeito comum de evitar "cascatas" é iniciar todas as requisições ao mesmo tempo.

em JavaScript, você pode usar a função `Promise.all()` ou `Promise.allSettled()` para inicia-los ao mesmo tempo. Por exemplo:

```ts
export async function fetchCardData() {
	// ...
    const data = await Promise.all([
      invoiceCountPromise,
      customerCountPromise,
      invoiceStatusPromise,
    ]);
    // ...
  }
}
```

Usando esse padrão, você poderá:

- Começar executando todas as buscas de dados ao mesmo tempo, no qual você pode liderar nos ganhos de performance

- Usar um padrão JavaScript nativo que pode ser aplicado para qualquer biblioteca ou framework

No entanto, tem uma desvantagem confiando apenas no padrão de JavaScript: 

*o que acontece se uma requisição de dado está mais lenta que outras?*

### Tipos de Renderização


#### Renderização Estática

com renderização estática, a busca de dados e a própria renderização acontece no servidor na hora do build (quando faz  o deploy) ou durante a revalidação.
O resultado pode então ser distribuído e armazenado em cache em uma [Content Delivery Network (CDN)](https://nextjs.org/docs/app/building-your-application/rendering/server-components#static-rendering-default).

![[Prints/Captura de tela de 2024-02-29 17-47-13.translated.jpg]]

A qualquer momento que um usuário visita sua aplicação, o resultado do cache está servido ao usuário. Esses são alguns dos benefícios de usar renderização estática:

- **Sites Rápidos** - conteúdo que já é pre-renderizado pode ser armazenado em cache e globalmente distribuído. Essa garantia de que qualquer usuário em qualquer lugar do mundo pode acessar seu site mais rápido e de forma mais confiável.

- **Reduz o carregamento do servidor** - por causa que o conteúdo está armazenado em cache, seu servidor não tem que gerar conteúdo dinamicamente para cada requisição de usuário.

- **SEO** - Conteúdo pre-renderizado é mais fácil de ferramentas de busca rastrearem, como o conteúdo já está disponível quando a página carrega. O site pode ser um dos melhores nos rankings das ferramentas de buscas.

Renderização estática é útil para sua UI sem dados ou dados que só são compartilhados entre usuários. Como um blog estático ou uma página de produtos.

essa ferramenta pode não ser uma boa maneira para usar em dashboards que tem dados personalizados e que está regularmente atualizando. 

#### Renderização Dinâmica

Com a renderização dinâmica, o conteúdo está renderizado no servidor para cada usuário no momento da requisição (quando o usuário visita a página). Existem vários benefícios:

- **Dados em tempo real** - renderização dinâmica permite a sua aplicação mostre em tempo real ou frequentemente atualize dados. É o ideal para aplicações aonde dados são mudados muitas vezes.

- **Conteúdo de Usuário especifico** - É mais fácil fornecer um conteúdo personalizável, tanto em dashboards quanto em perfis de usuários, e e atualizar os dados baseado na interação do usuário.

- **Informação no momento da requisição** - Renderização dinâmica permite que você acesse informação que só poderia ser acessada na momento a requisição, como os cookies ou os parâmetros de pesquisa URL.

#### Pre-renderização parcial

Pre-renderização parcial é um recurso experimental que permite renderizar uma rota com um shell de carregamento estático. Enquanto mantêm algumas partes dinâmicas. Em outra palavras, você pode isolar as partes de uma rota. Por exemplo:

![[Prints/Pasted image 20240307160341.png]]

Quando um usuário visita uma rota:

- Um shell de rota estática é servido, garantindo um carregamento inicial rápido.

- O shell deixa buracos onde o conteúdo dinâmico será carregado de forma assíncrona.

- Os buracos assíncronos são transmitidos em paralelo, reduzindo o tempo de carregamento total da página.

Pre-renderização parcial combina uma entrega de borda estática ultrarrápido com capacidades completamente dinâmicas 

##### Como a pre-renderização parcial funciona?

Pre-renderização parcial alavanca os APIs simultâneas do React e usa [Suspense](<### Streaming um componente>) para adiar partes da renderização de sua aplicação até alguma condição se encontrar

O fallback é embutido dentro do arquivo inicial estático junto com outros conteúdo estático. Na hora de se fazer o build (durante a revalidação), as partes estáticas de uma rota é pre-renderizada, e o resto está adiada até o usuário requisitar a rota.

Vale a pena notando que o envolvimento de um componente em Suspense não faz o componente dinâmico (lembre-se de usar `unstable_noStore` para alcançar esse objetivo), mas sim o Suspense é usado como um limite entre partes estáticas e dinâmicas.

A coisa boa sobre o pre-renderização parcial é que você não precisa mudar o seu código para usa-lo. Contanto que você está usando Suspense para envelopar as partes dinâmicas de uma rota.

### `unstable_noStore` e `noStore`

É uma API de Next.js usado dentro do seu componente de server ou funções de fetching data para excluir a renderização estática. 

```js /app/lib/data.ts
import { unstable_noStore as noStore } from 'next/cache';
 
export async function fetchRevenue() {
  // Adicione noStore() 
  // para evitar que a resposta sejá armazenada em cache.
  // Esse é o equivalente em fetch(..., {cache: 'no-store'}).
  noStore();
 
  // ...
}
 
export async function fetchLatestInvoices() {
  noStore();
  // ...
}
 
export async function fetchCardData() {
  noStore();
  // ...
}
 
```

> nota: `unstable_noStore` é um API experimental e pode mudar no futuro. Se você preferir usar um API instável em seus projetos. você pode também usar [Segment Config Option](https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config) `export const dynamic = "force-dynamic"`

### Simulando uma busca de dados lenta

Fazer um dashboard dinâmico é um bom primeiro passo. No entanto ainda tem o problema que foi mencionado na requisição paralela que se um dado for mais lento que o outro esse dado vai comprometer o seguinte.

```ts /app/lib/data.ts
export async function fetchRevenue() {
  try {
    // Adicionamos um delay artificial de resposta para uma demostração
    // Isso não é feito em produção :)
    console.log('Fetching revenue data...');
    await new Promise((resolve) => setTimeout(resolve, 3000));
 
    const data = await sql<Revenue>`SELECT * FROM revenue`;
 
    console.log('Data fetch completed after 3 seconds.');
 
    return data.rows;
  } catch (error) {
    console.error('Database Error:', error);
    throw new Error('Failed to fetch revenue data.');
  }
}
```

O resultado é que a sua página está bloqueada até seus dados for buscado.

### Streaming

Streaming é uma técnica de transferência de dados que permite você quebrar uma rota em pequenos pedaços e progressivamente transmitir eles do servidor para o cliente quando ele ficar pronto.

![[Prints/Pasted image 20240307111920.png]]

Em streaming, você pode evitar requisição de dados lenta que estão bloqueando toda a sua página. Isso ajuda o usuário a ver e interagir com partes da página sem esperar todos os dados carregar antes de qualquer UI ser mostrada ao usuário.

![[Prints/Pasted image 20240307113628.png]]

Streaming funciona bem com modelos de componentes React aonde cada componente pode ser considerado um pedaço.

Existem 2 maneiras de implementar um streaming in Next.js:

1. Criado na pasta aonde tem o `page`, com o arquivo `loading.tsx`.
2. Com componentes específicos, com `<Suspense>`.

#### `loading.tsx`

Em `/app/dashboard`, crie um novo arquivo chamado `loading.tsx`:

```tsx /app/dashboard/loading.tsx
export default function Loading() {
  return <div>Loading...</div>;
}
```

![[Prints/Pasted image 20240307115951.png]]

Algumas coisa estão acontecendo aqui:

1. `loading.tsx` é um arquivo especial de Next.js construído em cima de Suspense, permite que você crie uma UI de fallback demonstrável para servir como um substituto enquanto seu conteúdo está carregando.

2. Desde então o `sideNav` é estático, mostrando imediatamente. O usuário interage com a `<sideNav>` enquanto o conteúdo dinâmico está carregando.

3. O usuário não tem que esperar a página terminar de carregar para sair dela (isso se chama interruptible navigation)

##### Adicionando esqueleto em Loading

Esse esqueleto de carregamento é uma versão simplificada muitos websites usam ele como um placeholder (ou fallback) para indicar que o conteúdo está carregando. qualquer UI que você colocar dentro de `loading.tsx` será integrada como parte de um arquivo estático, e mandado primeiro.

![[Prints/Pasted image 20240307124740.png]]

#### Streaming um componente

Em vez de carregar toda a página carrega um componente só, pode ser feito usando um componente de React `<Suspense>`.

- Suspense permite adiar a renderização de partes de sua aplicação até alguma condição se encontrar (exemplo: dados carregados). 

- Você pode envolver seu componentes dinâmicos em Suspense. Então passar um componente de fallback para mostrar enquanto o componente dinâmico carrega.

```tsx /app/dashboard/(overview)/page.tsx
import { Suspense } from 'react';

export default async function Page() {
	// ...
  return (
	  // ...
        <Suspense fallback={<RevenueChartSkeleton />}>
          <RevenueChart />
        </Suspense>
    )
}
```

![[Prints/Pasted image 20240307130946.png]]

##### Decidindo aonde colocar limite em Suspense

Aonde colocar limite em Suspense depende de algumas coisas

1. Como você quer que o usuário experiencie a página durante o stream.
2. Que conteúdo você quer priorizar.
3. Se o componente depende dessa busca de dados.


### Resumo de Fetch Data

1. Criar uma base de dados na mesma região que a seu código aplicação para reduzir a latência entre seus servidores e base de dados.

2. Buscas de dados em servidor com [Componentes de Server React](<### Componentes de Server>). Libera que você mantem uma busca de dados rica e uma logica no servidor, reduz o pacote Javascript em client-side, e previne que seus "secrets" na base de dados sejam expostos para o cliente.

3. [SQL](<### SQL>) usado para só fazer a procura de dados que você precisa, reduzindo a maioria dos dados transferidos por cada requisição e a maior parte do javascript precisa para transformar dados "in-memory".

4. Tornar [paralelo](<### Requisição em Paralela>) a busca de dados com JavaScript (aonde faz sentido usar).

5. implementar ["Streaming"](<### Streaming>) para prevenir requisição de dados lenta bloqueando sua página toda, e habilitando o usuário interagir com a UI sem esperar por qualquer coisa carregando.

6. Mover busca de dados para os componentes que precisam deles, por isso isolando quais partes da sua rota aonde deveria ser dinâmica preparando para a [Pre-renderização Parcial](<### Pre-renderização Parcia>).


## Instalando Styled Components no Nextjs

`npm i styled-components`

`npm i -D @types/styled-components`

Devemos instalar os plugins do babel para funcionar o styled component sem erros

`npm i -D babel-plugin-styled-components`

### Exemplo de arquivo

https://github.com/vercel/next.js/tree/deprecated-main/examples/with-styled-components