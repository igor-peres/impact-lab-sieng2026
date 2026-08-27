# Case 2 — Estacionamento (fluxo e ocupação)

Workshop de IA — SIEng 2026 (28/08) · dataset de apoio · PUC-Rio / DSI

Este pacote é o par do bicicletário dentro do **Case 2 — Vagas & Carona**. O
bicicletário responde "tem vaga pra bike?"; o estacionamento responde a mesma
pergunta para o carro — e junto com o bairro de moradia do aluno (`alunos.csv`,
Case 1) é o que sustenta a ideia de **grupos de carona**.

## O problema

O aluno que chega de carro às 10h não sabe se vai encontrar vaga. A
administração sabe quantos veículos entraram por hora, mas o cruzamento entre
horário de pico, permanência e ocupação simultânea é feito na mão. O desafio é
sair do registro bruto e chegar em **previsão de ocupação** ("a que horas o
rotativo lota?") e em **recomendação de carona** ("quem do seu bairro chega no
mesmo horário?").

## Recorte

Primeira semana de aula de 2026.2: **17 a 21 de agosto de 2026**, 5 dias.
São duas visões do mesmo período, em formatos diferentes:

## Arquivos

| Arquivo | O que é |
|---|---|
| `FLUXO ESTACIONAMENTO PUC - 17 a 21 de Agosto.xlsx` | registro por veículo: 6.858 tickets com entrada, saída, status e valor |
| `17 a 21 de agosto Rotativo *.pdf` (15 arquivos) | relatório de fluxo **por hora** do sistema MBS32 Parking Manager |

### A planilha (`.xlsx`)

Três abas (`17 e 18`, `19 e 20`, `21 de Agosto`) com o mesmo cabeçalho —
junte as três num só quadro antes de analisar. Uma linha por ticket:

| Coluna | Tipo | Nota |
|---|---|---|
| `ID` | int | identificador do registro de ticket |
| `Ticket` | int | número do ticket; o mesmo `Ticket` reaparece (mensalista/recorrente) — 4.419 tickets distintos em 6.858 linhas |
| `Data de Entrada` / `Horário de Entrada` | data / hora | |
| `Data de Saída` / `Horário de Saída` | data / hora | vazio quando o veículo ainda estava dentro no fechamento da extração |
| `Status` | texto | `Fora` (5.617, já saiu), `Dentro` (1.207, sem saída registrada), `Pago` (34) |
| `Valor` | decimal | tarifa em R$; 0 a 60, média ~R$ 10; a maioria é 0 (conveniado/isento) |

### Os PDFs (relatório de fluxo horário)

Um conjunto por dia. `... Entrada` traz as **entradas** hora a hora; `... (Saída
Ac06)` e `... (Saída Ac07)` são as duas cancelas de **saída** do rotativo. Cada
tabela quebra o movimento por faixa de hora (`00:00 a 00:59` … `23:00 a 23:59`)
em colunas: Entradas/Saídas Rotativo, Saídas em Franquia, Entradas/Saídas
Conveniados (e Conveniados Externo), Entradas/Saídas Manual, Totais e — a coluna
que interessa para ocupação — **`Veículos no Estacionamento`**, o saldo
acumulado no fim de cada hora.

> Vocabulário do sistema: **Rotativo** = quem paga por hora (visitante);
> **Conveniado** = vínculo/permanente; **Franquia/Manual** = liberação especial
> ou manual na cancela.

## O que os dados já mostram

- O movimento de entrada começa forte às **6h–7h** e o saldo de veículos sobe ao
  longo da manhã (ex.: 17/08 passa de ~80 veículos às 6h para ~500 no fim da
  tarde). A curva de ocupação está pronta nos PDFs, na coluna
  `Veículos no Estacionamento`.
- A planilha e os PDFs cobrem **o mesmo período** por caminhos diferentes: a
  planilha dá permanência por veículo (dá para calcular duração), o PDF dá o
  agregado horário já fechado. Boa chance de validar um contra o outro.

## Cuidados com os dados (leia antes de concluir qualquer coisa)

1. **A planilha inclui TODAS as cancelas da PUC-Rio.** Não há campo dizendo se o
   registro é do rotativo ou do estacionamento interno, nem se é carro ou moto.
   Não dá para separar isso a partir da planilha sozinha — assuma que é o fluxo
   total do campus e diga isso na conclusão.
2. **Não existe placa.** A coluna que às vezes aparece como `Placa` traz só o
   texto `Visualizar` (link do sistema), não a placa real. Identificação de
   veículo é o `Ticket`, que é pseudônimo de recorrência, não a placa.
3. **1.207 registros estão `Dentro`** (sem saída). Para medir permanência ou
   ocupação a partir da planilha, decida o tratamento dessas linhas (descartar,
   truncar no fechamento) e **documente a escolha** — mesmo problema de saída não
   registrada do bicicletário.
4. **Planilha × PDF podem não bater exatamente.** A planilha é por ticket e inclui
   todas as cancelas; o PDF é o relatório oficial do rotativo por hora. Use o PDF
   como referência de ocupação e a planilha para permanência/recorrência.
5. Só há 5 dias. Dá para estudar o padrão de um dia típico de aula, não
   sazonalidade.

## Perguntas para atacar

- Reconstrua a curva de ocupação por hora a partir dos PDFs e compare com a
  reconstruída da planilha (entradas − saídas). Elas concordam? Onde divergem, por quê?
- A que horas o estacionamento atinge o pico? Existe um horário de chegada em que
  a chance de encontrar vaga cai muito?
- Cruzando com o bairro de `alunos.csv` (Case 1): que rotas de carona juntariam
  gente que chega no mesmo horário, vinda da mesma região? Quantos carros a menos
  isso tira do pico?
- Junte com o bicicletário: o pico do carro e o pico da bike são no mesmo
  horário? Uma política de incentivo à bike aliviaria o estacionamento?
- Como você trataria os 1.207 veículos `Dentro` para não enviesar a ocupação?

## Origem e anonimização

Extraído do sistema de controle de acesso do estacionamento (MBS32 Parking
Manager) referente a 17–21/08/2026. Não há placa, nome ou vínculo do
condutor — o `Ticket` serve para medir recorrência e nada mais.
