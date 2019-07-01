## MySQL comando e scripts

### 1ª Forma Normal(FN):

>**1-** Todo campo vetorizado se torna outra tabela. 

>**2-** Todo campo multivalorado se tornará outra tabela. **Atomicidade:** Um campo não pode ser divisível.

>**3-** Toda tabela necessita de pelo menos um campo que identifique todo o registro como sendo único(**Chave Primária**).

### 2ª Forma Normal(FN):

>Dependência direta. As chaves primárias(agregadas/composta) na mesma tabela passam a ser campos comuns em uma tabela com sua própria chave primária. A união dos campos assosciativos: qualquer campo não chave deve depender da totalidade das chaves. 

### 3ª Forma Normal(FN):

>Dependência transitiva. Os campos não chave que não depende da totalidade das chaves,mas sim de outros campos não chave. Eles se tornam outra tabela.

### DDL (Data Definition Language)-> Linguagem de definição de dados.
  >**Exemplos de comando:** Create table, Create DataBase, Alter Table, Drop Table.
### DML (Data Manipulation Language)-> Linguagem de manipulação de dados.
  >**Exemplos de comandos:** Insert Into, Update, Delete, Truncate.
### DQL (Data Query Language)-> Requisição de dados ou consulta.
  >**Exemplo:** SELECT
### DTL (Data Transaction Language)-> Linguagem de transação de dados.
  >**Exemplos de comandos:** BEGIN TRANSACTION, COMMIT E ROLLBACK.
### DCL (Data Control Language)-> Linguagem de controle de dados.
  >**Exemplo:** GRANT,REVOKE e DENY.
  
  ## Tipagem dos dados em MySQL
  
  |Tipo|Uso|
  |:---:|---|
  |**CHAR**|String. Caractéres|
  |**VARCHAR**|String Variante|
  |**INT**|Numéricos|
  |**FLOAT**|Numéricos.Pontos flutuantes|
  |**BLOB**|Fotos e documentos|
  |**TEXT**|Para textos extensos|
  
  #### CHAR x VARCHAR
  
  **CHAR:** Usado para locação de dados estáticos, pois não varia o seu tamanho, mantém o tamanho definido na sua criação.
  **VARCHAR:** Usado para dados variantes. Assim, o tamanho pode variar de acordo com o dado armazenado até o limite especificado na sua criação.
  
  #### ENUM - está presente apenas no MySQL
  
  #### Tratando consultas com menor impacto na performace
  
  **Situação - Trantando com OU/OR:** 70%(dado I) e 30%(dado II), passe o dado com maior procentagem(quantidade) como primeiro parâmetro.
  
  **Situação - Trantando com E/AND:** 70%(dado I) e 30%(dado II), passe o dado com menor procentagem(quantidade) como primeiro parâmetro.
  
  
>**OBS:** Extensão de arquivos SQL termina com : **.sql**
