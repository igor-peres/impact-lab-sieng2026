# Case 2 — Vagas & Carona

Workshop de IA — SIEng 2026 (28/08) · PUC-Rio / DSI

Um só problema visto por três ângulos: **onde estacionar (bike e carro) e como
dividir o trajeto**. O aluno que chega no campus enfrenta a mesma incerteza —
"vai ter vaga quando eu chegar?" — e a mesma oportunidade — "quem mora perto de
mim chega no mesmo horário e poderia vir junto?".

Este case tem dois pacotes de dados, cada um com o seu README:

- [`bicicletario/`](bicicletario/README.md) — 23.429 sessões de entrada/saída de
  bicicletas em 2026.1, com pico, platô e ocupação estimada.
- [`estacionamento/`](estacionamento/README.md) — 6.858 tickets de carro +
  relatórios de fluxo horário da 1ª semana de aula de 2026.2.

O elo com os outros cases: o **bairro de moradia** dos alunos está em
`alunos.csv` (Case 1) e as **restrições de horário** que definem a que horas o
aluno chega saem do Case 3 (grade). Uma boa solução de carona conversa com os
três.

Sites já criados por outros grupos de alunos:

https://venture-projects.github.io/temvaga/#

https://www.lotapuc.tech/estacionamento

## Ideias de recorte

- **Previsão de ocupação**: a que horas a bike / o carro lota? Qual o erro
  aceitável para o aluno confiar antes de sair de casa?
- **Recomendação de carona**: agrupar quem sai da mesma região no mesmo horário.
- **Política**: incentivar bike alivia o estacionamento? Qual capacidade evitaria
  lotar?
