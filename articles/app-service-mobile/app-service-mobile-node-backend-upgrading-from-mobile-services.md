---
title: "從行動服務 tooAzure 應用程式服務-Node.js aaaUpgrade"
description: "了解如何 tooeasily 升級您的行動服務應用程式 tooan App Service 行動應用程式"
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
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a><span data-ttu-id="0d9cb-103">升級您現有的 Node.js 的 Azure 行動服務 tooApp 服務</span><span class="sxs-lookup"><span data-stu-id="0d9cb-103">Upgrade your existing Node.js Azure Mobile Service tooApp Service</span></span>
<span data-ttu-id="0d9cb-104">App Service Mobile 是新的方式 toobuild 行動應用程式使用 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-104">App Service Mobile is a new way toobuild mobile applications using Microsoft Azure.</span></span> <span data-ttu-id="0d9cb-105">詳細資訊，請參閱 toolearn[行動應用程式是什麼？]。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-105">toolearn more, see [What are Mobile Apps?].</span></span>

<span data-ttu-id="0d9cb-106">本主題描述如何將現有 Node.js 後端應用程式從 Azure Mobile Services tooa tooupgrade 新的 App Service Mobile App。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-106">This topic describes how tooupgrade an existing Node.js backend application from Azure Mobile Services tooa new App Service Mobile Apps.</span></span> <span data-ttu-id="0d9cb-107">當您執行此升級時，現有的行動服務應用程式可以繼續 toooperate。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-107">While you perform this upgrade, your existing Mobile Services application can continue toooperate.</span></span>  <span data-ttu-id="0d9cb-108">如果您需要 tooupgrade Node.js 後端應用程式，請參閱太[升級您的.NET 行動服務](app-service-mobile-net-upgrading-from-mobile-services.md)。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-108">If you need tooupgrade a Node.js backend application, refer too[Upgrading your .NET Mobile Services](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<span data-ttu-id="0d9cb-109">升級的 tooAzure App Service 行動後端時，它有 App Service 功能且計費太根據存取 tooall[應用程式服務定價]、 定價不行動服務。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-109">When a mobile backend is upgraded tooAzure App Service, it has access tooall App Service features and are billed according too[App Service pricing], not Mobile Services pricing.</span></span>

## <a name="migrate-vs-upgrade"></a><span data-ttu-id="0d9cb-110">移轉與升級</span><span class="sxs-lookup"><span data-stu-id="0d9cb-110">Migrate vs. upgrade</span></span>
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> <span data-ttu-id="0d9cb-111">建議您在升級之前，先 [執行移轉](app-service-mobile-migrating-from-mobile-services.md) 。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-111">It is recommended that you [perform a migration](app-service-mobile-migrating-from-mobile-services.md) before going through an upgrade.</span></span> <span data-ttu-id="0d9cb-112">如此一來，您可以將您的應用程式的兩個版本上 hello 相同 App Service 方案，並會產生任何額外的成本。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-112">This way, you can put both versions of your application on hello same App Service Plan and incur no additional cost.</span></span>
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a><span data-ttu-id="0d9cb-113">Mobile Apps Node.js 伺服器 SDK 中的改進功能</span><span class="sxs-lookup"><span data-stu-id="0d9cb-113">Improvements in Mobile Apps Node.js server SDK</span></span>
<span data-ttu-id="0d9cb-114">升級新 toohello[行動應用程式 SDK](https://www.npmjs.com/package/azure-mobile-apps)提供許多增強功能，包括：</span><span class="sxs-lookup"><span data-stu-id="0d9cb-114">Upgrading toohello new [Mobile Apps SDK](https://www.npmjs.com/package/azure-mobile-apps) provides a lot of improvements, including:</span></span>

* <span data-ttu-id="0d9cb-115">根據 hello [Express framework](http://expressjs.com/en/index.html)，hello 新節點 SDK 是輕量且設計 tookeep 總，以新節點的版本為送。您可以自訂 hello Express 中介軟體的應用程式行為。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-115">Based on hello [Express framework](http://expressjs.com/en/index.html), hello new Node SDK is light-weight and designed tookeep up with new Node versions as they come out. You can customize hello application behavior with Express middleware.</span></span>
* <span data-ttu-id="0d9cb-116">大幅改良效能比較 toohello 行動服務 SDK。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-116">Significant performance improvements compared toohello Mobile Services SDK.</span></span>
* <span data-ttu-id="0d9cb-117">您現在可以在行動裝置的後端; 以及裝載網站同樣地，它是簡單 tooadd hello Azure Mobile SDK tooany 現有 express.v4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-117">You can now host a website together with your mobile backend; similarly, it's easy tooadd hello Azure Mobile SDK tooany existing express.v4 application.</span></span>
* <span data-ttu-id="0d9cb-118">建置跨平台和本機程式開發，hello 行動應用程式 SDK 開發和本機 Windows、 Linux 及 OSX 平台上執行。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-118">Built for cross-platform and local development, hello Mobile Apps SDK can be developed and run locally on Windows, Linux, and OSX platforms.</span></span> <span data-ttu-id="0d9cb-119">現在很容易 toouse 常見節點開發技術，如執行[Mocha](https://mochajs.org/)測試先前 toodeployment。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-119">It's now easy toouse common Node development techniques like running [Mocha](https://mochajs.org/) tests prior toodeployment.</span></span>

## <span data-ttu-id="0d9cb-120"><a name="overview"></a>基本升級概觀</span><span class="sxs-lookup"><span data-stu-id="0d9cb-120"><a name="overview"></a>Basic upgrade overview</span></span>
<span data-ttu-id="0d9cb-121">tooaid 升級 Node.js 後端 Azure App Service 中的提供的相容性封裝。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-121">tooaid in upgrading a Node.js backend, Azure App Service has provided a compatibility package.</span></span>  <span data-ttu-id="0d9cb-122">升級之後，您必須使用 niew 站台，可以部署的 tooa 新應用程式服務的站台。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-122">After upgrade, you will have a niew site that can be deployed tooa new App Service site.</span></span>

<span data-ttu-id="0d9cb-123">hello 行動服務用戶端 Sdk 是**不**與新行動裝置應用程式伺服器 hello SDK 相容。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-123">hello Mobile Services client SDKs are **not** compatible with hello new Mobile Apps server SDK.</span></span> <span data-ttu-id="0d9cb-124">在順序 tooprovide 服務連續性的應用程式，您不應該發行變更 tooa 站台目前正在服務已發佈的用戶端。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-124">In order tooprovide continuity of service for your app, you should not publish changes tooa site currently serving published clients.</span></span> <span data-ttu-id="0d9cb-125">而是應該建立新的行動應用程式做為重複項目。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-125">Instead, you should create a new mobile app that serves as a duplicate.</span></span> <span data-ttu-id="0d9cb-126">您可以將此應用程式相同的應用程式服務計劃在 hello tooavoid 產生額外的財務成本。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-126">You can put this application on hello same App Service plan tooavoid incurring additional financial cost.</span></span>

<span data-ttu-id="0d9cb-127">您將會讓 hello 應用程式的兩個版本： 一個維持相同 hello 和中 hello 普遍可已發佈的應用程式的另一個您可以接著升級和使用新的用戶端的目標版本。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-127">You will then have two versions of hello application: one that stays hello same and serves published apps in hello wild, and the other which you can then upgrade and target with a new client release.</span></span> <span data-ttu-id="0d9cb-128">您可以移動，或您的程式碼測試您的速度，但您應該確定您所做的任何 bug 修正取得套用的 tooboth。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-128">You can move and test your code at your pace, but you should make sure that any bug fixes you make get applied tooboth.</span></span> <span data-ttu-id="0d9cb-129">一旦您認為不應在用戶端應用程式所需的數目有更新 toohello 最新版本，如果您想要您可以刪除 hello 原始移轉應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-129">Once you feel that a desired number of client apps in the wild have updated toohello latest version, you can delete hello original migrated app if you desire.</span></span> <span data-ttu-id="0d9cb-130">如果裝載於相同應用程式服務計劃做為您的行動裝置應用程式的 hello，它不會產生任何額外的金錢費用。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-130">It doesn't incur any additional monetary costs, if hosted in hello same App Service plan as your Mobile App.</span></span>

<span data-ttu-id="0d9cb-131">hello 完整大綱 hello 升級程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="0d9cb-131">hello full outline for hello upgrade process is as follows:</span></span>

1. <span data-ttu-id="0d9cb-132">下載您現有的 (已移轉) Azure 行動服務。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-132">Download your existing (migrated) Azure Mobile Service.</span></span>
2. <span data-ttu-id="0d9cb-133">轉換 hello 專案 tooan Azure 行動應用程式使用 hello 相容性封裝。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-133">Convert hello project tooan Azure Mobile App using hello compatibility package.</span></span>
3. <span data-ttu-id="0d9cb-134">更正任何差異 (例如驗證設定)。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-134">Correct any differences (such as authentication settings).</span></span>
4. <span data-ttu-id="0d9cb-135">部署您已轉換的 Azure 行動應用程式專案 tooa 新應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-135">Deploy your converted Azure Mobile App project tooa new App Service.</span></span>
5. <span data-ttu-id="0d9cb-136">發行新版本的用戶端應用程式使用 hello 新的行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-136">Release a new version of your client application that use hello new Mobile App.</span></span>
6. <span data-ttu-id="0d9cb-137">(可省略) 刪除您已移轉的原始行動服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-137">(Optional) Delete your original migrated mobile service app.</span></span>

<span data-ttu-id="0d9cb-138">當已移轉的原始行動服務沒有任何流量時，就能加以刪除。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-138">Deletion can occur when you don't see any traffic on your original migrated mobile service.</span></span>

## <span data-ttu-id="0d9cb-139"><a name="install-npm-package"></a>安裝 hello 的必要元件</span><span class="sxs-lookup"><span data-stu-id="0d9cb-139"><a name="install-npm-package"></a> Install hello Pre-requisites</span></span>
<span data-ttu-id="0d9cb-140">您應該在本機電腦上安裝 [節點]。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-140">You should install [Node] on your local machine.</span></span>  <span data-ttu-id="0d9cb-141">您也應該安裝 hello 相容性封裝。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-141">You should also install hello compatibility package.</span></span>  <span data-ttu-id="0d9cb-142">節點安裝之後，您可以執行下列命令，從新的 cmd 或 PowerShell 命令提示字元的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d9cb-142">After Node is installed, you can run hello following command from a new cmd or PowerShell prompt:</span></span>

```npm i -g azure-mobile-apps-compatibility```

## <span data-ttu-id="0d9cb-143"><a name="obtain-ams-scripts"></a> 取得 Azure 行動服務指令碼</span><span class="sxs-lookup"><span data-stu-id="0d9cb-143"><a name="obtain-ams-scripts"></a> Obtain your Azure Mobile Services Scripts</span></span>
* <span data-ttu-id="0d9cb-144">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-144">Log in toohello [Azure Portal].</span></span>
* <span data-ttu-id="0d9cb-145">使用 [所有資源] 或 [應用程式服務]，尋找您的行動服務網站。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-145">Using **All Resources** or **App Services**, find your Mobile Services site.</span></span>
* <span data-ttu-id="0d9cb-146">在 hello 網站中，按一下**工具** -> **Kudu** -> **移**tooopen hello Kudu 站台。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-146">Within hello site, click on **Tools** -> **Kudu** -> **Go** tooopen hello Kudu site.</span></span>
* <span data-ttu-id="0d9cb-147">按一下**偵錯主控台** -> **PowerShell** tooopen hello 偵錯主控台。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-147">Click on **Debug Console** -> **PowerShell** tooopen hello Debug console.</span></span>
* <span data-ttu-id="0d9cb-148">瀏覽過`site/wwwroot/App_Data/config`依次按一下每個目錄</span><span class="sxs-lookup"><span data-stu-id="0d9cb-148">Navigate too`site/wwwroot/App_Data/config` by clicking on each directory in turn</span></span>
* <span data-ttu-id="0d9cb-149">按一下 hello 下載圖示下一步 toohello`scripts`目錄。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-149">Click on hello download icon next toohello `scripts` directory.</span></span>

<span data-ttu-id="0d9cb-150">這會下載 ZIP 格式中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-150">This will download hello scripts in ZIP format.</span></span>  <span data-ttu-id="0d9cb-151">在本機電腦上建立新的目錄，並解壓縮 hello `scripts.ZIP` hello 目錄內的檔案。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-151">Create a new directory on your local machine and unpack hello `scripts.ZIP` file within hello directory.</span></span>  <span data-ttu-id="0d9cb-152">這會建立 `scripts` 目錄。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-152">This will create a `scripts` directory.</span></span>

## <span data-ttu-id="0d9cb-153"><a name="scaffold-app"></a>Scaffold hello 新的 Azure 行動應用程式後端</span><span class="sxs-lookup"><span data-stu-id="0d9cb-153"><a name="scaffold-app"></a> Scaffold hello new Azure Mobile Apps backend</span></span>
<span data-ttu-id="0d9cb-154">執行下列命令，從包含 hello 指令碼目錄 hello 目錄 hello:</span><span class="sxs-lookup"><span data-stu-id="0d9cb-154">Run hello following command from hello directory containing hello scripts directory:</span></span>

```scaffold-mobile-app scripts out```

<span data-ttu-id="0d9cb-155">這會建立 scaffold 的 Azure 行動應用程式後端中 hello`out`目錄。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-155">This will create a scaffolded Azure Mobile Apps backend in hello `out` directory.</span></span>  <span data-ttu-id="0d9cb-156">雖然並非必要，是個不錯的主意 toocheck hello`out`到來源的程式碼儲存機制，您所選擇的目錄。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-156">Although not required, it's a good idea toocheck hello `out` directory into a source code repository of your choice.</span></span>

## <span data-ttu-id="0d9cb-157"><a name="deploy-ama-app"></a> 部署 Azure Mobile Apps 後端</span><span class="sxs-lookup"><span data-stu-id="0d9cb-157"><a name="deploy-ama-app"></a> Deploy your Azure Mobile Apps backend</span></span>
<span data-ttu-id="0d9cb-158">在部署期間，您將需要 toodo hello 下列：</span><span class="sxs-lookup"><span data-stu-id="0d9cb-158">During deployment, you will need toodo hello following:</span></span>

1. <span data-ttu-id="0d9cb-159">建立新的行動裝置應用程式在 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-159">Create a new Mobile App in hello [Azure Portal].</span></span>
2. <span data-ttu-id="0d9cb-160">執行 hello`createViews.sql`連接的資料庫上的指令碼。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-160">Run hello `createViews.sql` script on your connected database.</span></span>
3. <span data-ttu-id="0d9cb-161">連結 hello 資料庫連結的 tooyour 行動服務 tooyour 新應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-161">Link hello database that is linked tooyour Mobile Service tooyour new App Service.</span></span>
4. <span data-ttu-id="0d9cb-162">連結任何其他資源 （例如通知中樞） toohello 新應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-162">Link any other resources (such as Notification Hubs) toohello new App Service.</span></span>
5. <span data-ttu-id="0d9cb-163">部署 hello 產生程式碼 tooyour 新站台。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-163">Deploy hello generated code tooyour new site.</span></span>

### <a name="create-a-new-mobile-app"></a><span data-ttu-id="0d9cb-164">建立新的行動 App</span><span class="sxs-lookup"><span data-stu-id="0d9cb-164">Create a new Mobile App</span></span>
1. <span data-ttu-id="0d9cb-165">在 hello 登入[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-165">Log in at hello [Azure Portal].</span></span>
2. <span data-ttu-id="0d9cb-166">按一下 [+ 新增]  >  [Web + 行動]  >  [行動應用程式]，然後為您的行動應用程式後端提供名稱。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-166">Click **+NEW** > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="0d9cb-167">Hello**資源群組**，選取現有的資源群組，或建立新的 (使用 hello 與您的應用程式同名)。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-167">For hello **Resource Group**, select an existing resource group, or create a new one (using hello same name as your app.)</span></span>

    <span data-ttu-id="0d9cb-168">您可以選取另一個 App Service 方案或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-168">You can either select another App Service plan or create a new one.</span></span> <span data-ttu-id="0d9cb-169">如需詳細資訊，應用程式服務計劃和如何 toocreate 新計劃中不同的定價層，然後在您想要的位置，請參閱[Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-169">For more about App Services plans and how toocreate a new plan in a different pricing tier and in your desired location, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
4. <span data-ttu-id="0d9cb-170">Hello **App Service 方案**，hello 預設計劃 (在 hello[標準層](https://azure.microsoft.com/pricing/details/app-service/)) 已選取。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-170">For hello **App Service plan**, hello default plan (in hello [Standard tier](https://azure.microsoft.com/pricing/details/app-service/)) is selected.</span></span> <span data-ttu-id="0d9cb-171">您也可以選取不同的方案，或[建立新的方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan)。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-171">You can also  select a different plan, or [create a new one](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan).</span></span> <span data-ttu-id="0d9cb-172">hello 應用程式服務方案設定會決定 hello[位置、 功能、 成本及計算資源](https://azure.microsoft.com/pricing/details/app-service/)與您的應用程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-172">hello App Service plan's settings determine hello [location, features, cost and compute resources](https://azure.microsoft.com/pricing/details/app-service/) associated with your app.</span></span>

    <span data-ttu-id="0d9cb-173">當您決定 hello 計劃之後，請按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-173">After you decide on hello plan, click **Create**.</span></span> <span data-ttu-id="0d9cb-174">這會建立 hello 行動裝置應用程式後端。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-174">This creates hello Mobile App backend.</span></span>

### <a name="run-createviewssql"></a><span data-ttu-id="0d9cb-175">執行 CreateViews.SQL</span><span class="sxs-lookup"><span data-stu-id="0d9cb-175">Run CreateViews.SQL</span></span>
<span data-ttu-id="0d9cb-176">hello scaffold 應用程式包含檔案，稱為`createViews.sql`。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-176">hello scaffolded app contains a file called `createViews.sql`.</span></span>  <span data-ttu-id="0d9cb-177">您必須對目標資料庫執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-177">This script must be executed against the target database.</span></span>  <span data-ttu-id="0d9cb-178">hello hello 目標資料庫的連接字串可以取自您移轉的行動服務，從 hello**設定**刀鋒視窗底下**連接字串**。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-178">hello connection string for hello target database can be obtained from your migrated mobile service from hello **Settings** blade under **Connection Strings**.</span></span>  <span data-ttu-id="0d9cb-179">其名稱為 `MS_TableConnectionString`。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-179">It is named `MS_TableConnectionString`.</span></span>

<span data-ttu-id="0d9cb-180">您可以從 SQL Server Management Studio 或 Visual Studio 內執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-180">You can run this script from within SQL Server Management Studio or Visual Studio.</span></span>

### <a name="link-hello-database-tooyour-app-service"></a><span data-ttu-id="0d9cb-181">連結 hello 資料庫 tooyour 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="0d9cb-181">Link hello Database tooyour App Service</span></span>
<span data-ttu-id="0d9cb-182">連結現有資料庫 tooyour hello 應用程式服務：</span><span class="sxs-lookup"><span data-stu-id="0d9cb-182">Link hello existing database tooyour App Service:</span></span>

* <span data-ttu-id="0d9cb-183">在 hello [Azure 入口網站]，開啟您的應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-183">In hello [Azure Portal], open your App Service.</span></span>
* <span data-ttu-id="0d9cb-184">選取 [所有設定] -> [資料連接]。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-184">Select **All Settings** -> **Data Connections**.</span></span>
* <span data-ttu-id="0d9cb-185">按一下 [+ 新增] 。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-185">Click on **+ Add**.</span></span>
* <span data-ttu-id="0d9cb-186">在 hello 下拉式清單中，選取  **SQL 資料庫**</span><span class="sxs-lookup"><span data-stu-id="0d9cb-186">In hello drop-down, select **SQL Database**</span></span>
* <span data-ttu-id="0d9cb-187">在 [SQL Database] 底下選取現有資料庫，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-187">Under **SQL Database**, select your existing database, then click on **Select**.</span></span>
* <span data-ttu-id="0d9cb-188">在下**連接字串**、 輸入 hello 資料庫 hello 使用者名稱和密碼，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-188">Under **Connection string**, enter hello username and password for hello database, then click on **OK**.</span></span>
* <span data-ttu-id="0d9cb-189">在 hello**加入資料連接**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-189">In hello **Add data connections** blade, click on **OK**.</span></span>

<span data-ttu-id="0d9cb-190">可以藉由檢視移轉的行動服務中的 hello 目標資料庫的連接字串 hello 找到 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-190">hello username and password can be found by viewing hello Connection String for hello target database in your migrated Mobile Service.</span></span>

### <a name="set-up-authentication"></a><span data-ttu-id="0d9cb-191">設定驗證</span><span class="sxs-lookup"><span data-stu-id="0d9cb-191">Set up authentication</span></span>
<span data-ttu-id="0d9cb-192">Azure 行動應用程式可讓您 tooconfigure hello 服務內的 Azure Active Directory、 Facebook、 Google、 Microsoft 及 Twitter 驗證。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-192">Azure Mobile Apps allows you tooconfigure Azure Active Directory, Facebook, Google, Microsoft and Twitter authentication within hello service.</span></span>  <span data-ttu-id="0d9cb-193">Toobe 個別開發時，就需要自訂的驗證。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-193">Custom authentication will need toobe developed separately.</span></span>  <span data-ttu-id="0d9cb-194">請參閱 hello[驗證概念]文件和[驗證快速入門]文件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-194">Refer to hello [Authentication Concepts] documentation and [Authentication Quickstart] documentation for more information.</span></span>  

## <span data-ttu-id="0d9cb-195"><a name="updating-clients"></a>更新行動用戶端</span><span class="sxs-lookup"><span data-stu-id="0d9cb-195"><a name="updating-clients"></a>Update Mobile clients</span></span>
<span data-ttu-id="0d9cb-196">在您擁有可運作的行動 App 後端之後，就能在取用它的新版用戶端應用程式上運作。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-196">Once you have an operational Mobile App backend, you can work on a new version of your client application which consumes it.</span></span> <span data-ttu-id="0d9cb-197">行動應用程式也包含新版 hello client Sdk，以及類似的 toohello server 升級上方，您將需要的 tooremove toohello 行動服務 Sdk 之前的所有參照安裝行動應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-197">Mobile Apps also includes a new version of hello client SDKs, and similar toohello server upgrade above, you will need tooremove all references toohello Mobile Services SDKs before installing the Mobile Apps versions.</span></span>

<span data-ttu-id="0d9cb-198">其中一個 hello hello 版本之間的主要變更是 hello 建構函式不再需要應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-198">One of hello main changes between hello versions is that hello constructors no longer require an application key.</span></span>
<span data-ttu-id="0d9cb-199">您現在只需傳入 hello 行動應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-199">You now simply pass in hello URL of your Mobile App.</span></span> <span data-ttu-id="0d9cb-200">例如，在 hello.NET 用戶端，hello`MobileServiceClient`建構函式現在是：</span><span class="sxs-lookup"><span data-stu-id="0d9cb-200">For example, on hello .NET clients, hello `MobileServiceClient` constructor is now:</span></span>

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

<span data-ttu-id="0d9cb-201">您可以閱讀安裝 hello 新 Sdk，並使用 hello 透過以下的 hello 連結新的結構：</span><span class="sxs-lookup"><span data-stu-id="0d9cb-201">You can read about installing hello new SDKs and using hello new structure via hello links below:</span></span>

* [<span data-ttu-id="0d9cb-202">Android 2.2 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0d9cb-202">Android version 2.2 or later</span></span>](app-service-mobile-android-how-to-use-client-library.md)
* [<span data-ttu-id="0d9cb-203">iOS 3.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0d9cb-203">iOS version 3.0.0 or later</span></span>](app-service-mobile-ios-how-to-use-client-library.md)
* [<span data-ttu-id="0d9cb-204">.NET (Windows/Xamarin) 2.0.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0d9cb-204">.NET (Windows/Xamarin) version 2.0.0 or later</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)
* [<span data-ttu-id="0d9cb-205">Apache Cordova 2.0 版或更新版本</span><span class="sxs-lookup"><span data-stu-id="0d9cb-205">Apache Cordova version 2.0 or later</span></span>](app-service-mobile-cordova-how-to-use-client-library.md)

<span data-ttu-id="0d9cb-206">如果您的應用程式更能使用推播通知，請記下 hello 特定註冊指示每個平台，已有一些變更有以及。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-206">If your application makes use of push notifications, make note of hello specific registration instructions for each platform, as there have been some changes there as well.</span></span>

<span data-ttu-id="0d9cb-207">當您擁有 hello 新用戶端版本準備好時，現在就試試看對您已升級的伺服器專案。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-207">When you have hello new client version ready, try it out against your upgraded server project.</span></span> <span data-ttu-id="0d9cb-208">驗證它運作之後，您可以釋放您的應用程式 toocustomers 的新版本。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-208">After validating that it works, you can release a new version of your application toocustomers.</span></span> <span data-ttu-id="0d9cb-209">最後，一旦您的客戶有機會 tooreceive 這些更新，您可以刪除 hello 行動服務應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-209">Eventually, once your customers have had a chance tooreceive these updates, you can delete hello Mobile Services version of your app.</span></span> <span data-ttu-id="0d9cb-210">此時，您完全升級 tooan App Service 行動應用程式使用最新版行動應用程式伺服器 hello SDK。</span><span class="sxs-lookup"><span data-stu-id="0d9cb-210">At this point, you have completely upgraded tooan App Service Mobile App using hello latest Mobile Apps server SDK.</span></span>

<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[行動應用程式是什麼？]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[應用程式服務定價]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[驗證概念]: ../app-service/app-service-authentication-overview.md
[驗證快速入門]: app-service-mobile-auth.md

[Azure 入口網站]: https://portal.azure.com/
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
