## <a name="clean-up-deployment"></a><span data-ttu-id="e09ee-101">清除部署</span><span class="sxs-lookup"><span data-stu-id="e09ee-101">Clean up deployment</span></span>

<span data-ttu-id="e09ee-102">Hello 指令碼範例執行後，hello 後續命令可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="e09ee-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli
az group delete --name myResourceGroup
```