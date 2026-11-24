## A1
- Previsão a): COLLSCAN, 400.000 docs, SORT. Real: SORT > COLLSCAN, 400000, 527 ms. Acertei.
- Previsão b): ~14.000 chaves e ~14.000 docs, SORT. Real: 14383 chaves, 20 docs, SORT. Errei os docs: o FETCH ocorre depois do SORT+limit, e o sort usa peso_kg direto da chave.
- Previsão c): ~30 chaves, sem SORT. Real: 32 chaves, 20 docs, sem SORT. Acertei.
- Erros de ambiente: RA=0 no arquivo, entidades HTML, comandos de PowerShell colados no mongosh, helper `m` perdido ao reabrir o mongosh.