---
title: "aaaHow toocreate Web 應用程式使用 Redis 快取 |Microsoft 文件"
description: "深入了解如何 toocreate Web 應用程式使用 Redis 快取"
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
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>如何 toocreate Web 應用程式使用 Redis 快取
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

本教學課程示範如何 toocreate 及部署 ASP.NET web 應用程式 tooa web 應用程式中使用 Visual Studio 2017 Azure 應用程式服務。 hello 範例應用程式會顯示資料庫中的小組統計資料的清單會顯示不同的方式 toouse Azure Redis 快取 toostore 和 hello 快取中擷取資料。 當您完成 hello 教學課程，您將有讀取和寫入 tooa 資料庫，使用 Azure Redis 快取，最佳化，而裝載在 Azure 中執行 web 應用程式。

您將了解：

* 如何 toocreate ASP.NET MVC 5 web 應用程式，Visual Studio 中。
* 如何使用 Entity Framework 從資料庫 tooaccess 資料。
* 如何 tooimprove 資料輸送量並降低資料庫負載的儲存和使用 Azure Redis 快取擷取資料。
* Toouse Redis 排序組 tooretrieve hello 前 5 個小組的方式。
* 如何 tooprovision hello hello 使用資源管理員範本的應用程式的 Azure 資源。
* 如何 toopublish hello 使用 Visual Studio 的應用程式 tooAzure。

## <a name="prerequisites"></a>必要條件
toocomplete hello 教學課程中，您必須擁有下列必要條件 hello。

* [Azure 帳戶](#azure-account)
* [Visual Studio 2017 以 hello Azure SDK for.NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Azure 帳戶
您需要 Azure 帳戶 toocomplete hello 教學課程。 您可以：

* [免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero)。 就可以使用的 tootry 出支付 Azure 服務的信用額度。 即使 hello 信用額度用完之後，您可以讓 hello 帳戶，並使用免費的 Azure 服務和功能。
* [啟用 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero)。 您的 MSDN 訂用帳戶每月會提供您額度，您可以用在 Azure 付費服務。

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio 2017 以 hello Azure SDK for.NET
Visual Studio 2017 撰寫 hello 教學課程以 hello [Azure SDK for.NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools)。 hello Azure SDK 2.9.5 隨附於 hello Visual Studio 安裝程式。

如果您有 Visual Studio 2015，您可以遵循以 hello hello 教學課程[Azure SDK for.NET](../dotnet-sdk.md) 2.8.2 或更新版本。 [下載 hello 最新的 Azure SDK for Visual Studio 2015 這裡](http://go.microsoft.com/fwlink/?linkid=518003)。 如果您沒有 visual Studio 會自動安裝以 hello SDK。 某些畫面看起來可能與本教學課程中所示的 hello 描述的不同。

如果您有 Visual Studio 2013，您可以[下載 hello 最新的 Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322)。 某些畫面看起來可能與本教學課程中所示的 hello 描述的不同。

## <a name="create-hello-visual-studio-project"></a>建立 hello Visual Studio 專案
1. 開啟 Visual Studio，然後按一下檔案新增、專案。
2. 展開 hello **Visual C#**節點 hello**範本**清單中，選取**雲端**，然後按一下**ASP.NET Web 應用程式**。 確定已選取 [.NET Framework 4.5.2] 或更新版本。  型別**ContosoTeamStats**到 hello**名稱**文字方塊中，按一下 **確定**。
   
    ![建立專案][cache-create-project]
3. 選取**MVC** hello 專案類型。 

    請確認**非驗證**指定 hello**驗證**設定。 根據您的 Visual Studio 版本，hello 預設可能會設定其他 toosomething。 toochange，按一下 **變更驗證**選取**非驗證**。

    如果您要遵照以及 Visual Studio 2015 中，清除 hello **hello 雲端中的主機**核取方塊。 您將[佈建 hello Azure 資源](#provision-the-azure-resources)和[發行 hello 應用程式 tooAzure](#publish-the-application-to-azure) hello 教學課程中的後續步驟中。 如需範例，藉由保留佈建的 App Service web 應用程式從 Visual Studio 的**hello 雲端中的主機**核取，請參閱[開始使用 Azure App Service，使用 ASP.NET 和 Visual Studio 中的 Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md)。
   
    ![選取專案範本][cache-select-template]
4. 按一下**確定**toocreate hello 專案。

## <a name="create-hello-aspnet-mvc-application"></a>建立 hello ASP.NET MVC 應用程式
在本節中的 hello 教學課程，您將建立 hello 基本應用程式讀取並顯示 team 從資料庫的統計資料。

* [新增 hello Entity Framework NuGet 封裝](#add-the-entity-framework-nuget-package)
* [新增 hello 模型](#add-the-model)
* [新增 hello 控制站](#add-the-controller)
* [設定 hello 檢視](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>新增 hello Entity Framework NuGet 封裝

1. 按一下**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表。
2. 執行 hello 下列命令從 hello **Package Manager Console**視窗。
    
    ```
    Install-Package EntityFramework
    ```

如需有關此套件的詳細資訊，請參閱 hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet 頁面。

### <a name="add-hello-model"></a>新增 hello 模型
1. 在 [方案總管] 中以滑鼠右鍵按一下 [模型]，並選擇 [新增][類別]。 
   
    ![新增模型][cache-model-add-class]
2. 輸入`Team`hello 類別名稱，然後按一下**新增**。
   
    ![新增模型類別][cache-model-add-class-dialog]
3. 取代 hello`using`在 hello hello 最上方的陳述式`Team.cs`hello 下列檔案`using`陳述式。

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. 取代 hello hello 定義`Team`類別以下列程式碼片段，其中包含更新的 hello`Team`類別定義，以及一些其他的 Entity Framework helper 類別。 Hello 程式碼第一種方法 tooEntity 本教學課程中所使用的架構上的詳細資訊，請參閱[程式碼第一個 tooa 新資料庫](https://msdn.microsoft.com/data/jj193542)。

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


1. 在**方案總管 中**，連按兩下**web.config** tooopen 它。
   
    ![Web.config][cache-web-config]
2. 新增下列 hello `connectionStrings` > 一節。 hello 連接字串 hello 名稱必須符合 hello hello Entity Framework 資料庫內容類別，即名稱`TeamContext`。

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    您可以加入新的 hello`connectionStrings`區段，如此它會依照`configSections`hello 下列範例所示。

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
    > 您的連接字串可能會根據 hello 的 Visual Studio 版本而不同，而且 toocomplete hello 教學課程所使用 SQL Server Express 版本。 hello web.config 範本應該設定的 toomatch 您的安裝，而且可能包含`Data Source`喜歡的項目`(LocalDB)\v11.0`（從 SQL Server Express 2012) 或`Data Source=(LocalDB)\MSSQLLocalDB`（從 SQL Server Express 2014 及更新版本）。 如需有關連接字串和 SQL Express 版本的詳細資訊，請參閱 [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)。

### <a name="add-hello-controller"></a>新增 hello 控制站
1. 按**F6** toobuild hello 專案。 
2. 在**方案總管] 中**，以滑鼠右鍵按一下 hello**控制器**資料夾，然後選擇 [**新增**，**控制器**。
   
    ![新增控制器][cache-add-controller]
3. 選擇 [使用 Entity Framework，包含檢視的 MVC 5 控制器]，然後按一下 [新增]。 如果您收到錯誤之後按一下**新增**，請確定您已先建置 hello 專案。
   
    ![新增控制器類別][cache-add-controller-class]
4. 選取**小組 (ContosoTeamStats.Models)**從 hello**模型類別**下拉式清單。 選取**TeamContext (ContosoTeamStats.Models)**從 hello**資料內容類別**下拉式清單。 型別`TeamsController`在 hello**控制器**名稱 文字方塊中 （如果它不會自動擴展）。 按一下**新增**toocreate hello 控制器類別，並加入 hello 預設檢視。
   
    ![設定控制器][cache-configure-controller]
5. 在**方案總管 中**，依序展開**Global.asax**按兩下**Global.asax.cs** tooopen 它。
   
    ![Global.asax.cs][cache-global-asax]
6. 新增下列兩個 hello`using`在 hello hello 其他 hello 檔案最上方的陳述式`using`陳述式。

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. 新增下列一行程式碼結尾 hello hello hello`Application_Start`方法。

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. 在 [方案總管] 中展開 `App_Start`，然後按兩下 `RouteConfig.cs`。
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. 取代`controller = "Home"`在下列程式碼中 hello hello`RegisterRoutes`方法`controller = "Teams"`hello 下列範例所示。

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>設定 hello 檢視
1. 在**方案總管] 中**，依序展開 [hello**檢視**資料夾，然後再 hello**共用**資料夾，然後按兩下**_Layout.cshtml**。 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. 變更 hello hello 內容`title`項目和取代`My ASP.NET Application`與`Contoso Team Stats`hello 下列範例所示。

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. 在 hello`body`區段中，先更新 hello`Html.ActionLink`陳述式，並取代`Application name`與`Contoso Team Stats`和取代`Home`與`Teams`。
   
   * 取代前： `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * 取代後： `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![程式碼變更][cache-layout-cshtml-code]
2. 按**Ctrl + F5** toobuild 和執行 hello 應用程式。 這個版本的 hello 應用程式直接從 hello 資料庫讀取 hello 結果。 請注意 hello**建立新**，**編輯**，**詳細資料**，和**刪除**動作會自動加入 hello toohello 應用程式**的 MVC 5 控制器與檢視，使用 Entity Framework** scaffold。 Hello hello 教學課程的下一節中，您將新增 Redis 快取 toooptimize hello 資料存取和 toohello 應用程式提供額外的功能。

![起始應用程式][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>設定 hello 應用程式 toouse Redis 快取
在本節中的 hello 教學課程，您會設定 hello 範例應用程式 toostore，並擷取從 Azure Redis 快取執行個體的 Contoso 小組統計資料，使用 hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis)快取用戶端。

* [設定 hello 應用程式 toouse StackExchange.Redis](#configure-the-application-to-use-stackexchangeredis)
* [更新從 hello 快取或 hello 資料庫 hello TeamsController 類別 tooreturn 結果](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [更新 hello 建立、 編輯和刪除方法 toowork hello 快取](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [更新 hello 小組索引檢視 toowork hello 快取](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>設定 hello 應用程式 toouse StackExchange.Redis
1. tooconfigure 用戶端應用程式，在 Visual Studio 中使用 hello StackExchange.Redis NuGet 封裝，按一下**NuGet 套件管理員**， **Package Manager Console**從 hello**工具**功能表。
2. 執行 hello 下列命令從 hello`Package Manager Console`視窗。
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    hello NuGet 封裝下載並新增 hello hello StackExchange.Redis 快取用戶端與您用戶端應用程式 tooaccess Azure Redis 快取所需的組件參考。 如果您偏好 toouse hello 的強式名稱版本`StackExchange.Redis`用戶端程式庫、 安裝 hello`StackExchange.Redis.StrongName`封裝。
3. 在**方案總管] 中**，依序展開 [hello**控制器**資料夾，然後按兩下**TeamsController.cs** tooopen 它。
   
    ![隊伍控制器][cache-teamscontroller]
4. 新增下列兩個 hello`using`陳述式太**TeamsController.cs**。

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. 新增下列兩個屬性 toohello hello`TeamsController`類別。

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

6. 建立名為您電腦上的檔案`WebAppPlusCacheAppSecrets.config`並將它放在不簽入 hello 您範例應用程式的原始程式碼，您應該決定 toocheck 的位置在某處。 在此範例 hello`AppSettingsSecrets.config`檔案是位於`C:\AppSecrets\WebAppPlusCacheAppSecrets.config`。
   
    編輯 hello`WebAppPlusCacheAppSecrets.config`檔案，然後加入下列內容的 hello。 如果您在本機執行 hello 應用程式這項資訊是使用的 tooconnect tooyour Azure Redis 快取執行個體。 稍後在 hello 教學課程將佈建 Azure Redis 快取執行個體，並更新 hello 快取名稱和密碼。 如果您不打算 toorun hello 範例應用程式在本機略過此檔案建立 hello 和 hello 參考 hello 檔案，因為當您部署 tooAzure hello 應用程式的後續步驟會擷取 hello 應用程式中的 hello 快取連接資訊設定 hello Web 應用程式，而不是從這個檔案。 因為 hello`WebAppPlusCacheAppSecrets.config`未部署 tooAzure 與您的應用程式，您不需要它除非您正在本機 toorun hello 應用程式。

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. 在**方案總管 中**，連按兩下**web.config** tooopen 它。
   
    ![Web.config][cache-web-config]
2. 新增下列 hello`file`屬性 toohello`appSettings`項目。 如果您使用不同的檔案名稱或位置，以取代 hello 範例所示的這些值。
   
   * 取代前： `<appSettings>`
   * 取代後： ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   hello ASP.NET 執行階段會合併具有在 hello hello 標記的 hello 外部檔案 hello 內容`<appSettings>`項目。 如果找不到 hello 指定的檔案，hello 執行階段就會忽略 hello 檔案屬性。 您的機密 （hello 連接字串 tooyour 快取） 不包含 hello hello 應用程式的原始碼的過程。 當您部署您的 web 應用程式 tooAzure 時，hello`WebAppPlusCacheAppSecrests.config`檔案不會部署 （亦即您想要）。 有數種方式 toospecify 這些密碼在 Azure 中，而且在本教學課程會設定自動為您當您[佈建 hello Azure 資源](#provision-the-azure-resources)後續的教學課程步驟中。 如需有關使用 Azure 中的機密資料的詳細資訊，請參閱[密碼和其他機密資料 tooASP.NET 和 Azure App Service 部署的最佳做法](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)。

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>更新從 hello 快取或 hello 資料庫 hello TeamsController 類別 tooreturn 結果
在此範例中，小組統計資料可以擷取從 hello 資料庫或從 hello 快取。 小組統計資料會儲存為序列化的 hello 快取中`List<Team>`，，也可以作為使用 Redis 資料類型的已排序資料集。 從已排序集合擷取項目時，您可以擷取部分或所有項目，或是查詢特定項目。 在此範例中，您將查詢 hello top 5 小組 wins 的數字排名的 hello 排序集合。

> [!NOTE]
> 不需要的 toostore 順序 toouse Azure Redis 快取中的 hello 快取中的多種格式 hello 小組統計資料。 本教學課程中使用多個格式 toodemonstrate 一些 hello 不同的方式以及不同的資料型別中，您可以使用 toocache 資料。
> 
> 

1. 新增下列 hello`using`陳述式 toohello`TeamsController.cs`檔案頂端以 hello 其他 hello`using`陳述式。

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. 取代 hello 目前`public ActionResult Index()`以 hello 下列實作方法實作。

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

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. 新增下列三個方法 toohello hello`TeamsController`類別 tooimplement hello `playGames`， `clearCache`，和`rebuildDB`動作類型從 hello switch 陳述式加入 hello 先前的程式碼片段中。
   
    hello`PlayGames`方法以更新 hello 小組統計資料模擬遊戲的旺季期間，儲存 hello 結果 toohello 資料庫，並清除 hello 現在過期 hello 快取的資料。

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

    hello`RebuildDB`方法重新初始化 hello 資料庫 hello 預設一群小組，以產生統計資料，並清除 hello 現在過期 hello 快取的資料。

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    hello`ClearCachedTeams`方法從 hello 快取中移除任何快取的小組統計資料。

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. 新增下列四個方法 toohello hello`TeamsController`類別 tooimplement hello 從 hello 快取和 hello 資料庫擷取 hello 小組統計資料的各種方式。 每一種方法會傳回`List<Team>`然後便會顯示 hello 檢視。
   
    hello`GetFromDB`方法會讀取 hello 資料庫中的 hello 小組統計資料。
   
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

    hello`GetFromList`方法會讀取序列化的快取中的 hello 小組統計資料`List<Team>`。 如果沒有快取遺漏，hello 小組統計資料會從 hello 資料庫讀取，並且會儲存供下一次 hello 快取。 在此範例中，我們會使用 JSON.NET 序列化 tooserialize hello.NET 物件 tooand 從 hello 快取。 如需詳細資訊，請參閱[toowork 搭配.NET 中 Azure Redis 快取的物件如何](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)。

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

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    hello`GetFromSortedSet`方法會從快取的已排序資料集讀取 hello 小組統計資料。 如果沒有快取遺漏，hello 小組統計資料從 hello 資料庫讀取，並且儲存在 hello 做為已排序資料集的快取。

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    hello`GetFromSortedSetTop5`方法會讀取 hello top 5 小組與快取的 hello 排序集合。 它會開始檢查是否有 hello hello hello 快取`teamsSortedSet`索引鍵。 如果此機碼不存在，hello`GetFromSortedSet`方法呼叫 tooread hello 小組統計資料，並將其儲存在 hello 快取中。 接下來，hello 快取的已排序資料的集查詢 hello 前 5 個小組都傳回。

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>更新 hello 建立、 編輯和刪除方法 toowork hello 快取
因為此範例的一部分包含了方法 tooadd 產生 hello scaffolding 程式碼編輯和刪除小組。 每當加入、 編輯或移除小組時，會變成過期 hello 快取中的 hello 資料。 本章節內容，您將修改下列三種方法 tooclear hello 快取小組讓 hello 快取將不會與 hello 資料庫同步處理。

1. 瀏覽 toohello`Create(Team team)`方法在 hello`TeamsController`類別。 加入呼叫 toohello`ClearCachedTeams`方法 hello 下列範例所示。

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. 瀏覽 toohello`Edit(Team team)`方法在 hello`TeamsController`類別。 加入呼叫 toohello`ClearCachedTeams`方法 hello 下列範例所示。

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. 瀏覽 toohello`DeleteConfirmed(int id)`方法在 hello`TeamsController`類別。 加入呼叫 toohello`ClearCachedTeams`方法 hello 下列範例所示。

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>更新 hello 小組索引檢視 toowork hello 快取
1. 在**方案總管] 中**，依序展開 [hello**檢視**資料夾，然後 hello**小組**資料夾，然後按兩下**Index.cshtml**。
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Hello hello 檔案頂端附近尋找 hello 下列段落項目。
   
    ![動作資料表][cache-teams-index-table]
   
    這是 hello 連結 toocreate 新小組。 取代為下表中的 hello hello 段落項目。 這個資料表有動作連結建立新的小組，並玩的遊戲，清除 hello 快取的新旺季期間，從數種格式的 hello 快取擷取 hello 小組、 從 hello 資料庫擷取 hello 小組和重建 hello 與全新的範例資料的資料庫。

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


1. 捲軸 toohello 底部 hello **Index.cshtml**檔案，然後加入下列 hello`tr`項目，以便 hello hello 最後一個資料列上次資料表 hello 檔案中。
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    此資料列會顯示 hello 值`ViewBag.Msg`其中包含有關 hello 目前作業狀態報告。 hello`ViewBag.Msg`設定當您按一下任一 hello hello 上一個步驟的動作連結。   
   
    ![狀態訊息][cache-status-message]
2. 按**F6** toobuild hello 專案。

## <a name="provision-hello-azure-resources"></a>佈建 hello Azure 資源
toohost 您在 Azure 中的應用程式，您必須先佈建 hello Azure 應用程式所需的服務。 在此教學課程中的 hello 範例應用程式會使用下列 Azure 服務的 hello。

* Azure Redis 快取
* App Service Web 應用程式
* SQL Database

toodeploy 這些服務 tooa 新的或現有的資源群組您的選擇，按一下下列的 hello**部署 tooAzure**  按鈕。

[![部署 tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

這**部署 tooAzure**按鈕使用 hello[建立 Web 應用程式加上 Redis 快取加上 SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure 快速入門](https://github.com/Azure/azure-quickstart-templates)範本 tooprovision 這些服務和設定 helloAzure Redis 快取的連接字串 hello 的 hello SQL Database 和 hello 應用程式設定的連接字串。

> [!NOTE]
> 如果您沒有 Azure 帳戶，只需要幾分鐘的時間就可以 [建立免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) 。
> 
> 

按一下 hello**部署 tooAzure**按鈕會採用 toohello Azure 入口網站，並啟始 hello 建立 hello 資源 hello 範本所描述的程序。

![部署 tooAzure][cache-deploy-to-azure-step-1]

1. 在 hello**基本概念**區段中選取 hello Azure 訂用帳戶 toouse，和選取現有的資源群組或建立新的連線，然後指定 hello 資源群組的位置。
2. 在 hello**設定**區段中，指定**系統管理員身分登入**(請勿使用**admin**)，**系統管理員身分登入密碼**，和**資料庫名稱**。 hello 其他參數會設定可用的應用程式裝載之服務的計劃，以及 hello SQL Database 和 Azure Redis 快取，不會隨附免費層的低成本選項。

    ![部署 tooAzure][cache-deploy-to-azure-step-2]

3. 設定所需的 hello，完成後，捲動 toohello 結尾 hello 頁面、 讀取的 hello 條款和條件，並檢查 hello **toohello 條款和條件前面所述，即表示我同意**核取方塊。
4. 按一下 佈建 hello 資源 toobegin，**購買**。

tooview hello 進度、 以部署的 hello 通知圖示，再利用**部署已開始**。

![部署已開始][cache-deployment-started]

您可以檢視您部署的 hello 狀態上 hello **Microsoft.Template**刀鋒視窗。

![部署 tooAzure][cache-deploy-to-azure-step-3]

佈建完成時，您可以發佈您的應用程式 tooAzure 從 Visual Studio。

> [!NOTE]
> Hello 佈建程序期間可能會發生任何錯誤都會顯示在 hello **Microsoft.Template**刀鋒視窗。 常見錯誤包括 SQL Server 太多或每個訂用帳戶的免費 App Service 主控方案太多。 解決任何錯誤，然後重新啟動 hello 程序，依序按一下**重新部署**上 hello **Microsoft.Template**刀鋒視窗或 hello**部署 tooAzure**本教學課程中的按鈕。
> 
> 

## <a name="publish-hello-application-tooazure"></a>發行 hello 應用程式 tooAzure
在此步驟 hello 教學課程中，您將發佈 hello 應用程式 tooAzure，且 hello 雲端中執行它。

1. 以滑鼠右鍵按一下 hello **ContosoTeamStats**專案在 Visual Studio 中，選擇**發行**。
   
    ![發佈][cache-publish-app]
2. 按一下 [Microsoft Azure App Service]，選擇 [選取現有的]，然後按一下 [發佈]。
   
    ![發佈][cache-publish-to-app-service]
3. 選取 hello Azure 資源，建立 hello hello 資源群組展開包含 hello 資源，並選取 hello 預期 Web 應用程式時所使用的訂用帳戶。 如果您使用 hello**部署 tooAzure** Web 應用程式名稱開頭的按鈕**網站**後面接著一些額外的字元。
   
    ![選取 Web 應用程式][cache-select-web-app]
4. 按一下**確定**toobegin hello 發行程序。 在幾分鐘之後 hello 發行程序完成，並以 hello 執行範例應用程式啟動瀏覽器。 如果您收到 DNS 錯誤時驗證或發行，而且 hello 佈建程序的 hello hello 應用程式的 Azure 資源是最近才完成稍候片刻，再試一次。
   
    ![已新增快取][cache-added-to-application]

hello 下表說明每個動作連結，來自 hello 範例應用程式。

| 動作 | 說明 |
| --- | --- |
| 建立新的 |建立新的隊伍。 |
| 遊戲賽季 |播放一季的遊戲，更新 hello 小組統計資料，並清除任何過期小組 hello 快取的資料。 |
| 清除快取 |從 hello 快取清除 hello 小組統計資料。 |
| 快取中的清單 |從 hello 快取中擷取 hello 小組統計資料。 如果沒有快取遺漏，載入 hello 資料庫中的 hello 統計資料，並將 toohello 快取儲存供下一次。 |
| 快取中的已排序集合 |從使用已排序資料的集的 hello 快取擷取 hello 小組統計資料。 如果沒有快取遺漏，載入 hello 資料庫中的 hello 統計資料，並儲存 toohello 快取使用已排序資料的集。 |
| 快取中的前 5 名隊伍 |從使用已排序資料的集的 hello 快取擷取 hello top 5 小組。 如果沒有快取遺漏，載入 hello 資料庫中的 hello 統計資料，並儲存 toohello 快取使用已排序資料的集。 |
| 從資料庫載入 |從 hello 資料庫擷取 hello 小組統計資料。 |
| 重建資料庫 |重建 hello 資料庫後再重新載入該小組的範例資料。 |
| 編輯/詳細資料/刪除 |編輯隊伍、檢視隊伍的詳細資料、刪除隊伍。 |

按一下某些 hello 動作，然後試驗 hello 不同來源擷取 hello 資料。 不是 hello 差異 hello 花的時間 toocomplete hello 從 hello 資料庫與 hello 快取擷取 hello 資料的各種方式。

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>當您完成 hello 應用程式時，刪除 hello 資源
當您完成 hello 範例教學課程應用程式時，您可以刪除 hello Azure 成本的順序 tooconserve 中使用的資源和資源。 如果您使用 hello**部署 tooAzure**按鈕在 hello[佈建 hello Azure 資源](#provision-the-azure-resources)區段和所有資源都包含在 hello 相同資源群組中，您可以刪除它們一起中其中一個藉由刪除 hello 資源群組的作業。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)按一下**資源群組**。
2. 型別 hello hello 到資源群組名稱**篩選項目...**文字方塊。
3. 按一下**...** toohello 權限的資源群組。
4. 按一下 [刪除] 。
   
    ![刪除][cache-delete-resource-group]
5. 您的資源群組，然後按一下類型 hello 名稱**刪除**。
   
    ![Confirm delete][cache-delete-confirm]

在幾分鐘的時間 hello 資源之後會刪除群組及其所有包含的資源。

> [!IMPORTANT]
> 請注意，刪除資源群組無法回復，而且 hello 資源群組和所有 hello 資源會永久刪除。 請確定您沒有不小心刪除 hello 錯誤的資源群組或資源。 如果您建立裝載在現有的資源群組內的這個範例的 hello 資源時，您可以在個別從其各自的刀鋒視窗中刪除每個資源。
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>在本機電腦上執行 hello 範例應用程式
toorun hello 應用程式在本機電腦上的，您需要 Azure Redis 快取哪些 toocache 上您的資料執行個體。 

* 如果您已經發行應用程式 tooAzure hello 上一節中所述，您可以使用該步驟期間所佈建的 hello Azure Redis 快取執行個體。
* 如果您有另一個現有的 Azure Redis 快取執行個體，您可以使用該 toorun 此範例在本機。
* 如果您需要 toocreate Azure Redis 快取執行個體，您可以依照中的 hello 步驟[建立快取](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)。

一旦您選取或建立 hello 快取 toouse，瀏覽 toohello hello Azure 入口網站中的快取並擷取 hello[主機名稱](cache-configure.md#properties)和[存取金鑰](cache-configure.md#access-keys)快取。 如需相關指示，請參閱 [設定 Redis 快取設定](cache-configure.md#configure-redis-cache-settings)。

1. 開啟 hello `WebAppPlusCacheAppSecrets.config` hello 期間建立的檔案[設定 hello 應用程式 toouse Redis 快取](#configure-the-application-to-use-redis-cache)使用您選擇的 hello 編輯器本教學課程的步驟。
2. 編輯 hello`value`屬性，並取代`MyCache.redis.cache.windows.net`以 hello[主機名稱](cache-configure.md#properties)快取，並指定其中一個 hello[主要或次要金鑰](cache-configure.md#access-keys)hello 密碼快取。

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. 按**Ctrl + F5** toorun hello 應用程式。

> [!NOTE]
> 請注意，在本機執行 hello 應用程式，包括 hello 資料庫且 hello Redis 快取裝載在 Azure 中，因為 hello 快取可能會出現 toounder-執行 hello 資料庫。 為了達到最佳效能，hello 用戶端應用程式和 Azure Redis 快取執行個體應該在 hello 相同的位置。 
> 
> 

## <a name="next-steps"></a>後續步驟
* 深入了解[開始使用 ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started)上 hello [ASP.NET](http://asp.net/)站台。
* App Service 中建立 ASP.NET Web 應用程式的詳細範例，請參閱[建立及部署 ASP.NET web 應用程式在 Azure App Service 中的](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service)從 hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015年連接[示範](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * 如需從 hello HealthClinic.biz 示範的快速入門，請參閱[Azure 開發人員工具快速入門](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)。
* 深入了解 hello[程式碼第一個 tooa 新資料庫](https://msdn.microsoft.com/data/jj193542)接近 tooEntity 本教學課程中所使用的架構。
* 深入了解 [Azure App Service 中的 Web 應用程式](../app-service-web/app-service-web-overview.md)。
* 了解如何太[監視器](cache-how-to-monitor.md)hello Azure 入口網站中的快取。
* 瀏覽 Azure Redis 快取進階功能
  
  * [如何 tooconfigure Premium Azure Redis 快取的持續性](cache-how-to-premium-persistence.md)
  * [如何 tooconfigure Premium Azure Redis 快取叢集](cache-how-to-premium-clustering.md)
  * [如何 tooconfigure 虛擬網路支援 Premium Azure Redis 快取](cache-how-to-premium-vnet.md)
  * 請參閱 hello [Azure Redis 快取常見問題集](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)如需詳細資訊大小、 輸送量和進階版快取使用的頻寬。

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

