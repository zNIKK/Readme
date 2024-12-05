 
# Começando

React Native é uma estrutura para construir aplicativos móveis nativos usando JavaScript e React. Ele permite que você crie aplicativos para **iOS** e **Android** com um único código base.

## O que é React Native?

**React Native** é uma estrutura de desenvolvimento de software criada pelo Facebook. Ela permite construir **aplicativos móveis nativos** para **iOS** e **Android** usando **JavaScript** e **React**, o que facilita o desenvolvimento multiplataforma com um único código base.

---

## Características Principais

### 1. **Desenvolvimento Multiplataforma**
- **Código único**: Com React Native, você escreve uma única base de código JavaScript para ambos iOS e Android, o que reduz o tempo de desenvolvimento e facilita a manutenção.
- **Componentes nativos**: Embora o código seja escrito em JavaScript, os componentes são convertidos em elementos nativos, proporcionando uma experiência semelhante à de aplicativos nativos.

### 2. **Componentes Declarativos**
- A abordagem de desenvolvimento é declarativa, facilitando a criação de interfaces de usuário de forma previsível e organizada, utilizando **componentes reutilizáveis**.

### 3. **Hot Reload e Fast Refresh**
- Permite que os desenvolvedores vejam as mudanças de código em tempo real sem a necessidade de recompilar o aplicativo a cada alteração, tornando o processo de desenvolvimento mais ágil.

### 4. **Acesso a APIs Nativas**
- Você pode acessar APIs nativas de dispositivos como a câmera, GPS, armazenamento e outros serviços do sistema operacional, permitindo que o aplicativo tenha funcionalidades avançadas.

---

## Principais Vantagens

### 1. **Desenvolvimento Rápido**
- Com o **Hot Reload** e o compartilhamento de código entre plataformas, o ciclo de desenvolvimento é significativamente reduzido.

### 2. **Grande Comunidade e Suporte**
- Como o React Native é baseado no React e tem suporte da comunidade JavaScript, há uma grande quantidade de bibliotecas, pacotes e tutoriais disponíveis para ajudar no desenvolvimento.
### 3. **Performance Próxima ao Nativo**
- Embora use JavaScript, o React Native é capaz de oferecer uma performance próxima aos aplicativos nativos ao converter o código JavaScript em componentes nativos no dispositivo.

---

## Limitações

### 1. **Acesso Limitado a APIs Nativas**
- Para funcionalidades mais complexas, como gráficos 3D ou integração com algumas APIs do sistema, pode ser necessário escrever código nativo em **Swift** (iOS) ou **Java/Kotlin** (Android).

### 2. **Performance Inferior ao Nativo em Aplicações Pesadas**
- Para aplicações com muitas animações complexas ou que exigem alto desempenho (como jogos), a performance pode não ser tão boa quanto a de um aplicativo nativo.

### 3. **Diferenças entre iOS e Android**
- Mesmo com um código base compartilhado, ainda existem diferenças no comportamento de certos componentes entre as plataformas, exigindo ajustes específicos.

---

## Estrutura de Componentes

React Native possui um conjunto de **componentes pré-construídos** que facilitam a criação de interfaces:

### Exemplos:
- **View**: Container básico para layouts.
- **Text**: Para exibir texto.
- **Image**: Exibir imagens.
- **TextInput**: Entrada de texto.
- **ScrollView**: Exibir conteúdos com rolagem.
- **Button**: Botões de interação.

Estes componentes são semelhantes aos tags de HTML, mas mapeiam diretamente para componentes nativos do iOS e Android.

![[imagens/Componentes React Native.png]]


# [[Componentes React Native]]

---

## Estrutura de arquivos e pastas

A estrutura do React Native consiste em:

- **/app** - [rotas](##Navegação)
- **/assets/fonts** - fontes
- **/assets/images** - imagens
- **/components** - Componentes
- **/constants** - Estilização
- **app.json** - arquivo de configuração

# Navegação
Para navegação entre telas, o React Native utiliza a biblioteca `react-navigation`.

### **Estrutura de Navegação**

O React Navigation usa um conceito de **navegação por pilha** (stack navigation), onde as telas são empilhadas umas sobre as outras, permitindo o controle de navegação para frente (push) e para trás (pop).

- **Stack Navigator**: É o método mais comum de navegação, onde as telas são empilhadas e você pode ir de uma tela a outra. A tela anterior fica na memória até que seja removida ou o usuário volte.
- **Bottom Tab Navigator**: Organiza diferentes telas como abas, geralmente na parte inferior da tela.
- **Drawer Navigator**: Adiciona um menu lateral que desliza para mostrar opções de navegação.

### **Configuração de um Stack Navigator**

O `Stack Navigator` permite navegação entre diferentes telas de maneira linear. Veja como configurar:

```jsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './HomeScreen';
import DetailsScreen from './DetailsScreen';

const Stack = createStackNavigator();

function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

export default App;
```

- **`NavigationContainer`**: É um contêiner que envolve toda a aplicação e gerencia o estado de navegação.
- **`Stack.Navigator`**: Define o tipo de navegação (neste caso, por pilha).
- **`Stack.Screen`**: Define cada tela que faz parte da pilha de navegação, com um nome e o componente correspondente.

### **Navegação entre Telas**

Para navegar entre telas, você usa o método `navigation.navigate()` fornecido como uma prop ao componente:

   ```jsx
   function HomeScreen({ navigation }) {
     return (
       <Button
         title="Go to Details"
         onPress={() => navigation.navigate('Details')}
       />
     );
   }
   ```

1. **Passagem de Parâmetros**:
   Você pode passar parâmetros ao navegar entre telas:

   ```jsx
   onPress={() => navigation.navigate('Details', { itemId: 42 })}
   ```

   E, na tela de destino, acessar esses parâmetros assim:

   ```jsx
   function DetailsScreen({ route }) {
     const { itemId } = route.params;
     return <Text>Item ID: {itemId}</Text>;
   }
   ```

2. **Voltar entre Telas**:
   O método `navigation.goBack()` permite retornar à tela anterior:

   ```jsx
   navigation.goBack();
   ```

### Outros tipos de navegação

- **Tab Navigation**: Usa abas para alternar entre diferentes seções de uma aplicação.
- **Drawer Navigation**: Usa um menu que desliza da lateral da tela para navegação em diferentes áreas do app.



## Instalação:
```bash
npm install @react-navigation/native
npm install @react-navigation/stack
```

## Hooks

No React Native, a navegação é frequentemente gerenciada usando a biblioteca **React Navigation**, que oferece uma série de hooks para facilitar a navegação entre telas. Abaixo, estão listados os hooks mais comuns usados para navegação com **React Navigation**:

### 1. **useNavigation**
O `useNavigation` é um hook que fornece acesso ao objeto de navegação. Ele permite navegar entre telas de qualquer lugar no seu componente, sem a necessidade de passar explicitamente o objeto `navigation` como prop.

```javascript
import { useNavigation } from '@react-navigation/native';

const MyComponent = () => {
  const navigation = useNavigation();

  const navigateToDetails = () => {
    navigation.navigate('Details');
  };

  return (
    <Button title="Go to Details" onPress={navigateToDetails} />
  );
};
```

### 2. **useRoute**
O `useRoute` é um hook que fornece acesso ao objeto `route` da tela. Esse hook permite acessar parâmetros passados para a tela via navegação.

```javascript
import { useRoute } from '@react-navigation/native';

const MyComponent = () => {
  const route = useRoute();
  const { itemId, otherParam } = route.params;

  return (
    <Text>Item ID: {itemId}</Text>
  );
};
```

### 3. **useIsFocused**
O `useIsFocused` é um hook que retorna um valor booleano indicando se a tela está atualmente focada. Esse hook é útil para fazer algo quando a tela ganha ou perde o foco, como iniciar ou parar animações.

```javascript
import { useIsFocused } from '@react-navigation/native';

const MyComponent = () => {
  const isFocused = useIsFocused();

  useEffect(() => {
    if (isFocused) {
      // A tela está focada, pode carregar dados, iniciar animações, etc.
    }
  }, [isFocused]);

  return (
    <Text>{isFocused ? 'Tela Focada' : 'Tela Não Focada'}</Text>
  );
};
```

### 4. **useBackButton**
O `useBackButton` permite gerenciar o comportamento do botão "voltar" no dispositivo Android ou o botão de navegação. Ele permite adicionar funcionalidades personalizadas ao comportamento do botão de voltar, como navegar para a tela anterior ou evitar que a navegação volte.

```javascript
import { useBackButton } from '@react-navigation/native';

const MyComponent = () => {
  useBackButton(() => {
    console.log('Botão Voltar pressionado!');
    // Impedir o comportamento padrão ou customizar
    return true;
  });

  return <Text>Pressione o botão Voltar</Text>;
};
```

### 5. **useFocusEffect**
O `useFocusEffect` é semelhante ao `useEffect`, mas é executado sempre que a tela ganha foco (diferente de `useEffect`, que é executado apenas uma vez após a montagem do componente).

```javascript
import { useFocusEffect } from '@react-navigation/native';

const MyComponent = () => {
  useFocusEffect(
    React.useCallback(() => {
      console.log('Tela ganhou foco!');
      return () => {
        console.log('Tela perdeu o foco!');
      };
    }, [])
  );

  return <Text>Tela com efeito de foco</Text>;
};
```

### 6. **useLinking**
O `useLinking` permite configurar a navegação de link profundo (deep linking). Ele fornece hooks para configurar como os links são gerenciados no aplicativo. Usado principalmente para integração com links externos (como URLs), mas também pode ser útil para configurar navegação interna.

```javascript
import { useLinking } from '@react-navigation/native';

const MyComponent = () => {
  const { getInitialURL, getPathFromState } = useLinking();

  useEffect(() => {
    async function checkURL() {
      const url = await getInitialURL();
      console.log(url);
    }
    checkURL();
  }, []);

  return <Text>Linking no React Navigation</Text>;
};
```

### 7. **useNavigationState**
O `useNavigationState` permite acessar e manipular o estado de navegação atual. Isso é útil quando você precisa acessar informações sobre o estado atual da navegação, como qual é a tela ativa ou o histórico de navegação.

```javascript
import { useNavigationState } from '@react-navigation/native';

const MyComponent = () => {
  const routeIndex = useNavigationState(state => state.index);

  return <Text>Índice da rota atual: {routeIndex}</Text>;
};
```

---

## Exemplo de uso
```jsx
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './HomeScreen';
import DetailsScreen from './DetailsScreen';

const Stack = createStackNavigator();

const App = () => (
  <NavigationContainer>
    <Stack.Navigator initialRouteName="Home">
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Details" component={DetailsScreen} />
    </Stack.Navigator>
  </NavigationContainer>
);
```

---
# Instalação

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

## Para mais detalhes

- [[Começando um projeto]]

---

# API nativa
O React Native permite que você use APIs nativas como a câmera, GPS e armazenamento. Isso pode ser feito através de bibliotecas de terceiros ou escrevendo módulos nativos personalizados.

### Exemplo de acesso à câmera com a biblioteca `react-native-camera`:
```bash
npm install react-native-camera
```
```jsx
import { RNCamera } from 'react-native-camera';

const App = () => (
  <RNCamera
    style={{ flex: 1 }}
    type={RNCamera.Constants.Type.back}
    captureAudio={false}
  />
);
```

### [[Componentes React Native#API Nativas|Todas as API's Nativas]]

---

# Debugging
## Ferramentas de Debugging:
- **React Developer Tools**: Para inspecionar componentes React.
- **Console.log**: Pode ser usado diretamente no código.
- **Remote Debugging**: Conectar o app ao Chrome DevTools para debugar código JavaScript.
- **React Native Debugger**: Ferramenta completa que combina DevTools com funcionalidades de Redux.

## Exemplo:
Para habilitar o Debugging remoto, abra o Dev Menu (`Cmd+D` no iOS ou `Cmd+M` no Android) e selecione "Debug".

---

# Publicação
## iOS:
1. Configure sua conta de desenvolvedor Apple.
2. No Xcode, configure as informações de assinatura.
3. Gere um **.ipa** e publique na App Store via App Store Connect.

## Android:
1. Gere uma **keystore** para assinar seu aplicativo.
2. Atualize o arquivo `gradle.properties` com as credenciais da keystore.
3. Execute o build:
   ```bash
   npx react-native run-android --variant=release
   ```
4. Publique o **.apk** no Google Play Console.

---

# Bibliotecas Externas
React Native possui uma vasta gama de bibliotecas externas para diversas funcionalidades.

## Algumas bibliotecas populares:
- **Axios**: Para chamadas HTTP.
  ```bash
  npm install axios
  ```
- **React Native Maps**: Integração com mapas do Google.
  ```bash
  npm install react-native-maps
  ```
- **Lottie**: Para animações.
  ```bash
  npm install lottie-react-native
  ```

---
