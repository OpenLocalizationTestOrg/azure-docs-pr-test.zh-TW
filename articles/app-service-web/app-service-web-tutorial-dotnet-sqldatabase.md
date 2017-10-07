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
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>在 Azure 中搭配 SQL Database 來建置 ASP.NET 應用程式

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。 本教學課程告訴您如何 toodeploy 資料驅動的 ASP.NET web 應用程式在 Azure 中的並將它連接太[Azure SQL Database](../sql-database/sql-database-technical-overview.md)。 當您完成時，您有執行的 ASP.NET 應用程式[Azure App Service](../app-service/app-service-value-prop-what-is.md)且連線 tooSQL 資料庫。

![已在 Azure Web 應用程式中發佈的 ASP.NET 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 SQL Database
> * 連接的 ASP.NET 應用程式 tooSQL 資料庫
> * 部署 hello 應用程式 tooAzure
> * 更新 hello 資料模型，部署 hello 應用程式
> * 從 Azure tooyour 終端機的資料流記錄檔
> * 管理 hello hello Azure 入口網站中的應用程式

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

* 安裝[Visual Studio 2017](https://www.visualstudio.com/downloads/)以下列工作負載的 hello:
  - **ASP.NET 和 Web 開發**
  - **Azure 開發**

  ![ASP.NET 和 Web 開發及 Azure 開發 (在 [Web 和雲端] 之下)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>下載 hello 範例

[下載 hello 範例專案](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip)。

擷取 （解壓縮） hello *dotnet sqldb 教學課程-master.zip*檔案。

hello 範例專案包含基本[ASP.NET MVC](https://www.asp.net/mvc) CRUD （建立讀取-更新-刪除） 的應用程式使用[Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

### <a name="run-hello-app"></a>執行 hello 應用程式

開啟 hello *dotnet-sqldb-教學課程的主要/DotNetAppSqlDb.sln* Visual Studio 中的檔案。 

型別`Ctrl+F5`toorun hello 應用程式，但不偵錯。 hello 應用程式會顯示在預設瀏覽器。 選取 hello**新建**連結，並建立幾*待辦事項*項目。 

![[新增 ASP.NET 專案] 對話方塊](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

測試 hello**編輯**，**詳細資料**，和**刪除**連結。

hello 應用程式會將資料庫內容 tooconnect 使用 hello 資料庫。 在此範例中，hello 資料庫內容會使用名為連接字串`MyDbConnection`。 設定 hello 連接字串中 hello *Web.config*檔案和參考中的 hello *Models/MyDatabaseContext.cs*檔案。 稍後 hello 教學課程 tooconnect hello Azure web 應用程式 tooan Azure SQL Database 會使用 hello 連接字串名稱。 

## <a name="publish-tooazure-with-sql-database"></a>發行 SQL Database 的 tooAzure

在 [hello**方案總管] 中**，以滑鼠右鍵按一下您**DotNetAppSqlDb**專案，然後選取**發行**。

![從方案總管發佈](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

確定已選取 [Microsoft Azure App Service]，然後按一下 [發佈]。

![從專案概觀頁面發佈](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

發行會開啟 hello**建立 App Service**對話方塊中，可協助您建立所有 hello toorun 您需要在 Azure 中的 ASP.NET web 應用程式的 Azure 資源。

### <a name="sign-in-tooazure"></a>登入 tooAzure

在 hello**建立 App Service** ] 對話方塊中，按一下 [**將帳戶加入**，然後登入 tooyour Azure 訂用帳戶。 如果您已登入 Microsoft 帳戶，請確定該帳戶保留您的 Azure 訂用帳戶。 如果 hello 登入的 Microsoft 帳戶沒有 Azure 訂用帳戶，按一下 tooadd hello 正確的帳戶。
   
![登入 tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

一旦登入，您已準備好 toocreate 所有 hello 您需要在這個對話方塊中，Azure web 應用程式的資源。

### <a name="configure-hello-web-app-name"></a>設定 hello web 應用程式名稱

您可以保留 hello 產生 web 應用程式名稱，或將它變更 tooanother 唯一的名稱 (有效的字元是`a-z`， `0-9`，和`-`)。 hello web 應用程式名稱應用程式時做 hello 預設 URL 的一部分 (`<app_name>.azurewebsites.net`，其中`<app_name>`是您的 web 應用程式名稱)。 hello web 應用程式名稱必須 toobe 唯一跨 Azure 中的所有應用程式。 

![建立 App Service 對話方塊](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>建立資源群組

[!INCLUDE [resource-group](../../includes/resource-group.md)]

下一步太**資源群組**，按一下 **新增**。

![下一步 tooResource 群組中，按一下 [新增]。](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

名稱 hello 資源群組**myResourceGroup**。

> [!NOTE]
> 不要按一下 [建立]。 您必須先 tooset 稍後步驟中將 SQL 資料庫。

### <a name="create-an-app-service-plan"></a>建立應用程式服務方案

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

下一步太**App Service 方案**，按一下 **新增**。 

在 hello**設定應用程式服務方案** 對話方塊中，設定下列設定的 hello 與 hello 新應用程式服務方案：

![建立 App Service 方案](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| 設定  | 建議的值 | 如需 Blob 的詳細資訊， |
| ----------------- | ------------ | ----|
|**App Service 方案**| myAppServicePlan | [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**位置**| 西歐 | [Azure 區域](https://azure.microsoft.com/regions/) |
|**大小**| 免費 | [定價層](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>建立 SQL Server 執行個體

建立資料庫之前，您需要 [Azure SQL Database 邏輯伺服器](../sql-database/sql-database-features.md)。 邏輯伺服器包含一組當作群組管理的資料庫。

選取 [瀏覽其他 Azure 服務]。

![設定 Web 應用程式名稱](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

在 hello**服務**索引標籤上，按一下 hello  **+** 圖示下一步太**SQL Database**。 

![在 hello 服務索引標籤上，按一下 hello + 圖示下一步 tooSQL 資料庫。](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

在 [hello**設定 SQL Database** ] 對話方塊中，按一下**新增**下一步太**SQL Server**。 

唯一的伺服器名稱隨即產生。 這個名稱會用於 hello 預設 URL 的一部分邏輯伺服器， `<server_name>.database.windows.net`。 它在 Azure 中的所有邏輯伺服器執行個體之間必須是唯一的。 您可以變更 hello 伺服器名稱，但本教學課程中，保留 hello 產生值。

新增系統管理員使用者名稱和密碼，然後選取 [確定]。 如需密碼複雜性需求，請參閱[密碼原則](/sql/relational-databases/security/password-policy)。

請記住這個使用者名稱和密碼。 需要 toomanage hello 邏輯伺服器執行個體更新版本。

![建立 SQL Server 執行個體](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>建立 SQL Database

在 hello**設定 SQL Database**對話方塊： 

* 保留產生 hello 預設**資料庫名稱**。
* 在 [連接字串名稱] 中，輸入 *MyDbConnection*。 此名稱必須符合 hello 連接字串中所參考*Models/MyDatabaseContext.cs*。
* 選取 [確定] 。

![設定 SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

hello**建立 App Service**對話方塊會顯示 hello 資源已建立。 按一下 [建立] 。 

![您已建立 hello 資源](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

一旦 hello 精靈完成建立 hello Azure 資源時，它會發行您的 ASP.NET 應用程式 tooAzure。 預設的瀏覽器會使用 hello URL toohello 部署應用程式啟動。 

新增幾個待辦事項項目。

![已在 Azure Web 應用程式中發佈的 ASP.NET 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

恭喜！ 您的資料導向 ASP.NET 應用程式正在 Azure App Service 中執行。

## <a name="access-hello-sql-database-locally"></a>存取 hello 本機 SQL 資料庫

Visual Studio 可讓您瀏覽和管理您新的 SQL 資料庫，輕鬆地在 hello **SQL Server 物件總管**。

### <a name="create-a-database-connection"></a>建立資料庫連接

從 hello**檢視**功能表上，選取**SQL Server 物件總管**。

頂端的 hello **SQL Server 物件總管**，按一下 hello**加入 SQL Server**  按鈕。

### <a name="configure-hello-database-connection"></a>設定 hello 資料庫連接

在 [hello**連接**] 對話方塊中，展開 hello **Azure**節點。 此處會列出 Azure 中您所有的 SQL Database 執行個體。

選取 hello `DotNetAppSqlDb` SQL 資料庫。 您稍早建立的 hello 連線會自動填入 hello 底部。

輸入您稍早建立的 hello 資料庫系統管理員密碼，然後按一下**連接**。

![從 Visual Studio 設定資料庫連接](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>允許來自您電腦的用戶端連接

hello**建立新的防火牆規則**對話方塊開啟。 根據預設，您的 SQL Database 執行個體僅允許來自 Azure 服務 (例如 Azure Web 應用程式) 的連線。 tooconnect tooyour 資料庫，請在 hello SQL Database 執行個體中建立的防火牆規則。 hello 防火牆規則可讓您的本機電腦的 hello 公用 IP 位址。

hello 對話方塊已填入您的電腦公用 IP 位址。

確定已選取 [加入我的用戶端 IP]，然後按一下 [確定]。 

![設定 SQL Database 執行個體的防火牆](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Visual Studio 完成建立您的 SQL Database 執行個體的 hello 防火牆設定時，一旦您的連線會出現在**SQL Server 物件總管**。

在這裡，您可以執行 hello 最常見資料庫作業，例如執行查詢，建立檢視和預存程序，以及更多。 

以滑鼠右鍵按一下 hello`Todoes`資料表，然後選取**檢視資料**。 

![探索 SQL Database 物件](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>使用 Code First 移轉更新應用程式

您可以在 Azure 中使用 hello 熟悉的工具，在 Visual Studio tooupdate 資料庫與 web 應用程式。 在此步驟中，您會在 Entity Framework toomake 變更 tooyour 資料庫結構描述中使用 Code First 移轉，並將它發行 tooAzure。

如需有關使用 Entity Framework Code First 移轉的詳細資訊，請參閱[使用 MVC 5 開始使用 Entity Framework 6 Code First](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

### <a name="update-your-data-model"></a>更新資料模型

開啟_Models\Todo.cs_ hello 程式碼編輯器中。 新增下列屬性 toohello hello`ToDo`類別：

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>在本機執行 Code First 移轉

執行一些命令 toomake 更新 tooyour 本機資料庫。 

從 hello**工具**功能表上，按一下  **NuGet 套件管理員** > **Package Manager Console**。

在 [hello 封裝管理員主控台] 視窗，啟用 Code First 移轉：

```PowerShell
Enable-Migrations
```

新增移轉：

```PowerShell
Add-Migration AddProperty
```

更新 hello 本機資料庫：

```PowerShell
Update-Database
```

型別`Ctrl+F5`toorun hello 應用程式。 測試 hello 編輯詳細資料，與建立連結。

如果 hello 應用程式載入無錯誤，Code First 移轉已成功。 不過，您的頁面仍看起來會 hello 相同，因為應用程式邏輯還未使用這個新屬性。 

### <a name="use-hello-new-property"></a>使用 hello 新屬性

在您的程式碼 toouse hello 進行一些變更`Done`屬性。 為了簡單起見，本教學課程中，您只會 toochange hello`Index`和`Create`toosee hello 屬性檢視作用中。

開啟 _Controllers\TodosController.cs_。

尋找 hello`Create()`方法並加入`Done`toohello hello 中屬性清單`Bind`屬性。 當您完成時，您`Create()`方法簽章看起來像下列程式碼的 hello:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

開啟 _Views\Todos\Create.cshtml_。

在 hello Razor 程式碼，您應該會看到`<div class="form-group">`項目，會使用`model.Description`，和另一個`<div class="form-group">`項目，會使用`model.CreatedDate`。 在這兩個元素的正後方，新增另一個使用 `model.Done` 的 `<div class="form-group">` 元素：

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

開啟 _Views\Todos\Index.cshtml_。

搜尋空白的 hello`<th></th>`項目。 這個元素的正上方加入下列 Razor 程式碼的 hello:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

尋找 hello`<td>`項目，包含 hello `Html.ActionLink()` helper 方法。 這個元素的正上方加入下列 Razor 程式碼的 hello:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

您只需要在 hello toosee hello 變更`Index`和`Create`檢視。 

型別`Ctrl+F5`toorun hello 應用程式。

您現在可以新增待辦事項項目，並且勾選 [完成]。 然後，它應該會在您的首頁中顯示為已完成的項目。 請記住該 hello`Edit`檢視不會顯示 hello`Done`欄位，因為您沒有變更 hello`Edit`檢視。

### <a name="enable-code-first-migrations-in-azure"></a>啟用 Azure 中的 Code First 移轉

現在，您的程式碼變更的運作方式，包括資料庫移轉，您將它發行 tooyour Azure web 應用程式，然後太 Code First 移轉更新您的 SQL 資料庫。

就像之前一樣，以滑鼠右鍵按一下專案，然後選取 [發佈]。

按一下**設定**tooopen hello 發行精靈。

![開啟發佈設定](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

在 hello 精靈 中，按一下 **下一步**。

請確定該 hello 連接字串中已填入您的 SQL Database **MyDatabaseContext (MyDbConnection)**。 您可能需要 tooselect hello **myToDoAppDb**從 hello 下拉式清單中的資料庫。 

選取 [執行 Code First 移轉 (在應用程式啟動時執行)] ，然後按一下 [儲存]。

![在 Azure Web 應用程式中啟用 Code First 移轉](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>發佈您的變更

現在，您已在 Azure Web 應用程式中啟用 Code First 移轉，只需發佈您的程式碼變更即可。

在 hello 發行頁中，按一下**發行**。

嘗試再次新增待辦事項，然後選取 [完成]，而它們應該會在您的首頁中顯示為已完成的項目。

![Code First 移轉之後的 Azure Web 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

仍會顯示您現有的所有待辦事項項目。 當您重新發佈 ASP.NET 應用程式時，您 SQL Database 中現有的資料不會遺失。 此外，Code First 移轉只會變更 hello 資料結構描述，會保留現有的資料。


## <a name="stream-application-logs"></a>資料流應用程式記錄

您可以直接從您的 Azure web 應用程式 tooVisual Studio 串流追蹤訊息。

開啟 _Controllers\TodosController.cs_。

每個動作都是以 `Trace.WriteLine()` 方法開始。 此程式碼會加入 tooshow 您 tooadd 追蹤訊息 tooyour Azure web 應用程式的方式。

### <a name="open-server-explorer"></a>開啟伺服器總管

從 hello**檢視**功能表上，選取**伺服器總管**。 您可以在 [伺服器總管] 中設定 Azure Web 應用程式的記錄。 

### <a name="enable-log-streaming"></a>啟用記錄資料流

在 [伺服器總管] 中，展開 [Azure] > [App Service]。

展開 hello **myResourceGroup**資源群組時所建立您第一次建立 hello Azure web 應用程式。

以滑鼠右鍵按一下您的 Azure Web 應用程式，然後選取 [檢視資料流記錄]。

![啟用記錄資料流](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

hello 記錄檔現在串流處理到 hello**輸出**視窗。 

![[輸出] 視窗中的記錄資料流](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

不過，您不尚未看到任何 hello 追蹤訊息。 因為當您第一次選取**檢視串流記錄**，Azure web 應用程式設定 hello 追蹤層級太`Error`，這只記錄錯誤事件 (以 hello`Trace.TraceError()`方法)。

### <a name="change-trace-levels"></a>變更追蹤層級

toochange hello 追蹤層級 toooutput 其他追蹤訊息，請移回太**伺服器總管**。

再次以滑鼠右鍵按一下您的 Azure Web 應用程式，然後選取 [設定]。

在 hello**的應用程式記錄 （檔案系統）**下拉式清單中，選取**Verbose**。 按一下 [儲存] 。

![變更追蹤層級 tooVerbose](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> 您可以試驗不同的追蹤層級 toosee 的訊息類型會顯示每個層級。 例如，hello**資訊**層級包含所建立的所有記錄檔`Trace.TraceInformation()`， `Trace.TraceWarning()`，和`Trace.TraceError()`，但不是所建立的記錄檔`Trace.WriteLine()`。
>
>

在瀏覽器，請按一下 Azure 中的 hello 待辦事項清單應用程式周圍。 hello 追蹤訊息現在進行串流 toohello**輸出**Visual Studio 中的視窗。

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>停止記錄資料流

toostop hello 記錄串流服務，請按一下 hello**停止監視**按鈕在 hello**輸出**視窗。

![停止記錄資料流](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>管理您的 Azure Web 應用程式

移 toohello [Azure 入口網站](https://portal.azure.com)toosee hello web 應用程式所建立。 



從 hello 左窗格中，按一下  **App Service**，然後按一下 hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

您已來到 Web 應用程式的分頁。 

根據預設，hello 入口網站會顯示 hello**概觀**頁面。 此頁面可讓您檢視應用程式的執行方式。 您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 在左邊 hello 頁面 hello hello 索引標籤會顯示 hello 不同的組態頁面，您可以開啟。 

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 在 Azure 中建立 SQL Database
> * 連接的 ASP.NET 應用程式 tooSQL 資料庫
> * 部署 hello 應用程式 tooAzure
> * 更新 hello 資料模型，部署 hello 應用程式
> * 從 Azure tooyour 終端機的資料流記錄檔
> * 管理 hello hello Azure 入口網站中的應用程式

前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 toohello web 應用程式的方式。

> [!div class="nextstepaction"]
> [將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應](app-service-web-tutorial-custom-domain.md)
