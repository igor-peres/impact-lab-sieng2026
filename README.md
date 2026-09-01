# Impact Lab · SIEng 2026 — Consultoria com IA na prática

**Semana Integrada de Engenharia · PUC-Rio · 28 de agosto de 2026 · Casa da Inovação**
Tema da SIEng 2026 — **I³: Inovação, Inteligência Artificial e Impacto nas Engenharias**

Um dia de mão na massa: times multidisciplinares de alunos da PUC-Rio resolvem,
com o **Claude**, um problema real do campus — com **dados reais** já
anonimizados, **tutoria** de professores da PUC-Rio e de profissionais da
**Taicor**, **MGV Tech** e **Visagio**, e apresentação dos resultados no fim do dia.

Este repositório é o ponto de partida de todos os times: aqui estão os **cases**,
os **dados**, as **regras** e o lugar onde cada time **entrega** a sua solução.

---

## Como funciona

1. **Escolha um case** (abaixo). Leia o README do case inteiro antes de codar — os
   dados têm pegadinhas propositais, e metade do desafio é interpretá-los certo.
2. **Construa com o Claude.** Vale explorar dado, prototipar, escrever código,
   montar a apresentação — o que fizer o problema andar.
3. **Entregue no repositório** até o horário-limite (ver [regras](REGRAS_E_AVALIACAO.md)).
4. **Apresente** para a banca. A avaliação olha impacto real, produto, engenharia,
   ideia e apresentação.

Novo em Git/GitHub ou no Claude? Comece por **[COMO_COMECAR.md](COMO_COMECAR.md)**.

## Os 4 cases

| # | Case | Pergunta central | Dados |
|---|------|------------------|-------|
| 1 | **[Oportunidades integradas](data/case1_oportunidades/README.md)** | Cruzar o que o aluno é (curso, período, bairro, interesses) com o que está aberto (estágio, monitoria, IC) | 3.550 vagas · 2.187 alunos · 283 monitorias |
| 2 | **[Vagas & Carona](data/case2_vagas_carona/README.md)** | Prever ocupação de bike/carro e formar grupos de carona | 23.429 sessões de bike · 6.858 tickets de carro |
| 3 | **[Grade horária automatizada](data/case3_grade_horaria/README.md)** | Montar grade sem choque respeitando restrições do aluno | 74.381 blocos de aula · 4.947 turmas |
| 4 | **[Restaurantes integrados](data/case4_restaurantes/README.md)** | Cardápios, preços e pedidos num só lugar | *sem dado dado — parte do desafio é construí-lo* |

> Os cases conversam entre si: bairro (Case 1) alimenta carona (Case 2); horário
> da grade (Case 3) define a que horas o aluno chega (Case 2). Cruzar cases é
> bem-vindo.

## GitHubs final dos grupos que participaram da SIEng:

Facul Food: https://github.com/Aguimim/faculfood
Grade Sob Medida: https://github.com/JudyFaria/grade-sob-medida_/
Iteri: https://supabase.com/dashboard/project/oarkrgnjaheqjosgbdpj
SOL: https://github.com/PIST0LINHA/sieng_workshop

Vaga Certa: https://github.com/Bulquerque/vaga-certa-puc-rio

## Onde estão os dados

Tudo em **[`data/`](data/)**, uma pasta por case, cada uma com o seu `README.md`
explicando o problema, o dicionário de colunas, o que o dado já mostra, os
**cuidados de interpretação** e perguntas de partida. Leia o
**[uso dos dados e anonimização](USO-DOS-DADOS.md)** antes de publicar qualquer
resultado.

## Cronograma — sexta, 28/08 (Casa da Inovação)

| Horário | Atividade |
|---|---|
| 09h00 – 10h45 | Palestra *Consultoria com IA — cases reais* (Taicor · MGV Tech · Visagio) |
| 10h45 – 11h00 | Coffee break |
| 11h00 – 13h00 | **Workshop hands-on — mão na massa** (construção com tutoria) |
| 13h00 – 14h00 | Almoço |
| 14h00 – 15h00 | **Finalização** — entrega no GitHub até 14h30 (deadline) |
| 15h00 – 16h00 | **Apresentação dos cases pelos alunos** |
| 16h00 | Sorteio de brindes + confraternização · Planetário |

## Entrega e avaliação

Regras, horário-limite e critérios (com pesos) em
**[REGRAS_E_AVALIACAO.md](REGRAS_E_AVALIACAO.md)**. Cada time entrega numa pasta
própria em **[`times/`](times/)** — copie o modelo em `times/_MODELO_TIME/`.

## Organização e parceiros

**Professores organizadores (PUC-Rio):** Igor Peres, Isabel Almeida, João Ricardo,
Luiza Martins, Marcello Congro e Wilson Reis.
**Parceiros de consultoria (tutoria e banca):** Taicor · MGV Tech · Visagio.
**Dados:** Diretoria de Sistemas de Informação (DSI) — PUC-Rio.

## Estrutura do repositório

```
impact-lab-sieng2026/
├── README.md                  você está aqui
├── COMO_COMECAR.md            setup de Git, GitHub e Claude — comece aqui
├── REGRAS_E_AVALIACAO.md      regras, horário-limite, critérios e pesos
├── USO-DOS-DADOS.md           anonimização e uso responsável dos dados
├── data/                      os 4 cases e seus datasets
│   ├── case1_oportunidades/
│   ├── case2_vagas_carona/    (bicicletario/ + estacionamento/)
│   ├── case3_grade_horaria/
│   └── case4_restaurantes/
├── times/                     uma pasta por time (copie _MODELO_TIME/)
│   └── _MODELO_TIME/
└── entrega/
    └── CHECKLIST_APRESENTACAO.md
```
