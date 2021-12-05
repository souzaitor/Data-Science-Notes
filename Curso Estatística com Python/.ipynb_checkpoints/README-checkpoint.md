# Resumo Estatística
***

## Tabela de Conteúdo
***

- [Tipos de Dados](#tipos-de-dados)
  - [Variáveis Quantitativas](#variaveis-quantitativas)
  - [Variáveis Qualitativas](#variaveis-qualitativas)
- [Distribuição de Frequências](#distribuio-de-frequncias)
  - [Distribuição de Frequências para Variáveis Qualitativas](#distribuiçao-de-frequencias-para-variaveis-qualitativas)
  - [Distribuição de Frequências para Variáveis Quantitativas (Classes Personalizadas)](#distribuiçao-de-Frequencias-para-variveis-quantitativas-classes-personalizadas)
  - [Distribuição de Frequências para Variáveis Quantitativas (Classes de Amplitude fixa)](#distribuiçao-de-frequencias-para-variaveis-quantitativas-classes-de-amplitude-fixa)
  - [Histograma](#histograma)
- [Medidas de Tendência Central](#medidas-de-tendencia-central)
  - [Média Aritmética](#media-aritmtica)
  - [Mediana](#mediana)
  - [Moda](#moda)
- [Medidas Separatrizes](#medidas-separatrizes)
  - [Quartis, Decis e Percentis](#quartis-decis-e-percentis)
  - [Box-plot](#box-plot)
- [Medidas de Dispersão](#medidas-de-disperso)
  - [Desvio Médio Absoluto](#desvio-medio-absoluto)
  - [Variância](#variancia)
  - [Desvio Padrão](#desvio-padrao)
- [Distribuições de Probabilidade](#distribuiçoes-de-probabilidade)
  - [Distribuição Binomial](#distribuiçao-binomial)
  - [Distriubuição Poisson](#distriubuiçao-poisson)
  - [Distribuição Normal](#distribuiçao-normal)
- [Amostragem](#amostragem)
  - [Amostragem Aleatória Simples](#amostragem-aleatoria-simples)
- [Estimação](#estimaçao)
  - [Teorema do Limite Central](#teorema-do-limite-central)
  - [Níveis de Confiança e Significância](#niveis-de-confiança-e-significancia)
  - [Erro Inferencial](#erro-inferencial)
  - [Intervalos de Confiança](#intervalos-de-confiança)
- [Cálculo do Tamanho da Amostra](#calculo-do-tamanho-da-amostra)
  - [Variáveis Quantitativas e População Infinita](#variaveis-quantitativas-e-populaço-infinita)
  - [Variáveis Quantitativas e População Finita](#variaveis-quantitativas-e-populaço-finita)
  
## Tipos de Dados
***

### Variáveis Quantitativas
***
São representadas por meio de números resultantes de uma contagem ou mensuração. Elas podem ser de dois tipos:

#### Variáveis Quantitativas Discretas
Os valores representam um conjunto finito ou enumerável de números, e que resultam de uma contagem, por exemplo: Número de filhos (0,1,2,…), número de bactérias por amostra, número de copos de cerveja tomados por dia.

#### Variáveis Quantitativas Contínuas
Os valores pertencem a um intervalo de números reais e representam uma mensuração como por exemplo altura ou peso de uma pessoa. Nesses casos números fracionais fazem sentido. Exemplo: tempo (relógio) e pressão arterial.

### Variáveis Qualitativas
***
Representam uma qualidade (ou atributo) de um indivíduo pesquisado, são definidas por várias categorias. São características que não possuem valores quantitativos. Essas variáveis podem ser de dois tipos:

#### Variável Qualitativa Nominal
Quando não existe nenhuma ordenação nas possíveis representações. Exemplos: sexo, cor dos olhos, cor do cabelo, fumante/não fumante.

#### Variável Qualitativa Ordinal
Quando apresentam uma ordem nos seus resultados. Exemplos: escolaridade (1, 2, 3 graus), mês de observação (janeiro, fevereiro, …, dezembro.)

## Distribuição de Frequências
***


### Distribuição de Frequências para Variáveis Qualitativas
***
```python
import pandas as pd

frequencia = dados['Nome_da_Variável'].value_counts()
percentual = dados['Nome_da_Variável'].value_counts(normalize = True) * 100

dist_freq_qualitativas = pd.DataFrame({'Frequência': frequencia, 'Porcentagem (%)': percentual})
```

### Distribuição de Frequências para Variáveis Quantitativas (Classes Personalizadas)
***

#### Especificar os Limites de cada Classe
```python
import pandas as pd

classes = [0, 1576, 3152, 7880, 15760, 200000]
labels = ['E', 'D', 'C', 'B', 'A']
```

#### Criando a Tabela de Frequências

```python
frequencia = pd.value_counts(
  pd.cut(x = dados.Renda,
         bins = classes,
         labels = labels,
         include_lowest = True)
)

percentual = pd.value_counts(
  pd.cut(x = dados.Renda,
         bins = classes,
         labels = labels,
         include_lowest = True),
  normalize = True
)

dist_freq_quantitativas_personalizadas = pd.DataFrame(
    {'Frequência': frequencia, 'Porcentagem (%)': percentual}
)
```

### Distribuição de Frequências para Variáveis Quantitativas (Classes de Amplitude fixa)
***

#### Definindo Número de Classes

Regra de Sturges
$$k = 1 + \frac {10}{3}\log_{10}n$$

```python
import pandas as pd
import numpy as np

k = 1 + (10 /3) * np.log10(df.shape[0])
k = int(k.round(0))
```
#### Criando a Tabela de Frequências

```python
frequencia = pd.value_counts(
  pd.cut(
    x = df.Nome_da_Variável,
    bins = k,
    include_lowest = True
  ),
  sort = False
)

percentual = pd.value_counts(
  pd.cut(
    x = df.Nome_da_Variável,
    bins = k,
    include_lowest = True
  ),
  sort = False,
  normalize = True
)

dist_freq_quantitativas_amplitude_fixa = pd.DataFrame(
    {'Frequência': frequencia, 'Porcentagem (%)': percentual}
)
```

### Histograma
***

O <b>HISTOGRAMA</b> é a representação gráfica de uma distribuição de frequências. É um gráfico formado por um conjunto de retângulos colocados lado a lado, onde a área de cada retângulo é proporcional à frequência da classe que ele representa.

#### Plotando um Histograma

```python
ax = sns.distplot(df.Nome_da_Variável, kde = False)

ax.figure.set_size_inches(12, 6)
ax.set_title('Distribuição de Frequências - Nome_da_Variável', fontsize=18)
ax.set_xlabel('Unidade da Variável', fontsize=14)
ax
```

#### Plotando um Histograma 

```python
df.Nome_da_Variável.hist(bins = 50, figsize=(12, 6))
```

##  Medidas de Tendência Central
***

### Média Aritmética
***
É representada por $\mu$ quando se refere à população e por $\bar{X}$ quando se refere à amostra

$$\mu = \frac 1n\sum_{i=1}^{n}X_i$$ 

onde:
* $n$ = número de observações (registros)
* $X_i$ = valor da i-ésima observação (registro)

#### Calculando a Média Aritmética
```python
import pandas as pd
df.mean()
```

### Mediana
***

Para obtermos a mediana de uma conjunto de dados devemos proceder da seguinte maneira:
1. Ordenar o conjunto de dados;
2. Identificar o número de observações (registros) do conjunto de dados ($n$);
3. Identicar o elemento mediano:

> Quando $n$ for ímpar, a posição do elemento mediano será obtida da seguinte forma:

$$Elemento_{Md} = \frac{n+1}2$$

> Quando $n$ for par, a posição do elemento mediano será obtida da seguinte forma:

$$Elemento_{Md} = \frac{n}2$$

#### Obtendo a Mediana:

> Quando $n$ for ímpar:
$$Md = X_{Elemento_{Md}}$$

> Quando $n$ for par:
$$Md = \frac{X_{Elemento_{Md}} + X_{Elemento_{Md}+1}}2$$

#### Calculando a Mediana
```python
import pandas as pd
df.quantile()
# ou
df.median()
```
### Moda
***
Pode-se definir a moda como sendo o valor mais frequente de um conjunto de dados. A moda é bastante utilizada para dados qualitativos.

#### Calculando a Moda
```python
import pandas as pd
df.mode()
```

## Medidas Separatrizes
***

### Quartis, Decis e Percentis
***
Há uma série de medidas de posição semelhantes na sua concepção à mediana, embora não sejam medidas de tendência central. Como se sabe, a mediana divide a distribuição em duas partes iguais quanto ao número de elementos de cada parte. Já os quartis permitem dividir a distribuição em quatro partes iguais quanto ao número de elementos de cada uma; os decis em dez partes e os centis em cem partes iguais.

#### Calculando os Quartis
```python
import pandas as pd
# Return values at the given quantile over requested axis
df.quantile([0.25, 0.5, 0.75])
```

#### Calculando os Decis
```python
import pandas as pd
# Return values at the given quantile over requested axis
df.quantile([i / 10 for i in range(1, 10)])
```

#### Calculando os Percentis
```python
import pandas as pd
# Return values at the given quantile over requested axis
df.quantile([i / 10 for i in range(1, 100)])
```

### Box-plot
***

O box plot dá uma idéia da posição, dispersão, assimetria, caudas e dados discrepantes (outliers). A posição central é dada pela mediana e a dispersão por $IIQ$. As posições relativas de $Q1$, $Mediana$ e $Q3$ dão uma noção da simetria da distribuição. Os comprimentos das cauda são dados pelas linhas que vão do retângulo aos valores remotos e pelos valores atípicos.

<img src='https://caelum-online-public.s3.amazonaws.com/1177-estatistica-parte1/01/img005.png' width='65%' align='center'>

#### Plotando um Boxplot
```python
import pandas as pd
import seaborn as sns

# x, y: names of variables in data or vector data, Inputs for plotting long-form data.

# data: Dataset for plotting. If x and y are absent, this is interpreted as wide-form. Otherwise it is expected to be long-form.

# orient “v” | “h” (optional): Orientation of the plot (vertical or horizontal)

ax = sns.boxplot(x = 'Variável no eixo Horizantal', y = 'Variável no eixo Vertical', data = df, orient = 'h')

ax.figure.set_size_inches(12, 4)
ax.set_title('Título', fontsize=18)
ax.set_xlabel('Legenda eixo X', fontsize=14)
ax
```
<img src='https://caelum-online-public.s3.amazonaws.com/1177-estatistica-parte1/01/img006.png' width='80%' align='center'>

## Medidas de Dispersão
***

Embora as medidas de posição forneçam uma sumarização bastante importante dos dados, elas podem não ser suficientes para caracterizar conjuntos distintos, especialmente quando as observações de determinada distribuição apresentarem dados muito dispersos.

### Desvio Médio Absoluto
***

$$DM = \frac 1n\sum_{i=1}^{n}|X_i-\bar{X}|$$


O desvio absoluto médio de um conjunto de dados é a média das distâncias entre cada dado e a média. Ele nos dá uma noção da variabilidade em um conjunto de dados

#### Calculando o Desvio Médio Absoluto
```python 
import pandas as pd
# mad() is mean absolute deviation function   
df.mad()    
```

### Variância
***

A variância é construída a partir das diferenças entre cada observação e a média dos dados, ou seja, o desvio em torno da média. No cálculo da variância, os desvios em torno da média são elevados ao quadrado.

#### Variância Populacional

$$\sigma^2 = \frac 1n\sum_{i=1}^{n}(X_i-\mu)^2$$

#### Variância Amostral

$$S^2 = \frac 1{n-1}\sum_{i=1}^{n}(X_i-\bar{X})^2$$

#### Calculando a Variância
```python
import pandas as pd
df.var()    
```

### Desvio Padrão
***
Uma das restrições da variância é o fato de fornecer medidas em quadrados das unidades originais - a variância de medidas de comprimento, por exemplo, é em unidades de área. Logo, o fato de as unidades serem diferentes dificulta a comparação da dispersão com as variáveis que a definem. Um modo de eliminar essa dificuldade é considerar sua raiz quadrada.

#### Desvio Padrão Populacional

$$\sigma = \sqrt{\frac 1n\sum_{i=1}^{n}(X_i-\mu)^2} \Longrightarrow \sigma = \sqrt{\sigma^2}$$

#### Desvio Padrão Amostral

$$S = \sqrt{\frac 1{n-1}\sum_{i=1}^{n}(X_i-\bar{X})^2} \Longrightarrow S = \sqrt{S^2}$$

#### Calculando o Desvio Padrão
```python
import pandas as pd
df.std()    
```

## Distribuições de Probabilidade
***

### Distribuição Binomial
***
Um evento **binomial** é caracterizado pela possibilidade de ocorrência de apenas duas categorias. Estas categorias somadas representam todo o espaço amostral, sendo também mutuamente excludentes, ou seja, a ocorrência de uma implica na não ocorrência da outra.

Em análises estatísticas o uso mais comum da distribuição binomial é na solução de problemas que envolvem situações de **sucesso** e **fracasso**.

$$P(k)=\binom{n}{k} p^k q^{n-k}$$

Onde:

* $p$ = probabilidade de sucesso
* $q = (1 - p)$ = probabilidade de fracasso
* $n$ = número de eventos estudados
* $k$ = número de eventos desejados que tenham sucesso

O valor esperado ou a média da distribuição binomial é igual ao número de experimentos realizados multiplicado pela chance de ocorrência do evento.

#### Média da Distribuição Binomial
$$\mu = n \times p$$

#### Desvio Padrão da Distribuição Binomial
O desvio padrão é o produto entre o número de experimentos, a probabilidade de sucesso e a probabilidade de fracasso.
$$\sigma = \sqrt{n \times p \times q}$$

#### Calculando a Distribuição Binomial
```python
from scipy.stats import binom

# binom.pmf: Probability Mass Function
# F(X) = P(X = k)
binom.pmf(5, n, p) + binom.pmf(6, n, p) + binom.pmf(7, n, p) + binom.pmf(8, n, p) + binom.pmf(9, n, p) + binom.pmf(10, n, p)

# binom.CDF: Cumulative Distribution Function
# F(X) = P(X <= k)
# 1 - binom.CDF: F(X) = P(X > k)
1 - binom.cdf(4, n, p)

# binom.sf: Survival Function 
# F(X) = P(X > k)
binom.sf(4, n, p)
```

### Distriubuição Poisson
***
É empregada para descrever o número de ocorrências em um intervalo de tempo ou espaço específico. Os eventos são caracterizados pela possibilidade de contagem dos sucessos, mas a não possibilidade de contagem dos fracassos.

Como exemplos de processos onde podemos aplicar a distribuição de Poisson temos a determinação do número de clientes que entram em uma loja em determinada hora, o número de carros que chegam em um drive-thru de uma lanchonete na hora do almoço, a determinação do número de acidentes registrados em um trecho de estrada etc.

$$P(k) = \frac{e^{-\mu}(\mu)^k}{k!}$$

Onde:
* $e$ = constante cujo valor aproximado é 2,718281828459045
* $\mu$ = representa o número médio de ocorrências em um determinado intervalo de tempo ou espaço
* $k$ = número de sucessos no intervalo desejado

#### Média da Distribuição Poisson
$$\mu$$

#### Desvio Padrão da Distribuição Poisson
$$\sigma = \sqrt{\mu}$$

#### Calculando a Distribuição Poisson
```python
from scipy.stats import poisson

probabilidade = poisson.pmf(k, media)
print('%0.8f' % probabilidade)
```

### Distribuição Normal
A distribuição normal é uma das mais utilizadas em estatística. É uma distribuição contínua, onde a distribuição de frequências de uma variável quantitativa apresenta a forma de sino e é simétrica em relação a sua média.

![Normal](https://caelum-online-public.s3.amazonaws.com/1178-estatistica-parte2/01/img001.png)

#### Características
1. É simétrica em torno da média;
2. A área sob a curva corresponde à proporção 1 ou 100%;
3. As medidas de tendência central (média, mediana e moda) apresentam o mesmo valor;
4. Os extremos da curva tendem ao infinito em ambas as direções e, teoricamente, jamais tocam o eixo $x$;
5. O desvio padrão define o achatamento e largura da distribuição. Curvas mais largas e mais achatadas apresentam valores maiores de desvio padrão;
6. A distribuição é definida por sua média e desvio padrão;
7. A probabilidade sempre será igual à área sob a curva, delimitada pelos limites inferior e superior.

$$f(x) = \frac{1}{\sqrt{2\pi\sigma}}e^{-\frac{1}{2}\left(\frac{x-\mu}{\sigma}\right)^2}$$

Onde:
* $x$ = variável normal
* $\sigma$ = desvio padrão
* $\mu$ = média


A probabilidade é obtida a partir da área sob a curva, delimitada pelos limites inferior e superior especificados. Um exemplo pode ser visto na figura abaixo.
![alt text](https://caelum-online-public.s3.amazonaws.com/1178-estatistica-parte2/01/img002.png)

#### Problema A - Identificação da área sob a curva
<img src='https://caelum-online-public.s3.amazonaws.com/1178-estatistica-parte2/01/img004.png' width='350px'>

```python
from scipy.stats import norm
Z = (1.8 - media) / desvio_padrao
probabilidade = norm.cdf(Z)
```

#### Problema B - Identificação da área sob a curva
<img src='https://caelum-online-public.s3.amazonaws.com/1178-estatistica-parte2/01/img005.png' width='350px'>

```python
from scipy.stats import norm

Z_inferior = (1.6 - media) / desvio_padrao
round(Z_inferior, 2)

Z_superior = (1.8 - media) / desvio_padrao
round(Z_superior, 2)

probabilidade = norm.cdf(Z_superior) - norm.cdf(Z_inferior)
```

#### Problema C - Identificação da área sob a curva
<img src='https://caelum-online-public.s3.amazonaws.com/1178-estatistica-parte2/01/img006.png' width='350px'>

```python
from scipy.stats import norm
Z = (1.9 - media) / desvio_padrao
probabilidade = 1 - norm.cdf(Z)
```

## Amostragem
***

### Amostragem Aleatória Simples
*** 

```python
# Return a random sample of items from an axis of object.

# nint, optional: Number of items from axis to return. Cannot be used with frac. Default = 1 if frac = None.
# random_state: seed

amostra = df.sample(n = 1000, random_state = 101)
```

## Estimação
***

### Teorema do Limite Central
***
> O **Teorema do Limite Central** afirma que, com o aumento do tamanho da amostra, a distribuição das médias amostrais se aproxima de uma distribuição normal com média igual à média da população e desvio padrão igual ao desvio padrão da variável original dividido pela raiz quadrada do tamanho da amostra. Este fato é assegurado para $n$ maior ou igual a 30.

$$\sigma_\bar{x} = \frac{\sigma}{\sqrt{n}}$$

O desvio padrão das médias amostrais é conhecido como **erro padrão da média**

> O Teorema do Limite Central afirma que, com o aumento do tamanho da amostra, a distribuição das médias amostrais se aproxima de uma distribuição normal com média igual à média da população e **desvio padrão igual ao desvio padrão da variável original dividido pela raiz quadrada do tamanho da amostra**. Este fato é assegurado para n maior ou igual a 30.

$$\sigma_\bar{x} = \frac{\sigma}{\sqrt{n}}$$

### Níveis de Confiança e Significância
***

O **nível de confiança** ($1 - \alpha$) representa a probabilidade de acerto da estimativa. De forma complementar o **nível de significância** ($\alpha$) expressa a probabilidade de erro da estimativa.

O **nível de confiança** representa o grau de confiabilidade do resultado da estimativa estar dentro de determinado intervalo. Quando fixamos em uma pesquisa um **nível de confiança** de 95%, por exemplo, estamos assumindo que existe uma probabilidade de 95% dos resultados da pesquisa representarem bem a realidade, ou seja, estarem corretos.

O **nível de confiança** de uma estimativa pode ser obtido a partir da área sob a curva normal como ilustrado na figura abaixo.

![alt text](https://caelum-online-public.s3.amazonaws.com/1178-estatistica-parte2/01/img007.png)

### Erro Inferencial
***
O **erro inferencial** é definido pelo **desvio padrão das médias amostrais** $\sigma_\bar{x}$ e pelo **nível de confiança** determinado para o processo.
$$e = z \frac{\sigma}{\sqrt{n}}$$

### Intervalos de Confiança
***

#### Com desvio padrão populacional conhecido

$$\mu = \bar{x} \pm z\frac{\sigma}{\sqrt{n}}$$

#### Com desvio padrão populacional desconhecido

$$\mu = \bar{x} \pm z\frac{s}{\sqrt{n}}$$

#### Valores de $z$ para os níveis de confiança mais utilizados

|Nível de<br>confiança|Valor da área sob<br>a curva normal| $z$ |
|:----------------:|:---------------------------------:|:---:|
|90%               |0,95                               |1,645|
|95%               |0,975                              |1,96 |
|99%               |0,995                              |2,575|

#### Obtendo sigma
```python
sigma = desvio_padrao / np.sqrt(n)
```

#### Obtendo 𝑒

```python
e = z * sigma
```

#### Calculando o intervalo de confiança para a média

```python
intervalo = (

  media_amostra - e,

  media_amostra + e  

)
#ou
norm.interval(alpha = 0.95, loc = media_amostra, scale = sigma)
```

## Cálculo do Tamanho da Amostra
***

### Variáveis Quantitativas e População Infinita
***
$$e = z \frac{\sigma}{\sqrt{n}}$$
#### Com desvio padrão conhecido
$$n = \left(z\frac{\sigma}{e}\right)^2$$

#### Com desvio padrão desconhecido
$$n = \left(z\frac{s}{e}\right)^2$$

Onde:
* $z$ = variável normal padronizada
* $\sigma$ = desvio padrão populacional
* $s$ = desvio padrão amostral
* $e$ = erro inferencial

#### Calculando o Tamanho da Amostra
```python
n = (z * (sigma / e)) ** 2
int(n.round())
```

### Variáveis Quantitativas e População Finita
***
#### Com desvio padrão conhecido
$$n = \frac{z^2 \sigma^2 N}{z^2 \sigma^2 + e^2(N-1)}$$

#### Com desvio padrão desconhecido
$$n = \frac{z^2 s^2 N}{z^2 s^2 + e^2(N-1)}$$

Onde:
* $N$ = tamanho da população
* $z$ = variável normal padronizada
* $\sigma$ = desvio padrão populacional
* $s$ = desvio padrão amostral
* $e$ = erro inferencial

#### Calculando o Tamanho da Amostra
```python
n = ((z**2) * (s**2) * (N)) / (((z**2) * (s**2)) + ((e**2) * (N - 1)))
int(n.round())
```