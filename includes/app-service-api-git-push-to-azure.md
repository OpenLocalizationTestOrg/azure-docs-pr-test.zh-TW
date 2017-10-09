<span data-ttu-id="f739f-101">您 API 應用程式使用 hello Azure CLI tooget hello 遠端部署 URL。</span><span class="sxs-lookup"><span data-stu-id="f739f-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="f739f-102">下列命令，取代在 hello  *\<app_name >* web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="f739f-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="f739f-103">設定您本機 Git 部署 toobe 無法 toopush toohello 遠端。</span><span class="sxs-lookup"><span data-stu-id="f739f-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="f739f-104">將 Azure 遠端 toodeploy toohello 推送您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f739f-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="f739f-105">系統提示您先前建立 hello 部署使用者時所建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="f739f-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="f739f-106">請確定您輸入 hello 快速入門中，在中建立的 hello 密碼而不會 hello toolog 用於 toohello Azure 入口網站的密碼。</span><span class="sxs-lookup"><span data-stu-id="f739f-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
