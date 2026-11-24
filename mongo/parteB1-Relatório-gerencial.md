# B1: 1. Índice que beneficia o $match

**Comando:**
```bash
db.movimentacoes.createIndex({ classe: 1, ts: 1 }, { name: "idx_b1" })
```

**Saída no Terminal:**
```text
idx_b1
```

# B1: 2. Pipeline

**Comando:**
```bash
db.movimentacoes.aggregate([
  { $match: { classe: "Refrigerado", ts: { $gte: ISODate("2026-04-01") } } },
  { $group: {
      _id: "$terminal",
      total_movimentacoes: { $sum: 1 },
      peso_total: { $sum: "$peso_kg" },
      peso_medio: { $avg: "$peso_kg" },
      maior_peso: { $max: "$peso_kg" }
  } },
  { $sort: { peso_total: -1 } },
  { $limit: 3 },
  { $project: { _id: 0, terminal: "$_id", total_movimentacoes: 1, peso_total: 1, peso_medio: 1, maior_peso: 1 } }
])
```

**Saída no Terminal:**
```text
[
  {
    total_movimentacoes: 14383,
    peso_total: 229062139,
    peso_medio: 15925.894389209483,
    maior_peso: 30999,
    terminal: 'T1'
  },
  {
    total_movimentacoes: 14086,
    peso_total: 224358993,
    peso_medio: 15927.800156183444,
    maior_peso: 30999,
    terminal: 'T5'
  },
  {
    total_movimentacoes: 14011,
    peso_total: 223578930,
    peso_medio: 15957.385625579902,
    maior_peso: 30995,
    terminal: 'T2'
  }
]
```
# B1: 3. Explain: quantos docs entraram no $group

**Comando:**
```bash
db.movimentacoes.explain("executionStats").aggregate([
  { $match: { classe: "Refrigerado", ts: { $gte: ISODate("2026-04-01") } } },
  { $group: { _id: "$terminal", total_movimentacoes: { $sum: 1 }, peso_total: { $sum: "$peso_kg" }, peso_medio: { $avg: "$peso_kg" }, maior_peso: { $max: "$peso_kg" } } },
  { $sort: { peso_total: -1 } },
  { $limit: 3 },
  { $project: { _id: 0, terminal: "$_id", total_movimentacoes: 1, peso_total: 1, peso_medio: 1, maior_peso: 1 } }
])
```

**Saída no Terminal:**
```text
 command: {
    aggregate: 'movimentacoes',
    pipeline: [
      {
        '$match': {
          classe: 'Refrigerado',
          ts: { '$gte': ISODate('2026-04-01T00:00:00.000Z') }
        }
      },
      {
        '$group': {
          _id: '$terminal',
          total_movimentacoes: { '$sum': 1 },
          peso_total: { '$sum': '$peso_kg' },
          peso_medio: { '$avg': '$peso_kg' },
          maior_peso: { '$max': '$peso_kg' }
        }
      },
      { '$sort': { peso_total: -1 } },
      { '$limit': 3 },
      {
        '$project': {
          _id: 0,
          terminal: '$_id',
          total_movimentacoes: 1,
          peso_total: 1,
          peso_medio: 1,
          maior_peso: 1
        }
      }
    ],
    cursor: {},
    '$db': 'logiporto'
  },
  ok: 1
}
```