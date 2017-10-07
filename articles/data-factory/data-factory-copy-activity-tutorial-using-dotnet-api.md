---
title: "教學課程：使用 .NET API 建立具有複製活動的管線 | Microsoft Docs"
description: "在本教學課程中，您會使用 .NET API，建立具有複製活動的 Azure Data Factory 管線。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>教學課程：使用 .NET API 建立具有複製活動的管線
> [!div class="op_single_selector"]
> * [概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [複製精靈](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 入口網站](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 範本](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

在本文中，您將學習如何 toouse [.NET API](https://portal.azure.com) toocreate data factory 管線，將資料從 Azure blob 儲存體 tooan Azure SQL database 複製。 如果您是新 tooAzure Data Factory，閱讀 hello[簡介 tooAzure Data Factory](data-factory-introduction.md)發行項，然後再執行本教學課程。   

在本教學課程中，您可以建立包含一個活動的管線：複製活動。 hello 複製活動會將資料從支援的資料存放區 tooa 支援的接收資料存放區。 如需作為來源和接收區支援的資料存放區清單，請參閱[支援的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 hello 活動被提供安全、 可靠且可擴充的方式的各種資料存放區之間的資料可以複製的全域可用服務。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。

一個管線中可以有多個活動。 此外，您可以藉由設定 hello 輸出資料集的一個活動 hello 的輸入資料集的 hello 其他活動鏈結 （執行一個活動執行另一個之後） 的兩個活動。 如需詳細資訊，請參閱[管線中的多個活動](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)。 

> [!NOTE] 
> 如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。
> 
> 在此教學課程中的 hello 資料管線會將資料從來源資料存放區 tooa 目的地資料存放區。 如需如何使用 Azure Data Factory，tootransform 資料，請參閱[教學課程： 建立使用 Hadoop 叢集管線 tootransform 資料](data-factory-build-your-first-pipeline.md)。

## <a name="prerequisites"></a>必要條件
* 透過移[教學課程的概觀和必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)tooget hello 教學課程和完整 hello 概觀**必要條件**步驟。
* Visual Studio 2012、2013 或 2015
* 下載並安裝 [Azure .NET SDK](http://azure.microsoft.com/downloads/)
* Azure PowerShell。 遵循指示[如何 tooinstall 和設定 Azure PowerShell](../powershell-install-configure.md)文章 tooinstall Azure PowerShell，在您的電腦上。 您使用 Azure PowerShell toocreate Azure Active Directory 應用程式。

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
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
4. 新增下列 hello **appSetttings**區段 toohello **App.config**檔案。 Hello helper 方法會使用這些設定： **GetAuthorizationHeader**。

    以您自己的值取代**&lt;應用程式識別碼&gt;**、**&lt;密碼&gt;**、**&lt;訂用帳戶識別碼&gt;****&lt;租用戶識別碼&gt;**的值。

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

5. 新增下列 hello**使用**陳述式 toohello 原始程式檔 (Program.cs) hello 專案中的。

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
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > 取代 hello 值**resourceGroupName** hello Azure 資源群組名稱。
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

    資料處理站可以有一或多個管線。 其中的管線可以有一或多個活動。 例如，複製活動 toocopy 資料從來源 tooa 目的地資料存放區和 HDInsight Hive 活動 toorun Hive 指令碼 tootransform 輸入資料 tooproduct 輸出資料。 讓我們開始在此步驟中建立 hello 資料 factory。
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

    您可以建立連結的服務中的資料處理站 toolink 資料儲存和運算服務 toohello 資料 factory。 在本教學課程中，您不會使用任何計算服務，例如 Azure HDInsight 或 Azure Data Lake Analytics。 您可以使用兩種類型的資料存放區：Azure 儲存體 (來源) 和 Azure SQL Database (目的地)。 

    因此，您可以建立名為 AzureStorageLinkedService 和 AzureSqlLinkedService 的兩個連結服務︰類型為 AzureStorage 和 AzureSqlDatabase。  

    hello AzureStorageLinkedService 連結您的 Azure 儲存體帳戶 toohello data factory。 這個儲存體帳戶為其中一個 hello 在其中建立容器及 hello 資料上傳的過程[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
9. 新增下列程式碼會建立 hello **Azure SQL 連結服務**toohello **Main**方法。

   > [!IMPORTANT]
   > 以您的 Azure SQL 伺服器名稱、資料庫名稱、使用者和密碼取代 **servername**、**databasename**、**username** **password**。

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    AzureSqlLinkedService 連結您的 Azure SQL database toohello data factory。 複製 hello blob 儲存體中的 hello 資料會儲存在資料庫中。 在此資料庫中建立 hello emp 資料表的一部分[必要條件](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)。
10. 新增下列程式碼會建立 hello**輸入和輸出資料集**toohello **Main**方法。

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    在 hello 先前步驟中，您會建立連結的服務 toolink，您的 Azure 儲存體帳戶和 Azure SQL database tooyour 資料 factory。 在此步驟中，您可以定義名為 InputDataset OutputDataset 代表輸入和輸出資料儲存在 hello 分別 AzureStorageLinkedService 和 AzureSqlLinkedService 所參考的資料存放區中的兩個資料集。

    hello Azure 儲存體連結服務指定 Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure 儲存體帳戶的 hello 連接字串。 此外，hello 輸入的 blob 資料集 (InputDataset) 指定 hello 容器和包含 hello 輸入的資料的 hello 資料夾。  

    同樣地，hello 連結的 Azure SQL Database 服務指定 hello Data Factory 服務會使用在執行的階段 tooconnect tooyour Azure SQL database 的連接字串。 此外，hello 輸出 SQL 資料表資料集 (OututDataset) 會指定 hello 資料表中 hello 資料庫 toowhich hello hello blob 儲存體的資料複製。

    在此步驟中，您建立資料集名為指向 tooa blob 檔案 (emp.txt) InputDataset hello 的 blob 容器 (adftutorial) 的根資料夾中 hello hello AzureStorageLinkedService 連結服務所代表的 Azure 儲存體中。 如果您不指定 hello 檔名的值 （或略過它），從 hello 輸入資料夾中的所有 blob 資料，則複製的 toohello 目的地。 在本教學課程中，您可以指定 hello 檔案名稱的值。    

    在此步驟中，您會建立名為 **OutputDataset**的輸出資料集。 此資料集所代表的 hello Azure SQL database 中的點 tooa SQL 資料表**AzureSqlLinkedService**。
11. 新增 hello 下列程式碼的**會建立並啟動管線**toohello **Main**方法。 在此步驟中您會建立管線，其中含有使用 **InputDataset** 作為輸入和使用 **OutputDataset** 作為輸出的**複製活動**。

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    請注意下列點 hello:
   
    - 在 [hello 活動] 區段中，沒有一個活動其**類型**設定得**複製**。 如需 hello 複製活動的詳細資訊，請參閱[資料移動活動](data-factory-data-movement-activities.md)。 在 Data Factory 解決方案中，您也可以使用[資料轉換活動](data-factory-data-transformation-activities.md)。
    - 輸入 hello 活動設定太**InputDataset**和輸出 hello 活動設定太**OutputDataset**。 
    - 在 [hello **typeProperties** ] 區段中， **BlobSource**指定 hello 來源類型為和**SqlSink**指定為 hello 接收器類型。 支援的 hello 複製活動做為來源與接收的資料存放區的完整清單，請參閱[支援資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。 toolearn toouse 特定支援的資料如何儲存為來源/接收器，按一下 hello 資料表中的 hello 連結。  
   
    目前，輸出資料集是哪些磁碟機 hello 排程。 在本教學課程中，輸出資料集是設定的 tooproduce 配量小時一次。 hello 管線有開始時間和結束時間的一天分散，也就是 24 小時。 因此，hello 管線所產生的輸出資料集的 24 配量。
12. 新增下列程式碼 toohello hello **Main**方法 tooget hello 狀態 hello 的資料配量的輸出資料集。 在此範例中只預期有配量。

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

13. 新增下列程式碼執行 tooget 詳細資料的資料配量 toohello hello **Main**方法。

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
            }
        );

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

14. 新增下列 hello 所使用的 helper 方法的 hello **Main**方法 toohello**程式**類別。

    > [!NOTE] 
    > 當您複製並貼上下列程式碼的 hello 時，請確定該 hello 複製程式碼位於相同層級為 hello Main 方法的 hello。

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

15. 在 hello 方案總管 中，展開 hello 專案 (DataFactoryAPITestApp)，以滑鼠右鍵按一下**參考**，然後按一下**加入參考**。 選取 **System.Configuration** 組件的核取方塊。 然後按一下 [確定]。
16. 建置 hello 主控台應用程式。 按一下**建置**hello 功能表，然後按一下上**建置方案**。
17. 確認是否有至少一個檔案中 hello **adftutorial**您的 Azure blob 儲存體容器中。 如果沒有，請建立**Emp.txt**檔案 [記事本] 中以 hello 內容之後，並將它上傳 toohello adftutorial 容器。

    ```
    John, Doe
    Jane, Doe
    ```
18. 按一下以執行 hello 範例**偵錯** -> **開始偵錯**hello 功能表上。 當您看到 hello**正在執行的資料配量的詳細資料**，等待幾分鐘，然後按**ENTER**。
19. 使用 Azure 入口網站 tooverify hello 該 hello 資料 factory **APITutorialFactory**建立以 hello 下列成品：
   * 連結服務：**LinkedService_AzureStorage**
   * 資料集︰**InputDataset** 和 **OutputDataset**。
   * 管線： **PipelineBlobSample**
20. 確認 hello 兩個員工記錄建立於 hello **emp** hello 中的資料表指定 Azure SQL database。

## <a name="next-steps"></a>後續步驟
如需適用於 Data Factory 之 .NET API 的完整文件，請參閱 [Data Factory .NET API 參考](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1)。

在本教學課程中，您可使用 Azure Blob 儲存體作為來源資料存放區以及使用 Azure SQL Database 作為複製作業的目的地資料存放區。 hello 下表提供 hello 複製活動支援做為來源和目的地資料存放區的清單： 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

關於如何 toocopy 資料，從資料存放區，toolearn 按一下 hello 連結 hello hello 資料表中的資料存放區。

