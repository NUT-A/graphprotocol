Отправить эфир на оператора тестнета перед выполнением гайда

## Wipe Testnet
```bash
bash stop

cd graphprotocol-testnet-docker
docker-compose -f compose-all-services.yml down -v
```

## Add Celo Chain
[Supporting Multiple Chains](https://github.com/StakeSquid/graphprotocol-testnet-docker/blob/master/docs/getting-started.md#supporting-multiple-chains)

Pull updates
```bash
git submodule update --init --recursive
```

Update chains env
```bash
bash update_chains
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

graph indexer rules set QmeWfMioAVdipQoxM5WxjtpU3ySYt7aedCECYToST2Rfui decisionBasis always allocationAmount 66666

graph indexer rules set QmWGXQeVv1jfU2puJAbSXXwLDW4gtd6fhf2D4R2cRP7qCK decisionBasis always allocationAmount 66666

graph indexer rules set QmeGpvmEKqwf21YauM95vS6jsCDBjcXoa1KeQppde5tWbh decisionBasis always allocationAmount 66666
```

## Fix Grafana
```bash
set -o allexport; source {{path_to_env_folder}}/.env-mainnet; set +o allexport; docker exec -it graphprotocol-mainnet-docker_postgres_1 psql "-U" ${DB_USER} ${GRAPH_NODE_DB_NAME} "-c" "refresh materialized view info.subgraph_sizes;"
```
```bash
set -o allexport; source {{path_to_env_folder}}/.env-testnet; set +o allexport; docker exec -it graphprotocol-testnet-docker_postgres_1 psql "-U" ${DB_USER} ${GRAPH_NODE_DB_NAME} "-c" "refresh materialized view info.subgraph_sizes;"
```
