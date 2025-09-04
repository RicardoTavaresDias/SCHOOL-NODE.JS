- [VOLTAR](./index.md)

</br>

# Dayjs

Biblioteca para manipulação de datas

### Instalação

````ts
npm install dayjs
````

Uso:

 ````ts
import dayjs from "dayjs"
import "dayjs/locale/pt-br"

dayjs.locale("pt-br")

export { dayjs }
 ````

## 🔹Descobrir a semana de uma data.

Extensões:

````ts
import isoWeek from "dayjs/plugin/isoWeek.js"
dayjs.extend(isoWeek)
````

Uso:

````ts
// mostra o primeiro dia da semana
console.log(dayjs('2025-09-03').startOf("isoWeek").format("YYYY-MM-DD"))
// mostra o ultimo dia da semana
console.log(dayjs('2025-09-03').endOf("isoWeek").format("YYYY-MM-DD"))

// mostra o dia da semana
console.log(dayjs('2025-09-03').day()) 
````

Resultado:

````ts
2025-09-01 // segunda-feira
2025-09-07 // domingo-feira
3 // quata-feira
````


## 🔹Retornar uma boolean indicação se uma data está entre duas outras datas

Extensões:

````ts
import isBetween from 'dayjs/plugin/isBetween'

dayjs.extend(isBetween)
````

Uso:

````ts
const inicio = dayjs('2025-08-01')
const fim = dayjs('2025-08-09')

dayjs('2025-08-05').isBetween(inicio, fim, "day", "[]")
````

Resultado:

````
true
````

## 🔹Time Zone

Extensões:

````ts
import utc from 'dayjs/plugin/utc'
import timezone from 'dayjs/plugin/timezone'

dayjs.extend(utc)
dayjs.extend(timezone)

// Define o timezone padrão (opcional)
dayjs.tz.setDefault("America/Sao_Paulo")
````

Uso:

````ts
dayjs('2025-05-01T09:00:00').tz("America/Sao_Paulo").format("DD/MM/YY")
````

## 🔸Is Same
Isso indica se o objeto Day.js é o mesmo que a outra data e hora fornecida.

````ts
dayjs().isSame(dayjs('2011-01-01'))
````

Se você quiser limitar a granularidade a uma unidade diferente de milissegundos, passe-a como o segundo parâmetro.

Ao incluir um segundo parâmetro, ele corresponderá a todas as unidades iguais ou maiores. Passar o mês verificará o mês e o ano. Passar o dia verificará o dia, o mês e o ano.

````ts
dayjs().isSame('2011-01-01', 'year')
````

## 🔸Is Before

Isso indica se o objeto Day.js é anterior à outra data e hora fornecida.

````ts
dayjs().isBefore(dayjs('2011-01-01'))
````

Se você quiser limitar a granularidade a uma unidade diferente de milissegundos, passe-a como segundo parâmetro. Nesse caso, a comparação respeitará a unidade fornecida e as unidades acima.

````ts
dayjs().isBefore('2011-01-01', 'month')
````

## 🔸Is After

Isso indica se o objeto Day.js é posterior à outra data e hora fornecida.

````ts
dayjs().isAfter(dayjs('2011-01-01'))
````

Se você quiser limitar a granularidade a uma unidade diferente de milissegundos, passe-a como segundo parâmetro. Nesse caso, a comparação respeitará a unidade fornecida e as unidades acima.

````ts
dayjs().isAfter('2011-01-01', 'month')
````