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
`az sql db restore --dest-name Backup_2022_12_05_1300 -z true --elastic-pool ElasticPoolName --name DatabaseName --server ServerName --time "2022-12-05T13:00:00" --resource-group ResourceGroupName` | Point in time restore of a database with geo-replication (`-z true`)
`az sql db list --server ServerName --resource-group ResourceGroupName > dblist.json` | Get databases list in a json file
`az sql elastic-pool create --name <elastic-pool-name> --resource-group <resource-group-name> --server <server-name> --edition <elastic-pool-edition> --dtu <elastic-pool-dtu> --db-dtu-min <db-dtu-min-value> --db-dtu-max <db-dtu-max-value>` | Create a new SQL Elastic pool with classic DTU configuration
`az sql server ad-admin create --server-name <server-name> --resource-group <resource-group-name> --display-name "<display-name>" --object-id <object-guid>` | Set AD admin for the server. It is NOT possible to have more than one AD admin. `create` will replace the existing one if any.

## References

https://docs.microsoft.com/fr-fr/archive/blogs/waws/things-you-should-know-web-apps-and-ssh
