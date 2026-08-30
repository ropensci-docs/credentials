# Credential Helpers

Git supports several back-end stores for HTTPS credentials called
helpers. Default helpers include `cache` and `store`, see the
[git-credentials](https://git-scm.com/docs/gitcredentials) manual page
for details.

## Usage

``` r
credential_helper_list()

credential_helper_get(global = FALSE)

credential_helper_set(helper, global = FALSE)
```

## Arguments

- global:

  if FALSE the setting is done per git repository, if TRUE it is in your
  global user git configuration.

- helper:

  string with one of the supported helpers from credential_helper_list
