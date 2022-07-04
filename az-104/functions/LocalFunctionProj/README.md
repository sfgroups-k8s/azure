
https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-cli-python?tabs=azure-cli%2Cbash%2Cbrowser

```
python3 -m venv .venv

source .venv/bin/activate

func init LocalFunctionProj --python

cd LocalFunctionProj

func new --name HttpExample --template "HTTP trigger" --authlevel "anonymous"


func start

http://localhost:7071/api/HttpExample?name=Azue



```

deploy

```
az login
az config param-persist on

az group create --name AzureFunctionsQuickstart-rg --location eastus


az storage account create --name pythonapp01 -g AzureFunctionsQuickstart-rg --sku Standard_LRS


az functionapp create  --consumption-plan-location eastus --resource-group AzureFunctionsQuickstart-rg   --runtime python --runtime-version 3.9 --functions-version 4 --name python-sunny --os-type linux --storage-account pythonapp01

func azure functionapp publish python-sunny

https://python-sunny.azurewebsites.net/api/httpexample?name=az-104

func azure functionapp logstream python-sunny --browser

*) delete function

az group delete --name AzureFunctionsQuickstart-rg
```
