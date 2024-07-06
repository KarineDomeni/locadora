# Locadora

Este projeto contém diversas consultas SQL para análise de dados em um banco de dados de filmes e alugueis. As consultas foram organizadas em diferentes casos de uso para demonstrar como realizar análises agregadas, utilizar subconsultas e criar views.

## Tabelas Utilizadas
- `alugueis`
- `atores`
- `atuacoes`
- `clientes`
- `filmes`

## Consultas SQL

###  1: Análise do Preço Médio de Aluguel dos Filmes
Consulta para descobrir o preço médio de aluguel dos filmes.
```sql
SELECT AVG(preco_aluguel) FROM filmes;
```
###  2: Preço Médio por Gênero de Filme
Análise para descobrir o preço médio para cada gênero de filme.
```sql
SELECT 
    genero,
    ROUND(AVG(preco_aluguel), 2) AS preco_medio,
    COUNT(*) AS qtd_filmes
FROM filmes
GROUP BY genero;
```

###  3: Preço Médio por Gênero para Filmes Lançados em 2011
Análise semelhante ao Case 2, mas considerando apenas os filmes com ano de lançamento igual a 2011.
```sql
SELECT
    genero,
    ROUND(AVG(preco_aluguel), 2) AS preco_medio,
    COUNT(*) AS qtd_filmes
FROM filmes 
WHERE ano_lancamento = 2011
GROUP BY genero;
```

###  4: Identificação de Aluguéis com Nota Acima da Média
Análise de desempenho dos alugueis para identificar quais aluguéis tiveram nota acima da média.
```sql
-- Calcular a média das notas de aluguel
SELECT AVG(nota) FROM alugueis; -- 7.94

-- Selecionar aluguéis com nota acima da média
SELECT 
    *    
FROM alugueis
WHERE nota >= (SELECT AVG(nota) FROM alugueis);
```

###  5: Criação de Views
Criando uma view para armazenar o resultado de uma consulta no banco de dados.
```sql
CREATE VIEW resultado AS
SELECT
    genero,
    ROUND(AVG(preco_aluguel), 2) AS media_preco,
    COUNT(*) AS qtd_filmes
FROM filmes
GROUP BY genero;

-- Consultar a view criada
SELECT * FROM resultado;
```

### Ferramentas Utilizadas
MySQL
