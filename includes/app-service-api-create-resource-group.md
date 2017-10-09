<span data-ttu-id="348fe-101">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="348fe-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="348fe-102">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westeurope*位置。</span><span class="sxs-lookup"><span data-stu-id="348fe-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="348fe-103">toosee hello 可用的位置，執行 hello`az appservice list-locations`命令。</span><span class="sxs-lookup"><span data-stu-id="348fe-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="348fe-104">您通常會在附近的區域中建立資源。</span><span class="sxs-lookup"><span data-stu-id="348fe-104">You generally create resources in a region near you.</span></span>
