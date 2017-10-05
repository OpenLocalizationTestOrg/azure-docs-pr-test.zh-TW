---
title: "以範例作為起始"
description: "對於 Power BI Embedded，使用 SDK 將互動式 Power BI 報告加入您的商務智慧應用程式中"
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
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="bae99-103">開始使用 Power BI Embedded 範例</span><span class="sxs-lookup"><span data-stu-id="bae99-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="bae99-104">運用 **Microsoft Power BI Embedded**，您可以將 Power BI 報告整合至您的 Web 應用程式或行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="bae99-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="bae99-105">在本文中，會向您介紹 **Power BI Embedded** 開始使用範例。</span><span class="sxs-lookup"><span data-stu-id="bae99-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="bae99-106">在我們繼續之前，您可能想要儲存下列資源。</span><span class="sxs-lookup"><span data-stu-id="bae99-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="bae99-107">它們會協助您將 Power BI 報告整合至範例應用程式和您自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bae99-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="bae99-108">範例工作區 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="bae99-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="bae99-109">Power BI Embedded API 參考</span><span class="sxs-lookup"><span data-stu-id="bae99-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="bae99-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (透過 NuGet 提供)</span><span class="sxs-lookup"><span data-stu-id="bae99-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="bae99-111">JavaScript 報告內嵌範例</span><span class="sxs-lookup"><span data-stu-id="bae99-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="bae99-112">在您可以設定及執行 Power BI Embedded 開始使用範例之前，您需要在您的 Azure 訂用帳戶中至少建立一個「工作區集合」。</span><span class="sxs-lookup"><span data-stu-id="bae99-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="bae99-113">若要了解如何在 Azure 入口網站中建立**工作區集合**，請參閱[開始使用 Power BI Embedded](power-bi-embedded-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="bae99-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="bae99-114">設定範例應用程式</span><span class="sxs-lookup"><span data-stu-id="bae99-114">Configure the sample app</span></span>

<span data-ttu-id="bae99-115">讓我們逐步引導您設定 Visual Studio 開發環境，以存取執行範例應用程式時所需的元件。</span><span class="sxs-lookup"><span data-stu-id="bae99-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="bae99-116">下載並解壓縮 GitHub 上的 [Power BI Embedded - 將報表整合到 Web 應用程式中](http://go.microsoft.com/fwlink/?LinkId=761493) 範例。</span><span class="sxs-lookup"><span data-stu-id="bae99-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="bae99-117">在 Visual Studio 中開啟 **PowerBI-embedded.sln** 。</span><span class="sxs-lookup"><span data-stu-id="bae99-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="bae99-118">您可能需要執行 NuGET 套件管理器主控台中的 **Update-Package** 以更新此方案中使用的套件。</span><span class="sxs-lookup"><span data-stu-id="bae99-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="bae99-119">建置方案。</span><span class="sxs-lookup"><span data-stu-id="bae99-119">Build the solution.</span></span>
4. <span data-ttu-id="bae99-120">執行 **ProvisionSample** 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="bae99-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="bae99-121">您可以在範例主控台應用程式中，佈建工作區並匯入 PBIX 檔案。</span><span class="sxs-lookup"><span data-stu-id="bae99-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="bae99-122">若要佈建新的**工作區**，請選取選項 1 [集合管理]，然後選取選項 6 [佈建新的工作區]。</span><span class="sxs-lookup"><span data-stu-id="bae99-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="bae99-123">若要匯入新的**報告**，請選取選項 2 [報告管理]，然後選取選項 3 [將 PBIX 桌面檔案匯入工作區]。</span><span class="sxs-lookup"><span data-stu-id="bae99-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="bae99-124">輸入您的 [工作區集合] 名稱，以及 [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="bae99-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="bae99-125">您可以在「Azure 入口網站」 中取得這些項目。</span><span class="sxs-lookup"><span data-stu-id="bae99-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="bae99-126">若要深入了解如何取得存取金鑰 ，請參閱＜開始使用 Microsoft Power BI Embedded＞中的 [檢視 Power BI API 存取金鑰](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) 。</span><span class="sxs-lookup"><span data-stu-id="bae99-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="bae99-127">複製並儲存新建立的「工作區識別碼」  ，以供稍後在此文章中使用。</span><span class="sxs-lookup"><span data-stu-id="bae99-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="bae99-128">「工作區識別碼」建立之後，您就可以在「Azure 入口網站」中找到它。</span><span class="sxs-lookup"><span data-stu-id="bae99-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="bae99-129">若要將 PBIX 檔案匯入到您的**工作區**，請選取選項 **6。**\[將 PBIX Desktop 檔案匯入現有的工作區\]。</span><span class="sxs-lookup"><span data-stu-id="bae99-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="bae99-130">如果您現在沒有 PBIX 檔案，可以下載[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)。</span><span class="sxs-lookup"><span data-stu-id="bae99-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="bae99-131">如果出現提示，請輸入易記名稱做為您「資料集」 的名稱。</span><span class="sxs-lookup"><span data-stu-id="bae99-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="bae99-132">您應該會看到像這樣的回應：</span><span class="sxs-lookup"><span data-stu-id="bae99-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="bae99-133">如果您的 PBIX 檔案包含任何直接查詢連接，請執行選項 7 來更新連接字串。</span><span class="sxs-lookup"><span data-stu-id="bae99-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="bae99-134">此時，您已經將 Power BI PBIX 報表匯入到您的**工作區**。</span><span class="sxs-lookup"><span data-stu-id="bae99-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="bae99-135">現在我們看一下如何執行 **Power BI Embedded** 開始使用範例 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bae99-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="bae99-136">執行範例 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="bae99-136">Run the sample web app</span></span>
<span data-ttu-id="bae99-137">Web 應用程式範例是一個範例應用程式，會轉譯匯入到您**工作區**的報表。</span><span class="sxs-lookup"><span data-stu-id="bae99-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="bae99-138">以下說明如何設定 Web 應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="bae99-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="bae99-139">在 **PowerBI-embedded** Visual Studio 解決方案中，用滑鼠右鍵按一下 [EmbedSample] Web 應用程式，然後選擇 [設定為啟始專案]。</span><span class="sxs-lookup"><span data-stu-id="bae99-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="bae99-140">在 **web.config** 中，於 **EmbedSample** Web 應用程式中編輯 **appSettings**：**AccessKey**、**WorkspaceCollection** 名稱，及 **WorkspaceId**。</span><span class="sxs-lookup"><span data-stu-id="bae99-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="bae99-141">執行 **EmbedSample** Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bae99-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="bae99-142">在您執行 **EmbedSample** Web 應用程式之後，左邊瀏覽窗格應該就會包含一個 [多個報表] 功能表。</span><span class="sxs-lookup"><span data-stu-id="bae99-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="bae99-143">若要檢視您匯入的報表，請展開 [多個報表]，然後按一下報表。</span><span class="sxs-lookup"><span data-stu-id="bae99-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="bae99-144">如果您匯入了[零售分析範例 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)，範例 Web 應用程式看起來就會像這樣：</span><span class="sxs-lookup"><span data-stu-id="bae99-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="bae99-145">在您按一下報表之後，**EmbedSample** Web 應用程式應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="bae99-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="bae99-146">探討範例程式碼</span><span class="sxs-lookup"><span data-stu-id="bae99-146">Explore the sample code</span></span>

<span data-ttu-id="bae99-147">**Microsoft Power BI Embedded** 範例是向您示範如何將 **Power BI** 報告整合到您應用程式中的範例 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bae99-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="bae99-148">它會使用「模型-檢視-控制器」(MVC) 設計樣式來示範最佳作法。</span><span class="sxs-lookup"><span data-stu-id="bae99-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="bae99-149">本節重點在於 **PowerBI-embedded** Web 應用程式方案中您可以探討的部分範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="bae99-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="bae99-150">「模型-檢視-控制器」(MVC) 樣式會依據使用者在三種個別類型中的輸入來分隔網域、簡報及動作的模型製作：模型、檢視及控制器。</span><span class="sxs-lookup"><span data-stu-id="bae99-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="bae99-151">若要詳細了解 MVC，請參閱[了解 ASP.NET](http://www.asp.net/mvc)。</span><span class="sxs-lookup"><span data-stu-id="bae99-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="bae99-152">**Microsoft Power BI Embedded** 範例程式碼的各部分如下。</span><span class="sxs-lookup"><span data-stu-id="bae99-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="bae99-153">每個區段都包含 PowerBI-embedded.sln 解決方案中的檔案名稱，因此您可以很容易地在範例中找到程式碼。</span><span class="sxs-lookup"><span data-stu-id="bae99-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="bae99-154">本節是示範程式碼撰寫方式之範例程式碼的摘要。</span><span class="sxs-lookup"><span data-stu-id="bae99-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="bae99-155">若要檢視完整範例，請在 Visual Studio 中載入 PowerBI-embedded.sln 解決方案。</span><span class="sxs-lookup"><span data-stu-id="bae99-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="bae99-156">模型</span><span class="sxs-lookup"><span data-stu-id="bae99-156">Model</span></span>

<span data-ttu-id="bae99-157">範例有 **ReportsViewModel** 和 **ReportViewModel**。</span><span class="sxs-lookup"><span data-stu-id="bae99-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="bae99-158">**ReportsViewModel.cs**：代表 Power BI Reports。</span><span class="sxs-lookup"><span data-stu-id="bae99-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="bae99-159">**ReportViewModel.cs**：代表 Power BI Report。</span><span class="sxs-lookup"><span data-stu-id="bae99-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="bae99-160">連接字串</span><span class="sxs-lookup"><span data-stu-id="bae99-160">Connection string</span></span>

<span data-ttu-id="bae99-161">連接字串必須為下列格式：</span><span class="sxs-lookup"><span data-stu-id="bae99-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="bae99-162">使用一般伺服器和資料庫屬性將會失敗。</span><span class="sxs-lookup"><span data-stu-id="bae99-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="bae99-163">例如：Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="bae99-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="bae99-164">檢視</span><span class="sxs-lookup"><span data-stu-id="bae99-164">View</span></span>

<span data-ttu-id="bae99-165">**檢視**可管理 Power BI **Reports** 和 **Power BI Report** 的顯示。</span><span class="sxs-lookup"><span data-stu-id="bae99-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="bae99-166">**Reports.cshtml**：反覆執行 **Model.Reports** 來建立 **ActionLink**。</span><span class="sxs-lookup"><span data-stu-id="bae99-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="bae99-167">**ActionLink** 是由以下項目組成：</span><span class="sxs-lookup"><span data-stu-id="bae99-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="bae99-168">部分</span><span class="sxs-lookup"><span data-stu-id="bae99-168">Part</span></span> | <span data-ttu-id="bae99-169">說明</span><span class="sxs-lookup"><span data-stu-id="bae99-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bae99-170">Title</span><span class="sxs-lookup"><span data-stu-id="bae99-170">Title</span></span> |<span data-ttu-id="bae99-171">報表名稱。</span><span class="sxs-lookup"><span data-stu-id="bae99-171">Name of the Report.</span></span> |
| <span data-ttu-id="bae99-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="bae99-172">QueryString</span></span> |<span data-ttu-id="bae99-173">報表識別碼的連結。</span><span class="sxs-lookup"><span data-stu-id="bae99-173">A link to the Report ID.</span></span> |

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

<span data-ttu-id="bae99-174">Report.cshtml：設定 **Model.AccessToken**，以及 **PowerBIReportFor** 的 Lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="bae99-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="bae99-175">Controller</span><span class="sxs-lookup"><span data-stu-id="bae99-175">Controller</span></span>

<span data-ttu-id="bae99-176">**DashboardController.cs**：建立會傳遞**應用程式權杖**的 PowerBIClient。</span><span class="sxs-lookup"><span data-stu-id="bae99-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="bae99-177">JSON Web 權杖 (JWT) 是從**簽署金鑰**產生，可用於取得**認證**。</span><span class="sxs-lookup"><span data-stu-id="bae99-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="bae99-178">**Credentials** 是用來建立 **PowerBIClient** 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="bae99-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="bae99-179">在您擁有 **PowerBIClient** 的執行個體之後，您就可以呼叫 GetReports() 與 GetReportsAsync()。</span><span class="sxs-lookup"><span data-stu-id="bae99-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="bae99-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="bae99-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="bae99-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="bae99-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="bae99-182">Task<ActionResult> Report(string reportId)</span><span class="sxs-lookup"><span data-stu-id="bae99-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="bae99-183">將報表整合到您的應用程式中</span><span class="sxs-lookup"><span data-stu-id="bae99-183">Integrate a report into your app</span></span>

<span data-ttu-id="bae99-184">在您擁有 **Report** 之後，您就可以使用 **IFrame** 來內嵌 Power BI **Report**。</span><span class="sxs-lookup"><span data-stu-id="bae99-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="bae99-185">以下是來自 **Microsoft Power BI Embedded** 範例中 powerbi.js 的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="bae99-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="bae99-186">篩選內嵌在應用程式中的報表</span><span class="sxs-lookup"><span data-stu-id="bae99-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="bae99-187">您可以使用 URL 語法，篩選內嵌的報表。</span><span class="sxs-lookup"><span data-stu-id="bae99-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="bae99-188">若要這樣做，請將含有 **eq** 運算子的 **$filter** 查詢字串參數新增到含指定篩選的 iFrame src URL。</span><span class="sxs-lookup"><span data-stu-id="bae99-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="bae99-189">以下是篩選的查詢語法︰</span><span class="sxs-lookup"><span data-stu-id="bae99-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="bae99-190">{表格名稱/欄位名稱} 不能包含空格或特殊字元。</span><span class="sxs-lookup"><span data-stu-id="bae99-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="bae99-191">{欄位值} 接受單一類別目錄值。</span><span class="sxs-lookup"><span data-stu-id="bae99-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="bae99-192">另請參閱</span><span class="sxs-lookup"><span data-stu-id="bae99-192">See also</span></span>

[<span data-ttu-id="bae99-193">Microsoft Power BI Embedded 常見案例</span><span class="sxs-lookup"><span data-stu-id="bae99-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="bae99-194">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="bae99-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="bae99-195">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="bae99-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="bae99-196">從資料集建立新的報告</span><span class="sxs-lookup"><span data-stu-id="bae99-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="bae99-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="bae99-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="bae99-198">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="bae99-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="bae99-199">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="bae99-199">More questions?</span></span> [<span data-ttu-id="bae99-200">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="bae99-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
