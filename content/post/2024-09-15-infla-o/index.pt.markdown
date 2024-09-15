---
title: Inflação acumulada no Brasil
author: admin
date: '2024-09-15'
slug: inflação
categories: []
tags: 
  - Brasil
  - rstudio
  - Inflação
subtitle: 'de janeiro a agosto de 2024'
summary: 'No post de hoje iremos fazer um gráfico em linha contendo os dados da inflaçã acumulado no Brasil no perído de janeiro a agosto de 2024.'
authors: [admin]
lastmod: '2024-09-15T12:14:27-03:00'
featured: no
image:
  caption: 'Image credit: [**Freepick**]'
  focal_point: ''
  preview_only: no
projects: [Rstudio]
---

# **Introdução**

No post de hoje iremos fazer um gráfico em linha contendo os dados da inflação acumulado no Brasil no perído de janeiro a agosto de 2024. O gráfico será criado usando o pacote ggplot2, e utilizaremos os dados do SIDRA para obter tais informações. Acompanhe abaixo o passo a passo.

## **Instalando e carregando pacotes necessários**

Primeiro, você deverá instalar e carregar os pacotes ***sidrar***, ***ggplot2***, e ***ggrepel***. Se ainda não os tiver instalado, execute o seguinte código sem o "\#":


``` r
#install.packages("sidrar")
#install.packages("ggplot2")
#install.packages("ggrepel")

library(sidrar) 
library(ggplot2) 
library(ggrepel)
```

## **Obtendo os dados da inflação**

Iremos buscar os dados mensais do IPCA (Índice Nacional de Preços ao Consumidor Amplo) para o ano de 2024 usando a API da SIDRA.


``` r
# Consulta a série histórica do IPCA para 2024

ipca_2024 <- get_sidra(api= "/t/1737/n1/all/v/2265/p/last%208/d/v2265%202")    
```

## **Processando os dados**

Iremos converter os dados para um formato apropriado e calcular a inflação acumulada.


``` r
#Converteremos os dados para um data.frame  

dados <- data.frame( Mes = ipca_2024$`Mês`, Inflacao = ipca_2024$Valor )  

#Calculando a inflação acumulada  

dados$InflacaoAcumulada <- cumsum(dados$Inflacao)
```

## **Criando o gráfico de linha**

Utilizaremos o ggplot2 para criar o gráfico de linha da inflação acumulada do ano de 2024. Lembrando que é de janeiro até agosto.


``` r
# Criando o gráfico 7

ggplot(dados, aes(x = Mes, y = Inflacao, group = 1)) +
  geom_line(color = "#f5c105", size = 1) +
  geom_point(color = "black", size = 2) +
  geom_text_repel(aes(label = Inflacao),
                  data = dados, size = 3) +
  labs(title = "Inflação Acumulada no Brasil em 2024",
       x = "Mês",
       y = "Inflação Acumulada (%)",
       caption = " Autor: AGUIRRE, Deninson | Fonte: SIDRA/IBGE (2024)",
       tag = "Figura 1") +
  theme_gray() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) +
  scale_x_discrete(limits = dados$Mes) # Esta linha de comando permite ordenar de forma correta os meses
```

<img src="{{< blogdown/postref >}}index.pt_files/figure-html/gráfico-1.png" width="672" />

# **Conclusão**

Por fim, pudemos fazer de forma simples e com alguns comandos um gráfico de linha nos mostrando a inflação acumulada no Brasil. Outros resultados você poderá obter através do site do [**SIDRA**](https://sidra.ibge.gov.br/home/pimpfrg/nordeste), seja a respeito da inflação (IPCA), ou outros dados como: Produção Agrícola, Abate, Censo, Contas Nacionais, dentre outros.
