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

### Tipagem com Schema

````ts
type CreateUsersType = z.infer<typeof createUserSchema>
````

----

### Omit - remover propriedades

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