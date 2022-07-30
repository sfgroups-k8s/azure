# Create a resourceGroup

New-AzSubscriptionDeployment -Location eastus -TemplateFile .\azuredeploy.json -TemplateParameterFile  .\azuredeploy.parameters.json