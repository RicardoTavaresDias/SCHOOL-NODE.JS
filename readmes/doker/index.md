- [VOLTAR](../../README.md)

</br>

<img src="./assets/logo.png" alt="Logo do projeto" width="200"/>

----

</br>

📌 `docker-compose.yml`

#### <span style="color:#efb423">*🔹 Postgres*</span>

````ts
services:
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: desafio
    ports:
      - "5432:5432"
````

### Volumes: criando banco temporário para testes

Criar um banco de dados de teste, para não usar o banco em produção ou desenvolvimento.

````ts
    volumes:
      - ./docker/setup.sql:/docker-entrypoint-initdb.d/init.sql 
````

Criar pasta na raiz do projeto docker/setup.sql

````ts
CREATE DATABASE desafio_test
````

#### <span style="color:#efb423">*🔹 API*</span>

````ts
version: "3.9"
services:
  api_chatbot_ai:
    build:
      context: .
      dockerfile: Dockerfile
    image: nodejs
    container_name: apiChatBot_AI

    # Adicionado para carregar variáveis de ambiente do seu arquivo .env
    env_file:
      - .env
    ports:
      - "3000:3000"
````

----

📌 `.dockerignore`

````
node_modules
.git
.env*
coverage
vitest.config.ts
requisicoes.http
README.md
````

📌 `Dockerfile`

````ts
# Define a imagem base como sendo a versão alpine do Node.js 22, que é leve e contém o ambiente Node.js necessário
# O 'AS builder' nomeia esta etapa para possível uso em multi-stage builds

FROM node:22-alpine AS builder

# Define o diretório de trabalho dentro do container onde os arquivos da aplicação serão copiados e executados

WORKDIR /app

# Copia todos os arquivos e diretórios do diretório local para o diretório de trabalho (/app) no container

COPY . ./

# Executa o comando npm ci com a flag --only=production, instalando apenas as dependências listadas em "dependencies" no package.json
# Isso evita a instalação de dependências de desenvolvimento, otimizando o tamanho da imagem

RUN npm ci --only=production

# Informa que a aplicação dentro do container escutará na porta 3333
# Isso é apenas uma documentação e não publica a porta automaticamente; é necessário mapear a porta ao rodar o container

EXPOSE 3333

# Define o comando padrão a ser executado quando o container for iniciado
# Executa o arquivo src/server.ts usando o Node.js

CMD [ "node", "src/server.ts" ]
````