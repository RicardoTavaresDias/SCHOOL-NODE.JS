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