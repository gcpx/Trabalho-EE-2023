# Trabalho-EE-2023
##### Banco de dados df deve ser baixado no seguinte site: https://svs.aids.gov.br/daent/centrais-de-conteudos/dados-abertos/sinasc/

##### Setando o diretório !!!
getwd()
setwd("C:/Users/gabri/OneDrive/Área de Trabalho/Desktop/gabriel/R/DN22OPEN")

##### Instalando os pacotes que serão utilizados
install.packages("tidyverse")
install.packages("ggplot2")
install.packages("vcd")
install.packages("read.dbc")
install.packages(read.db)
install.packages("readxl")

library(foreign)
?read.dbf
library(readxl)
library(tidyverse)
library(ggplot2)
library(vcd)
library(read.dbc)
set.seed(1234)

##### Leitura do Arquivo do SINASC 2022
df = read.dbf(file = "DNOPEN22.dbf")

##### O Banco de dados COD_UF deve ser baixado no seguinte site - http://blog.mds.gov.br/redesuas/lista-de-municipios-brasileiros/
##### Leitura dos aqurivos com os códigos de munícipio e seus respectivos UF 
COD_UF <- read_excel("Lista-de-Municípios-com-IBGE-Brasil.xlsx")

library(dplyr)

# Converter a coluna CODMUNNASC para numérico
df$CODMUNNASC <- as.numeric(as.character(df$CODMUNNASC))

# Realizar o left join entre o DataFrame "df" e a tabela "COD_UF" usando a coluna "CODMUNNASC"
df_com_uf <- left_join(df, COD_UF, by = c("CODMUNNASC" = "IBGE"))

# Criar uma nova coluna de UF no DataFrame "df"
df$UF <- df_com_uf$UF
