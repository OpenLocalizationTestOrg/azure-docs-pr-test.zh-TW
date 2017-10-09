建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。

[!INCLUDE [resource group intro text](resource-group.md)]

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westeurope*位置。

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

您通常在資源群組和 hello 資源的地區中建立您附近。 Azure Web 應用程式，執行 hello toosee 所有支援位置`az appservice list-locations`命令。 
