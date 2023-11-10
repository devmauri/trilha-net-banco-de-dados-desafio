# DIO - Trilha .NET - Banco de Dados
www.dio.me

## Desafio de projeto
Para este desafio, você precisará usar seus conhecimentos adquiridos no módulo de banco de dados, da trilha .NET da DIO.

## Contexto
Você é responsável pelo banco de dados de um site de filmes, onde são armazenados dados sobre os filmes e seus atores. Sendo assim, foi solicitado para que você realize uma consulta no banco de dados com o objetivo de trazer alguns dados para análises.

## Proposta
Você precisará realizar 12 consultas ao banco de dados, cada uma retornando um tipo de informação.
O seu banco de dados está modelado da seguinte maneira:

![Diagrama banco de dados](Imagens/diagrama.png)

As tabelas sao descritas conforme a seguir:

**Filmes**

Tabela responsável por armazenar informações dos filmes.

**Atores**

Tabela responsável por armazenar informações dos atores.

**Generos**

Tabela responsável por armazenar os gêneros dos filmes.

**ElencoFilme**

Tabela responsável por representar um relacionamento do tipo muitos para muitos entre filmes e atores, ou seja, um ator pode trabalhar em muitos filmes, e filmes
podem ter muitos atores.

**FilmesGenero**

Tabela responsável por representar um relacionamento do tipo muitos para muitos entre filmes e gêneros, ou seja, um filme pode ter mais de um gênero, e um genêro pode fazer parte de muitos filmes.

## Preparando o banco de dados
Você deverá executar o arquivo **Script Filmes.sql** em seu banco de dados SQL Server, presente na pasta Scripts deste repositório ([ou clique aqui](Script%20Filmes.sql)). Esse script irá criar um banco chamado **Filmes**, contendo as tabelas e os dados necessários para você realizar este desafio.

## Objetivo
Você deverá criar diversas consultas, com o objetivo de retornar os dados a seguir.

## 1 - Buscar o nome e ano dos filmes
### Resposta 
```
SELECT Filmes.Nome as "Nome", Filmes.Ano as "Ano"FROM Filmes
```

## 2 - Buscar o nome e ano dos filmes, ordenados por ordem crescente pelo ano
### Resposta 
```
SELECT Filmes.Nome as "Nome", Filmes.Ano as "Ano"
    FROM Filmes
    ORDER BY Ano ASC
```
## 3 - Buscar pelo filme de volta para o futuro, trazendo o nome, ano e a duração
### Resposta 
```
SELECT Filmes.Nome as "Nome", Filmes.Ano as "Ano", Filmes.Duracao as "Duração"
    FROM Filmes
    WHERE Nome = 'De Volta para o Futuro'
```
## 4 - Buscar os filmes lançados em 1997
### Resposta 
```
SELECT Filmes.Nome as "Nome", Filmes.Ano as "Ano", Filmes.Duracao as "Duração"
    FROM Filmes
    WHERE Ano = 1997
```
## 5 - Buscar os filmes lançados APÓS o ano 2000
### Resposta 
```
SELECT Filmes.Nome as "Nome", Filmes.Ano as "Ano", Filmes.Duracao as "Duração"
    FROM Filmes
    WHERE Ano >2000
```
## 6 - Buscar os filmes com a duracao maior que 100 e menor que 150, ordenando pela duracao em ordem crescente
### Resposta 
```
SELECT Filmes.Nome as "Nome", Filmes.Ano as "Ano", Filmes.Duracao as "Duração"
    FROM Filmes
    WHERE Duracao >100 AND Duracao <150
    ORDER BY Duracao ASC
```
## 7 - Buscar a quantidade de filmes lançadas no ano, agrupando por ano, ordenando pela quantidade em ordem decrescente
### Resposta 
```
SELECT Filmes.Ano as "Ano", COUNT(Filmes.Id) as "Quantidade"
    FROM Filmes
    GROUP BY Ano
    ORDER BY Quantidade DESC
```

## 8 - Buscar os Atores do gênero masculino, retornando o PrimeiroNome, UltimoNome
### Resposta 
```
SELECT Atores.PrimeiroNome as "Primeiro Nome", Atores.UltimoNome as "Ultimo Nome"
    FROM Atores
    WHERE Atores.Genero = 'M'
```
## 9 - Buscar os Atores do gênero feminino, retornando o PrimeiroNome, UltimoNome, e ordenando pelo PrimeiroNome
### Resposta 
```
SELECT Atores.PrimeiroNome as "Primeiro Nome", Atores.UltimoNome as "Ultimo Nome"
    FROM Atores
    WHERE Atores.Genero = 'F'
    ORDER BY [Primeiro Nome] ASC
```
## 10 - Buscar o nome do filme e o gênero
### Resposta 
```
SELECT Filmes.Nome as "Nome do Filme", Generos.Genero as "Gênero"
    FROM Filmes,Generos,FilmesGenero
    WHERE FilmesGenero.IdFilme=Filmes.Id
    and  FilmesGenero.IdGenero=Generos.Id
```
Ou utilizando Join
```
SELECT Filmes.Nome as "Nome do Filme", Generos.Genero as "Gênero"
    FROM Filmes
    INNER JOIN FilmesGenero
    on FilmesGenero.IdFilme=Filmes.Id
    INNER JOIN Generos
    on  FilmesGenero.IdGenero=Generos.Id
```
## 11 - Buscar o nome do filme e o gênero do tipo "Mistério"
### Resposta 
```
SELECT Filmes.Nome as "Nome do Filme", Generos.Genero as "Gênero"
    FROM Filmes,Generos,FilmesGenero
    WHERE FilmesGenero.IdFilme=Filmes.Id
    and  FilmesGenero.IdGenero=Generos.Id
    and Generos.Genero = 'Mistério'
``` 
Ou utilizando Join
```
SELECT Filmes.Nome as "Nome do Filme", Generos.Genero as "Gênero"
    FROM Filmes
    INNER JOIN FilmesGenero
    on FilmesGenero.IdFilme=Filmes.Id
    INNER JOIN Generos
    on  FilmesGenero.IdGenero=Generos.Id
    and Generos.Genero = 'Mistério'
```
## 12 - Buscar o nome do filme e os atores, trazendo o PrimeiroNome, UltimoNome e seu Papel
### Resposta 
```
SELECT Filmes.Nome as "Nome do Filme", Atores.PrimeiroNome as "Nome Ator", Atores.UltimoNome as "Ultimo Nome Ator", ElencoFilme.Papel as "Papel do Ator"
    FROM Filmes,Atores, ElencoFilme
    WHERE ElencoFilme.IdFilme=Filmes.Id
    and  ElencoFilme.IdAtor=Atores.Id
    ORDER BY [Nome do Filme]
```
Ou utilizando Join
```
SELECT Filmes.Nome as "Nome do Filme", Atores.PrimeiroNome as "Nome Ator", Atores.UltimoNome as "Ultimo Nome Ator", ElencoFilme.Papel as "Papel do Ator"
    FROM Filmes
    INNER JOIN ElencoFilme
    ON ElencoFilme.IdFilme=Filmes.Id
    INNER JOIN Atores
    ON ElencoFilme.IdAtor=Atores.Id
    ORDER BY [Nome do Filme]
```