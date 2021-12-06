# weechat

## Introduction

My [weechat](https://weechat.org/) configuration.  I generally only use [freenode](https://freenode.net/) and authenticate using SASL, so settings reflect that.

This configuration relies on weechat's [secure data](https://www.weechat.org/files/doc/stable/weechat_user.en.html#secured_data) feature.  To use this configuration and set-up secure data, follow these steps:

1. Install weechat.
1. Clone this repository: `git clone https://github.com/craighurley/weechat.git ~/.weechat`
1. Create `~/.weechat/sec.conf` and fill in your freenode nickname and SASL details:

    ```
    #
    # weechat -- sec.conf
    #

    [crypt]
    cipher = aes256
    hash_algo = sha256
    passphrase_file = ""
    salt = on

    [data]
    __passphrase__ = off
    nick = "YOUR_NICKNAME"
    sasl_mechanism = "plain"
    freenode_sasl_password = "YOUR_PASSWORD"
    ```

    Alternatively, if you use SASL ECDSA-NIST256P-CHALLENGE:

    ```
    #
    # weechat -- sec.conf
    #

    [crypt]
    cipher = aes256
    hash_algo = sha256
    passphrase_file = ""
    salt = on

    [data]
    __passphrase__ = off
    nick = "YOUR_NICKNAME"
    sasl_mechanism = "ecdsa-nist256p-challenge"
    ```

1. Start weechat.
1. Update the path to the CA file according your your OS:

    - Alpine: `/set weechat.network.gnutls_ca_file "/etc/ssl/certs/ca-certificates.crt"`
    - CentOS: `/set weechat.network.gnutls_ca_file "/etc/ssl/certs/ca-bundle.crt"`
    - macOS: `/set weechat.network.gnutls_ca_file "/usr/local/etc/openssl/cert.pem"`
    - Ubuntu: `/set weechat.network.gnutls_ca_file "/etc/ssl/certs/ca-certificates.crt"`

1. (Optional) Once connected to freenode, consider protecting the contents of your `sec.conf` file with a password.  In the weechat buffer, run `/secure passphrase YOUR_PASSPHRASE`.

## weechat version

Tested on `2.3`

## docker-compose

If you want to run weechat in a container, mounting this content as your config, run the following:

```sh
docker-compose run --rm weechat
```
