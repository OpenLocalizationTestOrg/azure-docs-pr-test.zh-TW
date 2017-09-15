<span data-ttu-id="958de-101">使用 Azure CLI 取得 API 應用程式的遠端部署 URL。</span><span class="sxs-lookup"><span data-stu-id="958de-101">Use the Azure CLI to get the remote deployment URL for your API App.</span></span> <span data-ttu-id="958de-102">在下列命令中，使用您 Web 應用程式的名稱取代 *\<app_name>*。</span><span class="sxs-lookup"><span data-stu-id="958de-102">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="958de-103">將本機 Git 部署設定為可以推送至遠端。</span><span class="sxs-lookup"><span data-stu-id="958de-103">Configure your local Git deployment to be able to push to the remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="958de-104">推送到 Azure 遠端來部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="958de-104">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="958de-105">當您建立部署使用者時，系統會提示您輸入稍早建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="958de-105">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="958de-106">務必輸入先前在快速入門中建立的密碼，而不是您用來登入 Azure 入口網站的密碼。</span><span class="sxs-lookup"><span data-stu-id="958de-106">Make sure that you enter the password you created in earlier in the quickstart, and not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```
