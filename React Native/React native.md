
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

---

## Estrutura de arquivos e pastas

A estrutura do React Native consiste em:

- **/app** - [rotas](##Navegação)
- **/assets/fonts** - fontes
- **/assets/images** - imagens
- **/components** - Componentes
- **/constants** - Estilização
- **app.json** - arquivo de configuração

## Navegação


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

# Instalação

## Pré-requisitos

- Node.js
- Watchman (recomendado para macOS)
- Android Studio e/ou Xcode (para compilar os apps)
- Expo (virtualização de um celular)

## Como instalar

1. **Instalar a CLI do React Native**:

```bash
npx react-native init MyApp
```

2. **Executar o app**:

Para iOS:

```bash
npx react-native run-ios
```

Para Android:

```bash
npx react-native run-android
```

---

# Componentes Básicos
## 1. `View`
Container básico que suporta layout com flexbox, estilo, toques e outros controles de interface do usuário.
```jsx
import { View } from 'react-native';

const App = () => (
  <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
    {/* Conteúdo aqui */}
  </View>
);
```

## 2. `Text`
Usado para exibir texto na tela.
```jsx
import { Text } from 'react-native';

const App = () => <Text>Hello, World!</Text>;
```

## 3. `Image`
Exibe uma imagem, seja local ou da internet.
```jsx
import { Image } from 'react-native';

const App = () => (
  <Image source={{ uri: 'https://example.com/image.png' }} style={{ width: 100, height: 100 }} />
);
```

## 4. `TextInput`
Caixa de texto para entrada de dados.
```jsx
import { TextInput } from 'react-native';

const App = () => (
  <TextInput placeholder="Digite algo" style={{ borderWidth: 1, padding: 10 }} />
);
```

## 5. `ScrollView`
Componente de rolagem para exibir conteúdos longos.
```jsx
import { ScrollView, Text } from 'react-native';

const App = () => (
  <ScrollView>
    <Text>Texto longo aqui...</Text>
  </ScrollView>
);
```

## 6. `Button`
Botão simples que pode disparar ações ao ser pressionado.
```jsx
import { Button } from 'react-native';

const App = () => <Button title="Press me" onPress={() => alert('Pressed!')} />;
```

# Componentes Avançados

## 1. **FlatList e SectionList**

- **FlatList** é ideal para listas grandes e performáticas, com recursos como carregamento sob demanda (scroll infinito) e controle de performance.
- **SectionList** funciona bem para listas agrupadas, especialmente quando há necessidade de dividir a lista em seções, como categorias.

```tsx
import React from 'react';
import { View, Text, FlatList } from 'react-native';

const data = [
  { id: '1', title: 'Item 1' },
  { id: '2', title: 'Item 2' },
  { id: '3', title: 'Item 3' },
];

export default function App() {
  return (
    <FlatList
      data={data}
      keyExtractor={(item) => item.id}
      renderItem={({ item }) => (
        <View>
          <Text>{item.title}</Text>
        </View>
      )}
    />
  );
}

```

## 2. **Reanimated**

- A biblioteca **Reanimated** permite criar animações complexas e fluidas. É ideal para animações baseadas em gestos, e você pode usá-la em conjunto com a biblioteca Gesture Handler.
- Oferece uma abordagem baseada em "worklets", que são executados diretamente na camada de UI nativa, melhorando a performance das animações.

Instale o pacote:

```bash
npm install react-native-reanimated
```

```tsx
import React from 'react';
import { Button } from 'react-native';
import Animated, { useSharedValue, useAnimatedStyle, withSpring } from 'react-native-reanimated';

export default function App() {
  const offset = useSharedValue(0);

  const animatedStyle = useAnimatedStyle(() => {
    return {
      transform: [{ translateX: offset.value }],
    };
  });

  return (
    <>
      <Animated.View style={[{ width: 100, height: 100, backgroundColor: 'blue' }, animatedStyle]} />
      <Button onPress={() => (offset.value = withSpring(offset.value === 0 ? 100 : 0))} title="Move" />
    </>
  );
}

```

## 3. **React Native Gesture Handler**

- Para gestos como _swipe_, _pinch_, e _drag_, o **React Native Gesture Handler** permite detectar esses gestos com mais precisão e performance.
- Muito útil para criar componentes como carrosséis, sliders, e botões de swipe.

Instale o pacote:
```bash
npm install react-native-gesture-handler
```

Exemplo com um gesto de arraste:

```jsx
import React from 'react';
import { View, Text } from 'react-native';
import { GestureDetector, Gesture } from 'react-native-gesture-handler';

export default function App() {
  const dragGesture = Gesture.Pan()
    .onUpdate((event) => {
      console.log(event.translationX, event.translationY);
    });

  return (
    <GestureDetector gesture={dragGesture}>
      <View style={{ width: 100, height: 100, backgroundColor: 'red' }}>
        <Text>Drag me</Text>
      </View>
    </GestureDetector>
  );
}
```


## 4. **Drawer Navigator e Bottom Tabs (React Navigation)**

- Para navegação avançada, o **React Navigation** oferece várias opções, como Drawer Navigator para menus laterais e Bottom Tabs para criar navegação tabulada na parte inferior.
- Permite a criação de rotas aninhadas e navegação condicional, importante para fluxos complexos.

Instale o pacote:
```bash
npm install @react-navigation/native @react-navigation/drawer
```

Exemplo de navegação com drawer:

```jsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createDrawerNavigator } from '@react-navigation/drawer';
import { Text } from 'react-native';

const HomeScreen = () => <Text>Home Screen</Text>;
const SettingsScreen = () => <Text>Settings Screen</Text>;

const Drawer = createDrawerNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator>
        <Drawer.Screen name="Home" component={HomeScreen} />
        <Drawer.Screen name="Settings" component={SettingsScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

## 5. **Animated API**

- A API **Animated** do React Native é ideal para criar animações suaves de transformações de objetos, cores, opacidade e posições.
- Com ela, é possível criar animações de rotação, deslizamento, expansão e até efeitos visuais mais complexos.


```jsx
import React, { useRef } from 'react';
import { View, Animated, Button } from 'react-native';

export default function App() {
  const fadeAnim = useRef(new Animated.Value(0)).current;

  const fadeIn = () => {
    Animated.timing(fadeAnim, {
      toValue: 1,
      duration: 1000,
      useNativeDriver: true,
    }).start();
  };

  return (
    <View>
      <Animated.View style={{ opacity: fadeAnim, width: 100, height: 100, backgroundColor: 'blue' }} />
      <Button title="Fade In" onPress={fadeIn} />
    </View>
  );
}
```


## 6. **Modals e ActionSheets**

- Para criar _pop-ups_ ou menus temporários, você pode usar componentes de Modal do React Native ou pacotes como o **React Native ActionSheet**.
- O Modal é útil para janelas de confirmação ou formulários, enquanto o ActionSheet é ideal para opções de seleção rápidas.

Exemplo usando o componente Modal:

```jsx
import React, { useState } from 'react';
import { View, Text, Button, Modal } from 'react-native';

export default function App() {
  const [modalVisible, setModalVisible] = useState(false);

  return (
    <View>
      <Button title="Show Modal" onPress={() => setModalVisible(true)} />
      <Modal visible={modalVisible} transparent={true}>
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center', backgroundColor: 'rgba(0,0,0,0.5)' }}>
          <Text>Modal Content</Text>
          <Button title="Close" onPress={() => setModalVisible(false)} />
        </View>
      </Modal>
    </View>
  );
}
```

## 7. **Camera e Media Library**

- Para acessar a câmera e a galeria de fotos, use bibliotecas como **React Native Camera** ou **React Native Image Picker**.
- Isso permite funcionalidades de captura de imagem, vídeo e seleção de mídia com opções de customização.

Instale o pacote:
```bash
npm install react-native-image-picker
```

Exemplo de uso de câmera:

```jsx
import React from 'react';
import { Button, Image } from 'react-native';
import { launchCamera } from 'react-native-image-picker';

export default function App() {
  const [photo, setPhoto] = React.useState(null);

  const takePhoto = () => {
    launchCamera({ mediaType: 'photo' }, (response) => {
      if (response.assets) {
        setPhoto(response.assets[0].uri);
      }
    });
  };

  return (
    <>
      <Button title="Take Photo" onPress={takePhoto} />
      {photo && <Image source={{ uri: photo }} style={{ width: 100, height: 100 }} />}
    </>
  );
}
```


## 8. **Maps**

- Para integração com mapas, o **React Native Maps** permite exibir mapas com marcações, geolocalização e rotas.
- É útil para aplicações que envolvem localização, como aplicativos de entrega ou de transporte.

Instale o pacote:
```bash
npm install react-native-maps
```

Exemplo de mapa básico:

```jsx
import React from 'react';
import MapView, { Marker } from 'react-native-maps';

export default function App() {
  return (
    <MapView style={{ flex: 1 }} initialRegion={{ latitude: 37.78825, longitude: -122.4324, latitudeDelta: 0.0922, longitudeDelta: 0.0421 }}>
      <Marker coordinate={{ latitude: 37.78825, longitude: -122.4324 }} title="Marker" description="Description" />
    </MapView>
  );
}
```


## 9. **WebView**

- Quando precisar renderizar conteúdo da web, o **React Native WebView** permite incorporar páginas web diretamente no aplicativo.
- É útil para exibir documentos, vídeos externos ou até módulos interativos como chatbots.

Instale o pacote:
```bash
npm install react-native-webview
```

Exemplo de WebView:

```jsx
import React from 'react';
import { WebView } from 'react-native-webview';

export default function App() {
  return <WebView source={{ uri: 'https://reactnative.dev/' }} style={{ flex: 1 }} />;
}
```


## 10. **SVG e Gráficos (React Native SVG)**

- A biblioteca **React Native SVG** permite trabalhar com gráficos vetoriais. Combinada com bibliotecas como **Victory Native** ou **Recharts**, você pode criar gráficos e visualizações de dados interativas.

Instale o pacote:
```bash
npm install react-native-svg
```

Exemplo de SVG:

```jsx
import React from 'react';
import Svg, { Circle } from 'react-native-svg';

export default function App() {
  return (
    <Svg height="100" width="100">
      <Circle cx="50" cy="50" r="45" stroke="blue" strokeWidth="2.5" fill="green" />
    </Svg>
  );
}
```


---

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

---

# Navegação
Para navegação entre telas, o React Native utiliza a biblioteca `react-navigation`.

### Instalação:
```bash
npm install @react-navigation/native
npm install @react-navigation/stack
```

### Exemplo de uso:
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

## API nativa
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

---

## Debugging
### Ferramentas de Debugging:
- **React Developer Tools**: Para inspecionar componentes React.
- **Console.log**: Pode ser usado diretamente no código.
- **Remote Debugging**: Conectar o app ao Chrome DevTools para debugar código JavaScript.
- **React Native Debugger**: Ferramenta completa que combina DevTools com funcionalidades de Redux.

### Exemplo:
Para habilitar o Debugging remoto, abra o Dev Menu (`Cmd+D` no iOS ou `Cmd+M` no Android) e selecione "Debug".

---

## Publicação
### iOS:
1. Configure sua conta de desenvolvedor Apple.
2. No Xcode, configure as informações de assinatura.
3. Gere um **.ipa** e publique na App Store via App Store Connect.

### Android:
1. Gere uma **keystore** para assinar seu aplicativo.
2. Atualize o arquivo `gradle.properties` com as credenciais da keystore.
3. Execute o build:
   ```bash
   npx react-native run-android --variant=release
   ```
4. Publique o **.apk** no Google Play Console.

---

## Bibliotecas Externas
React Native possui uma vasta gama de bibliotecas externas para diversas funcionalidades.

### Algumas bibliotecas populares:
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
