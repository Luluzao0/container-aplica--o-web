# Executando uma Aplicação Web em um Container Apache com Docker Compose

Este guia passo a passo irá ajudá-lo a executar uma aplicação web em um container Apache usando o Docker Compose tanto no Linux quanto no Windows.

## Pré-requisitos

- Docker e Docker Compose instalados em seu sistema.

## Passos

1. **Crie um diretório para o projeto**: Em seu terminal, navegue até onde você deseja criar o projeto e execute `mkdir meu-projeto`. Em seguida, navegue para este diretório com `cd meu-projeto`.

2. **Crie um arquivo Dockerfile**: No diretório do projeto, crie um arquivo chamado `Dockerfile` (sem extensão). Este arquivo irá conter as instruções para criar a imagem Docker.

3. **Adicione instruções ao Dockerfile**: Abra o arquivo Dockerfile em um editor de texto e adicione as seguintes linhas:
    ```
    FROM httpd:2.4
    COPY ./public-html/ /usr/local/apache2/htdocs/
    ```
    A primeira linha indica que estamos usando a imagem httpd versão 2.4 do Docker Hub. A segunda linha copia os arquivos do diretório `public-html` (que criaremos na próxima etapa) para o diretório `htdocs` do container.

4. **Crie um diretório para os arquivos HTML**: No diretório do projeto, crie um diretório chamado `public-html`. Este diretório irá conter os arquivos HTML que você deseja servir.

5. **Adicione seus arquivos HTML, CSS e JS**: Coloque os arquivos HTML, CSS e JS que você deseja servir no diretório `public-html`.

6. **Crie um arquivo docker-compose.yml**: No diretório do projeto, crie um arquivo chamado `docker-compose.yml`. Este arquivo irá conter as instruções para o Docker Compose.

7. **Adicione instruções ao docker-compose.yml**: Abra o arquivo docker-compose.yml em um editor de texto e adicione as seguintes linhas:
    ```
    version: '3'
    services:
      web:
        build: .
        ports:
         - "8080:80"
    ```
    Esta configuração cria um serviço chamado "web" que constrói a imagem Docker a partir do Dockerfile no diretório atual e mapeia a porta 8080 do host para a porta 80 do container.

8. **Construa e execute o container**: No terminal, execute `docker-compose up`. Isso irá construir a imagem Docker a partir do Dockerfile e iniciar o container.

9. **Acesse a aplicação**: Abra um navegador web e navegue até `localhost:8080`. Você deverá ver sua aplicação HTML sendo servida pelo Apache no container Docker.

## Solução de problemas

- Se você receber uma mensagem de erro dizendo que a porta 8080 já está em uso, você pode mudar a porta que o Docker Compose está tentando usar. No seu arquivo `docker-compose.yml`, mude a linha que diz `"8080:80"` para usar outra porta, como `"8081:80"`.

- Se você fez alterações nos arquivos do seu projeto e deseja que essas alterações sejam refletidas no seu container Docker, você precisará reconstruir a imagem Docker e reiniciar o container. Para fazer isso, execute `docker-compose down` para parar e remover o container atual, depois execute `docker-compose build` para reconstruir a imagem, e finalmente execute `docker-compose up` para iniciar um novo container com a imagem recém-construída.