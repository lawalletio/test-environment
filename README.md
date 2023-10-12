# lawallet test environment

Quickly setup a lawallet test environment with the latest deployed images for
each module and a nostr relay.

**Modules:**
- [ledger](https://github.com/lawalletio/ledger)
- [urlx](https://github.com/lawalletio/urlx)
- [api-gateway](https://github.com/lawalletio/api-gateway)

## Setup

0. Install [docker](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/).
0. Copy all the `.env.<name>.example` files to `.env.<name>`.
0. Copy `resources/defaults-settings.yml` to `.nostr/settings.yml`
0. Complete the environment variables.
0. Run the following command:
    ```bash
    docker-compose -f nostream.yml    \
                   -f api-gateway.yml \
                   -f urlx.yml        \
                   -f ledger.yml      \
     up -d
    ```

