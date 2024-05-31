## <i> Projeto pratico Configuração e Otimização do Servidor NGINX </i>
***
<b>2º Projeto Prático - DevOps</b>
***
### 💻 <i> Desafio </i>

Configure e otimize um servidor NGINX para atuar como servidor web, proxy reverso e gateway de API. O projeto deve otimizar o desempenho, implementar HTTPS, configurar regras de proxy reverso e gerenciar servidores web seguros.

***
### 📋<i> Etapas </i>

- <b>Configuração Básica: Configure o NGINX para atuar como servidor web para um site ou aplicativo.</b>
####
- <b>Proxy Reverso: Configure regras de proxy reverso para direcionar o tráfego para diferentes serviços ou aplicativos.</b>
####
- <b>Segurança e HTTPS: Implemente HTTPS com certificados SSL/TLS e configure políticas de segurança.</b>
####
- <b>Otimização de Desempenho: Aplique técnicas de otimização para melhorar o desempenho do NGINX.</b>
####
- <b>Documentação: Documente a configuração e as decisões tomadas durante o projeto.</b>


***
### 📖<i> Introdução </i>

* Neste projeto foi utilizado:

[x] -  O ubuntu mais especificamente a versao Ubuntu 22.04.4 LTS.

[x] - [Nginx](https://nginx.org) para criar os arquivos de configuração e teste da pagina de web.

[x] - [Docker](https://www.docker.com/) para criar o container do NGINX e subir os arquivos para o mesmo.

[x] - [Openssl](https://www.openssl.org) para gerar o certificado auto assinado para acessar as paginas em HTTPS

### ⚙️ <i> Instalação </i>
***
#### ➡️  Etapas

1. Antes de instalar qualquer app ou programa devemos atualizar a maquina e utilizamos este comando:
- ```sudo apt-get update```

2. Caso não possua na maquina precisamos instalar antes de tudo o curl:
- ```sudo apt-get install curl```

3. instalação do NGINX:
- ```sudo apt-get install nginx```

4. Agora instalaremos o docker.
Clicando [aqui](https://docs.docker.com/desktop/install/ubuntu/) voce sera redirecionado para a pagina de instalação no ubuntu explicando que versão precisa possuir seu SO entre outras informações.

5. Esta etapa é opicional:
    É para executar o docker sem precisa digita o ``` sudo ``` a todo momento, se não quiser digitar tambem é so utilizar este comando:
    - ```sudo usermod -aG docker $USER```

6. Criação da key com a ajuda do openssl
OBS: especifique a pasta onde está antes de executar o comando ou especifique no comando mesmo a pasta onde quer salva esses dois arquivos tanto o ".key" quanto o ".crt".  
- ```openssl genpkey -algorithm RSA -out "caminho_exemplo/1/chave_privada.key" -aes256```
####
- ```openssl req -new -x509 -key "caminho_exemplo/1/chave_privada.key" -out "caminho_exemplo/1/certificado.crt" -days 90```

7. Com os arquivos baixados precisaremos criar dentro da pasta do projeto uma pasta com o nome de ssl e guardaremos estas chaves criadas dentro da mesma.

### 👨🏽‍💻<i> Explicação </i>
***
### <i> Docker </i>

O Docker é uma tecnologia que ajuda a criar "pacotes" ou como chamamos de "containers" autossuficientes para aplicativos, que podem ser facilmente movidos entre diferentes ambientes de computação. Isso simplifica o processo de desenvolvimento, distribuição e execução de software.

### <i> NGINX </i>

O Nginx é um software open source usado para disponibilizar sites e aplicativos na internet de forma rápida e eficiente. Ele tem a capacidade e facilidade de lidar com muitas conexões simultâneas sem sobrecarregar o sistema.
Quando um usuário solicita o carregamento de uma página, seu navegador entra em contato com o servidor do site. O servidor então procura pelos arquivos solicitados e os envia de volta ao navegador. Essa é a forma mais básica de solicitação.

Porém, servidores web convencionais operam de maneira diferente do Nginx. Enquanto eles criam uma thread individual para cada solicitação, o Nginx opera de forma assíncrona e orientada a eventos. Em vez disso, threads semelhantes são agrupadas em processos workers, cada uma contendo unidades menores conhecidas como conexões worker. Essas conexões podem lidar com várias solicitações, permitindo que o Nginx atenda a milhares delas de forma eficiente. Essa abordagem é especialmente útil para sites com muito tráfego, como e-commerces, mecanismos de busca e serviços de armazenamento em nuvem.


### <i> Proxy reverso </i>

Um proxy reverso é essencialmente um intermediário entre os clientes e os servidores de destino. Ele recebe solicitações dos clientes e, em seguida, encaminha essas solicitações para um ou mais servidores de destino. Depois que os servidores processam essas solicitações, o proxy reverso envia as respostas de volta aos clientes. No contexto do Nginx, uma popular solução de servidor web e proxy, o proxy reverso é configurado usando a diretiva `proxy_pass`. Isso permite que o Nginx ofereça uma variedade de recursos, como distribuição de carga, cache e roteamento inteligente de tráfego. Essa configuração é especialmente útil em ambientes onde há múltiplos servidores de destino e é necessário garantir alta disponibilidade, desempenho e segurança para os clientes.

### <i> Balanceamento de carga </i>

O balanceamento de carga é uma técnica essencial para distribuir o tráfego de rede entre diversos servidores. Essa estratégia visa otimizar o desempenho, aumentar a disponibilidade e assegurar a confiabilidade dos serviços online.

O principal propósito do balanceamento de carga é evitar sobrecarregar qualquer servidor específico, garantindo uma utilização eficiente de todos os servidores disponíveis. Isso é especialmente útil em ambientes onde a demanda por serviços online pode variar ao longo do tempo ou quando há um alto volume de tráfego a ser gerenciado.

No contexto do Nginx, o balanceamento de carga é tipicamente configurado usando a diretiva upstream, que define um conjunto de servidores de destino, e a diretiva proxy_pass, que encaminha as solicitações dos clientes para esses servidores.

### <i> HTTP e HTTPS </i>

HTTP e HTTPS são protocolos de comunicação utilizados na internet. O HTTP (Hypertext Transfer Protocol) é um protocolo padrão para transferência de dados na web. Ele é usado para acessar recursos como páginas da web, imagens, vídeos, etc. No entanto, o HTTP não é seguro, pois os dados são transmitidos sem criptografia, o que significa que eles podem ser interceptados e lidos por qualquer pessoa que tenha acesso à rede.

O HTTPS (Hypertext Transfer Protocol Secure) é uma versão segura do HTTP. Ele utiliza o protocolo SSL/TLS para criptografar os dados transmitidos entre o cliente (geralmente um navegador da web) e o servidor. Isso garante a privacidade e a integridade dos dados, tornando muito mais difícil para os invasores interceptarem ou modificarem as informações durante a transmissão.

No caso de resolver este problema é aqui onde o OpenSSL entra em cena.

### <i> Openssl </i>

O OpenSSL é uma biblioteca de código aberto que implementa os protocolos SSL e TLS, além de fornecer várias funções criptográficas e de segurança. Ele é amplamente utilizado para implementar o suporte a HTTPS em servidores da web, aplicativos de e-mail, servidores de VPN e muitos outros sistemas que precisam de comunicações seguras pela internet.

Em resumo, o OpenSSL é usado para criar e verificar certificados digitais, negociar conexões seguras e criptografar os dados transmitidos via HTTPS, garantindo assim a segurança das comunicações na web.

Agora com estas breves informações de cada aplicação e bibliotecas utilizadas, poderemos começar a entrar no projeto.

### 🛠️<i> Mãos a obra </i>
***
Após estas instalações iremos entra na pasta do projeto com o cmd iremos subir os arquivos utilizando o comando:

- ```docker compose up```

ou

- ```docker compose up -d```

se não quiser uma janela de cmd travada so para o container.

Este comando acima irá ler o arquivo .yaml e irá fazer o seguinte:

[x] - baixar o container do nginx em sua ultima versão estavel;

[x] - irá liberar as portas `8080` `8088` `8089` para acesso das paginas, e a `443` para acesso https das paginas;

[x] - E irá sobreescrever os arquivos de configuração do nginx para conseguir acessar os arquivos html da pagina e liberar o acesso http e https das portas liberadas;

Se quiser verificar se o container esta ativo é so utilizar o comando:

- ```docker ps -a```

para listar todos os containers tanto os ativos quanto os inativos com seus respectivos IDs e nomes.



### <i> Referências </i>

- [Install Docker Desktop on Ubuntu](https://docs.docker.com/desktop/install/ubuntu/)
- [Implementando um Certificado Auto-Assinado](https://help.ivanti.com/wl/help/pt_BR/AVA/6.2/Avalanche/Install/selfsigned_certs.htm)
- [Conheça NGINX e saiba as vantagens de utilizá-lo em seu servidor](https://qnax.sh/blog/nginx-vantagens-servidor/?gad_source=1&gclid=Cj0KCQjwpNuyBhCuARIsANJqL9OAOn5t8aKDwQtyG-nLFW7KtMN1ST5qV2t27zgGPXWQRyPE6DDX8JEaAs0MEALw_wcB)
- [NGINX, como funciona e por que você deve usá-lo](https://rockcontent.com/br/blog/nginx/)
- [NGINX: servidor Web, Proxy Reverso e API Gateway](https://www.alura.com.br/conteudo/nginx-servidor-web-proxy-reverso-api-gateway)
- [Instalando certificado SSL auto assinado no linux](https://ajudadoprogramador.com.br/artigo/certificado-auto-assinado-no-linux)
- [Pagina de onde tirei a pagina de erro 404](https://codepen.io/uiswarup/pen/XWdXGGV)
