---
title: "以程式設計方式監視串流分析的作業 | Microsoft Docs"
description: "了解如何以程式設計方式監視透過 REST API、Azure SDK 或 PowerShell 建立的串流分析作業。"
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
ms.openlocfilehash: 0d39e77316a03a705586af3ba970a7be1208ec85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="333ac-104">以程式設計方式來建立串流分析工作監視</span><span class="sxs-lookup"><span data-stu-id="333ac-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="333ac-105">本文示範如何為串流分析工作啟用監視。</span><span class="sxs-lookup"><span data-stu-id="333ac-105">This article demonstrates how to enable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="333ac-106">透過 REST API、Azure SDK 或 PowerShell 建立的串流分析作業預設不會啟用監視。</span><span class="sxs-lookup"><span data-stu-id="333ac-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="333ac-107">您可以在 Azure 入口網站中前往該作業的 [監視] 頁面，然後按一下 [啟用] 按鈕來手動啟用，或是按照本文中的步驟執行，將此程序自動化。</span><span class="sxs-lookup"><span data-stu-id="333ac-107">You can manually enable it in the Azure portal by going to the job’s Monitor page and clicking the Enable button or you can automate this process by following the steps in this article.</span></span> <span data-ttu-id="333ac-108">串流分析工作的監視資料將會顯示在 Azure 入口網站的 [計量] 區域中。</span><span class="sxs-lookup"><span data-stu-id="333ac-108">The monitoring data will show up in the Metrics area of the Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="333ac-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="333ac-109">Prerequisites</span></span>

<span data-ttu-id="333ac-110">開始此程序之前，您必須有下列項目：</span><span class="sxs-lookup"><span data-stu-id="333ac-110">Before you begin this process, you must have the following:</span></span>

* <span data-ttu-id="333ac-111">Visual Studio 2017 或 2015</span><span class="sxs-lookup"><span data-stu-id="333ac-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="333ac-112">已下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="333ac-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="333ac-113">一項已啟用監視的現有串流分析作業</span><span class="sxs-lookup"><span data-stu-id="333ac-113">An existing Stream Analytics job that needs to have monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="333ac-114">建立專案</span><span class="sxs-lookup"><span data-stu-id="333ac-114">Create a project</span></span>

1. <span data-ttu-id="333ac-115">建立 Visual Studio C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="333ac-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="333ac-116">在 Package Manager Console 中，執行下列命令以安裝 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="333ac-116">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="333ac-117">第一個是 Azure 串流分析管理 .NET SDK。</span><span class="sxs-lookup"><span data-stu-id="333ac-117">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="333ac-118">第二個是將用來啟用監視功能的 Azure 監視器 SDK。</span><span class="sxs-lookup"><span data-stu-id="333ac-118">The second one is the Azure Monitor SDK that will be used to enable monitoring.</span></span> <span data-ttu-id="333ac-119">最後一個是驗證要使用的 Azure Active Directory 用戶端。</span><span class="sxs-lookup"><span data-stu-id="333ac-119">The last one is the Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="333ac-120">將下列 appSettings 區段加入至 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="333ac-120">Add the following appSettings section to the App.config file.</span></span>
   
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
   <span data-ttu-id="333ac-121">以您的 Azure 訂用帳戶 ID 和租用戶識別碼取代 *SubscriptionId* 和 *ActiveDirectoryTenantId* 的值。</span><span class="sxs-lookup"><span data-stu-id="333ac-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="333ac-122">您可以藉由執行下列 PowerShell Cmdlet 來取得這些值：</span><span class="sxs-lookup"><span data-stu-id="333ac-122">You can get these values by running the following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="333ac-123">將下列 using 陳述式加入至專案的原始程式檔 (Program.cs) 中。</span><span class="sxs-lookup"><span data-stu-id="333ac-123">Add the following using statements to the source file (Program.cs) in the project.</span></span>
   
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
5. <span data-ttu-id="333ac-124">新增驗證協助程式方法。</span><span class="sxs-lookup"><span data-stu-id="333ac-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="333ac-125">public static string GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="333ac-125">public static string GetAuthorizationHeader()</span></span>
   
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
   
             throw new InvalidOperationException("Failed to acquire token");
     <span data-ttu-id="333ac-126">}</span><span class="sxs-lookup"><span data-stu-id="333ac-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="333ac-127">建立管理用戶端</span><span class="sxs-lookup"><span data-stu-id="333ac-127">Create management clients</span></span>

<span data-ttu-id="333ac-128">下列程式碼將設定必要的變數與管理用戶端。</span><span class="sxs-lookup"><span data-stu-id="333ac-128">The following code will set up the necessary variables and management clients.</span></span>

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="333ac-129">為現有串流分析作業啟用監視</span><span class="sxs-lookup"><span data-stu-id="333ac-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="333ac-130">下列程式碼將為「現有」 串流分析作業啟用監視。</span><span class="sxs-lookup"><span data-stu-id="333ac-130">The following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="333ac-131">程式碼的第一部分會對串流分析服務執行 GET 要求，以擷取特定串流分析工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="333ac-131">The first part of the code performs a GET request against the Stream Analytics service to retrieve information about the particular Stream Analytics job.</span></span> <span data-ttu-id="333ac-132">在程式碼的第二部分使用 *Id* 屬性 (擷取自 GET 要求) 當成 Put 方法的參數，將 PUT 要求傳送至 Insights 服務，來為串流分析作業啟用監視。</span><span class="sxs-lookup"><span data-stu-id="333ac-132">It uses the *Id* property (retrieved from the GET request) as a parameter for the Put method in the second half of the code, which sends a PUT request to the Insights service to enable monitoring for the Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="333ac-133">如果您先前已經為不同的串流分析作業啟用監視 (不論是透過 Azure 入口網站，還是以程式設計方式透過以下的程式碼)，**建議您提供先前啟用監視時所提供的相同儲存體帳戶名稱。**</span><span class="sxs-lookup"><span data-stu-id="333ac-133">If you have previously enabled monitoring for a different Stream Analytics job, either through the Azure portal or programmatically via the below code, **we recommend that you provide the same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="333ac-134">儲存體帳戶會連結到您建立串流分析作業所在的區域，而不是明確地連結到作業本身。</span><span class="sxs-lookup"><span data-stu-id="333ac-134">The storage account is linked to the region that you created your Stream Analytics job in, not specifically to the job itself.</span></span>
> 
> <span data-ttu-id="333ac-135">相同區域中的所有串流分析作業 (以及其他所有 Azure 資源) 都共用此儲存體帳戶儲存監視資料。</span><span class="sxs-lookup"><span data-stu-id="333ac-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account to store monitoring data.</span></span> <span data-ttu-id="333ac-136">如果您提供不同的儲存體帳戶，可能會對其他串流分析作業或其他 Azure 資源的監視產生非預期的副作用。</span><span class="sxs-lookup"><span data-stu-id="333ac-136">If you provide a different storage account, it might cause unintended side effects in the monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="333ac-137">用來取代下方程式碼中 `<YOUR STORAGE ACCOUNT NAME>` 的儲存體帳戶名稱應該是與您為其啟用監視功能的「串流分析」作業屬於相同訂用帳戶的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="333ac-137">The storage account name that you use to replace `<YOUR STORAGE ACCOUNT NAME>` in the following code should be a storage account that is in the same subscription as the Stream Analytics job that you are enabling monitoring for.</span></span>
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



## <a name="get-support"></a><span data-ttu-id="333ac-138">取得支援</span><span class="sxs-lookup"><span data-stu-id="333ac-138">Get support</span></span>

<span data-ttu-id="333ac-139">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="333ac-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="333ac-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="333ac-140">Next steps</span></span>

* [<span data-ttu-id="333ac-141">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="333ac-141">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="333ac-142">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="333ac-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="333ac-143">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="333ac-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="333ac-144">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="333ac-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="333ac-145">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="333ac-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

