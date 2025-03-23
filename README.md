<strong> Ferramentas utilizadas: </strong> MySQL 

<br> 

## PROJETO 1

<br>

[Gerenciamento de Estacionamento](https://github.com/Thyzxt/portfolio_sql/blob/main/estacionamento.sql)

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
