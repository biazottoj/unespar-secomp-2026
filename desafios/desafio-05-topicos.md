# Desafio 5 — Quais tipos de trabalho dominam o projeto?

## Contexto

Um novo responsável pelo projeto deseja entender quais tipos de atividade aparecem com maior frequência no histórico recente.

Não existe uma categorização explícita dos commits em manutenção corretiva, documentação, testes, dependências, novas funcionalidades ou outras atividades.

Seu grupo deverá explorar as mensagens de commit para identificar temas recorrentes.

## Problema

Quais tipos de atividade de desenvolvimento e manutenção parecem dominar o histórico recente do projeto?

## Objetivo

Aplicar técnicas de análise textual e topic modelling às mensagens de commit para descobrir grupos de termos recorrentes e interpretá-los como possíveis tipos de atividade.

## Perguntas de investigação

Seu grupo deve responder, no mínimo:

1. Quais tópicos aparecem nas mensagens de commit?
2. Quais palavras caracterizam cada tópico?
3. Como cada tópico pode ser interpretado no contexto do projeto?
4. Quais tópicos parecem aparecer com maior frequência?
5. O que esses tópicos sugerem sobre os tipos de trabalho realizados no projeto?

## Dados que podem ser necessários

Entre os dados potencialmente úteis estão:

- identificador do commit;
- mensagem;
- data;
- autor.

Outros dados podem ser incorporados caso o grupo considere necessário.

## Preparação textual

Antes do topic modelling, considere:

- remover mensagens de merge;
- remover palavras muito comuns;
- remover termos raros;
- evitar mensagens duplicadas;
- verificar se existem mensagens vazias ou pouco informativas.

## Técnica sugerida

Uma possibilidade é usar:

1. TF-IDF;
2. NMF;
3. inspeção das palavras mais relevantes de cada tópico.

O número de tópicos deve ser escolhido e justificado pelo grupo.

## Interpretação

O algoritmo não atribui significado aos tópicos.

Por exemplo, um tópico contendo:

```text
docs, readme, example, documentation
```

poderia ser interpretado como:

```text
Documentação
```

Mas essa interpretação deve ser feita pelo grupo com base nos termos e no contexto.

## Análise adicional

Se possível, associe cada mensagem de commit ao tópico dominante e estime a frequência de cada tópico.

Isso permite responder:

> Quais tipos de atividade parecem mais recorrentes?

## Visualizações

Produza pelo menos **duas visualizações**.

Exemplos:

- frequência dos tópicos;
- principais palavras por tópico;
- distribuição dos tópicos ao longo do tempo.

## Entregáveis

Ao final, o grupo deve apresentar:

1. as etapas de preparação textual;
2. os parâmetros utilizados;
3. os tópicos encontrados;
4. um nome interpretativo para cada tópico;
5. pelo menos duas visualizações;
6. uma conclusão sobre os tipos de trabalho observados;
7. pelo menos duas limitações.

## Atenção

Topic modelling é uma técnica exploratória.

Os tópicos dependem de decisões como:

- pré-processamento;
- número de tópicos;
- tamanho do corpus;
- qualidade das mensagens.

Não trate os tópicos encontrados como categorias objetivas ou definitivas.

## Questão para reflexão

Como você avaliaria se os tópicos encontrados são realmente úteis e interpretáveis para uma equipe de desenvolvimento?
