# B2a: rodar o código exatamente como está

**Comando:**
```bash
db.movimentacoes.aggregate([
  { $project: { terminal: 1, classe: 1 } },
  { $group: { _id: { terminal: "$terminal", classe: "$classe" }, kg_total: { $sum: "peso_kg" }, mov: { $sum: 1 } } },
  { $limit: 3 },
  { $sort: { kg_total: -1 } },
  { $match: { "_id.classe": "Refrigerado" } }
])
```

**Saída no Terminal:**
```text
 {
    _id: { terminal: 'T2', classe: 'Refrigerado' },
    kg_total: 0,
    mov: 19938
  }
```

# B2b - Debug Arquitetural

## Defeitos
| # | Defeito | Tipo |
|---|---|---|
| 1 | $sum: "peso_kg" sem $ (string literal, soma 0) | Lógica |
| 2 | $project descarta peso_kg | Lógica |
| 3 | $limit antes do $sort (corta grupos arbitrários antes de ordenar) | Lógica |
| 4 | $match no final (filtra depois do $limit e agrupa a coleção inteira) | Lógica e desempenho |
| 5 | $group por {terminal, classe} (20 grupos em vez de 5) | Desempenho |
| 6 | $project inicial sem utilidade | Desempenho |


# B2c: pipeline corrigido

**Comando:**
```bash
db.movimentacoes.aggregate([
|   { $match: { classe: "Refrigerado" } },
|   { $group: { _id: "$terminal", kg_total: { $sum: "$peso_kg" }, mov: { $sum: 1 } } },
|   { $sort: { kg_total: -1 } },
|   { $limit: 3 }
| ])
[
```

**Saída no Terminal:**
```text
 {
    { _id: 'T1', kg_total: 326235746, mov: 20424 },
  { _id: 'T5', kg_total: 320113777, mov: 20082 },
  { _id: 'T2', kg_total: 320025616, mov: 19938 }
  }
```

