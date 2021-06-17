# Azure CLI Cheat Sheet

## CLI Installation

Follow instructions provided here : https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt

## Frequently used commands

Command | Description
--- | ---
`az login` | authenticate on Azure with your Microsoft account
`az account set -s <subscription_guid_or_name>` | if you have multiple subscriptions then you have to set the one you want to use
`az acr login -n <registryName>` | authenticate to Azure Container Registry named <registryName> (without extension azurecr.io). Once connected you can pull/push.
`az extension add -n webapp` | install the webapp extension to allow webapp management
`az extension update -n webapp` | update the webapp extension
`az webapp create-remote-connection -g ResourceGroup -n WebAppName -p LocalPortNumber` | Open a TCP tunnel from local machine to webapp. Add `--slot staging` parameter to connect to a specific slot. You can now SSL through the tunnel via `ssh root@127.0.0.1 -p 9000`

## References

https://docs.microsoft.com/fr-fr/archive/blogs/waws/things-you-should-know-web-apps-and-ssh
