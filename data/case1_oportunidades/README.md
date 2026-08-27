# Case 1 — Sistema de oportunidades integradas

Workshop de IA — SIEng 2026 (28/08) · dataset de apoio · PUC-Rio / DSI

## O problema

Hoje um aluno da PUC-Rio procura oportunidade em lugares separados: estágio no
Vagas Online da CCESP, monitoria no departamento, iniciação científica com o
professor, mestrado na coordenação de pós. Não existe um lugar único que cruze
**o que o aluno é** (curso, período, interesses, onde mora) com **o que está
aberto** (vaga, requisito de período, jornada, bolsa, local).

O desafio é construir esse cruzamento: busca, recomendação, ranqueamento,
detecção de aluno elegível que não se candidatou, previsão de qual vaga vai
ficar sem candidato.

## Arquivos

| Arquivo | Linhas | O que é |
|---|---|---|
| `vagas.csv` | 3.550 | anúncios publicados de 01/08/2025 a 17/08/2026 |
| `vaga_cursos.csv` | 7.994 | quais cursos cada vaga aceita (N:N) |
| `alunos.csv` | 2.187 | alunos com cadastro no sistema desde 2024 |
| `aluno_interesses.csv` | 1.444 | áreas de interesse declaradas pelo aluno |
| `monitorias.csv` | 283 | monitorias concedidas, 2024.1 a 2025.2 |

### vagas.csv

| Coluna | Tipo | Nota |
|---|---|---|
| `vaga_id` | texto | pseudônimo estável dentro deste pacote |
| `data_publicacao` | data | |
| `tipo` | texto | `Estágio` (3.526), `Emprego` (23), `Trainee` (1) |
| `jornada` | texto | Integral, Manhã, Tarde, A Combinar… |
| `bolsa_mensal_brl` | decimal | mediana R$ 1.200; p10 R$ 800; p90 R$ 1.650; 115 vagas com 0 ou vazio |
| `periodo_min` / `periodo_max` | int | faixa de período do curso que a vaga aceita |
| `num_vagas` | int | |
| `cidade` / `bairro` | texto | local do estágio |
| `empresa_id` | texto | pseudônimo da contratante |
| `qtd_cursos_elegiveis` | int | atalho para o `vaga_cursos.csv` |
| `data_termino` | data | quando o anúncio expira |
| `atividades` / `requisitos` / `beneficios` | texto | texto livre do anúncio, já higienizado |

### alunos.csv

`aluno_id`, `curso`, `periodo_atual`, `habilitacao`, `bairro`, `cidade`, `uf`,
`faixa_idade` (`<=19`, `20-22`, `23-25`, `26-30`, `30+`; 731 vazios),
`matriculado` (S/N), `mes_cadastro`.

Cursos mais frequentes: Engenharia (296), Direito (295), Psicologia (206).
Bairros: Barra da Tijuca (299), Copacabana (149), Leblon (138). 87% mora no
município do Rio — o dado de bairro conversa direto com o Case 2 (bicicletário)
e com a ideia de grupos de carona.

### monitorias.csv

`periodo`, `aluno_id`, `cod_disciplina`, `disciplina`, `creditos`.

## Cuidados com os dados (leia antes de concluir qualquer coisa)

1. **`aluno_id` de `monitorias.csv` NÃO cruza com `alunos.csv`.** São sistemas
   diferentes (SGU acadêmico vs. Vagas Online) e a pseudonimização foi feita
   separada em cada um. Não existe chave de ligação entre os dois — de
   propósito.
2. **`monitorias.csv` cobre um centro só** (CCCI), não a PUC toda. Serve para
   modelar o formato "oportunidade de monitoria", não para medir volume.
3. **Iniciação científica e mestrado não estão neste pacote.** Esses dados
   moram na VRAC/SAU, fora do alcance desta extração. O modelo de dados aqui
   já foi pensado para receber esses tipos: `tipo` em `vagas.csv` é aberto,
   e o par (`periodo_min`, `periodo_max`) + `vaga_cursos.csv` descrevem
   elegibilidade de qualquer modalidade.
4. `requisitos` está vazio na maioria dos anúncios — a CCESP cadastra quase
   tudo em `atividades`. Não é bug de extração.
5. Higienização de texto livre substitui trechos por `[EMPRESA]`, `[EMAIL]`,
   `[TEL]`, `[LINK]`, `[DOC]`. Isso derruba um punhado de palavras comuns por
   tabela (uma razão social contém palavra de dicionário). Trate `[EMPRESA]`
   como ruído, não como sinal.
6. Só a faixa da idade veio, não a data de nascimento. Não tem nome, CPF,
   matrícula, e-mail, telefone nem endereço em nenhum arquivo.

## Perguntas para atacar

- Dado um aluno (curso, período, bairro, interesses), quais 5 vagas abertas
  fazem mais sentido? E o inverso: dada uma vaga, quais alunos avisar?
- Qual vaga fica sem candidato elegível? Cruze `vaga_cursos.csv` +
  `periodo_min/max` com a distribuição real de `alunos.csv`.
- `atividades` é texto livre e repetitivo. Consegue derivar uma taxonomia de
  área a partir dele e comparar com a área que o aluno declarou em
  `aluno_interesses.csv`?
- A bolsa mediana é R$ 1.200. O que explica a variação — bairro, jornada,
  curso exigido, tamanho da faixa de período?
- Vaga aceitando 10 períodos (`periodo_min=1`, `periodo_max=10`) é vaga
  genérica ou cadastro preguiçoso? Isso ajuda ou atrapalha a recomendação?

## Origem e anonimização

Extraído da base de produção do Vagas Online (CCESP) e do SGU acadêmico em
17/08/2026. Identificadores passaram por HMAC-SHA256 com sal aleatório
descartado no fim da extração: o pseudônimo é consistente dentro do pacote e
não volta ao original. Nome de pessoa, documento, contato e endereço exato
foram removidos na consulta, não depois.
