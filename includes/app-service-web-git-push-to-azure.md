## <a name="push-tooazure-from-git"></a><span data-ttu-id="9e470-101">從 Git 推送 tooAzure</span><span class="sxs-lookup"><span data-stu-id="9e470-101">Push tooAzure from Git</span></span>

<span data-ttu-id="9e470-102">新增 Azure 遠端 tooyour 本機 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9e470-102">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="9e470-103">將 Azure 遠端 toodeploy toohello 推送您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9e470-103">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="9e470-104">系統提示您先前建立 hello 部署使用者時所建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="9e470-104">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="9e470-105">請確認您輸入您在建立 hello 密碼[部署使用者設定](#configure-a-deployment-user)，不會 hello toolog 用於 toohello Azure 入口網站的密碼。</span><span class="sxs-lookup"><span data-stu-id="9e470-105">Make sure that you enter hello password you created in [Configure a deployment user](#configure-a-deployment-user), not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="9e470-106">hello 上述命令會顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="9e470-106">hello preceding command displays information similar toohello following example:</span></span>
