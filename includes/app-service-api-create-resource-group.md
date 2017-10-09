建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。

[!INCLUDE [resource group intro text](resource-group.md)]

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westeurope*位置。

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

toosee hello 可用的位置，執行 hello`az appservice list-locations`命令。 您通常會在附近的區域中建立資源。
