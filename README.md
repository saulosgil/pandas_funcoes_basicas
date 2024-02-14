# Pandas -  A potente biblioteca para análise de dados do Python
 - ### Explorando funções básicas 

![python.jpg]

Pandas é uma biblioteca de software de código aberto amplamente utilizada na linguagem de programação Python para manipulação e análise de dados. Foi criada por Wes McKinney em 2008 enquanto trabalhava na AQR Capital Management e desde então se tornou uma das ferramentas mais populares para análise de dados em Python.

O Pandas oferece estruturas de dados flexíveis e eficientes, especialmente duas estruturas principais: Series e DataFrame.

- *Series* é uma estrutura unidimensional que pode armazenar dados de qualquer tipo;

- *DataFrame* é uma estrutura bidimensional que se assemelha a uma planilha, com linhas e colunas rotuladas, permitindo manipulação de dados de forma poderosa e intuitiva.

Além das estruturas de dados, o Pandas fornece uma ampla gama de funcionalidades para ler e escrever dados em diversos formatos, como CSV, Excel, SQL, JSON, entre outros. 

Ele também oferece funcionalidades para limpeza, transformação, agregação e análise de dados, tornando-o uma ferramenta essencial para cientistas de dados, analistas e desenvolvedores que trabalham com dados em Python.

Neste notebook, eu irei aplicar algumas funções do Pandas pra exemplificar. 

## 1. Estrutura de dados

O Pandas fornece duas estruturas de dados fundamentais: Series e DataFrame.

Compreender essas estruturas de dados é essencial para um tratamento eficaz de dados com o Pandas.

### 1.1 Series
*Series* é uma matriz rotulada unidimensional que pode conter vários tipos de dados, como inteiros, flutuantes, strings ou até mesmo objetos personalizados. É semelhante a uma coluna em uma planilha do Excel ou a uma única coluna em uma tabela SQL.

Os principais recursos da série incluem:

- ***Rotulagem***: Cada elemento de uma Serie possui um rótulo ou índice, que permite fácil acesso e manipulação de dados;

- ***Dados homogêneos***: Ao contrário das listas em Python, Series normalmente armazena dados do mesmo tipo, garantindo consistência.

- ***Operações vetorizadas***: você pode realizar operações vetorizadas em séries, tornando-as eficientes para cálculos elemento a elemento. Este recurso permite executar operações com eficiência em colunas ou séries inteiras sem a necessidade de loops explícitos. É possivel adicionar, subtrair e multiplicar as séries (colunas de um dataframe) por uma série ou escalar.

**Vamos criar uma Serie e aplicar uma função vetorizada para visualizar!**


```python
import pandas as pd

data = [1, 2, 3, 4]
series = pd.Series(data, name='MySeries')

# Operação vetorizada
series = series * 2 
series
```




    0    2
    1    4
    2    6
    3    8
    Name: MySeries, dtype: int64



### 1.2 DataFrame

Um DataFrame é uma estrutura de dados tabular bidimensional com eixos rotulados (linhas e colunas). 

Assemelha-se a uma planilha ou tabela SQL e é a principal estrutura de dados para análise de dados no Pandas.

Os principais recursos dos DataFrames incluem:

 - ***Colunas***: Cada coluna em um DataFrame é uma Serie, o que significa que pode conter diferentes tipos de dados;

- ***Indexação***: DataFrames possuem índices de linha e coluna, permitindo uma seleção flexível de dados;

- ***Alinhamento de dados***: Assim como o Series, os DataFrames podem alinhar dados com base em rótulos, tornando as operações fáceis e intuitivas;

- ***Integração de dados***: você pode mesclar, unir e concatenar DataFrames para combinar e analisar dados de várias fontes.

**Vamos criar um dataframe e aplicar uma função para renomear as colunas!**


```python
import pandas as pd

data = {
 "Name": ["Alice", "Bob", "Charlie", "David"],
 "Age": [25, 30, 35, 40],
 "City": ["New York", "San Francisco", "Los Angeles", "Chicago"]
}

'''No formato acima, o objeto data é um dict. 
Veja o retorno do código abaixo.'''
type(data)
```




    dict




```python
# transformando em um dataframe
df = pd.DataFrame(data)

# Pronto, agora é um df
type(df)
```




    pandas.core.frame.DataFrame



#### Dando uma olhadinha no df


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>



#### Renomeando as colunas com Pandas


```python
# Renaming the 'Name' column to 'Person_Name'
df.rename(columns={'Name':'Person_Name'})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Person_Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>



## Carregamento de dados e inspeção inicial

#### 2.1 Lendo dados de diferentes formatos (CSV, Excel, SQL, etc.)

Pandas fornece uma ampla variedade de funções e métodos para carregar dados de várias fontes e formatos com eficiência em DataFrames.


```python
'''
import pandas as pd

# carrega dados de um csv pelo nome - data.csv
df_csv = pd.read_csv('data.csv')

# arrega dados de um excel pelo nome - data.xlsx
df_excel = pd.read_excel('data.xlsx')

# Especificando a aba do excel
df_sheet1 = pd.read_excel('data.xlsx', sheet_name='Sheet1')

# Crie um mecanismo SQLAlchemy
from sqlalchemy import create_engine
engine = create_engine('sqlite:///mydatabase.db')

# Carrega dados de uma tabela de banco de dados SQL
query = 'SELECT * FROM mytable'
df_sql = pd.read_sql_query(query, engine)

# Carregar dados de uma tabela HTML em uma página da web
url = 'https://example.com/data-table.html'
df_html_table = pd.read_html(url)

# Carregar dados de um arquivo JSON
df_json = pd.read_json('data.json')

# Carregar dados do arquivo Parquet
df_parquet = pd.read_parquet('data.parquet')
'''

'''
Nenhum dos códigos funcionam, servem apenas como exemplo de sintaxe.
'''
```




    '\nNenhum dos códigos funcionam, servem apenas como exemplo de sintaxe.\n'



****Parâmetros importantes a serem lembrados para usar o read_csv:****

- **1. filepath**: especifica o caminho para o arquivo CSV que você deseja ler. Você pode fornecer um caminho de arquivo (como uma string), uma URL ou um objeto semelhante a um arquivo;

- **2.** Para substituir nomes de colunas, você deve usar **names** como um parâmetro com a lista de novos nomes de colunas;

- **3. sep**: significa "separador" e define o caractere usado para separar campos no arquivo CSV. O padrão é uma vírgula (,), mas você pode especificar outros caracteres, como tabulações ('\t'), ponto e vírgula (';') ou qualquer delimitador personalizado;

- **4. index_col**: é o parâmetro que especifica quais colunas devem ser usadas como índice de quadros de dados. Você pode passar um nome de coluna ou um índice de coluna (baseado em 0) para esse parâmetro;

- **5. skiprows**: permite pular um número específico de linhas no início do arquivo CSV. Pode ser útil se houver metadados ou comentários no início do arquivo que você deseja ignorar.

#### 2.2 Exibindo DataFrames


Em geral, exibir um dataframe é o primeiro passo para compreender seu conteúdo. Você pode simplesmente digitar o nome do dataframe e executar a célula para ver as 5 linhas superiores e as 5 linhas inferiores. 

o Pandas oferece vários outros métodos para exibir diferentes partes do seu quadro de dados:

 - ****.head(n)****: Exibe as primeiras n linhas do quadro de dados. É útil para obter uma visão geral rápida da estrutura dos dados sem se sobrecarregar com muitas informações ou, se quiser apenas ver os nomes das colunas, você pode usar .columns;

- ****.tail(n)****: Semelhante a .head(), este método mostra as últimas n linhas do DataFrame. É útil para verificar o final do conjunto de dados;

- ****.sample(n)****: Serve para ver linhas aleatórias do DataFrame.


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>




```python
# df.sample(n=2) # deixei comentado para usar o df com outros métodos
```

#### 2.3 Exploração de dados: formato, informação, descrição


Pandas fornece métodos para obter insights fundamentais sobre seus dados. Estas são as primeiras coisas que você precisa verificar ao explorar seus dados.


- ****1. .shape****: Fornece um Serie onde o primeiro elemento especifica o número de amostras/linhas e o segundo elemento especifica o número de colunas;

- ****2. .info()****: Fornece um resumo conciso do DataFrame, incluindo os tipos de dados, contagens não nulas e uso de memória. É um excelente ponto de partida para entender a estrutura dos dados, ou se você quiser apenas ver os tipos de dados, pode usar ****.dtypes****;

- ****3. .describe()****: O método gera estatísticas básicas para cada coluna numérica no DataFrame, como contagem, média, desvio padrão, valores mínimos e máximos.


```python
# Shape
df.shape
```




    (4, 3)




```python
print(f'O dataframe contém {df.shape[0]} linhas e {df.shape[1]} colunas.')
```

    O dataframe contém 4 linhas e 3 colunas.
    


```python
# para confirmar
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>




```python
# info
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4 entries, 0 to 3
    Data columns (total 3 columns):
     #   Column  Non-Null Count  Dtype 
    ---  ------  --------------  ----- 
     0   Name    4 non-null      object
     1   Age     4 non-null      int64 
     2   City    4 non-null      object
    dtypes: int64(1), object(2)
    memory usage: 224.0+ bytes
    


```python
# Estatisticas básicas
df.describe()

# Repare que ele pegou apenas a coluna númerica
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>4.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>32.500000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>6.454972</td>
    </tr>
    <tr>
      <th>min</th>
      <td>25.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>28.750000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>32.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>36.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>40.000000</td>
    </tr>
  </tbody>
</table>
</div>



##### 2.4 Valores únicos, contagens de valores e estatísticas básicas



Para dados categóricos ou discretos, você podemos explorar valores únicos e suas frequências:

- ****.nunique()****: Calcula o número de valores únicos em cada coluna. É útil para compreender a diversidade de dados em colunas categóricas;

- ****.column_name ou ['column_name']****: Para acessar uma coluna específica no DataFrame. Você só pode usar a segunda abordagem quando o nome da coluna tiver espaços;

****.value_counts()****: Conta as ocorrências de cada valor exclusivo em uma coluna específica. É particularmente útil para colunas categóricas.


```python
# dataframe com 6 valores
unique_df = pd.DataFrame(["saulo","saulo","dri","su","sil"])

unique_df.shape
```




    (5, 1)




```python
# Quantos valores unicos
unique_df.nunique()
```




    0    4
    dtype: int64




```python
# para acessar uma coluna - Ambos retornam o mesmo resultado
df.City
df['City']
```




    0         New York
    1    San Francisco
    2      Los Angeles
    3          Chicago
    Name: City, dtype: object




```python
# Por padrão, as contagens de valores não retornarão a contagem de valores ausentes
unique_df.value_counts()
```




    saulo    2
    dri      1
    sil      1
    su       1
    dtype: int64




```python
# Por padrão, as contagens de valores não retornarão a contagem de valores ausentes
# escolhendo uma coluna
df['City'].value_counts()

```




    New York         1
    San Francisco    1
    Los Angeles      1
    Chicago          1
    Name: City, dtype: int64




```python
# Por padrão, as contagens de valores não retornarão a contagem de valores ausentes
# escolhendo uma coluna - do outro modo
df.City.value_counts()

```




    New York         1
    San Francisco    1
    Los Angeles      1
    Chicago          1
    Name: City, dtype: int64




```python
# use dropna = False, para também obter as contagens de valores ausentes junto com outros
df['City'].value_counts(dropna=False)
```




    New York         1
    San Francisco    1
    Los Angeles      1
    Chicago          1
    Name: City, dtype: int64




```python
# estatisticas básicas - média
df.Age.mean() # dataframe.column_name.mean()
```




    32.5




```python
# estatisticas básicas - mediana
df.Age.median() # dataframe.column_name.median()
```




    32.5




```python
# estatisticas básicas
df.Age.mode() # dataframe.column_name.mode()
```




    0    25
    1    30
    2    35
    3    40
    dtype: int64




```python
# estatisticas básicas
df.Age.std() # dataframe.column_name.mode()
```




    6.454972243679028



## 3. Seleção e indexação de dados

A seleção e indexação de dados são operações fundamentais no Pandas, permitindo extrair subconjuntos específicos de dados de um DataFrame.

#### 3.1. Selecionando Colunas e Linhas

 Você pode selecionar colunas e linhas específicas de um DataFrame usando colchetes ****[]****, ****.loc[]****, and ****.iloc[]****[]:

 - ****Colchetes []****: Seleciona uma ou mais colunas por seus nomes, você pode usar colchetes com os nomes das colunas como uma lista. indexing methods:



```python
# select_columns = df[['coluna1', 'coluna 2']]

df[['Name', 'Age']]

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>



- ****.loc[]****: Faz uma seleção baseada em rótulo: O indexador ****.loc[]**** permite selecionar linhas e colunas por rótulo. Você pode especificar rótulos de linha e coluna.


```python
# selected_data = df.loc[3:6, ['Column1', 'Column2']]

df.loc[2:3,['Name', "Age"]]

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>



- ****.iloc[]****: Realiza uma seleção baseada em número inteiro: O indexador ****.iloc[]**** permite selecionar linhas e colunas por localização de número inteiro, o que é útil para indexação numérica.


```python
# selected_data = df.iloc[1:4, 0:2]
df.iloc[2:4, 0:2]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>



#### 3.2. Filtragem/Seleção Condicional

A seleção condicional permite filtrar linhas com base em critérios específicos.

Você pode usar a indexação booleana (verdadeiro [TRUE] ou falso [FALSE]) para fazer isso.

Quando você passa uma lista de booleanos ( length = length of samples/rows ) para um quadro de dados, o quadro de dados seleciona as linhas específicas onde o índice da lista booleana é True.

- ****Boolean Indexing****: Crie uma máscara booleana aplicando uma condição a uma coluna e, em seguida, use essa máscara para filtrar linhas para a Condição Verdadeira.


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>




```python
boolean_mask = df['Age'] > 30 # Mascara com a condição idade > 30
filtered_data = df[boolean_mask] # Aplica a mascara no df (repare que retorna o que é true)

filtered_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>



- ****Multiple Conditions****: Combine várias condições usando operadores lógicos (**&** para **AND**, **|** para **OR**) e use parênteses para maior clareza.

Também é possivel usar .isin() um método do pandas para verificar se um valor de uma lista de coisas atende um critério.


```python
# Visualizado o df
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>




```python
boolean_mask = (df['Age'] > 25) & (df['City'] == 'Chicago')
filtered_data = df[boolean_mask]
filtered_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>David</td>
      <td>40</td>
      <td>Chicago</td>
    </tr>
  </tbody>
</table>
</div>




```python
boolean_mask = (df['Age'] >= 25) & (df['Age'] <= 35)
filtered_data = df[boolean_mask]
filtered_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
      <td>New York</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
      <td>San Francisco</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
      <td>Los Angeles</td>
    </tr>
  </tbody>
</table>
</div>




```python
city_ny_la = filtered_data.City.isin(['New York','Los Angeles'])
city_ny_la
```




    0     True
    1    False
    2     True
    Name: City, dtype: bool



#### 3.3. Filtragem/Seleção Condicional

O Pandas fornece vários métodos para personalizar e redefinir o índice do DataFrame.

- ****set_index()****: Este método permite definir uma ou mais colunas como índice do DataFrame. É útil quando você deseja realizar operações em uma coluna específica.

Para salvá-lo, temos que modificar o dataframe existente com o atualizado. Ou se você deseja salvá-lo diretamente, você pode usar o parâmetro inplace=True


```python
# Ambos salvarão os dados após a modificação

# df = df.set_index('ID') 
# df.set_index('ID',inplace=True)

```

- ****reset_index()****: O método reset_index() redefine o índice para o índice inteiro padrão e, opcionalmente, remove o índice existente.


```python
df = df.reset_index(drop=True) # nada acontece pq o df não tem uma coluna index
```

## Limpeza de dados

A limpeza de dados é uma etapa crítica no processo de preparação de dados. Envolve identificar e resolver problemas em seu conjunto de dados para garantir sua qualidade e confiabilidade.

- #### 4.2 Trabalhando com missing data

Dados faltates, ou missing data, é um problema comum em conjuntos de dados do mundo real.

A biblioteca Pandas oferece métodos para lidar com valores ausentes de maneira eficaz.

- ****.isna()and .notna()****: Esses métodos permitem identificar valores ausentes (NaN) e não ausentes, respectivamente, em seu DataFrame.

Aplicar este método para uma coluna retornará a lista booleana com True para os índices onde há um valor ausente. Sendo assim, passar essa lista para um dataframe retornará as linhas onde os valores da coluna são nulos.



```python
missing_data = df[df['Column'].isna()]

# Para obter a soma dos valores nulos em uma coluna
df.Column.isna().sum()

# Para obter a soma dos valores nulos para cada coluna
df.isna().sum()
```

- ****.fillna()****: Você pode substituir valores ausentes por um valor especificado ou calculado usando o método .fillna().

O exemplo abaixo substitui todos os valores nulos por zeros e modifica diretamente os dados conforme usamos em place = True.


```python
# especifique o valor pelo qual você deseja preencher o valor ausente
# No exemplo abaixo estamos substituindo o valor ausente por zero.
df['Column'].fillna(value=0, inplace=True)

# Se você deseja preencher os dados faltantes com a média da coluna numérica
df['Column'].fillna(value=df['Column'].mean(), inplace=True)

# Se você deseja preencher os dados faltantes com a mediana da coluna numérica
df['Column'].fillna(value=df['Column'].median(), inplace=True)

# Se você deseja preencher os dados faltantes com a moda da coluna numérica
df['Column'].fillna(value=df['Column'].mode(), inplace=True)
```

- ****.dropna()****: Remove as linhas ou colunas que contêm valores ausentes.

Por padrão, essa função removerá as linhas (axis = 0) onde qualquer um dos valores da coluna está faltando ( how = ‘any’ ).


```python
# Default axis = 0, how= 'any'. Elimina todas as linhas de qualquer coluna
df.dropna()

# Se você quiser que seja verificado apenas para determinadas colunas, use subset.
# Elimina as linhas onde qualquer valor da coluna1 ou coluna2 está faltando.
df.dropna(subset=['Column1', 'Column 2'], how = 'any', inplace=True)

# Elimina a coluna, se algum valor da coluna estiver faltando, não recomendado.
df.dropna(axis=1)
```

#### 4.2 Removendo dados duplicados

Linhas duplicadas podem distorcer os resultados da sua análise.

com o Pandas é possível remover duplicatas de modo simples.

- ****.duplicated()****: Este método identifica linhas duplicadas em um DataFrame.


```python
# Resultados as colunas duplicadas
# quando existe qualquer outra linha com correspondência exata de todas as colunas.
duplicates = df[df.duplicated()]

# Resultados as colunas duplicadas
# quando há uma correspondência entre as colunas especificadas
duplicates = df[df.duplicated(subset=['column1','column2'])]
```

- ****.drop_duplicates()****: Use este método para remover linhas duplicadas do DataFrame.


```python
# Antes de eliminarmos as linhas duplicadas,verifique a contagem de linhas duplicadas.
df.duplicated(subset=['column1','column2']).sum()

# Elimine as linhas duplicadas, a linha abaixo apenas mostrará os dados após a eliminação
df.drop_duplicates()

# É aconselhável verificar a forma após eliminar os missing antes de salvá-la
df.drop_duplicates().shape

# Se estiver satisfeito com a forma resultante, você pode salvá-la.
df.drop_duplicates(inplace=True)
```

#### 4.3 Conversão do tipo de dado


Os tipos de dados corretos são cruciais para a análise de dados. Pandas fornece métodos para converter tipos de dados conforme necessário.

- ****.astype()****:Você pode alterar o tipo de dados de uma coluna específica usando o método .astype(). 

Considere um caso em que item_price é salvo no tipo de dados do objeto, então você teria que alterá-lo para flutuante.


```python
# Para ver os tipos de dados de todas as colunas
df.dtypes

# Para alterar o tipo de dados de uma coluna
df['Column'] = df['Column'].astype('float')

# Convertendo colunas/séries com 'Masculino' para 1
df.Sex = pd.Series(df.Sex == 'Male').astype('int')
```

#### 4.4 String Operations

Ao trabalhar com dados de texto, o Pandas oferece operações de string por meio de .str uma via de acesso para aplicar a toda a coluna que é do tipo de dados de objeto.

- ****.str.lower() e .str.upper()****: Esses métodos convertem strings em minúsculas ou maiúsculas para todos os valores da coluna.

- ****.str.replace()****: Use este método para substituir substrings dentro de strings.

- ****.str.Contains()****: Este método permite verificar se existe uma substring ou padrão específico em uma string. Ele retorna uma série booleana indicando se cada elemento contém o padrão especificado.

- ****.str.slice()****: Você pode extrair uma substring de cada string em uma série usando o método .str.slice(). Especifique as posições inicial e final para definir a fatia.


```python
# Converte todos os valores da coluna do nome para letras minúsculas
df['Name'] = df['Name'].str.lower()

# Converte todos os valores da coluna do nome para letras maiúsculas
df['Name'] = df['Name'].str.upper()

# Encontrando um valor na coluna
contains_pattern = df['Text'].str.contains('keyword')
filtered_data = df[contains_pattern]

# Fatia de string
df['Substring'] = df['Text'].str.slice(start=2, stop=5) 

# String Replace, digamos que você deseja converter o objeto $ 5,4 em flutuante
df.price.str.replace('$','').astype('float')

# Usando operações String e astype
df.item_name.str.contains('chicken').astype('int')
```

## Manipulação de dados

A manipulação de dados é uma tarefa crucial na análise de dados e envolve transformar e modificar seus dados para obter insights ou prepará-los para análises posteriores. 

O Pandas fornece um rico conjunto de métodos para manipulação de dados que permitem moldar seus dados para atender às suas necessidades específicas.


#### 5.1 Aplicando Funções a DataFrames

Existe uma variedade de operações elementares que podem ser aplicadas a um dataframe usando python .iterrows().

No entanto, é importante observar que o Pandas é otimizado para operações vetorizadas, e iterar por meio de linha por linha de um DataFrame geralmente não é a maneira mais eficiente de trabalhar com dados no Pandas. 

Para essas tarefas, é recomendado usar operações vetorizadas sempre que possível.


```python
import pandas as pd

# Criar um df
data = {'Name': ['Alice', 'Bob', 'Charlie'],
        'Age': [25, 30, 35]}

df = pd.DataFrame(data)

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alice</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bob</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Charlie</td>
      <td>35</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Iterarar com indice e linha
for index, row in df.iterrows():
    print(f"Index: {index}, Name: {row['Name']}, Age: {row['Age']}")
```

    Index: 0, Name: Alice, Age: 25
    Index: 1, Name: Bob, Age: 30
    Index: 2, Name: Charlie, Age: 35
    

- ****.apply()****: Use este método para aplicar uma função personalizada a uma série ou a todo o dataframe.

  - quando você usa isso em série, cada elemento da coluna original será passado para a função.
  
  - quando você usa isso para todo o dataframe, com base no eixo (1 linha, 0 coluna), a linha inteira ou 
a coluna inteira será passada para a função.


```python
# Aplicando uma função personalizada a uma coluna
def square(x):
    return x ** 2 # pega o item e eleva ao 2

# Isso criará uma nova coluna com o nome - "Squared_Column"
df['Squared_Column'] = df['Original_Column'].apply(square)
```


```python
# Exemplo DataFrame
data = {'A': [1, 2, 3], 'B': [4, 5, 6]}
df = pd.DataFrame(data)

# função para calcular a média de uma linha
def average_row(row):
  return row.mean()

# Aplique a função linha a linha (eixo=0). Para colunas, use (eixo = 1)
df['Row_Average'] = df.apply(average_row, axis=1)

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>Row_Average</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5</td>
      <td>3.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>6</td>
      <td>4.5</td>
    </tr>
  </tbody>
</table>
</div>



- ****.map()****: Este método aplica uma função a cada elemento de uma série. É particularmente útil para transformar uma coluna com base nos valores de outra.


```python
# Mapeando valores em uma coluna com base em um dicionário
mapping_dict = {'A': 1, 'B': 2, 'C': 3}
df['New_Column'] = df['Old_Column'].map(mapping_dict)
```

- ****.applymap()****: Quando quiser aplicar uma função a cada elemento em todo o DataFrame, você pode usar .applymap().


```python
# exemplo
data = {'A': [1, 2, 3], 'B': [4, 5, 6]}
df = pd.DataFrame(data)

# function que adiciona 10 a um valor
def add_10(x):
    return x + 10

# Apply the function to the entire DataFrame
df = df.applymap(add_10)

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>



#### 5.2 Adicionando e removendo colunas

Você pode adicionar e remover colunas para personalizar seu DataFrame para análise:

  - ****Adicionando Colunas****: Para adicionar uma nova coluna ou substituir uma existente, basta atribuir valores a ela.

  - ****Removendo Colunas****: Use o método .drop() para remover colunas. Se deseja eliminar rótulos do índice (0 ou ‘índice’) ou colunas (1 ou ‘colunas’). Você pode usar axis=1/ ‘columns’ para eliminar a coluna ou usar axis =0/ ‘index’ para eliminar a linha.


```python
# Cria uma nova coluna com o nome New_Column
df['New_Column'] = [1, 2, 3, 4]

# Usando .drop() para remover colunas
df.drop(['Column1', 'Column2'], axis=1, inplace=True)
```

#### 5.3 Combinando DataFrames (Concatenation, Joining, Merging)

Pandas oferece métodos poderosos para combinar DataFrames:

- ****Concatenação****: Você pode concatenar DataFrames verticalmente ou horizontalmente usando pd.concat(). axis=0 irá concatená-los nas linhas, axis=1 irá concatená-los nas colunas. Ele verificará as colunas comuns entre os dataframes e as colunas correspondentes, concatenará nas linhas.


```python
import pandas as pd

# Exemplos de DataFrames com os mesmos nomes de coluna
data1 = {'A': [1, 2, 3], 'B': [4, 5, 6], 'C':[1,2,3]}
data2 = {'A': [7, 8, 9], 'B': [10, 11, 12], 'D':[1,2,3]}
df1 = pd.DataFrame(data1)
df2 = pd.DataFrame(data2)

# Concatena df1 e df2 horizontalmente (ao longo das colunas) com os mesmos nomes de colunas
result = pd.concat([df1, df2], axis=0)

# Exibe o DataFrame concatenado
print(result)

# Tip: Para tornar o índice adequado, você pode usar -> result.reset_index(drop=True)
```

       A   B    C    D
    0  1   4  1.0  NaN
    1  2   5  2.0  NaN
    2  3   6  3.0  NaN
    0  7  10  NaN  1.0
    1  8  11  NaN  2.0
    2  9  12  NaN  3.0
    

****Joining****: você pode realizar junções semelhantes a SQL em DataFrames usando o método .merge().

Merging: Pandas permite mesclar DataFrames com base em colunas comuns. Usando .merge(), você pode realizar várias junções amplamentes utilizadas na analise de dados como  inner, outer, left, and right joins.

  - O ***Inner Join*** é um formato comum de join que retorna dados apenas quando as duas tabelas têm chaves correspondentes na cláusula ON do join;

  - O ****Outer join****, também conhecido como FULL JOIN, retorna todos os registros de ambas as tabelas;

  - O ****Left Join**** retorna todos os registros da Tabela A e apenas os registros que coincidem com a igualdade do join na Tabela B (ou campos nulos para os campos sem correspondência);

  - O ****Right Join**** tem os mesmos efeitos que o Left Join, mas a tabela que retorna todos os registros é a Tabela B em vez da Tabela A.


```python
# Sample DataFrames
df1 = pd.DataFrame({'ID': [1, 2, 3], 'Name': ['Alice', 'Bob', 'Charlie']})
df2 = pd.DataFrame({'ID': [2, 3, 4], 'Age': [25, 30, 22]})

# Display the merged DataFrame
print("DataFrames")
print(df1)
print('-------------------')
print(df2)
print('-------------------')

# Inner join on 'ID'
result = pd.merge(df1, df2, on='ID', how='inner')

# Display the merged DataFrame
print("Inner Join - ON - ID")
print(result)
print('-------------------')

# Left join on 'ID'
result = pd.merge(df1, df2, on='ID', how='left')

# Display the merged DataFrame
print("Left Join - ON - ID")
print(result)
print('-------------------')

# If matching column names are different from both data frames
# you can specify them manually
# Considering, left table has ID1 and right table has ID2
pd.merge(df1,df2, left_on="ID1", right_on="ID2")

# Here it will try to match the left dataframe index with right ID column
pd.merge(df1,df2, left_index=True,right_on="ID")
```

    DataFrames
       ID     Name
    0   1    Alice
    1   2      Bob
    2   3  Charlie
    -------------------
       ID  Age
    0   2   25
    1   3   30
    2   4   22
    -------------------
    Inner Join - ON - ID
       ID     Name  Age
    0   2      Bob   25
    1   3  Charlie   30
    -------------------
    Left Join - ON - ID
       ID     Name   Age
    0   1    Alice   NaN
    1   2      Bob  25.0
    2   3  Charlie  30.0
    -------------------
    


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    ~\AppData\Local\Temp/ipykernel_11772/2950011593.py in <module>
         29 # you can specify them manually
         30 # Considering, left table has ID1 and right table has ID2
    ---> 31 pd.merge(df1,df2, left_on="ID1", right_on="ID2")
         32 
         33 # Here it will try to match the left dataframe index with right ID column
    

    c:\Users\saulo\anaconda3\lib\site-packages\pandas\core\reshape\merge.py in merge(left, right, how, on, left_on, right_on, left_index, right_index, sort, suffixes, copy, indicator, validate)
        104     validate: str | None = None,
        105 ) -> DataFrame:
    --> 106     op = _MergeOperation(
        107         left,
        108         right,
    

    c:\Users\saulo\anaconda3\lib\site-packages\pandas\core\reshape\merge.py in __init__(self, left, right, how, on, left_on, right_on, axis, left_index, right_index, sort, suffixes, copy, indicator, validate)
        697             self.right_join_keys,
        698             self.join_names,
    --> 699         ) = self._get_merge_keys()
        700 
        701         # validate the merge keys dtypes. We may need to coerce
    

    c:\Users\saulo\anaconda3\lib\site-packages\pandas\core\reshape\merge.py in _get_merge_keys(self)
       1094                     if not is_rkey(rk):
       1095                         if rk is not None:
    -> 1096                             right_keys.append(right._get_label_or_level_values(rk))
       1097                         else:
       1098                             # work-around for merge_asof(right_index=True)
    

    c:\Users\saulo\anaconda3\lib\site-packages\pandas\core\generic.py in _get_label_or_level_values(self, key, axis)
       1777             values = self.axes[axis].get_level_values(key)._values
       1778         else:
    -> 1779             raise KeyError(key)
       1780 
       1781         # Check for duplicates
    

    KeyError: 'ID2'


## Referencias 

- [Documentação oficial do Pandas](pandas.pydata.org);

- [Pandas Demystified: A Comprehensive Handbook for Data Enthusiasts](https://medium.com/python-in-plain-english/pandas-demystified-a-comprehensive-handbook-for-data-enthusiasts-part-1-136127e407f);
