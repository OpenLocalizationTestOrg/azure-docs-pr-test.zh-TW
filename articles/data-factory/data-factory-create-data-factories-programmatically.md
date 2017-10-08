---
title: "使用 Azure.NET SDK aaaCreate 資料管線 |Microsoft 文件"
description: "了解 tooprogrammatically 如何建立、 監視和管理 Azure data factory 使用 Data Factory SDK。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>使用 Azure Data Factory .NET SDK 來建立、監視及管理 Azure Data Factory
## <a name="overview"></a>概觀
您可以使用 Data Factory .NET SDK，以程式設計方式建立、監視及管理 Azure Data Factory 本文將逐步解說中，您可以遵循 toocreate 範例.NET 主控台應用程式建立及監視 data factory。 

> [!NOTE]
> 本文並未涵蓋所有 hello Data Factory.NET API。 如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。 

## <a name="prerequisites"></a>必要條件
* Visual Studio 2012、2013 或 2015
* 下載並安裝 [Azure .NET SDK](http://azure.microsoft.com/downloads/)。
* Azure PowerShell。 遵循指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)文章 tooinstall Azure PowerShell，在您的電腦上。 您使用 Azure PowerShell toocreate Azure Active Directory 應用程式。

### <a name="create-an-application-in-azure-active-directory"></a>在 Azure Active Directory 中建立應用程式
建立 Azure Active Directory 應用程式、 建立服務主體針對 hello 應用程式，並將它指派 toohello**資料 Factory 參與者**角色。

1. 啟動 **PowerShell**。
2. 執行下列命令的 hello 並輸入 hello 使用者名稱和密碼，您會使用 toosign toohello Azure 入口網站中。

    ```PowerShell
    Login-AzureRmAccount
    ```
3. 執行下列命令 tooview hello 這個帳戶的所有 hello 訂用帳戶。

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. 執行下列命令 tooselect hello 訂用帳戶，您想要使用 toowork hello。 取代 **&lt;NameOfAzureSubscription** &gt; hello 的 Azure 訂用帳戶的名稱。

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > 記下**SubscriptionId**和**TenantId**從 hello 這個命令的輸出。

5. 建立 Azure 資源群組名稱為**ADFTutorialResourceGroup**藉由執行下列命令在 hello PowerShell 中的 hello。

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    如果已經存在 hello 資源群組，指定是否 tooupdate 它 (Y) 或保留為 (N)。

    如果您使用不同的資源群組，您會在本教學課程需要資源群組來取代 ADFTutorialResourceGroup toouse hello 名稱。
6. 建立 Azure Active Directory 應用程式。

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    如果您收到下列錯誤 hello，請指定不同的 URL，然後再次執行 hello 命令。
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. 建立 hello AD 服務主體。

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. 新增服務主體 toohello**資料 Factory 參與者**角色。

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. 取得 hello 應用程式識別碼。

    ```PowerShell
    $azureAdApplication 
    ```
    記下 hello 輸出中的 hello 應用程式識別碼 (applicationID)。

您應會從這些步驟取得下列四個值︰

* 租用戶識別碼
* 訂用帳戶識別碼
* 應用程式識別碼
* （在 hello 第一個命令中指定） 的密碼

## <a name="walkthrough"></a>逐步介紹
Hello 逐步解說中，您可以建立 data factory 管線，包含複製活動。 hello 複製活動會將資料複製相同的 hello 您 Azure blob 儲存體 tooanother 資料夾中的資料夾從 blob 儲存體。 

hello 複製活動會在 Azure Data Factory 中執行 hello 資料移動。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 請參閱[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動的詳細資料的發行項。

1. 使用 Visual Studio 2012/2013/2015 建立 C# .NET 主控台應用程式。
   1. 啟動 **Visual Studio** 2012/2013/2015。
   2. 按一下**檔案**，點太**新增**，然後按一下**專案**。
   3. 展開 [範本]，然後選取 [Visual C#]。 在此逐步解說中，您使用的是 C#，但您可以使用任何 .NET 語言。
   4. 選取**主控台應用程式**從 hello hello 右上的專案類型清單。
   5. 輸入**DataFactoryAPITestApp** hello 名稱。
   6. 選取**C:\ADFGetStarted** hello 位置。
   7. 按一下**確定**toocreate hello 專案。
2. 按一下**工具**，點太**NuGet 套件管理員**，然後按一下**Package Manager Console**。
3. 在 hello **Package Manager Console**，執行下列步驟 hello:
   1. 執行下列命令 tooinstall Data Factory 套件 hello:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. 執行下列命令 tooinstall Azure Active Directory 封裝 （使用 Active Directory API hello 程式碼中） 的 hello:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. 取代 hello 內容**App.config** hello 以 hello 內容之後的專案中的檔案： 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. 在 hello App.Config 檔案中，更新值**&lt;應用程式識別碼&gt;**， **&lt;密碼&gt;**，  **&lt;訂用帳戶 ID&gt;**，和**&lt;租用戶識別碼&gt;**以您自己的值。
6. 新增下列 hello**使用**陳述式 toohello **Program.cs** hello 專案中的檔案。

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. 新增下列程式碼會建立的執行個體的 hello **DataPipelineManagementClient**類別 toohello **Main**方法。 您可以使用這個物件 toocreate data factory、 連結的服務、 輸入和輸出資料集和管線。 您也可以使用這個物件 toomonitor 配量的資料集在執行階段。

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > 取代 hello 值**resourceGroupName** hello Azure 資源群組名稱。 您可以建立資源群組使用 hello[新增 AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet。
   >
   > 更新的 hello 資料 factory () toobe 唯一的名稱。 Hello data factory 名稱必須是全域唯一的。 請參閱 [Data Factory - 命名規則](data-factory-naming-rules.md) 主題，以了解 Data Factory 成品的命名規則。
7. 新增下列程式碼會建立 hello**資料 factory** toohello **Main**方法。

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. 新增下列程式碼會建立 hello **Azure 儲存體連結服務**toohello **Main**方法。

   > [!IMPORTANT]
   > 以 Azure 儲存體帳戶的名稱和金鑰取代 **storageaccountname** 和 **accountkey**。

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. 新增下列程式碼會建立 hello**輸入和輸出資料集**toohello **Main**方法。

    hello **FolderPath** hello 輸入的 blob 設定太**adftutorial /**其中**adftutorial** hello 您的 blob 儲存體中的 hello 容器名稱。 如果此容器不存在於您的 Azure blob 儲存體中，建立容器具有此名稱： **adftutorial**並上傳的文字檔案 toohello 容器。

    hello FolderPath hello 輸出 blob 設： **adftutorial/apifactoryoutput / {Slice}**其中**配量**是動態計算出根據的 hello 值**SliceStart**（開始日期時間的每個配量）。

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. 新增 hello 下列程式碼的**會建立並啟動管線**toohello **Main**方法。 此管線有一個 **CopyActivity**，它以 **BlobSource** 為來源，**BlobSink** 為接收器。

    hello 複製活動會在 Azure Data Factory 中執行 hello 資料移動。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 請參閱[資料移動活動](data-factory-data-movement-activities.md)hello 複製活動的詳細資料的發行項。

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. 新增下列程式碼 toohello hello **Main**方法 tooget hello 狀態 hello 的資料配量的輸出資料集。 預期此範例中只有一個配量。

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. **（選擇性）**新增 hello 下列程式碼執行 tooget 詳細資料的資料配量 toohello **Main**方法。

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. 新增下列 hello 所使用的 helper 方法的 hello **Main**方法 toohello**程式**類別。 這個方法會出現，可讓您提供的對話方塊**使用者名**和**密碼**toolog 用於 tooAzure 入口網站。

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. 在 [hello 方案總管] 中，展開 hello 專案： **DataFactoryAPITestApp**，以滑鼠右鍵按一下**參考**，然後按一下**加入參考**。 選取 `System.Configuration` 組件的核取方塊，然後按一下 [確定]。
15. 建置 hello 主控台應用程式。 按一下**建置**hello 功能表，然後按一下上**建置方案**。
16. 確認至少一個檔案中沒有 hello adftutorial 容器在您的 Azure blob 儲存體。 如果不是，建立 Emp.txt 檔案 [記事本] 中以 hello 下列內容並將它上傳 toohello adftutorial 容器。

    ```
    John, Doe
    Jane, Doe
    ```
17. 按一下以執行 hello 範例**偵錯** -> **開始偵錯**hello 功能表上。 當您看到 hello**正在執行的資料配量的詳細資料**，等待幾分鐘，然後按**ENTER**。
18. 使用 Azure 入口網站 tooverify hello 該 hello 資料 factory **APITutorialFactory**建立以 hello 下列成品：
    * 連結服務：**AzureStorageLinkedService**
    * 資料集：**DatasetBlobSource** 和 **DatasetBlobDestination**。
    * 管線： **PipelineBlobSample**
19. 確認已建立的輸出檔中 hello **apifactoryoutput**資料夾中 hello **adftutorial**容器。

## <a name="get-a-list-of-failed-data-slices"></a>取得失敗資料配量的清單 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>後續步驟
請參閱下列範例建立管線中使用.NET SDK 將資料從 Azure blob 儲存體 tooan Azure SQL database 複製 hello: 

- [從 Blob 儲存體 tooSQL 資料庫中建立管線 toocopy 資料](data-factory-copy-activity-tutorial-using-dotnet-api.md)
