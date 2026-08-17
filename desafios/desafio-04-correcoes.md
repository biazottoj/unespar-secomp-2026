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

## Visualizações

Produza pelo menos **duas visualizações**.

Exemplos:

- ranking dos arquivos mais associados a correções;
- churn dos commits corretivos;
- distribuição temporal das correções.
