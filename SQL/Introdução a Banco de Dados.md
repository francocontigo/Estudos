# Conceitos

O que é um Banco de Dados?
R: Conjunto de dados relacionados e persistentes, sendo constrído com um propósito específico para determinados usuários.

O que é um Sistema Gerenciador de Banco de dados(SGBD)?
R: Sistema utilizado para gerenciar um banco de dados, onde é permitido salvar, editar e consultar dados. Ex: MySql, Oracle, Postgre, SQL - Server.
* SGBD é uma coleção de dados e um conjunto de programas para acessar o BD.

### Modelo Entidade-Relacionamento

![[Pasted image 20220831090218.png]]

* Entidade - Elemento do mundo real. Ex: Pessoa, carro, exames, empresa, hotel;
* Relacionamento - 
* Atributos - Caracterizam as entidades. Dado ou informação, menor unidade da informação do banco dos dados, possui um atributo determinante.
Obs: Dado é a menor unidade da informação, dado é algo que "existe por si" enquanto a informação se dá pelo pelo processamento de algum dado.

![[Pasted image 20220831090701.png]]
Exemplo:
Entidade - Pessoa;
Dados simples: nome e cpf(por serem independentes);
Dado composto: Endereço, depende de outros 3 dados.

Conceito de chave primária:
Entre os atributos de uma entidade, pode-se extrair um conjunto que identifica as diferentes ocorrências, chamado de chave primária. A chave é escolhida para representar as diferentes ocorrências no BD.
Pode ser simples(um atributo) ou composta(2 ou mais atributos).
Seguindo o exemplo acima, CPF ou RG, pois sempre irá identificar a entidade Pessoa atráves do número do CPF.

Entidades podem se relacionar entre si, através de uma dependência mediante o recurso da herança(Entidade Sub/Super Tipos), por meio de múltiplos relacionamentos entre as entidades.
* Super Tipo: Entidade dominante que dita a forma da relação entre as entidades Sub Tipos;
* Mais de uma entidade pode ser dominante para relacionar entidades;

Cardinalidade(representação da quantidade de correspondências de um relacionamento). Tipos: 1:1 um para um, 1:N um para muitos, N:N muitos para muitos

# Modelo Relacional
Um BD Relacional é uma coleção de relações, tabelas;
![[Pasted image 20220831091824.png]]
Entidade: Departamento;
Atributos: CodDept e Nome, em forma de coluna;
Linha ou Tupla: Registro nas colunas;
Chave primária nesse caso: Simples, CodDept.

Chave Estrangeira(FK):
Utilizada quando precisamos que um valor de atributo seja validade a partir do valor de atributo de outra tabela(caracterizando dependência entre as tabelas).
![[Pasted image 20220831092313.png]]
Identificador da primeira tabela: CodDept;
Se fosse buscar o nome dos funcionários(ou as relações do departamento com um funcionário), cria-se uma coluna com o mesmo atributo em uma outra tabela para ser usado como identificador.

# SQl
### SCHEMA, TABLE VIEW
* Schema, pode ser um conjunto de tabelas. Ex: Escola, vai ter uma tabela sobre alunos, professores, áreas. Essas 3 tabelas vão estar em um Schema.
* Tabelas, forma de estruturar dados;
* View, forma de consultar dados sem poder alterar eles. Cria uma view para x usuário poder ver os dados.

### Tipos de Dados
Alguns tipos:
* INTEGER | SMALLINT - Número inteiro;
* DECIMAL(precision, scale) - precision, número total de digitos. scale, número de digitos após a vírgula;
* DOUBLE PRECISION | FLOAT | REAL - Pode ser inteiro ou decimal;
* CHAR(n) - Tamanho fixo - n Caracteres exemplo Estado: CHAR(2);
* VARCHAR(n) - Tamanho variavél de caracteres, n define o máximo;
* DATE | TIME | TIMESTAMP - Data, tempo e etc.

## Comandos
CREATE x - Cria uma tabela x, schema ou view;
DROP x - Remove um schema x, tabela ou view;
ALTER x - Altera um view x, schema ou tabela. 

## Create
Para criar uma tabela:
```SQL
CREATE TABLE tabela(
	atributo1 tipo [(tamanho)][NOT NULL | DEFAULT valor][CHECK(condição)],
	atributo2 tipo [(tamanho)][NOT NULL | DEFAULT valor][CHECK(condição)],
	atributo3 tipo [(tamanho)][NOT NULL | DEFAULT valor][CHECK(condição)],
);
```
![[Pasted image 20220831102914.png]]
Exemplo de criação
auto_increment cria algo sequencial automáticamente para usar como primary key.

### Drop Table
* Obs: É uma prática ruim
``DROP TABLE tabela [CASCADE | RESTRICT];
CASCADE: Todos os dados da tabela são removidos automaticamente e suas relações do esquema em outras tabelas;
RESTRICT: O esquema será removido se não existir dados.

### ALTER TABLE
``ALTER TABLE tabela [alter specification];
ou
`` ALTER TABLE tabela MODIFY COLUMN nome_coluna datatype
![[Pasted image 20220831103617.png]]

### Popular Tabela
```SQL
INSERT INTO tabela(coluna1, coluna2...)
VALUES(valor1, valo2...);
```
Exemplo
![[Pasted image 20220831103745.png]]

### Selecionar algo
```SQL
SELECT [DISTINCT | ALL]
FROM tabela;
```
ALL é representado por *
DISTINCT retira tuplas duplicadas
WHERE sempre vem depois do from, define condição
Exemplo:
![[Pasted image 20220831103939.png]]
GROUP BY atributo, mostra todos os registros em que estamos usando esse atributo, exemplo: cor, data, sexo
ORDER BY ASC | DESC, é a forma que o agrupamento vai aparecer.
Exemplo:
![[Pasted image 20220831104458.png]]

### UPDATE
Diferença entre ALTER x UPDATE:
ALTER TABLE se refere a coisas estruturais(coluna e tipos), enquanto o update trata os registros.
``` SQL
UPDATE table
set coluna = <valor>
<WHERE condição>;
```
Caso vá mudar as cores de um produto amarelo para vermelho por exemplo:
```SQL
UPDATE table
set cor = <vermelho>
<WHERE IS amarelo>;
```
![[Pasted image 20220831104929.png]]
Exemplo onde se atualiza o número de departamento do empregado.
### Operações
* AVG: Média;
* COUNT: Contagem;
* MAX: Máximo;
* MIN: Mínimo;
* STDDEV: Desvio padrão;
* SUM: Soma;
* VARIANCE: Variação;
exemplo para pegar o salário máximo entre os funcionários:
```SQL
MAX(SAL)
```
![[Pasted image 20220831105326.png]]
