```bash
set -o allexport; source env/.env-mainnet; set +o allexport; docker exec -it graphprotocol-mainnet-docker_postgres_1 psql "-U" ${DB_USER} ${GRAPH_NODE_DB_NAME} "-c" "refresh materialized view info.subgraph_sizes;"
```
```bash
set -o allexport; source env/.env-testnet; set +o allexport; docker exec -it graphprotocol-testnet-docker_postgres_1 psql "-U" ${DB_USER} ${GRAPH_NODE_DB_NAME} "-c" "refresh materialized view info.subgraph_sizes;"
```
