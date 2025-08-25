- [VOLTAR](../../README.md)

## Estendendo o objeto Request do Express 

`express.d.ts`
````ts
declare namespace Express {
  export interface Request {
    user?: {
      id: string
      name: string
      role: string
    }
  }
}
````
----

## TypeScrip

Cria um novo tipo a partir de outro, removendo propriedades específicas.

### 🔹 *Omit*

exemplo:

````ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}
````

Criamos um tipo que remove "password"

````ts
type UserPublic = Omit<User, "password">
````

saída:

````ts
const user: UserPublic = {
  id: 1,
  name: "joão",
  email: "joao@example.com"
  // password: "123456" ❌ erro, não existe mais nesse tipo
}
````

multiplos

````ts
type UserSafe = Omit<User, "email" | "password">
````

saida:

````ts
const user: UserPublic = {
  id: 1,
  name: "joão",
  // email: "joao@example.com" ❌ erro, não existe mais nesse tipo
  // password: "123456" ❌ erro, não existe mais nesse tipo
}
````

----

### 🔹 *Pick*

Faz o oposto do *Omit:* em vez de remover, ele escolhe apenas algumas propriedades de um tipo.

exemplo:

````ts
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}
````

Cria um tipo só com id e name

````ts
type UserSummary = Pick<User, "id" | "name">;
````

saída:

````ts
const u: UserSummary = {
  id: 1,
  name: "joão",
  // email: "joao@test.com", ❌ não existe nesse tipo
  // password: "1234" ❌ também não existe
};
````

----