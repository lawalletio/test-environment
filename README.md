# lawallet test environment

Quickly setup a lawallet test environment with the latest deployed images for
each module and a nostr relay.

**Modules:**

- [ledger](https://github.com/lawalletio/ledger)
- [urlx](https://github.com/lawalletio/urlx)
- [api-gateway](https://github.com/lawalletio/api-gateway)

## Setup

0. Install [docker](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/).
1. Copy all the `.env.<name>.example` files to `.env.<name>`.
2. Copy `resources/defaults-settings.yaml` to `.nostr/settings.yaml`
3. Complete the environment variables (**INCLUDING** the `services.nostream.environment.SECRET` value in `./nostream.yaml`).
4. Run the following command:

    ```bash
    docker-compose -f nostream.yaml    \
                   -f api-gateway.yaml \
                   -f urlx.yaml        \
                   -f ledger.yaml      \
     up -d
    ```
