# Case 4 — Sistema integrado de restaurantes

Workshop de IA — SIEng 2026 (28/08) · PUC-Rio

## O problema

O campus tem vários restaurantes, lanchonetes e **food trucks**, cada um com seu
cardápio, preço e jeito de pedir — e nada disso vive num lugar só. O aluno não
consegue, num toque, ver **o que tem, quanto custa, onde fica e como pedir**. O
desafio é construir esse sistema integrado.

## Este case não vem com dados — vocês constroem a base

Diferente dos outros três, o Case 4 **não tem dataset entregue**, e isso é parte
do desafio: **os próprios alunos criam o dado**.

A ideia central: **percorrer todos os restaurantes e food trucks da PUC-Rio,
fotografar os cardápios** e usar o Claude para transformar as fotos em uma base
**estruturada e real** dos cardápios da PUC — item, preço, categoria, restrição
alimentar, ponto de venda, horário. Uma amostra bem-feita de alguns pontos já é
suficiente para a solução ficar de pé; comece por ela.

> Fotografe cardápios (não pessoas), respeite os estabelecimentos e registre a
> **data da coleta** — preço e cardápio mudam. Se faltar tempo, complemente com
> dados **claramente marcados como fictícios**, deixando explícito o que é real.

## Onde dá para chegar

O problema é aberto de propósito. Alguns caminhos que a solução pode tomar:

- **Busca e comparação**: encontrar opções por preço, tipo de comida e restrição
  alimentar entre todos os pontos do campus.
- **Pedidos e delivery**: um fluxo de pedido — e, se o time quiser, entrega no
  campus.
- **Área do restaurante (admin)**: tela para o estabelecimento cadastrar e
  atualizar cardápio, preços e disponibilidade.
- **Área do cliente**: acompanhar o pedido e o histórico.

Não precisa fazer tudo — escolha o recorte que gera mais valor no tempo que vocês
têm e faça bem.

## Perguntas para atacar

- Como transformar uma foto de cardápio em dados estruturados e confiáveis com o
  Claude? Onde ele erra, e como vocês conferem?
- Dado um orçamento, uma restrição e um tempo ("almoço até R$ 25, vegetariano,
  40 min"), o que pedir e onde?
- Como comparar cardápios que descrevem os pratos de formas diferentes? Dá para
  derivar uma taxonomia de pratos?
- Divisão de pedido em grupo: várias pessoas, restrições diferentes, um só
  delivery — qual combinação minimiza preço e espera?
- Qual é a **menor** base de dados que já torna a solução útil de verdade?

## Entregável

No README de entrega do time, deixe explícito **como a base foi construída**:
quantos pontos foram cobertos, como as fotos viraram dados, o que é real e o que
é fictício. Isso conta na avaliação tanto quanto o produto.
