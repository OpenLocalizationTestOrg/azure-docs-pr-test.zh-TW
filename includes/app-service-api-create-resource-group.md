<span data-ttu-id="8d1f7-101">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="8d1f7-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="8d1f7-102">下列範例會在 westeurope 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8d1f7-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="8d1f7-103">若要查看可用的位置，請執行 `az appservice list-locations` 命令。</span><span class="sxs-lookup"><span data-stu-id="8d1f7-103">To see the available locations, run the `az appservice list-locations` command.</span></span> <span data-ttu-id="8d1f7-104">您通常會在附近的區域中建立資源。</span><span class="sxs-lookup"><span data-stu-id="8d1f7-104">You generally create resources in a region near you.</span></span>
