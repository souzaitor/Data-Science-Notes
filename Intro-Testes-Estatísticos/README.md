## Sumário

- [Gerar Histogramas de Maneira Cumulativa](#gerar-histogramas-de-maneira-cumulativa)
- [Teste Z](#teste-z)
- [Teste Z de uma amostra](#teste-z-de-uma-amostra)
- [Teste Z de Duas Amostras](#teste-z-de-duas-amostras)
- [Teste T](#teste-t)
- [Teste t de uma amostra](#teste-t-de-uma-amostra)
- [Teste t de duas amostras](#teste-t-de-duas-amostras)
- [Descobrir intervalo de confiança com `tconfint()`](#descobrir-intervalo-de-confian-a-com--tconfint---)
- [Teste Z em comparação com uma média](#teste-z-em-compara--o-com-uma-m-dia)
- [Comparação de Dois Conjuntos de Amostras com Teste Z](#compara--o-de-dois-conjuntos-de-amostras-com-teste-z)
- [Comparação de Dois Conjuntos de Amostras com Teste T](#compara--o-de-dois-conjuntos-de-amostras-com-teste-t)
- [Comparação de Dois Conjuntos de Amostras com DescrStatsW](#compara--o-de-dois-conjuntos-de-amostras-com-descrstatsw)
- [Utilizando o `normaltest`](#utilizando-o--normaltest-)
- [Utilizando o `ranksums`](#utilizando-o--ranksums-)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## Gerar Histogramas de Maneira Cumulativa

```python
ax = sns.distplot(daddos.medida, hist_kws = {'cumulative':True}, kde_kws = {'cumulative':True})
```

[Voltar ao Topo](#Sumário)

## Teste Z
* Teste Z é qualquer teste estatístico no qual a distribuição do teste estatístico sob a hipótese nula pode ser aproximada por uma distribuição normal
* É um teste estatístico usado para inferência (afirma a verdade de uma preposição em decorrência de sua ligação com outras já reconhecidas como verdadeiras), capaz de determinar se a diferença entre a média da amostra e da população é grande o suficiente para ser significativa estatisticamente.
* Esse teste é utilizado para amostras grande (>= 30)

[Voltar ao Topo](#Sumário)

## Teste Z de uma amostra

Realizamos o teste Z de uma amostra quando queremos comparar a média da amostra com a média da população.

* H0: μ=μ0
* Ha: μ≠μ0; μ<μ0; μ>μ0
* Estatística de Teste: Assuma que H0 é verdadeiro e veja se você tem dados / evidências suficientes para rejeitar
* Valor P: Probabilidade quando H0 é verdadeiro de obter uma estatística de teste tão extrema quanto você fez. Suponha que H0 seja verdadeiro até ser refutado.
* Valor p menor que alpha = rejeitar H0, há evidências suficientes para dizer que Ha é verdadeiro
* Valor p maior que alpha = falha em rejeitar H0. Não há evidências suficientes para dizer que Ha é verdadeiro.

[Voltar ao Topo](#Sumário)

## Teste Z de Duas Amostras

Realizamos um teste Z de duas amostras quando queremos comparar a média de duas amostras.

## Teste T

Os testes t são uma forma estatística de testar uma hipótese quando:

* Não sabemos a variância da população
* Nosso tamanho de amostra é pequeno, (n < 30)

[Voltar ao Topo](#Sumário)

## Teste t de uma amostra

Realizamos um teste t de uma amostra quando queremos comparar a média da amostra com a média da população. 

* H0: μ=μ0
* Ha: μ≠μ0; μ<μ0; μ>μ0
* Estatística de Teste: Assuma que H0 é verdadeiro e veja se você tem dados / evidências suficientes para rejeitar
* Valor P: Probabilidade quando H0 é verdadeiro de obter uma estatística de teste tão extrema quanto você fez. Suponha que H0 seja verdadeiro até ser refutado.
* Valor p menor que alpha = rejeitar H0, há evidências suficientes para dizer que Ha é verdadeiro
* Valor p maior que alpha = falha em rejeitar H0. Não há evidências suficientes para dizer que Ha é verdadeiro.

[Voltar ao Topo](#Sumário)

## Teste t de duas amostras

Realizamos um teste t de duas amostras quando queremos comparar a média de duas amostras.

## Descobrir intervalo de confiança com `tconfint()`

```python
from statsmodels.stats.weightstats import zconfint
# Aplicar teste Z (>= 30 amostras) para obter intervalo de confiança 
zconfint(dados.medida)
```

[Voltar ao Topo](#Sumário)

## Teste Z em comparação com uma média

```python
from statsmodels.stats.weightstats import ztest as ztest

ztest(dados.medida, value = média)
```

[Voltar ao Topo](#Sumário)

## Comparação de Dois Conjuntos de Amostras com Teste Z

```python
from statsmodels.stats.weightstats import ztest
from statsmodels.stats.weightstats import zconfint

print(ztest(dados1.medida, dados2.medida))
# Intervalo de confiança de quão diferente são as médias
zconfint(dados1.medida, dados2.medida)
```

[Voltar ao Topo](#Sumário)

## Comparação de Dois Conjuntos de Amostras com Teste T

```python
from scipy.stats import ttest_ind
# T teste
# Intervalo de confiança de quão diferente são as médias e pvalue
ttest_ind(dados1.medida, dados2.medida)
```

[Voltar ao Topo](#Sumário)

## Comparação de Dois Conjuntos de Amostras com DescrStatsW

```python
from statsmodels.stats.weightstats import DescrStatsW
# Comparação utilizando vários testes
descr_1 = DescrStatsW(dados1.medida)
descr_2 = DescrStatsW(dados2.medida)
comparacao = descr_1.get_compare(descr_2)

# Comparação usando Z test
comparacao.summary(use_t=False)

# Comparação usando T test
comparacao.summary(use_t=True)
```

[Voltar ao Topo](#Sumário)

## Utilizando o `normaltest`

```python
from scipy.stats import normaltest
# Se p <alfa: hipótese nula: x vem de uma distribuição normal
# Se p >alfa: A hipótese nula pode ser rejeitada
_, p = normaltest(dados1.medida)
p
```

[Voltar ao Topo](#Sumário)

## Utilizando o `ranksums`
É um teste não paramétrico: não assume que seus dados seguem uma distribuição normal

```python
from scipy.stats import ranksums
_, p = ranksums(dados1.medida, dados2.medida)
p
```

[Voltar ao Topo](#Sumário)

