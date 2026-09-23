# Estudo de NoSQL e MongoDB
## O que é NoSQL?
**NoSQL** é um paradigma de banco de dados que engloba diversos tipos de bancos de dados não relacionais. Eles são projetados especificamente para oferecer **flexibilidade**, **escalabilidade** e **alto desempenho**.
### Principais Paradigmas
Os quatro principais modelos de bancos de dados NoSQL são:
- **Orientados a Documentos:** Ex: MongoDB.
- **Chave-Valor:** Ex: Redis.
- **Famílias de Colunas (Wide-column):** Ex: Cassandra.
- **Orientados a Grafos:** Ex: Neo4j.
## MongoDB
O termo MongoDB vem de *"Humongous"* (Gigante), refletindo sua capacidade de gerenciar volumes massivos de dados de forma eficiente. Ele é um banco de dados NoSQL de código aberto e orientado a documentos.
### Diferenças para o SQL Tradicional
Diferente dos bancos relacionais que utilizam tabelas e linhas, o MongoDB armazena dados em **documentos**. Além disso, o MongoDB minimiza o uso de relacionamentos entre coleções. Em vez de utilizar `JOIN`s complexos, ele geralmente armazena dados relacionados juntos no mesmo registro através de **documentos incorporados** (*embedded documents*).
### Estrutura de Dados
A hierarquia de dados no MongoDB é organizada da seguinte forma:
- **Database:** Um servidor pode hospedar múltiplos bancos de dados.
- **Collections:** Equivalente às tabelas, as coleções agrupam os documentos.
- **Documents:** Os registros individuais.

O MongoDB possui uma estrutura *"schemaless"* (sem esquema rígido), o que permite que documentos dentro de uma mesma coleção possuam campos e estruturas diferentes entre si.
### Formato JSON e BSON
Os registros são armazenados no formato **BSON** (*Binary JSON*), que é uma representação binária do JSON.
- **Campos (Fields):** Compostos por uma chave (*key*) e um valor (*value*).
- **Tipos de Valores:** Podem ser strings, números, booleanos, arrays e até outros documentos.
## Comandos e Operações CRUD
A interação com o banco pode ser feita através do shell `mongosh`.
### Comandos de Exploração
- `show dbs`: Lista os bancos de dados disponíveis.
- `use <nome_do_db>`: Seleciona o banco de dados para uso.
- `show collections`: Lista as coleções do banco atual.
### Operações CRUD
As operações fundamentais para manipulação de dados seguem os comandos abaixo:

| Operação | Comandos Principais |
| --- | --- |
| **Create** (Criar) | `insertOne(data, options)` |
| **Read** (Ler) | `find(filter, options)`, `findOne(filter, options)` |
| **Update** (Atualizar) | `updateOne(filter, data, options)`, `updateMany(filter, data, options)`, `replaceOne(filter, data, options)` |
| **Delete** (Deletar) | `deleteOne(filter, options)`, `deleteMany(filter, options)` |

## Ecossistema MongoDB
O ecossistema dispõe de diversas ferramentas para facilitar o gerenciamento e visualização dos dados:
- **MongoDB Atlas:** Solução de banco de dados na nuvem (*Cloud*).
- **MongoDB Compass:** Interface gráfica (*GUI*) para exploração de dados.
- **MongoDB Charts:** Ferramenta para criação de dashboards e visualização de dados.
<img width="771" height="396" alt="crud-operations" src="https://github.com/user-attachments/assets/d458b1e8-4774-4893-8032-8d0caa47262e" />

- Exibir os bancos de dados

  `show databases`

- Criar banco de dados

  `use loja_informatica`

- Criar nova collection

   `db.createCollection("cliente")`

- Mostar todas as collections

  `show collections`

- Mostrar todos os documentos/objetos

   `db.cliente.find()`

- Insere apenas 1 document (objeto)

   `db.cliente.insertOne({   "nome": "jefté",   "idade": 35,   "pets": ["dora", "sabrina"],      "endereco": {    "logradouro": "Sossego"   }})`

- Inserir Muitos documents de uma vez

  `db.cliente.insertMany([{ "nome": "Brenno"}, { "nome": "João"}, { "nome": "MAria"}, { "nome": "José"}, { "nome": "Noé"}])`

- Buscar pelo campo

   `db.cliente.find({"nome": "José"})`

- Buscar pelo identificador único

   `db.cliente.find({_id: ObjectId('6a7bbab007ff2cf8649f68a9'),})`

# MongoDB: Modelagem & Schemas

**Identificadores Únicos, Tipos de Dados, Projeções e Padrões Avançados de Relacionamento (1:1, 1:N, N:M)**

## 1. Identificadores Únicos (`_id`)

* **Obrigatoriedade:** Todo documento no MongoDB deve possuir obrigatoriamente um campo chave denominado `_id`.

* **Geração Automática:** Caso não seja informado, o MongoDB gera por padrão um `ObjectId()` de 12 bytes.

* **Customização:** É possível definir valores arbitrários e personalizados para o `_id` diretamente no `insertOne`:

  ```
  db.products.insertOne({
    "_id": "my-custom-id",
    "name": "gloves"
  })
  
  ```

## 2. Documentos Incorporados (*Embedded Documents*)

* Permitem armazenar dados relacionados diretamente dentro do documento principal.

* **Vantagens:**

  * Elimina a necessidade de operações de junção de coleções (*joins* / `$lookup`) de alto custo computacional.

  * Excelente desempenho para dados que são acessados em conjunto.

* **Limitações Importantes:**

  * **Aninhamento:** Suporta até 100 níveis de aninhamento (*nesting*).

  * **Tamanho Máximo:** O documento BSON possui tamanho limite estrito de **16 MB**.

## 3. Projeção (*Projection*) e Flexibilidade de Schema

### Projeção (*Projection*)

* Define quais atributos específicos devem retornar em uma consulta de busca.

* **Benefícios:** Evita tráfego desnecessário de dados na rede, economiza largura de banda e memória da aplicação consumidora.

### Flexibilidade de Schema (*Schema-less* / Schema Flexível)

* O MongoDB não impõe schemas estáticos a nível de banco de dados por padrão.

* Documentos dentro da mesma coleção podem possuir diferentes estruturas e campos (*polimorfismo*).

* Permite rápida evolução de código sem necessidade de rotinas de migração pesadas (*DDL migrations*).

* A aplicação pode, opcionalmente, impor validações estruturais via **JSON Schema**.

* **Espectro de Schemas:** Vai do "Caos" (estruturas totalmente divergentes), passando por "Dados Extras", até a "Igualdade Completa" (padrão relacional/SQL).

## 4. Tipos de Dados Suportados

| Categoria | Tipos Comuns | Exemplo Prático |
| :--- | :--- | :--- |
| **Texto & Booleano** | `Text`, `Boolean` | `"Jefté"`, `true` |
| **Numéricos** | `Integer (int32)`, `Long (int64)`, `Decimal` | `55`, `10000000000`, `12.99` |
| **Identificadores** | `ObjectId` | `ObjectId("5b98d4654d01c52e1637a99b")` |
| **Datas & Tempo** | `ISODate`, `Timestamp` | `ISODate("2026-09-15")` |
| **Estruturas Complexas** | `Embedded Document`, `Array` | `{ "a": { ... } }`, `["item1", "item2"]` |

## 5. Perguntas Essenciais de Arquitetura & Modelagem

Antes de definir as coleções e schemas, deve-se avaliar:

1. **Quais dados são necessários?** Define os campos e dependências.

2. **Onde o dado é consumido?** Define as coleções e agrupamentos de atributos.

3. **Qual o tipo de exibição?** Determina as consultas (*queries*) prioritárias.

4. **Qual a proporção Leitura vs. Escrita?**

   * **Muitas Consultas (*Read-Heavy*):** Otimiza o dado pronto no formato exigido pela interface/cliente. Prioriza **Documentos Incorporados** (*Embedded*).

   * **Muitas Gravações (*Write-Heavy*):** Otimiza para evitar duplicação ou redundância, permitindo alterações atômicas em local único. Prioriza **Referências** (*References*).

## 6. Padrões de Relacionamento

### 6.1. Relacionamento 1:1 (Um para Um)

* **Embedded (Incorporado):** Quando os dados pertencem exclusivamente à entidade principal e são lidos conjuntamente.

  * *Exemplo:* Paciente e Resumo da Doença (`diseaseSummary`).

    ```
    db.patients.insertOne({
      name: "Jefté",
      age: 35,
      diseaseSummary: {
        diseases: ["cold", "broken leg"]
      }
    })
    
    ```

* **References (Referência):** Quando as entidades têm ciclo de vida independente.

  * *Exemplo:* Pessoa e Carro via `ObjectId`.

    ```
    db.cars.insertOne({
      model: "BMW",
      owner: ObjectId("5b9...")
    })
    
    ```

### 6.2. Relacionamento 1:N (Um para Muitos)

* **Embedded (Incorporado):** Quando os subitens pertencem ao contexto principal e o número de itens é previsível e limitado.

  * *Exemplo:* Tópico de fórum com array de respostas (`answers`).

* **References (Referência):** Quando o número de itens filhos é potencialmente ilimitado, evitando estourar o limite de 16MB.

  * *Exemplo:* Cidade e Cidadãos (milhões de habitantes apontam para o `cityId`).

    ```
    db.citizens.insertMany([
      { name: "Jefté", cityId: ObjectId("5b9...") },
      { name: "Brenno", cityId: ObjectId("5b9...") }
    ])
    
    ```

### 6.3. Relacionamento N:M (Muitos para Muitos)

* **Embedded (Snapshot/Histórico):** Congelar o estado do dado em uma das pontas.

  * *Exemplo:* Clientes guardando um array de pedidos realizados com produtos embutidos.

* **Array de Referências:** Ambas as entidades possuem ciclos de vida independentes e dados dinâmicos compartilhados.

  * *Exemplo:* Livros guardando um array de identificadores de Autores.

    ```
    db.books.updateOne({}, {
      $set: {
        authors: [
          ObjectId("5b98d9e44d01c52e1637a9a6"),
          ObjectId("5b98d9e44d01c52e1637a9a7")
        ]
      }
    })
    
    ```

## 7. Resumo Comparativo: Embedded vs. References

| Característica | Documentos Incorporados (Embedded) | Referências (References) |
| :--- | :--- | :--- |
| **Organização** | Agrupa os dados no mesmo documento[cite: 1] | Divide os dados entre coleções distintas[cite: 1] |
| **Caso de Uso** | Dados que pertencem juntos e sem reuso[cite: 1] | Dados compartilhados ou independentes[cite: 1] |
| **Desempenho** | Otimizado para leitura rápida (sem joins)[cite: 1] | Evita redundância de escrita[cite: 1] |
| **Atenção/Gargalo** | Limite máximo de **16 MB** por documento[cite: 1] | Requer consultas adicionais ou `$lookup`[cite: 1] |

## 8. Guia Prático para Decisão

```
                Acesso frequente conjunto?
                         │
        ┌────────────────┴────────────────┐
       SIM                               NÃO
        │                                 │
Dados compartilhados?                     │
        │                                 │
  ┌─────┴─────┐                           │
 NÃO         SIM                          │
  │           │                           │
Tamanho < 16MB?                           │
  │           │                           │
 ┌┴┐          │                           │
SIM NÃO       │                           │
 │   │        │                           │
 ▼   └────────┴───────────► ◄─────────────┘
USE                       USE
EMBEDDED                  REFERENCES

```
