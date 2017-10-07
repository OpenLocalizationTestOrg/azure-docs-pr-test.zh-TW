---
title: "aaaCreate 業務的 Azure 應用程式與 Azure Active Directory 驗證 |Microsoft 文件"
description: "深入了解如何在 Azure App Service 中 toocreate ASP.NET MVC 的特定業務應用程式，向 Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="649c3-103">使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="649c3-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="649c3-104">本文章將示範如何 toocreate.NET 的特定業務應用程式中[Azure App Service Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)使用 hello[驗證 / 授權](../app-service/app-service-authentication-overview.md)功能。</span><span class="sxs-lookup"><span data-stu-id="649c3-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="649c3-105">它也會示範如何 toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery hello 應用程式中的目錄資料。</span><span class="sxs-lookup"><span data-stu-id="649c3-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="649c3-106">您使用的 hello Azure Active Directory 租用戶可以是僅 Azure 」 的目錄。</span><span class="sxs-lookup"><span data-stu-id="649c3-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="649c3-107">或者，它可以是[與您在內部部署 Active Directory 同步處理](../active-directory/active-directory-aadconnect.md)toocreate 單一登入體驗的內部部署和遠端的背景工作。</span><span class="sxs-lookup"><span data-stu-id="649c3-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="649c3-108">本文使用 hello 預設目錄，為您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="649c3-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="649c3-109">將建置的項目</span><span class="sxs-lookup"><span data-stu-id="649c3-109">What you will build</span></span>
<span data-ttu-id="649c3-110">您將建置簡單的特定業務建立讀取更新與刪除 (CRUD) 應用程式，App Service Web 應用程式中追蹤工作項目，以 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="649c3-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="649c3-111">比對 Azure Active Directory 驗證使用者</span><span class="sxs-lookup"><span data-stu-id="649c3-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="649c3-112">使用 [Azure Active Directory 圖形 API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="649c3-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="649c3-113">使用 hello ASP.NET MVC*非驗證*範本</span><span class="sxs-lookup"><span data-stu-id="649c3-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="649c3-114">如果您在 Azure 中的企業營運應用程式需要角色型存取控制 (RBAC)，請參閱 [後續步驟](#next)。</span><span class="sxs-lookup"><span data-stu-id="649c3-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="649c3-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="649c3-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="649c3-116">本教學課程，您需要 hello 下列 toocomplete 中：</span><span class="sxs-lookup"><span data-stu-id="649c3-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="649c3-117">Azure Active Directory 租用戶與不同的群組中的使用者</span><span class="sxs-lookup"><span data-stu-id="649c3-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="649c3-118">Hello Azure Active Directory 租用戶上的權限 toocreate 應用程式</span><span class="sxs-lookup"><span data-stu-id="649c3-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="649c3-119">Visual Studio 2013 Update 4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="649c3-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="649c3-120">Azure SDK 2.8.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="649c3-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="649c3-121">建立及部署 web 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="649c3-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="649c3-122">從 Visual Studio，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="649c3-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="649c3-123">選取 [ASP.NET Web 應用程式]、為專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="649c3-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="649c3-124">選取 hello **MVC**範本，然後變更太 hello 驗證**非驗證**。</span><span class="sxs-lookup"><span data-stu-id="649c3-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="649c3-125">請確定**hello 雲端中的主機**已選取並按**確定**。</span><span class="sxs-lookup"><span data-stu-id="649c3-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="649c3-126">在 hello**建立 App Service**  對話方塊中，按一下**將帳戶加入**(然後**將帳戶加入**hello 下拉式清單中) toolog tooyour Azure 帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="649c3-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="649c3-127">登入後，請設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="649c3-127">Once logged in configure your web app.</span></span> <span data-ttu-id="649c3-128">建立資源群組和新的 App Service 方案，按一下個別的 hello**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="649c3-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="649c3-129">按一下**瀏覽其他 Azure 服務**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="649c3-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="649c3-130">在 hello**服務**索引標籤上，按一下   **+**  tooadd 應用程式的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="649c3-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="649c3-131">在**設定 SQL Database**，按一下 **新增**toocreate SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="649c3-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="649c3-132">在 [設定 SQL Server] 中，設定 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="649c3-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="649c3-133">然後按一下  **確定**，**確定**，和**建立**tookick hello Azure 中的應用程式建立功能。</span><span class="sxs-lookup"><span data-stu-id="649c3-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="649c3-134">在**Azure 應用程式服務活動**，您可以看到 hello 應用程式建立完成時。</span><span class="sxs-lookup"><span data-stu-id="649c3-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="649c3-135">按一下**發行&lt;* appname*> toothis Web 應用程式現在 * *，然後按一下 **發行**。</span><span class="sxs-lookup"><span data-stu-id="649c3-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="649c3-136">一旦完成 Visual Studio 時，它會開啟 hello hello 瀏覽器中發行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="649c3-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="649c3-137">設定驗證和目錄存取</span><span class="sxs-lookup"><span data-stu-id="649c3-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="649c3-138">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="649c3-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="649c3-139">從 hello 左窗格中，按一下 **應用程式服務** > **&lt;*appname*> * * >**驗證 / 授權**.</span><span class="sxs-lookup"><span data-stu-id="649c3-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="649c3-140">按一下 [於] > [Azure Active Directory] > [Express] > [確定] 以開啟 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="649c3-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="649c3-141">按一下**儲存**hello 命令列中。</span><span class="sxs-lookup"><span data-stu-id="649c3-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="649c3-142">已成功儲存 hello 驗證設定之後, 再試一次巡覽 tooyour 再次 hello 瀏覽器中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="649c3-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="649c3-143">您的預設設定強制執行 hello 整個應用程式為基礎的驗證。</span><span class="sxs-lookup"><span data-stu-id="649c3-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="649c3-144">如果您沒有已登入，您必須重新導向的 tooa 登入畫面。</span><span class="sxs-lookup"><span data-stu-id="649c3-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="649c3-145">登入之後，您會看到應用程式已受到 HTTPS 的保護。</span><span class="sxs-lookup"><span data-stu-id="649c3-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="649c3-146">接下來，您需要 tooenable 存取 toodirectory 資料。</span><span class="sxs-lookup"><span data-stu-id="649c3-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="649c3-147">瀏覽 toohello[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="649c3-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="649c3-148">從 hello 左窗格中，按一下  **Active Directory** > **預設目錄** > **應用程式** >   **&lt;* appname*> * *。</span><span class="sxs-lookup"><span data-stu-id="649c3-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="649c3-149">這是您 tooenable hello 授權的建立應用程式服務的 hello Azure Active Directory 應用程式 / 驗證功能。</span><span class="sxs-lookup"><span data-stu-id="649c3-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="649c3-150">按一下**使用者**和**群組**toomake 確定 hello 目錄中有某些使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="649c3-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="649c3-151">如果沒有，請建立一些測試使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="649c3-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="649c3-152">按一下**設定**tooconfigure 此應用程式。</span><span class="sxs-lookup"><span data-stu-id="649c3-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="649c3-153">捲動 toohello**金鑰**區段，然後選取 持續時間中加入的機碼。</span><span class="sxs-lookup"><span data-stu-id="649c3-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="649c3-154">然後按一下 [委派的權限] 並選取 [讀取目錄資料]。</span><span class="sxs-lookup"><span data-stu-id="649c3-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="649c3-155">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="649c3-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="649c3-156">在您的設定會儲存後，向上捲動回到 toohello**金鑰**區段，然後按一下 hello**複製**按鈕 toocopy hello 用戶端金鑰。</span><span class="sxs-lookup"><span data-stu-id="649c3-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="649c3-157">如果現在離開此頁面，您必須能夠 tooaccess 此用戶端金鑰過一次。</span><span class="sxs-lookup"><span data-stu-id="649c3-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="649c3-158">接下來，您需要 tooconfigure 您 web 應用程式與這個機碼。</span><span class="sxs-lookup"><span data-stu-id="649c3-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="649c3-159">登入 toohello [Azure 資源總管](https://resources.azure.com)與 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="649c3-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="649c3-160">在 hello hello 頁面頂端，按一下**讀/寫**toomake hello Azure 資源總管中的變更。</span><span class="sxs-lookup"><span data-stu-id="649c3-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="649c3-161">尋找您應用程式中，位於 訂用帳戶的驗證設定 hello >   **&lt;*訂用帳戶名稱*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * >**提供者** > **Microsoft.Web** > **網站** > **&lt;*appname*> * * > **config**  > **authsettings**。</span><span class="sxs-lookup"><span data-stu-id="649c3-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="649c3-162">按一下 [ **編輯**]。</span><span class="sxs-lookup"><span data-stu-id="649c3-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="649c3-163">在編輯窗格中的 hello，設定 hello`clientSecret`和`additionalLoginParams`，如下所示的屬性。</span><span class="sxs-lookup"><span data-stu-id="649c3-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="649c3-164">按一下**放**在 hello 頂端 toosubmit 您的變更。</span><span class="sxs-lookup"><span data-stu-id="649c3-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="649c3-165">現在，如果您擁有 hello 授權權杖 tooaccess hello Azure Active Directory Graph API，只要瀏覽至 tootest 才 **https://&lt;*appname*>.azurewebsites.net/.auth/me** 中的您瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="649c3-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="649c3-166">如果您的所有項目已正確設定，您應該會看見 hello `access_token` hello JSON 回應中的屬性。</span><span class="sxs-lookup"><span data-stu-id="649c3-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="649c3-167">hello `~/.auth/me` URL 路徑受應用程式服務驗證 / 授權 toogive 您所有的 hello 資訊相關 tooyour 驗證工作階段。</span><span class="sxs-lookup"><span data-stu-id="649c3-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="649c3-168">如需詳細資訊，請參閱 [Azure App Service 中的驗證與授權](../app-service/app-service-authentication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="649c3-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="649c3-169">hello`access_token`具有到期期間。</span><span class="sxs-lookup"><span data-stu-id="649c3-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="649c3-170">不過，App Service 驗證/授權會以 `~/.auth/refresh`提供權杖重新整理功能。</span><span class="sxs-lookup"><span data-stu-id="649c3-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="649c3-171">如需有關如何 toouse，請參閱[應用程式服務語彙基元存放區](https://cgillum.tech/2016/03/07/app-service-token-store/)。</span><span class="sxs-lookup"><span data-stu-id="649c3-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="649c3-172">接下來，您會使用目錄資料進行一些有用的操作。</span><span class="sxs-lookup"><span data-stu-id="649c3-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="649c3-173">新增的業務功能 tooyour 應用程式</span><span class="sxs-lookup"><span data-stu-id="649c3-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="649c3-174">現在，您可以建立簡單的 CRUD 工作項目追蹤器。</span><span class="sxs-lookup"><span data-stu-id="649c3-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="649c3-175">在 hello ~\Models 資料夾中，建立一個稱為 WorkItem.cs 的類別檔案，並取代`public class WorkItem {...}`以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="649c3-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="649c3-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="649c3-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="649c3-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="649c3-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="649c3-178">}</span><span class="sxs-lookup"><span data-stu-id="649c3-178">}</span></span>
   
     <span data-ttu-id="649c3-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="649c3-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="649c3-180">}</span><span class="sxs-lookup"><span data-stu-id="649c3-180">}</span></span>
2. <span data-ttu-id="649c3-181">建立 hello 專案 toomake 您新模型存取 toohello scaffolding 邏輯 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="649c3-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="649c3-182">加入新的 scaffold 項目`WorkItemsController`toohello ~\Controllers 資料夾 (以滑鼠右鍵按一下**控制器**，點太**新增**，然後選取**新的 scaffold 項目**)。</span><span class="sxs-lookup"><span data-stu-id="649c3-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="649c3-183">選取 [使用 Entity Framework，包含檢視的 MVC 5 控制器]，再按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="649c3-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="649c3-184">選取 hello 您所建立模型，然後按一下 **+** 然後**新增**tooadd 資料內容，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="649c3-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="649c3-185">在 ~\Views\WorkItems\Create.cshtml （自動 scaffold 項目），尋找 hello `Html.BeginForm` helper 方法，並進行下列反白顯示的變更的 hello:</span><span class="sxs-lookup"><span data-stu-id="649c3-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="649c3-186">請注意，`token`和`tenant`所使用的 hello`AadPicker`物件 toomake Azure Active Directory Graph API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="649c3-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="649c3-187">您稍後會新增 `AadPicker` 。</span><span class="sxs-lookup"><span data-stu-id="649c3-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="649c3-188">您也可以取得`token`和`tenant`從用戶端 hello 與`~/.auth/me`，但那是額外的伺服器呼叫。</span><span class="sxs-lookup"><span data-stu-id="649c3-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="649c3-189">例如：</span><span class="sxs-lookup"><span data-stu-id="649c3-189">For example:</span></span>
   > 
   > <span data-ttu-id="649c3-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="649c3-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="649c3-191">具有相同的變更進行 hello ~ \Views\WorkItems\Edit.cshtml。</span><span class="sxs-lookup"><span data-stu-id="649c3-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="649c3-192">hello`AadPicker`定義物件的指令碼中，您需要 tooadd tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="649c3-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="649c3-193">Hello ~\Scripts 資料夾上按一下滑鼠右鍵，指向太**新增**，然後按一下**JavaScript 檔案**。</span><span class="sxs-lookup"><span data-stu-id="649c3-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="649c3-194">型別`AadPickerLibrary`hello 檔案名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="649c3-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="649c3-195">複製 hello 內容從[這裡](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js)到 ~ \Scripts\AadPickerLibrary.js。</span><span class="sxs-lookup"><span data-stu-id="649c3-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="649c3-196">在 hello 指令碼 hello`AadPicker`物件會呼叫[Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch 使用者和群組的比對輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="649c3-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="649c3-197">~\Scripts\AadPickerLibrary.js 也會使用 hello [jQuery UI 自動完成 widget](https://jqueryui.com/autocomplete/)。</span><span class="sxs-lookup"><span data-stu-id="649c3-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="649c3-198">因此，您需要 tooadd jQuery UI tooyour 專案。</span><span class="sxs-lookup"><span data-stu-id="649c3-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="649c3-199">以滑鼠右鍵按一下專案，然後按一下 [管理 NuGet 套件] 。</span><span class="sxs-lookup"><span data-stu-id="649c3-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="649c3-200">在 hello NuGet 套件管理員中，按一下 瀏覽，類型**jquery ui**在 hello 搜尋列中，然後按一下**jQuery.UI.Combined**。</span><span class="sxs-lookup"><span data-stu-id="649c3-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="649c3-201">Hello 右窗格中，按一下 **安裝**，然後按一下 **確定**tooproceed。</span><span class="sxs-lookup"><span data-stu-id="649c3-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="649c3-202">開啟 ~\App_Start\BundleConfig.cs 然後進行下列反白顯示的變更的 hello:</span><span class="sxs-lookup"><span data-stu-id="649c3-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="649c3-203">有更多的高效能的方式 toomanage JavaScript 和 CSS 檔案中您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="649c3-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="649c3-204">不過，為了簡單起見就得 toopiggyback 上已用的每個檢視載入的 hello 組合。</span><span class="sxs-lookup"><span data-stu-id="649c3-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="649c3-205">最後，在 ~ \Global.asax，加入下列一行程式碼 hello hello`Application_Start()`方法。</span><span class="sxs-lookup"><span data-stu-id="649c3-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="649c3-206">`Ctrl`+`.`在每個命名的解析錯誤太修正此問題。</span><span class="sxs-lookup"><span data-stu-id="649c3-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="649c3-207">您需要這行程式碼，因為 hello 預設 MVC 範本使用<code>[ValidateAntiForgeryToken]</code>上某些 hello 動作裝飾。</span><span class="sxs-lookup"><span data-stu-id="649c3-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="649c3-208">因為所描述的 toohello 行為[Brock Allen](https://twitter.com/BrockLAllen)在[MVC 4、 AntiForgeryToken 和宣告](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/)HTTP POST 可能會因為失敗防偽語彙基元驗證：</span><span class="sxs-lookup"><span data-stu-id="649c3-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="649c3-209">Azure Active Directory 不會傳送 hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello 防偽語彙基元所需要的預設值。</span><span class="sxs-lookup"><span data-stu-id="649c3-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="649c3-210">如果 Azure Active Directory 與 AD FS 進行同步處理目錄，預設的 hello AD FS 信任不會傳送 hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider 宣告，雖然您可以手動設定 AD FS toosend這個宣告中。</span><span class="sxs-lookup"><span data-stu-id="649c3-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="649c3-211">`ClaimTypes.NameIdentifies`指定 hello 宣告`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`，Azure Active Directory 並提供它。</span><span class="sxs-lookup"><span data-stu-id="649c3-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="649c3-212">現在，發佈您的變更。</span><span class="sxs-lookup"><span data-stu-id="649c3-212">Now, publish your changes.</span></span> <span data-ttu-id="649c3-213">以滑鼠右鍵按一下專案，然後按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="649c3-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="649c3-214">按一下**設定**，請確定沒有連線字串 tooyour SQL 資料庫，選取**更新資料庫**toomake hello 為您的模型結構描述變更，然後按一下**發行**.</span><span class="sxs-lookup"><span data-stu-id="649c3-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="649c3-215">在 hello 瀏覽器中，瀏覽 toohttps: / /&lt;*appname*>.azurewebsites.net/workitems，然後按一下**新建**。</span><span class="sxs-lookup"><span data-stu-id="649c3-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="649c3-216">按一下 hello **AssignedToName**方塊。</span><span class="sxs-lookup"><span data-stu-id="649c3-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="649c3-217">現在您應該可以在下拉式清單中看到 Azure Active Directory 租用戶中的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="649c3-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="649c3-218">您可以輸入 toofilter，或使用 hello`Up`或`Down`索引鍵或按一下 tooselect hello 使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="649c3-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="649c3-219">按一下**建立**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="649c3-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="649c3-220">然後，按一下 **編輯**hello 建立工作項目 tooobserve hello 相同的行為。</span><span class="sxs-lookup"><span data-stu-id="649c3-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="649c3-221">恭喜，您現在已使用目錄存取在 Azure 中執行企業營運應用程式！</span><span class="sxs-lookup"><span data-stu-id="649c3-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="649c3-222">沒有更多您可以使用 hello Graph API 執行。</span><span class="sxs-lookup"><span data-stu-id="649c3-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="649c3-223">請參閱 [Azure AD 圖形 API 參考](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)。</span><span class="sxs-lookup"><span data-stu-id="649c3-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="649c3-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="649c3-224">Next Step</span></span>
<span data-ttu-id="649c3-225">如果您需要以角色為基礎的存取控制 (RBAC) 為您在 azure 中的特定業務應用程式，請參閱[WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)的 hello Azure Active Directory 團隊中的範例。</span><span class="sxs-lookup"><span data-stu-id="649c3-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="649c3-226">它為您示範如何為 Azure Active Directory 應用程式，tooenable 角色，然後再授權使用者以 hello`[Authorize]`裝飾。</span><span class="sxs-lookup"><span data-stu-id="649c3-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="649c3-227">如果您的特定業務應用程式需要存取 tooon 內部部署資料，請參閱[存取內部部署混合式連線使用 Azure App Service 中的資源](web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="649c3-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="649c3-228">進一步資源</span><span class="sxs-lookup"><span data-stu-id="649c3-228">Further resources</span></span>
* [<span data-ttu-id="649c3-229">Azure App Service 中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="649c3-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="649c3-230">在 Azure 應用程式中使用內部部署 Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="649c3-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="649c3-231">在 Azure 中使用 AD FS 驗證建立企業營運應用程式</span><span class="sxs-lookup"><span data-stu-id="649c3-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="649c3-232">應用程式服務快速地驗證並 hello Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="649c3-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="649c3-233">Microsoft Azure Active Directory 範例與文件</span><span class="sxs-lookup"><span data-stu-id="649c3-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="649c3-234">Azure Active Directory 支援的權杖和宣告類型</span><span class="sxs-lookup"><span data-stu-id="649c3-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
