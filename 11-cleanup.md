# Clean up

After you are done exploring your deployed [AKS secure baseline cluster](./), you'll want to delete the created Azure resources to prevent undesired costs from accruing. Follow these steps to delete all resources created as part of this reference implementation.

## Steps

1. Delete the resource groups, which will delete all related Azure resources.

   :warning: Ensure you are using the correct subscription, and validate that the only resources that exist in these groups are ones you're okay deleting.
   ```bash
   az group delete -n rg-shipping-dronedelivery --no-wait
   az group delete -n rg-shipping-dronedelivery-acr --no-wait
   az group delete -n rg-enterprise-networking-spokes --no-wait
   az group delete -n rg-enterprise-networking-hubs --no-wait
   ```

1. Purge Azure Key Vault

   > Because this reference implementation enables soft delete on Key Vault, execute a purge, so your next deployment of this implementation doesn't run into a naming conflict.

   ```bash
   az keyvault purge --name ${KEYVAULT_NAME} --location eastus2
   ```

1. If any temporary changes were made to Microsoft Entra ID or Azure RBAC permissions, consider removing those as well.

1. [Remove the Azure Policy assignments](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyMenuBlade/Compliance) scoped to the cluster's resource group. To identify those created by this implementation, look for ones that are prefixed with `[your-cluster-name] `.

### Next step

:arrow_forward: [Review additional information in the main README](./README.md#broom-clean-up-resources)
