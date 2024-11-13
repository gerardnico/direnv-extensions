# Direnv X - Add vault and multi-env support to direnv


## About

Do you want to:
* add secrets from [Hashicorp vault](https://www.vaultproject.io/)
* use multiple environments files (`.env`,`.env.docker`)
for your project ?

The `direnv extensions script` is here to help.

## Example and Documentation

See [the direnv-x-print documentation](docs/bin-generated/direnv-x-print.md)

## Install

### Homebrew

* Install `direnv-x` with [homebrew](https://brew.sh/)
```bash
brew install --HEAD gerardnico/tap/direnvx
# Set the libraries directory in your `.bashrc` file
export BASHLIB_LIBRARY_PATH=$(brew --prefix bashlib)/lib
```

