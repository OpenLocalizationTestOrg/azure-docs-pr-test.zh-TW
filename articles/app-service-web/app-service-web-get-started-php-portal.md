---
title: "aaaDeploy hello 在五分鐘的 Azure 入口網站中的 WordPress 應用程式 |Microsoft 文件"
description: "了解如何輕鬆 toorun App Service 中的 web 應用程式部署的 WordPress 應用程式。 立即看到結果。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a><span data-ttu-id="01633-104">WordPress 中部署應用程式 hello Azure 入口網站在五分鐘</span><span class="sxs-lookup"><span data-stu-id="01633-104">Deploy a WordPress app in hello Azure portal in five minutes</span></span>

<span data-ttu-id="01633-105">本教學課程示範如何 toodeploy 您第一次[WordPress](https://wordpress.org/) web 應用程式太[Azure App Service](../app-service/app-service-value-prop-what-is.md)以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="01633-105">This tutorial shows you how toodeploy your first [WordPress](https://wordpress.org/) web app too[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress 網站](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="01633-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="01633-107">Prerequisites</span></span>
<span data-ttu-id="01633-108">您需要 Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="01633-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="01633-109">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="01633-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="01633-110">您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="01633-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="01633-111">建立起始應用程式，並玩的總 tooan 小時-沒有所需的信用卡，任何承諾。</span><span class="sxs-lookup"><span data-stu-id="01633-111">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-hello-wordpress-app"></a><span data-ttu-id="01633-112">部署 hello WordPress 應用程式</span><span class="sxs-lookup"><span data-stu-id="01633-112">Deploy hello WordPress app</span></span>
1. <span data-ttu-id="01633-113">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="01633-113">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="01633-114">開啟 [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress)。</span><span class="sxs-lookup"><span data-stu-id="01633-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="01633-115">此連結是快顯 tooimmediately hello Azure 入口網站中設定的新 WordPress 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01633-115">This link is a shortcut tooimmediately configure a new WordPress app in hello Azure portal.</span></span>

3. <span data-ttu-id="01633-116">在 [應用程式名稱] 中，輸入 Web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="01633-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="01633-117">您會看到綠色的核取記號，在 [hello] 方塊中，如果 hello 名稱是唯一在 hello`azurewebsites.net`網域。</span><span class="sxs-lookup"><span data-stu-id="01633-117">You will see a green checkmark in hello box if hello name is unique in hello `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="01633-118">在**資源群組**，按一下 [**建立新**新 toocreate[資源群組](../azure-resource-manager/resource-group-overview.md)，然後為它命名。</span><span class="sxs-lookup"><span data-stu-id="01633-118">In **Resource Group**, click **Create new** toocreate a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="01633-119">在 [資料庫提供者] 中，選取 [CleaDB]。</span><span class="sxs-lookup"><span data-stu-id="01633-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="01633-120">按一下 [App Service 方案/位置] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="01633-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="01633-121">設定 hello [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)所示：</span><span class="sxs-lookup"><span data-stu-id="01633-121">Configure hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="01633-122">在**App Service 方案**，型別 hello 所需的名稱。</span><span class="sxs-lookup"><span data-stu-id="01633-122">In **App Service plan**, type hello desired name.</span></span>
    - <span data-ttu-id="01633-123">在**位置**，選擇位置 toohost 您計劃。</span><span class="sxs-lookup"><span data-stu-id="01633-123">In **Location**, choose a location toohost your plan.</span></span>
    - <span data-ttu-id="01633-124">按一下 [定價層]，然後選取 [F1 免費] 或另一個適合您的層級，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="01633-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="01633-125">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="01633-125">Click **OK**.</span></span>

8. <span data-ttu-id="01633-126">按一下 [資料庫] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="01633-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="01633-127">設定 hello SQL 資料庫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="01633-127">Configure hello SQL Database as shown:</span></span>

    - <span data-ttu-id="01633-128">在 [資料庫名稱] 中，輸入資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="01633-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="01633-129">在**位置**，選擇 hello hello 應用程式服務計劃與相同的位置。</span><span class="sxs-lookup"><span data-stu-id="01633-129">In **Location**, choose hello same location as hello App Service plan.</span></span>
    - <span data-ttu-id="01633-130">按一下 [定價層]，然後選取 [Mercury] 或另一個適合您的層級，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="01633-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="01633-131">按一下 [法律條款]，然後按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="01633-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="01633-132">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="01633-132">Click **OK**.</span></span>

9. <span data-ttu-id="01633-133">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="01633-133">Click **Create**.</span></span>

    <span data-ttu-id="01633-134">Azure 現在會根據您的設定建立 WordPress 應用程式。</span><span class="sxs-lookup"><span data-stu-id="01633-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="01633-135">您應該會看到 [部署已開始...] 通知。</span><span class="sxs-lookup"><span data-stu-id="01633-135">You should see a **Deployment started...** notification.</span></span>

    ![已開始部署 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="01633-137">啟動和管理 WordPress Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="01633-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="01633-138">當 Azure 完成應用程式部署時，您會看到另一個通知。</span><span class="sxs-lookup"><span data-stu-id="01633-138">When Azure completes app deployment you see another notification.</span></span>

![已成功部署 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="01633-140">按一下 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="01633-140">Click hello notification.</span></span> <span data-ttu-id="01633-141">如果您遺漏了，您永遠可以存取它，即可 hello 通知鈴鐺 (![通知方-Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-dotnet-portal/notification.png))。</span><span class="sxs-lookup"><span data-stu-id="01633-141">If you missed it, you can always access it by clicking hello notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="01633-142">您現在應該會看到 Web 應用程式的管理[刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources) (*刀鋒視窗*︰水平開啟的入口網站頁面)。</span><span class="sxs-lookup"><span data-stu-id="01633-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="01633-143">在 [hello hello 概觀] 頁面頂端，按一下 [**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="01633-143">In hello top of hello Overview page, click **Browse**.</span></span>
   
    ![瀏覽 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="01633-145">現在您會看到 hello WordPress ** 褖畫惎**頁面。</span><span class="sxs-lookup"><span data-stu-id="01633-145">Now you see hello WordPress **Welcome** page.</span></span> <span data-ttu-id="01633-146">設定 hello WordPress 安裝和開始玩玩看 ！</span><span class="sxs-lookup"><span data-stu-id="01633-146">Configure hello WordPress installation and start playing with it!</span></span>

    ![WordPress 設定 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="01633-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="01633-148">Next steps</span></span>
* <span data-ttu-id="01633-149">[建立、 設定及部署 Laravel web 應用程式 tooAzure](app-service-web-php-get-started.md) -了解您需要 toorun 任何 PHP web 應用程式在 Azure 中，例如 hello 基本技巧：</span><span class="sxs-lookup"><span data-stu-id="01633-149">[Create, configure, and deploy a Laravel web app tooAzure](app-service-web-php-get-started.md) - Learn hello basic skills you need toorun any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="01633-150">從 PowerShell/Bash 在 Azure 中建立及設定 App。</span><span class="sxs-lookup"><span data-stu-id="01633-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="01633-151">設定 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="01633-151">Set PHP version.</span></span>
    * <span data-ttu-id="01633-152">使用不是 hello 應用程式根目錄中啟動檔案。</span><span class="sxs-lookup"><span data-stu-id="01633-152">Use a start file that is not in hello root application directory.</span></span>
    * <span data-ttu-id="01633-153">啟用編寫器自動化。</span><span class="sxs-lookup"><span data-stu-id="01633-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="01633-154">存取環境特有的變數。</span><span class="sxs-lookup"><span data-stu-id="01633-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="01633-155">針對常見錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="01633-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="01633-156">[部署您的應用程式服務的程式碼 tooAzure](web-sites-deploy.md)-了解如何 toodeploy 從 FTP 或從原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="01633-156">[Deploy your code tooAzure App Service](web-sites-deploy.md)- Learn how toodeploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="01633-157">[新增功能 tooyour 第一個 web 應用程式](app-service-web-get-started-2.md)-採用 Azure 應用程式 toohello 下一個層級。</span><span class="sxs-lookup"><span data-stu-id="01633-157">[Add functionality tooyour first web app](app-service-web-get-started-2.md) - Take your Azure app toohello next level.</span></span> <span data-ttu-id="01633-158">驗證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="01633-158">Authenticate your users.</span></span> <span data-ttu-id="01633-159">根據需求加以調整。</span><span class="sxs-lookup"><span data-stu-id="01633-159">Scale it based on demand.</span></span> <span data-ttu-id="01633-160">設定一些效能警示。</span><span class="sxs-lookup"><span data-stu-id="01633-160">Set up some performance alerts.</span></span> <span data-ttu-id="01633-161">都只要點幾下滑鼠就能完成。</span><span class="sxs-lookup"><span data-stu-id="01633-161">All with a few clicks.</span></span>
