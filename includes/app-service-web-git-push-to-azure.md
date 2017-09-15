## <a name="push-to-azure-from-git"></a><span data-ttu-id="e1b2f-101">從 Git 推送至 Azure</span><span class="sxs-lookup"><span data-stu-id="e1b2f-101">Push to Azure from Git</span></span>

<span data-ttu-id="e1b2f-102">將 Azure 遠端新增至本機 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="e1b2f-102">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="e1b2f-103">推送到 Azure 遠端來部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1b2f-103">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="e1b2f-104">當您建立部署使用者時，系統會提示您輸入稍早建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1b2f-104">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="e1b2f-105">務必輸入您在[設定部署使用者](#configure-a-deployment-user)中建立的密碼，而不是您用來登入 Azure 入口網站的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1b2f-105">Make sure that you enter the password you created in [Configure a deployment user](#configure-a-deployment-user), not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="e1b2f-106">上述命令會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="e1b2f-106">The preceding command displays information similar to the following example:</span></span>
