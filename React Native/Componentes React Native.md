---
sticker: ""
color: ""
---

# Componentes de interfaces
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

## 4. ImageBackground
O componente `ImageBackground` do React Native permite que você exiba uma imagem de fundo dentro de um contêiner e coloque outros elementos sobre essa imagem, como texto, botões ou qualquer outro componente.

### Características principais do `ImageBackground`:
- **Imagem de fundo**: Exibe uma imagem como background para a área definida pelo componente.
- **Conteúdo sobreposto**: Permite adicionar filhos dentro do componente, como se fosse um `View`, e esses elementos ficam sobrepostos à imagem de fundo.
- **Estilização**: Suporta estilos para definir o tamanho, posição e aparência da imagem e dos elementos sobrepostos.

### Exemplo de uso:

```javascript
import React from 'react';
import { ImageBackground, Text, StyleSheet } from 'react-native';

const App = () => (
  <ImageBackground 
    source={{ uri: 'https://example.com/background.jpg' }}
    style={styles.background}
  >
    <Text style={styles.text}>Texto sobre a imagem de fundo</Text>
  </ImageBackground>
);

const styles = StyleSheet.create({
  background: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    color: 'white',
    fontSize: 24,
    fontWeight: 'bold',
  },
});

export default App;
```

### Propriedades principais:
- **source**: Define a imagem a ser exibida (pode ser uma URL ou imagem local).
- **style**: Estilos aplicados à área de fundo (ex.: dimensões, alinhamento, etc.).
- **resizeMode**: Define como a imagem deve se ajustar ao contêiner (ex.: `cover`, `contain`, etc.).

Assim, `ImageBackground` é uma ótima opção para criar uma interface com imagens de fundo e conteúdo sobreposto de forma prática e flexível.

## 5. `TextInput`
Caixa de texto para entrada de dados.
```jsx
import { TextInput } from 'react-native';

const App = () => (
  <TextInput placeholder="Digite algo" style={{ borderWidth: 1, padding: 10 }} />
);
```

## 6. `ScrollView`
Componente de rolagem para exibir conteúdos longos.
```jsx
import { ScrollView, Text } from 'react-native';

const App = () => (
  <ScrollView>
    <Text>Texto longo aqui...</Text>
  </ScrollView>
);
```


## 7. **FlatList e SectionList**
- **FlatList** é ideal para listas grandes e performáticas, com recursos como carregamento sob demanda (scroll infinito) e controle de performance.
- **SectionList** funciona bem para listas agrupadas, especialmente quando há necessidade de dividir a lista em seções, como categorias.
- **VirtualizedList** 

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

## 8. Pressable

O componente `Pressable` do React Native é um componente que permite capturar interações de toque de forma flexível e responsiva. Com ele, você pode adicionar feedback visual e reagir a diferentes estados de interação (como pressionado, solto ou focado), oferecendo mais controle do que os componentes `Touchable`.

### Características principais do `Pressable`:

- **Flexibilidade de Interação**: `Pressable` oferece várias propriedades de callback que permitem capturar eventos específicos, como `onPressIn`, `onPressOut`, `onLongPress` e `onPress`.
- **Feedback Visual Condicional**: Permite alterar a aparência do componente dependendo do estado de toque, como quando o usuário está pressionando ou soltando.
- **Controle sobre Estados**: Propriedades como `hovered`, `focused` e `pressed` ajudam a estilizar o componente de acordo com o estado atual.

### Exemplo de uso:

```javascript
import React from 'react';
import { Pressable, Text, StyleSheet } from 'react-native';

const App = () => (
  <Pressable
    style={({ pressed }) => [
      styles.button,
      { backgroundColor: pressed ? 'darkblue' : 'blue' }
    ]}
    onPress={() => alert('Button Pressed')}
  >
    <Text style={styles.text}>Press Me</Text>
  </Pressable>
);

const styles = StyleSheet.create({
  button: {
    padding: 10,
    borderRadius: 5,
    alignItems: 'center',
  },
  text: {
    color: 'white',
    fontWeight: 'bold',
  },
});

export default App;
```

### Propriedades principais:
- **onPress**: Chamado quando o componente é pressionado.
- **onPressIn** e **onPressOut**: Chamados respectivamente quando o toque começa e termina.
- **onLongPress**: Chamado quando o toque é mantido por mais tempo.
- **style**: Recebe uma função que usa o estado (`pressed`, `hovered`, etc.) para alterar o estilo dinamicamente.

### Quando Usar `Pressable`:
Use `Pressable` sempre que precisar de um controle detalhado sobre o comportamento de toque e feedback visual, como em botões customizados, links e áreas interativas.

## 9. TouchableOpacity

No React Native, o componente `Touchable` serve para criar áreas interativas e responder a toques, como botões, links ou áreas sensíveis ao toque. Existem alguns tipos principais de componentes `Touchable`, cada um com comportamentos específicos para interações de toque:

### **TouchableOpacity**
   - Muda a opacidade do componente quando pressionado.
   - Comumente usado para botões e ícones.
   - Exemplo:

     ```javascript
     import React from 'react';
     import { TouchableOpacity, Text, StyleSheet } from 'react-native';

     const MyButton = () => (
       <TouchableOpacity style={styles.button} onPress={() => alert('Button pressed!')}>
         <Text style={styles.buttonText}>Press Me</Text>
       </TouchableOpacity>
     );

     const styles = StyleSheet.create({
       button: {
         backgroundColor: 'blue',
         padding: 10,
         borderRadius: 5,
       },
       buttonText: {
         color: 'white',
         fontWeight: 'bold',
       },
     });

     export default MyButton;
     ```

### **TouchableHighlight**
   - Muda a cor de fundo (ou "highlight") quando pressionado.
   - Útil quando você quer uma mudança de estilo de fundo ao invés de opacidade.
   - Exemplo:

     ```javascript
     import React from 'react';
     import { TouchableHighlight, Text, StyleSheet } from 'react-native';

     const MyHighlightButton = () => (
       <TouchableHighlight
         style={styles.button}
         underlayColor="darkblue"
         onPress={() => alert('Button pressed!')}
       >
         <Text style={styles.buttonText}>Press Me</Text>
       </TouchableHighlight>
     );

     const styles = StyleSheet.create({
       button: {
         backgroundColor: 'blue',
         padding: 10,
         borderRadius: 5,
       },
       buttonText: {
         color: 'white',
         fontWeight: 'bold',
       },
     });

     export default MyHighlightButton;
     ```

### **TouchableWithoutFeedback**
   - Não aplica nenhuma modificação visual.
   - Útil para envoltórios que não precisam de feedback visual.
   - Exemplo:

     ```javascript
     import React from 'react';
     import { TouchableWithoutFeedback, Text, StyleSheet, View } from 'react-native';

     const MyTouchArea = () => (
       <TouchableWithoutFeedback onPress={() => alert('Area pressed!')}>
         <View style={styles.touchArea}>
           <Text style={styles.text}>Touch Me</Text>
         </View>
       </TouchableWithoutFeedback>
     );

     const styles = StyleSheet.create({
       touchArea: {
         backgroundColor: 'gray',
         padding: 20,
         borderRadius: 5,
       },
       text: {
         color: 'white',
       },
     });

     export default MyTouchArea;
     ```

### **TouchableNativeFeedback** (apenas para Android)
   - Usa o efeito de toque nativo do Android, criando "ripple effects".
   - Exemplo:

     ```javascript
     import React from 'react';
     import { TouchableNativeFeedback, Text, StyleSheet, View } from 'react-native';

     const MyAndroidButton = () => (
       <TouchableNativeFeedback onPress={() => alert('Button pressed!')}>
         <View style={styles.button}>
           <Text style={styles.buttonText}>Press Me</Text>
         </View>
       </TouchableNativeFeedback>
     );

     const styles = StyleSheet.create({
       button: {
         backgroundColor: 'blue',
         padding: 10,
         borderRadius: 5,
       },
       buttonText: {
         color: 'white',
         fontWeight: 'bold',
       },
     });

     export default MyAndroidButton;
     ```

Esses componentes permitem personalizar as interações de toque de acordo com o comportamento desejado, seja mudança de opacidade, cor de fundo ou efeito ripple.


## 10. **Modals e ActionSheets**

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

## 11. RefreshControl

O componente `RefreshControl` no React Native é usado para adicionar a funcionalidade de "puxar para atualizar" (pull-to-refresh) em componentes de rolagem, como `ScrollView`, `FlatList` e `SectionList`. Ele é especialmente útil para recarregar dados quando o usuário puxa a tela para baixo.

### Características principais do `RefreshControl`:
- **Atualização por Deslizamento**: Exibe um indicador de carregamento enquanto os dados são atualizados, proporcionando uma experiência visual clara para o usuário.
- **Controle do Estado de Carregamento**: Oferece controle total sobre quando iniciar e parar o indicador de atualização, normalmente usando o estado do componente.
- **Compatibilidade com Listas**: Integra-se facilmente com `ScrollView`, `FlatList` e `SectionList`, mas não funciona em `View`.

### Exemplo de uso com `FlatList`:

```javascript
import React, { useState, useCallback } from 'react';
import { FlatList, RefreshControl, Text, StyleSheet } from 'react-native';

const App = () => {
  const [refreshing, setRefreshing] = useState(false);
  const [data, setData] = useState(["Item 1", "Item 2", "Item 3"]);

  const onRefresh = useCallback(() => {
    setRefreshing(true);
    // Simula uma atualização de dados
    setTimeout(() => {
      setData([...data, `Item ${data.length + 1}`]);
      setRefreshing(false);
    }, 2000);
  }, [data]);

  return (
    <FlatList
      data={data}
      keyExtractor={(item, index) => index.toString()}
      renderItem={({ item }) => <Text style={styles.item}>{item}</Text>}
      refreshControl={
        <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
      }
    />
  );
};

const styles = StyleSheet.create({
  item: {
    padding: 20,
    fontSize: 18,
    borderBottomWidth: 1,
    borderColor: '#ccc',
  },
});

export default App;
```

### Propriedades principais:
- **refreshing**: Booleano que indica se o `RefreshControl` está em estado de carregamento. Geralmente, é vinculado a um estado.
- **onRefresh**: Função chamada quando o usuário realiza a ação de atualizar, onde você define o que fazer para recarregar os dados.
- **colors** (para Android) e **tintColor** (para iOS): Definem as cores do indicador de atualização.
- **progressBackgroundColor**: Define a cor de fundo do indicador de progresso.

### Quando Usar `RefreshControl`:
Use `RefreshControl` quando precisar dar aos usuários a capacidade de atualizar dados manualmente em uma lista ou área de conteúdo rolável.

# Componentes de Entrada

## 1. `Button`
Botão simples que pode disparar ações ao ser pressionado.
```jsx
import { Button } from 'react-native';

const App = () => <Button title="Press me" onPress={() => alert('Pressed!')} />;
```

## 2. Switch

- **Descrição**: Um botão de alternância (toggle) que permite mudar entre dois estados, como "ligado" e "desligado".
- **Uso Comum**: Usado para configurações que precisam ser ativadas ou desativadas, como notificações ou configurações de preferências.
### **Propriedades principais**:

- **value**: Define o estado atual do switch (true ou false).
- **onValueChange**: Função chamada quando o usuário altera o estado do switch.
- **trackColor** e **thumbColor**: Define as cores do track (barra) e do thumb (círculo) do switch.

```js
<Switch value={isEnabled} onValueChange={(value) => setIsEnabled(value)} />
```

## 3. Slider

- **Descrição**: Um controle deslizante que permite selecionar um valor dentro de um intervalo.
- **Uso Comum**: Para ajustar valores contínuos, como volume, brilho ou intensidade.
### Propriedades principais:

- **value**: Valor atual do slider.
- **onValueChange**: Função chamada quando o usuário move o slider.
- **minimumValue** e **maximumValue**: Define o intervalo de valores possíveis.
- **step**: Define o incremento dos valores quando o slider é movido.

```javascript
<Slider
  value={50}
  onValueChange={(value) => setVolume(value)}
  minimumValue={0}
  maximumValue={100}
  step={1}
/>
```

## 4. Picker

- **Descrição**: Um componente de seleção que permite escolher uma opção de uma lista suspensa (dropdown).
- **Uso Comum**: Em formulários ou configurações onde o usuário deve selecionar uma única opção, como país, categoria ou tipo de item.
### **Propriedades principais**:
- **selectedValue**: Valor atualmente selecionado.
- **onValueChange**: Função chamada quando o usuário escolhe uma nova opção.
- **enabled**: Define se o picker está habilitado ou desabilitado.

# Componentes de Layout

## 1. SafeAreaView

## 2. KeyboardAvoidingView

# Componentes de Mídia

## 1. **Camera e Media Library**

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

## 2. Video

# Componentes de Navegação

## 1. NavigationContainer
## 2. StackNavigator
## 3. BottomTabNavigator
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


# API Nativas

## 1. Async Storage

O **AsyncStorage** é uma API simples e assincrônica de armazenamento de dados para o React Native. Ele permite salvar dados no dispositivo do usuário, funcionando como um armazenamento persistente de chave-valor, semelhante ao `localStorage` em aplicações web. No entanto, ao contrário do `localStorage`, que é síncrono, o **AsyncStorage** é completamente assíncrono.

### Instalação

O **AsyncStorage** foi separado do core do React Native e agora é uma biblioteca independente. Para usá-lo, você precisa instalá-lo como uma dependência.

```bash
npm install @react-native-async-storage/async-storage
# ou
yarn add @react-native-async-storage/async-storage
```

Após a instalação, você pode importá-lo:

```javascript
import AsyncStorage from '@react-native-async-storage/async-storage';
```

### Principais Métodos

#### 1. `setItem`

Armazena um valor associado a uma chave.

```javascript
await AsyncStorage.setItem('@chave', 'valor');
```

- **Parâmetros**: `chave` e `valor`, ambos precisam ser strings.
- **Uso Comum**: Para armazenar informações como tokens, configurações, etc.

#### 2. `getItem`

Recupera o valor associado a uma chave.

```javascript
const valor = await AsyncStorage.getItem('@chave');
```

- **Parâmetros**: `chave`.
- **Retorno**: Retorna o valor como uma string ou `null` se a chave não existir.

#### 3. `removeItem`

Remove um item específico baseado na chave.

```javascript
await AsyncStorage.removeItem('@chave');
```

- **Parâmetros**: `chave`.
- **Uso Comum**: Para apagar informações, como ao deslogar o usuário.

#### 4. `mergeItem`

Atualiza parte de um valor JSON armazenado, sem substituir o objeto inteiro.

```javascript
await AsyncStorage.mergeItem('@chave', JSON.stringify({ subChave: 'novoValor' }));
```

- **Parâmetros**: `chave` e `valor` (como uma string JSON).
- **Uso Comum**: Para atualizar apenas parte de um objeto armazenado, como configurações do usuário.

#### 5. `clear`

Remove todos os itens do armazenamento.

```javascript
await AsyncStorage.clear();
```

- **Uso Comum**: Para limpar todos os dados, geralmente ao resetar a aplicação ou deslogar completamente o usuário.

#### 6. `getAllKeys`

Obtém todas as chaves salvas no AsyncStorage.

```javascript
const keys = await AsyncStorage.getAllKeys();
```

- **Retorno**: Um array de strings com todas as chaves armazenadas.

#### 7. `multiSet` e `multiGet`

Esses métodos permitem armazenar e recuperar múltiplos itens ao mesmo tempo.

```javascript
// Armazenando múltiplos itens
await AsyncStorage.multiSet([['@chave1', 'valor1'], ['@chave2', 'valor2']]);

// Recuperando múltiplos itens
const valores = await AsyncStorage.multiGet(['@chave1', '@chave2']);
valores.forEach(([chave, valor]) => console.log(chave, valor));
```

### Boas Práticas

1. **Transformar objetos em JSON**: Como o AsyncStorage só armazena strings, converta objetos para JSON com `JSON.stringify` ao salvar e use `JSON.parse` ao ler.
   
2. **Limpar dados sensíveis ao deslogar**: Para proteger a privacidade, sempre remova dados sensíveis do AsyncStorage quando o usuário deslogar.

3. **Manter dados importantes atualizados**: AsyncStorage não é ideal para grandes quantidades de dados ou dados frequentemente atualizados. Prefira um banco de dados local (como **SQLite**) para essas situações.

### Limitações

- **Armazenamento limitado**: AsyncStorage não é recomendado para grandes quantidades de dados.
- **Performance**: Para manipulação frequente de grandes volumes de dados, considere outras opções, pois o AsyncStorage pode ser lento.

### Conclusão

O AsyncStorage é ideal para armazenar pequenas quantidades de dados simples e persistentes em apps React Native. Para dados mais complexos ou grandes volumes, outras soluções podem ser mais adequadas.

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

## 11. Alert

O `Alert` é uma API nativa do React Native que permite exibir caixas de diálogo modais (alertas) simples para o usuário. Esses alertas podem ser usados para exibir mensagens, pedir confirmações ou fornecer informações importantes ao usuário.


A API `Alert` é simples e possui três principais métodos: **`alert`**, **`prompt`** e **`dialog`** (em versões mais recentes).

### 1. **`Alert.alert`**

O método mais comum é o `Alert.alert`, que exibe uma caixa de diálogo com um título, uma mensagem e uma série de botões.

```javascript
import { Alert } from 'react-native';

const showAlert = () => {
  Alert.alert(
    "Título do Alerta",  // Título
    "Mensagem de alerta.", // Mensagem
    [
      {
        text: "Cancelar", // Texto do botão
        onPress: () => console.log("Cancelar Pressionado"),
        style: "cancel" // Estilo do botão
      },
      {
        text: "OK", // Texto do botão
        onPress: () => console.log("OK Pressionado")
      }
    ],
    { cancelable: true } // Determina se o alerta pode ser fechado ao tocar fora
  );
};

showAlert();
```

#### Parâmetros do `Alert`:

1. **Título (Opcional)**: O título do alerta (string).
2. **Mensagem (Opcional)**: O corpo do alerta, geralmente é o texto que descreve a razão do alerta (string).
3. **Botões (Obrigatório)**: Um array de botões que o alerta exibirá. Cada botão é um objeto com:
   - **`text`**: O texto exibido no botão.
   - **`onPress`**: A função que será chamada quando o botão for pressionado.
   - **`style`** (Opcional): Pode ser `"default"`, `"cancel"` ou `"destructive"`, que altera a aparência do botão.
4. **Opções adicionais (Opcional)**: Um objeto para definir opções adicionais, como se o alerta pode ser cancelado tocando fora dele (`cancelable`).

### 2. **`Alert.prompt`**

O `Alert.prompt` é utilizado quando você deseja pedir ao usuário uma entrada (como texto). Ele exibe uma caixa de diálogo que permite ao usuário digitar algo.

```javascript
import { Alert } from 'react-native';

const showPrompt = () => {
  Alert.prompt(
    "Digite algo",  // Título
    "Por favor, insira seu nome:", // Mensagem
    [
      {
        text: "Cancelar", // Botão de cancelar
        style: "cancel",
      },
      {
        text: "OK", // Botão de confirmação
        onPress: (text) => console.log("Texto inserido:", text),
      }
    ],
    'plain-text' // Define o tipo de entrada (pode ser "default", "plain-text", "secure-text")
  );
};

showPrompt();
```

**Parâmetros do `Alert.prompt`**:
- **Título**: O título da caixa de diálogo.
- **Mensagem**: O texto explicativo na caixa de diálogo.
- **Botões**: Um array de objetos de botão, como no `Alert.alert`.
- **Tipo de entrada**: O tipo de entrada que você deseja permitir. Os valores podem ser `"default"`, `"plain-text"`, ou `"secure-text"`, dependendo do tipo de dado que você espera (texto simples ou senha).

### 3. **Exemplo de Uso do `Alert`**

Um exemplo simples de uso seria mostrar um alerta ao pressionar um botão:

```javascript
import React from 'react';
import { View, Button, Alert } from 'react-native';

const App = () => {
  const showAlert = () => {
    Alert.alert(
      "Alerta de Confirmação",
      "Você tem certeza que quer continuar?",
      [
        { text: "Cancelar", onPress: () => console.log("Cancelado") },
        { text: "Confirmar", onPress: () => console.log("Confirmado") }
      ]
    );
  };

  return (
    <View>
      <Button title="Mostrar Alerta" onPress={showAlert} />
    </View>
  )
```

### Características do `Alert`

- **Modais**: O `Alert` é uma janela modal, ou seja, ela impede que o usuário interaja com o resto da interface até que a caixa de diálogo seja fechada.
- **Estilo padrão**: Em dispositivos iOS, o estilo do alerta segue as convenções do iOS (por exemplo, botões com estilos mais suaves), enquanto no Android ele segue o estilo de botões padrão de diálogos.
- **Cancelamento**: O alerta pode ser configurado para ser cancelável, ou seja, o usuário pode fechá-lo tocando fora da caixa ou pressionando o botão "Cancelar".

### Exemplos de Estilo de Botões

- **`"default"`**: O estilo de botão padrão.
- **`"cancel"`**: Um botão com estilo de "cancelamento" (geralmente mais proeminente).
- **`"destructive"`**: Um botão com estilo para ações destrutivas (geralmente em vermelho, para confirmar ações como excluir).
