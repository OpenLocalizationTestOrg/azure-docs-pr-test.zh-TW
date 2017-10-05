---
title: "適用於 Azure 串流分析的管理 .NET SDK | Microsoft Docs"
description: "Azure 串流分析管理 .NET SDK 入門。 了解如何設定及執行分析作業。 建立專案、輸入、輸出及轉換。"
keywords: ".net SDK, 分析 API"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: f9aa812e6e82cc0f72d0cd1fe63058e53f794775
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="7026f-106">管理 .NET SDK：透過適用於 .NET 的 Azure 串流分析 API 來設定及執行分析工作</span><span class="sxs-lookup"><span data-stu-id="7026f-106">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="7026f-107">了解如何使用管理 .NET SDK，透過適用於 .NET 的串流分析 API 來設定及執行分析作業。</span><span class="sxs-lookup"><span data-stu-id="7026f-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="7026f-108">設定專案，建立輸入與輸出來源、轉換，以及開始和停止工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="7026f-109">對於您的分析工作，您可以從 Blob 儲存體或從事件中樞串流資料。</span><span class="sxs-lookup"><span data-stu-id="7026f-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="7026f-110">請參閱 [適用於 .NET 的串流分析 API 之管理參考文件](https://msdn.microsoft.com/library/azure/dn889315.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7026f-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="7026f-111">Azure 資料流分析是完全受管理的服務，可用來對雲端中的串流資料進行低延遲、高可用性、可延展的複雜事件處理。</span><span class="sxs-lookup"><span data-stu-id="7026f-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="7026f-112">串流分析可讓客戶設定串流工作以分析資料流，並可讓客戶以接近即時的方式進行分析。</span><span class="sxs-lookup"><span data-stu-id="7026f-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="7026f-113">我們已將本文中的範例程式碼更新為 Azure 串流分析管理 .NET SDK v2.x 版本。</span><span class="sxs-lookup"><span data-stu-id="7026f-113">We have updated the sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="7026f-114">如需查看使用舊版 (1.x) SDK 的範例程式碼，請參閱[使用適用於串流分析的管理 .NET SDK v1.x](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1)。</span><span class="sxs-lookup"><span data-stu-id="7026f-114">For sample code using the uses lagecy (1.x) SDK version, please see [Use the Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7026f-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="7026f-115">Prerequisites</span></span>
<span data-ttu-id="7026f-116">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="7026f-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="7026f-117">安裝 Visual Studio 2017 或 2015。</span><span class="sxs-lookup"><span data-stu-id="7026f-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="7026f-118">下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="7026f-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="7026f-119">在您的訂用帳戶中建立「Azure 資源群組」。</span><span class="sxs-lookup"><span data-stu-id="7026f-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="7026f-120">下列是 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="7026f-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="7026f-121">如需 Azure PowerShell 資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7026f-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="7026f-122">設定要使用的輸入來源和輸出目標。</span><span class="sxs-lookup"><span data-stu-id="7026f-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="7026f-123">如需進一步的指示，請參閱[新增輸入](stream-analytics-add-inputs.md)來設定範例輸入，以及[新增輸出](stream-analytics-add-outputs.md)來設定範例輸出。</span><span class="sxs-lookup"><span data-stu-id="7026f-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="7026f-124">設定專案</span><span class="sxs-lookup"><span data-stu-id="7026f-124">Set up a project</span></span>
<span data-ttu-id="7026f-125">您必須先設定自己的專案，才能透過適用於 .NET 的串流分析 API 來建立分析工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="7026f-126">建立 Visual Studio C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="7026f-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="7026f-127">在 Package Manager Console 中，執行下列命令以安裝 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="7026f-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="7026f-128">第一個是 Azure 串流分析管理 .NET SDK。</span><span class="sxs-lookup"><span data-stu-id="7026f-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="7026f-129">第二個用於 Azure 用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="7026f-129">The second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="7026f-130">將下列 **appSettings** 區段加入 App.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="7026f-130">Add the following **appSettings** section to the App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="7026f-131">以您的 Azure 訂用帳戶 ID 和租用戶識別碼取代 **SubscriptionId** 和 **ActiveDirectoryTenantId** 的值。</span><span class="sxs-lookup"><span data-stu-id="7026f-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="7026f-132">您可以藉由執行下列 Azure PowerShell Cmdlet 來取得這些值：</span><span class="sxs-lookup"><span data-stu-id="7026f-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="7026f-133">在您的 .csproj 檔案中新增下列參考：</span><span class="sxs-lookup"><span data-stu-id="7026f-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="7026f-134">將下列 **using** 陳述式加入專案的原始程式檔 (Program.cs) 中。</span><span class="sxs-lookup"><span data-stu-id="7026f-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="7026f-135">新增驗證協助程式方法：</span><span class="sxs-lookup"><span data-stu-id="7026f-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="7026f-136">建立資料流分析管理用戶端</span><span class="sxs-lookup"><span data-stu-id="7026f-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="7026f-137">**StreamAnalyticsManagementClient** 物件可讓您管理工作和工作元件，例如輸入、輸出和轉換。</span><span class="sxs-lookup"><span data-stu-id="7026f-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="7026f-138">在 **Main** 方法的開頭加入下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="7026f-138">Add the following code to the beginning of the **Main** method:</span></span>

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

<span data-ttu-id="7026f-139">**resourceGroupName** 變數的值應該會與您在先決條件步驟中建立或選取的資源群組名稱相同。</span><span class="sxs-lookup"><span data-stu-id="7026f-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="7026f-140">若要自動化作業建立的認證提供層面，請參閱 [使用 Azure 資源管理員驗證服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="7026f-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="7026f-141">本文的其餘章節會假設 **Main** 方法的開頭已有這段程式碼。</span><span class="sxs-lookup"><span data-stu-id="7026f-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="7026f-142">建立串流分析作業</span><span class="sxs-lookup"><span data-stu-id="7026f-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="7026f-143">下列程式碼會在您已定義的資源群組下方建立一個串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="7026f-144">您稍後可以在工作中加入輸入、輸出和轉換。</span><span class="sxs-lookup"><span data-stu-id="7026f-144">You will add an input, output, and transformation to the job later.</span></span>

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="7026f-145">建立資料流分析輸入來源</span><span class="sxs-lookup"><span data-stu-id="7026f-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="7026f-146">下列程式碼會使用 Blob 輸入來源類型和 CSV 序列化，來建立資料流分析輸入來源。</span><span class="sxs-lookup"><span data-stu-id="7026f-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="7026f-147">若要建立事件中心輸入來源，請使用 **EventHubStreamInputDataSource**，而不是 **BlobStreamInputDataSource**。</span><span class="sxs-lookup"><span data-stu-id="7026f-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="7026f-148">同樣地，您可以自訂輸入來源的序列化類型。</span><span class="sxs-lookup"><span data-stu-id="7026f-148">Similarly, you can customize the serialization type of the input source.</span></span>

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

<span data-ttu-id="7026f-149">輸入來源 (來自 Blob 儲存體或事件中樞) 受限於特定工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="7026f-150">若要在不同的工作中使用相同的輸入來源，您必須重新呼叫此方法，並指定不同的工作名稱。</span><span class="sxs-lookup"><span data-stu-id="7026f-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="7026f-151">測試資料流分析輸入來源</span><span class="sxs-lookup"><span data-stu-id="7026f-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="7026f-152">**TestConnection** 方法可測試資料流分析作業是否能夠連接到輸入來源，以及測試輸入來源類型特定的其他層面。</span><span class="sxs-lookup"><span data-stu-id="7026f-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="7026f-153">例如，在您在先前步驟中建立的 Blob 輸入來源中，此方法會檢查可用來連接到儲存體帳戶的儲存體帳戶名稱和金鑰組，以及檢查指定的容器是否存在。</span><span class="sxs-lookup"><span data-stu-id="7026f-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

   ```
   // Test the connection to the input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="7026f-154">建立資料流分析輸出目標</span><span class="sxs-lookup"><span data-stu-id="7026f-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="7026f-155">建立輸出目標與建立資料流分析輸入來源非常類似。</span><span class="sxs-lookup"><span data-stu-id="7026f-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="7026f-156">和輸入來源一樣，輸出目標會繫結至特定工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="7026f-157">若要在不同的工作中使用相同的輸出目標，您必須重新呼叫此方法，並指定不同的工作名稱。</span><span class="sxs-lookup"><span data-stu-id="7026f-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="7026f-158">下列程式碼會建立輸出目標 (Azure SQL Database)。</span><span class="sxs-lookup"><span data-stu-id="7026f-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="7026f-159">您可以自訂輸出目標的資料類型和/或序列化類型。</span><span class="sxs-lookup"><span data-stu-id="7026f-159">You can customize the output target's data type and/or serialization type.</span></span>

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="7026f-160">測試資料流分析輸出目標</span><span class="sxs-lookup"><span data-stu-id="7026f-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="7026f-161">資料流分析輸出目標也有可測試連線的 **TestConnection** 方法。</span><span class="sxs-lookup"><span data-stu-id="7026f-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

   ```
   // Test the connection to the output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="7026f-162">建立資料流分析轉換</span><span class="sxs-lookup"><span data-stu-id="7026f-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="7026f-163">下列程式碼會使用 "select * from Input" 查詢來建立串流分析轉換，並指定為串流分析工作配置一個串流單位。</span><span class="sxs-lookup"><span data-stu-id="7026f-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="7026f-164">如需有關如何調整資料流單位的詳細資訊，請參閱 [調整 Azure 資料流分析工作](stream-analytics-scale-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="7026f-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with the value you put for the 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="7026f-165">如同輸入和輸出，轉換也繫結至建立該轉換時所在的特定串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="7026f-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="7026f-166">啟動資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="7026f-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="7026f-167">建立資料流分析工作及其輸入、輸出和轉換之後，您可以藉由呼叫 **Start** 方法來啟動工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="7026f-168">下列範例程式碼會啟動自訂輸出開始時間設為 2012 年 12 月 12 日 12:12:12 UTC 的資料流分析工作：</span><span class="sxs-lookup"><span data-stu-id="7026f-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="7026f-169">停止資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="7026f-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="7026f-170">您可以藉由呼叫 **Stop** 方法來停止執行中的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="7026f-171">刪除資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="7026f-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="7026f-172">**Delete** 方法將會刪除作業及其基礎子資源，包括輸入、輸出，以及轉換工作。</span><span class="sxs-lookup"><span data-stu-id="7026f-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="7026f-173">取得支援</span><span class="sxs-lookup"><span data-stu-id="7026f-173">Get support</span></span>
<span data-ttu-id="7026f-174">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="7026f-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7026f-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7026f-175">Next steps</span></span>
<span data-ttu-id="7026f-176">您已經學到使用 .NET SDK 建立及執行分析作業的基本知識。</span><span class="sxs-lookup"><span data-stu-id="7026f-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="7026f-177">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="7026f-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="7026f-178">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="7026f-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7026f-179">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="7026f-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="7026f-180">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="7026f-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="7026f-181">[Azure 串流分析管理 .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7026f-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="7026f-182">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="7026f-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7026f-183">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="7026f-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
