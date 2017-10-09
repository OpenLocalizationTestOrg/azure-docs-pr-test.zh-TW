---
title: "aaaManagement Azure Stream Analytics 的.NET SDK |Microsoft 文件"
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
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>管理.NET SDK： 設定及執行使用適用於.NET 的 hello Azure 資料流分析 API 的分析工作
了解如何向上 tooset 和執行的分析工作，會使用資料流分析 API hello.NET 使用 hello 管理.NET SDK。 設定專案，建立輸入與輸出來源、轉換，以及開始和停止工作。 對於您的分析工作，您可以從 Blob 儲存體或從事件中樞串流資料。

請參閱 hello[管理參考文件資料流分析 API hello.net](https://msdn.microsoft.com/library/azure/dn889315.aspx)。

Azure Stream Analytics 是完全受管理的服務，透過 hello 雲端中的資料流提供低延遲、 高可用性、 可調整且複雜事件處理。 串流分析可讓客戶 tooset 安裝作業 tooanalyze 資料流，資料流，並讓他們 toodrive 接近即時的分析。  

> [!NOTE]
> 我們已更新此文件中的 hello 範例程式碼與 Azure Stream Analytics Management.NET SDK v2.x 版本。 如範例程式碼使用 hello 使用 lagecy (1.x) SDK 版本，請參閱[hello 管理.NET SDK v1.x 用於資料流分析](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1)。

## <a name="prerequisites"></a>必要條件
在開始這份文件之前，您必須擁有 hello 下列：

* 安裝 Visual Studio 2017 或 2015。
* 下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)。
* 在您的訂用帳戶中建立「Azure 資源群組」。 hello 以下是範例 Azure PowerShell 指令碼。 如需 Azure PowerShell 資訊，請參閱 [安裝並設定 Azure PowerShell](/powershell/azure/overview)。  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* 設定輸入來源，且輸出目標 toouse。 如進一步指示，請參閱[加入輸入](stream-analytics-add-inputs.md)tooset 向上範例輸入和[加入輸出](stream-analytics-add-outputs.md)tooset 組成的範例輸出。

## <a name="set-up-a-project"></a>設定專案
toocreate 分析工作使用 hello 資料流分析 API 的.NET 中，第一次設定您的專案。

1. 建立 Visual Studio C# .NET 主控台應用程式。
2. Hello Package Manager Console 中，執行的 hello 下列命令，tooinstall hello NuGet 封裝。 hello 第一次是 hello Azure Stream Analytics Management.NET SDK。 hello 第二個是 Azure 用戶端驗證。
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. 新增下列 hello **appSettings**節 toohello App.config 檔案：
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    以您的 Azure 訂用帳戶 ID 和租用戶識別碼取代 **SubscriptionId** 和 **ActiveDirectoryTenantId** 的值。 您可以藉由執行下列 Azure PowerShell cmdlet 的 hello 取得這些值：

        Get-AzureAccount

4. 加入下列參考.csproj 檔案中的 hello:

        <Reference Include="System.Configuration" />

5. 新增下列 hello**使用**陳述式 toohello 原始程式檔 (Program.cs) hello 專案中：
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. 新增驗證協助程式方法：

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a>建立資料流分析管理用戶端
A **StreamAnalyticsManagementClient**物件可讓您 toomanage hello 作業和 hello 的工作元件，例如輸入、 輸出和轉換。

新增下列程式碼 toohello 開頭 hello hello **Main**方法：

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

hello **resourceGroupName**變數的值應為您建立或 hello 先決條件步驟中挑選群組 hello hello 資源名稱相同的 hello。

tooautomate hello 認證簡報層面建立工作，請參閱太[驗證 Azure 資源管理員與服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)。

hello 這篇文章的其餘章節假設此程式碼是在 hello hello 開頭**Main**方法。

## <a name="create-a-stream-analytics-job"></a>建立串流分析工作
hello 下列程式碼會建立在您已定義的 hello 資源群組下的資料流分析工作。 稍後您將加入的輸入、 輸出和轉換 toohello 作業。

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

## <a name="create-a-stream-analytics-input-source"></a>建立資料流分析輸入來源
hello 下列程式碼會建立資料流分析的輸入的來源具有 hello blob 輸入的來源類型和 CSV 序列化。 toocreate 事件中樞輸入來源，使用**EventHubStreamInputDataSource**而不是**BlobStreamInputDataSource**。 同樣地，您可以自訂 hello 輸入來源的 hello 序列化類型。

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

輸入的來源，包括從 Blob 儲存體或事件中心，會繫結的 tooa 特定作業。 toouse hello 不同工作的相同輸入的來源，您必須再次呼叫 hello 方法並指定不同的作業名稱。

## <a name="test-a-stream-analytics-input-source"></a>測試資料流分析輸入來源
hello **TestConnection** hello 資料流分析工作是否能 tooconnect toohello 輸入來源，以及其他方面的特定 toohello 方法測試輸入來源類型。 例如，在 hello blob 輸入來源您在前述步驟中建立，hello 方法會檢查，hello 儲存體帳戶名稱和金鑰組可以是使用的 tooconnect toohello 儲存體帳戶，以及檢查該 hello 指定的容器存在。

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>建立資料流分析輸出目標
建立輸出目標是非常類似 toocreating 資料流分析的輸入來源。 輸入來源，例如輸出目標是繫結的 tooa 特定作業。 toouse hello 相同的輸出目標為不同的工作，您必須再次呼叫 hello 方法並指定不同的作業名稱。

下列程式碼的 hello 建立的輸出目標 (Azure SQL database)。 您可以自訂 hello 輸出目標的資料類型及/或序列化的型別。

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

## <a name="test-a-stream-analytics-output-target"></a>測試資料流分析輸出目標
資料流分析輸出目標也有 hello **TestConnection**方法來測試連接。

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>建立資料流分析轉換
hello 下列程式碼會建立資料流分析轉換與 hello 查詢 」 選取 * 從輸入 」，並指定 tooallocate 一個資料流處理的單位 hello 資料流分析工作。 如需有關如何調整資料流單位的詳細資訊，請參閱 [調整 Azure 資料流分析工作](stream-analytics-scale-jobs.md)。

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

輸入和輸出，例如轉換也是繫結的 toohello 底下建立特定資料流分析工作。

## <a name="start-a-stream-analytics-job"></a>啟動資料流分析工作
建立資料流分析工作的輸入、 輸出及轉換之後，您可以啟動 hello 作業呼叫 hello**啟動**方法。

下列範例程式碼的 hello 開頭自訂輸出開始時間組 tooDecember 12，2012，12:12:12 中的資料流分析工作 UTC:

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a>停止資料流分析工作
您可以停止執行中的資料流分析工作呼叫 hello**停止**方法。

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>刪除資料流分析工作
hello**刪除**hello 作業，以及 hello 基礎子資源，包括輸入、 輸出，以及 hello 作業的轉換，將會刪除方法。

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>取得支援
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
您已了解使用.NET SDK toocreate hello 基本概念，並執行分析工作。 toolearn 詳細資訊，請參閱 hello 下列資訊：

* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure 串流分析管理 .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx)。
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
