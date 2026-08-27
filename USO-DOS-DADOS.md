# Uso dos dados e anonimização

Os datasets foram extraídos das bases de produção da PUC-Rio pela **Diretoria de
Sistemas de Informação (DSI)** e preparados especificamente para este workshop.
Use-os **apenas** para o Impact Lab da SIEng 2026.

## O que já foi feito na origem

- **Nenhum dado direto de identificação saiu da base**: nome, CPF, matrícula,
  e-mail, telefone e endereço exato ficaram **fora da própria consulta** — não
  foram removidos depois.
- Aluno, ciclista, empresa, professor e sala viraram **pseudônimo** por
  HMAC-SHA256 com sal aleatório descartado no fim da extração: o pseudônimo é
  consistente **dentro de cada pacote** e não volta ao valor original.
- Idade virou **faixa**. Texto livre dos anúncios passou por higienização que
  troca contato, link, documento e razão social por marcador (`[EMAIL]`, etc.).

## O que você deve fazer

- **Não tente reidentificar** ninguém, cruzar com bases externas para "descobrir"
  quem é, ou publicar recortes que isolem um indivíduo.
- Trate os pseudônimos como o que são: servem para medir **recorrência e relação**,
  não para saber quem é a pessoa.
- Ao apresentar, mostre **padrões agregados**, não linhas individuais.
- Dois avisos que mudam resultado, repetidos aqui porque é fácil esquecer:
  - o `aluno_id` de `monitorias.csv` **não cruza** com `alunos.csv` (sistemas
    diferentes, pseudonimização separada, de propósito);
  - no Case 2, saídas não registradas (bike) e veículos ainda `Dentro` (carro)
    **enviesam a ocupação** — escolha e documente o tratamento.

## Depois do evento

Estes dados não devem ser redistribuídos fora do contexto do workshop. Em caso de
dúvida sobre uso, fale com a organização (professores da PUC-Rio) ou com a DSI.
