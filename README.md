# Entendendo o Projeto

Olá, meu nome é Jefferson Kauan e neste documento, farei uma apresentação geral sobre este projeto.

Esse dataset se refere a candidatos de vários partidos brasileiros, seu genero, raça e cor. 

## Objetivo

O objetivo principal desse projeto é analisar as proporções de cor e genero e avaliar quais são os cargos mais comuns baseado nesses dados.

## Premissas

- A base de dados utilizada foi disponibilizada pelo *Kaggle.com*.
- Existia um valor discrepante em relação ao total de Bens do partido MDB. Ao identificar esse erro através de consultas sql, os valores discrepantes foram substituidos pela média geral

# Representação dos 5 partidos mais ricos e suas proporções.

| Partido       | TotalBens    | Taxa total de bens (%) | Total Pessoas em Geral | Total de Mulheres | % Mulheres sobre Total | Total Pessoas Pretas | % Pessoas Pretas | Total de Candidaturas | % Sobre Total de Candidaturas |
|---------------|--------------|-----------------------|------------------------|-------------------|------------------------|----------------------|------------------|-----------------------|--------------------|
| PL            | 9,92463E+12  | 1.76                  | 183,508                | 47,560            | 25.92                  | 10,836               | 5.90             | 142,960               | 7.79                           |
| UNIÃO         | 7,65857E+12  | 1.36                  | 220,424                | 49,104            | 22.28                  | 14,516               | 6.59             | 145,360               | 7.92                           |
| PSD           | 4,61275E+12  | 0.82                  | 229,012                | 51,436            | 22.46                  | 16,152               | 7.05             | 154,488               | 8.42                           |
| PP            | 3,99150E+11  | 0.07                  | 223,168                | 52,760            | 23.64                  | 14,784               | 6.62             | 158,384               | 8.63                           |
| Republicanos  | 3,97952E+11  | 0.07                  | 207,960                | 45,436            | 21.85                  | 14,812               | 7.12             | 134,964               | 7.35                           |

# Representação dos 5 partidos menos ricos e suas proporções
| Partido       | TotalBens    | Taxa total de bens (%) | Total Pessoas em Geral | Total de Mulheres | % Mulheres sobre Total | Total Pessoas Pretas | % Pessoas Pretas  | Total de Candidaturas | % Sobre Total de Candidaturas |
|---------------|--------------|-----------------------|------------------------|-------------------|------------------------|----------------------|-------------------|-----------------------|-------------------|
| UP            | 2,143,924,816| 0.00038               | 868                    | 232               | 26.73                  | 144                  | 16.59             | 440                   | 0.02                           |
| PCB           | 2,804,061,608| 0.00050               | 240                    | 44                | 18.33                  | 48                   | 20.00             | 140                   | 0.01                           |
| PCO           | 4,534,885,976| 0.00081               | 1,132                  | 240               | 21.20                  | 148                  | 13.07             | 688                   | 0.04                           |
| PSTU          | 7,383,123,976| 0.00131               | 1,168                  | 248               | 21.23                  | 196                  | 16.78             | 636                   | 0.03                           |
| PSOL          | 158,102,000,000| 0.02809             | 31,424                 | 6,348             | 20.20                  | 4,452                | 14.17             | 15,720                | 0.86                           |
