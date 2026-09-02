# Prática MongoDb
**1. Busca pelo nome e projeta apenas os campos desejados, ocultando o _id**

`db.customers.find({"name": "Ana"}, {"_id": 0, "name":1, "city":2})`

`db.customers.find({"name": "Carlos"}, {"_id": 0, "name":1, "city":2})`


**2. Atualiza o campo active do Carlos via $set.**

 `db.customers.updateOne({"name": "Carlos"}, {$set:{"active": "true"}})`


**3. Adiciona o campo "state": "BA" a todos os clientes de Salvador.**

` db.customers.updateMany({"city": "Salvador"}, {$set:{"state": "BA"}})`


**4. Soma 50 pontos ao saldo atual da Ana usando $inc**

` db.customers.updateMany({"name": "Ana"}, {$inc:{"points": 50}})`


**5. Cadastra um novo cliente completo na coleção com insertOne.**

` db.customers.insertOne({
   "name": "Fernando",
   "age": 29,
   "city": "Recife",
   "active": true,
   "points": 90 })`


**6. Remove permanentemente o cadastro da Eduarda com deleteOne**

`db.customers.deleteOne({"name": "Eduarda"})`


**7. Adiciona o novo campo "vip": true no documento da Daniela.**

 `db.customers.updateOne({"name": "Daniela"}, {$set:{"vip": true}})`


**8. Deleta o atributo points do Bruno utilizando o operador $unset.**

`db.customers.updateOne({"name": "Bruno"},{$unset: {"points": 300}} )`


**9. Ordena os clientes por idade em ordem decrescente.**

`db.clientes.find().sort({ idade: -1 })`

**10. Exibe somente clientes ativos com mais de 30 anos.**

`db.customers.find({ active: true, age: { $gt: 30 } }, { _id: 0, name: 1 })`
