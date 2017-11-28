---
title: "在 Stream Analytics aaaProgrammatically 監控工作 |Microsoft 文件"
description: "了解如何 tooprogrammatically 監視透過 REST Api、 Azure SDK 或 PowerShell 建立串流分析工作。"
keywords: ".net 監視, 工作監視, 監視應用程式"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="033d0-104">以程式設計方式來建立串流分析工作監視</span><span class="sxs-lookup"><span data-stu-id="033d0-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="033d0-105">本文示範如何 tooenable 監視的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="033d0-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="033d0-106">透過 REST API、Azure SDK 或 PowerShell 建立的串流分析作業預設不會啟用監視。</span><span class="sxs-lookup"><span data-stu-id="033d0-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="033d0-107">您可以手動方式啟用它 hello Azure 入口網站中移 toohello 工作監視頁面和按一下 hello 啟用按鈕，或您可以遵循本文章中的 hello 步驟自動化此程序。</span><span class="sxs-lookup"><span data-stu-id="033d0-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="033d0-108">hello 度量區域中的 hello 串流分析工作的 Azure 入口網站會顯示 hello 監視資料。</span><span class="sxs-lookup"><span data-stu-id="033d0-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="033d0-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="033d0-109">Prerequisites</span></span>

<span data-ttu-id="033d0-110">在開始此程序之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="033d0-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="033d0-111">Visual Studio 2017 或 2015</span><span class="sxs-lookup"><span data-stu-id="033d0-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="033d0-112">已下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="033d0-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="033d0-113">現有的資料流分析作業需要啟用 toohave 監視</span><span class="sxs-lookup"><span data-stu-id="033d0-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="033d0-114">建立專案</span><span class="sxs-lookup"><span data-stu-id="033d0-114">Create a project</span></span>

1. <span data-ttu-id="033d0-115">建立 Visual Studio C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="033d0-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="033d0-116">Hello Package Manager Console 中，執行的 hello 下列命令，tooinstall hello NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="033d0-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="033d0-117">hello 第一次是 hello Azure Stream Analytics Management.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="033d0-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="033d0-118">hello 第二個是 hello 將使用的 Azure 監視 SDK tooenable 監視。</span><span class="sxs-lookup"><span data-stu-id="033d0-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="033d0-119">hello 最後一個是 hello Azure Active Directory 用戶端將用來驗證。</span><span class="sxs-lookup"><span data-stu-id="033d0-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="033d0-120">新增下列 appSettings 區段 toohello App.config 檔的 hello。</span><span class="sxs-lookup"><span data-stu-id="033d0-120">Add hello following appSettings section toohello App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="033d0-121">以您的 Azure 訂用帳戶 ID 和租用戶識別碼取代 *SubscriptionId* 和 *ActiveDirectoryTenantId* 的值。</span><span class="sxs-lookup"><span data-stu-id="033d0-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="033d0-122">您可以藉由執行下列 PowerShell cmdlet 的 hello 取得這些值：</span><span class="sxs-lookup"><span data-stu-id="033d0-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="033d0-123">新增 hello 下列使用陳述式 toohello 來源檔案 (Program.cs) hello 專案中的。</span><span class="sxs-lookup"><span data-stu-id="033d0-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="033d0-124">新增驗證協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="033d0-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="033d0-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="033d0-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="033d0-126">}</span><span class="sxs-lookup"><span data-stu-id="033d0-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="033d0-127">建立管理用戶端</span><span class="sxs-lookup"><span data-stu-id="033d0-127">Create management clients</span></span>

<span data-ttu-id="033d0-128">hello 下列程式碼會設定 hello 必要變數和管理用戶端。</span><span class="sxs-lookup"><span data-stu-id="033d0-128">hello following code will set up hello necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="033d0-129">為現有串流分析作業啟用監視</span><span class="sxs-lookup"><span data-stu-id="033d0-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="033d0-130">hello 下列程式碼啟用監視**現有**資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="033d0-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="033d0-131">hello hello 程式碼的第一個部分會執行對 hello hello 特定資料流分析工作的相關資料流分析服務 tooretrieve 資訊的 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="033d0-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="033d0-132">它會使用 hello*識別碼*hello hello 中的 Put 方法的參數屬性 （從 hello GET 要求擷取） 第二個部份 hello 程式碼，傳送 PUT 要求 toohello Insights 服務 tooenable 監視 hello 資料流分析作業。</span><span class="sxs-lookup"><span data-stu-id="033d0-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="033d0-133">如果您先前已啟用監視不同的資料流分析工作，透過 hello Azure 入口網站或以程式設計方式透過程式碼下, 面 hello**我們建議您提供 hello 時使用的相同儲存體帳戶名稱您先前已啟用監視。**</span><span class="sxs-lookup"><span data-stu-id="033d0-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="033d0-134">您在中，未特別 toohello 工作本身建立串流分析工作的連結的 toohello 區域 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="033d0-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="033d0-135">所有的資料流分析工作 （和所有其他 Azure 資源） 在該相同區域中共用這個儲存體帳戶 toostore 監視資料。</span><span class="sxs-lookup"><span data-stu-id="033d0-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="033d0-136">如果您提供不同的儲存體帳戶時，它可能會導致非預期的副作用 hello 監視其他的資料流分析工作或其他 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="033d0-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="033d0-137">hello 儲存體帳戶名稱，而您使用 tooreplace `<YOUR STORAGE ACCOUNT NAME>` hello 下列程式碼中應該是儲存體帳戶中 hello hello 資料流分析工作，您要啟用監視相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="033d0-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="033d0-138">取得支援</span><span class="sxs-lookup"><span data-stu-id="033d0-138">Get support</span></span>

<span data-ttu-id="033d0-139">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="033d0-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="033d0-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="033d0-140">Next steps</span></span>

* [<span data-ttu-id="033d0-141">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="033d0-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="033d0-142">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="033d0-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="033d0-143">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="033d0-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="033d0-144">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="033d0-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="033d0-145">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="033d0-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

