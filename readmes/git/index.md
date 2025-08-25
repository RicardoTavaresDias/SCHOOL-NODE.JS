- [VOLTAR](../../README.md)

### 🔹 Recuperando arquivo anterior do commit - Forma forçado e remover tudo dos commits futuros

Lista todos os Commit enviado
````ts
git reflog
````

selecionando e voltando o commit solicitado
````ts
git reset —hard 1658aa4 
````

Forçar para remover no gihub (nome-da-branch ⇒ main ou master)
````ts
git push -f origin nome-da-branch 
````

para sair da lista commit
````ts
:q
````

----

### 🔹 Clonar o mesmo projeto no computador

````ts
git clone https://github.com/usuario/meu-projeto.git
````

````ts
cd meu-projeto
`````

----

### 🔹 Trabalhar no projeto e enviar alterações

ver o que mudou
````ts
git status
````

adiciona todas as alterações
````ts
git add .
````

cria um commit
````ts
git commit -m "mensagem"
````

envia para o GitHub (main ou master)
````ts
git push origin main 
````

----

### 🔹 Configurar usuário e e-mail

````ts
git config --global user.name "Seu Nome"
````

````ts
git config --global user.email "seuemail@example.com"
````

----

### 🔹Trabalhando com Branches 

Ambiente Desenvolvimento / Ambiente Produção.

*Criando feature*

````ts
git checkout -b feature/shake_feedback
````

`obs:` </br>
*<feature/shake_feedback>* nome da feature criado. </br>
executa e realiza mudança no código no ambiente de desenvolvimento.

*Adicionar as alterações*

````ts
git add .
````

*commit*

````ts
git commit -m "feat: shake feedback ehwn user a wrong guess"
````

*Subir as alterações no gitHub*

````ts
git push origin feature/shake_feedback
````

`obs:` </br>
Criado branche de Preview no vercel sem mexer com maste ou main. </br>
Possivel visualizar e testar antes de motificar.

----

### 🔹 Promovendo para produção

*Troca o branch atual para o main.*

````ts
git checkout main
````

*Baixar as atualizações do branch main*

````ts
git pull origin main
````

*Pegar as alterações do branch feature/shake_feedback e integrá-las (main) ao branch em que você está no momento.*

````ts
git merge feature/shake_feedback
````