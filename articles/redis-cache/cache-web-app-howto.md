---
title: "如何使用 Redis 快取建立 Web 應用程式 | Microsoft Docs"
description: "了解如何使用 Redis 快取建立 Web 應用程式"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="e88d4-103">如何使用 Redis 快取建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="e88d4-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e88d4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e88d4-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="e88d4-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e88d4-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="e88d4-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="e88d4-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="e88d4-107">Java</span><span class="sxs-lookup"><span data-stu-id="e88d4-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="e88d4-108">Python</span><span class="sxs-lookup"><span data-stu-id="e88d4-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="e88d4-109">本教學課程示範如何使用 Visual Studio 2017，在 Azure App Service 的 Web 應用程式中建立和部署 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="e88d4-110">此範例應用程式會顯示資料庫中的隊伍統計資料清單，並示範各種使用 Azure Redis 快取在快取中儲存和擷取資料的方式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="e88d4-111">完成本教學課程時您將會擁有執行中的 Web 應用程式，其可對資料庫進行讀取和寫入、已使用 Azure Redis 快取進行最佳化，並裝載在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="e88d4-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="e88d4-112">您將了解：</span><span class="sxs-lookup"><span data-stu-id="e88d4-112">You'll learn:</span></span>

* <span data-ttu-id="e88d4-113">如何在 Visual Studio 中建立 ASP.NET MVC 5 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="e88d4-114">如何使用 Entity Framework 從資料庫存取資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="e88d4-115">如何透過使用 Azure Redis 快取來儲存和擷取資料，以改善資料輸送量並降低資料庫負載。</span><span class="sxs-lookup"><span data-stu-id="e88d4-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="e88d4-116">如何使用 Redis 的已排序集合來擷取前 5 名的隊伍。</span><span class="sxs-lookup"><span data-stu-id="e88d4-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="e88d4-117">如何使用 Resource Manager 範本為應用程式佈建 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="e88d4-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="e88d4-118">如何使用 Visual Studio 將應用程式發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e88d4-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e88d4-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="e88d4-119">Prerequisites</span></span>
<span data-ttu-id="e88d4-120">若要完成本教學課程，您必須具備下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="e88d4-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="e88d4-121">Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e88d4-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="e88d4-122">Visual Studio 2017 (含 Azure SDK for .NET)</span><span class="sxs-lookup"><span data-stu-id="e88d4-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="e88d4-123">Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e88d4-123">Azure account</span></span>
<span data-ttu-id="e88d4-124">您需要有 Azure 帳戶，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="e88d4-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="e88d4-125">您可以：</span><span class="sxs-lookup"><span data-stu-id="e88d4-125">You can:</span></span>

* <span data-ttu-id="e88d4-126">[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="e88d4-127">您將獲得能用來試用 Azure 付費服務的額度。</span><span class="sxs-lookup"><span data-stu-id="e88d4-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="e88d4-128">即使在額度用完後，您仍可保留帳戶並使用免費的 Azure 服務和功能。</span><span class="sxs-lookup"><span data-stu-id="e88d4-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="e88d4-129">[啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="e88d4-130">您的 MSDN 訂用帳戶每月會提供您額度，您可以用在 Azure 付費服務。</span><span class="sxs-lookup"><span data-stu-id="e88d4-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="e88d4-131">Visual Studio 2017 (含 Azure SDK for .NET)</span><span class="sxs-lookup"><span data-stu-id="e88d4-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="e88d4-132">本教學課程是特別為 Visual Studio 2017 (含 [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools)) 所撰寫。</span><span class="sxs-lookup"><span data-stu-id="e88d4-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="e88d4-133">Azure SDK 2.9.5 隨附於 Visual Studio 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="e88d4-134">如果您有 Visual Studio 2015，您可以遵循 [Azure SDK for.NET](../dotnet-sdk.md) 2.8.2 或更新版本的教學課程。</span><span class="sxs-lookup"><span data-stu-id="e88d4-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="e88d4-135">[在此下載最新的 Azure SDK for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="e88d4-136">如果您沒有 Visual Studio，它會自動與 SDK 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="e88d4-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="e88d4-137">有些畫面看起來可能與本教學課程所示插圖不同。</span><span class="sxs-lookup"><span data-stu-id="e88d4-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="e88d4-138">如果您有 Visual Studio 2013，您可以 [下載最新的 Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="e88d4-139">有些畫面看起來可能與本教學課程所示插圖不同。</span><span class="sxs-lookup"><span data-stu-id="e88d4-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e88d4-140">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="e88d4-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="e88d4-141">開啟 Visual Studio，然後按一下 [檔案][新增]、[專案]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="e88d4-142">展開 [範本] 清單中的 [Visual C#] 節點、選取 [雲端]，然後按一下 [ASP.NET Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="e88d4-143">確定已選取 [.NET Framework 4.5.2] 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e88d4-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="e88d4-144">在 [名稱] 文字方塊中輸入 **ContosoTeamStats**，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![建立專案][cache-create-project]
3. <span data-ttu-id="e88d4-146">選取 [MVC]  做為專案類型。</span><span class="sxs-lookup"><span data-stu-id="e88d4-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="e88d4-147">確保已針對 [驗證] 設定指定 [不需要驗證]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="e88d4-148">視您的 Visual Studio 版本而言，預設值可能會設定為其他項目。</span><span class="sxs-lookup"><span data-stu-id="e88d4-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="e88d4-149">若要加以變更，請按一下 [變更驗證]，然後選取 [不需要驗證]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="e88d4-150">如果您密切注意 Visual Studio 2015，請清除 [雲端中的主機] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e88d4-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="e88d4-151">在本教學課程的後續步驟中，您將會[佈建 Azure 資源](#provision-the-azure-resources)和[發佈應用程式至 Azure](#publish-the-application-to-azure)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="e88d4-152">如需在保持核取 [雲端中的主機]  的狀態下從 Visual Studio 佈建 App Service Web 應用程式的範例，請參閱 [使用 ASP.NET 和 Visual Studio 在 Azure App Service 中開始使用 Web Apps](../app-service-web/app-service-web-get-started-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![選取專案範本][cache-select-template]
4. <span data-ttu-id="e88d4-154">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="e88d4-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="e88d4-155">建立 ASP.NET MVC 應用程式</span><span class="sxs-lookup"><span data-stu-id="e88d4-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="e88d4-156">在本教學課程的這一節當中，您將會建立可從資料庫讀取並顯示隊伍統計資料的基本應用程式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="e88d4-157">新增 Entity Framework NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e88d4-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="e88d4-158">新增模型</span><span class="sxs-lookup"><span data-stu-id="e88d4-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="e88d4-159">新增控制器</span><span class="sxs-lookup"><span data-stu-id="e88d4-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="e88d4-160">設定檢視</span><span class="sxs-lookup"><span data-stu-id="e88d4-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="e88d4-161">新增 Entity Framework NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="e88d4-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="e88d4-162">按一下 [NuGet 套件管理員]、[工具] 功能表中的 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="e88d4-163">從 [Package Manager Console] 視窗中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="e88d4-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="e88d4-164">如需此套件的詳細資訊，請參閱 [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet 頁面。</span><span class="sxs-lookup"><span data-stu-id="e88d4-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="e88d4-165">新增模型</span><span class="sxs-lookup"><span data-stu-id="e88d4-165">Add the model</span></span>
1. <span data-ttu-id="e88d4-166">在 [方案總管] 中以滑鼠右鍵按一下 [模型]，並選擇 [新增][類別]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![新增模型][cache-model-add-class]
2. <span data-ttu-id="e88d4-168">針對類別名稱輸入 `Team`，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![新增模型類別][cache-model-add-class-dialog]
3. <span data-ttu-id="e88d4-170">將 `Team.cs` 檔案頂端的 `using` 陳述式替換為下列 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="e88d4-171">將 `Team` 類別的定義取代為包含已更新的 `Team` 類別定義以及一些其他 Entity Framework 協助程式類別的下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e88d4-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="e88d4-172">如需本教學課程中使用之 Entity Framework 的 Code First 方法的詳細資訊，請參閱 [Code First 至新的資料庫](https://msdn.microsoft.com/data/jj193542)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="e88d4-173">在 [方案總管] 中，連按兩下 [web.config] 來加以開啟。</span><span class="sxs-lookup"><span data-stu-id="e88d4-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="e88d4-175">新增下列 `connectionStrings` 區段。</span><span class="sxs-lookup"><span data-stu-id="e88d4-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="e88d4-176">連接字串的名稱必須符合 Entity Framework 資料庫內容類別的名稱，亦即 `TeamContext`。</span><span class="sxs-lookup"><span data-stu-id="e88d4-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="e88d4-177">您可以新增 `connectionStrings` 區段，以便它遵照如下列範例所示的 `configSections`。</span><span class="sxs-lookup"><span data-stu-id="e88d4-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > <span data-ttu-id="e88d4-178">連接字串可能會依用來完成本教學課程的 Visual Studio 和 SQL Server Express Edition 而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e88d4-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="e88d4-179">應該將 Web.config 範本設定為符合您的安裝，而且可能包含 `Data Source` 項目，例如 `(LocalDB)\v11.0`(從 SQL Server Express 2012) 或 `Data Source=(LocalDB)\MSSQLLocalDB` (從 SQL Server Express 2014 及更新版本)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="e88d4-180">如需有關連接字串和 SQL Express 版本的詳細資訊，請參閱 [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="e88d4-181">新增控制器</span><span class="sxs-lookup"><span data-stu-id="e88d4-181">Add the controller</span></span>
1. <span data-ttu-id="e88d4-182">按 **F6** 來建置專案。</span><span class="sxs-lookup"><span data-stu-id="e88d4-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="e88d4-183">在 [方案總管] 中，於 [控制器] 資料夾上按一下滑鼠右鍵，然後依序選擇 [新增] 和 [控制器]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![新增控制器][cache-add-controller]
3. <span data-ttu-id="e88d4-185">選擇 [使用 Entity Framework，包含檢視的 MVC 5 控制器]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="e88d4-186">如果您在按一下 [新增] 後收到錯誤，請確定您已先建置專案。</span><span class="sxs-lookup"><span data-stu-id="e88d4-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![新增控制器類別][cache-add-controller-class]
4. <span data-ttu-id="e88d4-188">在 [模型類別] 下拉式清單中選取 [Team (ContosoTeamStats.Models)]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="e88d4-189">在 [資料內容類別] 下拉式清單中選取 [TeamContext (ContosoTeamStats.Models)]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="e88d4-190">在 [控制器名稱] 文字方塊中輸入 `TeamsController` (如果尚未自動填入)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="e88d4-191">按一下 [新增]  以建立控制器類別並新增預設檢視。</span><span class="sxs-lookup"><span data-stu-id="e88d4-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![設定控制器][cache-configure-controller]
5. <span data-ttu-id="e88d4-193">在 [方案總管] 中展開 [Global.asax]，然後按兩下 [Global.asax.cs] 來加以開啟。</span><span class="sxs-lookup"><span data-stu-id="e88d4-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="e88d4-195">在檔案頂端的其他 `using` 陳述式底下新增下列兩個 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="e88d4-196">在 `Application_Start` 方法的結尾新增下列程式碼行。</span><span class="sxs-lookup"><span data-stu-id="e88d4-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="e88d4-197">在 [方案總管] 中展開 `App_Start`，然後按兩下 `RouteConfig.cs`。</span><span class="sxs-lookup"><span data-stu-id="e88d4-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="e88d4-199">在 `RegisterRoutes` 方法的下列程式碼中，將 `controller = "Home"` 取代為 `controller = "Teams"`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="e88d4-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="e88d4-200">設定檢視</span><span class="sxs-lookup"><span data-stu-id="e88d4-200">Configure the views</span></span>
1. <span data-ttu-id="e88d4-201">在 [方案總管] 中依序展開 [檢視] 資料夾和 [共用] 資料夾，然後按兩下 **_Layout.cshtml**。</span><span class="sxs-lookup"><span data-stu-id="e88d4-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="e88d4-203">變更 `title` 元素的內容，並將 `My ASP.NET Application` 取代為 `Contoso Team Stats`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="e88d4-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="e88d4-204">在 `body` 區段中，更新第一個 `Html.ActionLink` 陳述式，並將 `Application name` 取代為 `Contoso Team Stats` 以及將 `Home` 取代為 `Teams`。</span><span class="sxs-lookup"><span data-stu-id="e88d4-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="e88d4-205">取代前： `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="e88d4-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="e88d4-206">取代後： `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="e88d4-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![程式碼變更][cache-layout-cshtml-code]
2. <span data-ttu-id="e88d4-208">按 **Ctrl+F5** 以建置並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="e88d4-209">這個版本的應用程式會直接從資料庫讀取結果。</span><span class="sxs-lookup"><span data-stu-id="e88d4-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="e88d4-210">請注意透過 [使用 Entity Framework，包含檢視的 MVC 5 控制器] scaffold 自動新增至應用程式的 [建立新的]、[編輯]、[詳細資料] 和 [刪除] 動作。</span><span class="sxs-lookup"><span data-stu-id="e88d4-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="e88d4-211">在本教學課程的下一節裡，您將會新增 Redis 快取以將資料存取最佳化並為應用程式提供其他功能。</span><span class="sxs-lookup"><span data-stu-id="e88d4-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![起始應用程式][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="e88d4-213">設定應用程式以使用 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="e88d4-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="e88d4-214">在教學課程的這一節當中，您將會設定範例應用程式，讓其使用 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) 快取用戶端在 Azure Redis 快取執行個體中儲存和擷取 Contoso 的隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="e88d4-215">設定應用程式以使用 StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="e88d4-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="e88d4-216">更新 TeamsController 類別以從快取或資料庫中傳回結果</span><span class="sxs-lookup"><span data-stu-id="e88d4-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="e88d4-217">更新用來使用快取的建立、編輯和刪除方法</span><span class="sxs-lookup"><span data-stu-id="e88d4-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="e88d4-218">更新用來使用快取的隊伍索引檢視</span><span class="sxs-lookup"><span data-stu-id="e88d4-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="e88d4-219">設定應用程式以使用 StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="e88d4-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="e88d4-220">若要在 Visual Studio 中使用 StackExchange.Redis NuGet 套件來設定用戶端應用程式，請按一下 [工具] 功能表中的 [NuGet 套件管理員]、[套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="e88d4-221">從 `Package Manager Console` 視窗執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="e88d4-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="e88d4-222">NuGet 封裝會為您的用戶端應用程式下載並加入必要的組件參考，以利用 StackExchange.Redis 快取用戶端來存取 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="e88d4-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="e88d4-223">如果您偏好使用強式命名的 `StackExchange.Redis` 用戶端程式庫版本，請安裝 `StackExchange.Redis.StrongName` 套件。</span><span class="sxs-lookup"><span data-stu-id="e88d4-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="e88d4-224">在 [方案總管] 中展開 [控制器] 資料夾，然後按兩下 [TeamsController.cs] 來加以開啟。</span><span class="sxs-lookup"><span data-stu-id="e88d4-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![隊伍控制器][cache-teamscontroller]
4. <span data-ttu-id="e88d4-226">在 **TeamsController.cs** 中加入下列兩個 `using` 陳述式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="e88d4-227">將下列兩個屬性加入至 `TeamsController` 類別。</span><span class="sxs-lookup"><span data-stu-id="e88d4-227">Add the following two properties to the `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="e88d4-228">在您的電腦上建立名為 `WebAppPlusCacheAppSecrets.config` 的檔案，並將它放在範例應用程式的原始程式碼不會簽入的位置 (如果您決定在某處簽入檔案)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="e88d4-229">在此範例中，`AppSettingsSecrets.config` 檔案會放在 `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`。</span><span class="sxs-lookup"><span data-stu-id="e88d4-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="e88d4-230">編輯 `WebAppPlusCacheAppSecrets.config` 檔案，並加入下列內容。</span><span class="sxs-lookup"><span data-stu-id="e88d4-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="e88d4-231">如果您是在本機執行此應用程式，這項資訊將會用來連線到您的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="e88d4-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="e88d4-232">在本教學課程稍後，您將會佈建 Azure Redis 快取執行個體，並更新快取名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e88d4-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="e88d4-233">如果您不打算在本機執行範例應用程式，由於當您部署至 Azure 時，此應用程式會從 Web 應用程式的應用程式設定擷取快取連接資訊，而不是從這個檔案擷取，因此您可以將建立此檔案的步驟和參照此檔案的後續步驟略過。</span><span class="sxs-lookup"><span data-stu-id="e88d4-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="e88d4-234">由於 `WebAppPlusCacheAppSecrets.config` 不會隨著您的應用程式部署至 Azure，因此除非您要在本機執行此應用程式，否則您不需要它。</span><span class="sxs-lookup"><span data-stu-id="e88d4-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="e88d4-235">在 [方案總管] 中，連按兩下 [web.config] 來加以開啟。</span><span class="sxs-lookup"><span data-stu-id="e88d4-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="e88d4-237">將下列 `file` 屬性新增至 `appSettings` 元素。</span><span class="sxs-lookup"><span data-stu-id="e88d4-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="e88d4-238">如果您使用不同檔案名稱或位置，請以這些值取代範例中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="e88d4-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="e88d4-239">取代前： `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="e88d4-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="e88d4-240">取代後： ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="e88d4-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="e88d4-241">ASP.NET 執行階段會將外部檔案的內容與 `<appSettings>` 元素的標記合併。</span><span class="sxs-lookup"><span data-stu-id="e88d4-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="e88d4-242">如果找不到指定的檔案，則執行階段會略過檔案屬性。</span><span class="sxs-lookup"><span data-stu-id="e88d4-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="e88d4-243">您的密碼 (您的快取的連接字串) 不會包含在應用程式的原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="e88d4-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="e88d4-244">當您將 Web 應用程式部署至 Azure，將不會部署 `WebAppPlusCacheAppSecrests.config` 檔案 (這正是您要的結果)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="e88d4-245">有許多方式可在 Azure 中指定這些密碼，在本教學課程中，當您在後續的教學課程步驟中 [佈建 Azure 資源](#provision-the-azure-resources) 時，系統會自動為您設定這些密碼。</span><span class="sxs-lookup"><span data-stu-id="e88d4-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="e88d4-246">如需在 Azure 中使用密碼的詳細資訊，請參閱 [將密碼和其他機密資料部署到 ASP.NET 和 Azure App Service 的最佳作法](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="e88d4-247">更新 TeamsController 類別以從快取或資料庫中傳回結果</span><span class="sxs-lookup"><span data-stu-id="e88d4-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="e88d4-248">在此範例中，隊伍統計資料可以擷取自資料庫或快取。</span><span class="sxs-lookup"><span data-stu-id="e88d4-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="e88d4-249">隊伍統計資料可儲存在快取中做為序列化的 `List<Team>`，也可以使用 Redis 資料類型做為已排序集合。</span><span class="sxs-lookup"><span data-stu-id="e88d4-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="e88d4-250">從已排序集合擷取項目時，您可以擷取部分或所有項目，或是查詢特定項目。</span><span class="sxs-lookup"><span data-stu-id="e88d4-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="e88d4-251">在此範例中，您將查詢已排序集合內獲勝次數排在前 5 名的隊伍。</span><span class="sxs-lookup"><span data-stu-id="e88d4-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="e88d4-252">想要使用 Azure Redis 快取並不需要將隊伍統計資料以多種格式儲存在快取中。</span><span class="sxs-lookup"><span data-stu-id="e88d4-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="e88d4-253">本教學課程之所以使用多種格式，是為了示範某些可用來快取資料的不同方式和不同資料類型。</span><span class="sxs-lookup"><span data-stu-id="e88d4-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="e88d4-254">在 `TeamsController.cs` 檔案頂端新增下列 `using` 陳述式，和其他 `using` 陳述式放在一起。</span><span class="sxs-lookup"><span data-stu-id="e88d4-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="e88d4-255">將目前的 `public ActionResult Index()` 方法實作替換為下列實作。</span><span class="sxs-lookup"><span data-stu-id="e88d4-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="e88d4-256">在 `TeamsController` 類別中新增下列三種方法，實作來自先前程式碼片段中新增之 switch 陳述式中的 `playGames`、`clearCache` 和 `rebuildDB` 動作類型。</span><span class="sxs-lookup"><span data-stu-id="e88d4-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="e88d4-257">`PlayGames` 方法會藉由模擬一個賽季的遊戲來更新隊伍統計資料、將結果儲存至資料庫，並清除快取中現已過時的資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="e88d4-258">`RebuildDB` 方法會以一組預設的隊伍重新初始化資料庫、為這些隊伍產生統計資料，並清除快取中現已過時的資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="e88d4-259">`ClearCachedTeams` 方法會移除快取中任何已快取過的隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="e88d4-260">在 `TeamsController` 類別中加入下列四種方法來實作各種從快取和資料庫中擷取隊伍統計資料的方式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="e88d4-261">這四種方法皆會傳回 `List<Team>` 以在檢視中顯示。</span><span class="sxs-lookup"><span data-stu-id="e88d4-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="e88d4-262">`GetFromDB` 方法會從資料庫讀取隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="e88d4-263">`GetFromList` 方法會從快取中讀取序列化 `List<Team>` 形式的隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="e88d4-264">如果發生快取遺漏情形，便會從資料庫讀取隊伍統計資料，然後儲存在快取中以供下次使用。</span><span class="sxs-lookup"><span data-stu-id="e88d4-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="e88d4-265">在此範例中，我們會使用 JSON.NET 序列化在快取中傳入和傳出序列化的 .NET 物件。</span><span class="sxs-lookup"><span data-stu-id="e88d4-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="e88d4-266">如需詳細資訊，請參閱 [如何在 Azure Redis 快取中使用 .NET 物件](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="e88d4-267">`GetFromSortedSet` 方法會從快取的已排序集合讀取隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="e88d4-268">如果發生快取遺漏情形，便會從資料庫讀取隊伍統計資料，然後儲存在快取中做為已排序集合。</span><span class="sxs-lookup"><span data-stu-id="e88d4-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="e88d4-269">`GetFromSortedSetTop5` 方法會從快取的已排序集合讀取前 5 名的隊伍。</span><span class="sxs-lookup"><span data-stu-id="e88d4-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="e88d4-270">它會先檢查快取中是否有 `teamsSortedSet` 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="e88d4-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="e88d4-271">如果這個索引鍵不存在，便會呼叫 `GetFromSortedSet` 方法來讀取隊伍統計資料，並將資料儲存在快取中。</span><span class="sxs-lookup"><span data-stu-id="e88d4-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="e88d4-272">接著便會查詢快取的已排序集合中傳回的前 5 名隊伍。</span><span class="sxs-lookup"><span data-stu-id="e88d4-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="e88d4-273">更新用來使用快取的建立、編輯和刪除方法</span><span class="sxs-lookup"><span data-stu-id="e88d4-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="e88d4-274">此範例進行過程所產生的樣板程式碼包括用來新增、編輯和刪除隊伍的方法。</span><span class="sxs-lookup"><span data-stu-id="e88d4-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="e88d4-275">每當您加入、編輯或移除隊伍時，快取中的資料就會變得過時。</span><span class="sxs-lookup"><span data-stu-id="e88d4-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="e88d4-276">在本節中，您將會修改這三種方法來清除已快取的隊伍，讓快取不會與資料庫失去同步。</span><span class="sxs-lookup"><span data-stu-id="e88d4-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="e88d4-277">瀏覽至 `TeamsController` 類別中的 `Create(Team team)` 方法。</span><span class="sxs-lookup"><span data-stu-id="e88d4-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="e88d4-278">在 `ClearCachedTeams` 方法中新增呼叫，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="e88d4-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="e88d4-279">瀏覽至 `TeamsController` 類別中的 `Edit(Team team)` 方法。</span><span class="sxs-lookup"><span data-stu-id="e88d4-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="e88d4-280">在 `ClearCachedTeams` 方法中新增呼叫，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="e88d4-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="e88d4-281">瀏覽至 `TeamsController` 類別中的 `DeleteConfirmed(int id)` 方法。</span><span class="sxs-lookup"><span data-stu-id="e88d4-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="e88d4-282">在 `ClearCachedTeams` 方法中新增呼叫，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="e88d4-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="e88d4-283">更新用來使用快取的隊伍索引檢視</span><span class="sxs-lookup"><span data-stu-id="e88d4-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="e88d4-284">在 [方案總管] 中依序展開 [檢視] 資料夾和 [隊伍] 資料夾，然後按兩下 [Index.cshtml]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="e88d4-286">在檔案頂端附近尋找下列段落元素。</span><span class="sxs-lookup"><span data-stu-id="e88d4-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![動作資料表][cache-teams-index-table]
   
    <span data-ttu-id="e88d4-288">這是用來建立新隊伍的連結。</span><span class="sxs-lookup"><span data-stu-id="e88d4-288">This is the link to create a new team.</span></span> <span data-ttu-id="e88d4-289">請將此段落元素取代為下列資料表。</span><span class="sxs-lookup"><span data-stu-id="e88d4-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="e88d4-290">這個資料表內有動作連結，可供建立新的隊伍、進行新一賽季的遊戲、清除快取、從快取中以數種格式擷取隊伍、從資料庫中擷取隊伍，以及使用全新的範例資料重建資料庫。</span><span class="sxs-lookup"><span data-stu-id="e88d4-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="e88d4-291">捲動至 **Index.cshtml** 檔案底部並新增下列 `tr` 元素，使其成為檔案中最後一個資料表內的最後一個資料列。</span><span class="sxs-lookup"><span data-stu-id="e88d4-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="e88d4-292">這個資料列會顯示 `ViewBag.Msg` 的值，其包含目前作業的相關狀態報告。</span><span class="sxs-lookup"><span data-stu-id="e88d4-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="e88d4-293">當您按一下上一個步驟中的任何一個動作連結時，便會設定 `ViewBag.Msg`。</span><span class="sxs-lookup"><span data-stu-id="e88d4-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![狀態訊息][cache-status-message]
2. <span data-ttu-id="e88d4-295">按 **F6** 來建置專案。</span><span class="sxs-lookup"><span data-stu-id="e88d4-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="e88d4-296">佈建 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="e88d4-296">Provision the Azure resources</span></span>
<span data-ttu-id="e88d4-297">若要在 Azure 中裝載您的應用程式，您必須先佈建應用程式所需的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e88d4-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="e88d4-298">本教學課程中的範例應用程式會使用下列 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e88d4-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="e88d4-299">Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="e88d4-299">Azure Redis Cache</span></span>
* <span data-ttu-id="e88d4-300">App Service Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="e88d4-300">App Service Web App</span></span>
* <span data-ttu-id="e88d4-301">SQL Database</span><span class="sxs-lookup"><span data-stu-id="e88d4-301">SQL Database</span></span>

<span data-ttu-id="e88d4-302">若要在您選擇的新的或現有的資源群組部署這些服務，請按一下下面的 [部署至 Azure]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="e88d4-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="e88d4-303">[![部署至 Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e88d4-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="e88d4-304">這個 [部署至 Azure] 按鈕使用[建立 Web 應用程式、Redis 快取和 SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure 快速入門](https://github.com/Azure/azure-quickstart-templates)範本來佈建這些服務，並設定 SQL Database 的連接字串和 Azure Redis 快取連接字串的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="e88d4-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="e88d4-305">如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以 [建立免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) 。</span><span class="sxs-lookup"><span data-stu-id="e88d4-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="e88d4-306">按一下 [部署至 Azure]  按鈕會帶您前往 Azure 入口網站，並起始範本所述資源的建立程序。</span><span class="sxs-lookup"><span data-stu-id="e88d4-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![部署至 Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="e88d4-308">在 [基本] 區段中，選取要使用的 Azure 訂用帳戶，然後選取現有資源群組或建立新的資源群組，並指定資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="e88d4-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="e88d4-309">在 [設定] 區段中，指定 [系統管理員登入] \(請勿使用 **admin**)、[系統管理員登入密碼] 和 [資料庫名稱]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="e88d4-310">其他參數則針對免費的 App Service 主控方案進行設定，至於 SQL Database 和 Azure Redis 快取請設定較低成本選項，因為免費層不提供這兩種服務。</span><span class="sxs-lookup"><span data-stu-id="e88d4-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![部署至 Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="e88d4-312">設定所需的設定之後，捲動至頁面結尾，閱讀條款和條件，然後勾選 [我同意上方所述的條款及條件] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e88d4-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="e88d4-313">若要開始佈建資源，請按一下 [購買]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="e88d4-314">若要檢視部署進度，請按一下 [通知] 圖示，然後按一下 [部署已開始] 。</span><span class="sxs-lookup"><span data-stu-id="e88d4-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![部署已開始][cache-deployment-started]

<span data-ttu-id="e88d4-316">您可以在 [Microsoft.Template]  刀鋒視窗上檢視您的部署狀態。</span><span class="sxs-lookup"><span data-stu-id="e88d4-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![部署至 Azure][cache-deploy-to-azure-step-3]

<span data-ttu-id="e88d4-318">佈建完成後，您就可以從 Visual Studio 將應用程式發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e88d4-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="e88d4-319">佈建程序期間可能發生的任何錯誤皆會顯示在 [Microsoft.Template]**Microsoft.Template** 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="e88d4-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="e88d4-320">常見錯誤包括 SQL Server 太多或每個訂用帳戶的免費 App Service 主控方案太多。</span><span class="sxs-lookup"><span data-stu-id="e88d4-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="e88d4-321">請解決所有錯誤，然後按一下 [Microsoft.Template] 刀鋒視窗上的 [重新部署] 或本教學課程中的 [部署至 Azure] 按鈕重新啟動程序。</span><span class="sxs-lookup"><span data-stu-id="e88d4-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="e88d4-322">將應用程式發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="e88d4-322">Publish the application to Azure</span></span>
<span data-ttu-id="e88d4-323">在教學課程的這個步驟中，您會將應用程式發佈至 Azure 並在雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="e88d4-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="e88d4-324">在 Visual Studio 中以滑鼠右鍵按一下 [ContosoTeamStats] 專案，然後選擇 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![發佈][cache-publish-app]
2. <span data-ttu-id="e88d4-326">按一下 [Microsoft Azure App Service]，選擇 [選取現有的]，然後按一下 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![發佈][cache-publish-to-app-service]
3. <span data-ttu-id="e88d4-328">選取建立 Azure 資源時所使用的訂用帳戶、展開包含資源的資源群組，然後選取所需的 Web App。</span><span class="sxs-lookup"><span data-stu-id="e88d4-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="e88d4-329">如果您之前是使用 [部署至 Azure] 按鈕，您的 Web 應用程式名稱將會以 **webSite** 開頭，後面再接著一些額外字元。</span><span class="sxs-lookup"><span data-stu-id="e88d4-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![選取 Web 應用程式][cache-select-web-app]
4. <span data-ttu-id="e88d4-331">按一下 [確定]  即可開始發佈程序。</span><span class="sxs-lookup"><span data-stu-id="e88d4-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="e88d4-332">片刻過後，發佈程序會完成，而且會啟動具有執行中範例應用程式的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="e88d4-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="e88d4-333">如果您在驗證或發佈時收到 DNS 錯誤，而且應用程式的 Azure 資源佈建程序才剛完成不久，請稍候片刻，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="e88d4-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![已新增快取][cache-added-to-application]

<span data-ttu-id="e88d4-335">下表描述範例應用程式中的每個動作連結。</span><span class="sxs-lookup"><span data-stu-id="e88d4-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="e88d4-336">動作</span><span class="sxs-lookup"><span data-stu-id="e88d4-336">Action</span></span> | <span data-ttu-id="e88d4-337">說明</span><span class="sxs-lookup"><span data-stu-id="e88d4-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e88d4-338">建立新的</span><span class="sxs-lookup"><span data-stu-id="e88d4-338">Create New</span></span> |<span data-ttu-id="e88d4-339">建立新的隊伍。</span><span class="sxs-lookup"><span data-stu-id="e88d4-339">Create a new Team.</span></span> |
| <span data-ttu-id="e88d4-340">遊戲賽季</span><span class="sxs-lookup"><span data-stu-id="e88d4-340">Play Season</span></span> |<span data-ttu-id="e88d4-341">玩一個賽季的遊戲、更新隊伍統計資料，並清除快取中任何已過時的隊伍資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="e88d4-342">清除快取</span><span class="sxs-lookup"><span data-stu-id="e88d4-342">Clear Cache</span></span> |<span data-ttu-id="e88d4-343">清除快取中的隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="e88d4-344">快取中的清單</span><span class="sxs-lookup"><span data-stu-id="e88d4-344">List from Cache</span></span> |<span data-ttu-id="e88d4-345">擷取快取中的隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="e88d4-346">如果發生快取遺漏情形，則載入資料庫中的統計資料，並儲存至快取中以供下次使用。</span><span class="sxs-lookup"><span data-stu-id="e88d4-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="e88d4-347">快取中的已排序集合</span><span class="sxs-lookup"><span data-stu-id="e88d4-347">Sorted Set from Cache</span></span> |<span data-ttu-id="e88d4-348">使用已排序集合擷取快取中的隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="e88d4-349">如果發生快取遺漏的情形，請從資料庫中載入統計資料，並使用已排序集合儲存至快取中。</span><span class="sxs-lookup"><span data-stu-id="e88d4-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="e88d4-350">快取中的前 5 名隊伍</span><span class="sxs-lookup"><span data-stu-id="e88d4-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="e88d4-351">使用已排序集合擷取快取中的前 5 名隊伍。</span><span class="sxs-lookup"><span data-stu-id="e88d4-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="e88d4-352">如果發生快取遺漏的情形，請從資料庫中載入統計資料，並使用已排序集合儲存至快取中。</span><span class="sxs-lookup"><span data-stu-id="e88d4-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="e88d4-353">從資料庫載入</span><span class="sxs-lookup"><span data-stu-id="e88d4-353">Load from DB</span></span> |<span data-ttu-id="e88d4-354">擷取資料庫中的隊伍統計資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="e88d4-355">重建資料庫</span><span class="sxs-lookup"><span data-stu-id="e88d4-355">Rebuild DB</span></span> |<span data-ttu-id="e88d4-356">重建資料庫並在其中重新載入範例隊伍資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="e88d4-357">編輯/詳細資料/刪除</span><span class="sxs-lookup"><span data-stu-id="e88d4-357">Edit / Details / Delete</span></span> |<span data-ttu-id="e88d4-358">編輯隊伍、檢視隊伍的詳細資料、刪除隊伍。</span><span class="sxs-lookup"><span data-stu-id="e88d4-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="e88d4-359">對某些動作按一下，然後試驗從不同來源擷取資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="e88d4-360">請注意從資料庫和快取擷取資料的各種方式若要完成所需花費之時間的差異。</span><span class="sxs-lookup"><span data-stu-id="e88d4-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="e88d4-361">在完成應用程式時刪除資源</span><span class="sxs-lookup"><span data-stu-id="e88d4-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="e88d4-362">當您完成教學課程的範例應用程式時，您可以刪除使用的 Azure 資源以節省成本和資源。</span><span class="sxs-lookup"><span data-stu-id="e88d4-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="e88d4-363">如果您在[佈建 Azure 資源](#provision-the-azure-resources)一節使用 [部署至 Azure] 按鈕，而且您的所有資源都包含在相同的資源群組內，您可以透過刪除資源群組在單一作業中將它們一起刪除。</span><span class="sxs-lookup"><span data-stu-id="e88d4-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="e88d4-364">登入 [Azure 入口網站](https://portal.azure.com)，然後按一下 [資源群組]。</span><span class="sxs-lookup"><span data-stu-id="e88d4-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="e88d4-365">在 [篩選項目...]  文字方塊中輸入您的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="e88d4-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="e88d4-366">按一下資源群組右邊的 [...]  。</span><span class="sxs-lookup"><span data-stu-id="e88d4-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="e88d4-367">按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="e88d4-367">Click **Delete**.</span></span>
   
    ![刪除][cache-delete-resource-group]
5. <span data-ttu-id="e88d4-369">輸入您的資源群組名稱，然後按一下 [刪除] 。</span><span class="sxs-lookup"><span data-stu-id="e88d4-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![Confirm delete][cache-delete-confirm]

<span data-ttu-id="e88d4-371">片刻過後，便會刪除資源群組及其所有內含的資源。</span><span class="sxs-lookup"><span data-stu-id="e88d4-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e88d4-372">請注意，刪除資源群組是無法回復的動作，資源群組和其內的所有資源將會永久刪除。</span><span class="sxs-lookup"><span data-stu-id="e88d4-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="e88d4-373">請確定您不會不小心刪除錯誤的資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="e88d4-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="e88d4-374">如果您是在現有資源群組內建立用來裝載此範例的資源，您可以從每個資源各自的刀鋒視窗中個別刪除每個資源。</span><span class="sxs-lookup"><span data-stu-id="e88d4-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="e88d4-375">在您的本機電腦上執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="e88d4-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="e88d4-376">若要在本機電腦上執行應用程式，您需要 Azure Redis 快取執行個體以供快取資料。</span><span class="sxs-lookup"><span data-stu-id="e88d4-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="e88d4-377">如果您已如上一節所述將應用程式發佈到 Azure，您可以使用該步驟期間佈建的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="e88d4-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="e88d4-378">如果您有其他現有的 Azure Redis 快取執行個體，您可以用它在本機執行此範例。</span><span class="sxs-lookup"><span data-stu-id="e88d4-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="e88d4-379">如果您需要建立 Azure Redis 快取執行個體，您可以依照 [建立快取](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)中的步驟來進行。</span><span class="sxs-lookup"><span data-stu-id="e88d4-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="e88d4-380">一旦您選取或建立了要使用的快取，請瀏覽至 Azure 入口網站中的快取，並擷取快取的[主機名稱](cache-configure.md#properties)和[存取金鑰](cache-configure.md#access-keys)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="e88d4-381">如需相關指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="e88d4-382">使用您選擇的編輯器開啟本教學課程的[設定應用程式以使用 Redis 快取](#configure-the-application-to-use-redis-cache)步驟期間建立的 `WebAppPlusCacheAppSecrets.config` 檔案。</span><span class="sxs-lookup"><span data-stu-id="e88d4-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="e88d4-383">編輯 `value` 屬性，並將 `MyCache.redis.cache.windows.net` 取代為快取的[主機名稱](cache-configure.md#properties)，然後將快取的[主要或次要金鑰](cache-configure.md#access-keys)指定為密碼。</span><span class="sxs-lookup"><span data-stu-id="e88d4-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="e88d4-384">按 **CTRL+F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="e88d4-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="e88d4-385">請注意，因為包含資料庫的應用程式是在本機執行，且 Redis 快取是裝載在 Azure，因此快取可能會讓資料庫的效能變差。</span><span class="sxs-lookup"><span data-stu-id="e88d4-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="e88d4-386">為了獲得最佳效能，用戶端應用程式和 Azure Redis 快取執行個體應該位於相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e88d4-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e88d4-387">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e88d4-387">Next steps</span></span>
* <span data-ttu-id="e88d4-388">深入了解 [ASP.NET](http://asp.net/) 網站上的[開始使用 ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="e88d4-389">如需在 App Service 中建立 ASP.NET Web 應用程式的範例，請參閱 [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [示範](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/)中的[在 Azure App Service 中建立和部署 ASP.NET Web 應用程式](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="e88d4-390">如需來自 HealthClinic.biz 示範的更多快速入門，請參閱 [Azure 開發人員工具快速入門](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="e88d4-391">深入了解本教學課程中使用之 Entity Framework 的 [Code First 至新的資料庫](https://msdn.microsoft.com/data/jj193542) 方法。</span><span class="sxs-lookup"><span data-stu-id="e88d4-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="e88d4-392">深入了解 [Azure App Service 中的 Web 應用程式](../app-service-web/app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e88d4-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="e88d4-393">了解如何在 Azure 入口網站中 [監視](cache-how-to-monitor.md) 您的快取。</span><span class="sxs-lookup"><span data-stu-id="e88d4-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="e88d4-394">瀏覽 Azure Redis 快取進階功能</span><span class="sxs-lookup"><span data-stu-id="e88d4-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="e88d4-395">如何設定高階 Azure Redis Cache 的永續性</span><span class="sxs-lookup"><span data-stu-id="e88d4-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="e88d4-396">如何設定高階 Azure Redis Cache 的叢集</span><span class="sxs-lookup"><span data-stu-id="e88d4-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="e88d4-397">如何設定高階 Azure Redis Cache 的虛擬網路支援</span><span class="sxs-lookup"><span data-stu-id="e88d4-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="e88d4-398">如需高階快取的大小、輸送量和頻寬等方面的詳細資訊，請參閱 [Azure Redis Cache 常見問題集](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) 。</span><span class="sxs-lookup"><span data-stu-id="e88d4-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

