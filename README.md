# lawallet Environment

Quickly setup a lawallet environment with the latest deployed images for each module.

Included lawallet modules:

- [api-gateway](https://github.com/lawalletio/api-gateway)
- [card](https://github.com/lawalletio/card)
- [ledger](https://github.com/lawalletio/ledger)
- [monitor](https://github.com/lawalletio/monitor)
- [urlx](https://github.com/lawalletio/urlx)

## Development

Development environments can be easily set up, including the aforementioned lawallet modules, alongside:

- [nostream](https://github.com/Cameri/nostream)
- [NGINX](https://nginx.org) SSL Proxy
- [Polar](https://lightningpolar.com) Network

### Requirements

- `openssl`: required for public / private key generation (you may install it with `apt install openssl`)
- `mkcert`: required for local certificate trusting (see: [`mkcert`'s homepage](https://github.com/FiloSottile/mkcert))
- `docker`: required to launch the individual containers (you may install it with `apt install docker-compose`) **--- REQUIRES `docker compose` VERSION 2.20.0 OR NEWER**
- `polar`: a local lightning network development environment (you may download the _AppImage_ file from the [Polar Homepage](https://lightningpolar.com/))

In order to check these, you may run:

```sh
$ openssl version
...
$ mkcert -install
...
$ docker compose version
...
```

Running `mkcert -install` will incidentally install `mkcert`'s root CA so that you may use it right away.

### Quick Start

Simply:

1. Launch the Polar network:
    1. run the Polar `AppImage` file,
    2. click on **Import Network**,
    3. select the `./polar/testing.polar.zip` file, and
    4. click on the **Start** button to launch the network proper.
2. (optionally) Customize the `.env.example.dev` environment file if you so desire (you really don't need to),
3. Run `./dev` and follow on-screen instructions.

> _**Why are you asking for my `sudo` password?**_
>
> The `./dev` script will try to _reversibly_ add entries to `/etc/hosts`, in order for this process to be non-invasive, we need to be able to run `mount --bind ...` and `umount -f ...`, and this can only be done via `sudo`.
>
> The script will only ask once, and keep the credentials fresh in the background.

The `./dev` script will generate all required public / private NOSTR keys, and the nostream secret to use, all other parameters are preconfigured to work correctly with the composed setup.

It will then start the docker instances and show the ongoing logs.
When you're done testing, you may stop all the instances with `Ctrl+C`, and docker will stop all the containers for you, and the script will undo the hosts mappings.

## Production

Production environments are easily set up as well, but will spin up a reduced number of containers (since we do not wish to use the Polar Network, nor the SSL proxy).

You're likely to want to change the following environment variables in `.env.example.prod`:

- `SERVER_AES_KEY_HEX`
- `CARD_WRITER_PUBKEY`
- `FEDERATION_ID`

Even if just for prod / dev separations purposes.

Next, you'll need to access your LND and get the admin url which contains the cert and the macaroon. Then add it to the following env variable:

- `LNDCONNECT_URI`

Finally, the following environmental variables will only be regenerated if empty:

- `NOSTREAM_SECRET`
- `LEDGER_PRIVATE_KEY` / `LEDGER_PUBLIC_KEY`
- `URLX_PRIVATE_KEY` / `URLX_PUBLIC_KEY`
- `CARD_PRIVATE_KEY` / `CARD_PUBLIC_KEY`

Finally, simply run `./prod -b` to start the production environment. The `-b` flag is for building the images, this only needs to be done when you want to build the current images in the master branches of each repo.

## Extra environments

This project supports starting multiple stacks at the same time, all you need to to is provide the `-t tag` to the `./prod` script with the desired name. You can also override docker compose configuration by using the `docker-compose.override.yaml` file. Lets say you want to test a different version of the `urlx` module, all you need to do is writing the following:

```yaml
services:
  urlx:
    image: lawallet/urlx:my-feature
```
