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
