## <a name="clean-up-deployment"></a><span data-ttu-id="34ef1-101">清除部署</span><span class="sxs-lookup"><span data-stu-id="34ef1-101">Clean up deployment</span></span> 

<span data-ttu-id="34ef1-102">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Azure Redis 快取執行個體，以及資源群組中任何相關的資源。</span><span class="sxs-lookup"><span data-stu-id="34ef1-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```