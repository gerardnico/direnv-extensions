% direnv-x-print(1) Version Latest | Vault and multi-env support to direnv
# NAME

Add vault and multi-env support to direnv

## Example

With this `.env` file in your project root:
* Add one or more `.env` file in your project root
```ini
POSTGRES_USER=postgres
POSTGRES_PASSWORD=vault:secret/postgres/password
```
You would get
```bash
export POSTGRES_USER=postgres
export POSTGRES_PASSWORD=welcome # value from vault
export DIRENV_EXPORTED_ENVS=POSTGRES_USER,POSTGRES_PASSWORD
```

`DIRENV_EXPORTED_ENVS` may be used to recreate a list of env.
For instance, [for docker in the form `-e KEY=VALUE`](#how-to-use-direnv_exported_envs-to-list-and-pass-envs-as-argument-at-the-command-line)


## How it works

You create an `.envrc` file at the root of your project
with the following command
```bash
eval "$(direnv-x-print)"
```

# DESCRIPTION

This script will take all env file (`.env` and `.env.*`)
* print it in a bash export format
* retrieve value from a vault if the value has the form: `vault:/path/to/secret/field`
* export the keys in the `DIRENV_EXPORTED_KEYS` variable
    Why? `DIRENV_EXPORTED_ENVS` may be used to recreate a list of env. For instance, for docker in the form `-e KEY=VALUE`


# FEATURES

Support:
* Windows file format (ie CRLF)
* Vault

# VAULT VALUE SYNTAX

The vault syntax value is `vault:/path/to/secret/fieldName`

You would have installed vault locally and initialized it with
```bash
vault login
```


# How to use DIRENV_EXPORTED_ENVS to list and pass envs as argument at the command line

This example shows you how to pass environment variable to docker in the form `-e KEY=VALUE`
```bash
declare -a DOCKER_ENV_ARGS=()
IFS=',' read -ra DIRENV_EXPORTED_KEYS_AS_ARRAY <<< ""
for ENV in "${DIRENV_EXPORTED_KEYS_AS_ARRAY[@]}"; do
    # Filter out all docker variable
    if [[  == DOCKER* ]]; then
        continue
    fi
    if [[ -v  ]]; then
        DOCKER_ENV_ARGS+=("-e")
        DOCKER_ENV_ARGS+=("=${!ENV}")
    fi
done

# then add them to docker
docker run \
  "${DOCKER_ENV_ARGS[@]}" 
```