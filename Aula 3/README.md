Tabelas criadas.

TB_CARTEIRA ( Carteira )

| Nome da Campo | Título            | Tipo      | Tamanho | Permite Nulo |
| ------------- | ----------------- | --------- | ------- | ------------ |
| CAR_ID        | ID Carteira       | Numérico  | 10      | Não          |
| CAR_NOME      | Nome da Carteira  | Caracter  | 100     | Não          |
	

TB_CENTRO_DE_CUSTO ( Centro de Custo )

| Nome da Campo | Título                  | Tipo      | Tamanho | Permite Nulo |
| ------------- | ----------------------- | --------- | ------- | ------------ |
| CC_ID         | ID do Centro            | Numérico  | 10      | Não          |
| CC_NOME       | Nome do centro de custo | Caracter  | 100     | Não          |

TB_GRUPO_CONTA ( Grupo de Conta )

| Nome da Campo | Título                 | Tipo      | Tamanho | Permite Nulo |
| ------------- | ---------------------- | --------- | ------- | ------------ |
| GC_ID         | ID do Grupo            | Numérico  | 10      | Não          |
| GC_NOME       | Nome do grupo de conta | Caracter  | 100     | Não          |


TB_CONTA ( Conta )

| Nome da Campo | Título                 | Tipo      | Tamanho | Permite Nulo |
| ------------- | ---------------------- | --------- | ------- | ------------ |
| CT_ID         | ID do Grupo            | Numérico  | 10      | Não          |
| CT_NOME       | Nome do grupo de conta | Caracter  | 100     | Não          |
| GC_ID         | ID do Grupo            | Caracter  | 100     | Não          |
