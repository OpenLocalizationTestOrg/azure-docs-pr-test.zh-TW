<span data-ttu-id="da3da-101">設定本機 Git 部署 toohello web 應用程式以 hello [az webapp 部署來源設定為本機的 git](/cli/azure/webapp/deployment/source#config-local-git)命令。</span><span class="sxs-lookup"><span data-stu-id="da3da-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="da3da-102">應用程式服務支援數種方式 toodeploy 內容 tooa web 應用程式，例如 FTP、 本機 Git、 GitHub、 Visual Studio Team Services 和 Bitbucket。</span><span class="sxs-lookup"><span data-stu-id="da3da-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="da3da-103">針對這個快速入門，您要使用本機 Git 來進行部署。</span><span class="sxs-lookup"><span data-stu-id="da3da-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="da3da-104">這表示您使用 Git 命令 toopush 從本機儲存機制 tooa 儲存機制，在 Azure 中部署。</span><span class="sxs-lookup"><span data-stu-id="da3da-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="da3da-105">下列命令，取代在 hello  *\<app_name >* web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="da3da-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="da3da-106">hello 輸出具有下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="da3da-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="da3da-107">hello`<username>`為 hello[部署使用者](#configure-a-deployment-user)您在上一個步驟中建立。</span><span class="sxs-lookup"><span data-stu-id="da3da-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="da3da-108">複製 hello URI 所示。您將 hello 下一個步驟中使用它。</span><span class="sxs-lookup"><span data-stu-id="da3da-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
