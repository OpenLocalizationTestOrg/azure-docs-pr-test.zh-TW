---
title: "五分鐘內在 Azure 入口網站中部署 WordPress 應用程式 | Microsoft Docs"
description: "藉由部署 WordPress 應用程式，了解在 App Service 中執行 Web 應用程式有多麼簡單。 立即看到結果。"
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
ms.openlocfilehash: ef3be9823384bd8dc978c86f5cfde00d1117c4a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-wordpress-app-in-the-azure-portal-in-five-minutes"></a><span data-ttu-id="f39a0-104">五分鐘內在 Azure 入口網站中部署 WordPress 應用程式</span><span class="sxs-lookup"><span data-stu-id="f39a0-104">Deploy a WordPress app in the Azure portal in five minutes</span></span>

<span data-ttu-id="f39a0-105">本教學課程示範如何在幾分鐘內，將您的第一個 [WordPress](https://wordpress.org/) Web 應用程式部署至 [Azure App Service](../app-service/app-service-value-prop-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="f39a0-105">This tutorial shows you how to deploy your first [WordPress](https://wordpress.org/) web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in minutes.</span></span>

![WordPress 網站](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a><span data-ttu-id="f39a0-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="f39a0-107">Prerequisites</span></span>
<span data-ttu-id="f39a0-108">您需要 Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f39a0-108">You need a Microsoft Azure account.</span></span> <span data-ttu-id="f39a0-109">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="f39a0-109">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="f39a0-110">您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f39a0-110">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="f39a0-111">建立入門 App，並試用長達一小時。不需要信用卡，也不需簽定合約。</span><span class="sxs-lookup"><span data-stu-id="f39a0-111">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="deploy-the-wordpress-app"></a><span data-ttu-id="f39a0-112">部署 WordPress 應用程式</span><span class="sxs-lookup"><span data-stu-id="f39a0-112">Deploy the WordPress app</span></span>
1. <span data-ttu-id="f39a0-113">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f39a0-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f39a0-114">開啟 [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress)。</span><span class="sxs-lookup"><span data-stu-id="f39a0-114">Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).</span></span>

    <span data-ttu-id="f39a0-115">此連結是在 Azure 入口網站中立即設定新 WordPress 應用程式的捷徑。</span><span class="sxs-lookup"><span data-stu-id="f39a0-115">This link is a shortcut to immediately configure a new WordPress app in the Azure portal.</span></span>

3. <span data-ttu-id="f39a0-116">在 [應用程式名稱] 中，輸入 Web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="f39a0-116">In **App name**, type a web app name.</span></span> <span data-ttu-id="f39a0-117">如果名稱在 `azurewebsites.net` 網域中是唯一的，您將在方塊中看到綠色核取記號。</span><span class="sxs-lookup"><span data-stu-id="f39a0-117">You will see a green checkmark in the box if the name is unique in the `azurewebsites.net` domain.</span></span>
   
5. <span data-ttu-id="f39a0-118">在 [資源群組] 中，按一下 [新建] 來建立新的[資源群組](../azure-resource-manager/resource-group-overview.md)，然後為它命名。</span><span class="sxs-lookup"><span data-stu-id="f39a0-118">In **Resource Group**, click **Create new** to create a new [resource group](../azure-resource-manager/resource-group-overview.md), then give it a name.</span></span>

6. <span data-ttu-id="f39a0-119">在 [資料庫提供者] 中，選取 [CleaDB]。</span><span class="sxs-lookup"><span data-stu-id="f39a0-119">In **Database Provider**, select **CleaDB**.</span></span>

7. <span data-ttu-id="f39a0-120">按一下 [App Service 方案/位置] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="f39a0-120">Click **App Service plan/Location** > **Create New**.</span></span> <span data-ttu-id="f39a0-121">設定 [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f39a0-121">Configure the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) as shown:</span></span>

    - <span data-ttu-id="f39a0-122">在 [App Service 方案] 中，輸入所需的名稱。</span><span class="sxs-lookup"><span data-stu-id="f39a0-122">In **App Service plan**, type the desired name.</span></span>
    - <span data-ttu-id="f39a0-123">在 [位置] 中，選擇要裝載方案的位置。</span><span class="sxs-lookup"><span data-stu-id="f39a0-123">In **Location**, choose a location to host your plan.</span></span>
    - <span data-ttu-id="f39a0-124">按一下 [定價層]，然後選取 [F1 免費] 或另一個適合您的層級，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="f39a0-124">Click **Pricing tier**, then select **F1 Free** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f39a0-125">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f39a0-125">Click **OK**.</span></span>

8. <span data-ttu-id="f39a0-126">按一下 [資料庫] > [新建]。</span><span class="sxs-lookup"><span data-stu-id="f39a0-126">Click **Database** > **Create New**.</span></span> <span data-ttu-id="f39a0-127">設定 SQL Database，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f39a0-127">Configure the SQL Database as shown:</span></span>

    - <span data-ttu-id="f39a0-128">在 [資料庫名稱] 中，輸入資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="f39a0-128">In **Database Name**, type a database name.</span></span> 
    - <span data-ttu-id="f39a0-129">在 [位置] 中，選擇與 App Service 方案相同的位置。</span><span class="sxs-lookup"><span data-stu-id="f39a0-129">In **Location**, choose the same location as the App Service plan.</span></span>
    - <span data-ttu-id="f39a0-130">按一下 [定價層]，然後選取 [Mercury] 或另一個適合您的層級，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="f39a0-130">Click **Pricing tier**, then select **Mercury** or another tier that suits you, and then click **Select**.</span></span>
    - <span data-ttu-id="f39a0-131">按一下 [法律條款]，然後按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="f39a0-131">Click **Legal Terms** and click **Purchase**.</span></span>
    - <span data-ttu-id="f39a0-132">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f39a0-132">Click **OK**.</span></span>

9. <span data-ttu-id="f39a0-133">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f39a0-133">Click **Create**.</span></span>

    <span data-ttu-id="f39a0-134">Azure 現在會根據您的設定建立 WordPress 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f39a0-134">Azure now creates your WordPress app based on your configuration.</span></span> <span data-ttu-id="f39a0-135">您應該會看到 [部署已開始...] 通知。</span><span class="sxs-lookup"><span data-stu-id="f39a0-135">You should see a **Deployment started...** notification.</span></span>

    ![已開始部署 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="f39a0-137">啟動和管理 WordPress Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f39a0-137">Launch and manage your WordPress web app</span></span>

<span data-ttu-id="f39a0-138">當 Azure 完成應用程式部署時，您會看到另一個通知。</span><span class="sxs-lookup"><span data-stu-id="f39a0-138">When Azure completes app deployment you see another notification.</span></span>

![已成功部署 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. <span data-ttu-id="f39a0-140">按一下通知。</span><span class="sxs-lookup"><span data-stu-id="f39a0-140">Click the notification.</span></span> <span data-ttu-id="f39a0-141">如果您錯過了通知，一律可按一下通知鈴來存取該通知 (![通知鈴 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-dotnet-portal/notification.png))。</span><span class="sxs-lookup"><span data-stu-id="f39a0-141">If you missed it, you can always access it by clicking the notification bell (![Notification bellow - first WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).</span></span>

    <span data-ttu-id="f39a0-142">您現在應該會看到 Web 應用程式的管理[刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources) (*刀鋒視窗*︰水平開啟的入口網站頁面)。</span><span class="sxs-lookup"><span data-stu-id="f39a0-142">You should now see your web app's management [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) (*blade*: a portal page that opens horizontally).</span></span>

3. <span data-ttu-id="f39a0-143">在 [概觀] 頁面頂端，按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="f39a0-143">In the top of the Overview page, click **Browse**.</span></span>
   
    ![瀏覽 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/browse.png)

    <span data-ttu-id="f39a0-145">現在您會看到 WordPress 的 [歡迎使用] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f39a0-145">Now you see the WordPress **Welcome** page.</span></span> <span data-ttu-id="f39a0-146">設定 WordPress 安裝，然後開始使用！</span><span class="sxs-lookup"><span data-stu-id="f39a0-146">Configure the WordPress installation and start playing with it!</span></span>

    ![WordPress 設定 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a><span data-ttu-id="f39a0-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f39a0-148">Next steps</span></span>
* <span data-ttu-id="f39a0-149">[建立、設定和部署 PHP Web 應用程式至 Azure](app-service-web-php-get-started.md) - 了解您在 Azure 中執行任何 PHP Web 應用程式所需的基本技巧，例如：</span><span class="sxs-lookup"><span data-stu-id="f39a0-149">[Create, configure, and deploy a Laravel web app to Azure](app-service-web-php-get-started.md) - Learn the basic skills you need to run any PHP web app in Azure, such as:</span></span>

    * <span data-ttu-id="f39a0-150">從 PowerShell/Bash 在 Azure 中建立及設定 App。</span><span class="sxs-lookup"><span data-stu-id="f39a0-150">Create and configure apps in Azure from PowerShell/Bash.</span></span>
    * <span data-ttu-id="f39a0-151">設定 PHP 版本。</span><span class="sxs-lookup"><span data-stu-id="f39a0-151">Set PHP version.</span></span>
    * <span data-ttu-id="f39a0-152">使用不在應用程式根目錄中的啟動檔案。</span><span class="sxs-lookup"><span data-stu-id="f39a0-152">Use a start file that is not in the root application directory.</span></span>
    * <span data-ttu-id="f39a0-153">啟用編寫器自動化。</span><span class="sxs-lookup"><span data-stu-id="f39a0-153">Enable Composer automation.</span></span>
    * <span data-ttu-id="f39a0-154">存取環境特有的變數。</span><span class="sxs-lookup"><span data-stu-id="f39a0-154">Access environment-specific variables.</span></span>
    * <span data-ttu-id="f39a0-155">針對常見錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="f39a0-155">Troubleshoot common errors.</span></span>

* <span data-ttu-id="f39a0-156">[將程式碼部署至 Azure App Service](web-sites-deploy.md) - 了解如何從 FTP 或從原始檔控制儲存機制進行部署。</span><span class="sxs-lookup"><span data-stu-id="f39a0-156">[Deploy your code to Azure App Service](web-sites-deploy.md)- Learn how to deploy from FTP or from source control repositories.</span></span>
* <span data-ttu-id="f39a0-157">[在您的第一個 Web 應用程式中新增功能](app-service-web-get-started-2.md) - 加強您 Azure App 的功能。</span><span class="sxs-lookup"><span data-stu-id="f39a0-157">[Add functionality to your first web app](app-service-web-get-started-2.md) - Take your Azure app to the next level.</span></span> <span data-ttu-id="f39a0-158">驗證您的使用者。</span><span class="sxs-lookup"><span data-stu-id="f39a0-158">Authenticate your users.</span></span> <span data-ttu-id="f39a0-159">根據需求加以調整。</span><span class="sxs-lookup"><span data-stu-id="f39a0-159">Scale it based on demand.</span></span> <span data-ttu-id="f39a0-160">設定一些效能警示。</span><span class="sxs-lookup"><span data-stu-id="f39a0-160">Set up some performance alerts.</span></span> <span data-ttu-id="f39a0-161">都只要點幾下滑鼠就能完成。</span><span class="sxs-lookup"><span data-stu-id="f39a0-161">All with a few clicks.</span></span>
