# lawallet test environment

Quickly setup a lawallet test environment with the latest deployed images for each module and a nostr relay.

**Modules:**

- [ledger](https://github.com/lawalletio/ledger)
- [urlx](https://github.com/lawalletio/urlx)
- [api-gateway](https://github.com/lawalletio/api-gateway)

## Setup

0. Install [docker](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/).
1. Copy the `.env.example` file `.env`.
2. Complete the environment variables therein.
3. Run the following command: `docker compose up`
