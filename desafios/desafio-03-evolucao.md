# Desafio 3 — Como a manutenção do projeto mudou ao longo do tempo?

## Contexto

A equipe quer entender se o projeto está se tornando mais estável ou se a atividade de manutenção está aumentando. Para isso, pretende analisar como o histórico de mudanças evoluiu ao longo do tempo.

Seu grupo deverá transformar o histórico Git em uma visão temporal do projeto.

## Problema

Como o volume e a natureza das mudanças evoluíram durante o período analisado?

## Objetivo

Investigar tendências temporais no histórico do projeto e identificar períodos de maior ou menor atividade de manutenção.

## Perguntas de investigação

Seu grupo deve responder, no mínimo:

1. Como o número de commits varia ao longo do tempo?
2. Como o churn varia ao longo do tempo?
3. Em quais períodos houve maior quantidade de arquivos modificados?
4. Existem picos ou mudanças de comportamento claramente visíveis?
5. O projeto parece estar se tornando mais ou menos ativo?

## Dados que podem ser necessários

Entre os dados potencialmente úteis estão:

- identificador do commit;
- data;
- arquivo;
- autor;
- linhas adicionadas;
- linhas removidas;
- mensagem do commit.

## Preparação dos dados

Será necessário transformar a data em algum tipo de período.

Por exemplo:

- semana;
- mês;
- trimestre.

A escolha da granularidade deve ser justificada.

## Possíveis métricas

Considere analisar:

- commits por período;
- churn por período;
- arquivos modificados por período;
- autores ativos por período;
- tamanho médio das mudanças.

## Visualizações

Produza pelo menos **duas visualizações temporais**.

Exemplos:

- gráfico de linhas;
- barras por período;
- comparação entre duas métricas.

## Extensão opcional

Se houver tempo, compare também as mensagens de commit entre dois períodos diferentes.

Por exemplo:

- primeira metade do histórico analisado;
- segunda metade do histórico analisado.

A pergunta pode ser:

> Os tipos de atividade parecem ter mudado ao longo do tempo?

## Entregáveis

Ao final, o grupo deve apresentar:

1. a pergunta de investigação refinada;
2. a unidade temporal escolhida;
3. os dados coletados;
4. as métricas utilizadas;
5. pelo menos duas visualizações;
6. uma interpretação dos principais períodos;
7. uma conclusão;
8. pelo menos duas limitações.

## Atenção

Um pico de commits não significa necessariamente um problema.

Ele pode estar associado, por exemplo, a:

- uma release;
- uma refatoração;
- uma nova funcionalidade;
- uma migração;
- atividades automatizadas.

## Questão para reflexão

Que informações adicionais seriam necessárias para explicar por que determinado período apresentou um pico de atividade?
