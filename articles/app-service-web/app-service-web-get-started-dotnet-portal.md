---
title: "五分鐘內在 Azure 入口網站中部署 Umbraco Web 應用程式 | Microsoft Docs"
description: "藉由部署範例 ASP.NET 應用程式，了解在 App Service 中執行 Web 應用程式有多麼簡單。 立即看到結果。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 9e3e2130a66cdfe5f06eb3b366e53028c44e7e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-umbraco-web-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="9bc4c-104">五分鐘內在 Azure 入口網站中部署 Umbraco Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bc4c-104">Deploy an Umbraco web app in the Azure portal in five minutes</span></span>

<span data-ttu-id="9bc4c-105">本教學課程將協助您在幾分鐘內將 n 個 [Umbraco](https://our.umbraco.org/) Web 應用程式部署至 [Azure App Service](../app-service/app-service-value-prop-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco 應用程式](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="9bc4c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="9bc4c-107">Prerequisites</span></span>
<span data-ttu-id="9bc4c-108">您需要 Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="9bc4c-109">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="9bc4c-110">您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="9bc4c-111">建立入門 App，並試用長達一小時。不需要信用卡，也不需簽定合約。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-aspnet-app"></a><span data-ttu-id="9bc4c-112">部署 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bc4c-112">Deploy the ASP.NET app</span></span>
1. <span data-ttu-id="9bc4c-113">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="9bc4c-114">開啟 [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS)。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="9bc4c-115">此連結是在 Azure 入口網站中立即設定新 Umbraco 應用程式的捷徑。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-115">This link is a shortcut to immediately configure a new Umbraco app in the Azure portal.</span></span>

3. <span data-ttu-id="9bc4c-116">在 [應用程式名稱] 中，輸入 Web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="9bc4c-117">如果名稱在 `azurewebsites.net` 網域中是唯一的，您將在方塊中看到綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="9bc4c-118">在 [資源群組] 中，按一下 [新建] 來建立新的[資源群組](../azure-resource-manager/resource-group-overview.md)，然後為它命名。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="9bc4c-119">按一下 [App Service 方案/位置] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="9bc4c-120">設定 [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bc4c-120">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="9bc4c-121">在 [App Service 方案] 中，輸入所需的名稱。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-121">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="9bc4c-122">在 [位置] 中，選擇要裝載方案的位置。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-122">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="9bc4c-123">按一下 [定價層]，然後選取 [F1 免費] 或另一個適合您的層級，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="9bc4c-124">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-124">Click **OK**.</span></span>

    <span data-ttu-id="9bc4c-125">Umbraco CMS 設定現在看起來應該類似下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="9bc4c-125">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![設定進行中 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="9bc4c-127">按一下 [SQL Database] > [建立新的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="9bc4c-128">設定 SQL Database，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bc4c-128">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="9bc4c-129">在 [名稱] 中輸入名稱，例如 **myDB**。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="9bc4c-130">按一下 [定價層]，然後選取 [F 免費] 或另一個適合您的層級，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="9bc4c-131">按一下 [目標伺服器] > [建立新的伺服器]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="9bc4c-132">設定資料庫伺服器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bc4c-132">Configure the database server as shown:</span></span>

        - <span data-ttu-id="9bc4c-133">在 [伺服器名稱] 中，輸入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="9bc4c-134">如果名稱在 `.database.windows.net` 網域中是唯一的，您將在方塊中看到綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-134">You will see a green checkmark in the box if the name is unique in the `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="9bc4c-135">在 [伺服器管理員登入] 中，輸入所需的管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-135">In **Server admin login**, type the desired admininistrator username.</span></span>
        - <span data-ttu-id="9bc4c-136">在 [密碼] 和 [確認密碼] 中，輸入所需的密碼。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-136">In **Password** and **Confirm password**, type the desired password.</span></span>
        - <span data-ttu-id="9bc4c-137">在 [位置] 中，選取 Web 應用程式所使用的相同位置。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-137">In Location, select the same location you use for the web app.</span></span>
        - <span data-ttu-id="9bc4c-138">確定已選取 [允許 Azure 服務存取伺服器]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-138">Make sure **Allow azure services to access server** is selected.</span></span>
        - <span data-ttu-id="9bc4c-139">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="9bc4c-140">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-140">Click **Select**.</span></span>

13. <span data-ttu-id="9bc4c-141">按一下 [Web 應用程式設定]、指定資料庫使用者名稱和密碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-141">Click **Web app settings**, specify the database username and password, and click **OK**.</span></span>

    <span data-ttu-id="9bc4c-142">Umbraco CMS 設定現在看起來應該類似下列螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="9bc4c-142">Your Umbraco CMS configuration should now look like the following screenshot:</span></span>

    ![設定完成 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="9bc4c-144">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-144">Click **Create**.</span></span>
    
    <span data-ttu-id="9bc4c-145">Azure 現在會根據您的設定建立 Umbraco 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="9bc4c-146">您應該會看到 [部署已開始...] 通知。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-146">You should see a **Deployment started...** notification.</span></span>

    ![部署成功 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="9bc4c-148">啟動及管理您的 Umrbaco Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bc4c-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="9bc4c-149">當 Azure 完成應用程式部署時，您會看到另一個通知。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-149">When Azure completes app deployment you see another notification.</span></span>

![部署成功 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="9bc4c-151">按一下通知。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-151">Click the notification.</span></span> <span data-ttu-id="9bc4c-152">如果您錯過了通知，一律可按一下通知鈴來存取該通知 (![通知鈴 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png))。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-152">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="9bc4c-153">您現在應該會看到 Web 應用程式的管理[刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources) (*刀鋒視窗*︰水平開啟的入口網站頁面)。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="9bc4c-154">在 [概觀] 頁面頂端，按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-154">In the top of the Overview page, click **Browse**.</span></span>
   
    ![瀏覽 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="9bc4c-156">現在您會看到 Umbraco 的 [歡迎使用] 頁面。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-156">Now you see the Umbraco **Welcome** page.</span></span> <span data-ttu-id="9bc4c-157">設定 Umbraco 安裝，然後開始使用！</span><span class="sxs-lookup"><span data-stu-id="9bc4c-157">Configure the Umbraco installation and start playing with it!</span></span>

    ![Umbraco 設定 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="9bc4c-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bc4c-159">Next steps</span></span>
* <span data-ttu-id="9bc4c-160">[使用 Visual Studio 將 ASP.NET Web 應用程式部署至 Azure App Service](app-service-web-get-started-dotnet.md) - 了解如何從 Visual Studio 中，使用任一個隨附的應用程式範本建立新的 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-160">[Deploy an ASP.NET web app to Azure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how to create a new Azure web app from Visual Studio, using any one of the included application templates.</span></span>
* <span data-ttu-id="9bc4c-161">[將程式碼部署至 Azure App Service](web-sites-deploy.md) - 了解如何從 FTP 或從原始檔控制儲存機制進行部署。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-161">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="9bc4c-162">[在您的第一個 Web 應用程式中新增功能](app-service-web-get-started-2.md) - 加強您 Azure App 的功能。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-162">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="9bc4c-163">驗證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-163">Authenticate your users.</span></span> <span data-ttu-id="9bc4c-164">根據需求加以調整。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-164">Scale it based on demand.</span></span> <span data-ttu-id="9bc4c-165">設定一些效能警示。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-165">Set up some performance alerts.</span></span> <span data-ttu-id="9bc4c-166">都只要點幾下滑鼠就能完成。</span><span class="sxs-lookup"><span data-stu-id="9bc4c-166">All with a few clicks.</span></span>
