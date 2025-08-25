🔹 Encodings mais usados no Node.js

*  utf8 → padrão do Node.js (se não especificado).
*  utf16le → UTF-16 little endian (cada caractere ocupa 2 bytes, usado em arquivos do Windows, como .txt do Notepad).
*  latin1 (ou binary) → ISO-8859-1 (um byte por caractere, útil para dados binários simples).
*  ascii → apenas os primeiros 128 caracteres da tabela ASCII (A–Z, números, símbolos básicos).

Outros encodings suportados

*  base64 → codifica/decodifica em Base64.

*  hex → lê ou escreve bytes em representação hexadecimal.

*  ucs2 → alias para utf16le.

---

</br>

🔹 Importando o módulo fs

````ts
import fs from "node:fs"
````

🔹 Verificando se um caminho existe

````ts
const caminho = "./exemplo.txt";

if (fs.existsSync(caminho)) {
  console.log("O arquivo existe!");
} else {
  console.log("O arquivo não existe.");
}
````

🔹 Leitura de arquivos (assíncrona)

````ts
const conteudo = await fs.promises.readFile("./exemplo.txt", "utf8");
console.log(conteudo);
````

🔹 Escrita de arquivos (assíncrona)

````ts
await fs.promises.writeFile("./saida.txt", "Conteúdo de exemplo", "utf8");
````

🔹 Listando arquivos dentro de uma pasta

````ts
const arquivos = fs.readdirSync("./pasta-exemplo");
console.log(arquivos);
````