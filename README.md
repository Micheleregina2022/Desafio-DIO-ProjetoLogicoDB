# Bootcamp Potência Tech powered by iFood | Ciência de Dados - Digital Innovation One

</br>

![](https://img.shields.io/badge/MySQL-4479A1.svg?style=for-the-badge&logo=MySQL&logoColor=white)

</br> 

Este repositório contém um desafio de projeto lógico de banco de dados do Bootcamp Potência Tech powered by iFood | Ciência de Dados da DIO

O objetivo do projeto é criar um esquema de banco de dados e desenvolver um script SQL que abrange as seguintes cláusulas:
</br>

* Recuperações simples com SELECT Statement
* Filtros com WHERE Statement
* Criação de expressões para gerar atributos derivados
* Definição de ordenações dos dados com ORDER BY
* Aplicação de condições de filtros aos grupos com HAVING Statement
* Criação de junções entre tabelas para fornecer uma perspectiva mais complexa dos dados
* O objetivo final é aplicar o mapeamento para um cenário, refinando um modelo apresentado e acrescentando informações sobre clientes PJ e PF, pagamentos, e entregas com status e código de rastreio.

</br>

### Passo a passo:

</br>
Tabelas Criadas:

1. Cliente: Armazena informações dos clientes, tanto pessoa física quanto pessoa jurídica, com os campos: idCliente, Pnome, NMeioInicial, Sobrenome, CPF, Endereço e DataDeNascimento.

2. Pedido: Contém informações dos pedidos feitos pelos clientes, como idPedido, Status, Descrição, DataPedido e a chave estrangeira Cliente_idCliente relacionada à tabela Cliente.

3. Produto: Armazena informações dos produtos disponíveis para venda, com os campos idProduto, Categoria, Descrição e Valor.

4. Fornecedor: Contém informações sobre os fornecedores dos produtos, com os campos idFornecedor, RazaoSocial e CNPJ.

5. Disponibiliza: É uma tabela de relacionamento entre fornecedores e produtos, com as chaves estrangeiras Fornecedor_idFornecedor e Produto_idProduto para relacionar os fornecedores e produtos disponíveis.

6. Estoque: Armazena informações sobre o estoque dos produtos, com os campos idEstoque e Local.

7. Possui: É uma tabela de relacionamento entre estoque e produtos, com as chaves estrangeiras Estoque_idEstoque e Produto_idProduto para relacionar os estoques e produtos.

8. Relação Produto/Pedido: Tabela de relacionamento entre produtos e pedidos, com as chaves estrangeiras Produto_idProduto e Pedido_idPedido e campos como Quantidade e Status.

9. Entrega: Contém informações sobre a entrega dos pedidos, com os campos idEntrega, CodigoRastreio, DataEnvio, DataEntrega, Status e a chave estrangeira Pedido_idPedido relacionada à tabela Pedido.

10. TerceiroVendedor: Armazena informações sobre os vendedores terceirizados, com os campos idTerceiroVendedor, RazaoSocial e NomeFantasia.

11. ProdutoVendedor: É uma tabela de relacionamento entre vendedores terceirizados e produtos, com as chaves estrangeiras TerceiroVendedor_idTerceiroVendedor e Produto_idProduto para relacionar os vendedores e produtos.

12. PessoaFisica: Armazena informações específicas de clientes pessoa física, com os campos idPessoaFisica, CPF e a chave estrangeira Cliente_idCliente relacionada à tabela Cliente.

13. PessoaJuridica: Armazena informações específicas de clientes pessoa jurídica, com os campos idPessoaFisica, CNPJ e a chave estrangeira Cliente_idCliente relacionada à tabela Cliente.

14. Pagamento: Contém informações sobre os pagamentos dos pedidos, com os campos idPagamento, FormaPagamento e as chaves estrangeiras Pedido_idPedido e Pedido_Cliente_idCliente relacionadas à tabela Pedido.

15. Boleto: Tabela específica para informações de pagamentos feitos por boleto, com os campos idBoleto, Valor, DataPagamento e as chaves estrangeiras Pagamento_idPagamento, Pagamento_Pedido_idPedido e Pagamento_Pedido_Cliente_idCliente relacionadas à tabela Pagamento.

16. Cartão: Tabela específica para informações de pagamentos feitos por cartão de crédito, com os campos idCartão, Tipo, Parcelas, Valor, Número, DataVencimento e as chaves estrangeiras Pagamento_idPagamento, Pagamento_Pedido_idPedido e Pagamento_Pedido_Cliente_idCliente relacionadas à tabela Pagamento.

</br>

### Consultas SQL e expressões:

* Select da tabela cliente: Essa consulta seleciona todos os registros da tabela cliente e retorna todas as colunas disponíveis.

```mysql
SELECT * FROM cliente;
```

* Filtro com WHERE em pedidos: 
Nesta consulta, utilizamos o WHERE para filtrar os registros da tabela pedido onde o campo Cliente_idCliente é igual a 1, ou seja, estamos buscando os pedidos feitos pelo cliente de ID 1.

```mysql
SELECT * FROM pedido WHERE Cliente_idCliente = 1;
```

* Insert em cliente: Nesta consulta, realizamos uma inserção na tabela cliente, adicionando um novo cliente com os respectivos valores nas colunas especificadas.

```mysql
  INSERT INTO cliente
(`idCliente`, `Pnome`, `NMeioInicial`, `Sobrenome`, `CPF`, `Endereço`, `DataDeNascimento`)
VALUES 
(1, 'João', 'AB', 'Silva', '12345678901', 'Rua 1', '1990-01-01');
```

* Expressão com atributo derivado:
Essa consulta seleciona o registro da tabela cliente onde o idCliente é igual a 1 e a expressão (Pnome + ' ' + Sobrenome) é igual a 'João Silva'. Essa expressão concatena os valores das colunas Pnome e Sobrenome para comparar com o nome completo 'João Silva'.

```mysql
SELECT * FROM cliente WHERE idCliente = 1 AND (Pnome + ' ' + Sobrenome) = 'João Silva';
```


* Orderby em cliente: Nesta consulta, utilizamos o ORDER BY para ordenar os registros da tabela cliente com base na coluna DataDeNascimento, ou seja, os registros são exibidos em ordem crescente de data de nascimento.

```mysql
SELECT * FROM cliente ORDER BY DataDeNascimento;
```

* HAVING em cliente: Nesta consulta, utilizamos o HAVING para filtrar os resultados após a junção das tabelas cliente e pedido. O GROUP BY agrupa os registros pelo idCliente, Pnome, Sobrenome e CPF, e o HAVING seleciona apenas os grupos que têm mais de 10 registros, ou seja, clientes que fizeram mais de 10 pedidos.

```mysql
SELECT c.idCliente, c.Pnome, c.Sobrenome, c.CPF
FROM cliente c
INNER JOIN pedido p ON c.idCliente = p.Cliente_idCliente
GROUP BY c.idCliente, c.Pnome, c.Sobrenome, c.CPF
HAVING COUNT(c.idCliente) > 10;
```
</br>
</br>
</br>

#### Autora </br>
Michele Regina Bora
