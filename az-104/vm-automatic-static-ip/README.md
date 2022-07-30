 
# Create a vnet

$resourceGroupName = "sfg-dev01"

New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile .\azuredeploy.json -TemplateParameterFile  .\azuredeploy.parameters.json
