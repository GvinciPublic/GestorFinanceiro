CONS_GRAFICO ( Gráfico ) View

| Nome da Campo    | Título                  | Tipo      | Máscara        | Tamanho |
| --------------   | ----------------------  | --------- | -------------- | ------- |
| Mes              | Mês                     | Caracter  |                | 10      |
| Tipo             | Tipo                    | Caracter  |                | 10      |
| Valor            | Saldo                   | Numérico  | 99.999.999,99  | 10      |

Script da Views

```sql
Select Top 24 tb.Mes,
  tb.Tipo,
  tb.Valor,
  tb.A,
  tb.M
From (Select Top 1000 Format(TB_LANCAMENTO.LANC_DATA_PAG, 'MM/yyyy') As Mes,
      'Entrada' As Tipo,
      Sum(TB_LANCAMENTO.LANC_VALOR) As Valor,
      Year(TB_LANCAMENTO.LANC_DATA_PAG) As A,
      Month(TB_LANCAMENTO.LANC_DATA_PAG) As M
    From TB_LANCAMENTO
      Cross Join TB_CONFIGURACOES
    Where TB_LANCAMENTO.LANC_DATA_PAG Between DateAdd(M, -5, GetDate()) And
      DateAdd(M, +6, GetDate()) And TB_LANCAMENTO.LANC_TIPO = 'Entrada' And
      TB_LANCAMENTO.CAR_ID = IsNull(TB_CONFIGURACOES.CONFIG_CARTEIRA_PADRAO,
      TB_LANCAMENTO.CAR_ID) And TB_LANCAMENTO.LANC_PAGO = 1
    Group By Format(TB_LANCAMENTO.LANC_DATA_PAG, 'MM/yyyy'),
      Year(TB_LANCAMENTO.LANC_DATA_PAG),
      Month(TB_LANCAMENTO.LANC_DATA_PAG)
    Union All
    Select Top 1000 Format(TB_LANCAMENTO.LANC_DATA_PAG, 'MM/yyyy') As Mes,
      'Saída' As Tipo,
      Sum(TB_LANCAMENTO.LANC_VALOR) As Valor,
      Year(TB_LANCAMENTO.LANC_DATA_PAG) As A,
      Month(TB_LANCAMENTO.LANC_DATA_PAG) As M
    From TB_LANCAMENTO
      Cross Join TB_CONFIGURACOES
    Where TB_LANCAMENTO.LANC_DATA_PAG Between DateAdd(M, -5, GetDate()) And
      DateAdd(M, +6, GetDate()) And TB_LANCAMENTO.LANC_TIPO = 'Saída' And
      TB_LANCAMENTO.CAR_ID = IsNull(TB_CONFIGURACOES.CONFIG_CARTEIRA_PADRAO,
      TB_LANCAMENTO.CAR_ID) And TB_LANCAMENTO.LANC_PAGO = 1
    Group By Format(TB_LANCAMENTO.LANC_DATA_PAG, 'MM/yyyy'),
      Year(TB_LANCAMENTO.LANC_DATA_PAG),
      Month(TB_LANCAMENTO.LANC_DATA_PAG)) As tb
Order By tb.A,
  tb.M
```
