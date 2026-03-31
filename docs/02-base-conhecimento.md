# Base de Conhecimento

## Dados Utilizados



| Arquivo | Formato | Para que serve no Agente de IA para Monitoramento de Custos Financeiros |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores, ou seja, dar continuidade ao atendimento de forma mais eficiente. |
| `perfil_investidor.json` | JSON | Personalizar o comportamento do agente, permitindo análises mais precisas e recomendações alinhadas ao perfil do cliente.|
| `transacoes.json` | JSON | Contém o histórico de transações financeiras do cliente (gastos, receitas, categorias).|
| `limites.csv` | CSV | Define limites de gastos por categoria e orçamento mensal do cliente. |
| `alertas_config.csv` | CSV | Configura regras de alertas, frequência de notificações e preferências do usuário. |
| `categorias.csv` | CSV | Lista e organiza as categorias de despesas (alimentação, transporte, lazer, etc.). |



---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

O produto Fundo Imobiliário (FII) substituiu o Fundo Multimercado, pois pessoalmente me sinto mais confiante em usar apenas produtos financeiros que eu conheço. Assim,poderei validar as respostas do Agente de IA para Monitoramento de Custos Financeiros de forma mais assertiva.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.
Existem duas possibilidades, injetar os dados diretamente no prompt (Ctrl + C, Ctrl + V) ou carregar os arquivos via código, como no exemplo abaixo:

import pandas as pd
import json

print(resposta.choices[0].message.content)


# CSVs
historico - pd_read_csv('data/historico_atendimento.csv')
transacoes -pd_read_csv('data/transacoes.csv')

# jsons
with open('data/perfil_investidor.json', 'r'. encoding= 'utf=8') as f:
perfil - json.load(f)

with open("data/produtos_financeiros.json', 'r', encoding='utf-8') as f:
produtos = json.load(f)

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

historico_atendimento
perfil_investidor
transacoes
limites
alertas_config
categorias


---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida
