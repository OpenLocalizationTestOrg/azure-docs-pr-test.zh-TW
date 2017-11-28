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
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="a68ef-103">開始使用 Power BI Embedded 範例</span><span class="sxs-lookup"><span data-stu-id="a68ef-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="a68ef-104">運用 **Microsoft Power BI Embedded**，您可以將 Power BI 報告整合至您的 Web 應用程式或行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68ef-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="a68ef-105">在本文中，我們將介紹您 toohello **Power BI Embedded** get 啟動的範例。</span><span class="sxs-lookup"><span data-stu-id="a68ef-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="a68ef-106">繼續討論之前，您可能會想 toosave hello 下列資源。</span><span class="sxs-lookup"><span data-stu-id="a68ef-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="a68ef-107">它們會太將 Power BI 報表整合到 hello 範例應用程式和您自己的應用程式時提供協助。</span><span class="sxs-lookup"><span data-stu-id="a68ef-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="a68ef-108">範例工作區 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68ef-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="a68ef-109">Power BI Embedded API 參考</span><span class="sxs-lookup"><span data-stu-id="a68ef-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="a68ef-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (透過 NuGet 提供)</span><span class="sxs-lookup"><span data-stu-id="a68ef-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="a68ef-111">JavaScript 報告內嵌範例</span><span class="sxs-lookup"><span data-stu-id="a68ef-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="a68ef-112">您可以設定及執行的 hello Power BI Embedded 取得啟動範例之前，您需要至少一個 toocreate**工作區集合**您 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a68ef-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="a68ef-113">toolearn 如何 toocreate**工作區集合**hello Azure 入口網站中看到[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="a68ef-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="a68ef-114">Hello 範例應用程式設定</span><span class="sxs-lookup"><span data-stu-id="a68ef-114">Configure hello sample app</span></span>

<span data-ttu-id="a68ef-115">讓我們逐步解說設定 Visual Studio 開發環境 tooaccess hello 元件所需的 toorun hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68ef-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="a68ef-116">下載並解壓縮 hello [Power BI Embedded-將報表整合到 web 應用程式](http://go.microsoft.com/fwlink/?LinkId=761493)GitHub 上的範例。</span><span class="sxs-lookup"><span data-stu-id="a68ef-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="a68ef-117">在 Visual Studio 中開啟 **PowerBI-embedded.sln** 。</span><span class="sxs-lookup"><span data-stu-id="a68ef-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="a68ef-118">您可能需要 tooexecute hello**更新套件**hello 這個解決方案中的使用順序 tooupdate hello 封裝中的 NuGET 封裝管理員主控台中的命令。</span><span class="sxs-lookup"><span data-stu-id="a68ef-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="a68ef-119">建置 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="a68ef-119">Build hello solution.</span></span>
4. <span data-ttu-id="a68ef-120">執行 hello **ProvisionSample**主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68ef-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="a68ef-121">Hello 範例主控台應用程式，您可以佈建的工作區，並匯入 PBIX 檔案。</span><span class="sxs-lookup"><span data-stu-id="a68ef-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="a68ef-122">新 tooprovision**工作區**，選取選項 1，**集合管理**，然後選取選項 6，**提供新的工作區**</span><span class="sxs-lookup"><span data-stu-id="a68ef-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="a68ef-123">新 tooimport**報表**，選取 選項 2:**報告管理**，然後選取選項 3，**匯入 PBIX Desktop 檔案，在工作區**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="a68ef-124">輸入您的 [工作區集合] 名稱，以及 [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="a68ef-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="a68ef-125">您可以取得這些 hello **Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="a68ef-126">深入了解如何 toolearn tooget 您**便捷鍵**，請參閱[檢視 Power BI API 存取金鑰](power-bi-embedded-get-started.md#view-power-bi-api-access-keys)中開始使用 Microsoft Power BI Embedded。</span><span class="sxs-lookup"><span data-stu-id="a68ef-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="a68ef-127">複製並儲存新建立的 hello**工作區識別碼**toouse 本文稍後。</span><span class="sxs-lookup"><span data-stu-id="a68ef-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="a68ef-128">之後 hello**工作區識別碼**已建立，您可以找到它 hello **Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="a68ef-129">tooimport PBIX 檔案到您**工作區**，選取選項**6。**\[將 PBIX Desktop 檔案匯入現有的工作區\]。</span><span class="sxs-lookup"><span data-stu-id="a68ef-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="a68ef-130">如果您沒有 PBIX 檔案很方便，您可以下載 hello[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)。</span><span class="sxs-lookup"><span data-stu-id="a68ef-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="a68ef-131">如果出現提示，請輸入易記名稱做為您「資料集」 的名稱。</span><span class="sxs-lookup"><span data-stu-id="a68ef-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="a68ef-132">您應該會看到像這樣的回應：</span><span class="sxs-lookup"><span data-stu-id="a68ef-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="a68ef-133">如果您的 PBIX 檔案包含的任何直接查詢連接，執行選項 7 tooupdate hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="a68ef-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="a68ef-134">此時，您已經將 Power BI PBIX 報表匯入到您的**工作區**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="a68ef-135">現在，讓我們看看 toorun hello **Power BI Embedded**取得已啟動的範例 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68ef-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="a68ef-136">執行 hello 範例 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a68ef-136">Run hello sample web app</span></span>
<span data-ttu-id="a68ef-137">hello web 應用程式範例是範例應用程式匯入到將報表轉譯您**工作區**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="a68ef-138">以下是如何 tooconfigure hello web 應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="a68ef-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="a68ef-139">在 hello **PowerBI 內嵌**Visual Studio 方案，右邊按一下 hello **EmbedSample** web 應用程式，並選擇**設定為啟始專案**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="a68ef-140">在**web.config**，在 hello **EmbedSample** web 應用程式，請編輯 hello **appSettings**: **AccessKey**， **WorkspaceCollection**名稱，和**工作區識別碼**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="a68ef-141">執行 hello **EmbedSample** web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68ef-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="a68ef-142">一旦執行 hello **EmbedSample** web 應用程式，應該包含 hello 左邊的導覽面板**報表**功能表。</span><span class="sxs-lookup"><span data-stu-id="a68ef-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="a68ef-143">tooview hello 報表匯入，依序展開**報表**，按一下報表。</span><span class="sxs-lookup"><span data-stu-id="a68ef-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="a68ef-144">如果您匯入 hello[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)，hello 範例 web 應用程式會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a68ef-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="a68ef-145">按一下報表之後，hello **EmbedSample** web 應用程式看起來應該這樣：</span><span class="sxs-lookup"><span data-stu-id="a68ef-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="a68ef-146">瀏覽 hello 範例程式碼</span><span class="sxs-lookup"><span data-stu-id="a68ef-146">Explore hello sample code</span></span>

<span data-ttu-id="a68ef-147">hello **Microsoft Power BI Embedded**範例是為您示範如何的範例 web 應用程式 toointegrate **Power BI**報表到應用程式。</span><span class="sxs-lookup"><span data-stu-id="a68ef-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="a68ef-148">它會使用模型檢視控制器 (MVC) 設計模式 toodemonstrate 最佳作法。</span><span class="sxs-lookup"><span data-stu-id="a68ef-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="a68ef-149">本章節強調 hello 範例程式碼，您可以瀏覽 hello 內的部分**PowerBI 內嵌**web 應用程式方案。</span><span class="sxs-lookup"><span data-stu-id="a68ef-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="a68ef-150">hello 模型檢視控制器 (MVC) 模式分隔 hello hello 網域、 hello 簡報和 hello 動作分成三個不同類別的使用者輸入所根據的模型： 模型、 檢視和控制。</span><span class="sxs-lookup"><span data-stu-id="a68ef-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="a68ef-151">toolearn 深入了解 MVC，請參閱[深入了解 ASP.NET](http://www.asp.net/mvc)。</span><span class="sxs-lookup"><span data-stu-id="a68ef-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="a68ef-152">hello **Microsoft Power BI Embedded**範例程式碼會區隔，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a68ef-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="a68ef-153">每個區段 hello PowerBI embedded.sln 方案中包含 hello 檔案名稱，以便您可以輕鬆找到 hello 範例中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="a68ef-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="a68ef-154">此區段是摘要的 hello 範例程式碼會顯示 hello 程式碼撰寫的方式。</span><span class="sxs-lookup"><span data-stu-id="a68ef-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="a68ef-155">tooview hello 完整範例，請載入 Visual Studio 中的 hello PowerBI embedded.sln 方案。</span><span class="sxs-lookup"><span data-stu-id="a68ef-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="a68ef-156">模型</span><span class="sxs-lookup"><span data-stu-id="a68ef-156">Model</span></span>

<span data-ttu-id="a68ef-157">hello 範例具有**ReportsViewModel**和**ReportViewModel**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="a68ef-158">**ReportsViewModel.cs**：代表 Power BI Reports。</span><span class="sxs-lookup"><span data-stu-id="a68ef-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="a68ef-159">**ReportViewModel.cs**：代表 Power BI Report。</span><span class="sxs-lookup"><span data-stu-id="a68ef-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="a68ef-160">連接字串</span><span class="sxs-lookup"><span data-stu-id="a68ef-160">Connection string</span></span>

<span data-ttu-id="a68ef-161">hello 連接字串必須是下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="a68ef-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="a68ef-162">使用一般伺服器和資料庫屬性將會失敗。</span><span class="sxs-lookup"><span data-stu-id="a68ef-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="a68ef-163">例如：Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="a68ef-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="a68ef-164">檢視</span><span class="sxs-lookup"><span data-stu-id="a68ef-164">View</span></span>

<span data-ttu-id="a68ef-165">hello**檢視**管理 Power BI 的 hello 顯示**報表**和 Power BI**報表**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="a68ef-166">**Reports.cshtml**： 逐一查看**Model.Reports** toocreate **ActionLink**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="a68ef-167">hello **ActionLink**是由所組成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a68ef-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="a68ef-168">部分</span><span class="sxs-lookup"><span data-stu-id="a68ef-168">Part</span></span> | <span data-ttu-id="a68ef-169">說明</span><span class="sxs-lookup"><span data-stu-id="a68ef-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a68ef-170">Title</span><span class="sxs-lookup"><span data-stu-id="a68ef-170">Title</span></span> |<span data-ttu-id="a68ef-171">Hello 報表的名稱。</span><span class="sxs-lookup"><span data-stu-id="a68ef-171">Name of hello Report.</span></span> |
| <span data-ttu-id="a68ef-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="a68ef-172">QueryString</span></span> |<span data-ttu-id="a68ef-173">連結 toohello 報表識別碼。</span><span class="sxs-lookup"><span data-stu-id="a68ef-173">A link toohello Report ID.</span></span> |

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

<span data-ttu-id="a68ef-174">Report.cshtml： 設定 hello **Model.AccessToken**，hello 的 Lambda 運算式和**PowerBIReportFor**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="a68ef-175">Controller</span><span class="sxs-lookup"><span data-stu-id="a68ef-175">Controller</span></span>

<span data-ttu-id="a68ef-176">**DashboardController.cs**：建立會傳遞**應用程式權杖**的 PowerBIClient。</span><span class="sxs-lookup"><span data-stu-id="a68ef-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="a68ef-177">JSON Web Token (JWT) 會產生從 hello**簽署金鑰**tooget hello**認證**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="a68ef-178">hello**認證**的執行個體是使用的 toocreate **PowerBIClient**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="a68ef-179">在您擁有 **PowerBIClient** 的執行個體之後，您就可以呼叫 GetReports() 與 GetReportsAsync()。</span><span class="sxs-lookup"><span data-stu-id="a68ef-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="a68ef-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="a68ef-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="a68ef-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="a68ef-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="a68ef-182">Task<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="a68ef-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="a68ef-183">將報表整合到您的應用程式中</span><span class="sxs-lookup"><span data-stu-id="a68ef-183">Integrate a report into your app</span></span>

<span data-ttu-id="a68ef-184">一旦**報表**，您使用**IFrame** tooembed hello Power BI**報表**。</span><span class="sxs-lookup"><span data-stu-id="a68ef-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="a68ef-185">以下是從 powerbi.js hello 中的程式碼片段**Microsoft Power BI Embedded**範例。</span><span class="sxs-lookup"><span data-stu-id="a68ef-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="a68ef-186">篩選內嵌在應用程式中的報表</span><span class="sxs-lookup"><span data-stu-id="a68ef-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="a68ef-187">您可以使用 URL 語法，篩選內嵌的報表。</span><span class="sxs-lookup"><span data-stu-id="a68ef-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="a68ef-188">toodo，您將加入**$filter**查詢字串參數**eq**運算子 tooyour iFrame src url 並指定 hello 篩選器。</span><span class="sxs-lookup"><span data-stu-id="a68ef-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="a68ef-189">以下是 hello 篩選的查詢語法：</span><span class="sxs-lookup"><span data-stu-id="a68ef-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="a68ef-190">{表格名稱/欄位名稱} 不能包含空格或特殊字元。</span><span class="sxs-lookup"><span data-stu-id="a68ef-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="a68ef-191">hello {fieldValue} 接受單一類別值。</span><span class="sxs-lookup"><span data-stu-id="a68ef-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="a68ef-192">另請參閱</span><span class="sxs-lookup"><span data-stu-id="a68ef-192">See also</span></span>

[<span data-ttu-id="a68ef-193">Microsoft Power BI Embedded 常見案例</span><span class="sxs-lookup"><span data-stu-id="a68ef-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="a68ef-194">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="a68ef-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="a68ef-195">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="a68ef-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="a68ef-196">從資料集建立新的報告</span><span class="sxs-lookup"><span data-stu-id="a68ef-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="a68ef-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="a68ef-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="a68ef-198">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="a68ef-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="a68ef-199">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="a68ef-199">More questions?</span></span> [<span data-ttu-id="a68ef-200">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="a68ef-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
