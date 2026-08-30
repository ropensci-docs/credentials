# Retrieve and store git HTTPS credentials

Low-level wrappers for the
[git-credential](https://git-scm.com/docs/git-credential) command line
tool. Try the user-friendly
[git_credential_ask](https://docs.ropensci.org/credentials/reference/http_credentials.md)
and
[git_credential_update](https://docs.ropensci.org/credentials/reference/http_credentials.md)
functions first.

## Usage

``` r
credential_fill(cred, verbose = TRUE)

credential_approve(cred, verbose = TRUE)

credential_reject(cred, verbose = TRUE)
```

## Arguments

- cred:

  named list with at least fields `protocol` and `host` and optionally
  also `path`, `username` ,`password`.

- verbose:

  emit some useful output about what is happening

## Details

The credential_fill function looks up credentials for a given host, and
if none exists it will attempt to prompt the user for new credentials.
Upon success it returns a list with the same `protocol` and `host`
fields as the `cred` input, and additional `username` and `password`
fields.

After you have tried to authenticate the provided credentials, you can
report back if the credentials were valid or not. Call
credential_approve and credential_reject with the `cred` that was
returned by credential_fill in order to validate or invalidate a
credential from the store.

Because git credential interacts with the system password manager, the
appearance of the prompts vary by OS and R frontend. Note that
credential_fill should only be used interactively, because it may
require the user to enter credentials or unlock the system keychain. On
the other hand credential_approve and credential_reject are
non-interactive and could be used to save or delete credentials in a
scripted program. However note that some credential helpers (e.g. on
Windows) have additional security restrictions that limit use of
credential_approve and credential_reject to credentials that were
actually entered by the user via credential_fill. Here it is not
possible at all to update the credential store without user interaction.

## Examples

``` r
# \donttest{
# Insert example cred
example <- list(protocol = "https", host = "example.org",
  username = "test", password = "secret")
credential_approve(example)

# Retrieve it from the store
cred <- credential_fill(list(protocol = "https", host = "example.org", path = "/foo"))
print(cred)
#> $protocol
#> [1] "https"
#> 
#> $host
#> [1] "example.org"
#> 
#> $username
#> [1] "test"
#> 
#> $password
#> [1] "secret"
#> 
#> attr(,"class")
#> [1] "git_credential"

# Delete it
credential_reject(cred)
# }
```
