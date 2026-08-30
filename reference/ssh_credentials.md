# Managing Your SSH Key

Utility functions to find or generate your SSH key for use with git
remotes or other ssh servers.

## Usage

``` r
ssh_key_info(host = NULL, auto_keygen = NA)

ssh_keygen(file = ssh_home("id_ecdsa"))

ssh_setup_github()

ssh_home(file = NULL)

ssh_agent_add(file = NULL)

ssh_update_passphrase(file = ssh_home("id_rsa"))

ssh_read_key(file = ssh_home("id_rsa"), password = askpass)
```

## Arguments

- host:

  target host (only matters if you have configured specific keys per
  host)

- auto_keygen:

  if `TRUE` automatically generates a key if none exists yet. Default
  `NA` is to prompt the user what to.

- file:

  destination path of the private key. For the public key, `.pub` is
  appended to the filename.

- password:

  a passphrase or callback function

## Details

Use `ssh_key_info()` to find the appropriate key file on your system to
connect with a given target host. In most cases this will simply be
`ssh_home('id_rsa')` unless you have configured ssh to use specific keys
for specific hosts.

To use your key to authenticate with GitHub, copy the pubkey from
`ssh_key_info()` to your profile: <https://github.com/settings/ssh/new>.

If this is the first time you use ssh, ssh_keygen can help generate a
key and save it in the default location. This will also automatically
opens the above Github page in your browser where you can add the key to
your profile.

`ssh_read_key` reads a private key and caches the result (in memory) for
the duration of the R session. This prevents having to enter the key
passphrase many times. Only use this if `ssh-agent` is not available
(i.e. Windows)

## See also

Other credentials:
[`http_credentials`](https://docs.ropensci.org/credentials/reference/http_credentials.md)
