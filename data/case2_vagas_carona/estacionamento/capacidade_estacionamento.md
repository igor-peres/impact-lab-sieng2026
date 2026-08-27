# Capacidade do estacionamento — PUC-Rio

Transcrito dos quadros de aviso da PUC-Rio (2025). Serve como **parâmetro de
capacidade** para o Case 2 — a planilha de fluxo não traz esse número.

> **Importante:** o **Rotativo é o estacionamento usado pelos alunos.** É a
> capacidade relevante para modelar a ocupação do dia a dia do aluno. A "Área
> Interna" é de vagas permanentes (funcionários/permanentes), organizada por
> zonas. A planilha `FLUXO ESTACIONAMENTO ...xlsx` inclui **todas as cancelas**
> da PUC, sem separar rotativo de interno.

## Rotativo — exclusivo para alunos

Funcionamento: **Seg–Sex 06h–23h · Sáb 07h–18h**.

| Local | Vagas de carro |
|---|---|
| Edifício Garagem | 280 |
| Laje (40 + 40 frente da academia) | 80 |
| **Total de carros** | **360** |

- **Motocicletas:** 30 vagas.
- Com a retomada das obras do **Metrô Gávea**, foram desativadas **35 vagas de
  carro** (frente e lateral do Ginásio) e **30 de moto** (lateral do Gênesis).
- Cadastros no Shopping da Gávea (2025): **454 usuários**, sendo **50 mensalistas**.

## Área Interna — vagas permanentes, por zona

- Usuários cadastrados: **664** · Lista de espera de veículos: **232**.
- **Vagas de carro: 288** (detalhe em `capacidade_interno_zonas.csv`):

| Zona | Vagas |
|---|---|
| Azul | 25 |
| Amarela | 60 |
| Preta | 25 |
| Verde | 90 (80 + 10 DAU) |
| Vermelha | 80 |
| Reitoria | 8 |

- Motocicletas: 69 usuários cadastrados · 19 na lista de espera.
- **Vagas desativadas no campus (2023–2025): 172** — ex.: Área Amarela (Casa de
  Inovação 18, Boulevard 27, Boulevard Gastronômico 10), Área Azul (Faixa de
  Pedestre IAG 7), Horista (Praça 13; Contâiners/Instituto Behring de IA 86),
  Área Preta (Jardinagem 6), Área Verde (Escada do NIT 2), Área Vermelha
  (Bicicletário 3).
- **Vagas canceladas em 2025: 91** — 17 pelo próprio + 74 por encerramento de
  contrato de trabalho.

## Como usar no Case 2

- Para "a que horas o rotativo lota?", use **360 vagas de carro** (rotativo) como
  capacidade e compare com a ocupação reconstruída dos dados.
- Lembre que a planilha soma todas as cancelas; se for isolar o rotativo, deixe
  a suposição explícita.
