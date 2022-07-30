 
# Create a vnet

$resourceGroupName = "sfg-dev01"

New-AzResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile .\vnet1.json
