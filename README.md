# Ambiente simplificado — Oficina de MSR

Este ambiente contém apenas:

- JupyterLab
- PyDriller
- pandas / numpy
- matplotlib / seaborn / plotly
- scikit-learn / NLTK / wordcloud para análise textual e topic modelling

## Estrutura

```text
msr-workshop-simplificado/
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── notebooks/
├── datasets/
└── repositories/
```

Crie as pastas, caso ainda não existam:

```bash
mkdir -p notebooks datasets repositories
```

## Subir o ambiente

```bash
docker compose up -d --build
```

Acesse:

```text
http://localhost:8888
```

Token padrão:

```text
msr-workshop
```

## Verificar

```bash
docker compose ps
```

## Ver logs

```bash
docker compose logs -f jupyter
```

## Parar

```bash
docker compose down
```

Os repositórios clonados em `/workspace/repositories` dentro do Jupyter ficam persistidos na pasta `repositories/` do host.
