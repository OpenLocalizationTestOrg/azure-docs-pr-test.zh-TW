<span data-ttu-id="55705-101">使用 [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) 命令設定 Web 應用程式的本機 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="55705-101">Configure local Git deployment to the web app with the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="55705-102">App Service 支援數種將內容部署至 Web 應用程式的方式，例如 FTP、本機 Git、GitHub、Visual Studio Team Services 和 Bitbucket。</span><span class="sxs-lookup"><span data-stu-id="55705-102">App Service supports several ways to deploy content to a web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="55705-103">針對這個快速入門，您要使用本機 Git 來進行部署。</span><span class="sxs-lookup"><span data-stu-id="55705-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="55705-104">這表示您要使用 Git 命令來進行部署，從本機存放庫推送到 Azure 中的存放庫。</span><span class="sxs-lookup"><span data-stu-id="55705-104">That means you deploy by using a Git command to push from a local repository to a repository in Azure.</span></span> 

<span data-ttu-id="55705-105">在下列命令中，使用您 Web 應用程式的名稱取代 *\<app_name>*。</span><span class="sxs-lookup"><span data-stu-id="55705-105">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="55705-106">輸出具備下列格式：</span><span class="sxs-lookup"><span data-stu-id="55705-106">The output has the following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="55705-107">`<username>` 是您在上一個步驟中建立的[部署使用者](#configure-a-deployment-user)。</span><span class="sxs-lookup"><span data-stu-id="55705-107">The `<username>` is the [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="55705-108">複製顯示的 URI；您在下一個步驟中將會用到它。</span><span class="sxs-lookup"><span data-stu-id="55705-108">Copy the URI shown; you'll use it in the next step.</span></span>
