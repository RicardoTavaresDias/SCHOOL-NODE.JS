# Reduce Javascript

Agrupar registros duplicados com reduce, consolidando campos únicos e armazenando variações em arrays

### Exemplo de dados retornados do banco com duplicações.

````ts

const object = [
    {
        // Repetido
		"id_called": 77,
		"title_called": "Gdhdg",
		"description_called": "Gdhdg",
		"statu_called": "open",
		"appointment_Time": "2025-08-06T12:00:00.000Z",
		"updated_at_called": "2025-08-07T13:43:22.205Z",
		"name_technical": "Mateus Silva",
		"email_technical": "mateus@email.com",
		"role_technical": "technical",
		"name_customer": "Tatiane Alves",
		"email_customer": "tatiane@email.com",
		"role_customer": "customer",

        // Diferente
        "price_service": 100,
        "title_service": "Configuração de Roteador Wi-Fi",
        "updated_at_comments": "2025-08-06T15:59:02.436",
        "description_comments": "Comentário testedd"
	},
    {
         // Repetido
		"id_called": 77,
		"title_called": "Gdhdg",
		"description_called": "Gdhdg",
		"statu_called": "open",
		"appointment_Time": "2025-08-06T12:00:00.000Z",
		"updated_at_called": "2025-08-07T13:43:22.205Z",
		"name_technical": "Mateus Silva",
		"email_technical": "mateus@email.com",
		"role_technical": "technical",
		"name_customer": "Tatiane Alves",
		"email_customer": "tatiane@email.com",
		"role_customer": "customer",

        // Diferente
        "price_service": 220,
        "title_service": "Auditoria de Segurança Básica",
        "updated_at_comments": "2025-08-06T16:23:33.538",
        "description_comments": "Tarefa teste"	
	},
    {
      // Repetido
		"id_called": 78,
		"title_called": "Gdhdg",
		"description_called": "Gdhdg",
		"statu_called": "open",
		"appointment_Time": "2025-08-06T12:00:00.000Z",
		"updated_at_called": "2025-08-07T13:43:22.205Z",
		"name_technical": "Mateus Silva",
		"email_technical": "mateus@email.com",
		"role_technical": "technical",
		"name_customer": "Tatiane Alves",
		"email_customer": "tatiane@email.com",
		"role_customer": "customer",
    
         // Repetido
        "price_service": 220,
        "title_service": "Auditoria de Segurança Básica",
        "updated_at_comments": "2025-08-06T16:23:33.538",
        "description_comments": "Tarefa teste"	
	}
]

````

### Transformando dados duplicados em uma estrutura única com `reduce`

````ts
const teste = object.reduce((acc, item) => {
   // Se ainda não existe no acumulador, cria a base
   if(!acc[item.id_called]){
      acc[item.id_called] = {
            id_called: item.id_called,
            title_called: item.title_called,
            description_called: item.description_called,
            statu_called: item.statu_called,
            appointment_Time: item.appointment_Time,
            updated_at_called: item.updated_at_called,
            name_technical: item.name_technical,
            email_technical: item.email_technical,
            role_technical: item.role_technical,
            name_customer: item.name_customer,
            email_customer: item.email_customer,
            role_customer: item.role_customer,
            services: [],
            comments: []
      }
   }

   // Adiciona service e comentário
   acc[item.id_called].services.push({
      price_service: item.price_service,
      title_service: item.title_service
   })

   acc[item.id_called].comments.push({
      updated_at_comments: item.updated_at_comments,
      description_comments: item.description_comments
   })

   return acc
}, {})

// Se quiser transformar de objeto em array:
const result = Object.values(teste)

````

### Saída:

````ts
[
  {
    id_called: 77,
    title_called: 'Gdhdg',
    description_called: 'Gdhdg',
    statu_called: 'open',
    appointment_Time: '2025-08-06T12:00:00.000Z',
    updated_at_called: '2025-08-07T13:43:22.205Z',
    name_technical: 'Mateus Silva',
    email_technical: 'mateus@email.com',
    role_technical: 'technical',
    name_customer: 'Tatiane Alves',
    email_customer: 'tatiane@email.com',
    role_customer: 'customer',
    services: [
      {
         price_service: 100,
         title_service: 'Configuração de Roteador Wi-Fi'
      },
      {
         price_service: 220,
         title_service: 'Auditoria de Segurança Básica'
      }
   ],
    comments: [
      {
         updated_at_comments: '2025-08-06T15:59:02.436',
         description_comments: 'Comentário testedd'
      },
      {
         updated_at_comments: '2025-08-06T16:23:33.538',
         description_comments: 'Tarefa teste'
      }
   ]
  },
  {
    id_called: 78,
    title_called: 'Gdhdg',
    description_called: 'Gdhdg',
    statu_called: 'open',
    appointment_Time: '2025-08-06T12:00:00.000Z',
    updated_at_called: '2025-08-07T13:43:22.205Z',
    name_technical: 'Mateus Silva',
    email_technical: 'mateus@email.com',
    role_technical: 'technical',
    name_customer: 'Tatiane Alves',
    email_customer: 'tatiane@email.com',
    role_customer: 'customer',
    services: [
      {
         price_service: 220,
         title_service: 'Auditoria de Segurança Básica'
      }
   ],
    comments: [
      {
         updated_at_comments: '2025-08-06T16:23:33.538',
         description_comments: 'Tarefa teste'
      }
   ]
  }
]

````

----

### Exemplo contendo duplicações de serviços, comentários e do próprio objeto

````ts
const refature = query.rows.reduce((acc, called, index) => {
   if(!acc[called.id_called]){
      acc[called.id_called] = {
         id_called: called.id_called,
         title_called: called.title_called,
         description_called: called.description_called,
         statu_called: called.statu_called,
         appointment_Time: called.appointment_Time,
         updated_at_called: called.updated_at_called,
         name_technical: called.name_technical,
         email_technical: called.email_technical,
         role_customer: called.role_customer,
         services: [],
         comments: []
      }
   }

   //@ts-ignore
   if(!acc[called.id_called].services.some(service => 
         service.title_service === called.title_service 
         && service.price === called.price)){

      acc[called.id_called].services.push({
         title_service: called.title_service,
         price: called.price
      })

   }

   //@ts-ignore
   if(!acc[called.id_called].comments.some(comment => 
         comment.description === called.description 
         && String(comment.updated_at) === String(called.updated_at))){

      acc[called.id_called].comments.push({
         description: called.description,
         updated_at: called.updated_at
      })

   }

   return acc
},{})
      
// Se quiser transformar de objeto em array:
return Object.values(refature)

````