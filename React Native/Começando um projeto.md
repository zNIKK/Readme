
# Fazendo o Figma

Fazer o exemplo do figma é bastante importante para um projeto novo

https://www.figma.com

#  Criar o projeto

## Instalação
### Pré-requisitos

- Node.js
- Watchman (recomendado para macOS)
- Android Studio e/ou Xcode (para compilar os apps)
- Expo (virtualização de um celular)

### Como instalar

1. **Instalar o Expo CLI**:

```bash
npx create-expo-app@latest my-project
```

1. **Executar o app**:

Entre no diretório do projeto:

```bash
cd my-project
```

Inicie o app:
```bash
npx expo start
```

## Estrutura de Pastas do Projeto

```bash
my-project/ 
└── src/ # Código fonte
	├── add/ # Arquivos para telas diferentes 
	├── assets/ # Imagens e outros arquivos estáticos 
	├── components/ # Componentes em React Native
	├── storage/ # Arquivos para guardar no cache (AsyncStorage)
	└── styles/ # Arquivos para estilização 
├── package.json # Lista de dependências e scripts 
└── ...
```

## Criando Index principal

Arquivo que contem tela inicial do seu aplicativo:

`src/app/index/index.tsx` 
```tsx
import { Text, View } from "react-native";

export default function Index() {
	return (
		<View>
			<Text>Hello World</Text>
		</View>
	)
}
```


## Criando layout

Arquivo padrão aplicado em todos os arquivos

```tsx
import { Stack } from "expo-router";
import { colors } from "../styles/colors";

export default function Layout() {
    const backgroundColor = colors.gray[900]

    return <Stack screenOptions={{
        headerShown: false,
        contentStyle: {backgroundColor},
    }}/>
}
```


# Estilização
O React Native usa um sistema de estilo similar ao CSS, mas com algumas diferenças. A propriedade `style` pode ser usada em qualquer componente, e os estilos são passados como objetos JavaScript.

Exemplo:
```jsx
import { StyleSheet, View, Text } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  text: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
});

const App = () => (
  <View style={styles.container}>
    <Text style={styles.text}>Hello, React Native!</Text>
  </View>
);
```

## Padronização

A padronização é umas das principals coisas quando falamos em organização e produtividade. Até porque quanto mais organizado seu código, mais legível ele será.

A padronização tem mais eficacia com componentes, ou seja se um elemento se repete em sua página.

A padronização deve seguir:

- Temas de cores
- Temas de fontes
- Tamanhos e estilos de textos
- Tamanhos de imagens e de Ícones
-  mapeamento de caminhos import

## Styled Components

Como o próprio nome diz são componentes estilizados, conhecido como 
`CSS-in-JS`

### Instalação

```bash
npm install styled-components
```


### Criando os temas da sua aplicação 

Criar temas para sua aplicação ajuda na organização de seu aplicativo e na produtividade. Criando cores, fontes padrões.


Crie uma pasta `src/theme/index.ts` aonde ficara um objeto com os temas padrões

```ts
export default {
    COLORS: {
      WHITE: '#FFFFFF',
  
      GREEN_700: '#00875F',
      GREEN_500: '#00B37E',
  
      RED: '#F75A68',
      RED_DARK: '#AA2834',
  
      GRAY_700: '#121214',
      GRAY_600: '#202024',
      GRAY_500: '#29292E',
      GRAY_400: '#323238',
      GRAY_300: '#7C7C8A',
      GRAY_200: '#C4C4CC',
      GRAY_100: '#E1E1E6'
    },
    FONT_FAMILY: {
      REGULAR: 'Roboto_400Regular',
      BOLD: 'Roboto_700Bold'
    },
    FONT_SIZE: {
      SM: 14,
      MD: 16,
      LG: 18,
      XL: 24
    }
  };
```


#### Theme Provider

Serve para gerenciar e fornecer um tema global para os componentes estilizados em uma aplicação React. Ele permite que você defina um conjunto de valores (como cores, espaçamentos, fontes, etc.) que podem ser 
reutilizados em qualquer parte da aplicação sem a necessidade de repetição.

`/app.tsx`
```tsx
import { ThemeProvider } from "styled-components";
import theme from "@/src/theme";

export default function App() {
    return (
        <ThemeProvider theme={theme}>
            <Groups />
        </ThemeProvider>
    )
}
```

como usar:

`/src/screens/Groups/style.ts`
```ts
import styled from 'styled-components/native';

export const Container = styled.View`
  flex: 1;
  background-color: ${({ theme }) => theme.COLORS.GRAY_300};
  align-items: center;
  justify-content: center;
`;
```

##### Tipagem

Esse tipo de estilização precisa de tipagem em typescript. Assim devemos criar um arquivo `@types/styled.d.ts`

`/src/@types/styled.d.ts`
```ts
import 'styled-components/native';
import theme from '../theme';

declare module 'styled-components/native' {
  type ThemeType = typeof theme;

  export interface DefaultTheme extends ThemeType { }
}
```

### Mudar atributos de um componente

Para mudar a estilização de um componente já feito precisamos mudar o atributo dele usando o `attrs()` no styled component

exemplo quero mudar a cor do componente de loading chamado `ActivityIndicator`

```ts
export const LoadingIndicator = styled.ActivityIndicator.attrs(({ theme }) => ({
    color: 'red',
}))``;
```

### Mudar componente não padrão

```tsx
import { CaretLeft } from 'phosphor-react-native';

// estilizando o componente do phosphor e os atributos dele
export const BackIcon = styled(CaretLeft).attrs(( {theme} ) => ({
    color: theme.COLORS.WHITE,
    size: 36
}))`
```

## Path Mapping
Ao decorrer do projeto os caminhos de `import` se tornaram caminhos grandes e complexos assim o `path mapping` ajudará seu projeto a ficar mais legível 

Vamos usar o `babel-plugin-module-resolver`

```js
// Sem o Path Mapping
import UtilsFn from '../../../../../utils/UtilsFn'

// Com o Path Mapping
import UtilsFn from 'utils/UtilsFn'
```

### instalação

```bash
npm install --save-dev babel-plugin-module-resolver
```

### Criar um arquivo de configuração

`.babel.config.js` arquivo raiz com configurações de seus alias

```js
{
  "plugins": [
    ["module-resolver", {
      "root": ["./src"],
      "alias": {
	    // nome do alias : para onde apontar
        "@assets": "./src/assets",
        "@screens": "./src/screens",
      }
    }]
  ]
}
```

### Tipagem dos alias

em `tsconfig.json`

```json
...
{
	...
	"baseUrl": "./",
      "@assets/*": [
        "./src/assets/*"
      ],
      "@screens/*": [
        "./src/screens/*"
      ],      
    }
    ...
}
...
```


## Hacks

### Criar um componente que tem dois estados ao mesmo tempo

Exemplo de botão que tem dois tipos o primário e o secundário:
```ts
// crie uma string para que possa mudar
export type ButtonTypeStyleProps = 'PRIMARY' | 'SECONDARY';

// tipagem do Props para passar as propiedades 
type Props = {
    type: ButtonTypeStyleProps;
}
```

aqui eu faço uma condição se o type for igual a "PRIMARY" use a cor verde se não use a vermelha:
```ts
export const Container = styled(TouchableOpacity)<Props>`
	background-color: ${({ theme, type }) => type === 'PRIMARY' ? green : red};
`
```



## Fontes

Também nas estilização de seu projeto temos as fontes. O próprio expo tem ferramentas para facilitar sua produtividade como o `expo-font`

`npx expo install expo-font`

#### Google fonts

Existem vários metodos de adicionar fontes em seu projeto usando expo, a google fonts é o que se destaca mais:

```bash
npx expo install expo-font @expo-google-fonts/roboto
```

`/app.tsx`
```tsx
import { ActivityIndicator } from "react-native";

// tipos de fontes instaladas
import { useFonts, Roboto_400Regular, Roboto_700Bold  } from '@expo-google-fonts/roboto'

export default function App() {
	// hook para carregar fontes
    const [ fontsLoaded ] =  useFonts({ Roboto_400Regular, Roboto_700Bold});


    return (
        <ThemeProvider theme={theme}>
	        // enqunto a fonte não for carregada 
		        ele ira carregar a pagina 
            {fontsLoaded ? <Groups />  : <ActivityIndicator />}
        </ThemeProvider>
    )
}
```

## Ícones

### phosphor icon

Biblioteca para usar ícones em seu projeto

procurar um ícone:
https://phosphoricons.com/

```bash
npm install --save phosphor-react-native
```

escolha um ícone e use ele como um componente normal do react:
```tsx
// icone de seta para a esquerda
import { CaretLeft } from 'phosphor-react-native';

export function Header() {
    return(
        <CaretLeft color="#fff" size={32} />
    );
};
```
