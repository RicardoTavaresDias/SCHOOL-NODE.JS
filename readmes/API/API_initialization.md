- [VOLTAR](../../README.md)

## Inicializar com instalação das dependências do projeto

`Cors`
````bash
npm i cors
````

````bash
npm i @types/cors -D
````


`Express`
````bash
npm i express
````

````bash
npm i @types/express -D
````

`Zod`
````bash
npm i zod
````

`Typescript`
````bash
npm i typescript -D
````

````bash
npm i tsx
````

````bash
npm i tsup  // coverte typescript para javascript na produção
````

````bash
npm i ts-node
````

### package.json - inicialização
````ts
"scripts": {
  "dev": "tsx --watch --env-file .env src/server.ts",
  "build": "tsup src --out-dir build",
  "start": "node build/server.js",
}
````


### tsconfig.json

````ts
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["ES2023"],
    "paths": {
      "@/*": ["./src/*"]
    },
    "module": "commonjs",
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true,
    "resolveJsonModule": true //swagger
  }
}
````

## Prisma

````bash
npm i @prisma/client
````

````bash
npm i prisma -D
````
package.json

````ts
"scripts": {
  "db:migrate": "npx prisma migrate dev",
  "db:generate": "npx prisma generate"
}
````

## Bcrypt

````bash
npm i bcrypt
````

````bash
npm i @types/bcrypt -D
````

## Token

````bash
npm i jsonwebtoken
````

````bash
npm i @types/jsonwebtoken -D
````

## Pasta do projeto

```
EXPRESS-SWAGGER/
├── src/
│   ├── config/           # Arquivos de configuração
│   ├── controller/       # Controladores da API
│   ├── middlewares/      # Middlewares personalizados
│   ├── routes/           # Rotas da API
│   ├── app.ts            # Configuração principal
│   └── server.ts         # Inicialização do servidor
└── .env                  # Variáveis de ambiente
```

`app.ts`

````ts
import express from "express"
import cors from "cors"
import { router } from "./routers"

const app = express()

const allowedOrigins = [
  'http://localhost:5173',
]

app.use(cors({
  origin: allowedOrigins
}))

app.use(express.json())
app.use(router)
app.use(ErrorHandling)

export { app }
````

`server.ts`

````ts
import { app } from "./app";
import { env } from "./config/env.config";

app.listen(env.PORT, () => console.log("Server in running port " + env.PORT))
````

`routes/index.ts`
````ts
import { Router } from "express";
import { userRouter } from "@/modules/users/routers/user.router";

export const router = Router()

router.use("/user", userRouter)
````

`routes/user.router.ts`

````ts
import { Router } from "express";
import { UserController } from "../controllers/user.controller";

const userController = new UserController()
export const userRouter = Router()

userRouter.get("/", validateUserId, userController.showUser)
````