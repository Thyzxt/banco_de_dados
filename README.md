<strong> Ferramentas utilizadas: </strong> MySQL 

<br> 

## PROJETO 1

<br>

[Gerenciamento de Estacionamento](https://github.com/Thyzxt/banco_de_dados/blob/main/estacionamento.sql)

Consulta das informações sobre os carros cadastrados, suas marcas, e permanências no estacionamento.

<br>

Tópicos:

- Manipulação de dados

```sql
-- Alterando a placa do carro
UPDATE Carro
SET Placa = 'JKL8765'
WHERE Placa LIKE 'JKL9999';
```

<br>

- Agregação de informações 

```sql
-- Listando a descricao e a placa de cada carro, contando quantas vezes o carro permaneceu
SELECT P.CarroPlaca, C.Descricao, COUNT(P.CarroPlaca) AS Permanencia
FROM Permanencia P
INNER JOIN Carro C
ON P.CarroPlaca = C.Placa
GROUP BY P.CarroPlaca, C.Descricao;
```

<br>

- Filtragem de dados

```sql
-- Listando a placa dos carros que não tiveram nenhuma permanencia
SELECT Placa
FROM Carro
WHERE Placa NOT IN (SELECT DISTINCT CarroPlaca FROM Permanencia);
```

<br>

- Junção entre tabelas

```sql
-- Listando a marca, a descricao e a placa dos carros
SELECT C.Descricao, C.Placa, M.Nome
FROM Carro C
INNER JOIN Marca M
ON C.MarcaId = M.Id;
```

<br> <br>

## PROJETO 2

<br>

[Gerenciamento de Biblioteca Pública](https://github.com/Thyzxt/banco_de_dados/blob/main/biblioteca.sql)

Organização das atividades e informações sobre autores, empréstimos, membros e livros.

<br>

Tópicos:

- Manipulação de dados

```sql
-- Mudando a data de devolução real de todos os empréstimos para a data atual
UPDATE Emprestimo
SET DtaDevolucao = CURDATE();
```

<br>

- Agregação de informações

```sql
-- Listando o nome da categoria e a quantidade de livros por categoria
SELECT C.Genero, COUNT(L.Id) AS QtdLivros
FROM Categoria C 
INNER JOIN Livro L 
ON C.Id = L.Categoria
GROUP BY C.Id;
```

<br>

- Filtragem de dados

```sql
-- Listando todos os livros que nunca foram emprestados
SELECT Titulo
FROM Livro
WHERE Id NOT IN (SELECT LivroId FROM Emprestimo);
```

<br>

- Junção entre tabelas

```sql
-- Listando a data de empréstimo, data da devolução real, nome do membro que emprestou, título do livro, nome da categoria e nome do autor (ou autores) de todos os empréstimos realizados
SELECT DtaEmprestimo, DtaDevolucao, M.Nome, L.Titulo, C.Genero, A.Nome
FROM Emprestimo E
INNER JOIN Membro M 
ON E.MembroId = M.Id
INNER JOIN Livro L 
ON E.LivroId = L.Id
INNER JOIN Categoria C 
ON L.Categoria = C.Id
INNER JOIN Autor A 
ON L.AutorId = A.Id;
```

<br> <br>

## PROJETO 3

<br>

[Gerenciamento de Hotel e Serviços](https://github.com/Thyzxt/portfolio_sql/blob/main/hotel.sql)

Controle de dados em um hotel sobre os clientes, acomodações, reservas, serviços e as formas de pagamento.

<br>

Tópicos:

- Manipulação de dados

```sql 
-- Aplicando um acréscimo de 15% nas diárias dos quartos acima do 3º andar
UPDATE Quarto
SET VlrDiaria = VlrDiaria * 1.15
WHERE Andar > 3;
```

<br>

- Agregação de informações

```sql
-- Contando o número de reservas feitas por cada cliente
SELECT ClienteId, COUNT(*) AS NumeroDeReservas
FROM Reserva
GROUP BY ClienteId;
```

<br>

- Filtragem de dados

```sql
-- Listando CPF e CEP dos clientes brasileiros residentes em Curitiba
SELECT CPF, CEP
FROM ClienteBrasileiro
WHERE Cidade = 'Curitiba';
```

<br>

- Junção entre tabelas

```sql
-- Listando o nome de todos os clientes e a data de entrada de suas reservas
SELECT C.Nome, R.Entrada
FROM Cliente C
INNER JOIN Reserva R
ON C.Id = R.ClienteId
ORDER BY C.Nome ASC;
```
