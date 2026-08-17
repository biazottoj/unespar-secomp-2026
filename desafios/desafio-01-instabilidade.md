# Desafio 1 — Quais partes do projeto parecem mais instáveis?

## Contexto

A equipe responsável pelo projeto percebe que algumas partes do sistema parecem exigir manutenção constantemente. Antes de iniciar uma iniciativa de refatoração, os desenvolvedores querem identificar quais arquivos ou módulos concentram maior atividade de mudança ao longo do histórico recente.

Seu grupo foi encarregado de investigar o repositório e produzir evidências que ajudem a equipe a responder essa questão.

## Problema

Quais partes do projeto parecem apresentar maior instabilidade no período analisado?

## Objetivo

Usar o histórico Git para identificar arquivos ou diretórios que concentram mudanças frequentes e/ou grandes volumes de alteração.

## Perguntas de investigação

Seu grupo deve responder, no mínimo:

1. Quais arquivos foram modificados com maior frequência?
2. Quais arquivos apresentam maior churn?
3. Os arquivos que mudam com maior frequência são também os que possuem maior churn?
4. Quais arquivos ou módulos parecem merecer uma investigação mais detalhada?

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

Entretanto, cabe ao grupo definir quais medidas são mais adequadas para caracterizar "instabilidade".

## Visualizações

Produza pelo menos **duas visualizações** que ajudem a responder ao problema.

Exemplos de possibilidades:

- gráfico de barras;
- scatter plot;
- série temporal;
- comparação entre arquivos ou módulos.

## Entregáveis

Ao final, o grupo deve apresentar:

1. a pergunta de investigação refinada;
2. os dados coletados;
3. uma breve explicação de como os dados foram preparados;
4. pelo menos duas visualizações;
5. uma conclusão baseada nas evidências;
6. pelo menos duas limitações da análise.

## Atenção

Um arquivo que muda frequentemente não é necessariamente um arquivo ruim.

A análise deve distinguir entre:

- evidência observada;
- interpretação;
- conclusão.

Evite afirmar causalidade a partir de uma simples associação.

## Questão para reflexão

Se um arquivo aparece como altamente instável, que outras evidências seriam necessárias para decidir se ele realmente precisa ser refatorado?
