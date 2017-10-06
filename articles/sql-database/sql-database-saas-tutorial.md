---
title: "aaaDeploy 和瀏覽 hello 多租用戶 Wingtip SaaS 應用程式使用 Azure SQL Database |Microsoft 文件"
description: "部署及瀏覽 hello Wingtip SaaS 多租用戶應用程式，示範使用 Azure SQL Database 的 SaaS 模式。"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a><span data-ttu-id="0a8e4-104">部署及探索使用 Azure SQL Database 的多租用戶應用程式 - Wingtip SaaS</span><span class="sxs-lookup"><span data-stu-id="0a8e4-104">Deploy and explore a multi-tenant application that uses Azure SQL Database - Wingtip SaaS</span></span>

<span data-ttu-id="0a8e4-105">在本教學課程中，您可以部署，並瀏覽 hello Wingtip SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-105">In this tutorial, you deploy and explore hello Wingtip SaaS application.</span></span> <span data-ttu-id="0a8e4-106">hello 應用程式會使用資料庫的各個租用戶，SaaS 應用程式模式 tooservice 多個租用戶。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-106">hello application uses a database-per-tenant, SaaS application pattern, tooservice multiple tenants.</span></span> <span data-ttu-id="0a8e4-107">hello 應用程式是簡化啟用 SaaS 案例的設計的 tooshowcase 功能的 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-107">hello application is designed tooshowcase features of Azure SQL Database that simplify enabling SaaS scenarios.</span></span>

<span data-ttu-id="0a8e4-108">五分鐘後按一下 hello*部署 tooAzure*下方的按鈕，您有多租用戶 SaaS 應用程式中，最多使用 SQL Database 和 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-108">Five minutes after clicking hello *Deploy tooAzure* button below, you have a multi-tenant SaaS application, using SQL Database, up and running in hello cloud.</span></span> <span data-ttu-id="0a8e4-109">hello 應用程式會使用三個範例租用戶，各有其專屬資料庫到 SQL 彈性集區已部署的所有部署。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-109">hello application is deployed with three sample tenants, each with its own database, all deployed into a SQL elastic pool.</span></span> <span data-ttu-id="0a8e4-110">hello 應用程式是部署的 tooyour Azure 訂用帳戶，讓您完整存取 tooexplore 及處理 hello 個別應用程式元件。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-110">hello app is deployed tooyour Azure subscription, giving you full access tooexplore and work with hello individual application components.</span></span> <span data-ttu-id="0a8e4-111">hello 應用程式來源的程式碼和管理指令碼可用於 hello WingtipSaaS GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-111">hello application source code and management scripts are available in hello WingtipSaaS GitHub repo.</span></span>


<span data-ttu-id="0a8e4-112">您會在本教學課程中學到：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-112">In this tutorial you learn:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="0a8e4-113">如何 toodeploy hello Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a8e4-113">How toodeploy hello Wingtip SaaS application</span></span>
> * <span data-ttu-id="0a8e4-114">其中 tooget hello 應用程式的原始程式碼，並管理指令碼</span><span class="sxs-lookup"><span data-stu-id="0a8e4-114">Where tooget hello application source code, and management scripts</span></span>
> * <span data-ttu-id="0a8e4-115">關於 hello、 集區的伺服器和資料庫組成 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a8e4-115">About hello servers, pools, and databases that make up hello app</span></span>
> * <span data-ttu-id="0a8e4-116">租用戶的方式對應 tootheir 資料以 hello*類別目錄*</span><span class="sxs-lookup"><span data-stu-id="0a8e4-116">How tenants are mapped tootheir data with hello *catalog*</span></span>
> * <span data-ttu-id="0a8e4-117">如何 tooprovision 新的租用戶</span><span class="sxs-lookup"><span data-stu-id="0a8e4-117">How tooprovision a new tenant</span></span>
> * <span data-ttu-id="0a8e4-118">如何 toomonitor 租用戶 hello 應用程式中的活動</span><span class="sxs-lookup"><span data-stu-id="0a8e4-118">How toomonitor tenant activity in hello app</span></span>

<span data-ttu-id="0a8e4-119">tooexplore 各種 SaaS 設計和管理模式[相關教學課程系列](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)可用，是根據此初始的部署。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-119">tooexplore various SaaS design and management patterns, a [series of related tutorials](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) is available that build upon this initial deployment.</span></span> <span data-ttu-id="0a8e4-120">時經過 hello 教學課程，深入了解 hello 提供指令碼，並檢查 hello SaaS 模式不同的實作方式。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-120">While going through hello tutorials, dive into hello provided scripts, and examine how hello different SaaS patterns are implemented.</span></span> <span data-ttu-id="0a8e4-121">逐步執行每個教學課程 toogain 深入了解如何 tooimplement hello 許多 SQL Database 功能可讓您簡化開發 SaaS 應用程式中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-121">Step through hello scripts in each tutorial toogain a deeper understanding how tooimplement hello many SQL Database features that simplify developing SaaS applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a8e4-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a8e4-122">Prerequisites</span></span>

<span data-ttu-id="0a8e4-123">toocomplete 完成本教學課程，請確定 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-123">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

* <span data-ttu-id="0a8e4-124">已安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-124">Azure PowerShell is installed.</span></span> <span data-ttu-id="0a8e4-125">如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="0a8e4-125">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>

## <a name="deploy-hello-wingtip-saas-application"></a><span data-ttu-id="0a8e4-126">部署 hello Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a8e4-126">Deploy hello Wingtip SaaS application</span></span>

<span data-ttu-id="0a8e4-127">部署 hello Wingtip SaaS 應用程式：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-127">Deploy hello Wingtip SaaS app:</span></span>

1. <span data-ttu-id="0a8e4-128">按一下 hello**部署 tooAzure**按鈕會開啟 hello Azure 入口網站 toohello Wingtip SaaS 部署範本。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-128">Clicking hello **Deploy tooAzure** button opens hello Azure portal toohello Wingtip SaaS deployment template.</span></span> <span data-ttu-id="0a8e4-129">hello 範本需要兩個參數值。新的資源群組名稱和使用者名稱，可區別此部署中的其他部署的 hello Wingtip SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-129">hello template requires two parameter values; a name for a new resource group, and a user name that distinguishes this deployment from other deployments of hello Wingtip SaaS app.</span></span> <span data-ttu-id="0a8e4-130">hello 下一個步驟將詳細說明如何設定這些值。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-130">hello next step provides details for setting these values.</span></span>

   <span data-ttu-id="0a8e4-131">請確定 toonote hello 確切值，您使用，因為您將的 tooenter 其組態檔更新版本。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-131">Make sure toonote hello exact values that you use, because you will need tooenter them into a configuration file later.</span></span>

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. <span data-ttu-id="0a8e4-132">輸入 hello 部署必要的參數值：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-132">Enter required parameter values for hello deployment:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0a8e4-133">為了示範的目的，已刻意將某些驗證和伺服器防火牆設為不安全。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-133">Some authentication, and server firewalls are intentionally unsecured for demonstration purposes.</span></span> <span data-ttu-id="0a8e4-134">**建立新的資源群組**，而不要使用現有資源群組、伺服器或集區。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-134">**Create a new resource group**, and do not use existing resource groups, servers, or pools.</span></span> <span data-ttu-id="0a8e4-135">請不要將此應用程式或任何它所建立的資源用於生產環境。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-135">Do not use this application, or any resources it creates, for production.</span></span> <span data-ttu-id="0a8e4-136">刪除此資源群組，當您完成 hello 應用程式 toostop 相關計費。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-136">Delete this resource group when you are finished with hello application toostop related billing.</span></span>

    * <span data-ttu-id="0a8e4-137">**資源群組**-選取**建立新**並提供**名稱**hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-137">**Resource group** - Select **Create new** and provide a **Name** for hello resource group.</span></span> <span data-ttu-id="0a8e4-138">選取**位置**hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-138">Select a **Location** from hello drop-down list.</span></span>
    * <span data-ttu-id="0a8e4-139">**使用者** - 部分資源需要全域唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-139">**User** - Some resources require names that are globally unique.</span></span> <span data-ttu-id="0a8e4-140">tooensure 唯一性，每次部署 hello 應用程式提供的值 toodifferentiate 所建立的資源，從任何其他部署的 hello Wingtip 應用程式所建立的資源。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-140">tooensure uniqueness, each time you deploy hello application provide a value toodifferentiate resources you create, from resources created by any other deployment of hello Wingtip application.</span></span> <span data-ttu-id="0a8e4-141">建議 toouse 簡短**使用者**名稱，例如您的首字母加上數字 (例如， *bg1*)，然後 hello 資源群組名稱中使用，(比方說， *wingtip bg1*).</span><span class="sxs-lookup"><span data-stu-id="0a8e4-141">It’s recommended toouse a short **User** name, such as your initials plus a number (for example, *bg1*), and then use that in hello resource group name (for example, *wingtip-bg1*).</span></span> <span data-ttu-id="0a8e4-142">[使用者] 參數只能包含字母、數字和連字號 (無空格)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-142">The **User** parameter can only contain letters, numbers, and hyphens (no spaces).</span></span> <span data-ttu-id="0a8e4-143">hello 第一個和最後一個字元必須是字母或數字 （建議使用所有小寫）。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-143">hello first and last character must be a letter or a number (all lowercase is recommended).</span></span>


1. <span data-ttu-id="0a8e4-144">**部署的應用程式 hello**。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-144">**Deploy hello application**.</span></span>

    * <span data-ttu-id="0a8e4-145">按一下 tooagree toohello 條款和條件。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-145">Click tooagree toohello terms and conditions.</span></span>
    * <span data-ttu-id="0a8e4-146">按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-146">Click **Purchase**.</span></span>

1. <span data-ttu-id="0a8e4-147">監視部署狀態，依序按一下**通知**（hello hello 搜尋 方塊右邊的鈴鐺圖示）。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-147">Monitor deployment status by clicking **Notifications** (hello bell icon right of hello search box).</span></span> <span data-ttu-id="0a8e4-148">部署的 hello Wingtip SaaS 應用程式會大約五分鐘。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-148">Deploying hello Wingtip SaaS app takes approximately five minutes.</span></span>

   ![部署成功](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a><span data-ttu-id="0a8e4-150">下載並解除封鎖 hello Wingtip SaaS 指令碼</span><span class="sxs-lookup"><span data-stu-id="0a8e4-150">Download and unblock hello Wingtip SaaS scripts</span></span>

<span data-ttu-id="0a8e4-151">雖然 hello 應用程式正在部署，下載 hello 來源的程式碼和管理指令碼。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-151">While hello application is deploying, download hello source code and management scripts.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a8e4-152">從外部來源下載 zip 檔案並進行解壓縮時，Windows 可能會封鎖可執行的內容 (指令碼、dll)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-152">Executable contents (scripts, dlls) may be blocked by Windows when zip files are downloaded from an external source and extracted.</span></span> <span data-ttu-id="0a8e4-153">當從 zip 檔案解壓縮 hello 指令碼，請遵循 hello 步驟下方 toounblock hello.zip 檔案，然後才能擷取。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-153">When extracting hello scripts from a zip file, follow hello steps below toounblock hello .zip file before extracting.</span></span> <span data-ttu-id="0a8e4-154">這可確保會允許 toorun hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-154">This ensures hello scripts are allowed toorun.</span></span>

1. <span data-ttu-id="0a8e4-155">瀏覽過[hello Wingtip SaaS github 儲存機制](https://github.com/Microsoft/WingtipSaaS)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-155">Browse too[hello Wingtip SaaS github repo](https://github.com/Microsoft/WingtipSaaS).</span></span>
1. <span data-ttu-id="0a8e4-156">按一下 [複製或下載]。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-156">Click **Clone or download**.</span></span>
1. <span data-ttu-id="0a8e4-157">按一下**Download ZIP**儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-157">Click **Download ZIP** and save hello file.</span></span>
1. <span data-ttu-id="0a8e4-158">以滑鼠右鍵按一下 hello **WingtipSaaS master.zip**檔案，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-158">Right-click hello **WingtipSaaS-master.zip** file, and select **Properties**.</span></span>
1. <span data-ttu-id="0a8e4-159">在 hello**一般**索引標籤上，選取**解除封鎖**，然後按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-159">On hello **General** tab, select **Unblock**, and click **Apply**.</span></span>
1. <span data-ttu-id="0a8e4-160">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-160">Click **OK**.</span></span>
1. <span data-ttu-id="0a8e4-161">Hello 檔案解壓縮。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-161">Extract hello files.</span></span>

<span data-ttu-id="0a8e4-162">指令碼位於 hello *...\\WingtipSaaS master\\學習模組*資料夾。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-162">Scripts are located in hello *..\\WingtipSaaS-master\\Learning Modules* folder.</span></span>

## <a name="update-hello-configuration-file-for-this-deployment"></a><span data-ttu-id="0a8e4-163">更新此部署的 hello 設定檔</span><span class="sxs-lookup"><span data-stu-id="0a8e4-163">Update hello configuration file for this deployment</span></span>

<span data-ttu-id="0a8e4-164">再執行任何指令碼，設定 hello*資源群組*和*使用者*值**UserConfig.psm1**。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-164">Before running any scripts, set hello *resource group* and *user* values in **UserConfig.psm1**.</span></span> <span data-ttu-id="0a8e4-165">設定這些變數 toohello 您在部署期間設定的值。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-165">Set these variables toohello values you set during deployment.</span></span>

1. <span data-ttu-id="0a8e4-166">開啟...\\學習模組\\*UserConfig.psm1*在 hello *PowerShell ISE*</span><span class="sxs-lookup"><span data-stu-id="0a8e4-166">Open ...\\Learning Modules\\*UserConfig.psm1* in hello *PowerShell ISE*</span></span>
1. <span data-ttu-id="0a8e4-167">更新*ResourceGroupName*和*名稱*（位於行 10 和 11 只） 部署的 hello 特定值。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-167">Update *ResourceGroupName* and *Name* with hello specific values for your deployment (on lines 10 and 11 only).</span></span>
1. <span data-ttu-id="0a8e4-168">儲存 hello 變更 ！</span><span class="sxs-lookup"><span data-stu-id="0a8e4-168">Save hello changes!</span></span>

<span data-ttu-id="0a8e4-169">這裡將此設定，只可防止您在每個指令碼中具有 tooupdate 這些部署專屬的值。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-169">Setting this here simply keeps you from having tooupdate these deployment-specific values in every script.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="0a8e4-170">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a8e4-170">Run hello application</span></span>

<span data-ttu-id="0a8e4-171">hello 應用程式示範管道，例如搭配放逐，爵士梅花、 運動梅花裝載的事件。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-171">hello app showcases venues, such as concert halls, jazz clubs, sports clubs, that host events.</span></span> <span data-ttu-id="0a8e4-172">管道註冊為 hello Wingtip 平台，針對簡單的方式 toolist 事件客戶 （或租用戶），並銷售票券。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-172">Venues register as customers (or tenants) of hello Wingtip platform, for an easy way toolist events and sell tickets.</span></span> <span data-ttu-id="0a8e4-173">每個地點取得個人化的 web 應用程式 toomanage 及列出其事件並銷售票券，獨立且從其他租用戶隔離。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-173">Each venue gets a personalized web app toomanage and list their events and sell tickets, independent and isolated from other tenants.</span></span> <span data-ttu-id="0a8e4-174">在 hello 過程中，每個租用戶會取得 SQL 資料庫部署到 SQL 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-174">Under hello covers, each tenant gets a SQL database deployed into a SQL elastic pool.</span></span>

<span data-ttu-id="0a8e4-175">中央**事件中樞**Url 特定 tooyour 部署提供租用戶的清單。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-175">A central **Events Hub** provides a list of tenant URLs specific tooyour deployment.</span></span>

1. <span data-ttu-id="0a8e4-176">開啟 hello_事件中樞_網頁瀏覽器： http://events.wtp。&lt;使用者&gt;。 trafficmanager.net （取代為您的部署使用者名稱）：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-176">Open hello _Events Hub_ in your web browser: http://events.wtp.&lt;USER&gt;.trafficmanager.net (replace with your deployment's user name):</span></span>

    ![事件中樞](media/sql-database-saas-tutorial/events-hub.png)

1. <span data-ttu-id="0a8e4-178">按一下 [Events Hub (活動中心)] 中的 [Fabrikam Jazz Club (Fabrikam 爵士俱樂部)]。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-178">Click **Fabrikam Jazz Club** in the *Events Hub*.</span></span>

   ![事件](./media/sql-database-saas-tutorial/fabrikam.png)


<span data-ttu-id="0a8e4-180">toocontrol hello 發佈的連入要求，hello 應用程式會使用[ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-180">toocontrol hello distribution of incoming requests, hello app uses [*Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).</span></span> <span data-ttu-id="0a8e4-181">hello 事件頁面，也就是租用戶專屬，需要確定 hello Url 中包含租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-181">hello events pages, which are tenant-specific, require that tenant names are included in hello URLs.</span></span> <span data-ttu-id="0a8e4-182">所有 hello 租用戶 Url 包含您的特定*使用者*值，並遵循以下格式： http://events.wtp。&lt;使用者&gt;.trafficmanager.net/*fabrikamjazzclub*。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-182">All hello tenant URLs include your specific *User* value and follow this format: http://events.wtp.&lt;USER&gt;.trafficmanager.net/*fabrikamjazzclub*.</span></span> <span data-ttu-id="0a8e4-183">hello 事件應用程式剖析從 hello URL hello 租用戶名稱，並使用它 toocreate 類別目錄，使用金鑰 tooaccess [*分區對應管理*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-183">hello events app parses hello tenant name from hello URL and uses it toocreate a key tooaccess a catalog using [*shard map management*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management).</span></span> <span data-ttu-id="0a8e4-184">hello 目錄對應 hello 金鑰 toohello 租用戶的資料庫位置。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-184">hello catalog maps hello key toohello tenant's database location.</span></span> <span data-ttu-id="0a8e4-185">hello**事件中樞**Url 的每個資料庫 tooprovide hello 清單相關聯的 hello 目錄 tooretrieve hello 租用戶的名稱中使用擴充的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-185">hello **Events Hub** uses extended metadata in hello catalog tooretrieve hello tenant’s name associated with each database tooprovide hello list of URLs.</span></span>

<span data-ttu-id="0a8e4-186">在實際執行環境中，您通常會建立一筆 CNAME DNS 記錄[*點將公司網際網路網域*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) hello 流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-186">In a production environment, you would typically create a CNAME DNS record to [*point a company internet domain*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) to hello traffic manager profile.</span></span>

## <a name="start-generating-load-on-hello-tenant-databases"></a><span data-ttu-id="0a8e4-187">開始產生 hello 租用戶資料庫的負載</span><span class="sxs-lookup"><span data-stu-id="0a8e4-187">Start generating load on hello tenant databases</span></span>

<span data-ttu-id="0a8e4-188">既然 hello 的應用程式部署，讓我們將其放 toowork ！</span><span class="sxs-lookup"><span data-stu-id="0a8e4-188">Now that hello app is deployed, let’s put it toowork!</span></span> <span data-ttu-id="0a8e4-189">hello*示範 LoadGenerator* PowerShell 指令碼會啟動所有租用戶資料庫上執行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-189">hello *Demo-LoadGenerator* PowerShell script starts a workload running against all tenant databases.</span></span> <span data-ttu-id="0a8e4-190">許多 SaaS 應用程式的 hello 真實世界負載通常是偶發和無法預期。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-190">hello real-world load on many SaaS apps is typically sporadic and unpredictable.</span></span> <span data-ttu-id="0a8e4-191">toosimulate 這種類型的負載，hello 產生器會產生負載分散到所有租用戶，隨機暴增上發生隨機的間隔在每個租用戶。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-191">toosimulate this type of load, hello generator produces a load distributed across all tenants, with randomized bursts on each tenant occurring at randomized intervals.</span></span> <span data-ttu-id="0a8e4-192">因為這個緣故花幾分鐘的時間 hello 負載模式 tooemerge，因此，最佳的 toolet hello 產生器，至少三個執行或四分鐘後再監視 hello 負載。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-192">Because of this it takes several minutes for hello load pattern tooemerge, so it’s best toolet hello generator run for at least three or four minutes before monitoring hello load.</span></span>

1. <span data-ttu-id="0a8e4-193">在 hello *PowerShell ISE*，開啟 hello...\\學習模組\\公用程式\\*示範 LoadGenerator.ps1*指令碼。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-193">In hello *PowerShell ISE*, open hello ...\\Learning Modules\\Utilities\\*Demo-LoadGenerator.ps1* script.</span></span>
1. <span data-ttu-id="0a8e4-194">按**F5**執行 hello 指令碼，並啟動 hello 負載產生器 （保持 hello 預設參數值現在）。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-194">Press **F5** to run hello script and start hello load generator (leave hello default parameter values for now).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a8e4-195">toorun 其他指令碼中，開啟新的 PowerShell ISE 視窗。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-195">toorun other scripts, open a new PowerShell ISE window.</span></span> <span data-ttu-id="0a8e4-196">hello 負載產生器以一系列的工作執行，本機 PowerShell 工作階段中。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-196">hello load generator is running as a series of jobs in your local PowerShell session.</span></span> <span data-ttu-id="0a8e4-197">hello*示範 LoadGenerator.ps1* hello 實際負載產生器指令碼，以便為前景工作加上背景負載產生工作的一系列執行指令碼就會啟動。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-197">hello *Demo-LoadGenerator.ps1* script kicks off hello actual load generator script, which runs as a foreground task plus a series of background load-generation jobs.</span></span> <span data-ttu-id="0a8e4-198">負載產生器工作叫用 hello 目錄中註冊每個資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-198">A load-generator job is invoked for each database registered in hello catalog.</span></span> <span data-ttu-id="0a8e4-199">hello 工作執行本機的 PowerShell 工作階段中，所以正在關閉 hello PowerShell 工作階段停止所有工作。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-199">hello jobs are running in your local PowerShell session, so closing hello PowerShell session stops all jobs.</span></span> <span data-ttu-id="0a8e4-200">如果您暫停電腦，則負載產生會暫停並在您喚醒電腦時繼續。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-200">If you suspend your machine, load generation is paused and will resume when you wake up your machine.</span></span>

<span data-ttu-id="0a8e4-201">一旦 hello 負載產生器中，會叫用的工作負載產生每個租用戶，hello 前景工作仍會留在作業叫用的狀態，它會額外的背景工作啟動後續將佈建任何新租用戶。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-201">Once hello load generator invokes load-generation jobs for each tenant, hello foreground task remains in a job-invoking state, where it starts additional background jobs for any new tenants that are subsequently provisioned.</span></span> <span data-ttu-id="0a8e4-202">您可以使用*CTRL-C*或按 hello*停止*按鈕 toostop hello 前景工作，但現有的背景作業會繼續產生每個資料庫上的負載。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-202">You can use *Ctrl-C* or press hello *Stop* button toostop hello foreground task, but existing background jobs will continue generating load on each database.</span></span> <span data-ttu-id="0a8e4-203">如果您需要 toomonitor 並控制 hello 背景工作，請使用*Get-job*， *Receive-job*和*Stop-job*。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-203">If you need toomonitor and control hello background jobs, use *Get-Job*, *Receive-Job* and *Stop-Job*.</span></span> <span data-ttu-id="0a8e4-204">Hello 前景工作執行時您不能使用 hello 相同的 PowerShell 工作階段 tooexecute 其他指令碼。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-204">While hello foreground task is running you cannot use hello same PowerShell session tooexecute other scripts.</span></span> <span data-ttu-id="0a8e4-205">toorun 其他指令碼中，開啟新的 PowerShell ISE 視窗。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-205">toorun other scripts, open a new PowerShell ISE window.</span></span>

<span data-ttu-id="0a8e4-206">如果您想 toorestart hello 負載產生器工作階段，例如使用不同的參數，您可以停止 hello 前景工作，然後重新執行 hello*示範 LoadGenerator.ps1*指令碼。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-206">If you want toorestart hello load generator session, for example with different parameters, you can stop hello foreground task and then re-run hello *Demo-LoadGenerator.ps1* script.</span></span> <span data-ttu-id="0a8e4-207">重新執行*示範 LoadGenerator.ps1*先停止任何目前正在執行工作，然後再重新啟動 hello 產生器，就會啟動一組新的作業使用 hello 目前參數。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-207">Re-running *Demo-LoadGenerator.ps1* first stops any currently running jobs, and then restarts hello generator, which kicks off a new set of jobs using hello current parameters.</span></span>

<span data-ttu-id="0a8e4-208">現在請將保留在 hello 作業叫用的狀態下執行的 hello 負載產生器。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-208">For now, leave hello load generator running in hello job-invoking state.</span></span>


## <a name="provision-a-new-tenant"></a><span data-ttu-id="0a8e4-209">佈建新租用戶</span><span class="sxs-lookup"><span data-stu-id="0a8e4-209">Provision a new tenant</span></span>

<span data-ttu-id="0a8e4-210">hello 初始部署會建立三個範例租用戶，但我們來建立另一個租用戶 toosee 如何影響部署的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-210">hello initial deployment creates three sample tenants, but let’s create another tenant toosee how this impacts hello deployed application.</span></span> <span data-ttu-id="0a8e4-211">hello Wingtip SaaS 佈建租用工作流程會詳細說明 hello[佈建和類別目錄的教學課程](sql-database-saas-tutorial-provision-and-catalog.md)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-211">hello Wingtip SaaS provisioning-tenants workflow is detailed in hello [Provision and catalog tutorial](sql-database-saas-tutorial-provision-and-catalog.md).</span></span> <span data-ttu-id="0a8e4-212">在此步驟中，您會快速建立新的租用戶。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-212">In this step, you quickly create a new tenant.</span></span>

1. <span data-ttu-id="0a8e4-213">開啟...\\學習 Modules\Provision 和類別目錄\\*示範 ProvisionAndCatalog.ps1*在 hello *PowerShell ISE*。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-213">Open ...\\Learning Modules\Provision and Catalog\\*Demo-ProvisionAndCatalog.ps1* in hello *PowerShell ISE*.</span></span>
1. <span data-ttu-id="0a8e4-214">按**F5**執行 hello 指令碼 （保持 hello 預設值現在）。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-214">Press **F5** to run hello script (leave hello default values for now).</span></span>

   > [!NOTE]
   > <span data-ttu-id="0a8e4-215">許多 Wingtip SaaS 指令碼會使用*$PSScriptRoot* tooallow 瀏覽其他指令碼中的資料夾 toocall 函式。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-215">Many Wingtip SaaS scripts use *$PSScriptRoot* tooallow navigating folders toocall functions in other scripts.</span></span> <span data-ttu-id="0a8e4-216">此變數只會評估 hello 指令碼執行按下時**F5**。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-216">This variable is only evaluated when hello script is executed by pressing **F5**.</span></span>  <span data-ttu-id="0a8e4-217">醒目提示並執行選取項目 (**F8**) 可能會導致錯誤，因此請在執行指令碼時按 **F5**。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-217">Highlighting and running a selection (**F8**) can result in errors, so press **F5** when running scripts.</span></span>

<span data-ttu-id="0a8e4-218">hello 新租用戶資料庫是 SQL 彈性集區中建立、 初始化和註冊 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-218">hello new tenant database is created in a SQL elastic pool, initialized and registered in hello catalog.</span></span> <span data-ttu-id="0a8e4-219">成功佈建之後，新租用戶 hello 的票證銷售*事件*網站會出現在您的瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-219">After successful provisioning, hello new tenant's ticket-selling *Events* site appears in your browser:</span></span>

![新租用戶](./media/sql-database-saas-tutorial/red-maple-racing.png)

<span data-ttu-id="0a8e4-221">重新整理 hello*事件中樞*且 hello 新的租用戶現在會顯示 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-221">Refresh hello *Events Hub* and hello new tenant now appears in hello list.</span></span>


## <a name="explore-hello-servers-pools-and-tenant-databases"></a><span data-ttu-id="0a8e4-222">瀏覽 hello 伺服器集區和租用戶資料庫</span><span class="sxs-lookup"><span data-stu-id="0a8e4-222">Explore hello servers, pools, and tenant databases</span></span>

<span data-ttu-id="0a8e4-223">既然您已啟動的租用戶的 hello 集合上執行負載，讓我們看看一些已部署的 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-223">Now that you've started running a load against hello collection of tenants, let’s look at some of hello resources that were deployed:</span></span>

1. <span data-ttu-id="0a8e4-224">在[Azure 入口網站](http://portal.azure.com)，瀏覽 SQL server 的 tooyour 清單並開啟**目錄-&lt;使用者&gt;**伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-224">In the [Azure portal](http://portal.azure.com), browse tooyour list of SQL servers and open the **catalog-&lt;USER&gt;** server.</span></span> <span data-ttu-id="0a8e4-225">hello 類別目錄伺服器包含兩個資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-225">hello catalog server contains two databases.</span></span> <span data-ttu-id="0a8e4-226">hello **tenantcatalog**，和 hello **basetenantdb** (空*黃金*或範本資料庫複製 toocreate 新租用戶)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-226">hello **tenantcatalog**, and hello **basetenantdb** (an empty *golden* or template database that is copied toocreate new tenants).</span></span>

   ![資料庫](./media/sql-database-saas-tutorial/databases.png)

1. <span data-ttu-id="0a8e4-228">返回 SQL server 的 tooyour 清單並開啟 hello **tenants1-&lt;使用者&gt;**持有 hello 租用戶資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-228">Go back tooyour list of SQL servers and open hello **tenants1-&lt;USER&gt;** server that holds hello tenant databases.</span></span> <span data-ttu-id="0a8e4-229">每個租用戶資料庫都是 50 eDTU 標準集區中的「彈性標準」資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-229">Each tenant database is an _Elastic Standard_ database in a 50 eDTU standard pool.</span></span> <span data-ttu-id="0a8e4-230">同時也請注意沒有_紅色楓樹賽_資料庫，您先前佈建的 hello 租用戶資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-230">Also notice there is a _Red Maple Racing_ database, hello tenant database you provisioned previously.</span></span>

   ![伺服器](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a><span data-ttu-id="0a8e4-232">監視 hello 集區</span><span class="sxs-lookup"><span data-stu-id="0a8e4-232">Monitor hello pool</span></span>

<span data-ttu-id="0a8e4-233">如果 hello 負載產生器已執行幾分鐘的時間，足夠的資料應該可用 toostart 查看一些 hello 監視集區和資料庫內建功能。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-233">If hello load generator has been running for several minutes, enough data should be available toostart looking at some of hello monitoring capabilities built into pools and databases.</span></span>

1. <span data-ttu-id="0a8e4-234">瀏覽 toohello 伺服器**tenants1-&lt;使用者&gt;**，然後按一下**Pool1**來檢視資源使用率 hello 集區 （執行 hello 下列圖表中的一小時的 hello 負載產生器）:</span><span class="sxs-lookup"><span data-stu-id="0a8e4-234">Browse toohello server **tenants1-&lt;USER&gt;**, and click **Pool1** to view resource utilization for hello pool (hello load generator ran for an hour in hello following charts):</span></span>

   ![監視集區](./media/sql-database-saas-tutorial/monitor-pool.png)

<span data-ttu-id="0a8e4-236">這兩個圖表清楚說明：彈性集區和 SQL Database 非常適合 SaaS 應用程式工作負載。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-236">What these two charts nicely illustrate, is how well suited elastic pools and SQL Database are for SaaS application workloads.</span></span> <span data-ttu-id="0a8e4-237">為每個 invalidreportparameterexception tooas 一樣 40 Edtu 輕鬆 50 eDTU 集區中所支援的四個資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-237">Four databases that are each bursting tooas much as 40 eDTUs are easily being supported in a 50 eDTU pool.</span></span> <span data-ttu-id="0a8e4-238">如果它們已佈建為獨立資料庫，它們就是每個需要 toobe S2 (50 的 DTU) toosupport hello 暴增。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-238">If they were provisioned as standalone databases, they would each need toobe an S2 (50 DTU) toosupport hello bursts.</span></span> <span data-ttu-id="0a8e4-239">hello 成本的 4 獨立 S2 資料庫是 hello 集區中，幾乎 3 次 hello 價格和 hello 集區仍有大量的許多的多個資料庫的空間。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-239">hello cost of 4 standalone S2 databases would be nearly 3 times hello price of hello pool, and hello pool still has plenty of headroom for many more databases.</span></span> <span data-ttu-id="0a8e4-240">在真實世界的情況下，SQL Database 客戶目前正在 too500 200 eDTU 集區中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-240">In real-world situations, SQL Database customers are currently running up too500 databases in 200 eDTU pools.</span></span> <span data-ttu-id="0a8e4-241">如需詳細資訊，請參閱 hello[效能監視教學課程](sql-database-saas-tutorial-performance-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="0a8e4-241">For more information, see hello [performance monitoring tutorial](sql-database-saas-tutorial-performance-monitoring.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="0a8e4-242">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a8e4-242">Next steps</span></span>

<span data-ttu-id="0a8e4-243">在本教學課程中，您已了解：</span><span class="sxs-lookup"><span data-stu-id="0a8e4-243">In this tutorial you learned:</span></span>

> [!div class="checklist"]

> * <span data-ttu-id="0a8e4-244">如何 toodeploy hello Wingtip SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a8e4-244">How toodeploy hello Wingtip SaaS application</span></span>
> * <span data-ttu-id="0a8e4-245">關於 hello、 集區的伺服器和資料庫組成 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0a8e4-245">About hello servers, pools, and databases that make up hello app</span></span>
> * <span data-ttu-id="0a8e4-246">租用戶不對應的 tootheir 資料以 hello*類別目錄*</span><span class="sxs-lookup"><span data-stu-id="0a8e4-246">Tenants are mapped tootheir data with hello *catalog*</span></span>
> * <span data-ttu-id="0a8e4-247">如何 tooprovision 新租用戶</span><span class="sxs-lookup"><span data-stu-id="0a8e4-247">How tooprovision new tenants</span></span>
> * <span data-ttu-id="0a8e4-248">如何 tooview 集區使用量 toomonitor 租用戶活動</span><span class="sxs-lookup"><span data-stu-id="0a8e4-248">How tooview pool utilization toomonitor tenant activity</span></span>
> * <span data-ttu-id="0a8e4-249">Toodelete 範例資源 toostop 相關性計費</span><span class="sxs-lookup"><span data-stu-id="0a8e4-249">How toodelete sample resources toostop related billing</span></span>

<span data-ttu-id="0a8e4-250">現在，請嘗試 hello[佈建和類別目錄的教學課程](sql-database-saas-tutorial-provision-and-catalog.md)</span><span class="sxs-lookup"><span data-stu-id="0a8e4-250">Now try hello [Provision and catalog tutorial](sql-database-saas-tutorial-provision-and-catalog.md)</span></span>



## <a name="additional-resources"></a><span data-ttu-id="0a8e4-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="0a8e4-251">Additional resources</span></span>

* <span data-ttu-id="0a8e4-252">其他[建置的教學課程 hello Wingtip SaaS 應用程式](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="0a8e4-252">Additional [tutorials that build on hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* <span data-ttu-id="0a8e4-253">toolearn 有關彈性集區，請參閱[*什麼是 Azure SQL 彈性集區*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)</span><span class="sxs-lookup"><span data-stu-id="0a8e4-253">toolearn about elastic pools, see [*What is an Azure SQL elastic pool*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)</span></span>
* <span data-ttu-id="0a8e4-254">toolearn 關於彈性的工作，請參閱[*管理向外延展雲端資料庫*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)</span><span class="sxs-lookup"><span data-stu-id="0a8e4-254">toolearn about elastic jobs, see [*Managing scaled-out cloud databases*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)</span></span>
* <span data-ttu-id="0a8e4-255">toolearn 有關多租用戶 SaaS 應用程式，請參閱[*設計模式為多租用戶 SaaS 應用程式*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="0a8e4-255">toolearn about multi-tenant SaaS applications, see [*Design patterns for multi-tenant SaaS applications*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>
