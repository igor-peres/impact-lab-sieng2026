# Case 2 — Bicicletário do campus (vagas, pico e carona)

Workshop de IA — SIEng 2026 (28/08) · dataset de apoio · PUC-Rio / DSI

## O problema

O bicicletário da PUC-Rio registra entrada e saída de cada bicicleta. O aluno
que chega às 10h não sabe se vai encontrar vaga. A administração não sabe
quanto da lotação é gente que fica 3h e quanto é gente que estaciona às 7h e
sai às 19h. E a mesma pergunta vale para o estacionamento de carro e para
grupos de carona: **quem chega junto, de onde, e a que hora**.

O desafio é sair do registro bruto e chegar em previsão de ocupação e em
recomendação — inclusive "não vem de bike hoje às 10h, vem 8h" ou "essas 6
pessoas do seu bairro chegam no mesmo horário".

## Recorte

3 últimos meses de aula do período 2026.1: **04/05/2026 a 31/07/2026**,
65 dias com movimento, **23.429 sessões** de **1.358 ciclistas distintos**.

## Arquivos

| Arquivo | Linhas | O que é |
|---|---|---|
| `sessoes.csv` | 23.429 | uma linha por uso: entrada, saída, duração |
| `uso_por_dia_hora.csv` | 89 | agregado dia da semana × hora de entrada |
| `ocupacao_estimada.csv` | 1.055 | bicicletas simultâneas por data × hora |

### sessoes.csv

| Coluna | Tipo | Nota |
|---|---|---|
| `sessao_id` | texto | sequencial |
| `ciclista_id` | texto | pseudônimo estável — dá para medir recorrência |
| `data` | data | |
| `dia_semana` | texto | Segunda … Sábado |
| `hora_entrada` | HH:MM | |
| `faixa_hora_entrada` | int 0-23 | hora cheia, para agrupar |
| `hora_saida` / `faixa_hora_saida` | HH:MM / int | |
| `duracao_min` | decimal | mediana 197,5 min |
| `suspeita_saida_nao_registrada` | S/N | `S` quando a duração passa de 14h |

### ocupacao_estimada.csv

`data`, `dia_semana`, `hora`, `bicicletas_no_bicicletario`. Calculado por
soma corrida de entradas menos saídas dentro do dia — é **estimativa**, herda
o erro das saídas não registradas (ver abaixo).

## O que os dados já mostram

- Pico de entrada às **9h** (4.354 entradas), segundo pico às **7h** (3.517),
  terceiro no começo da tarde (13h, 2.514).
- Ocupação média sobe até um platô de ~160 bicicletas entre **10h e 12h** e cai
  a partir das 16h. Máximo observado no período: **396**.
- Terça é o dia mais cheio (5.334), sexta cai um terço (3.343), sábado é
  praticamente nulo (5 sessões).
- Uso é recorrente, não eventual: mediana de 15,5 sessões por ciclista no
  trimestre e **523 ciclistas com 20+ sessões**. Isso é o que viabiliza a ideia
  de grupo de carona / grupo de pedal.

## Cuidados com os dados

1. **1.720 sessões (7,3%) têm duração acima de 14h** e estão marcadas em
   `suspeita_saida_nao_registrada`. Quase sempre é saída que ninguém registrou,
   não bicicleta que dormiu no campus. Decida o tratamento (descartar, imputar
   pela mediana do ciclista, truncar no fechamento) e **documente a escolha** —
   ela muda o resultado da ocupação.
2. Este arquivo só tem **sessões completas** (com entrada e saída registradas).
   Quem entrou e nunca teve saída lançada não virou linha. Ou seja: a ocupação
   real é **maior ou igual** à estimada aqui, nunca menor.
3. **A capacidade instalada do bicicletário não está no dado.** Trate como
   parâmetro do modelo. O máximo observado (396) é piso, não capacidade.
4. Julho tem menos aula (fim de período): a queda de volume é calendário, não
   comportamento.
5. Não há identificação do usuário, do vínculo (aluno/professor/funcionário)
   nem da bicicleta. Só o pseudônimo, que serve para recorrência e nada mais.

## Perguntas para atacar

- Prever a ocupação da próxima hora / do próximo dia. Qual o erro aceitável
  para o aluno confiar na informação antes de sair de casa?
- Existem perfis de uso claros (aula da manhã, dia inteiro, uso curto de
  tarde)? Clusterize por (hora de entrada, duração, dias por semana).
- Combinando com `alunos.csv` do Case 1 (bairro de moradia), que rotas de
  carona ou de pedal em grupo se formariam? Quantas pessoas por rota?
- Qual capacidade seria necessária para nunca lotar? E qual política de
  incentivo (chegar mais cedo, reserva de vaga) resolveria mais barato?
- Como você mediria se a saída não registrada está enviesando sua previsão?

## Origem e anonimização

Extraído da base de produção do COBRA (sistema que registra o ciclo de entrada
e saída do bicicletário e-Bike) em 17/08/2026. O identificador do ciclista
passou por HMAC-SHA256 com sal aleatório descartado no fim da extração. Nome e
CPF foram deixados de fora da consulta.
