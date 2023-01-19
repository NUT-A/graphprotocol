## Setup Poligon Archive Node
[StakeSquid](https://thegraphfoundation.notion.site/Polygon-Baremetal-Archive-Node-77a651bd46544df5b59ed49f17289f7e)

## Wipe Testnet
```bash
cd graphprotocol-testnet-docker
docker-compose -f compose-all-services.yml down -v
```

## Add Polygon Chain
[Supporting Multiple Chains](https://github.com/StakeSquid/graphprotocol-testnet-docker/blob/master/docs/getting-started.md#supporting-multiple-chains)

Pull updates
```bash
git submodule update --init --recursive
```

Add to `env/.env-testnet`
```
CHAIN_1_NAME="matic"
CHAIN_1_RPC="http://ip:port"
```

## Run without Autoagora
```bash
bash start
```
## Setup Allocations
1. Delete all Allocations ([discord](https://discord.com/channels/438038660412342282/807005869836861461/1065609092732825611))
```bash
cd graphprotocol-testnet-docker
docker-compose -f compose-indexer.yml exec cli bash

# this table will get you your current active allocations
graph indexer allocations get | grep Active

# Replace the subgraph IPFS hash and the allocation hash with your values
graph indexer actions queue unallocate {ipfs} {hash} 0x0 true

# it will list the queued actions
# you will see the manual ones there that you just queued
graph indexer actions get all

graph indexer actions approve {number of manual action}
graph indexer actions execute approved
```
2. Wait for epoch end
3. Setup new Allocations
```
cd graphprotocol-testnet-docker
docker-compose -f compose-indexer.yml exec cli bash

graph indexer rules set QmcWyUejpse9agsiB6xitDhZpyox4aqir4ARReJwUsTY45 decisionBasis always allocationAmount 50000

graph indexer rules set QmZ2egWxWWiEoxujgVVvqLyvh2yNG8Q8QyXvmoWYDiB4Ua decisionBasis always allocationAmount 50000

graph indexer rules set QmYe4UxoSPD71dfsgnD8d34M5t3YgswwLLeLRrNJ3v4hqA decisionBasis always allocationAmount 50000
```

## Fix Grafana
```bash
set -o allexport; source {{path_to_env_folder}}/.env-mainnet; set +o allexport; docker exec -it graphprotocol-mainnet-docker_postgres_1 psql "-U" ${DB_USER} ${GRAPH_NODE_DB_NAME} "-c" "refresh materialized view info.subgraph_sizes;"
```
```bash
set -o allexport; source {{path_to_env_folder}}/.env-testnet; set +o allexport; docker exec -it graphprotocol-testnet-docker_postgres_1 psql "-U" ${DB_USER} ${GRAPH_NODE_DB_NAME} "-c" "refresh materialized view info.subgraph_sizes;"
```
