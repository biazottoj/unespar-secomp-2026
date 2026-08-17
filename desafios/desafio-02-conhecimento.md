# Desafio 2 — Onde existe concentração de conhecimento?

## Contexto

A equipe está preocupada com a continuidade do projeto. Alguns componentes podem depender excessivamente de poucos desenvolvedores, tornando a manutenção mais arriscada caso essas pessoas deixem a equipe ou fiquem indisponíveis.

Seu grupo deverá investigar o histórico do repositório para identificar possíveis sinais de concentração de conhecimento.

## Problema

Quais arquivos ou módulos importantes parecem depender de poucos desenvolvedores?

## Objetivo

Analisar a relação entre arquivos, modificações e autores para identificar componentes com alta atividade de manutenção, mas baixa diversidade de contribuidores.

## Perguntas de investigação

1. Quantos desenvolvedores distintos modificaram cada arquivo?
2. Quais arquivos possuem grande volume de mudanças, mas poucos autores?

## Dados que podem ser necessários

Entre os dados potencialmente úteis estão:

- identificador do commit;
- autor;
- arquivo modificado;
- data;
- linhas adicionadas;
- linhas removidas.

Você pode coletar outras informações caso considere necessário.

## Sugestão de análise

Considere combinar diferentes dimensões.

Por exemplo:

- número de autores distintos por arquivo;
- número de modificações;
- churn;
- quantidade de commits.

## Visualizações

Produza pelo menos **duas visualizações**.

Uma possibilidade interessante é relacionar:

- número de modificações;
- quantidade de autores.

Você também pode incorporar churn ou outra medida adicional.