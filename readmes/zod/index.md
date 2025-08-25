## Removendo propriedades do schema

exemplo:

````ts
const createUserSchema = z.object({
  id: z.string().uuid(),
  name: z.string().min(1, { message: "name: Campo obrigatório." }),
  email: z.string().email({ message: "Email inválido" }),
  role: z.string().default("member")
})
````

Tipagem com Schema

````ts
type CreateUsersType = z.infer<typeof createUserSchema>
````

Validação com schema

````ts
  const createData = createUserSchema.safeParse(request.body)

  if(!createData.success) {
    return response.status(400).json({ 
      message: createData.error.issues[0].message 
    })
  }
````

----

## Omit - Remover propriedades

````ts
const updateUserSchema = z.object({
  ...createUserSchema.omit({
    id: true,
    role: true
  }).shape
})
````

saída

````ts
{
  name: string
  email: string
}
````

----