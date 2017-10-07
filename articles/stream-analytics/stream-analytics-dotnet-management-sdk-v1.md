---
title: "Azure Stream Analytics 的 aaaManagement.NET SDK v1.x |Microsoft 文件"
description: "Azure 串流分析管理 .NET SDK 入門。 深入了解如何 tooset 及執行分析工作。 建立專案、輸入、輸出及轉換。"
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
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="3b72b-106">管理.NET SDK v1.x： 設定及執行的分析工作，會使用 hello 適用於.NET 的 Azure 資料流分析 API</span><span class="sxs-lookup"><span data-stu-id="3b72b-106">Management .NET SDK v1.x: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="3b72b-107">了解如何向上 tooset 和執行的分析工作，會使用資料流分析 API hello.NET 使用 hello 管理.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="3b72b-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="3b72b-108">設定專案，建立輸入與輸出來源、轉換，以及開始和停止工作。</span><span class="sxs-lookup"><span data-stu-id="3b72b-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="3b72b-109">對於您的分析工作，您可以從 Blob 儲存體或從事件中樞串流資料。</span><span class="sxs-lookup"><span data-stu-id="3b72b-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="3b72b-110">請參閱 hello[管理參考文件資料流分析 API hello.net](https://msdn.microsoft.com/library/azure/dn889315.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="3b72b-111">Azure Stream Analytics 是完全受管理的服務，透過 hello 雲端中的資料流提供低延遲、 高可用性、 可調整且複雜事件處理。</span><span class="sxs-lookup"><span data-stu-id="3b72b-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="3b72b-112">串流分析可讓客戶 tooset 安裝作業 tooanalyze 資料流，資料流，並讓他們 toodrive 接近即時的分析。</span><span class="sxs-lookup"><span data-stu-id="3b72b-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="3b72b-113">本文中的範例程式碼仍使用舊版 (1.x) 的 Azure 串流分析管理 .NET SDK。</span><span class="sxs-lookup"><span data-stu-id="3b72b-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="3b72b-114">範例程式碼使用 hello 最新的 SDK 版本，請參閱[使用 hello Stream Analytics Management.NET SDK](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-114">For sample code using hello up-to-date SDK version, please see [Use hello Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b72b-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="3b72b-115">Prerequisites</span></span>
<span data-ttu-id="3b72b-116">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="3b72b-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="3b72b-117">安裝 Visual Studio 2017 或 2015。</span><span class="sxs-lookup"><span data-stu-id="3b72b-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="3b72b-118">下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="3b72b-119">在您的訂用帳戶中建立「Azure 資源群組」。</span><span class="sxs-lookup"><span data-stu-id="3b72b-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="3b72b-120">hello 以下是範例 Azure PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="3b72b-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="3b72b-121">如需 Azure PowerShell 資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="3b72b-122">設定輸入來源，且輸出目標 toouse。</span><span class="sxs-lookup"><span data-stu-id="3b72b-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="3b72b-123">如進一步指示，請參閱[加入輸入](stream-analytics-add-inputs.md)tooset 向上範例輸入和[加入輸出](stream-analytics-add-outputs.md)tooset 組成的範例輸出。</span><span class="sxs-lookup"><span data-stu-id="3b72b-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="3b72b-124">設定專案</span><span class="sxs-lookup"><span data-stu-id="3b72b-124">Set up a project</span></span>
<span data-ttu-id="3b72b-125">toocreate 分析工作使用 hello 資料流分析 API 的.NET 中，第一次設定您的專案。</span><span class="sxs-lookup"><span data-stu-id="3b72b-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="3b72b-126">建立 Visual Studio C# .NET 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b72b-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="3b72b-127">Hello Package Manager Console 中，執行的 hello 下列命令，tooinstall hello NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="3b72b-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="3b72b-128">hello 第一次是 hello Azure Stream Analytics Management.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="3b72b-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="3b72b-129">hello 第二個是 hello Azure Active Directory 用戶端將用來驗證。</span><span class="sxs-lookup"><span data-stu-id="3b72b-129">hello second one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="3b72b-130">新增下列 hello **appSettings**節 toohello App.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="3b72b-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    <span data-ttu-id="3b72b-131">以您的 Azure 訂用帳戶 ID 和租用戶識別碼取代 **SubscriptionId** 和 **ActiveDirectoryTenantId** 的值。</span><span class="sxs-lookup"><span data-stu-id="3b72b-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="3b72b-132">您可以藉由執行下列 Azure PowerShell cmdlet 的 hello 取得這些值：</span><span class="sxs-lookup"><span data-stu-id="3b72b-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="3b72b-133">加入下列參考.csproj 檔案中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3b72b-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="3b72b-134">新增下列 hello**使用**陳述式 toohello 原始程式檔 (Program.cs) hello 專案中：</span><span class="sxs-lookup"><span data-stu-id="3b72b-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="3b72b-135">新增驗證協助程式方法：</span><span class="sxs-lookup"><span data-stu-id="3b72b-135">Add an authentication helper method:</span></span>

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="3b72b-136">建立資料流分析管理用戶端</span><span class="sxs-lookup"><span data-stu-id="3b72b-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="3b72b-137">A **StreamAnalyticsManagementClient**物件可讓您 toomanage hello 作業和 hello 的工作元件，例如輸入、 輸出和轉換。</span><span class="sxs-lookup"><span data-stu-id="3b72b-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="3b72b-138">新增下列程式碼 toohello 開頭 hello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="3b72b-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

<span data-ttu-id="3b72b-139">hello **resourceGroupName**變數的值應為您建立或 hello 先決條件步驟中挑選群組 hello hello 資源名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="3b72b-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="3b72b-140">tooautomate hello 認證簡報層面建立工作，請參閱太[驗證 Azure 資源管理員與服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="3b72b-141">hello 這篇文章的其餘章節假設此程式碼是在 hello hello 開頭**Main**方法。</span><span class="sxs-lookup"><span data-stu-id="3b72b-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="3b72b-142">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="3b72b-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="3b72b-143">hello 下列程式碼會建立在您已定義的 hello 資源群組下的資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="3b72b-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="3b72b-144">稍後您將加入的輸入、 輸出和轉換 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="3b72b-144">You will add an input, output, and transformation toohello job later.</span></span>

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="3b72b-145">建立資料流分析輸入來源</span><span class="sxs-lookup"><span data-stu-id="3b72b-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="3b72b-146">hello 下列程式碼會建立資料流分析的輸入的來源具有 hello blob 輸入的來源類型和 CSV 序列化。</span><span class="sxs-lookup"><span data-stu-id="3b72b-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="3b72b-147">toocreate 事件中樞輸入來源，使用**EventHubStreamInputDataSource**而不是**BlobStreamInputDataSource**。</span><span class="sxs-lookup"><span data-stu-id="3b72b-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="3b72b-148">同樣地，您可以自訂 hello 輸入來源的 hello 序列化類型。</span><span class="sxs-lookup"><span data-stu-id="3b72b-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

<span data-ttu-id="3b72b-149">輸入的來源，包括從 Blob 儲存體或事件中心，會繫結的 tooa 特定作業。</span><span class="sxs-lookup"><span data-stu-id="3b72b-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="3b72b-150">toouse hello 不同工作的相同輸入的來源，您必須再次呼叫 hello 方法並指定不同的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="3b72b-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="3b72b-151">測試資料流分析輸入來源</span><span class="sxs-lookup"><span data-stu-id="3b72b-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="3b72b-152">hello **TestConnection** hello 資料流分析工作是否能 tooconnect toohello 輸入來源，以及其他方面的特定 toohello 方法測試輸入來源類型。</span><span class="sxs-lookup"><span data-stu-id="3b72b-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="3b72b-153">例如，在 hello blob 輸入來源您在前述步驟中建立，hello 方法會檢查，hello 儲存體帳戶名稱和金鑰組可以是使用的 tooconnect toohello 儲存體帳戶，以及檢查該 hello 指定的容器存在。</span><span class="sxs-lookup"><span data-stu-id="3b72b-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="3b72b-154">建立資料流分析輸出目標</span><span class="sxs-lookup"><span data-stu-id="3b72b-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="3b72b-155">建立輸出目標是非常類似 toocreating 資料流分析的輸入來源。</span><span class="sxs-lookup"><span data-stu-id="3b72b-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="3b72b-156">輸入來源，例如輸出目標是繫結的 tooa 特定作業。</span><span class="sxs-lookup"><span data-stu-id="3b72b-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="3b72b-157">toouse hello 相同的輸出目標為不同的工作，您必須再次呼叫 hello 方法並指定不同的作業名稱。</span><span class="sxs-lookup"><span data-stu-id="3b72b-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="3b72b-158">下列程式碼的 hello 建立的輸出目標 (Azure SQL database)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="3b72b-159">您可以自訂 hello 輸出目標的資料類型及/或序列化的型別。</span><span class="sxs-lookup"><span data-stu-id="3b72b-159">You can customize hello output target's data type and/or serialization type.</span></span>

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="3b72b-160">測試資料流分析輸出目標</span><span class="sxs-lookup"><span data-stu-id="3b72b-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="3b72b-161">資料流分析輸出目標也有 hello **TestConnection**方法來測試連接。</span><span class="sxs-lookup"><span data-stu-id="3b72b-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="3b72b-162">建立資料流分析轉換</span><span class="sxs-lookup"><span data-stu-id="3b72b-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="3b72b-163">hello 下列程式碼會建立資料流分析轉換與 hello 查詢 」 選取 * 從輸入 」，並指定 tooallocate 一個資料流處理的單位 hello 資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="3b72b-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="3b72b-164">如需有關如何調整資料流單位的詳細資訊，請參閱 [調整 Azure 資料流分析工作](stream-analytics-scale-jobs.md)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

<span data-ttu-id="3b72b-165">輸入和輸出，例如轉換也是繫結的 toohello 底下建立特定資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="3b72b-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="3b72b-166">啟動資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="3b72b-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="3b72b-167">建立資料流分析工作的輸入、 輸出及轉換之後，您可以啟動 hello 作業呼叫 hello**啟動**方法。</span><span class="sxs-lookup"><span data-stu-id="3b72b-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="3b72b-168">下列範例程式碼的 hello 開頭自訂輸出開始時間組 tooDecember 12，2012，12:12:12 中的資料流分析工作 UTC:</span><span class="sxs-lookup"><span data-stu-id="3b72b-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="3b72b-169">停止資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="3b72b-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="3b72b-170">您可以停止執行中的資料流分析工作呼叫 hello**停止**方法。</span><span class="sxs-lookup"><span data-stu-id="3b72b-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="3b72b-171">刪除資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="3b72b-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="3b72b-172">hello**刪除**hello 作業，以及 hello 基礎子資源，包括輸入、 輸出，以及 hello 作業的轉換，將會刪除方法。</span><span class="sxs-lookup"><span data-stu-id="3b72b-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="3b72b-173">取得支援</span><span class="sxs-lookup"><span data-stu-id="3b72b-173">Get support</span></span>
<span data-ttu-id="3b72b-174">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b72b-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b72b-175">Next steps</span></span>
<span data-ttu-id="3b72b-176">您已了解使用.NET SDK toocreate hello 基本概念，並執行分析工作。</span><span class="sxs-lookup"><span data-stu-id="3b72b-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="3b72b-177">toolearn 詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="3b72b-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="3b72b-178">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="3b72b-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3b72b-179">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3b72b-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3b72b-180">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="3b72b-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="3b72b-181">[Azure 串流分析管理 .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3b72b-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="3b72b-182">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="3b72b-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3b72b-183">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="3b72b-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
