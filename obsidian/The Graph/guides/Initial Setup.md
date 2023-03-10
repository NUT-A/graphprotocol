## Установите докер
```bash <(curl -s https://raw.githubusercontent.com/DOUBLE-TOP/tools/main/go.sh)
```

## Склонируйте репозиторий
```bash
git clone https://github.com/NUT-A/graphprotocol.git
cd graphprotocol
```

## Заполните переменные
```bash
bash setup-env
```

- **email** - ваша почта
- **domain** - ваше доменное имя
- **admin_password http_password db_password** - сгенерируйте пароли и сохраните их куда-то. Желательно для всех трёх разные пароли(и разные между тестнетом и мейннетом). **admin_password** будет использоваться для доступа к графане, **http_password** к прометею и прочим веб приложениям
- **gnosis_rpc** - адрес гносис ноды
- **infura** - URL проекта инфура. Для мейненета выбираете мейннет сеть, для тестнета Goerli. Регистрируйте для мейннета и тестнета разные аккаунты, иначе не влезите по квоте
- **operator_seed** - сид фраза вашего оператор кошелька(набор слов)
- **address** - адрес кошелька, на котором вы стейкали граф
Кошельки я реюзнул старые, но, если вы хотите всё сделать красиво — делайте отдельную пару для мейннета.

Ваши данные сохранятся в папке `env`.

## Запустите скрипт
```bash
bash start
```
