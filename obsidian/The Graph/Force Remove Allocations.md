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
