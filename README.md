# connectors-demo

1. Environment

Create a `.env` in the project root with `APOLLO_KEY` and `APOLLO_GRAPH_REF`

2. Compose

```
rover supergraph compose --config rover.yml > ./router/supergraph.graphql
```

3. Start Router

```
docker-compose --env-file .env up
```

