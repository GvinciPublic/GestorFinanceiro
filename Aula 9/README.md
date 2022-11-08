CONS_RESUMO_DASHBOARD ( Resumo de valores ) View

| Nome da Campo    | Título                  | Tipo      | Máscara        | Tamanho |
| --------------   | ----------------------  | --------- | -------------- | ------- |
| Apagar           | A pagar                 | Numérico  | 99.999.999,99  | 10      |
| AReceber         | A receber               | Numérico  | 99.999.999,99  | 10      |
| Receita          | Receita                 | Numérico  | 99.999.999,99  | 10      |
| Despesa          | Despesa                 | Numérico  | 99.999.999,99  | 10      |
| Total            | Total                   | Numérico  | 99.999.999,99  | 10      |
| Transferencia    | Transferencia           | Numérico  | 99.999.999,99  | 10      |


Script da Views

```sql
    Select 
        Sum(Case When Cons_lancamentos.PAGO = 'Não' And Cons_lancamentos.LANC_TIPO ='Despesa' Then Cons_lancamentos.LANC_VALOR Else 0 End) As APagar,
        Sum(Case When Cons_lancamentos.PAGO = 'Não' And Cons_lancamentos.LANC_TIPO = 'Receita' Then Cons_lancamentos.LANC_VALOR Else 0 End) As AReceber,
        Sum(Case When Cons_lancamentos.LANC_TIPO = 'Receita' And Cons_lancamentos.PAGO = 'Sim' Then Cons_lancamentos.LANC_VALOR Else 0 End) As Receita,
        Sum(Case When Cons_lancamentos.LANC_TIPO = 'Despesa' And Cons_lancamentos.PAGO = 'Sim' Then Cons_lancamentos.LANC_VALOR Else 0 End) As Despesa,
        Sum(Case When Cons_lancamentos.LANC_TIPO = 'Transferência' And Cons_lancamentos.PAGO = 'Sim' Then Cons_lancamentos.LANC_VALOR Else 0 End) As Transferencia,
        Sum(Case When Cons_lancamentos.PAGO = 'Sim' Then Cons_lancamentos.LANC_VALOR Else 0 End) As Total
    From Cons_lancamentos
    Cross Join TB_CONFIGURACOES
    Where Cons_lancamentos.CAR_ID = IsNull(TB_CONFIGURACOES.CONFIG_CARTEIRA_PADRAO, Cons_lancamentos.CAR_ID)
```