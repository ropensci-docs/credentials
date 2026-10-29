# Set your Github Personal Access Token

Populates the `GITHUB_PAT` environment variable using the
[git_credential](https://docs.ropensci.org/credentials/reference/http_credentials.md)
manager, which `git` itself uses for storing passwords. The credential
manager returns stored credentials if available, and securely prompt the
user for credentials when needed.

## Usage

``` r
set_github_pat(force_new = FALSE, validate = interactive(), verbose = validate)
```

## Arguments

- force_new:

  forget existing pat, always ask for new one.

- validate:

  checks with the github API that this token works. Defaults to `TRUE`
  only in an interactive R session (not when running e.g. CMD check).

- verbose:

  prints a message showing the credential helper and PAT owner.

## Value

Returns `TRUE` if a valid GITHUB_PAT was set, and FALSE if not.

## Details

Packages that require a `GITHUB_PAT` can call this function to
automatically set the `GITHUB_PAT` when needed. Users may call this
function in their [.Rprofile](https://rdrr.io/r/base/Startup.html)
script to automatically set `GITHUB_PAT` for each R session without
hardcoding any tokens on disk in plain-text.
