# Desafio 1 — Quais partes do projeto parecem mais instáveis?

## Contexto

A equipe responsável pelo projeto percebe que algumas partes do sistema parecem exigir manutenção constantemente. Antes de iniciar uma iniciativa de refatoração, os desenvolvedores querem identificar quais arquivos ou módulos concentram maior atividade de mudança ao longo do histórico recente.

Seu grupo foi encarregado de investigar o repositório e produzir evidências que ajudem a equipe a responder essa questão.

## Problema

Quais partes do projeto parecem apresentar maior instabilidade no período analisado?

## Objetivo

Usar o histórico Git para identificar arquivos ou diretórios que concentram mudanças frequentes e/ou grandes volumes de alteração.

## Perguntas de investigação

1. Quais arquivos foram modificados com maior frequência?
2. Quais arquivos apresentam maior churn?
3. Os arquivos que mudam com maior frequência são também os que possuem maior churn?

## Dados que podem ser necessários

Considere quais informações do repositório podem ajudar a responder às perguntas.

Entre os dados potencialmente úteis estão:

- identificador do commit;
- data do commit;
- arquivo modificado;
- linhas adicionadas;
- linhas removidas.

Você pode coletar outros dados caso considere necessário.

## Sugestão de análise

Você pode considerar medidas como:

- quantidade de modificações por arquivo;
- churn total;
- quantidade de períodos diferentes em que um arquivo foi alterado;
- agregação por diretório ou módulo.

## Visualizações

Produza pelo menos **duas visualizações** que ajudem a responder ao problema.

Exemplos de possibilidades:

- gráfico de barras;
- gráfoco de pizza;
- distribuicao de arquivos/churn
