# A4: 1. Criar o índice

**Comando:**
```bash
db.movimentacoes.createIndex({ tipo: 1, terminal: 1, container: 1 }, { name: "idx_coberto" })
```

**Saída no Terminal:**
```text
idx_coberto
```

# A4: 2. Consulta coberta(com _id: 0)

**Comando:**
```bash
printjson((({executionStats: s, queryPlanner: p}) => ({winningPlan: JSON.stringify(p.winningPlan), totalDocsExamined: s.totalDocsExamined, totalKeysExamined: s.totalKeysExamined, nReturned: s.nReturned, executionTimeMillis: s.executionTimeMillis}))(db.movimentacoes.find({ tipo: "inspecao", terminal: "T1" }, { _id: 0, container: 1 }).explain("executionStats")))
```

**Saída no Terminal:**
```text
{
  winningPlan: '{"isCached":false,"stage":"PROJECTION_COVERED","transformBy":{"_id":0,"container":1},"inputStage":{"stage":"IXSCAN","nss":"logiporto.movimentacoes","keyPattern":{"tipo":1,"terminal":1,"container":1},"indexName":"idx_coberto","isMultiKey":false,"multiKeyPaths":{"tipo":[],"terminal":[],"container":[]},"isUnique":false,"isSparse":false,"isPartial":false,"indexVersion":2,"direction":"forward","indexBounds":{"tipo":["[\\"inspecao\\", \\"inspecao\\"]"],"terminal":["[\\"T1\\", \\"T1\\"]"],"container":["[MinKey, MaxKey]"]}}}',
  totalDocsExamined: 0,
  totalKeysExamined: 16237,
  nReturned: 16237,
  executionTimeMillis: 23
}
```

# A4: 3. Sem _id: 0

**Comando:**
```bash
printjson((({executionStats: s, queryPlanner: p}) => ({winningPlan: JSON.stringify(p.winningPlan), totalDocsExamined: s.totalDocsExamined, totalKeysExamined: s.totalKeysExamined, nReturned: s.nReturned, executionTimeMillis: s.executionTimeMillis}))(db.movimentacoes.find({ tipo: "inspecao", terminal: "T1" }, { container: 1 }).explain("executionStats")))
```

**Saída no Terminal:**
```text
{
  winningPlan: '{"isCached":false,"stage":"PROJECTION_SIMPLE","transformBy":{"container":1},"inputStage":{"stage":"FETCH","nss":"logiporto.movimentacoes","inputStage":{"stage":"IXSCAN","nss":"logiporto.movimentacoes","keyPattern":{"tipo":1,"terminal":1,"container":1},"indexName":"idx_coberto","isMultiKey":false,"multiKeyPaths":{"tipo":[],"terminal":[],"container":[]},"isUnique":false,"isSparse":false,"isPartial":false,"indexVersion":2,"direction":"forward","indexBounds":{"tipo":["[\\"inspecao\\", \\"inspecao\\"]"],"terminal":["[\\"T1\\", \\"T1\\"]"],"container":["[MinKey, MaxKey]"]}}}}',
  totalDocsExamined: 16237,
  totalKeysExamined: 16237,
  nReturned: 16237,
  executionTimeMillis: 291
}
```