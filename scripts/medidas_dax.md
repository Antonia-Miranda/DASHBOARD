# Medidas DAX

## Quantidade de Ações Massivas
```DAX
Qtd Ações = DISTINCTCOUNT(Acionamentos[ID_Acao])
```

## Quantidade de clientes 
```DAX
QTD_CLI = DISTINCTCOUNT(Clientes[ID_Cliente])
```

## Quantidade de contratos 
```DAX
QTD_CONTRATOS = DISTINCTCOUNT(Contratos[ID_Contrato])
```

## Resultado de Pagamento por Status 
```DAX
RESULTADO_PAGAMENTO = 
CALCULATE(
    DISTINCTCOUNT(Acionamentos[ID_Divida]),
    Acionamentos[Resultado] IN {
        "PAGAMENTO PARCIAL",
        "PROMESSA DE PAGAMENTO"
    }
)
```

## Somatoria do saldo da carteira
```DAX
VALOR_CARTEIRA = SUM(Contratos[Valor_Original])
```

## Ticket Médio da carteira 
```DAX
TKM_CARTEIRA = DIVIDE([VALOR_CARTEIRA], [QTD_CLI],0)
```

## Total de Acionamentos
```DAX
% Resultado = 
DIVIDE(
    [Qtd Ações],
    CALCULATE(
        [Qtd Ações],
        ALL(Acionamentos[Resultado])
    )
)
```

## % Representatividade de pagamento
```DAX
%RET_PAGO = 
DIVIDE([RESULTADO_PAGAMENTO],[Qtd Ações],0)
```

## Faixa de Renda - Criado a Coluna
```DAX
FAIXA RENDA = 
SWITCH(
    TRUE(),
    Clientes[Renda_Mensal] <= 2000, "1-Até R$ 2 mil",
    Clientes[Renda_Mensal] <= 5000, "2-R$ 2 mil a R$ 5 mil",
    Clientes[Renda_Mensal] <= 10000, "3-R$ 5 mil a R$ 10 mil",
    Clientes[Renda_Mensal] <= 20000, "4-R$ 10 mil a R$ 20 mil",
    "5-Acima de R$ 20 mil"
)
```

## Faixa de Score - Criado a Coluna
```DAX
FAIXA SCORE = 
SWITCH(
    TRUE(),
    Clientes[Score_Credito] <= 300, "Score Muito Baixo",
    Clientes[Score_Credito] <= 500, "Score Baixo",
    Clientes[Score_Credito] <= 700, "Score Médio",
    Clientes[Score_Credito] <= 850, "Score Alto",
    "Score Excelente"
)
```


## Faixa de Idade - Criado a Coluna
```DAX
RANGE_IDADE = SWITCH(
    TRUE(),
    Clientes[Idade] >= 18 && Clientes[Idade] <= 24, "18-24",
    Clientes[Idade] >= 25 && Clientes[Idade] <= 34, "25-34",
    Clientes[Idade] >= 35 && Clientes[Idade] <= 44, "35-44",
    Clientes[Idade] >= 45 && Clientes[Idade] <= 54, "45-54",
    Clientes[Idade] >= 55 && Clientes[Idade] <= 64, "55-64",
    Clientes[Idade] >= 65, "65+",
    "Não Informado"
)

```




