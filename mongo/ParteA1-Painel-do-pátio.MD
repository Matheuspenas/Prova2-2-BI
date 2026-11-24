# A1 Painel do pátio

**Comando:**
```bash
db.movimentacoes.find({
  terminal: "T1",
  classe: "Refrigerado",
  ts: { $gte: ISODate("2026-04-01") }
}).sort({ peso_kg: -1 }).limit(20)
```

**Saída no Terminal**
```text
 {
    _id: ObjectId('6b04c4aab18c72a909b562ae'),
    container: 'CTN11038',
    tipo: 'descarga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30999,
    ts: ISODate('2026-07-02T10:58:40.751Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.48009009369882, -25.460245691903403 ]
    },
    tags: [ 'urgente', 'overweight', 'refrigerado' ],
    obs: 'doca vistoria patio descarga guindaste vistoria atraso atraso'
  },
  {
    _id: ObjectId('6b04c4a9b18c72a909b4889a'),
    container: 'CTN04213',
    tipo: 'carga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30993,
    ts: ISODate('2026-09-19T07:30:15.227Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.47064685181715, -25.463397386821452 ]
    },
    tags: [ 'lacre_violado', 'granel' ],
    obs: 'descarga lacre liberado guindaste balanca guindaste atraso vistoria'
  },
  {
    _id: ObjectId('6b04c4a4b18c72a909b1e458'),
    container: 'CTN29757',
    tipo: 'descarga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30991,
    ts: ISODate('2026-06-02T08:57:48.296Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.50888194255997, -25.47992440017406 ]
    },
    tags: [ 'lacre_violado' ],
    obs: 'balanca fila liberado lacre descarga fila balanca descarga'
  },
  {
    _id: ObjectId('6b04c4a5b18c72a909b2b2ff'),
    container: 'CTN41145',
    tipo: 'gate_out',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30988,
    ts: ISODate('2026-09-10T03:58:48.216Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.4712816383387, -25.467735121422447 ]
    },
    tags: [ 'transbordo', 'exportacao' ],
    obs: 'descarga carga guindaste lacre doca vistoria doca fila'
  },
  {
    _id: ObjectId('6b04c4a5b18c72a909b25c45'),
    container: 'CTN59233',
    tipo: 'descarga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30983,
    ts: ISODate('2026-10-23T08:56:14.999Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.50644186945167, -25.477415014384313 ]
    },
    tags: [ 'lacre_violado', 'importacao', 'perigoso' ],
    obs: 'doca vistoria atraso patio descarga atraso balanca navio'
  },
  {
    _id: ObjectId('6b04c4aab18c72a909b5946a'),
    container: 'CTN30960',
    tipo: 'inspecao',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30980,
    ts: ISODate('2026-04-08T20:45:52.283Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.48866335205268, -25.451175017328932 ]
    },
    tags: [ 'transbordo', 'transbordo' ],
    obs: 'lacre balanca fila atraso lacre vistoria doca fila'
  },
  {
    _id: ObjectId('6b04c4a3b18c72a909b17f61'),
    container: 'CTN57730',
    tipo: 'carga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30979,
    ts: ISODate('2026-05-27T17:12:19.770Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.49508386733243, -25.474445846595337 ]
    },
    tags: [ 'lacre_violado', 'exportacao' ],
    obs: 'vistoria patio lacre vistoria vistoria carga liberado balanca'
  },
  {
    _id: ObjectId('6b04c4a7b18c72a909b39c9a'),
    container: 'CTN35509',
    tipo: 'gate_out',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30972,
    ts: ISODate('2026-05-29T03:46:04.635Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.508939214788846, -25.481674100784584 ]
    },
    tags: [ 'urgente' ],
    obs: 'descarga balanca balanca liberado carga guindaste fila atraso'
  },
  {
    _id: ObjectId('6b04c4a4b18c72a909b1d4ee'),
    container: 'CTN21709',
    tipo: 'inspecao',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30971,
    ts: ISODate('2026-08-11T02:04:13.296Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.51937312991824, -25.491731515654827 ]
    },
    tags: [ 'lacre_violado' ],
    obs: 'liberado balanca patio carga guindaste fila vistoria doca'
  },
  {
    _id: ObjectId('6b04c4a9b18c72a909b516ba'),
    container: 'CTN57596',
    tipo: 'carga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30969,
    ts: ISODate('2026-07-27T00:44:14.220Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.50864904131042, -25.45126299050171 ]
    },
    tags: [ 'urgente', 'importacao', 'fragil' ],
    obs: 'carga patio carga balanca navio doca atraso doca'
  },
  {
    _id: ObjectId('6b04c4acb18c72a909b6b56f'),
    container: 'CTN39817',
    tipo: 'gate_out',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30967,
    ts: ISODate('2026-06-20T07:40:58.328Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.516049493621104, -25.452354336949064 ]
    },
    tags: [ 'perigoso', 'refrigerado' ],
    obs: 'fila liberado patio patio descarga descarga descarga liberado'
  },
  {
    _id: ObjectId('6b04c4a8b18c72a909b45213'),
    container: 'CTN27213',
    tipo: 'gate_in',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30961,
    ts: ISODate('2026-09-15T20:55:12.947Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.495955481932036, -25.469054566614794 ]
    },
    tags: [ 'alto_valor', 'perigoso', 'overweight' ],
    obs: 'guindaste lacre patio liberado fila patio patio carga'
  },
  {
    _id: ObjectId('6b04c4abb18c72a909b618a6'),
    container: 'CTN46733',
    tipo: 'gate_in',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30959,
    ts: ISODate('2026-10-24T14:35:48.397Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.513106824602005, -25.496207692380995 ]
    },
    tags: [ 'overweight', 'lacre_violado', 'granel' ],
    obs: 'vistoria descarga atraso liberado descarga liberado patio carga'
  },
  {
    _id: ObjectId('6b04c4a3b18c72a909b16e96'),
    container: 'CTN42645',
    tipo: 'gate_in',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30956,
    ts: ISODate('2026-08-18T11:09:44.908Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.482311217107345, -25.47213727182243 ]
    },
    tags: [ 'overweight', 'overweight', 'urgente' ],
    obs: 'balanca balanca liberado navio navio descarga patio liberado'
  },
  {
    _id: ObjectId('6b04c4a9b18c72a909b49b16'),
    container: 'CTN50171',
    tipo: 'carga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30949,
    ts: ISODate('2026-10-04T06:00:18.951Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.49453123929445, -25.472293960372916 ]
    },
    tags: [ 'refrigerado', 'urgente' ],
    obs: 'lacre doca carga descarga vistoria liberado carga doca'
  },
  {
    _id: ObjectId('6b04c4a5b18c72a909b2dc19'),
    container: 'CTN50044',
    tipo: 'gate_in',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30948,
    ts: ISODate('2026-05-03T08:17:46.067Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.48993256695569, -25.46891444744542 ]
    },
    tags: [ 'alto_valor', 'perigoso' ],
    obs: 'lacre patio liberado patio balanca navio atraso carga'
  },
  {
    _id: ObjectId('6b04c4a4b18c72a909b2071a'),
    container: 'CTN26829',
    tipo: 'carga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30947,
    ts: ISODate('2026-07-27T11:28:30.649Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.509118627109565, -25.45370729662245 ]
    },
    tags: [ 'granel', 'alto_valor' ],
    obs: 'fila liberado descarga lacre atraso guindaste fila doca'
  },
  {
    _id: ObjectId('6b04c4acb18c72a909b6c07a'),
    container: 'CTN41208',
    tipo: 'gate_in',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30946,
    ts: ISODate('2026-04-18T17:16:48.745Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.48394342185231, -25.491956193151417 ]
    },
    tags: [ 'overweight', 'fragil', 'inspecao_fiscal' ],
    obs: 'fila atraso balanca liberado carga atraso balanca liberado'
  },
  {
    _id: ObjectId('6b04c4aab18c72a909b5c2e8'),
    container: 'CTN45558',
    tipo: 'gate_in',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30944,
    ts: ISODate('2026-07-30T18:54:43.564Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.498487771551595, -25.481349260639398 ]
    },
    tags: [ 'lacre_violado', 'overweight' ],
    obs: 'patio balanca doca fila navio balanca balanca descarga'
  },
  {
    _id: ObjectId('6b04c4aab18c72a909b57ef6'),
    container: 'CTN15984',
    tipo: 'carga',
    terminal: 'T1',
    classe: 'Refrigerado',
    peso_kg: 30944,
    ts: ISODate('2026-05-30T04:59:16.774Z'),
    posicao: {
      type: 'Point',
      coordinates: [ -48.487590225744064, -25.450384358724115 ]
    },
    tags: [ 'urgente' ],
    obs: 'guindaste navio navio patio descarga vistoria carga atraso'
  }
```

# A1 a) sem índice

**Comando:**
```bash
 m(q().explain("executionStats"), "a) Sem índice")
```

**Saída no Terminal**
```text
{
  stages: 'SORT > COLLSCAN',
  totalDocsExamined: 400000,
  totalKeysExamined: 0,
  nReturned: 20,
  executionTimeMillis: 527
}
| a) Sem índice | SORT > COLLSCAN | 400000 | 0 | 20 | 527 | sim |
```

# A1 b) índice na ordem do filtro

**Comando:**
```bash
db.movimentacoes.createIndex({ terminal: 1, classe: 1, ts: 1, peso_kg: -1 }, { name: "idx_filtro" })
```

**Saída no Terminal**
```text
idx_filtro
```

**Comando:**
```bash
m(q().explain("executionStats"), "b) {terminal,classe,ts,peso_kg:-1}"))
```

**Saída no Terminal**
```text
{
  stages: 'FETCH > SORT > IXSCAN',
  totalDocsExamined: 20,
  totalKeysExamined: 14383,
  nReturned: 20,
  executionTimeMillis: 29
}
| b) {terminal,classe,ts,peso_kg:-1} | FETCH > SORT > IXSCAN | 20 | 14383 | 20 | 29 | sim |
```

# A1 c) índice ESR

**Comando:**
```bash
db.movimentacoes.dropIndex("idx_filtro")
```

**Saída no Terminal**
```text
{ nIndexesWas: 2, ok: 1 }
```

**Comando:**
```bash
db.movimentacoes.createIndex({ terminal: 1, classe: 1, peso_kg: -1, ts: 1 }, { name: "idx_esr" })
```

**Saída no Terminal**
```text
idx_esr
```

**Comando:**
```bash
m(q().explain("executionStats"), "c) ESR {terminal,classe,peso_kg:-1,ts}")
```

**Saída no Terminal**
```text
{
  stages: 'LIMIT > FETCH > IXSCAN',
  totalDocsExamined: 20,
  totalKeysExamined: 32,
  nReturned: 20,
  executionTimeMillis: 5
}
| c) ESR {terminal,classe,peso_kg:-1,ts} | LIMIT > FETCH > IXSCAN | 20 | 32 | 20 | 5 | não |
```

# A1 d) Comparação das três estratégias

Consulta: terminal "T1", classe "Refrigerado", ts >= 2026-04-01, sort peso_kg desc, limit 20.

| Cenário | Índice | Stages | totalDocsExamined | totalKeysExamined | nReturned | executionTimeMillis | SORT em memória |
|---|---|---|---|---|---|---|---|
| a) Sem índice | apenas `_id_` | SORT > COLLSCAN | 400000 | 0 | 20 | 527 | sim |
| b) Ordem do filtro | `{terminal:1, classe:1, ts:1, peso_kg:-1}` | FETCH > SORT > IXSCAN | 20 | 14383 | 20 | 29 | sim |
| c) ESR | `{terminal:1, classe:1, peso_kg:-1, ts:1}` | LIMIT > FETCH > IXSCAN | 20 | 32 | 20 | 5 | não |

(Nos stages, a leitura é de baixo para cima: o IXSCAN/COLLSCAN é o primeiro estágio executado.)

## Diferença entre b) e c)

Uma B-Tree armazena as chaves ordenadas pela sequência dos campos do índice. Ela só entrega resultados já ordenados quando a ordem do sort coincide com a ordem em que as chaves são percorridas.

**Em b)**, `ts` vem antes de `peso_kg`. Como o filtro em `ts` é um range, o IXSCAN percorre um trecho que contém muitos valores distintos de `ts`. Dentro de cada valor de `ts` o peso está ordenado, mas o conjunto todo não está em ordem de `peso_kg`. Por isso o plano precisa de um estágio SORT em memória, e para ordenar ele examina todas as chaves que casam com o filtro: 14.383. Só depois do SORT é feito o FETCH, e só dos 20 vencedores. Por isso totalDocsExamined é 20, e não 14.383: o índice contém `peso_kg`, então o sort é feito sobre as chaves, sem ler os documentos. O custo restante está nas 14.383 chaves lidas e ordenadas em RAM.

**Em c)**, seguindo a regra ESR (Equality, Sort, Range), `terminal` e `classe` (igualdades) fixam um trecho contíguo da B-Tree, e dentro dele as chaves já estão em ordem decrescente de `peso_kg`. O Mongo percorre nessa ordem, avalia o range de `ts` sobre a própria chave do índice e para no limit de 20. Não há SORT em memória, e foram lidas apenas 32 chaves: as 20 que casaram e 12 descartadas por `ts` anterior a 2026-04-01.

**Resumo:** de a) para c), as chaves lidas caem de 400.000 documentos varridos para 32 e o tempo vai de 527 ms para 5 ms. A diferença entre b) e c) é a ordem dos campos: colocar o sort antes do range permite que o índice entregue os dados já ordenados, evitando o SORT em memória e lendo 14.383 chaves a menos (cerca de 450 vezes menos).