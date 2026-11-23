# Pré-registro de previsões (antes de executar as questões)

Dataset: 400.000 movimentações, ts uniforme em 300 dias a partir de 2026-01-01.
Terminal T1 = 1/5, classe Refrigerado = 1/4, ts >= 2026-04-01 = 210/300 = 70%.
Docs que casam com o filtro da A1: 400.000 x 1/5 x 1/4 x 0,7 = ~14.000.

## A1 - Painel do pátio
- a) Sem índice: COLLSCAN, totalDocsExamined ~400.000, totalKeysExamined 0, SORT em memória (top-k com limit), nReturned 20.
- b) Índice na ordem do filtro {terminal, classe, ts, peso_kg:-1}: IXSCAN + FETCH + SORT. O range em ts quebra a ordem de peso_kg, então as chaves não saem ordenadas. keysExamined ~14.000, docsExamined ~14.000, SORT em memória sim, nReturned 20.
- c) Índice ESR {terminal:1, classe:1, peso_kg:-1, ts:1}: IXSCAN + FETCH, sem SORT. As chaves já saem por peso decrescente e ts é filtrado nos limites do índice. Como ~70% dos docs passam no filtro de ts, espero keysExamined ~30 e docsExamined ~20-30, nReturned 20.

## A2 - Incidente (coordenadas [-48.5000, -25.4880])
- Sem índice: erro de que não há índice geoespacial para a consulta $near ("unable to find index for $geoNear query").
- Com índice 2dsphere em posicao: estágio GEO_NEAR_2DSPHERE (+ FETCH), sem COLLSCAN.
- Área dos dados ~0,05° x 0,05° (~27 km2) e círculo de 300 m (~0,28 km2): ~1% dos pontos, ~4.000 dentro do raio. Com limit 10, nReturned 10 e docsExamined na casa de dezenas.

## A3 - TTL
- Hipótese: registrado_em foi gravado como String ISO (toISOString()) e o índice TTL só expira campos do tipo Date. Por isso nenhum documento é removido. O monitor de TTL roda a cada ~60 s, então o tempo não explica.
- Comprovação planejada: agregação com $type em registrado_em e getIndexes().

## A4 - Consulta coberta
- Índice {tipo:1, terminal:1, container:1}. Estágio PROJECTION_COVERED sobre IXSCAN, totalDocsExamined 0, keysExamined ~16.000 (400.000 x 1/5 x 1/5), nReturned ~16.000.
- Sem _id:0: o _id não está no índice, então aparece FETCH, totalDocsExamined ~16.000 e a projeção deixa de ser coberta.

## B1 - Relatório gerencial
- Índice {classe:1, ts:1}: IXSCAN no $match.
- Docs entrando no $group: 400.000 x 1/4 x 0,7 = ~70.000.
- Saída: 3 documentos (terminais com maior peso total).

## B2 - Debug
- O pipeline original roda sem erro. $project descarta peso_kg e $sum:"peso_kg" (sem $) soma 0, então kg_total = 0 em todos os grupos.
- Agrupa a coleção inteira (400.000 docs) em ~20 grupos (5 terminais x 4 classes). $limit pega 3 grupos arbitrários antes do $sort e o $match final filtra por Refrigerado depois.
- Saída esperada: de 0 a 3 documentos (em média ~1), todos com kg_total 0.

## C2 - Neo4j
- Direção: (sancionada)-[:SOCIA_DE*1..3]->(empresa), seguindo as participações da E2 para as empresas em que ela é sócia, que é a rede sob influência dela. Quem entra no padrão é a rede controlada, então a direção é a da aresta, não o grafo não direcionado.
- Grafo: 30 empresas, 45 sociedades, 90 contêineres, 2 passagens cada, 5 terminais, 30 datas.
- Empresas alcançáveis em até 3 níveis: ~6-12. Coincidências de terminal+data com os 3 contêineres da E2: probabilidade ~1/150 por par de passagens, então espero poucos registros (~1 a 5) após DISTINCT.