# lawallet Test Environment

Quickly setup a lawallet test environment with the latest deployed images for each module and a nostr relay.

**Included lawallet modules:**

- [ledger](https://github.com/lawalletio/ledger)
- [urlx](https://github.com/lawalletio/urlx)
- [api-gateway](https://github.com/lawalletio/api-gateway)

Additionally, the following NOSTR relay is bundled:

- [nostream](https://github.com/Cameri/nostream)

## Prerequisites

In order to launch the testing environment you'll need:

- `openssl`: required for public / private key generation (you may install it with `apt install openssl`)
- `docker`: required to launch the individual containers (you may install it with `apt install docker-compose`)
- `polar`: a local lightning network development environment (you may download the _AppImage_ file from the [Polar Homepage](https://lightningpolar.com/))

## Setup

Prior to running the test environment, the local lightning network must be booted:

1. launch the Polar _AppImage_ file,
2. click on **Import Network**,
3. select the `./polar/testing.polar.zip` file, and
4. click on the **Start** button to launch the network proper.

Once the local lightning network is up, simply run the `./up` script to generate the `.env` file with keys and secrets, and launch the testing environment proper.

This will start the docker instances and show the ongoing logs.
WHen you're done testing, you may stop all the instances with `Ctrl+C`, and docker will stop all the containers for you.
