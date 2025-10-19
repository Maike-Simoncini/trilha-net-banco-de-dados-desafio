# DIO - Trilha .NET - Banco de Dados  
🌐 [www.dio.me](https://www.dio.me)

## 📌 Desafio de projeto
Para este desafio, você precisará usar seus conhecimentos adquiridos no módulo de banco de dados, da trilha .NET da DIO.

## 🎯 Contexto
Você é responsável pelo banco de dados de um site de filmes, onde são armazenados dados sobre os filmes e seus atores. Sendo assim, foi solicitado que você realize consultas no banco de dados com o objetivo de trazer dados para análises.

## 📋 Proposta
Você precisará realizar **12 consultas** ao banco de dados, cada uma retornando um tipo de informação.  
O seu banco de dados está modelado da seguinte maneira:

![Diagrama banco de dados](Imagens/diagrama.png)

As tabelas são descritas conforme a seguir:

**📽️ Filmes**  
Tabela responsável por armazenar informações dos filmes.

**🎭 Atores**  
Tabela responsável por armazenar informações dos atores.

**🏷️ Generos**  
Tabela responsável por armazenar os gêneros dos filmes.

**👥 ElencoFilme**  
Tabela de relacionamento muitos-para-muitos entre filmes e atores.

**🎭🏷️ FilmesGenero**  
Tabela de relacionamento muitos-para-muitos entre filmes e gêneros.

## ⚙️ Preparando o banco de dados
Execute o arquivo **`Script Filmes.sql`** no SQL Server (disponível na pasta `Scripts` ou [clique aqui](Script%20Filmes.sql)). Ele criará o banco **Filmes** com todas as tabelas e dados de exemplo.

## 🎯 Objetivo
Crie as consultas abaixo. O resultado de cada uma deve ser **idêntico às imagens fornecidas**.

---

## 1️⃣ Buscar o nome e ano dos filmes

### 🔍 Pesquisa
```sql
SELECT Nome, Ano
FROM Filmes;
```

### 🖼️ Resultado Esperado
![Exercicio 1](Imagens/1.png)

---

## 2️⃣ Buscar o nome e ano dos filmes, ordenados por ordem crescente pelo ano

### 🔍 Pesquisa
```sql
SELECT Nome, Ano
FROM Filmes
ORDER BY Ano ASC;
```

### 🖼️ Resultado Esperado
![Exercicio 2](Imagens/2.png)

---

## 3️⃣ Buscar pelo filme "De Volta para o Futuro", trazendo o nome, ano e a duração

### 🔍 Pesquisa
```sql
SELECT Nome, Ano, Duracao
FROM Filmes
WHERE Nome = 'De Volta para o Futuro';
```

### 🖼️ Resultado Esperado
![Exercicio 3](Imagens/3.png)

---

## 4️⃣ Buscar os filmes lançados em 1997

### 🔍 Pesquisa
```sql
SELECT *
FROM Filmes
WHERE Ano = 1997;
```

### 🖼️ Resultado Esperado
![Exercicio 4](Imagens/4.png)

---

## 5️⃣ Buscar os filmes lançados APÓS o ano 2000

### 🔍 Pesquisa
```sql
SELECT *
FROM Filmes
WHERE Ano > 2000;
```

### 🖼️ Resultado Esperado
![Exercicio 5](Imagens/5.png)

---

## 6️⃣ Buscar os filmes com a duração maior que 100 e menor que 150, ordenando pela duração em ordem crescente

### 🔍 Pesquisa
```sql
SELECT *
FROM Filmes
WHERE Duracao > 100 AND Duracao < 150
ORDER BY Duracao ASC;
```

### 🖼️ Resultado Esperado
![Exercicio 6](Imagens/6.png)

---

## 7️⃣ Buscar a quantidade de filmes lançados por ano, agrupando por ano, ordenando pela quantidade em ordem decrescente

> ⚠️ **Observação**: O enunciado menciona "ordenando pela duração", mas isso é logicamente inviável com `GROUP BY Ano`. A imagem de resultado mostra ordenação por **quantidade**. A consulta abaixo está correta e compatível com o resultado esperado.

### 🔍 Pesquisa
```sql
SELECT Ano, COUNT(*) AS Quantidade
FROM Filmes
GROUP BY Ano
ORDER BY Quantidade DESC;
```

### 🖼️ Resultado Esperado
![Exercicio 7](Imagens/7.png)

---

## 8️⃣ Buscar os Atores do gênero masculino, retornando o PrimeiroNome e UltimoNome

### 🔍 Pesquisa
```sql
SELECT PrimeiroNome, UltimoNome
FROM Atores
WHERE Genero = 'M';
```

### 🖼️ Resultado Esperado
![Exercicio 8](Imagens/8.png)

---

## 9️⃣ Buscar os Atores do gênero feminino, retornando o PrimeiroNome e UltimoNome, ordenando pelo PrimeiroNome

### 🔍 Pesquisa
```sql
SELECT PrimeiroNome, UltimoNome
FROM Atores
WHERE Genero = 'F'
ORDER BY PrimeiroNome;
```

### 🖼️ Resultado Esperado
![Exercicio 9](Imagens/9.png)

---

## 🔟 Buscar o nome do filme e o gênero

### 🔍 Pesquisa
```sql
SELECT f.Nome, g.Genero
FROM Filmes f
JOIN FilmesGenero fg ON f.Id = fg.IdFilme
JOIN Generos g ON fg.IdGenero = g.Id;
```

### 🖼️ Resultado Esperado
![Exercicio 10](Imagens/10.png)

---

## 1️⃣1️⃣ Buscar o nome do filme e o gênero do tipo "Mistério"

### 🔍 Pesquisa
```sql
SELECT f.Nome, g.Genero
FROM Filmes f
JOIN FilmesGenero fg ON f.Id = fg.IdFilme
JOIN Generos g ON fg.IdGenero = g.Id
WHERE g.Genero = 'Mistério';
```

### 🖼️ Resultado Esperado
![Exercicio 11](Imagens/11.png)

---

## 1️⃣2️⃣ Buscar o nome do filme e os atores, trazendo o PrimeiroNome, UltimoNome e seu Papel

### 🔍 Pesquisa
```sql
SELECT f.Nome, a.PrimeiroNome, a.UltimoNome, ef.Papel
FROM Filmes f
JOIN ElencoFilme ef ON f.Id = ef.IdFilme
JOIN Atores a ON ef.IdAtor = a.Id;
```

### 🖼️ Resultado Esperado
![Exercicio 12](Imagens/12.png)
