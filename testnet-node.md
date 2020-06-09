---
layout: smart
description: "Запуск Ноды на Тестовой Сети (testnet) Stacks"
# permalink: /:collection/:path.html
# redirect_from:
#   - /core/smart/neon-node.html
---
# Running a Testnet Node
# Запуск Ноды на Тестовой Сети
{:.no_toc}

The Stacks 2.0 testnet is currently in development. As part of the testnet, you can run a node and connect it to a public network. This guide will walk you through downloading and running your own node in the testnet network.

Тестовая сеть Stacks 2.0 в данный момент находится в разработке. Как часть тестовой сети, вы можете запустить ноду и подключить её к публичной сети. Это руководство проведет вас от скачивания до запуска своей собственной ноды на тестовой сети.

* TOC
{:toc}

### Prerequisites
Note: If you use Linux, you may need to manually install [`libssl-dev`](https://wiki.openssl.org/index.php/Libssl_API) and other packages. In your command line, run the following to get all packages:

### Необходимая конфигурация
Обратите внимание: Если вы используетее Linux, вам необходимо установить [`libssl-dev`](https://wiki.openssl.org/index.php/Libssl_API) и остальные пакеты. Чтобы это сделать, запустите следующую команду в командной строке:

```bash
sudo apt-get install build-essential cmake libssl-dev pkg-config
```

Ensure that you have Rust installed. If you are using macOS, Linux, or another Unix-like OS, run the following. If you are on a different OS, follow the [official Rust installation guide](https://www.rust-lang.org/tools/install).

Убедитесь, что у вас установлен Rust. Если вы используете macOS, Linux, или другую Unix-подобную ОС, запустите следующую команду. Для других операционных систем следуйте [официальной инструкции установки Rust](https://www.rust-lang.org/tools/install).

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

If Rust is already installed, you might see this prompt. Select 'Proceed with Installation' to make sure you have the latest version installed.

Если Rust уже установлен, вы можете увидеть следующее сообщение. Выберите 'Proceed with Installation', чтобы убедиться, что у вас установлена последняя версия.

  ![rustup prompt](/core/images/rust-install.png)

In case you just installed Rust, you will be prompted to run the following command to make the `cargo` command available:

Если вы только что установили Rust, вас попросят запустить следующую команду, чтобы сделать команду `cargo` доступной.

```bash
source $HOME/.cargo/env
```

### Download and install the `stacks-blockchain` repository

### Скачивание и установка репозитория `stacks-blockchain`

Next, clone this repository:

Затем, скачайте этот репозиторий:

```bash
git clone https://github.com/blockstack/stacks-blockchain.git

cd stacks-blockchain
```

Install the Stacks node by running:

Установите Stacks Ноду с помощью следующей команды:

```bash
cargo install --path ./testnet/stacks-node
```

### Run your node

### Запустите свою ноду

You're all set to run a node that connects to the testnet network.

Теперь вы готовы к запуску ноды, которая подключится к тестовой сети.

Back in the command line, run:

Снова запустите в командной строке:

```bash
stacks-node argon
```

The first time you run this, you'll see some logs indicating that the Rust code is being compiled. Once that's done, you should see some logs that look something like the this:

Первый раз, когда вы это запустите, вы увидите несколько сообщений, показывающие, что код в Rust скомпилирован. Как только это произойдет, вы должны увидеть что-то похожее на это:

```
INFO [1588108047.585] [src/chainstate/stacks/index/marf.rs:732] First-ever block 0f9188f13cb7b2c71f2a335e3a4fc328bf5beb436012afca590b1a11466e2206
```

Awesome! Your node is now connected to the testnet network. Your node will receive new blocks when they are produced, and you can use your [node's RPC API](/core/smart/rpc-api) to send transactions, fetch information for contracts and accounts, and more.

Отлично! Ваша нода теперь подключена к тестовой сети. Нода будет получать новые блоки по мере их создания, и вы можете использовать [RPC API ноды](/core/smart/rpc-api), чтобы высылать транзакции, получать информацию о контрактах и аккаунтах, а также делать многое другое.

### Running a miner

### Запуск майнера

Once you've followed the above steps to run a node, it's only a few more steps to run a proof-of-burn miner on the testnet.

После того, как вы выполнили шаги выше и запустили ноду, осталось совсем немного шагов, чтобы запустить proof-of-burn майнер на тестовой сети.

First, we need to generate a keychain. With this keychain, we'll get some testnet BTC from a faucet, and then use that BTC to start mining.

Для начала, нам нужно сгенерировать keychain. На этот keychain мы получим несколько тестовых BTC (testnet BTC) из крана (faucet). Затем мы будет использовать эти BTC, чтобы начать майнинг.

To get a keychain, the simplest way is to use the `blockstack-cli`. We'll use the `make_keychain` command, and pass `-t` to indicate that we want a testnet keychain.

Самый простой способ получить keychain - это использовать `blockstack-cli`. Мы будем использовать команду `make_keychain`, передавая параметр `-t`, обозначающий, что мы хотим получить keychain для тестовой сети.

```bash
npx blockstack-cli@1.1.0-beta.1 make_keychain -t
```

After this runs, you'll probably see some installation logs, and at the end you should see some JSON that looks like this:

После запуска вы вероятно увидите несколько установочных сообщений, в конце которых должен быть какой-то JSON, похожий на:

```json
{
  "mnemonic": "exhaust spin topic distance hole december impulse gate century absent breeze ostrich armed clerk oak peace want scrap auction sniff cradle siren blur blur",
  "keyInfo": {
    "privateKey": "2033269b55026ff2eddaf06d2e56938f7fd8e9d697af8fe0f857bb5962894d5801",
    "address": "STTX57EGWW058FZ6WG3WS2YRBQ8HDFGBKEFBNXTF",
    "btcAddress": "mkRYR7KkPB1wjxNjVz3HByqAvVz8c4B6ND",
    "index": 0
  }
}
```

We need to get some testnet BTC to that address. Grab the `btcAddress` field, and head over to [the Stacks testnet website](https://testnet.blockstack.org/faucet). In the BTC faucet section, past in your `btcAddress`, and submit. You'll be sent 0.5 testnet BTC to that address. **Don't lose this information** - we'll need to use the `privateKey` field later on.

Нам нужно получить немного тестовых BTC на этот адрес. Скопируйте значение поля `btcAddress`, и перейдите на [страницу Stacks testnet](https://testnet.blockstack.org/faucet). В секции "BTC faucet", вставьте `btcAddress`, и подтвердите данные. Вы получите 0.5 testnet BTC на этот адрес. **Запомните эту информацию** - нам будет необходимо значение поля `privateKey` позже.

Now, we need to configure out node to use this Bitcoin keychain. In the `stacks-blockchain` folder, create a new file called `testnet/stacks-node/conf/testnet-miner-conf.toml`.

Теперь нам нужно настроить нашу ноду, чтобы она использовала Bitcoin keychain. В папке `stacks-blockchain`, создайте новый файл с именем `testnet/stacks-node/conf/testnet-miner-conf.toml`.

Paste in the following configuration:

Вставьте в него следующую конфигурацию:

```toml
[node]
rpc_bind = "0.0.0.0:20443"
p2p_bind = "0.0.0.0:20444"
bootstrap_node = "048dd4f26101715853533dee005f0915375854fd5be73405f679c1917a5d4d16aaaf3c4c0d7a9c132a36b8c5fe1287f07dad8c910174d789eb24bdfb5ae26f5f27@argon.blockstack.org:20444"
# Enter your private key here!
seed = "replace-with-your-private-key"
miner = true

[burnchain]
chain = "bitcoin"
mode = "argon"
peer_host = "argon.blockstack.org"
rpc_port = 18443
peer_port = 18444

[[mstx_balance]]
address = "STB44HYPYAT2BB2QE513NSP81HTMYWBJP02HPGK6"
amount = 10000000000000000
[[mstx_balance]]
address = "ST11NJTTKGVT6D1HY4NJRVQWMQM7TVAR091EJ8P2Y"
amount = 10000000000000000
[[mstx_balance]]
address = "ST1HB1T8WRNBYB0Y3T7WXZS38NKKPTBR3EG9EPJKR"
amount = 10000000000000000
[[mstx_balance]]
address = "STRYYQQ9M8KAF4NS7WNZQYY59X93XEKR31JP64CP"
amount = 10000000000000000
```

Now, grab your `privateKey` from earlier, when you ran the `make_keychain` command. Replace the `seed` field with your private key. Save and close this configuration file.

Теперь возьмите `privateKey`, который мы ранее запомнили, когда использовали `make_keychain`. Замените поле `seed` своим приватным ключом. Сохраните и закройте этот конфигурационный файл.

To run your miner, run this in the command line:

Для запуска майнера, запустите следующий код в командной строке:

```bash
stacks-node start --config=./testnet/stacks-node/conf/testnet-miner-conf.toml
```

Your node should start. It will take some time to sync, and then your miner will be running!

Нода должна запуститься. Синхронизация займет какое-то время, а затем ваш майнер запуститься!

### Creating an optimized binary

### Создание оптимизированного бинарного файла

The steps above are great for trying to run a node temporarily. If you want to host a node on a server somewhere, you might want to generate an optimized binary. To do so, use the same configuration as above, but run:

Шаги выше отлично подходят для запуска временной ноды. Если же вы хотите захостить ноду на каком-то сервере, вам стоит сгенерировать оптимизированный бинарный файл. Чтобы это сделать, выполните те же шаги, что и раньше, но запустите:

```bash
cd testnet/stacks-node
cargo build --release --bin stacks-node
```

The above code will compile an optimized binary. To use it, run:

Этот код скомпилирует оптимизированный бинарный файл. Чтобы его использовать, запустите:

```bash
cd ../..
./target/release/stacks-node start --config=./testnet/conf/argon-follower-conf.toml
```

### Enable debug logging

### Включение диагностических сообщений (debug logging)

In case you are running into issues or would like to see verbose logging, you can run your node with debug logging enabled. In the command line, run:

В случае, если вы столкнклись с проблемами или хотели бы видеть подробные диагностические сообщения, вы можете запустить свою ноду в диагностическом режиме (debug logging). Для этого запустите в командной строке:

```bash
BLOCKSTACK_DEBUG=1 stacks-node argon
```