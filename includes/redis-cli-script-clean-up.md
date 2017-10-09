## <a name="clean-up-deployment"></a><span data-ttu-id="28415-101">清除部署</span><span class="sxs-lookup"><span data-stu-id="28415-101">Clean up deployment</span></span> 

<span data-ttu-id="28415-102">Hello 指令碼範例執行後，hello 後續命令可以使用的 tooremove hello 資源群組、 Azure Redis 快取執行個體和 hello 資源群組中的任何相關的資源。</span><span class="sxs-lookup"><span data-stu-id="28415-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```