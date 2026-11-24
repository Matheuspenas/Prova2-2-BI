# A3: o TTL que não apaga


# A3: 1 Ver o estado atual

**Comando:**
```bash
db.alertas.getIndexes()
```

**Saída no Terminal:**
```text
{ v: 2, key: { _id: 1 }, name: '_id_' }
```

**Comando:**
```bash
db.alertas.findOne()
```

**Saída no Terminal:**
```text
 _id: ObjectId('6b04c4adb18c72a909b77ed0'),
  sensor: 'S451',
  nivel: 'info',
  registrado_em: '2026-09-14T10:34:25.132Z'
```

# A3: 2. Reproduzir o índice do desenvolvedor anterior

**Comando:**
```bash
db.alertas.createIndex({ registrado_em: 1 }, { name: "ttl_errado", expireAfterSeconds: 2592000 })
```

**Saída no Terminal:**
```text
ttl_errado
```

# A3: 3 Comprovar a causa raiz

**Comando:**
```bash
db.alertas.aggregate([{ $group: { _id: { $type: "$registrado_em" }, n: { $sum: 1 } } }])
```

**Saída no Terminal:**
```text
[ { _id: 'string', n: 100000 } ]
```

**Comando:**
```bash
db.alertas.countDocuments()
```

**Saída no Terminal:**
```text
100000
```

# A4: 4. Corrigir

**Comando:**
```bash
db.alertas.dropIndex("ttl_errado")
```

**Saída no Terminal:**
```text
{ nIndexesWas: 2, ok: 1 }
```

**Comando:**
```bash
db.alertas.createIndex({ registrado_em: 1 }, { name: "ttl_30d", expireAfterSeconds: 2592000 })
```

**Saída no Terminal:**
```text
ttl_30d
```

# A4: 5. Prova de que o índice correto funciona com Date

**Comando:**
```bash
db.alertas.insertOne({ sensor: "TESTE", nivel: "info", registrado_em: new Date(Date.now() - 40*24*3600*1000) })
```

**Saída no Terminal:**
```text
{
  acknowledged: true,
  insertedId: ObjectId('6b04e04b2014ba31f4e5feab')
}
```

**Comando:**
```bash
db.alertas.countDocuments({ sensor: "TESTE" })
```

**Saída no Terminal:**
```text
{
 0
}
```