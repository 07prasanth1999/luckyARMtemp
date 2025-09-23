# ARM: Ubuntu VM + Apache on 8080

This template deploys:
- Ubuntu VM (password login)
- Apache (HTTPD) on **port 8080**
- NSG that allows only `allowedSourceCidr`
- Home page shows **current date/time**

## Where things are in `deploy.json`
- DNS name: `resources -> Microsoft.Network/publicIPAddresses -> properties.dnsSettings.domainNameLabel`
- Only-my-IP rule: `resources -> Microsoft.Network/networkSecurityGroups -> properties.securityRules[0].sourceAddressPrefix`
- Date/time page (Apache install): `resources -> Microsoft.Compute/virtualMachines/extensions -> CustomScript -> settings.commandToExecute`
- Outputs: `outputs.browseUrl` and `outputs.publicIpAddress`

## How to deploy
1) create RG: `az group create -n LuckyRG -l eastus`
2) put real values in local `parameters.json` (do **not** commit it)
3) `az deployment group create --name web8080 --resource-group LuckyRG --template-file .\deploy.json --parameters @.\parameters.json`
