Отправить эфир на оператора тестнета перед выполнением гайда

## Запросить GRT
В канале `#testnet-faucet` дважды запросить токены на ваш стейкинг адрес
```
!grt {{address}}
```

## Застейкать токены
[Link](https://github.com/StakeSquid/graphprotocol-mainnet-docker/blob/master/docs/pre-requisites.md)

## Добавить RPC
```bash
bash update-chains
```

## Перезапустить
```bash
bash stop
bash start
```

## Аллоцировать сабграфы
```bash
docker-compose -f $HOME/graphprotocol/graphprotocol-testnet-docker/compose-indexer.yml exec cli bash

graph indexer rules set QmdPYiwtdBqeDKeMHKWDhuJFxu1TAxWP3qo2Peptia4sLB decisionBasis always allocationAmount 50000
graph indexer rules set QmVbEmYjNRU5zyRDq6WDCWLnq952vDVWaM8AmVtvxpMy4b decisionBasis always allocationAmount 50000
graph indexer rules set QmPy774Z6xNnELMwcie5stweyWdVhj3PMRWxwV9Xm8VpUr decisionBasis always allocationAmount 50000
graph indexer rules set QmPeDVt7ygNQfmQoxsVazBHosebMeDW62tpyP8gqbZDvbJ decisionBasis always allocationAmount 50000
```