# Componentes de um Navegador
    
**Hash:** NP202206202316
**Notas Permanentes:** 
	- [[]]
**Notas Rápidas:**
	- [[NR202206202324 - Explicando como funciona o Navegador (Youtube)]]
	[[NR202206252157 - How browsers work (MDN)]]
	[[NR202206260031 - Understanding the Role of Rendering Engine in Browsers]]
	[[NR202206242318 - How browsers work]]
**Notas de Literatura:**
	- [[]]
**Tags:** #browser  #internet 

Um dos softwares mais utilizados em nosso dia-a-dia sem dúvidas é o nosso navegador (_browser_). Existem diversos no mercado, vai depender bastante do seu gosto na hora de escolher. Listando alguns, para fins de exemplos, temos o Firefox, Chrome, Brave, Safari e vários outros.

Mesmo com tantas opções, a essência de todos são bastante parecidas, não se tratando somente da finalidade, mas também em seus componentes internos. Esse texto busca explicar, em um nível mais superficial, os principais componentes que compõem um navegador.

## Componentes de um navegador

Muitos navegadores possuem seu código aberto (_Open Source_), o que nos ajuda a compreender um pouco mais do funcionamento e decisões por trás do desenvolvimento dos mesmos. Alguns exemplos de navegadores de código aberto são: (Firefox)[https://firefox-source-docs.mozilla.org/index.html], (Chromium)[https://www.chromium.org/Home/],  (Brave)[https://github.com/brave/brave-browser],  (Basilisk)[https://github.com/JustOff/Basilisk], etc.

Olhando o código e a estrutura desses navegadores, começamos a reconhecer um certo padrão em seus componentes, são eles: **User Interface**, **Browser Engine**, **Rendering Engine**, **Networking**, **UI Backend**, **JavaScript Interpreter** e **Data Storage**. 

![[BrowserEngine.png]]

A fim de entendermos melhor a responsabilidade de cada um deles, vamos abordá-los a seguir em pequenos tópicos. Novamente, não é intuito desta postagem nos aprofundarmos em cada um dos componentes, vamos tentar nos ater a pontuarmos suas principais características e responsabilidades.

### User Interface

A User Interface está relacionado a todos aqueles botões de atualização de página, retornar (tanto para trás quanto para frente), salvar uma página como favorito, caixa de buscas, etc. Em resumo, é tudo aquilo que o usuário interage e que não esteja envolvido diretamente com a página do site que ele está acessando.

![[user-interface.png]]

### Browser Engine

O Browser Engine é o componente que funciona como um "intermediário", basicamente sendo uma ponte entre a **User Interface** e o **Rendering Engine**. Ele consulta e atua juntamente com o Rendering Engine de acordo com as entradas recebidas através da User Interface. 

### Rendering Engine

O Rendering Engine é o componente responsável por exibir o conteúdo solicitado. Por exemplo, se o conteúdo solicitado for HTML, o mecanismo de renderização analisa HTML e CSS e exibe o conteúdo analisado na tela. É interessante ressaltar que geralmente cada navegador possui seu próprio Rendering Engine. Por exemplo: O Firefox usa o [**Gecko**](https://developer.mozilla.org/pt-BR/docs/Glossary/Gecko), o Chromium usa o [**Blink**](https://www.chromium.org/blink/), já o Basilisk utiliza a [**Goanna**](http://www.moonchildproductions.info/goanna.shtml) (que inclusive, é um fork do Gecko).

### Networking

O Networking é o componente responsável por gerenciar as chamadas de rede usando protocolos padrão, como por exemplo lidando diretamente com requisições HTTP, FTP etc. 

### UI Backend

O UI Backend é o componente utilizado para desenhar widgets básicos como _combo boxes_ e janelas. Por baixo, ele usa métodos de UI do próprio sistema operacional.

### JavaScript Interpreter

O JavaScript Interpreter é o componente, como o próprio nome já sugere, responsável por analisar e executar código JavaScript. Muitas vezes esse componente interage diretamente com o **Rendering Engine**, onde depois que alguns resultados do cõdigo são gerados, eles devem ser encaminhado para exibição na página em que o usuário está navegando.

### Data Storage

O Data Storage é o componente onde está a "camada de persistência". O navegador pode precisar salvar todos os tipos de dados localmente, como por exemplo, os famosos "_cookies_". A maioria dos navegadores também suportam mecanismos de armazenamento como **localStorage**, **IndexedDB**, **WebSQL** e **FileSystem**.
