# TV de Indicadores · Suprimentos Agrícola

Painel em tela cheia para ficar rodando num monitor do setor de **Suprimentos Agrícola**. As telas passam sozinhas, com números grandes para leitura de longe, semáforo de metas, relógio e uma faixa de alertas no rodapé.

🔗 **Demonstração:** https://jmarcelogomesparreira-ship-it.github.io/tv-suprimentos-agricola/

> ⚠️ **Protótipo com dados fictícios.** Os números, fornecedores e compradores são exemplos criados para validar o layout. Nenhum dado real de empresa está neste repositório.

---

## As 10 telas

| # | Tela | O que mostra |
|---|------|--------------|
| 1 | **Visão geral** | 8 indicadores-chave com meta, semáforo e linha de tendência (RCs abertas, RCs antigas, entregas atrasadas, OTIF, lead time, saving, gasto em contrato, compras emergenciais) |
| 2 | **Mercado e Economia** | Dólar, Selic, IPCA, IGP-M, petróleo Brent, diesel, ureia, cloreto de potássio, açúcar e etanol, com a oscilação no período e o impacto de cada um nas compras |
| 3 | **Requisições** | Envelhecimento (aging) das RCs abertas e RCs por comprador |
| 4 | **Pedidos e entregas** | Pedidos em aberto, entregas previstas para os próximos 7 dias e maiores atrasos |
| 5 | **Fornecedores** | OTIF mensal contra a meta, ranking de OTIF e concentração do gasto |
| 6 | **Relação** | Os 6 maiores fornecedores: gasto, prazo real x prometido, % no prazo, % de divergências e nota IQF |
| 7 | **Curva ABC** | Pareto do gasto da safra, dependência de fornecedor, prazo médio e problemas nas entregas |
| 8 | **Contratos** | Vencimentos em 30/60/90 dias, saldo consumido e gasto em contrato x spot |
| 9 | **Estoque crítico** | Cobertura em dias dos insumos-chave e itens abaixo do ponto de pedido |
| 10 | **Orçamento** | Orçado x realizado por centro de custo e ritmo de consumo da safra |

**Nota IQF (0–100):** 50% pontualidade + 30% qualidade (entregas sem divergência) + 20% cumprimento do prazo prometido.

## Dados ao vivo

Quando o computador tem internet, a tela de Mercado busca sozinha, a cada 10 minutos:

- **Dólar:** [AwesomeAPI](https://docs.awesomeapi.com.br/)
- **Selic, IPCA 12 meses e IGP-M 12 meses:** [API SGS do Banco Central](https://dadosabertos.bcb.gov.br/)

Os demais indicadores (Brent, diesel, fertilizantes, açúcar e etanol) usam valores de referência editáveis. Se a internet cair, a tela continua com os valores de referência.

## Controles

| Tecla | Ação |
|-------|------|
| `←` `→` | Tela anterior / próxima |
| `Espaço` | Pausa ou retoma a rotação |
| `F` | Tela cheia |
| Clique no menu lateral | Vai direto para a tela |

**Parâmetros na URL:**

- `?t=20`: cada tela fica 20 segundos (padrão: 15)
- `?tela=3`: abre direto na tela 3

## Como usar

1. Baixe o `index.html` e abra no Chrome ou Edge.
2. Aperte `F` para tela cheia.

Não precisa de servidor nem instalação.

## Como trocar os dados

Todos os números ficam em um único bloco no início do script, `const D = { ... }`. Cada parte corresponde a uma tela. A fonte prevista no SAP MM é:

| Bloco | Transação / tabela |
|-------|--------------------|
| Requisições | ME5A / EBAN |
| Pedidos e entregas | ME2M / EKKO-EKPO / EKET |
| Prazos e recebimentos | MB51 (mov. 101) |
| Fornecedores | EKET x MB51, LFA1 |
| Contratos | ME3M |
| Estoque | MB52 / MMBE / MD04 |
| Orçamento | ZFM110 |

## Tecnologia

- HTML, CSS e JavaScript em um único arquivo
- [Chart.js 4](https://www.chartjs.org/) para os gráficos
- Fonte Barlow Condensed, como alternativa à DIN
- Layout fixo em 1920×1080, que se ajusta automaticamente ao tamanho da tela
- Visual seguindo o padrão de dashboards da empresa: laranjas e verdes, sem azul e sem cinza, cabeçalho com ícone sólido e "Dados atualizados em"

## Próximos passos

- [ ] Validar os indicadores e as metas com a coordenação de compras
- [ ] Importar os exports do SAP direto na TV
- [ ] Tela de necessidades da safra (próximos 30–60 dias via MRP)

---

Desenvolvido por **Marcelo José Gomes Parreira**: ideia, indicadores e lógica de negócio, com IA como ferramenta de programação.
[LinkedIn](https://www.linkedin.com/in/marcelo-josé-gomes-parreira-101b352ab) · [GitHub](https://github.com/jmarcelogomesparreira)
