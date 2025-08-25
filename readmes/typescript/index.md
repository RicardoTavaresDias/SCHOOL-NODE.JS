## Extender request do express 

express.d.ts

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