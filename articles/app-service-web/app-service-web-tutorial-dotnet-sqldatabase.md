---
title: "aaaBuild Azure SQL Database 的 ASP.NET 應用程式 |Microsoft 文件"
description: "深入了解如何 tooget ASP.NET 應用程式在 Azure 中，使用連接 tooa SQL 資料庫。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="6b72b-103">在 Azure 中搭配 SQL Database 來建置 ASP.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="6b72b-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="6b72b-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="6b72b-105">本教學課程告訴您如何 toodeploy 資料驅動的 ASP.NET web 應用程式在 Azure 中的並將它連接太[Azure SQL Database](../sql-database/sql-database-technical-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="6b72b-106">當您完成時，您有執行的 ASP.NET 應用程式[Azure App Service](../app-service/app-service-value-prop-what-is.md)且連線 tooSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![已在 Azure Web 應用程式中發佈的 ASP.NET 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="6b72b-108">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="6b72b-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b72b-109">在 Azure 中建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="6b72b-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="6b72b-110">連接的 ASP.NET 應用程式 tooSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="6b72b-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="6b72b-111">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b72b-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="6b72b-112">更新 hello 資料模型，部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="6b72b-113">從 Azure tooyour 終端機的資料流記錄檔</span><span class="sxs-lookup"><span data-stu-id="6b72b-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="6b72b-114">管理 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b72b-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="6b72b-115">Prerequisites</span></span>

<span data-ttu-id="6b72b-116">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="6b72b-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="6b72b-117">安裝[Visual Studio 2017](https://www.visualstudio.com/downloads/)以下列工作負載的 hello:</span><span class="sxs-lookup"><span data-stu-id="6b72b-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="6b72b-118">**ASP.NET 和 Web 開發**</span><span class="sxs-lookup"><span data-stu-id="6b72b-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="6b72b-119">**Azure 開發**</span><span class="sxs-lookup"><span data-stu-id="6b72b-119">**Azure development**</span></span>

  ![ASP.NET 和 Web 開發及 Azure 開發 (在 [Web 和雲端] 之下)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="6b72b-121">下載 hello 範例</span><span class="sxs-lookup"><span data-stu-id="6b72b-121">Download hello sample</span></span>

<span data-ttu-id="6b72b-122">[下載 hello 範例專案](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="6b72b-123">擷取 （解壓縮） hello *dotnet sqldb 教學課程-master.zip*檔案。</span><span class="sxs-lookup"><span data-stu-id="6b72b-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="6b72b-124">hello 範例專案包含基本[ASP.NET MVC](https://www.asp.net/mvc) CRUD （建立讀取-更新-刪除） 的應用程式使用[Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="6b72b-125">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-125">Run hello app</span></span>

<span data-ttu-id="6b72b-126">開啟 hello *dotnet-sqldb-教學課程的主要/DotNetAppSqlDb.sln* Visual Studio 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="6b72b-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="6b72b-127">型別`Ctrl+F5`toorun hello 應用程式，但不偵錯。</span><span class="sxs-lookup"><span data-stu-id="6b72b-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="6b72b-128">hello 應用程式會顯示在預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="6b72b-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="6b72b-129">選取 hello**新建**連結，並建立幾*待辦事項*項目。</span><span class="sxs-lookup"><span data-stu-id="6b72b-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![[新增 ASP.NET 專案] 對話方塊](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="6b72b-131">測試 hello**編輯**，**詳細資料**，和**刪除**連結。</span><span class="sxs-lookup"><span data-stu-id="6b72b-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="6b72b-132">hello 應用程式會將資料庫內容 tooconnect 使用 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="6b72b-133">在此範例中，hello 資料庫內容會使用名為連接字串`MyDbConnection`。</span><span class="sxs-lookup"><span data-stu-id="6b72b-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="6b72b-134">設定 hello 連接字串中 hello *Web.config*檔案和參考中的 hello *Models/MyDatabaseContext.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="6b72b-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="6b72b-135">稍後 hello 教學課程 tooconnect hello Azure web 應用程式 tooan Azure SQL Database 會使用 hello 連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="6b72b-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="6b72b-136">發行 SQL Database 的 tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b72b-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="6b72b-137">在 [hello**方案總管] 中**，以滑鼠右鍵按一下您**DotNetAppSqlDb**專案，然後選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![從方案總管發佈](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="6b72b-139">確定已選取 [Microsoft Azure App Service]，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![從專案概觀頁面發佈](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="6b72b-141">發行會開啟 hello**建立 App Service**對話方塊中，可協助您建立所有 hello toorun 您需要在 Azure 中的 ASP.NET web 應用程式的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="6b72b-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="6b72b-142">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b72b-142">Sign in tooAzure</span></span>

<span data-ttu-id="6b72b-143">在 hello**建立 App Service** ] 對話方塊中，按一下 [**將帳戶加入**，然後登入 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b72b-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="6b72b-144">如果您已登入 Microsoft 帳戶，請確定該帳戶保留您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b72b-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="6b72b-145">如果 hello 登入的 Microsoft 帳戶沒有 Azure 訂用帳戶，按一下 tooadd hello 正確的帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b72b-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![登入 tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="6b72b-147">一旦登入，您已準備好 toocreate 所有 hello 您需要在這個對話方塊中，Azure web 應用程式的資源。</span><span class="sxs-lookup"><span data-stu-id="6b72b-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="6b72b-148">設定 hello web 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="6b72b-148">Configure hello web app name</span></span>

<span data-ttu-id="6b72b-149">您可以保留 hello 產生 web 應用程式名稱，或將它變更 tooanother 唯一的名稱 (有效的字元是`a-z`， `0-9`，和`-`)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="6b72b-150">hello web 應用程式名稱應用程式時做 hello 預設 URL 的一部分 (`<app_name>.azurewebsites.net`，其中`<app_name>`是您的 web 應用程式名稱)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="6b72b-151">hello web 應用程式名稱必須 toobe 唯一跨 Azure 中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![建立 App Service 對話方塊](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="6b72b-153">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="6b72b-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="6b72b-154">下一步太**資源群組**，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-154">Next too**Resource Group**, click **New**.</span></span>

![下一步 tooResource 群組中，按一下 [新增]。](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="6b72b-156">名稱 hello 資源群組**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="6b72b-157">不要按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-157">Do not click **Create**.</span></span> <span data-ttu-id="6b72b-158">您必須先 tooset 稍後步驟中將 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="6b72b-159">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="6b72b-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="6b72b-160">下一步太**App Service 方案**，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="6b72b-161">在 hello**設定應用程式服務方案** 對話方塊中，設定下列設定的 hello 與 hello 新應用程式服務方案：</span><span class="sxs-lookup"><span data-stu-id="6b72b-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![建立 App Service 方案](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="6b72b-163">設定</span><span class="sxs-lookup"><span data-stu-id="6b72b-163">Setting</span></span>  | <span data-ttu-id="6b72b-164">建議的值</span><span class="sxs-lookup"><span data-stu-id="6b72b-164">Suggested value</span></span> | <span data-ttu-id="6b72b-165">如需 Blob 的詳細資訊，</span><span class="sxs-lookup"><span data-stu-id="6b72b-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="6b72b-166">**App Service 方案**</span><span class="sxs-lookup"><span data-stu-id="6b72b-166">**App Service Plan**</span></span>| <span data-ttu-id="6b72b-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6b72b-167">myAppServicePlan</span></span> | [<span data-ttu-id="6b72b-168">App Service 方案</span><span class="sxs-lookup"><span data-stu-id="6b72b-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="6b72b-169">**位置**</span><span class="sxs-lookup"><span data-stu-id="6b72b-169">**Location**</span></span>| <span data-ttu-id="6b72b-170">西歐</span><span class="sxs-lookup"><span data-stu-id="6b72b-170">West Europe</span></span> | [<span data-ttu-id="6b72b-171">Azure 區域</span><span class="sxs-lookup"><span data-stu-id="6b72b-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="6b72b-172">**大小**</span><span class="sxs-lookup"><span data-stu-id="6b72b-172">**Size**</span></span>| <span data-ttu-id="6b72b-173">免費</span><span class="sxs-lookup"><span data-stu-id="6b72b-173">Free</span></span> | [<span data-ttu-id="6b72b-174">定價層</span><span class="sxs-lookup"><span data-stu-id="6b72b-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="6b72b-175">建立 SQL Server 執行個體</span><span class="sxs-lookup"><span data-stu-id="6b72b-175">Create a SQL Server instance</span></span>

<span data-ttu-id="6b72b-176">建立資料庫之前，您需要 [Azure SQL Database 邏輯伺服器](../sql-database/sql-database-features.md)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="6b72b-177">邏輯伺服器包含一組當作群組管理的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="6b72b-178">選取 [瀏覽其他 Azure 服務]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-178">Select **Explore additional Azure services**.</span></span>

![設定 Web 應用程式名稱](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="6b72b-180">在 hello**服務**索引標籤上，按一下 hello  **+** 圖示下一步太**SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![在 hello 服務索引標籤上，按一下 hello + 圖示下一步 tooSQL 資料庫。](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="6b72b-182">在 [hello**設定 SQL Database** ] 對話方塊中，按一下**新增**下一步太**SQL Server**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="6b72b-183">唯一的伺服器名稱隨即產生。</span><span class="sxs-lookup"><span data-stu-id="6b72b-183">A unique server name is generated.</span></span> <span data-ttu-id="6b72b-184">這個名稱會用於 hello 預設 URL 的一部分邏輯伺服器， `<server_name>.database.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="6b72b-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="6b72b-185">它在 Azure 中的所有邏輯伺服器執行個體之間必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6b72b-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="6b72b-186">您可以變更 hello 伺服器名稱，但本教學課程中，保留 hello 產生值。</span><span class="sxs-lookup"><span data-stu-id="6b72b-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="6b72b-187">新增系統管理員使用者名稱和密碼，然後選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="6b72b-188">如需密碼複雜性需求，請參閱[密碼原則](/sql/relational-databases/security/password-policy)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="6b72b-189">請記住這個使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6b72b-189">Remember this username and password.</span></span> <span data-ttu-id="6b72b-190">需要 toomanage hello 邏輯伺服器執行個體更新版本。</span><span class="sxs-lookup"><span data-stu-id="6b72b-190">You need them toomanage hello logical server instance later.</span></span>

![建立 SQL Server 執行個體](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="6b72b-192">建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="6b72b-192">Create a SQL Database</span></span>

<span data-ttu-id="6b72b-193">在 hello**設定 SQL Database**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="6b72b-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="6b72b-194">保留產生 hello 預設**資料庫名稱**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="6b72b-195">在 [連接字串名稱] 中，輸入 *MyDbConnection*。</span><span class="sxs-lookup"><span data-stu-id="6b72b-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="6b72b-196">此名稱必須符合 hello 連接字串中所參考*Models/MyDatabaseContext.cs*。</span><span class="sxs-lookup"><span data-stu-id="6b72b-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="6b72b-197">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="6b72b-197">Select **OK**.</span></span>

![設定 SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="6b72b-199">hello**建立 App Service**對話方塊會顯示 hello 資源已建立。</span><span class="sxs-lookup"><span data-stu-id="6b72b-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="6b72b-200">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6b72b-200">Click **Create**.</span></span> 

![您已建立 hello 資源](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="6b72b-202">一旦 hello 精靈完成建立 hello Azure 資源時，它會發行您的 ASP.NET 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6b72b-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="6b72b-203">預設的瀏覽器會使用 hello URL toohello 部署應用程式啟動。</span><span class="sxs-lookup"><span data-stu-id="6b72b-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="6b72b-204">新增幾個待辦事項項目。</span><span class="sxs-lookup"><span data-stu-id="6b72b-204">Add a few to-do items.</span></span>

![已在 Azure Web 應用程式中發佈的 ASP.NET 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="6b72b-206">恭喜！</span><span class="sxs-lookup"><span data-stu-id="6b72b-206">Congratulations!</span></span> <span data-ttu-id="6b72b-207">您的資料導向 ASP.NET 應用程式正在 Azure App Service 中執行。</span><span class="sxs-lookup"><span data-stu-id="6b72b-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="6b72b-208">存取 hello 本機 SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="6b72b-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="6b72b-209">Visual Studio 可讓您瀏覽和管理您新的 SQL 資料庫，輕鬆地在 hello **SQL Server 物件總管**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="6b72b-210">建立資料庫連接</span><span class="sxs-lookup"><span data-stu-id="6b72b-210">Create a database connection</span></span>

<span data-ttu-id="6b72b-211">從 hello**檢視**功能表上，選取**SQL Server 物件總管**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="6b72b-212">頂端的 hello **SQL Server 物件總管**，按一下 hello**加入 SQL Server**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6b72b-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="6b72b-213">設定 hello 資料庫連接</span><span class="sxs-lookup"><span data-stu-id="6b72b-213">Configure hello database connection</span></span>

<span data-ttu-id="6b72b-214">在 [hello**連接**] 對話方塊中，展開 hello **Azure**節點。</span><span class="sxs-lookup"><span data-stu-id="6b72b-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="6b72b-215">此處會列出 Azure 中您所有的 SQL Database 執行個體。</span><span class="sxs-lookup"><span data-stu-id="6b72b-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="6b72b-216">選取 hello `DotNetAppSqlDb` SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="6b72b-217">您稍早建立的 hello 連線會自動填入 hello 底部。</span><span class="sxs-lookup"><span data-stu-id="6b72b-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="6b72b-218">輸入您稍早建立的 hello 資料庫系統管理員密碼，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![從 Visual Studio 設定資料庫連接](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="6b72b-220">允許來自您電腦的用戶端連接</span><span class="sxs-lookup"><span data-stu-id="6b72b-220">Allow client connection from your computer</span></span>

<span data-ttu-id="6b72b-221">hello**建立新的防火牆規則**對話方塊開啟。</span><span class="sxs-lookup"><span data-stu-id="6b72b-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="6b72b-222">根據預設，您的 SQL Database 執行個體僅允許來自 Azure 服務 (例如 Azure Web 應用程式) 的連線。</span><span class="sxs-lookup"><span data-stu-id="6b72b-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="6b72b-223">tooconnect tooyour 資料庫，請在 hello SQL Database 執行個體中建立的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="6b72b-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="6b72b-224">hello 防火牆規則可讓您的本機電腦的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6b72b-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="6b72b-225">hello 對話方塊已填入您的電腦公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6b72b-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="6b72b-226">確定已選取 [加入我的用戶端 IP]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![設定 SQL Database 執行個體的防火牆](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="6b72b-228">Visual Studio 完成建立您的 SQL Database 執行個體的 hello 防火牆設定時，一旦您的連線會出現在**SQL Server 物件總管**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="6b72b-229">在這裡，您可以執行 hello 最常見資料庫作業，例如執行查詢，建立檢視和預存程序，以及更多。</span><span class="sxs-lookup"><span data-stu-id="6b72b-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="6b72b-230">以滑鼠右鍵按一下 hello`Todoes`資料表，然後選取**檢視資料**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![探索 SQL Database 物件](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="6b72b-232">使用 Code First 移轉更新應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="6b72b-233">您可以在 Azure 中使用 hello 熟悉的工具，在 Visual Studio tooupdate 資料庫與 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="6b72b-234">在此步驟中，您會在 Entity Framework toomake 變更 tooyour 資料庫結構描述中使用 Code First 移轉，並將它發行 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="6b72b-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="6b72b-235">如需有關使用 Entity Framework Code First 移轉的詳細資訊，請參閱[使用 MVC 5 開始使用 Entity Framework 6 Code First](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="6b72b-236">更新資料模型</span><span class="sxs-lookup"><span data-stu-id="6b72b-236">Update your data model</span></span>

<span data-ttu-id="6b72b-237">開啟_Models\Todo.cs_ hello 程式碼編輯器中。</span><span class="sxs-lookup"><span data-stu-id="6b72b-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="6b72b-238">新增下列屬性 toohello hello`ToDo`類別：</span><span class="sxs-lookup"><span data-stu-id="6b72b-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="6b72b-239">在本機執行 Code First 移轉</span><span class="sxs-lookup"><span data-stu-id="6b72b-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="6b72b-240">執行一些命令 toomake 更新 tooyour 本機資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="6b72b-241">從 hello**工具**功能表上，按一下  **NuGet 套件管理員** > **Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="6b72b-242">在 [hello 封裝管理員主控台] 視窗，啟用 Code First 移轉：</span><span class="sxs-lookup"><span data-stu-id="6b72b-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="6b72b-243">新增移轉：</span><span class="sxs-lookup"><span data-stu-id="6b72b-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="6b72b-244">更新 hello 本機資料庫：</span><span class="sxs-lookup"><span data-stu-id="6b72b-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="6b72b-245">型別`Ctrl+F5`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="6b72b-246">測試 hello 編輯詳細資料，與建立連結。</span><span class="sxs-lookup"><span data-stu-id="6b72b-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="6b72b-247">如果 hello 應用程式載入無錯誤，Code First 移轉已成功。</span><span class="sxs-lookup"><span data-stu-id="6b72b-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="6b72b-248">不過，您的頁面仍看起來會 hello 相同，因為應用程式邏輯還未使用這個新屬性。</span><span class="sxs-lookup"><span data-stu-id="6b72b-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="6b72b-249">使用 hello 新屬性</span><span class="sxs-lookup"><span data-stu-id="6b72b-249">Use hello new property</span></span>

<span data-ttu-id="6b72b-250">在您的程式碼 toouse hello 進行一些變更`Done`屬性。</span><span class="sxs-lookup"><span data-stu-id="6b72b-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="6b72b-251">為了簡單起見，本教學課程中，您只會 toochange hello`Index`和`Create`toosee hello 屬性檢視作用中。</span><span class="sxs-lookup"><span data-stu-id="6b72b-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="6b72b-252">開啟 _Controllers\TodosController.cs_。</span><span class="sxs-lookup"><span data-stu-id="6b72b-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="6b72b-253">尋找 hello`Create()`方法並加入`Done`toohello hello 中屬性清單`Bind`屬性。</span><span class="sxs-lookup"><span data-stu-id="6b72b-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="6b72b-254">當您完成時，您`Create()`方法簽章看起來像下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6b72b-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="6b72b-255">開啟 _Views\Todos\Create.cshtml_。</span><span class="sxs-lookup"><span data-stu-id="6b72b-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="6b72b-256">在 hello Razor 程式碼，您應該會看到`<div class="form-group">`項目，會使用`model.Description`，和另一個`<div class="form-group">`項目，會使用`model.CreatedDate`。</span><span class="sxs-lookup"><span data-stu-id="6b72b-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="6b72b-257">在這兩個元素的正後方，新增另一個使用 `model.Done` 的 `<div class="form-group">` 元素：</span><span class="sxs-lookup"><span data-stu-id="6b72b-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="6b72b-258">開啟 _Views\Todos\Index.cshtml_。</span><span class="sxs-lookup"><span data-stu-id="6b72b-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="6b72b-259">搜尋空白的 hello`<th></th>`項目。</span><span class="sxs-lookup"><span data-stu-id="6b72b-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="6b72b-260">這個元素的正上方加入下列 Razor 程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6b72b-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="6b72b-261">尋找 hello`<td>`項目，包含 hello `Html.ActionLink()` helper 方法。</span><span class="sxs-lookup"><span data-stu-id="6b72b-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="6b72b-262">這個元素的正上方加入下列 Razor 程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="6b72b-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="6b72b-263">您只需要在 hello toosee hello 變更`Index`和`Create`檢視。</span><span class="sxs-lookup"><span data-stu-id="6b72b-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="6b72b-264">型別`Ctrl+F5`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="6b72b-265">您現在可以新增待辦事項項目，並且勾選 [完成]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="6b72b-266">然後，它應該會在您的首頁中顯示為已完成的項目。</span><span class="sxs-lookup"><span data-stu-id="6b72b-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="6b72b-267">請記住該 hello`Edit`檢視不會顯示 hello`Done`欄位，因為您沒有變更 hello`Edit`檢視。</span><span class="sxs-lookup"><span data-stu-id="6b72b-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="6b72b-268">啟用 Azure 中的 Code First 移轉</span><span class="sxs-lookup"><span data-stu-id="6b72b-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="6b72b-269">現在，您的程式碼變更的運作方式，包括資料庫移轉，您將它發行 tooyour Azure web 應用程式，然後太 Code First 移轉更新您的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="6b72b-270">就像之前一樣，以滑鼠右鍵按一下專案，然後選取 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="6b72b-271">按一下**設定**tooopen hello 發行精靈。</span><span class="sxs-lookup"><span data-stu-id="6b72b-271">Click **Settings** tooopen hello publish wizard.</span></span>

![開啟發佈設定](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="6b72b-273">在 hello 精靈 中，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="6b72b-274">請確定該 hello 連接字串中已填入您的 SQL Database **MyDatabaseContext (MyDbConnection)**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="6b72b-275">您可能需要 tooselect hello **myToDoAppDb**從 hello 下拉式清單中的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6b72b-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="6b72b-276">選取 [執行 Code First 移轉 (在應用程式啟動時執行)] ，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![在 Azure Web 應用程式中啟用 Code First 移轉](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="6b72b-278">發佈您的變更</span><span class="sxs-lookup"><span data-stu-id="6b72b-278">Publish your changes</span></span>

<span data-ttu-id="6b72b-279">現在，您已在 Azure Web 應用程式中啟用 Code First 移轉，只需發佈您的程式碼變更即可。</span><span class="sxs-lookup"><span data-stu-id="6b72b-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="6b72b-280">在 hello 發行頁中，按一下**發行**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="6b72b-281">嘗試再次新增待辦事項，然後選取 [完成]，而它們應該會在您的首頁中顯示為已完成的項目。</span><span class="sxs-lookup"><span data-stu-id="6b72b-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Code First 移轉之後的 Azure Web 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="6b72b-283">仍會顯示您現有的所有待辦事項項目。</span><span class="sxs-lookup"><span data-stu-id="6b72b-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="6b72b-284">當您重新發佈 ASP.NET 應用程式時，您 SQL Database 中現有的資料不會遺失。</span><span class="sxs-lookup"><span data-stu-id="6b72b-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="6b72b-285">此外，Code First 移轉只會變更 hello 資料結構描述，會保留現有的資料。</span><span class="sxs-lookup"><span data-stu-id="6b72b-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="6b72b-286">資料流應用程式記錄</span><span class="sxs-lookup"><span data-stu-id="6b72b-286">Stream application logs</span></span>

<span data-ttu-id="6b72b-287">您可以直接從您的 Azure web 應用程式 tooVisual Studio 串流追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="6b72b-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="6b72b-288">開啟 _Controllers\TodosController.cs_。</span><span class="sxs-lookup"><span data-stu-id="6b72b-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="6b72b-289">每個動作都是以 `Trace.WriteLine()` 方法開始。</span><span class="sxs-lookup"><span data-stu-id="6b72b-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="6b72b-290">此程式碼會加入 tooshow 您 tooadd 追蹤訊息 tooyour Azure web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="6b72b-291">開啟伺服器總管</span><span class="sxs-lookup"><span data-stu-id="6b72b-291">Open Server Explorer</span></span>

<span data-ttu-id="6b72b-292">從 hello**檢視**功能表上，選取**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="6b72b-293">您可以在 [伺服器總管] 中設定 Azure Web 應用程式的記錄。</span><span class="sxs-lookup"><span data-stu-id="6b72b-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="6b72b-294">啟用記錄資料流</span><span class="sxs-lookup"><span data-stu-id="6b72b-294">Enable log streaming</span></span>

<span data-ttu-id="6b72b-295">在 [伺服器總管] 中，展開 [Azure] > [App Service]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="6b72b-296">展開 hello **myResourceGroup**資源群組時所建立您第一次建立 hello Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="6b72b-297">以滑鼠右鍵按一下您的 Azure Web 應用程式，然後選取 [檢視資料流記錄]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![啟用記錄資料流](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="6b72b-299">hello 記錄檔現在串流處理到 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="6b72b-299">hello logs are now streamed into hello **Output** window.</span></span> 

![[輸出] 視窗中的記錄資料流](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="6b72b-301">不過，您不尚未看到任何 hello 追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="6b72b-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="6b72b-302">因為當您第一次選取**檢視串流記錄**，Azure web 應用程式設定 hello 追蹤層級太`Error`，這只記錄錯誤事件 (以 hello`Trace.TraceError()`方法)。</span><span class="sxs-lookup"><span data-stu-id="6b72b-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="6b72b-303">變更追蹤層級</span><span class="sxs-lookup"><span data-stu-id="6b72b-303">Change trace levels</span></span>

<span data-ttu-id="6b72b-304">toochange hello 追蹤層級 toooutput 其他追蹤訊息，請移回太**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="6b72b-305">再次以滑鼠右鍵按一下您的 Azure Web 應用程式，然後選取 [設定]。</span><span class="sxs-lookup"><span data-stu-id="6b72b-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="6b72b-306">在 hello**的應用程式記錄 （檔案系統）**下拉式清單中，選取**Verbose**。</span><span class="sxs-lookup"><span data-stu-id="6b72b-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="6b72b-307">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6b72b-307">Click **Save**.</span></span>

![變更追蹤層級 tooVerbose](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="6b72b-309">您可以試驗不同的追蹤層級 toosee 的訊息類型會顯示每個層級。</span><span class="sxs-lookup"><span data-stu-id="6b72b-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="6b72b-310">例如，hello**資訊**層級包含所建立的所有記錄檔`Trace.TraceInformation()`， `Trace.TraceWarning()`，和`Trace.TraceError()`，但不是所建立的記錄檔`Trace.WriteLine()`。</span><span class="sxs-lookup"><span data-stu-id="6b72b-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="6b72b-311">在瀏覽器，請按一下 Azure 中的 hello 待辦事項清單應用程式周圍。</span><span class="sxs-lookup"><span data-stu-id="6b72b-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="6b72b-312">hello 追蹤訊息現在進行串流 toohello**輸出**Visual Studio 中的視窗。</span><span class="sxs-lookup"><span data-stu-id="6b72b-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="6b72b-313">停止記錄資料流</span><span class="sxs-lookup"><span data-stu-id="6b72b-313">Stop log streaming</span></span>

<span data-ttu-id="6b72b-314">toostop hello 記錄串流服務，請按一下 hello**停止監視**按鈕在 hello**輸出**視窗。</span><span class="sxs-lookup"><span data-stu-id="6b72b-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![停止記錄資料流](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="6b72b-316">管理您的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-316">Manage your Azure web app</span></span>

<span data-ttu-id="6b72b-317">移 toohello [Azure 入口網站](https://portal.azure.com)toosee hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="6b72b-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="6b72b-318">從 hello 左窗格中，按一下  **App Service**，然後按一下 hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="6b72b-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="6b72b-320">您已來到 Web 應用程式的分頁。</span><span class="sxs-lookup"><span data-stu-id="6b72b-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="6b72b-321">根據預設，hello 入口網站會顯示 hello**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="6b72b-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="6b72b-322">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="6b72b-323">您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="6b72b-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="6b72b-324">在左邊 hello 頁面 hello hello 索引標籤會顯示 hello 不同的組態頁面，您可以開啟。</span><span class="sxs-lookup"><span data-stu-id="6b72b-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="6b72b-326">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b72b-326">Next steps</span></span>

<span data-ttu-id="6b72b-327">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="6b72b-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b72b-328">在 Azure 中建立 SQL Database</span><span class="sxs-lookup"><span data-stu-id="6b72b-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="6b72b-329">連接的 ASP.NET 應用程式 tooSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="6b72b-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="6b72b-330">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="6b72b-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="6b72b-331">更新 hello 資料模型，部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="6b72b-332">從 Azure tooyour 終端機的資料流記錄檔</span><span class="sxs-lookup"><span data-stu-id="6b72b-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="6b72b-333">管理 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="6b72b-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="6b72b-334">前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 toohello web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="6b72b-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b72b-335">將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應</span><span class="sxs-lookup"><span data-stu-id="6b72b-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
