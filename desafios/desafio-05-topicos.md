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
3. Quais tópicos parecem aparecer com maior frequência?

## Dados que podem ser necessários

Entre os dados potencialmente úteis estão:

- identificador do commit;
- mensagem;
- data;
- autor.

Outros dados podem ser incorporados caso o grupo considere necessário.

## Técnica sugerida

Uma possibilidade é usar:

1. TF-IDF;
2. NMF;
3. inspeção das palavras mais relevantes de cada tópico.

O número de tópicos deve ser escolhido e justificado pelo grupo.

## Visualizações

Produza pelo menos **duas visualizações**.

Exemplos:

- frequência dos tópicos;
- principais palavras por tópico;
- distribuição dos tópicos ao longo do tempo.