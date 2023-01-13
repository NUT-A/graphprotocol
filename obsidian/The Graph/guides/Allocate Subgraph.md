Пока нет других сабграфов, советую аллоцировать весь баланс. Позже сможете сбалансировать.

Если вы "для теста" аллоцируете часть токенов — поменять это значение сможете только через день. Копируйте блоки по одному
```bash
cd graphprotocol-testnet-docker
./shell cli
```
```bash
graph indexer rules set QmXWbpH76U6TM4teRNMZzog2ismx577CkH7dzn1Nw69FcV decisionBasis always allocationAmount 100000
```