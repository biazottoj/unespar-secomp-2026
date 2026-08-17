# Desafio 2 — Onde existe concentração de conhecimento?

## Contexto

A equipe está preocupada com a continuidade do projeto. Alguns componentes podem depender excessivamente de poucos desenvolvedores, tornando a manutenção mais arriscada caso essas pessoas deixem a equipe ou fiquem indisponíveis.

Seu grupo deverá investigar o histórico do repositório para identificar possíveis sinais de concentração de conhecimento.

## Problema

Quais arquivos ou módulos importantes parecem depender de poucos desenvolvedores?

## Objetivo

Analisar a relação entre arquivos, modificações e autores para identificar componentes com alta atividade de manutenção, mas baixa diversidade de contribuidores.

## Perguntas de investigação

Seu grupo deve responder, no mínimo:

1. Quantos desenvolvedores distintos modificaram cada arquivo?
2. Quais arquivos possuem grande volume de mudanças, mas poucos autores?
3. Existem arquivos importantes que parecem depender de apenas um ou dois desenvolvedores?
4. Quais componentes poderiam representar maior risco de continuidade?

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

Um arquivo alterado muitas vezes por apenas um ou dois desenvolvedores pode ser mais interessante do que um arquivo pouco alterado por um único desenvolvedor.

## Visualizações

Produza pelo menos **duas visualizações**.

Uma possibilidade interessante é relacionar:

- número de modificações;
- quantidade de autores.

Você também pode incorporar churn ou outra medida adicional.

## Entregáveis

Ao final, o grupo deve apresentar:

1. a pergunta de investigação refinada;
2. os dados coletados;
3. as métricas utilizadas;
4. pelo menos duas visualizações;
5. uma lista de componentes considerados mais críticos;
6. uma conclusão baseada nas evidências;
7. pelo menos duas limitações.

## Atenção

Não trate "número de autores" como uma medida completa de conhecimento.

O histórico Git mostra quem realizou commits, mas não necessariamente:

- quem revisou o código;
- quem participou da decisão;
- quem possui conhecimento informal;
- quem trabalhou em pares.

## Questão para reflexão

Quais outras fontes de dados poderiam ser combinadas ao Git para medir melhor a distribuição de conhecimento em uma equipe?
