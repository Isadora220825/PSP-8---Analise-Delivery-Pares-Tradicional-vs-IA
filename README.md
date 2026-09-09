# PSP-8--elivery de Comida: Análise Tradicional vs. Inteligência Artificial

Projeto de análise de dados que compara, **aos pares**, uma abordagem tradicional (estatística manual) com uma abordagem de Inteligência Artificial, nas três frentes clássicas de análise de dados: **descritiva, preditiva e prescritiva**.

## Pergunta do projeto

> A Inteligência Artificial melhora, de fato, a análise de um conjunto de dados de pedidos de delivery — ou uma análise tradicional já é suficiente?

Em vez de simplesmente "rodar um modelo e mostrar a acurácia", este projeto **testa essa pergunta com método científico**: cada tipo de análise é feito duas vezes (tradicional e inteligente), os resultados são comparados com métricas concretas, e a conclusão é reportada **mesmo quando ela é "a IA não ajudou aqui"** — que também é um resultado válido e importante.

## Base de dados

- **Fonte:** [Kaggle — Daily Food Delivery Orders](https://www.kaggle.com/)
- **Arquivo:** `daily_food_delivery_orders.csv`
- **Tamanho:** 2.600 pedidos, ano de 2024
- **Colunas:** id do pedido, data, idade do cliente, tipo de restaurante, valor do pedido, distância de entrega, tempo de entrega, forma de pagamento, avaliação do entregador e status do pedido (Delivered / Cancelled / Delayed)

## Metodologia — os 3 pares

| # | Tipo de análise | Par Tradicional | Par Inteligente |
|---|---|---|---|
| 1 | **Descritiva** | Estatística manual (médias, contagens, tabelas cruzadas) | Clusterização não supervisionada (K-Means + PCA) |
| 2 | **Preditiva** | Baseline (classe majoritária) + regra de negócio manual | Regressão Logística, Random Forest e Gradient Boosting, com validação cruzada e matriz de confusão explicada |
| 3 | **Prescritiva** | Recomendações por "bom senso" a partir das médias | Recomendações validadas por testes de hipótese (Qui-quadrado, ANOVA) e simulação de cenário ("e se") |

Cada seção do notebook termina com uma comparação explícita do par e uma conclusão sobre se houve, ou não, ganho real ao usar IA.

## Principais resultados

- Nenhuma variável disponível (idade, distância, valor, forma de pagamento, tipo de restaurante, dia da semana) apresentou associação estatisticamente significativa com o status do pedido (todos os testes com p-valor ≥ 0,05).
- Os modelos de Machine Learning (Regressão Logística, Random Forest, Gradient Boosting) obtiveram acurácia muito próxima da esperada em um chute aleatório (~33%, para 3 classes), o mesmo valendo para a tarefa de regressão do tempo de entrega (R² ≈ 0).
- A clusterização K-Means encontrou apenas segmentos fracos (*silhouette score* ~0,14), sem relação com o status do pedido.
- **Maior ganho da IA no projeto:** na análise prescritiva, a simulação de cenário mostrou que mudar a forma de pagamento não altera de forma relevante a probabilidade de cancelamento — evitando uma decisão operacional baseada em um padrão que não existe nos dados.
- **Conclusão:** o valor da IA aqui não foi "encontrar um padrão para agir" e sim **comprovar, com rigor estatístico, a ausência de sinal preditivo** nessas variáveis — e apontar quais dados novos precisariam ser coletados (motivo real do cancelamento, carga do entregador, clima, tempo de preparo do restaurante) para uma futura reanálise.


## Como executar

### Opção 1 — Google Colab (recomendado)
1. Baixe o notebook [`Analise_Delivery_Pares_Tradicional_vs_IA.ipynb`](./Analise_Delivery_Pares_Tradicional_vs_IA.ipynb) deste repositório.
2. Acesse [colab.research.google.com](https://colab.research.google.com/) → **Arquivo → Fazer upload de notebook**.
3. Rode as células em ordem (`Ambiente de execução → Executar tudo`).
4. Se o CSV não estiver na mesma pasta, uma janela de upload vai pedir o arquivo `daily_food_delivery_orders.csv` (baixe-o do Kaggle).

### Opção 2 — Ambiente local
```bash
git clone <link-deste-repositorio>
cd <pasta-do-repositorio>
pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter
jupyter notebook Analise_Delivery_Pares_Tradicional_vs_IA.ipynb
```

## Estrutura do repositório

```
├── Analise_Delivery_Pares_Tradicional_vs_IA.ipynb   # notebook completo (já executado, com gráficos)
├── daily_food_delivery_orders.csv                    # base de dados usada
└── README.md
```

## Limitações

O comportamento estatístico observado (correlações próximas de zero, testes de hipótese não significativos, acurácia de ML equivalente ao acaso) é típico de bases de dados sintéticas/geradas aleatoriamente para fins didáticos, comuns em datasets de prática no Kaggle. Isso não invalida a metodologia aplicada — pelo contrário, demonstra que ela é capaz de **detectar esse cenário** em vez de mascará-lo com métricas infladas.


