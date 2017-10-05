---
title: "從行動服務升級為 Azure App Service - Node.js"
description: "了解如何輕鬆地將您的行動服務應用程式升級為 App Service 行動 App"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ce0572e85c258aa377c3eea7923d43a30c935bb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-to-app-service"></a><span data-ttu-id="0afde-103">將您現有的 Node.js Azure 行動服務升級為 App Service</span><span class="sxs-lookup"><span data-stu-id="0afde-103">Upgrade your existing Node.js Azure Mobile Service to App Service</span></span>
<span data-ttu-id="0afde-104">App Service Mobile 是一種使用 Microsoft Azure 建置行動應用程式的新方式。</span><span class="sxs-lookup"><span data-stu-id="0afde-104">App Service Mobile is a new way to build mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="0afde-105">若要深入了解，請參閱 [何謂 Mobile Apps？]</span><span class="sxs-lookup"><span data-stu-id="0afde-105">To learn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="0afde-106">本主題說明如何將現有的 Node.js 後端應用程式從 Azure 行動服務升級為新的 App Service Mobile Apps。</span><span class="sxs-lookup"><span data-stu-id="0afde-106">This topic describes how to upgrade an existing Node.js backend application from Azure Mobile Services to a new App Service Mobile Apps.</span></span> <span data-ttu-id="0afde-107">執行此升級時，您現有的行動服務應用程式可以繼續運作。</span><span class="sxs-lookup"><span data-stu-id="0afde-107">While you perform this upgrade, your existing Mobile Services application can continue to operate.</span></span>  <span data-ttu-id="0afde-108">如果您需要升級 Node.js 後端應用程式，請參閱[升級 .NET 行動服務](app-service-mobile-net-upgrading-from-mobile-services.md)。</span><span class="sxs-lookup"><span data-stu-id="0afde-108">If you need to upgrade a Node.js backend application, refer to [Upgrading your .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="0afde-109">當行動後端升級為 Azure App Service 時，就會具備所有 App Service 功能的存取權，而且會根據 [App Service 定價]而不是行動服務定價進行計費。</span><span class="sxs-lookup"><span data-stu-id="0afde-109">When a mobile backend is upgraded to Azure App Service, it has access to all App Service features and are billed according to [App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="0afde-110">移轉與升級</span><span class="sxs-lookup"><span data-stu-id="0afde-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="0afde-111">建議您在升級之前，先 [執行移轉](app-service-mobile-migrating-from-mobile-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="0afde-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="0afde-112">如此一來，您就能夠在同一個 App Service 方案中放置兩個版本的應用程式，而不需支付額外成本。</span><span class="sxs-lookup"><span data-stu-id="0afde-112">This way, you can put both versions of your application on the same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a><span data-ttu-id="0afde-113">Mobile Apps Node.js 伺服器 SDK 中的改進功能</span><span class="sxs-lookup"><span data-stu-id="0afde-113">Improvements in Mobile Apps Node.js server SDK</span></span>
<span data-ttu-id="0afde-114">升級至新的 [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) 提供了許多改進功能，包括：</span><span class="sxs-lookup"><span data-stu-id="0afde-114">Upgrading to the new [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) provides a lot of improvements, including:</span></span>

* <span data-ttu-id="0afde-115">根據 [Express 架構](http://expressjs.com/en/index.html)，新的節點 SDK 是輕量型，而其設計目的是在它們發佈時可以跟上新的節點版本。</span><span class="sxs-lookup"><span data-stu-id="0afde-115">Based on the [Express framework](http://expressjs.com/en/index.html), the new Node SDK is light-weight and designed to keep up with new Node versions as they come out.</span></span> <span data-ttu-id="0afde-116">您可以利用 Express 中介軟體來自訂應用程式行為。</span><span class="sxs-lookup"><span data-stu-id="0afde-116">You can customize the application behavior with Express middleware.</span></span>
* <span data-ttu-id="0afde-117">相較於行動服務 SDK，有顯著的效能改進。</span><span class="sxs-lookup"><span data-stu-id="0afde-117">Significant performance improvements compared to the Mobile Services SDK.</span></span>
* <span data-ttu-id="0afde-118">您現在可以將網站和您的行動後端裝載在一起。同樣地，很容易就能將 Azure Mobile SDK 新增至任何現有的 express.v4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0afde-118">You can now host a website together with your mobile backend; similarly, it's easy to add the Azure Mobile SDK to any existing express.v4 application.</span></span>
* <span data-ttu-id="0afde-119">Mobile Apps SDK 是建置來進行跨平台和本機開發，可在 Windows、Linux 和 OSX 平台上進行本機開發與執行。</span><span class="sxs-lookup"><span data-stu-id="0afde-119">Built for cross-platform and local development, the Mobile Apps SDK can be developed and run locally on Windows, Linux, and OSX platforms.</span></span> <span data-ttu-id="0afde-120">現在常見的節點開發技術非常容易使用，像是在部署之前執行 [Mocha](https://mochajs.org/) 測試。</span><span class="sxs-lookup"><span data-stu-id="0afde-120">It's now easy to use common Node development techniques like running [Mocha](https://mochajs.org/) tests prior to deployment.</span></span>

## <span data-ttu-id="0afde-121"><a name="overview"></a>基本升級概觀</span><span class="sxs-lookup"><span data-stu-id="0afde-121"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="0afde-122">為了協助升級 Node.js 後端，Azure App Service 提供了相容性套件。</span><span class="sxs-lookup"><span data-stu-id="0afde-122">To aid in upgrading a Node.js backend, Azure App Service has provided a compatibility package.</span></span>  <span data-ttu-id="0afde-123">在升級之後，您將會擁有可部署到新的 App Service 網站的新網站。</span><span class="sxs-lookup"><span data-stu-id="0afde-123">After upgrade, you will have a niew site that can be deployed to a new App Service site.</span></span>

<span data-ttu-id="0afde-124">行動服務用戶端 SDK 與新的 Mobile Apps 伺服器 SDK「不」  相容。</span><span class="sxs-lookup"><span data-stu-id="0afde-124">The Mobile Services client SDKs are **not** compatible with the new Mobile Apps server SDK.</span></span> <span data-ttu-id="0afde-125">為了提供您應用程式的服務持續性，您不應該將變更發佈至目前正在服務已發佈之用戶端的網站。</span><span class="sxs-lookup"><span data-stu-id="0afde-125">In order to provide continuity of service for your app, you should not publish changes to a site currently serving published clients.</span></span> <span data-ttu-id="0afde-126">而是應該建立新的行動應用程式做為重複項目。</span><span class="sxs-lookup"><span data-stu-id="0afde-126">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="0afde-127">您可以在同一個 App Service 方案中放置此應用程式，以避免產生額外的財務成本。</span><span class="sxs-lookup"><span data-stu-id="0afde-127">You can put this application on the same App Service plan to avoid incurring additional financial cost.</span></span>

<span data-ttu-id="0afde-128">您之後會有兩個版本的應用程式：一個維持不變並為已發佈的現有應用程式提供服務，另一個則可升級且目標為新的用戶端版本。</span><span class="sxs-lookup"><span data-stu-id="0afde-128">You will then have two versions of the application: one that stays the same and serves published apps in the wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="0afde-129">您可依自己的步調移動並測試程式碼，但應該確定您所進行的任何錯誤修正都會套用到這兩個版本。</span><span class="sxs-lookup"><span data-stu-id="0afde-129">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied to both.</span></span> <span data-ttu-id="0afde-130">當您覺得已將現有用戶端 app 的所需數量升級到最新版本，就可以視需要刪除原本移轉的 app。</span><span class="sxs-lookup"><span data-stu-id="0afde-130">Once you feel that a desired number of client apps in the wild have updated to the latest version, you can delete the original migrated app if you desire.</span></span> <span data-ttu-id="0afde-131">如果裝載於與您行動 app 相同的 App Service 方案中，就不會產生任何額外的金錢成本。</span><span class="sxs-lookup"><span data-stu-id="0afde-131">It doesn't incur any additional monetary costs, if hosted in the same App Service plan as your Mobile App.</span></span>

<span data-ttu-id="0afde-132">完整的升級程序大致如下：</span><span class="sxs-lookup"><span data-stu-id="0afde-132">The full outline for the upgrade process is as follows:</span></span>

1. <span data-ttu-id="0afde-133">下載您現有的 (已移轉) Azure 行動服務。</span><span class="sxs-lookup"><span data-stu-id="0afde-133">Download your existing (migrated) Azure Mobile Service.</span></span>
2. <span data-ttu-id="0afde-134">使用相容性套件將專案轉換至 Azure 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0afde-134">Convert the project to an Azure Mobile App using the compatibility package.</span></span>
3. <span data-ttu-id="0afde-135">更正任何差異 (例如驗證設定)。</span><span class="sxs-lookup"><span data-stu-id="0afde-135">Correct any differences (such as authentication settings).</span></span>
4. <span data-ttu-id="0afde-136">將轉換後的 Azure 行動應用程式專案部署到新的 App Service。</span><span class="sxs-lookup"><span data-stu-id="0afde-136">Deploy your converted Azure Mobile App project to a new App Service.</span></span>
5. <span data-ttu-id="0afde-137">發行使用新的行動應用程式的新版用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="0afde-137">Release a new version of your client application that use the new Mobile App.</span></span>
6. <span data-ttu-id="0afde-138">(可省略) 刪除您已移轉的原始行動服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="0afde-138">(Optional) Delete your original migrated mobile service app.</span></span>

<span data-ttu-id="0afde-139">當已移轉的原始行動服務沒有任何流量時，就能加以刪除。</span><span class="sxs-lookup"><span data-stu-id="0afde-139">Deletion can occur when you don't see any traffic on your original migrated mobile service.</span></span>

## <span data-ttu-id="0afde-140"><a name="install-npm-package"></a> 安裝必要元件</span><span class="sxs-lookup"><span data-stu-id="0afde-140"><a name="install-npm-package"></a> Install the Pre-requisites</span></span>
<span data-ttu-id="0afde-141">您應該在本機電腦上安裝 [節點]。</span><span class="sxs-lookup"><span data-stu-id="0afde-141">You should install [Node] on your local machine.</span></span>  <span data-ttu-id="0afde-142">您也應該安裝相容性套件。</span><span class="sxs-lookup"><span data-stu-id="0afde-142">You should also install the compatibility package.</span></span>  <span data-ttu-id="0afde-143">安裝了節點之後，您可以從新的 cmd 或 PowerShell 命令提示字元執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="0afde-143">After Node is installed, you can run the following command from a new cmd or PowerShell prompt:</span></span>

```npm i -g azure-mobile-apps-compatibility```

## <span data-ttu-id="0afde-144"><a name="obtain-ams-scripts"></a> 取得 Azure 行動服務指令碼</span><span class="sxs-lookup"><span data-stu-id="0afde-144"><a name="obtain-ams-scripts"></a> Obtain your Azure Mobile Services Scripts</span></span>
* <span data-ttu-id="0afde-145">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="0afde-145">Log in to the [Azure Portal].</span></span>
* <span data-ttu-id="0afde-146">使用 [所有資源] 或 [應用程式服務]，尋找您的行動服務網站。</span><span class="sxs-lookup"><span data-stu-id="0afde-146">Using **All Resources** or **App Services**, find your Mobile Services site.</span></span>
* <span data-ttu-id="0afde-147">在網站內按一下 [工具] -> [Kudu] -> [執行] 以開啟 Kudu 網站。</span><span class="sxs-lookup"><span data-stu-id="0afde-147">Within the site, click on **Tools** -> **Kudu** -> **Go** to open the Kudu site.</span></span>
* <span data-ttu-id="0afde-148">按一下 [偵錯主控台] -> [PowerShell] 以開啟偵錯主控台。</span><span class="sxs-lookup"><span data-stu-id="0afde-148">Click on **Debug Console** -> **PowerShell** to open the Debug console.</span></span>
* <span data-ttu-id="0afde-149">輪流按一下每個目錄以瀏覽至 `site/wwwroot/App_Data/config`</span><span class="sxs-lookup"><span data-stu-id="0afde-149">Navigate to `site/wwwroot/App_Data/config` by clicking on each directory in turn</span></span>
* <span data-ttu-id="0afde-150">按一下 `scripts` 目錄旁的 [下載] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0afde-150">Click on the download icon next to the `scripts` directory.</span></span>

<span data-ttu-id="0afde-151">這會下載 ZIP 格式的指令碼。</span><span class="sxs-lookup"><span data-stu-id="0afde-151">This will download the scripts in ZIP format.</span></span>  <span data-ttu-id="0afde-152">在本機電腦上建立新的目錄，並在該目錄內解壓縮 `scripts.ZIP` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0afde-152">Create a new directory on your local machine and unpack the `scripts.ZIP` file within the directory.</span></span>  <span data-ttu-id="0afde-153">這會建立 `scripts` 目錄。</span><span class="sxs-lookup"><span data-stu-id="0afde-153">This will create a `scripts` directory.</span></span>

## <span data-ttu-id="0afde-154"><a name="scaffold-app"></a> 建立新的 Azure Mobile Apps 後端的結構</span><span class="sxs-lookup"><span data-stu-id="0afde-154"><a name="scaffold-app"></a> Scaffold the new Azure Mobile Apps backend</span></span>
<span data-ttu-id="0afde-155">從包含指令碼目錄的目錄執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="0afde-155">Run the following command from the directory containing the scripts directory:</span></span>

```scaffold-mobile-app scripts out```

<span data-ttu-id="0afde-156">這會在 `out` 目錄中建立已建立結構的 Azure Mobile Apps 後端。</span><span class="sxs-lookup"><span data-stu-id="0afde-156">This will create a scaffolded Azure Mobile Apps backend in the `out` directory.</span></span>  <span data-ttu-id="0afde-157">雖然並非必要，但最好將 `out` 目錄放置到您選擇的原始程式碼儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0afde-157">Although not required, it's a good idea to check the `out` directory into a source code repository of your choice.</span></span>

## <span data-ttu-id="0afde-158"><a name="deploy-ama-app"></a> 部署 Azure Mobile Apps 後端</span><span class="sxs-lookup"><span data-stu-id="0afde-158"><a name="deploy-ama-app"></a> Deploy your Azure Mobile Apps backend</span></span>
<span data-ttu-id="0afde-159">在部署期間，您必須執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="0afde-159">During deployment, you will need to do the following:</span></span>

1. <span data-ttu-id="0afde-160">在 [Azure 入口網站]中建立新的行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0afde-160">Create a new Mobile App in the [Azure Portal].</span></span>
2. <span data-ttu-id="0afde-161">在連線的資料庫上執行 `createViews.sql` 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0afde-161">Run the `createViews.sql` script on your connected database.</span></span>
3. <span data-ttu-id="0afde-162">將連結至行動服務的資料庫連結至新的 App Service。</span><span class="sxs-lookup"><span data-stu-id="0afde-162">Link the database that is linked to your Mobile Service to your new App Service.</span></span>
4. <span data-ttu-id="0afde-163">將任何其他資源 (例如通知中樞) 連結到新的 App Service。</span><span class="sxs-lookup"><span data-stu-id="0afde-163">Link any other resources (such as Notification Hubs) to the new App Service.</span></span>
5. <span data-ttu-id="0afde-164">將產生的程式碼部署到新網站。</span><span class="sxs-lookup"><span data-stu-id="0afde-164">Deploy the generated code to your new site.</span></span>

### <a name="create-a-new-mobile-app"></a><span data-ttu-id="0afde-165">建立新的行動 App</span><span class="sxs-lookup"><span data-stu-id="0afde-165">Create a new Mobile App</span></span>
1. <span data-ttu-id="0afde-166">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="0afde-166">Log in at the [Azure Portal].</span></span>
2. <span data-ttu-id="0afde-167">按一下 [+ 新增]  >  [Web + 行動]  >  [行動應用程式]，然後為您的行動應用程式後端提供名稱。</span><span class="sxs-lookup"><span data-stu-id="0afde-167">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="0afde-168">針對 [資源群組] ，選取現有的資源群組或建立新的群組 (使用與應用程式相同的名稱)。</span><span class="sxs-lookup"><span data-stu-id="0afde-168">For the **Resource Group**, select an existing resource group, or create a new one (using the same name as your app.)</span></span>

    <span data-ttu-id="0afde-169">您可以選取另一個 App Service 方案或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="0afde-169">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="0afde-170">如需有關應用程式服務方案以及如何在不同的定價層和您所要的位置建立新方案的詳細資訊，請參閱 [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0afde-170">For more about App Services plans and how to create a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="0afde-171">若為 **App Service 方案**，則會選取預設方案 (在 [標準層](https://azure.microsoft.com/pricing/details/app-service/))。</span><span class="sxs-lookup"><span data-stu-id="0afde-171">For the **App Service plan**, the default plan (in the [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="0afde-172">您也可以選取不同的方案，或[建立新的方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan)。</span><span class="sxs-lookup"><span data-stu-id="0afde-172">You can also  select a different plan, or [create a new one](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="0afde-173">App Service 方案的設定會決定與您應用程式相關聯的 [位置、功能、成本和計算資源](https://azure.microsoft.com/pricing/details/app-service/) 。</span><span class="sxs-lookup"><span data-stu-id="0afde-173">The App Service plan's settings determine the [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span>

    <span data-ttu-id="0afde-174">在決定方案之後，按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0afde-174">After you decide on the plan, click **Create**.</span></span> <span data-ttu-id="0afde-175">這會建立行動應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="0afde-175">This creates the Mobile App backend.</span></span>

### <a name="run-createviewssql"></a><span data-ttu-id="0afde-176">執行 CreateViews.SQL</span><span class="sxs-lookup"><span data-stu-id="0afde-176">Run CreateViews.SQL</span></span>
<span data-ttu-id="0afde-177">已建立結構的應用程式包含稱為 `createViews.sql`的檔案。</span><span class="sxs-lookup"><span data-stu-id="0afde-177">The scaffolded app contains a file called `createViews.sql`.</span></span>  <span data-ttu-id="0afde-178">您必須對目標資料庫執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="0afde-178">This script must be executed against the target database.</span></span>  <span data-ttu-id="0afde-179">目標資料庫的連接字串可取自已移轉的行動服務的 [設定] 刀鋒視窗底下的 [連接字串]。</span><span class="sxs-lookup"><span data-stu-id="0afde-179">The connection string for the target database can be obtained from your migrated mobile service from the **Settings** blade under **Connection Strings**.</span></span>  <span data-ttu-id="0afde-180">其名稱為 `MS_TableConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="0afde-180">It is named `MS_TableConnectionString`.</span></span>

<span data-ttu-id="0afde-181">您可以從 SQL Server Management Studio 或 Visual Studio 內執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="0afde-181">You can run this script from within SQL Server Management Studio or Visual Studio.</span></span>

### <a name="link-the-database-to-your-app-service"></a><span data-ttu-id="0afde-182">將資料庫連結到 App Service</span><span class="sxs-lookup"><span data-stu-id="0afde-182">Link the Database to your App Service</span></span>
<span data-ttu-id="0afde-183">將現有資料庫連結到 App Service：</span><span class="sxs-lookup"><span data-stu-id="0afde-183">Link the existing database to your App Service:</span></span>

* <span data-ttu-id="0afde-184">在 [Azure 入口網站]中，開啟您的 App Service。</span><span class="sxs-lookup"><span data-stu-id="0afde-184">In the [Azure Portal], open your App Service.</span></span>
* <span data-ttu-id="0afde-185">選取 [所有設定] -> [資料連接]。</span><span class="sxs-lookup"><span data-stu-id="0afde-185">Select **All Settings** -> **Data Connections**.</span></span>
* <span data-ttu-id="0afde-186">按一下 [+ 新增] 。</span><span class="sxs-lookup"><span data-stu-id="0afde-186">Click on **+ Add**.</span></span>
* <span data-ttu-id="0afde-187">在下拉式清單中，選取 [SQL Database] </span><span class="sxs-lookup"><span data-stu-id="0afde-187">In the drop-down, select **SQL Database**</span></span>
* <span data-ttu-id="0afde-188">在 [SQL Database] 底下選取現有資料庫，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="0afde-188">Under **SQL Database**, select your existing database, then click on **Select**.</span></span>
* <span data-ttu-id="0afde-189">在 [連接字串] 底下，輸入資料庫的使用者名稱和密碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0afde-189">Under **Connection string**, enter the username and password for the database, then click on **OK**.</span></span>
* <span data-ttu-id="0afde-190">在 [新增資料連接] 刀鋒視窗中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0afde-190">In the **Add data connections** blade, click on **OK**.</span></span>

<span data-ttu-id="0afde-191">檢視已移轉的行動服務中目標資料庫的連接字串，就能找到使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0afde-191">The username and password can be found by viewing the Connection String for the target database in your migrated Mobile Service.</span></span>

### <a name="set-up-authentication"></a><span data-ttu-id="0afde-192">設定驗證</span><span class="sxs-lookup"><span data-stu-id="0afde-192">Set up authentication</span></span>
<span data-ttu-id="0afde-193">Azure Mobile Apps 可讓您在服務內設定 Azure Active Directory、Facebook、Google、Microsoft 和 Twitter 驗證。</span><span class="sxs-lookup"><span data-stu-id="0afde-193">Azure Mobile Apps allows you to configure Azure Active Directory, Facebook, Google, Microsoft and Twitter authentication within the service.</span></span>  <span data-ttu-id="0afde-194">自訂驗證則必須另外開發。</span><span class="sxs-lookup"><span data-stu-id="0afde-194">Custom authentication will need to be developed separately.</span></span>  <span data-ttu-id="0afde-195">如需詳細資訊，請參閱[驗證概念]文件和[驗證快速入門]文件。</span><span class="sxs-lookup"><span data-stu-id="0afde-195">Refer to the [Authentication Concepts] documentation and [Authentication Quickstart] documentation for more information.</span></span>  

## <span data-ttu-id="0afde-196"><a name="updating-clients"></a>更新行動用戶端</span><span class="sxs-lookup"><span data-stu-id="0afde-196"><a name="updating-clients"></a>Update Mobile clients</span></span>
<span data-ttu-id="0afde-197">在您擁有可運作的行動 App 後端之後，就能在取用它的新版用戶端應用程式上運作。</span><span class="sxs-lookup"><span data-stu-id="0afde-197">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="0afde-198">Mobile Apps 也會包含新版的用戶端 SDK，而且與上述的伺服器升級類似，您必須先移除所有對行動服務 SDK 的參考，然後安裝 Mobile Apps 版本。</span><span class="sxs-lookup"><span data-stu-id="0afde-198">Mobile Apps also includes a new version of the client SDKs, and similar to the server upgrade above, you will need to remove all references to the Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="0afde-199">版本間的其中一個主要變更是建構函式不再需要應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="0afde-199">One of the main changes between the versions is that the constructors no longer require an application key.</span></span>
<span data-ttu-id="0afde-200">您現在只需傳入行動 App 的 URL。</span><span class="sxs-lookup"><span data-stu-id="0afde-200">You now simply pass in the URL of your Mobile App.</span></span> <span data-ttu-id="0afde-201">例如，在 .NET 用戶端上， `MobileServiceClient` 建構函式現在是：</span><span class="sxs-lookup"><span data-stu-id="0afde-201">For example, on the .NET clients, the `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of the Mobile App
        );

<span data-ttu-id="0afde-202">您可以透過下列連結，閱讀有關安裝新的 SDK 以及使用新結構的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="0afde-202">You can read about installing the new SDKs and using the new structure via the links below:</span></span>

* [<span data-ttu-id="0afde-203">Android 2.2 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0afde-203">Android version 2.2 or later</span></span>](app-service-mobile-android-how-to-use-client-library.md)
* [<span data-ttu-id="0afde-204">iOS 3.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0afde-204">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="0afde-205">.NET (Windows/Xamarin) 2.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0afde-205">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)
* [<span data-ttu-id="0afde-206">Apache Cordova 2.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0afde-206">Apache Cordova version 2.0 or later</span></span>](app-service-mobile-cordova-how-to-use-client-library.md)

<span data-ttu-id="0afde-207">如果您的應用程式會使用推播通知，請記下每個平台特定的註冊指示，因為也已有一些變更。</span><span class="sxs-lookup"><span data-stu-id="0afde-207">If your application makes use of push notifications, make note of the specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="0afde-208">當您準備好新的用戶端版本時，請嘗試對已升級的伺服器專案執行該版本。</span><span class="sxs-lookup"><span data-stu-id="0afde-208">When you have the new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="0afde-209">驗證它的運作方式之後，您就能將新版的應用程式發行給客戶。</span><span class="sxs-lookup"><span data-stu-id="0afde-209">After validating that it works, you can release a new version of your application to customers.</span></span> <span data-ttu-id="0afde-210">最後，在您的客戶有機會接收這些更新後，您就能刪除應用程式的行動服務版本。</span><span class="sxs-lookup"><span data-stu-id="0afde-210">Eventually, once your customers have had a chance to receive these updates, you can delete the Mobile Services version of your app.</span></span> <span data-ttu-id="0afde-211">現在，您已使用最新的 Mobile Apps 伺服器 SDK 完全升級為 App Service 行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="0afde-211">At this point, you have completely upgraded to an App Service Mobile App using the latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

<span data-ttu-id="0afde-212">[Azure portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="0afde-212">[Azure portal]: https://portal.azure.com/</span></span>
[Azure classic portal]: https://manage.windowsazure.com/
<span data-ttu-id="0afde-213">[何謂 Mobile Apps？]: app-service-mobile-value-prop.md</span><span class="sxs-lookup"><span data-stu-id="0afde-213">[What are Mobile Apps?]: app-service-mobile-value-prop.md</span></span>
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications to your mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication to your mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How to use the .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services to an App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service to App Service]: app-service-mobile-migrating-from-mobile-services.md
<span data-ttu-id="0afde-214">[App Service 定價]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="0afde-214">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
<span data-ttu-id="0afde-215">[驗證概念]: ../app-service/app-service-authentication-overview.md</span><span class="sxs-lookup"><span data-stu-id="0afde-215">[Authentication Concepts]: ../app-service/app-service-authentication-overview.md</span></span>
<span data-ttu-id="0afde-216">[驗證快速入門]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="0afde-216">[Authentication Quickstart]: app-service-mobile-auth.md</span></span>

<span data-ttu-id="0afde-217">[Azure 入口網站]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="0afde-217">[Azure Portal]: https://portal.azure.com/</span></span>
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
