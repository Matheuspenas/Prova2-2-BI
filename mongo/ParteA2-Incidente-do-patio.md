# A2a: sem índice geoespacial 


**Comando:**
```bash
const qGeo = () => db.movimentacoes.find({
  posicao: { $near: { $geometry: { type: "Point", coordinates: [-48.5000, -25.4880] }, $maxDistance: 300 } }
}).limit(10);
```

```bash
 qGeo().toArray()
```

**Saída no Terminal**
```text
MongoServerError[NoQueryExecutionPlans]: unable to find index for $geoNear query
```

# A2b: criar o índice


**Comando:**
```bash
db.movimentacoes.createIndex({ posicao: "2dsphere" }, { name: "idx_geo" })
```

**Saída no Terminal**
```text
idx_geo
```

# A2c: executar com explain

**Comando:**
```bash
qGeo().toArray().forEach(d => print(d.container, JSON.stringify(d.posicao.coordinates)))
```

**Saída no Terminal**
```text
CTN03515 [-48.50002830103506,-25.487957890890538]
CTN59457 [-48.499952795035206,-25.488044674147385]
CTN58184 [-48.49996858324623,-25.488057885796298]
CTN39554 [-48.50003027416999,-25.487939532788005]
CTN51067 [-48.49996686041588,-25.487919952336235]
CTN27075 [-48.49990532690892,-25.4880004710285]
CTN17194 [-48.50000736449613,-25.488088063080795]
CTN46798 [-48.49988496645121,-25.48802908437792]
CTN30921 [-48.50012730331393,-25.48797296192497]
CTN34371 [-48.50013457537163,-25.488008178863673]
```

```text
Métricas do plano
```

**Comando:**
```bash
printjson((({executionStats: s, queryPlanner: p}) => ({stage: p.winningPlan.stage, inputStage: p.winningPlan.inputStage && p.winningPlan.inputStage.stage, totalDocsExamined: s.totalDocsExamined, totalKeysExamined: s.totalKeysExamined, nReturned: s.nReturned, executionTimeMillis: s.executionTimeMillis}))(db.movimentacoes.find({posicao: {$near: {$geometry: {type: "Point", coordinates: [-48.5000, -25.4880]}, $maxDistance: 300}}}).limit(10).explain("executionStats")))
```

**Saída no Terminal**
```text
{
  stage: 'LIMIT',
  inputStage: 'GEO_NEAR_2DSPHERE',
  totalDocsExamined: 50,
  totalKeysExamined: 74,
  nReturned: 10,
  executionTimeMillis: 5
}
```