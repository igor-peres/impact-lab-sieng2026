# Como começar

Guia rápido para quem vai construir no Impact Lab. Não precisa ser especialista em
Git — o essencial cabe em 15 minutos.

## 1. O que você precisa

- Uma **conta no GitHub** (grátis, em github.com).
- **Git** instalado, ou o **GitHub Desktop** (interface visual, mais fácil).
- **Python 3** (recomendado para abrir os CSVs) ou a ferramenta que preferir.
- Acesso ao **Claude** — o assistente que você vai usar o dia todo.

## 2. Pegar o repositório

**Opção A — GitHub Desktop (mais simples):** *File → Clone repository →* cole a URL
deste repo → *Clone*.

**Opção B — linha de comando:**

```bash
git clone <URL-DO-REPOSITORIO>
cd impact-lab-sieng2026
```

Se preferir trabalhar isolado, cada time pode dar **fork** no repo e trabalhar no
próprio; combine com a organização qual caminho o evento vai usar.

## 3. Criar a pasta do seu time

Copie o modelo e renomeie com o nome do time:

```bash
cp -r times/_MODELO_TIME times/time-03-nome-do-time
```

Todo o trabalho do time vive aí dentro: código, notebooks, a apresentação e o
`README.md` de entrega (o modelo já vem com a estrutura).

## 4. Abrir os dados

Os arquivos são CSV e XLSX em `data/`. Um jeito rápido em Python:

```python
import pandas as pd
vagas = pd.read_csv("data/case1_oportunidades/vagas.csv")
print(vagas.shape)
print(vagas.head())
```

**Antes de analisar, leia o `README.md` do case.** Ele traz o dicionário de
colunas e os cuidados de interpretação — há pegadinhas propositais.

## 5. Construir com o Claude

O Claude é seu par o dia inteiro. Bons usos:

- **Entender o dado**: cole o README do case e peça um plano de ataque.
- **Explorar**: peça o código para carregar, limpar e visualizar.
- **Prototipar**: da recomendação ao app — descreva o objetivo e itere.
- **Comunicar**: rascunhar a apresentação e revisar a narrativa.

Dica: descreva o **problema e o resultado que você quer**, não só "escreve um
código". E confira o que o Claude produz contra o README — você é responsável
pelas conclusões.

## 6. Salvar e entregar

Salve com frequência (commits pequenos):

```bash
git add times/time-03-nome-do-time
git commit -m "Analise inicial do case 1"
git push
```

No GitHub Desktop: escreva a mensagem embaixo à esquerda → *Commit* → *Push origin*.

A entrega vale quando está **no repositório antes do horário-limite** — ver
[REGRAS_E_AVALIACAO.md](REGRAS_E_AVALIACAO.md).

## Travou?

Chame um **mentor** (eles circulam por todas as mesas) ou abra uma
[issue de dúvida](.github/ISSUE_TEMPLATE/duvida.md). Perguntar cedo é mais barato
que perder duas horas.
