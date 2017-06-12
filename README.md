# Cryptocurrency demo

This is demo of cryptocurrency implemented on Exonum blockchain.

It demonstrates the very basic operations:

- create a new wallet

- add funds into a wallet

- transfer funds from the one wallet to another

- monitor blocks status

## Backend

Backend keeps balances of wallets and handles secure transactions between them.
It consists of nodes which interact with each other. Distributed nodes ensure the reliability.

#### Build

To build the backend, use cargo:

```
cargo build --manifest-path=backend/Cargo.toml
```

#### Run

When backend was built, you should declare all nodes to run.
There is a special command `generate` which does it automatically:

```
cryptocurrency generate 4 --output-dir=example
```

In the example above we created configs for 4 nodes and put them into `example/` folder.

The next step you should start all nodes:

```
cryptocurrency run --leveldb-path=example/0 --node-config=example/validators/0.toml --public-api-address=127.0.0.1:8000
cryptocurrency run --leveldb-path=example/1 --node-config=example/validators/1.toml
cryptocurrency run --leveldb-path=example/2 --node-config=example/validators/2.toml
cryptocurrency run --leveldb-path=example/3 --node-config=example/validators/3.toml
```

## Frontend

Frontend is a lightweight single page application served by Node.js.
It communicates with the backend via REST API and uses [Exonum client](https://github.com/exonum/exonum-client) library to parse and verify data and perform cryptographic operations.

All business logic is can be found in [cryptocurrency.js](frontend/js/cryptocurrency.js).

#### How it works?

Find detailed [step-by-step tutorial](http://exonum.com/doc/home/cryptocurrency/intro/) how to set up all this demo functionality from the very beginning.

#### Build

Install npm dependencies:

```
cd frontend
npm install
```

#### Run

Before start check backend configuration at [frontend/config.json](frontend/config.json):

```
{
  "endpoint": "http://127.0.0.1:8000",
  "network_id": 0,
  "protocol_version": 0,
  "service_id": 128,
  "validators": [
    "756f0bb877333e4059e785e38d72b716a2ae9981011563cf21e60ab16bec1fbc",
    ...
  ] 
}
```

Now run application:

```
npm start
```

Application is served on [http://127.0.0.1:3000](http://127.0.0.1:3000). Port can be changred in the [frontend/app.js](frontend/app.js).
