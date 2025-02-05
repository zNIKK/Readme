## Origem
- **Criado por**: Ryan Dahl
- **Ano**: 2009
- **Baseado em**: JavaScript, utilizando o **V8 Engine** (motor de execução de JavaScript do Google)
- **Motivação**: Criar um ambiente para executar JavaScript fora do navegador, especialmente para o backend.

## Características

- **Single-threaded**: Usa um único thread para processar operações, mas consegue lidar com muitas conexões simultâneas de forma eficiente.

- **Event-driven**: Usa um modelo de I/O orientado a eventos, tornando-o eficiente para aplicações de I/O intensivo (como servidores web).

- **Non-blocking I/O**: Executa operações de entrada/saída de forma assíncrona, sem bloquear o thread principal, permitindo melhor desempenho em operações de leitura/escrita de arquivos ou rede.

- **Cross-platform**: Funciona em várias plataformas (Windows, macOS, Linux).

## Principais Conceitos

### Event Loop
- O **Event Loop** é o mecanismo responsável por gerenciar a execução de operações assíncronas e callbacks no Node.js.
- Node.js não bloqueia a execução de código enquanto aguarda operações de I/O, usando o event loop para processar tarefas.

### Callbacks e Promises
- **Callback**: Função passada como argumento para outra função e chamada após a conclusão de uma operação assíncrona.
- **Promise**: Um objeto que representa a eventual conclusão (ou falha) de uma operação assíncrona e seu valor resultante.
  - As **Promises** ajudam a evitar o problema de "callback hell" com um fluxo mais claro de tratamento de operações assíncronas.

### Módulos
- Node.js usa o sistema de **módulos** para organizar o código:
  - **CommonJS** (sintaxe tradicional): `require()` para importar e `module.exports` para exportar.
  - **ESModules** (mais recente): `import` e `export`.
- Módulos populares:
  - `fs`: Manipulação de arquivos.
  - `http`: Criação de servidores HTTP.
  - `path`: Manipulação de caminhos de arquivos.
### NPM (Node Package Manager)

- **NPM** é o gerenciador de pacotes do Node.js, usado para instalar bibliotecas e ferramentas.
  - **Comandos comuns**:
    - `npm init`: Inicializa um projeto Node.js.
    - `npm install`: Instala dependências.
    - `npm run`: Executa scripts definidos no arquivo `package.json`.

## Casos de Uso
- **APIs REST**: Node.js é amplamente usado para construir APIs rápidas e escaláveis.
- **Aplicações em tempo real**: Como chatbots e serviços de streaming, devido à sua natureza assíncrona e capacidade de lidar com múltiplas conexões.
- **Ferramentas de desenvolvimento**: Muitos pacotes e ferramentas de frontend são baseados em Node.js, como Webpack, Babel, e outros.

## Vantagens
- **Escalabilidade**: Capaz de lidar com grandes volumes de tráfego.
- **Desempenho**: Alta eficiência em operações de I/O.
- **Ampla comunidade**: Grande número de pacotes disponíveis no NPM.

## Desvantagens
- **CPU-bound tasks**: Não é ideal para tarefas que exigem muita CPU, pois o modelo de thread único pode sofrer com bloqueios.

# Módulos

## Backend

### [[Modulos em NodeJS#🌐 HTTP|HTTP]]




