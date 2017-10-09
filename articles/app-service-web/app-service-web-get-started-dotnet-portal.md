---
title: "aaaDeploy hello Azure 入口網站在五分鐘 Umbraco web 應用程式 |Microsoft 文件"
description: "了解如何輕鬆 toorun App Service 中的 web 應用程式部署範例 ASP.NET 應用程式。 立即看到結果。"
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
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="2c9a5-104">Umbraco web 應用程式在 hello Azure 入口網站部署在五分鐘</span><span class="sxs-lookup"><span data-stu-id="2c9a5-104">Deploy an Umbraco web app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="2c9a5-105">本教學課程可幫助您部署 n [Umbraco](https://our.umbraco.org/) web 應用程式太[Azure App Service](../app-service/app-service-value-prop-what-is.md)以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-105">This tutorial helps you deploy n [Umbraco](https://our.umbraco.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![Umbraco 應用程式](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a><span data-ttu-id="2c9a5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="2c9a5-107">Prerequisites</span></span>
<span data-ttu-id="2c9a5-108">您需要 Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="2c9a5-109">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="2c9a5-110">您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="2c9a5-111">建立起始應用程式，並玩的總 tooan 小時-沒有所需的信用卡，任何承諾。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-aspnet-app"></a><span data-ttu-id="2c9a5-112">部署 hello ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c9a5-112">Deploy hello ASP.NET app</span></span>
1. <span data-ttu-id="2c9a5-113">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2c9a5-114">開啟 [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS)。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-114">Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).</span></span>

    <span data-ttu-id="2c9a5-115">此連結是快顯 tooimmediately hello Azure 入口網站中設定新的 Umbraco 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-115">This link is a shortcut tooimmediately configure a new Umbraco app in hello Azure portal.</span></span>

3. <span data-ttu-id="2c9a5-116">在 [應用程式名稱] 中，輸入 Web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="2c9a5-117">您會看到綠色的核取記號，在 [hello] 方塊中，如果 hello 名稱是唯一在 hello`azurewebsites.net`網域。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="2c9a5-118">在**資源群組**，按一下 **建立新**新 toocreate[資源群組](../azure-resource-manager/resource-group-overview.md)，然後為它命名。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

7. <span data-ttu-id="2c9a5-119">按一下 [App Service 方案/位置] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-119">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="2c9a5-120">設定 hello [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)所示：</span><span class="sxs-lookup"><span data-stu-id="2c9a5-120">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="2c9a5-121">在**App Service 方案**，型別 hello 所需的名稱。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-121">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="2c9a5-122">在**位置**，選擇位置 toohost 您計劃。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-122">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="2c9a5-123">按一下 定價層，然後選取 F1 免費 或另一個適合您的層級，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-123">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="2c9a5-124">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-124">Click **OK**.</span></span>

    <span data-ttu-id="2c9a5-125">Umbraco CMS 設定現在看起來應該像下列螢幕擷取畫面的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c9a5-125">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![設定進行中 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. <span data-ttu-id="2c9a5-127">按一下 [SQL Database] > [建立新的資料庫]。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-127">Click **SQL Database** > **Create a new database**.</span></span> <span data-ttu-id="2c9a5-128">設定 hello SQL 資料庫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2c9a5-128">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="2c9a5-129">在 [名稱] 中輸入名稱，例如 **myDB**。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-129">In **Name**, type a name, such as **myDB**.</span></span>
    - <span data-ttu-id="2c9a5-130">按一下 定價層，然後選取 F 免費 或另一個適合您的層級，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-130">Click **Pricing tier**, then select **F Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="2c9a5-131">按一下 [目標伺服器] > [建立新的伺服器]。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-131">Click **Target server** > **Create a new server**.</span></span> <span data-ttu-id="2c9a5-132">Hello 資料庫伺服器設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2c9a5-132">Configure hello database server as shown:</span></span>

        - <span data-ttu-id="2c9a5-133">在 [伺服器名稱] 中，輸入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-133">In **Server name**, type a server name.</span></span> <span data-ttu-id="2c9a5-134">您會看到綠色的核取記號，在 [hello] 方塊中，如果 hello 名稱是唯一在 hello`.database.windows.net`網域。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-134">You will see a green checkmark in hello box if hello name is unique in hello `.database.windows.net` domain.</span></span>
        - <span data-ttu-id="2c9a5-135">在**Server 系統管理員登入**，型別 hello 需要系統管理員外的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-135">In **Server admin login**, type hello desired admininistrator username.</span></span>
        - <span data-ttu-id="2c9a5-136">在**密碼**和**確認密碼**，型別 hello 想要的密碼。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-136">In **Password** and **Confirm password**, type hello desired password.</span></span>
        - <span data-ttu-id="2c9a5-137">在位置中，選取 hello 您 hello web 應用程式所使用的相同位置。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-137">In Location, select hello same location you use for hello web app.</span></span>
        - <span data-ttu-id="2c9a5-138">請確定**允許 azure 服務 tooaccess 伺服器**已選取。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-138">Make sure **Allow azure services tooaccess server** is selected.</span></span>
        - <span data-ttu-id="2c9a5-139">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-139">Click **Select**.</span></span>
    
    - <span data-ttu-id="2c9a5-140">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-140">Click **Select**.</span></span>

13. <span data-ttu-id="2c9a5-141">按一下**Web 應用程式設定**，指定 hello 資料庫使用者名稱和密碼，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-141">Click **Web app settings**, specify hello database username and password, and click **OK**.</span></span>

    <span data-ttu-id="2c9a5-142">Umbraco CMS 設定現在看起來應該像下列螢幕擷取畫面的 hello:</span><span class="sxs-lookup"><span data-stu-id="2c9a5-142">Your Umbraco CMS configuration should now look like hello following screenshot:</span></span>

    ![設定完成 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. <span data-ttu-id="2c9a5-144">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-144">Click **Create**.</span></span>
    
    <span data-ttu-id="2c9a5-145">Azure 現在會根據您的設定建立 Umbraco 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-145">Azure now creates your Umbraco app based on your configuration.</span></span> <span data-ttu-id="2c9a5-146">您應該會看到 [部署已開始...] 通知。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-146">You should see a **Deployment started...** notification.</span></span>

    ![部署成功 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a><span data-ttu-id="2c9a5-148">啟動及管理您的 Umrbaco Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c9a5-148">Launch and manage your Umrbaco web app</span></span>

<span data-ttu-id="2c9a5-149">當 Azure 完成應用程式部署時，您會看到另一個通知。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-149">When Azure completes app deployment you see another notification.</span></span>

![部署成功 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. <span data-ttu-id="2c9a5-151">按一下 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-151">Click hello notification.</span></span> <span data-ttu-id="2c9a5-152">如果您遺漏了，您永遠可以存取它，即可 hello 通知鈴鐺 (![通知方-Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png))。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-152">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="2c9a5-153">您現在應該會看到 Web 應用程式的管理[刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources) (*刀鋒視窗*︰水平開啟的入口網站頁面)。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-153">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="2c9a5-154">在 hello hello 概觀 頁面頂端，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-154">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![瀏覽 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    <span data-ttu-id="2c9a5-156">現在您會看到 hello Umbraco ** 褖畫惎**頁面。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-156">Now you see hello Umbraco **Welcome** page.</span></span> <span data-ttu-id="2c9a5-157">設定 hello Umbraco 安裝和開始玩玩看 ！</span><span class="sxs-lookup"><span data-stu-id="2c9a5-157">Configure hello Umbraco installation and start playing with it!</span></span>

    ![Umbraco 設定 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="2c9a5-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c9a5-159">Next steps</span></span>
* <span data-ttu-id="2c9a5-160">[部署 ASP.NET web 應用程式 tooAzure 應用程式服務，使用 Visual Studio](app-service-web-get-started-dotnet.md) -了解如何 toocreate 新的 Azure web 應用程式，從 Visual Studio 中，使用 hello 其中包含應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-160">[Deploy an ASP.NET web app tooAzure App Service, using Visual Studio](app-service-web-get-started-dotnet.md) - Learn how toocreate a new Azure web app from Visual Studio, using any one of hello included application templates.</span></span>
* <span data-ttu-id="2c9a5-161">[部署您的應用程式服務的程式碼 tooAzure](web-sites-deploy.md)-了解如何 toodeploy 從 FTP 或從原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-161">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="2c9a5-162">[新增功能 tooyour 第一個 web 應用程式](app-service-web-get-started-2.md)-採用 Azure 應用程式 toohello 下一個層級。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-162">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="2c9a5-163">驗證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-163">Authenticate your users.</span></span> <span data-ttu-id="2c9a5-164">根據需求加以調整。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-164">Scale it based on demand.</span></span> <span data-ttu-id="2c9a5-165">設定一些效能警示。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-165">Set up some performance alerts.</span></span> <span data-ttu-id="2c9a5-166">都只要點幾下滑鼠就能完成。</span><span class="sxs-lookup"><span data-stu-id="2c9a5-166">All with a few clicks.</span></span>
