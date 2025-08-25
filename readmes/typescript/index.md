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