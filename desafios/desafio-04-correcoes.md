# Desafio 4 — Onde estão concentradas as correções?

## Contexto

A equipe suspeita que alguns componentes do projeto aparecem repetidamente em atividades de correção. No entanto, não existe uma classificação formal dos commits como correção, funcionalidade, documentação ou outra categoria.

Seu grupo deverá usar as mensagens de commit como uma aproximação para identificar possíveis commits corretivos.

## Problema

Quais arquivos aparecem com maior frequência em commits que parecem estar relacionados a correções?

## Objetivo

Usar informações textuais das mensagens de commit para identificar um subconjunto de commits possivelmente corretivos e analisar quais arquivos aparecem com maior frequência nesse subconjunto.

## Perguntas de investigação

Seu grupo deve responder, no mínimo:

1. Como identificar commits potencialmente relacionados a correções?
2. Quantos commits do período analisado atendem aos critérios definidos?
3. Quais arquivos aparecem com maior frequência nesses commits?
4. Esses arquivos também estão entre os mais modificados do projeto?
5. Existem componentes que parecem concentrar atividades corretivas?

## Dados que podem ser necessários

Entre os dados potencialmente úteis estão:

- identificador do commit;
- mensagem;
- arquivo modificado;
- data;
- linhas adicionadas;
- linhas removidas.

## Definição do critério

O grupo deverá definir uma estratégia para reconhecer mensagens relacionadas a correções.

Por exemplo, podem ser explorados termos como:

- `fix`;
- `bug`;
- `error`;
- `crash`;
- `regression`.

Essa lista é apenas uma possibilidade. O grupo pode propor outra estratégia.

## Comparação importante

Não analise apenas os commits identificados como correções.

Compare também:

- arquivos mais modificados em geral;
- arquivos mais frequentes em possíveis correções.

Essa comparação pode revelar se atividade geral e atividade corretiva estão concentradas nos mesmos locais.

## Visualizações

Produza pelo menos **duas visualizações**.

Exemplos:

- ranking dos arquivos mais associados a correções;
- comparação entre frequência geral e frequência em correções;
- churn dos commits corretivos;
- distribuição temporal das correções.

## Entregáveis

Ao final, o grupo deve apresentar:

1. o critério utilizado para identificar possíveis correções;
2. os dados coletados;
3. a quantidade de commits identificados;
4. pelo menos duas visualizações;
5. os componentes considerados mais relevantes;
6. uma conclusão;
7. pelo menos duas limitações.

## Atenção

Uma mensagem contendo a palavra `fix` não prova que o commit corrige um defeito.

Da mesma forma, um commit corretivo pode não utilizar nenhuma das palavras selecionadas.

Portanto, sua classificação é um **proxy** e deve ser tratada como tal.

## Questão para reflexão

Como você validaria se o critério utilizado realmente identifica commits corretivos com precisão aceitável?
