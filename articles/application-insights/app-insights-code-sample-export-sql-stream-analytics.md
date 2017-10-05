---
title: "從 Azure Application Insights 匯出至 SQL | Microsoft Docs"
description: "使用 Stream Analytics 持續將 Application Insights 資料匯出至 SQL。"
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="ddec1-103">逐步解說：使用串流分析從 Application Insights 匯出至 SQL</span><span class="sxs-lookup"><span data-stu-id="ddec1-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="ddec1-104">本文將說明如何使用[連續匯出][export]和 [Azure 串流分析](https://azure.microsoft.com/services/stream-analytics/)，將您的遙測資料從 [Azure Application Insights][start] 移入 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ddec1-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="ddec1-105">連續匯出會以 JSON 格式將遙測資料移入 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ddec1-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="ddec1-106">我們將使用 Azure 串流分析來剖析 JSON 物件，並在資料庫資料表中建立資料列。</span><span class="sxs-lookup"><span data-stu-id="ddec1-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="ddec1-107">(一般來說，「連續匯出」是對應用程式傳送至 Application Insights 的遙測資料自行進行分析的方式。</span><span class="sxs-lookup"><span data-stu-id="ddec1-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="ddec1-108">您可以調整這個程式碼範例，以使用匯出的遙測資料執行其他作業，例如彙總資料)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="ddec1-109">我們先假設您已經有想要監視的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddec1-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="ddec1-110">在此範例中，我們使用頁面檢視資料，但相同的模式可以很輕易地延伸到其他資料類型，例如自訂事件和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ddec1-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="ddec1-111">將 Application Insights 加入應用程式中</span><span class="sxs-lookup"><span data-stu-id="ddec1-111">Add Application Insights to your application</span></span>
<span data-ttu-id="ddec1-112">開始進行之前：</span><span class="sxs-lookup"><span data-stu-id="ddec1-112">To get started:</span></span>

1. <span data-ttu-id="ddec1-113">[為您的網頁設定 Application Insights](app-insights-javascript.md)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="ddec1-114">(在此範例中，我們將著重於處理來自用戶端瀏覽器的頁面檢視資料，但您也可以針對 [Java](app-insights-java-get-started.md) 或 [ASP.NET](app-insights-asp-net.md) 應用程式的伺服器端設定 Application Insights，並處理要求、相依性及其他伺服器遙測。)</span><span class="sxs-lookup"><span data-stu-id="ddec1-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="ddec1-115">發行應用程式，並觀察出現在 Application Insights 資源中的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="ddec1-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="ddec1-116">在 Azure 中建立儲存體</span><span class="sxs-lookup"><span data-stu-id="ddec1-116">Create storage in Azure</span></span>
<span data-ttu-id="ddec1-117">連續匯出一律會將資料輸出至 Azure 儲存體帳戶，因此您必須先建立儲存體。</span><span class="sxs-lookup"><span data-stu-id="ddec1-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="ddec1-118">在 [Azure 入口網站][portal]的訂用帳戶中建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddec1-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![在 Azure 入口網站中，依序選擇 [新增]、[資料]、[儲存體]。](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="ddec1-122">建立容器</span><span class="sxs-lookup"><span data-stu-id="ddec1-122">Create a container</span></span>
   
    ![在新的儲存體中，選取 [容器]，按一下容器磚，然後按一下 [新增]](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="ddec1-124">複製儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="ddec1-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="ddec1-125">稍後您會需要使用它來設定串流分析服務的輸入。</span><span class="sxs-lookup"><span data-stu-id="ddec1-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![在儲存體中，依序開啟 [設定]、[金鑰]，然後複製主要存取金鑰](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="ddec1-127">啟動對 Azure 儲存體的連續匯出</span><span class="sxs-lookup"><span data-stu-id="ddec1-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="ddec1-128">在 Azure 入口網站中，瀏覽至您為應用程式建立的 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="ddec1-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![依序選擇 [瀏覽]、[Application Insights]、您的應用程式](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="ddec1-130">建立連續匯出。</span><span class="sxs-lookup"><span data-stu-id="ddec1-130">Create a continuous export.</span></span>
   
    ![依序選擇 [設定]、[連續匯出]、[新增]](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="ddec1-132">選取您稍早建立的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="ddec1-132">Select the storage account you created earlier:</span></span>

    ![設定匯出目的地](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="ddec1-134">設定您想要查看的事件類型：</span><span class="sxs-lookup"><span data-stu-id="ddec1-134">Set the event types you want to see:</span></span>

    ![選擇事件類型](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="ddec1-136">可讓一些資料累積。</span><span class="sxs-lookup"><span data-stu-id="ddec1-136">Let some data accumulate.</span></span> <span data-ttu-id="ddec1-137">請休息一下，讓其他人使用您的應用程式一段時間。</span><span class="sxs-lookup"><span data-stu-id="ddec1-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="ddec1-138">遙測資料會送過來，而您會在[計量瀏覽器](app-insights-metrics-explorer.md)中看到統計圖表，並在[診斷搜尋](app-insights-diagnostic-search.md)中看到個別事件。</span><span class="sxs-lookup"><span data-stu-id="ddec1-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="ddec1-139">此外，資料會匯出至您的儲存體。</span><span class="sxs-lookup"><span data-stu-id="ddec1-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="ddec1-140">在入口網站 (選擇 [瀏覽]、選取您的儲存體帳戶，然後選取 [容器]) 或 Visual Studio 中，檢查匯出的資料。</span><span class="sxs-lookup"><span data-stu-id="ddec1-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="ddec1-141">在 Visual Studio 中，依序選擇 [檢視] 和 [Cloud Explorer]，然後依序開啟 [Azure] 和 [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="ddec1-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="ddec1-142">(如果您沒有此功能表選項，您需要安裝 Azure SDK：開啟 [新增專案] 對話方塊，然後開啟 [Visual C#] / [Cloud] / [取得 Microsoft Azure SDK for .NET]。)</span><span class="sxs-lookup"><span data-stu-id="ddec1-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![在 Visual Studio 中，依序開啟 [Server Browser]、[Azure]、[儲存體]](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="ddec1-144">記下衍生自應用程式名稱和檢測金鑰之路徑名稱的共同部分。</span><span class="sxs-lookup"><span data-stu-id="ddec1-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="ddec1-145">事件會以 JSON 格式寫入至 Blob 檔案。</span><span class="sxs-lookup"><span data-stu-id="ddec1-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="ddec1-146">每個檔案可能會包含一或多個事件。</span><span class="sxs-lookup"><span data-stu-id="ddec1-146">Each file may contain one or more events.</span></span> <span data-ttu-id="ddec1-147">因此我們想要讀取事件資料，並篩選出需要的欄位。</span><span class="sxs-lookup"><span data-stu-id="ddec1-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="ddec1-148">我們可以利用資料執行各種作業，但我們現在打算使用串流分析，將資料移至 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ddec1-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="ddec1-149">這麼做可讓您輕鬆執行許多有趣的查詢工作。</span><span class="sxs-lookup"><span data-stu-id="ddec1-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="ddec1-150">建立 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ddec1-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="ddec1-151">同樣地，請從您在 [Azure 入口網站][portal]中的訂用帳戶開始，建立您將寫入資料的資料庫 (和一部新伺服器，除非您已經有新伺服器)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![[新增]、[資料]、[SQL]](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="ddec1-153">確定資料庫伺服器允許存取 Azure 服務：</span><span class="sxs-lookup"><span data-stu-id="ddec1-153">Make sure that the database server allows access to Azure services:</span></span>

![[瀏覽]、[伺服器]、您的伺服器、[設定]、[防火牆]、[允許存取 Azure]](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="ddec1-155">在 Azure SQL Database 中建立資料表</span><span class="sxs-lookup"><span data-stu-id="ddec1-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="ddec1-156">使用您慣用的管理工具，連接到上一節所建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ddec1-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="ddec1-157">在本逐步解說中，我們將使用 [SQL Server 管理工具](https://msdn.microsoft.com/ms174173.aspx) (SSMS)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="ddec1-158">建立新的查詢，然後執行下列 T-SQL：</span><span class="sxs-lookup"><span data-stu-id="ddec1-158">Create a new query, and execute the following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="ddec1-159">在此範例中，我們會使用頁面檢視的資料。</span><span class="sxs-lookup"><span data-stu-id="ddec1-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="ddec1-160">若要查看其他可用的資料，請檢查您的 JSON 輸出，並查看 [匯出資料模型](app-insights-export-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="ddec1-161">建立 Azure 串流分析執行個體</span><span class="sxs-lookup"><span data-stu-id="ddec1-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="ddec1-162">在 [傳統 Azure 入口網站](https://manage.windowsazure.com/)中，選取 Azure 串流分析服務，然後建立新的串流分析工作：</span><span class="sxs-lookup"><span data-stu-id="ddec1-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="ddec1-163">建立新工作後，請展開其詳細資料：</span><span class="sxs-lookup"><span data-stu-id="ddec1-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="ddec1-164">設定 Blob 位置</span><span class="sxs-lookup"><span data-stu-id="ddec1-164">Set blob location</span></span>
<span data-ttu-id="ddec1-165">將此設定為從您的連續匯出 Blob 接收輸入：</span><span class="sxs-lookup"><span data-stu-id="ddec1-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="ddec1-166">現在您需要儲存體帳戶的主要存取金鑰 (您已在稍早記下此金鑰)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="ddec1-167">請將此金鑰設為儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ddec1-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="ddec1-168">設定路徑前置詞模式</span><span class="sxs-lookup"><span data-stu-id="ddec1-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="ddec1-169">請務必將 [日期格式] 設定為 [YYYY-MM-DD] \(含「虛線」)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="ddec1-170">[路徑前置詞模式] 會指定串流分析在儲存體中尋找輸入檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="ddec1-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="ddec1-171">您需要將它設定為與連續匯出儲存資料的方式相對應。</span><span class="sxs-lookup"><span data-stu-id="ddec1-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="ddec1-172">請設定如下：</span><span class="sxs-lookup"><span data-stu-id="ddec1-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="ddec1-173">在此範例中：</span><span class="sxs-lookup"><span data-stu-id="ddec1-173">In this example:</span></span>

* <span data-ttu-id="ddec1-174">`webapplication27` 是 Application Insights 資源名稱， **全部小寫**。</span><span class="sxs-lookup"><span data-stu-id="ddec1-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="ddec1-175">`1234...` 是 Application Insights 資源的檢測金鑰， **但移除了連字號**。</span><span class="sxs-lookup"><span data-stu-id="ddec1-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="ddec1-176">`PageViews` 是我們想要分析的資料類型。</span><span class="sxs-lookup"><span data-stu-id="ddec1-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="ddec1-177">可用的類型取決於您在「連續匯出」中設定的篩選。</span><span class="sxs-lookup"><span data-stu-id="ddec1-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="ddec1-178">檢查匯出的資料以查看其他可用的類型，並查看 [匯出資料模型](app-insights-export-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ddec1-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="ddec1-179">`/{date}/{time}` 是要依字面意思寫入資訊的格式。</span><span class="sxs-lookup"><span data-stu-id="ddec1-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="ddec1-180">若要取得 Application Insights 資源的名稱和 iKey，請在資源的概觀頁面中開啟 Essentials，或開啟 [設定]。</span><span class="sxs-lookup"><span data-stu-id="ddec1-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="ddec1-181">完成初始設定</span><span class="sxs-lookup"><span data-stu-id="ddec1-181">Finish initial setup</span></span>
<span data-ttu-id="ddec1-182">確認序列化格式：</span><span class="sxs-lookup"><span data-stu-id="ddec1-182">Confirm the serialization format:</span></span>

![確認並關閉精靈](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="ddec1-184">關閉精靈，並等候設定完成。</span><span class="sxs-lookup"><span data-stu-id="ddec1-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="ddec1-185">使用範例函數來檢查您是否已正確設定輸入路徑。</span><span class="sxs-lookup"><span data-stu-id="ddec1-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="ddec1-186">如果此方法失敗：請檢查儲存體中您所選擇的範例時間範圍的資料。</span><span class="sxs-lookup"><span data-stu-id="ddec1-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="ddec1-187">編輯輸入定義，並檢查您是否已正確設定儲存體帳戶、路徑前置詞和日期格式。</span><span class="sxs-lookup"><span data-stu-id="ddec1-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="ddec1-188">設定查詢</span><span class="sxs-lookup"><span data-stu-id="ddec1-188">Set query</span></span>
<span data-ttu-id="ddec1-189">開啟 [查詢] 區段：</span><span class="sxs-lookup"><span data-stu-id="ddec1-189">Open the query section:</span></span>

![在串流分析中選取 [查詢]](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="ddec1-191">將預設查詢替換為以下內容：</span><span class="sxs-lookup"><span data-stu-id="ddec1-191">Replace the default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="ddec1-192">請注意，前幾個屬性是頁面檢視資料的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="ddec1-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="ddec1-193">其他遙測資料類型的匯出會有不同的屬性。</span><span class="sxs-lookup"><span data-stu-id="ddec1-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="ddec1-194">請參閱 [屬性類型和值的詳細資料模型參考。](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="ddec1-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="ddec1-195">設定資料庫的輸出</span><span class="sxs-lookup"><span data-stu-id="ddec1-195">Set up output to database</span></span>
<span data-ttu-id="ddec1-196">選取 SQL 做為輸出。</span><span class="sxs-lookup"><span data-stu-id="ddec1-196">Select SQL as the output.</span></span>

![在串流分析中選取 [輸出]](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="ddec1-198">指定 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ddec1-198">Specify the SQL database.</span></span>

![填入資料庫的詳細資料](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="ddec1-200">關閉精靈，然後等待輸出設定完成的通知。</span><span class="sxs-lookup"><span data-stu-id="ddec1-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="ddec1-201">開始處理</span><span class="sxs-lookup"><span data-stu-id="ddec1-201">Start processing</span></span>
<span data-ttu-id="ddec1-202">從動作列啟動工作：</span><span class="sxs-lookup"><span data-stu-id="ddec1-202">Start the job from the action bar:</span></span>

![在串流分析中，按一下 [開始]](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="ddec1-204">您可以選擇是否要處理從現在開始的資料，或是從較早的資料開始處理。</span><span class="sxs-lookup"><span data-stu-id="ddec1-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="ddec1-205">如果您的「連續匯出」已經執行了一段時間，則後者會是很好用的選項。</span><span class="sxs-lookup"><span data-stu-id="ddec1-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![在串流分析中，按一下 [開始]](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="ddec1-207">經過數分鐘後，即可返回 SQL Server 管理工具，觀看資料的流入。</span><span class="sxs-lookup"><span data-stu-id="ddec1-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="ddec1-208">例如，使用如下查詢：</span><span class="sxs-lookup"><span data-stu-id="ddec1-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="ddec1-209">相關文章</span><span class="sxs-lookup"><span data-stu-id="ddec1-209">Related articles</span></span>
* [<span data-ttu-id="ddec1-210">使用串流分析匯出至 PowerBI</span><span class="sxs-lookup"><span data-stu-id="ddec1-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="ddec1-211">屬性類型和值的詳細資料模型參考。</span><span class="sxs-lookup"><span data-stu-id="ddec1-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="ddec1-212">Application Insights 中的連續匯出</span><span class="sxs-lookup"><span data-stu-id="ddec1-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="ddec1-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="ddec1-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

