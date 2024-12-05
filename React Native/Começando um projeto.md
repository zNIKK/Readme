	
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

### Estrutura de Pastas do Projeto

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

### Criando Index principal

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


### Criando layout

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

### Exemplo:
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

# Path Mapping
Ao decorrer do projeto os caminhos de `import` se tornaram caminhos grandes e complexos assim o `path mapping` ajudará seu projeto a ficar mais legível 

Vamos usar o `babel-plugin-module-resolver`

```js
// Sem o Path Mapping
import UtilsFn from '../../../../../utils/UtilsFn'

// Com o Path Mapping
import UtilsFn from 'utils/UtilsFn'
```

## instalação

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