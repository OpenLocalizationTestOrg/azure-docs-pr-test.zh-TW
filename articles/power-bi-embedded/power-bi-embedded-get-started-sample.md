---
title: "aaaGet 入門範例"
description: "Power BI Embedded，使用 SDK tooadd 互動式 Power BI 報表到您的商業智慧應用程式"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a>開始使用 Power BI Embedded 範例

運用 **Microsoft Power BI Embedded**，您可以將 Power BI 報告整合至您的 Web 應用程式或行動應用程式。 在本文中，我們將介紹您 toohello **Power BI Embedded** get 啟動的範例。

繼續討論之前，您可能會想 toosave hello 下列資源。 它們會太將 Power BI 報表整合到 hello 範例應用程式和您自己的應用程式時提供協助。

* [範例工作區 Web 應用程式](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Power BI Embedded API 參考](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (透過 NuGet 提供)
* [JavaScript 報告內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> 您可以設定及執行的 hello Power BI Embedded 取得啟動範例之前，您需要至少一個 toocreate**工作區集合**您 Azure 訂用帳戶中。 toolearn 如何 toocreate**工作區集合**hello Azure 入口網站中看到[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。

## <a name="configure-hello-sample-app"></a>Hello 範例應用程式設定

讓我們逐步解說設定 Visual Studio 開發環境 tooaccess hello 元件所需的 toorun hello 範例應用程式。

1. 下載並解壓縮 hello [Power BI Embedded-將報表整合到 web 應用程式](http://go.microsoft.com/fwlink/?LinkId=761493)GitHub 上的範例。
2. 在 Visual Studio 中開啟 **PowerBI-embedded.sln** 。 您可能需要 tooexecute hello**更新套件**hello 這個解決方案中的使用順序 tooupdate hello 封裝中的 NuGET 封裝管理員主控台中的命令。
3. 建置 hello 方案。
4. 執行 hello **ProvisionSample**主控台應用程式。 Hello 範例主控台應用程式，您可以佈建的工作區，並匯入 PBIX 檔案。
5. 新 tooprovision**工作區**，選取選項 1，**集合管理**，然後選取選項 6，**提供新的工作區**
6. 新 tooimport**報表**，選取 選項 2:**報告管理**，然後選取選項 3，**匯入 PBIX Desktop 檔案，在工作區**。

7. 輸入您的 [工作區集合] 名稱，以及 [存取金鑰]。 您可以取得這些 hello **Azure 入口網站**。 深入了解如何 toolearn tooget 您**便捷鍵**，請參閱[檢視 Power BI API 存取金鑰](power-bi-embedded-get-started.md#view-power-bi-api-access-keys)中開始使用 Microsoft Power BI Embedded。

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. 複製並儲存新建立的 hello**工作區識別碼**toouse 本文稍後。 之後 hello**工作區識別碼**已建立，您可以找到它 hello **Azure 入口網站**。

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. tooimport PBIX 檔案到您**工作區**，選取選項**6。**\[將 PBIX Desktop 檔案匯入現有的工作區\]。 如果您沒有 PBIX 檔案很方便，您可以下載 hello[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)。
10. 如果出現提示，請輸入易記名稱做為您「資料集」 的名稱。

您應該會看到像這樣的回應：

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> 如果您的 PBIX 檔案包含的任何直接查詢連接，執行選項 7 tooupdate hello 連接字串。

此時，您已經將 Power BI PBIX 報表匯入到您的**工作區**。 現在，讓我們看看 toorun hello **Power BI Embedded**取得已啟動的範例 web 應用程式。

## <a name="run-hello-sample-web-app"></a>執行 hello 範例 web 應用程式
hello web 應用程式範例是範例應用程式匯入到將報表轉譯您**工作區**。 以下是如何 tooconfigure hello web 應用程式範例。

1. 在 hello **PowerBI 內嵌**Visual Studio 方案，右邊按一下 hello **EmbedSample** web 應用程式，並選擇**設定為啟始專案**。
2. 在**web.config**，在 hello **EmbedSample** web 應用程式，請編輯 hello **appSettings**: **AccessKey**， **WorkspaceCollection**名稱，和**工作區識別碼**。

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. 執行 hello **EmbedSample** web 應用程式。

一旦執行 hello **EmbedSample** web 應用程式，應該包含 hello 左邊的導覽面板**報表**功能表。 tooview hello 報表匯入，依序展開**報表**，按一下報表。 如果您匯入 hello[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)，hello 範例 web 應用程式會看起來像這樣：

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

按一下報表之後，hello **EmbedSample** web 應用程式看起來應該這樣：

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>瀏覽 hello 範例程式碼

hello **Microsoft Power BI Embedded**範例是為您示範如何的範例 web 應用程式 toointegrate **Power BI**報表到應用程式。 它會使用模型檢視控制器 (MVC) 設計模式 toodemonstrate 最佳作法。 本章節強調 hello 範例程式碼，您可以瀏覽 hello 內的部分**PowerBI 內嵌**web 應用程式方案。 hello 模型檢視控制器 (MVC) 模式分隔 hello hello 網域、 hello 簡報和 hello 動作分成三個不同類別的使用者輸入所根據的模型： 模型、 檢視和控制。 toolearn 深入了解 MVC，請參閱[深入了解 ASP.NET](http://www.asp.net/mvc)。

hello **Microsoft Power BI Embedded**範例程式碼會區隔，如下所示。 每個區段 hello PowerBI embedded.sln 方案中包含 hello 檔案名稱，以便您可以輕鬆找到 hello 範例中的 hello 程式碼。

> [!NOTE]
> 此區段是摘要的 hello 範例程式碼會顯示 hello 程式碼撰寫的方式。 tooview hello 完整範例，請載入 Visual Studio 中的 hello PowerBI embedded.sln 方案。

### <a name="model"></a>模型

hello 範例具有**ReportsViewModel**和**ReportViewModel**。

**ReportsViewModel.cs**：代表 Power BI Reports。

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**：代表 Power BI Report。

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>連接字串

hello 連接字串必須是下列格式的 hello:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

使用一般伺服器和資料庫屬性將會失敗。 例如：Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>檢視

hello**檢視**管理 Power BI 的 hello 顯示**報表**和 Power BI**報表**。

**Reports.cshtml**： 逐一查看**Model.Reports** toocreate **ActionLink**。 hello **ActionLink**是由所組成，如下所示：

| 部分 | 說明 |
| --- | --- |
| Title |Hello 報表的名稱。 |
| QueryString |連結 toohello 報表識別碼。 |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

Report.cshtml： 設定 hello **Model.AccessToken**，hello 的 Lambda 運算式和**PowerBIReportFor**。

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs**：建立會傳遞**應用程式權杖**的 PowerBIClient。 JSON Web Token (JWT) 會產生從 hello**簽署金鑰**tooget hello**認證**。 hello**認證**的執行個體是使用的 toocreate **PowerBIClient**。 在您擁有 **PowerBIClient** 的執行個體之後，您就可以呼叫 GetReports() 與 GetReportsAsync()。

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


Task<ActionResult> Report(string reportId)

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a>將報表整合到您的應用程式中

一旦**報表**，您使用**IFrame** tooembed hello Power BI**報表**。 以下是從 powerbi.js hello 中的程式碼片段**Microsoft Power BI Embedded**範例。

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>篩選內嵌在應用程式中的報表

您可以使用 URL 語法，篩選內嵌的報表。 toodo，您將加入**$filter**查詢字串參數**eq**運算子 tooyour iFrame src url 並指定 hello 篩選器。 以下是 hello 篩選的查詢語法：

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {表格名稱/欄位名稱} 不能包含空格或特殊字元。 hello {fieldValue} 接受單一類別值。  

## <a name="see-also"></a>另請參閱

[Microsoft Power BI Embedded 常見案例](power-bi-embedded-scenarios.md)  
[在 Power BI Embedded 中驗證和授權](power-bi-embedded-app-token-flow.md)  
[內嵌報告](power-bi-embedded-embed-report.md)  
[從資料集建立新的報告](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript 內嵌範例](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)
