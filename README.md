# Entendendo o Projeto

Olá, meu nome é Jefferson Kauan e neste documento, farei uma apresentação geral sobre este projeto.

Esse dataset se refere a candidatos de vários partidos brasileiros, seu genero, raça e cor. 

## Objetivo

O objetivo principal desse projeto é fazer uma análise descritiva dos dados.

## Premissas

- A base de dados utilizada foi disponibilizada pelo *Kaggle.com*.
- Existia um valor discrepante em relação ao total de Bens do partido MDB. Ao identificar esse erro através de consultas sql, os valores discrepantes foram substituidos pela média geral

## Representação dos 5 partidos mais ricos e suas proporções.

| Partido       | TotalBens    | Taxa total de bens (%) | Total Pessoas em Geral | Total de Mulheres | % Mulheres sobre Total | Total Pessoas Pretas | % Pessoas Pretas | Total de Candidaturas | % Sobre Total de Candidaturas |
|---------------|--------------|-----------------------|------------------------|-------------------|------------------------|----------------------|------------------|-----------------------|--------------------|
| PL            | 9,92463E+12  | 1.76                  | 183,508                | 47,560            | 25.92                  | 10,836               | 5.90             | 142,960               | 7.79                           |
| UNIÃO         | 7,65857E+12  | 1.36                  | 220,424                | 49,104            | 22.28                  | 14,516               | 6.59             | 145,360               | 7.92                           |
| PSD           | 4,61275E+12  | 0.82                  | 229,012                | 51,436            | 22.46                  | 16,152               | 7.05             | 154,488               | 8.42                           |
| PP            | 3,99150E+11  | 0.07                  | 223,168                | 52,760            | 23.64                  | 14,784               | 6.62             | 158,384               | 8.63                           |
| Republicanos  | 3,97952E+11  | 0.07                  | 207,960                | 45,436            | 21.85                  | 14,812               | 7.12             | 134,964               | 7.35                           |

## Representação dos 5 partidos menos ricos e suas proporções
| Partido       | TotalBens    | Taxa total de bens (%) | Total Pessoas em Geral | Total de Mulheres | % Mulheres sobre Total | Total Pessoas Pretas | % Pessoas Pretas  | Total de Candidaturas | % Sobre Total de Candidaturas |
|---------------|--------------|-----------------------|------------------------|-------------------|------------------------|----------------------|-------------------|-----------------------|-------------------|
| UP            | 2,143,924,816| 0.00038               | 868                    | 232               | 26.73                  | 144                  | 16.59             | 440                   | 0.02                           |
| PCB           | 2,804,061,608| 0.00050               | 240                    | 44                | 18.33                  | 48                   | 20.00             | 140                   | 0.01                           |
| PCO           | 4,534,885,976| 0.00081               | 1,132                  | 240               | 21.20                  | 148                  | 13.07             | 688                   | 0.04                           |
| PSTU          | 7,383,123,976| 0.00131               | 1,168                  | 248               | 21.23                  | 196                  | 16.78             | 636                   | 0.03                           |
| PSOL          | 158,102,000,000| 0.02809             | 31,424                 | 6,348             | 20.20                  | 4,452                | 14.17             | 15,720                | 0.86                           |

## Conclusões a partir dessas tabelas
- Os partidos mais ricos representam 40.5% do total de candidaturas. Ou seja, a cada 5 candidatos, 2 são filiados aos partidos mais ricos
- A proporção de mulheres se mantém praticamente a mesma tanto nos mais ricos quanto nos menos ricos (20 - 25%). O que representa aproximadamente 1/4 do total de pessoas por partido
- De uma forma geral, os partidos mais ricos possuem um intervalo semelhante de pessoas pretas(5 - 7%). Já os partidos mais pobres possuem uma proporção praticamente duplicada de representantes pretos (13 - 20%)
- Isso significa que nos partidos mais pobres, mulheres e pessoas pretas representam aproximadamente 40% ou mais do total de pessoas. Enquanto nos partidos mais ricos isso representa aproximadamente 30%.

  ### Principais consultas SQL utilizadas
```sql
-- Consulta para retornar o somatório dos bens agrupado por partido
SELECT SUM(totalBens) AS totalBensPartido, SG_PARTIDO
FROM tse_analytics_partidos
GROUP BY SG_PARTIDO;
```
```sql
-- Consulta para retornar o somatório de mulheres por partido
SELECT SUM(totalGenFeminino) AS totalGenFeminino, SG_PARTIDO
FROM tse_analytics_partidos
GROUP BY SG_PARTIDO;
```
```sql
-- Consulta para calcular a quantidade de pessoas por partido
SELECT SG_PARTIDO,
    SUM(totalGenFeminino) AS totalGenFeminino,
    SUM(totalCorRacaPreta) AS totalCorRacaPreta,
    SUM(totalCorRacaPretaParda) AS totalCorRacaPretaParda,
    SUM(totalCorNaoBranca) AS totalCorNaoBranca
FROM tse_analytics_partidos
GROUP BY SG_PARTIDO;
```
```sql
-- Consulta para retornar o total de candidaturas por partido
SELECT sum(totalCandidaturas) AS somaTotal, SG_PARTIDO
FROM tse_analytics_partidos
GROUP BY SG_PARTIDO
ORDER BY somaTotal DESC;
```

## Análise exploratória
### Box Plot
* ### Box Plot total bens por partido
<div align = "center">
  
![image](https://github.com/user-attachments/assets/270954ba-8634-4100-bd21-809a05a3c108)

</div>

* Após a montagem de uma tabela com os 5 partidos mais ricos e os menos ricos( baseado na somatória de bens), montei o box plot acima para verificar se havia valores discrepantes. Como pode ser visto, não há outliers, a maioria dos partidos possuem sua renda variando em torno da mediana, existem partidos com rendas altas, porém se encontra dentro daquilo que é esperado.

### Box plot com total de candidaturas por partido
<div align = "center">
  
![image](https://github.com/user-attachments/assets/0d2e5d05-e5bf-47b0-bfec-140124a61c22)
  
</div>

* Após agrupar a quantidade de candidaturas por partido, esse box plot nos mostra que mediana de candidaturas está aproximadamente em 26 mil candidaturas e a média aproximadamente em 73 mil. Não há outliers nesse gráfico, porém, percebe-se que a média está sendo altamente influeciada pelos valores mais altos de candidaturas, como o mais alto(175 mil). A tabela abaixo que será mostrada, foi gerada a partir de um filtro do banco de dados mostrando os 5 maiores partidos em relação ao total de candidaturas.

<div align = "center">
  
| Partido | totalCandidaturas |
|---------|-------------------|
| MDB     | 176344            |
| PP      | 158384            |
| PSD     | 154488            |
| UNIÃO   | 145360            |
| PL      | 142960            |

</div>

* Vê-se, portanto que dos 5 partidos com maior quantidade de candidaturas, 4 estão entre os mais ricos, e com valores bem acima da média e da mediana

### Quantidade de candidaturas pelo total de bens
<div align = "center">

![image](https://github.com/user-attachments/assets/a153607a-42e7-4b5a-97e1-2e60971547db)
</div>

* Observa-se que essa gráfico de dispersão nos mostra que existe uma correlação positiva entre quantidade de candidaturas e total de bens, essa correlação foi calculada chegando a um valor de 0.83. O que significa uma forte correlação entre variáveis. Ou seja, quando o total de bens aumenta, a quantidade de candidaturas também tende a aumentar.


## Visualização Geral



<div align="center>

  
![image](https://github.com/user-attachments/assets/b508edee-e613-4155-95dd-c2fbf70c1ec3)
![image](https://github.com/user-attachments/assets/b508edee-e613-4155-95dd-c2fbf70c1ec3)



</div>

