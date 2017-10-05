---
title: "使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式 | Microsoft Docs"
description: "了解如何在 Azure App Service 中建立使用 Azure Active Directory 進行驗證的 ASP.NET MVC 特定業務應用程式"
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
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="17719-103">使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="17719-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="17719-104">本文說明如何在 [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) 中使用[驗證/授權](../app-service/app-service-authentication-overview.md)功能建立 .NET 企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="17719-105">文中也會說明如何在應用程式中使用 [Azure Active Directory 圖形 API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 來查詢目錄資料。</span><span class="sxs-lookup"><span data-stu-id="17719-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="17719-106">您所使用的 Azure Active Directory 租用戶可以是純 Azure 目錄。</span><span class="sxs-lookup"><span data-stu-id="17719-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="17719-107">或者，它可以[與您的內部部署 Active Directory 同步處理](../active-directory/active-directory-aadconnect.md)，以便為內部部署和遠端的工作者建立單一登入體驗。</span><span class="sxs-lookup"><span data-stu-id="17719-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="17719-108">本文使用 Azure 帳戶的預設目錄。</span><span class="sxs-lookup"><span data-stu-id="17719-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="17719-109">將建置的項目</span><span class="sxs-lookup"><span data-stu-id="17719-109">What you will build</span></span>
<span data-ttu-id="17719-110">您將在應用程式服務 Web Apps 中建置簡單的「建立/讀取/更新/刪除」(CRUD) 特定業務應用程式，它使用下列功能追蹤工作項目：</span><span class="sxs-lookup"><span data-stu-id="17719-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="17719-111">比對 Azure Active Directory 驗證使用者</span><span class="sxs-lookup"><span data-stu-id="17719-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="17719-112">使用 [Azure Active Directory 圖形 API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="17719-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="17719-113">使用 ASP.NET MVC 的「不需要驗證」  範本</span><span class="sxs-lookup"><span data-stu-id="17719-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="17719-114">如果您在 Azure 中的企業營運應用程式需要角色型存取控制 (RBAC)，請參閱 [後續步驟](#next)。</span><span class="sxs-lookup"><span data-stu-id="17719-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="17719-115">您需要什麼</span><span class="sxs-lookup"><span data-stu-id="17719-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="17719-116">您需要下列項目完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="17719-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="17719-117">Azure Active Directory 租用戶與不同的群組中的使用者</span><span class="sxs-lookup"><span data-stu-id="17719-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="17719-118">在 Azure Active Directory 租用戶建立應用程式的權限</span><span class="sxs-lookup"><span data-stu-id="17719-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="17719-119">Visual Studio 2013 Update 4 或更新版本</span><span class="sxs-lookup"><span data-stu-id="17719-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="17719-120">Azure SDK 2.8.1 或更新版本</span><span class="sxs-lookup"><span data-stu-id="17719-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="17719-121">對 Azure 建立和部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="17719-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="17719-122">從 Visual Studio，按一下 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="17719-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="17719-123">選取 [ASP.NET Web 應用程式]、為專案命名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="17719-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="17719-124">選取 [MVC] 範本，然後將驗證變更為 [不需要驗證]。</span><span class="sxs-lookup"><span data-stu-id="17719-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="17719-125">確定已選取 [雲端中的主機]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="17719-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="17719-126">在 [建立 App Service] 對話方塊中，按一下 [新增帳戶]\(然後是下拉式清單中的 [新增帳戶]) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="17719-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="17719-127">登入後，請設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-127">Once logged in configure your web app.</span></span> <span data-ttu-id="17719-128">建立資源群組和新的 App Service 方案，方法是按一下各自的 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="17719-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="17719-129">按一下 [瀏覽其他 Azure 服務]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="17719-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="17719-130">在 [服務] 索引標籤上，按一下 **[+]** 來為應用程式新增 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="17719-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="17719-131">在 [設定 SQL Database] 中，按一下 [新增] 以建立 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="17719-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="17719-132">在 [設定 SQL Server] 中，設定 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="17719-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="17719-133">然後依序按一下 [確定]、[確定] 和 [建立]，開始在 Azure 中建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="17719-134">在 [Azure App Service 活動] 中，當應用程式建立完成時您便會看到。</span><span class="sxs-lookup"><span data-stu-id="17719-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="17719-135">按一下 **[立即將&lt;應用程式名稱**> 發佈至此 Web 應用程式]，然後按一下[發佈]。</span><span class="sxs-lookup"><span data-stu-id="17719-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="17719-136">當 Visual Studio 完成後，它會在瀏覽器中開啟發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="17719-137">設定驗證和目錄存取</span><span class="sxs-lookup"><span data-stu-id="17719-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="17719-138">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="17719-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="17719-139">從左側功能表中，按一下 [應用程式服務] > **&lt;*應用程式名稱*>** > [驗證/授權]。</span><span class="sxs-lookup"><span data-stu-id="17719-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="17719-140">按一下 [於] > [Azure Active Directory] > [Express] > [確定] 以開啟 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="17719-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="17719-141">按一下命令列中的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="17719-141">Click **Save** in the command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="17719-142">成功儲存驗證設定後，請嘗試在瀏覽器中再次瀏覽至應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="17719-143">預設設定會強制對整個應用程式執行驗證。</span><span class="sxs-lookup"><span data-stu-id="17719-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="17719-144">如果您還未登入，系統會將您重新導向至登入畫面。</span><span class="sxs-lookup"><span data-stu-id="17719-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="17719-145">登入之後，您會看到應用程式已受到 HTTPS 的保護。</span><span class="sxs-lookup"><span data-stu-id="17719-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="17719-146">接著，您必須啟用目錄資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="17719-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="17719-147">瀏覽至 [傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="17719-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="17719-148">從左側功能表中，按一下 [Active Directory] > [預設目錄] > [應用程式] > **&lt;*應用程式名稱*>**。</span><span class="sxs-lookup"><span data-stu-id="17719-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="17719-149">這是 App Service 為您建立以便啟用授權/驗證功能的 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="17719-150">按一下 [使用者] 和 [群組] 以確定目錄中有一些使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="17719-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="17719-151">如果沒有，請建立一些測試使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="17719-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="17719-152">按一下 [設定]  以設定此應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="17719-153">向下捲動至 [金鑰]  區段，並選取持續時間來新增金鑰。</span><span class="sxs-lookup"><span data-stu-id="17719-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="17719-154">然後按一下 [委派的權限] 並選取 [讀取目錄資料]。</span><span class="sxs-lookup"><span data-stu-id="17719-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="17719-155">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="17719-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="17719-156">設定儲存好之後，往回捲動至 [金鑰] 區段，然後按一下 [複製] 按鈕以複製用戶端金鑰。</span><span class="sxs-lookup"><span data-stu-id="17719-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="17719-157">如果您現在離開此頁面，就無法再存取此用戶端金鑰。</span><span class="sxs-lookup"><span data-stu-id="17719-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="17719-158">接著，您必須使用此金鑰設定 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17719-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="17719-159">使用 Azure 帳戶登入 [Azure 資源總管](https://resources.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="17719-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="17719-160">在頁面頂端按一下 [讀取/寫入]  以在 Azure 資源總管中進行變更。</span><span class="sxs-lookup"><span data-stu-id="17719-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="17719-161">尋找應用程式的驗證設定，位置在 subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**。</span><span class="sxs-lookup"><span data-stu-id="17719-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="17719-162">按一下 [ **編輯**]。</span><span class="sxs-lookup"><span data-stu-id="17719-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="17719-163">在編輯窗格中，設定 `clientSecret` 和 `additionalLoginParams` 屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="17719-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="17719-164">按一下頂端的 [PUT]  以提交變更。</span><span class="sxs-lookup"><span data-stu-id="17719-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="17719-165">現在，若要測試是否有可供存取 Azure Active Directory 圖形 API 的授權權杖，請直接在瀏覽器中瀏覽到 **https://&lt;*appname*>.azurewebsites.net/.auth/me**。</span><span class="sxs-lookup"><span data-stu-id="17719-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="17719-166">如果一切設定皆正確，您應該會在 JSON 回應中看到 `access_token` 屬性。</span><span class="sxs-lookup"><span data-stu-id="17719-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="17719-167">`~/.auth/me` URL 路徑由 App Service 驗證/授權進行管理，以提供您與驗證的工作階段相關的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="17719-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="17719-168">如需詳細資訊，請參閱 [Azure App Service 中的驗證與授權](../app-service/app-service-authentication-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="17719-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="17719-169">`access_token` 具有到期期間。</span><span class="sxs-lookup"><span data-stu-id="17719-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="17719-170">不過，App Service 驗證/授權會以 `~/.auth/refresh`提供權杖重新整理功能。</span><span class="sxs-lookup"><span data-stu-id="17719-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="17719-171">如需其使用方式的詳細資訊，請參閱 [App Service 權杖存放區](https://cgillum.tech/2016/03/07/app-service-token-store/)。</span><span class="sxs-lookup"><span data-stu-id="17719-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="17719-172">接下來，您會使用目錄資料進行一些有用的操作。</span><span class="sxs-lookup"><span data-stu-id="17719-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="17719-173">將企業營運功能新增至應用程式</span><span class="sxs-lookup"><span data-stu-id="17719-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="17719-174">現在，您可以建立簡單的 CRUD 工作項目追蹤器。</span><span class="sxs-lookup"><span data-stu-id="17719-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="17719-175">在 ~\Models 資料夾中，建立稱為 WorkItem.cs 的類別檔案，並以下列程式碼取代 `public class WorkItem {...}`：</span><span class="sxs-lookup"><span data-stu-id="17719-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="17719-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="17719-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="17719-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="17719-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="17719-178">}</span><span class="sxs-lookup"><span data-stu-id="17719-178">}</span></span>
   
     <span data-ttu-id="17719-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="17719-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="17719-180">}</span><span class="sxs-lookup"><span data-stu-id="17719-180">}</span></span>
2. <span data-ttu-id="17719-181">建置專案，讓 Visual Studio 中的建構邏輯可存取新的模型。</span><span class="sxs-lookup"><span data-stu-id="17719-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="17719-182">將新的建構項目 `WorkItemsController` 新增至 ~\Controllers 資料夾 (以滑鼠右鍵按一下 [控制器]、指向 [新增]，然後選取 [新增建構項目])。</span><span class="sxs-lookup"><span data-stu-id="17719-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="17719-183">選取 [使用 Entity Framework，包含檢視的 MVC 5 控制器]，再按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="17719-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="17719-184">選取您建立的模型，接著依序按一下 **[+]** 和 [新增] 來新增資料內容，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="17719-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="17719-185">在 ~\Views\WorkItems\Create.cshtml (自動建構的項目) 中尋找 `Html.BeginForm` Helper 方法，並進行下列醒目提示的變更︰</span><span class="sxs-lookup"><span data-stu-id="17719-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
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
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
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
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="17719-186">請注意，`AadPicker` 物件會使用 `token` 和 `tenant` 來進行 Azure Active Directory 圖形 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="17719-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="17719-187">您稍後會新增 `AadPicker` 。</span><span class="sxs-lookup"><span data-stu-id="17719-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="17719-188">您也可以使用 `~/.auth/me`直接用戶端取得 `token` 和 `tenant`，但這會是額外的伺服器呼叫。</span><span class="sxs-lookup"><span data-stu-id="17719-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="17719-189">例如：</span><span class="sxs-lookup"><span data-stu-id="17719-189">For example:</span></span>
   > 
   > <span data-ttu-id="17719-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="17719-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="17719-191">對 ~\Views\WorkItems\Edit.cshtml 進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="17719-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="17719-192">`AadPicker` 物件定義在您必須新增至專案的指令碼中。</span><span class="sxs-lookup"><span data-stu-id="17719-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="17719-193">在 ~\Scripts 資料夾上按一下滑鼠右鍵、指向 [新增]，然後按一下 [JavaScript 檔案]。</span><span class="sxs-lookup"><span data-stu-id="17719-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="17719-194">輸入 `AadPickerLibrary` 做為檔名，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="17719-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="17719-195">從[這裡](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js)將內容複製到 ~\Scripts\AadPickerLibrary.js。</span><span class="sxs-lookup"><span data-stu-id="17719-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="17719-196">在指令碼中， `AadPicker` 物件會呼叫 [Azure Active Directory 圖形 API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 以搜尋符合輸入的使用者與群組。</span><span class="sxs-lookup"><span data-stu-id="17719-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="17719-197">~\Scripts\AadPickerLibrary.js 也會使用 [jQuery UI 自動完成 Widget](https://jqueryui.com/autocomplete/)。</span><span class="sxs-lookup"><span data-stu-id="17719-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="17719-198">因此，您需要將 jQuery UI 新增至專案。</span><span class="sxs-lookup"><span data-stu-id="17719-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="17719-199">以滑鼠右鍵按一下專案，然後按一下 [管理 NuGet 套件] 。</span><span class="sxs-lookup"><span data-stu-id="17719-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="17719-200">在 NuGet 套件管理員中按一下 [瀏覽]，在搜尋列中輸入 **jquery-ui**，然後按一下 [jQuery.UI.Combined]。</span><span class="sxs-lookup"><span data-stu-id="17719-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="17719-201">在右窗格中按一下 [安裝]，然後按一下 [確定] 繼續進行。</span><span class="sxs-lookup"><span data-stu-id="17719-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="17719-202">開啟 ~\App_Start\BundleConfig.cs，然後進行下列醒目提示的變更︰</span><span class="sxs-lookup"><span data-stu-id="17719-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
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
    
    <span data-ttu-id="17719-203">有更多高效能的方式可管理應用程式中的 JavaScript 和 CSS 檔案。</span><span class="sxs-lookup"><span data-stu-id="17719-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="17719-204">不過，為了簡單起見，你只會利用載入了每個檢視的套組。</span><span class="sxs-lookup"><span data-stu-id="17719-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="17719-205">最後，在 ~\Global.asax 中，於 `Application_Start()` 方法內新增下面這一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="17719-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="17719-206">`Ctrl`+`.` 來加以修正。</span><span class="sxs-lookup"><span data-stu-id="17719-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="17719-207">您需要這行程式碼，因為預設的 MVC 範本會在某些動作上使用 <code>[ValidateAntiForgeryToken]</code> 裝飾。</span><span class="sxs-lookup"><span data-stu-id="17719-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="17719-208">基於 [Brock Allen](https://twitter.com/BrockLAllen) 在 [MVC 4、AntiForgeryToken 和宣告](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/)中描述的行為，您的 HTTP POST 可能無法通過防偽權杖驗證，因為：</span><span class="sxs-lookup"><span data-stu-id="17719-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="17719-209">Azure Active Directory 不會傳送防偽權杖預設所需要的 http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider。</span><span class="sxs-lookup"><span data-stu-id="17719-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="17719-210">如果 Azure Active Directory 目錄與 AD FS 進行同步處理，AD FS 信任預設不會傳送 http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider 宣告，但您可以手動設定 AD FS 來傳送此宣告。</span><span class="sxs-lookup"><span data-stu-id="17719-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="17719-211">`ClaimTypes.NameIdentifies` 指定宣告 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`，而 Azure Active Directory 確實會提供此宣告。</span><span class="sxs-lookup"><span data-stu-id="17719-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="17719-212">現在，發佈您的變更。</span><span class="sxs-lookup"><span data-stu-id="17719-212">Now, publish your changes.</span></span> <span data-ttu-id="17719-213">以滑鼠右鍵按一下專案，然後按一下 [發佈] 。</span><span class="sxs-lookup"><span data-stu-id="17719-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="17719-214">按一下 [設定]，確定其中有 SQL Database 的連接字串，選取 [更新資料庫] 以變更模型的結構描述，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="17719-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="17719-215">在瀏覽器中，瀏覽至 https://&lt;appname>.azurewebsites.net/workitems，然後按一下 [建立新的]。</span><span class="sxs-lookup"><span data-stu-id="17719-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="17719-216">按一下 [AssignedToName]  方塊。</span><span class="sxs-lookup"><span data-stu-id="17719-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="17719-217">現在您應該可以在下拉式清單中看到 Azure Active Directory 租用戶中的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="17719-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="17719-218">您可以輸入以進行篩選，或使用 `Up` 或 `Down` 鍵，或是按一下以選取使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="17719-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="17719-219">按一下 [建立]  以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="17719-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="17719-220">然後，在建立的工作項目上按一下 [編輯]  來觀察相同的行為。</span><span class="sxs-lookup"><span data-stu-id="17719-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="17719-221">恭喜，您現在已使用目錄存取在 Azure 中執行企業營運應用程式！</span><span class="sxs-lookup"><span data-stu-id="17719-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="17719-222">圖形 API 還有其他更多用途。</span><span class="sxs-lookup"><span data-stu-id="17719-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="17719-223">請參閱 [Azure AD 圖形 API 參考](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog)。</span><span class="sxs-lookup"><span data-stu-id="17719-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="17719-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17719-224">Next Step</span></span>
<span data-ttu-id="17719-225">如果您在 Azure 中的企業營運應用程式需要角色型存取控制 (RBAC)，請參閱 [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) 以取得 Azure Active Directory 團隊提供的範例。</span><span class="sxs-lookup"><span data-stu-id="17719-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="17719-226">它會說明如何為 Azure Active Directory 應用程式啟用角色，然後使用 `[Authorize]` 裝飾授權使用者。</span><span class="sxs-lookup"><span data-stu-id="17719-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="17719-227">如果企業營運應用程式需要存取內部部署資料，請參閱 [在 Azure App Service 中使用混合式連線存取內部部署資源](web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="17719-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="17719-228">進一步資源</span><span class="sxs-lookup"><span data-stu-id="17719-228">Further resources</span></span>
* [<span data-ttu-id="17719-229">Azure App Service 中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="17719-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="17719-230">在 Azure 應用程式中使用內部部署 Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="17719-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="17719-231">在 Azure 中使用 AD FS 驗證建立企業營運應用程式</span><span class="sxs-lookup"><span data-stu-id="17719-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="17719-232">App Service 驗證和 Azure AD 圖形 API</span><span class="sxs-lookup"><span data-stu-id="17719-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="17719-233">Microsoft Azure Active Directory 範例與文件</span><span class="sxs-lookup"><span data-stu-id="17719-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="17719-234">Azure Active Directory 支援的權杖和宣告類型</span><span class="sxs-lookup"><span data-stu-id="17719-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
