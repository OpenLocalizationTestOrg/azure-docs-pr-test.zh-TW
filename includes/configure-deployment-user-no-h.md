<span data-ttu-id="2a21e-101">建立部署認證以 hello [az webapp 部署使用者集合](/cli/azure/webapp/deployment/user#set)命令。</span><span class="sxs-lookup"><span data-stu-id="2a21e-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="2a21e-102">若為 FTP 和本機 Git 部署 tooa web 應用程式需要部署使用者。</span><span class="sxs-lookup"><span data-stu-id="2a21e-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="2a21e-103">hello 使用者名稱和密碼是帳戶層級。</span><span class="sxs-lookup"><span data-stu-id="2a21e-103">hello user name and password are account level.</span></span> <span data-ttu-id="2a21e-104">_它們與您的 Azure 訂用帳戶認證不同。_</span><span class="sxs-lookup"><span data-stu-id="2a21e-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="2a21e-105">下列命令，取代在 hello *\<使用者名稱 >*和*\<密碼 >*與新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2a21e-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="2a21e-106">hello 使用者名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="2a21e-106">hello user name must be unique.</span></span> <span data-ttu-id="2a21e-107">hello 密碼必須至少為八個字元，以下列三個元素的 hello 的兩個： 字母、 數字、 符號。</span><span class="sxs-lookup"><span data-stu-id="2a21e-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="2a21e-108">如果您收到` 'Conflict'. Details: 409`錯誤，變更 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2a21e-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="2a21e-109">如果您收到 ` 'Bad Request'. Details: 400` 錯誤，請使用更強的密碼。</span><span class="sxs-lookup"><span data-stu-id="2a21e-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="2a21e-110">您只需建立此部署使用者一次；可以用於所有 Azure 部署。</span><span class="sxs-lookup"><span data-stu-id="2a21e-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="2a21e-111">記錄 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2a21e-111">Record hello user name and password.</span></span> <span data-ttu-id="2a21e-112">您需要它們 toodeploy hello web 應用程式更新版本。</span><span class="sxs-lookup"><span data-stu-id="2a21e-112">You need them toodeploy hello web app later.</span></span>
>
>