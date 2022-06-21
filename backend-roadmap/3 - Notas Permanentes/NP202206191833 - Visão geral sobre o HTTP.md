# Visão geral sobre o HTTP

**Hash:** NP202206191833
**Notas Permanentes:** 
	- [[]]
**Notas Rápidas:**
	- [[NR202206191826 - HTTP Overview (MDN)]]
	- [[NR202206191831 - HTTP Tópicos diversos (MDN)]]
	- [[NR202206192111 - What is HTTP?]]
	- [[NR202206192059 - Um pouco mais sobre o protocolo HTTP]]
	- [[NR202206192113 - RFC 2616]]
**Notas de Literatura:**
	- [[]]
**Tags:**  #http 

**HTTP** é uma sigla para _Hypertext Transfer Protocol_, que significa: Protocolo de Transferência de Hipertexto. Basicamente, HTTP é um protocolo que permite a obtenção de recursos, como por exemplo: documentos HTML, imagens, vídeos, etc.

Ele é considerado um protocolo “**Cliente-Servidor**”, ou seja, ele determina padrões e define as regras para a troca de informações entre clientes e servidores. O **WWW** (World Wide Web) é totalmente construído com base na comunicação de clientes e servidores web.

A comunicação entre clientes e servidores é feita através da troca de mensagens individuais que são divididas entre as solicitações (_requests_) e respostas (_responses_). As mensagens enviadas pelo cliente (geralmente um navegador) a fim de se obter algum recurso é tida como _request_. Já a mensagem de resposta da solicitação enviada pelo servidor é tida como _response_.

**PS:** É válido ressaltar que as requisições são sempre iniciadas pelo destinatário (cliente).

O HTTP é um “protocolo da camada de aplicação”, que é executado no topo da pilha do modelo **TCP/IP**. O HTTP é enviado sobre o protocolo TCP, onde basicamente será criada uma conexão entre o cliente e o servidor, que será iniciada no momento do envio da solicitação, e após a resposta, a conexão será finalizada. Devido a essa característica, é dito que o HTTP é sem estado (_stateless_), já que não existe uma relação entre duas requisições sendo feitas através da mesma conexão.

## Características do HTTP

* **Simplicidade:** O HTTP foi projetado para ser de fácil legibilidade aos seres humanos. As mensagens podem ser entendidas por qualquer pessoa, facilitando o desenvolvimento e testes;    
* **Extensível:** Os cabeçalhos HTTP fazem com que o protocolo seja fácil de “estender”. Novas funcionalidades podem ser introduzidas pelo simples acordo entre um cliente e um servidor utilizando a semântica de um cabeçalho;
* **Sem estado:** O HTTP é “sem estado”, ou seja, não há relação entre duas requisições sendo feitas através da mesma conexão. Como o fundamento básico do HTTP é não manter estados, utilizamos os _Cookies_ HTTP para que as sessões tenham estados. Dessa forma, podemos adicionar os _cookies_ aos cabeçalhos para permitir que a criação de sessão em cada requisição possam compartilhar o mesmo contexto/estado.
* **Conexões:** As conexões são controladas pela camada de transporte, e portanto, estão fora do controle do HTTP, contudo, para cada par de requisição/resposta, uma conexão TCP é aberta. De fato, talvez caso haja a necessidade de haver várias requisições sendo feitas simultaneamente, não seja uma das característica mais agradáveis, e para contornar isso, foram criadas duas funcionalidades, uma no HTTP/1.1 e outra no HTTP/2.0. No HTTP/1.1 foi introduzida o conceito de “_pipelining_”, que dá uma maior controle para as conexões TCP utilizando o cabeçalho “Connection”. Já no HTTP/2.0, há a "multiplexação" de várias mensagens através de uma única conexão, ajudando a manter a conexão “mais quente”.

## Fluxo HTTP

Quando um cliente quer se comunicar com um servidor, ele realiza os seguintes passos:

-   Abre uma conexão TCP: Uma conexão TCP será utilizada para enviar uma requisição e receber a resposta. Você pode criar uma conexão nova, reusar uma existente ou abrir várias conexões.    
-   Envia uma  requisição HTTP: Essas mensagens são legíveis aos seres humanos (Vamos dar um exemplo melhor na sessão Requisição HTTP);
-   O servidor devolve uma Resposta HTTP (Também falaremos melhor na sessão Resposta HTTP);
-   A conexão é fechada. 

## Requisição HTTP

Exemplo de uma requisição HTTP:
```
GET / HTTP/1.1
Host: developer.mozilla.org
Accept-Language: en
```

Podemos dividir as requisições nos seguintes elementos:

* Um método HTTP é um “verbo”, como por exemplo **GET**, **POST**, **DELETE**, **PUT** ou também um substantivo como **OPTIONS** ou **HEAD** que são utilizados para definir qual operação o cliente quer fazer. Cada método é utilizado para uma função diferente por convenção, por exemplo o método GET é utilizado para obtenção de recursos e o POST para publicação de dados.
* O caminho do recurso a ser buscado (**URL**);
* A versão do protocolo HTTP;
* Cabeçalhos opcionais que possuem informações adicionais para os servidores;
* E para alguns métodos como o POST, um corpo com os dados;

## Resposta HTTP

```
HTTP/1.1 200 OK
Date: Sat, 09 Oct 2010 14:28:02 GMT
Server: Apache
Last-Modified: Tue, 01 Dec 2009 20:18:22 GMT
ETag: “51142bc1-744-479b075b2891b”
Accept-Ranges: bytes
Content-Length: 29769
Content-Type: text/html
```

As resposta consistem em:
*   A versão do protocolo HTTP;
*   Um código de status (valos falar mais abaixo);
*   Uma mensagem de status, que basicamente é uma descrição do código de status;
*   Cabeçalhos HTTP, similar aos da requisição;    
*   Opcionalmente, um corpo com dados do recurso requisitado;

## Código de Status HTTP

Os códigos de status HTTP indicam se uma requisição HTTP foi corretamente concluída. Ao todo, as respostas são agrupadas em cinco classes:

-   **1XX** - Respostas de informação;    
-   **2XX** - Respostas de sucesso;
-   **3XX** - Redirecionamentos;
-   **4XX** - Erros do Cliente;
-   **5XX** - Erros do servidor.

Para cada grupo desses, existe um código específico para uma determinada situação. Você pode ter acesso a cada um deles clicando [aqui](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html).

## Diferenças entre o HTTP e o HTTPS

Por se tratar de um protocolo na camada de aplicação, o HTTP não precisa necessariamente se preocupar em como a mensagem é transmitida. Essa responsabilidade é da camada de transporte (conexão criada utilizando o TCP). Como o HTTP é um protocolo baseado em texto, pessoas má intencionadas podem “sniffar” a conexão e acessar os dados que estão sendo transmitidos. Para tornar a conexão entre o Cliente e Servidor mais segura, utilizamos uma conexão TCP criptografada com **TLS** (_Transport Layer Security_), e é justamente por estar utilizando esse tipo de criptografia que temos o “S” de Secure no final do HTTPS. Essa funcionalidade é oferecida pelo **Certificado SSL**, que por sua vez é oferecido pela maioria dos servidores.

Sumarizando algumas diferenças:

*   HTTPS é uma extensão do HTTP. Para que ele possa transmitir os dados de maneira segura, ele utiliza um outro protocolo chamado TLS.    
*   HTTP utiliza a porta TCP 80 por padrão, já o HTTP usa a porta TCP 443;
*   O HTTP funciona na camada de aplicação, o HTTPS funciona na camada de transporte (TCP + TLS);
*   Não há necessidade de um certificado SSL para o HTTP, mas para o HTTPS, precisamos de um certificado SSL assinado e implementado por um **CA** (_Certification Authority_);
*   No HTTP não há necessidade de validação de domínio, enquanto para o HTTPS é obrigatória a validação do domínio;
