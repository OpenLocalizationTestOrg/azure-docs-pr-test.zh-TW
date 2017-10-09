<span data-ttu-id="7e323-101">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="7e323-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="7e323-102">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *westeurope*位置。</span><span class="sxs-lookup"><span data-stu-id="7e323-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="7e323-103">您通常在資源群組和 hello 資源的地區中建立您附近。</span><span class="sxs-lookup"><span data-stu-id="7e323-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="7e323-104">Azure Web 應用程式，執行 hello toosee 所有支援位置`az appservice list-locations`命令。</span><span class="sxs-lookup"><span data-stu-id="7e323-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
