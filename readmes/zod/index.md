## Removendo campos de um schema existente

exemplo:

````ts
const createUserSchema = z.object({
  id: z.string().uuid(),
  name: z.string().min(1, { message: "name: Campo obrigatório." }),
  email: z.string().email({ message: "Email inválido" }),
  role: z.string().default("member")
})
````

`Tipagem com Schema`

````ts
type CreateUsersType = z.infer<typeof createUserSchema>
````

`Validação com schema`

````ts
  const createData = createUserSchema.safeParse(request.body)

  if(!createData.success) {
    return response.status(400).json({ 
      message: createData.error.issues[0].message 
    })
  }
````

----

## Omit – Criar um schema sem determinadas propriedades

````ts
const updateUserSchema = z.object({
  ...createUserSchema.omit({
    id: true,
    role: true
  }).shape
})
````

`saída`

````ts
{
  name: string
  email: string
}
````

## Baseando-se em um schema existente e incrementando novos atributos

````ts
const createSchema = z.object({
  ...createUserSchema.omit({
    id: true,
    role: true
  }).shape,

  id: z.string().uuid(),
  role: z.string().default("member")
})
````

`saída`

````ts
{
  id: string
  name: string
  email: string
  role: string
}
````

----