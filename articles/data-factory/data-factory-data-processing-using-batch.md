---
title: "aaaProcess 大型資料集使用 Data Factory 和批次 |Microsoft 文件"
description: "描述如何 tooprocess 大量的 Azure Data Factory 中的資料管線所使用的 Azure 批次的平行處理功能。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>使用 Data Factory 和 Batch 處理大型資料集
本文說明範例解決方案的架構，此解決方案能以自動且排程的方式移動和處理大型資料集。 它也提供使用 Azure Data Factory 和 Azure 批次的端對端逐步解說 tooimplement hello 方案。

這篇文章比我們的一般文章還長，因為它包含整個範例解決方案的逐步解說。 如果您是新 tooBatch 及資料 Factory，您可以了解這些服務，它們共同運作的方式。 如果您知道 hello 服務的相關項目，會設計/架構解決方案，您可以專注於 hello 只[架構 > 一節](#architecture-of-sample-solution)的 hello 發行項，如果您正在開發原型或方案，您可能也想 tootry逐步解說中 hello[逐步解說](#implementation-of-sample-solution)。 歡迎您對此內容以及您如何使用它提出看法。

首先，讓我們看看如何協助 Data Factory 和批次服務處理 hello 雲端中的大型資料集。     

## <a name="why-azure-batch"></a>為何使用 Azure Batch？
Azure 批次，可讓您有效率地在 hello 雲端中的 toorun 大規模平行和高效能運算 (HPC) 應用程式。 這是排程需要大量計算工作 toorun managed 集合上的虛擬機器的平台服務，可以自動調整計算資源 toomeet hello 需求的工作。

以 hello 批次服務，您定義 Azure 計算資源 tooexecute 應用程式以平行方式，而是在標尺。 您可以依需求或排程執行作業，而不需要 toomanually 建立、 設定和管理 HPC 叢集、 個別的虛擬機器、 虛擬網路或複雜的工作和工作排程基礎結構。

請參閱下列文章，如果您不熟悉 Azure 批次因為它有助於了解 hello 架構/hello 方案實作本文所述的 hello。   

* [Azure Batch 的基本概念](../batch/batch-technical-overview.md)
* [Batch 功能概觀](../batch/batch-api-basics.md)

（選擇性） toolearn 進一步了解 Azure 批次，請參閱 hello [Azure 批次學習路徑](https://azure.microsoft.com/documentation/learning-paths/batch/)。

## <a name="why-azure-data-factory"></a>為何使用 Azure Data Factory？
Data Factory 是以雲端為基礎的資料整合服務會協調及自動 hello 移動和轉換資料。 使用 hello Data Factory 服務，您可以建立將資料從內部部署和雲端資料儲存區 tooa 集中的資料存放區的 managed 的資料管線 (例如： Azure Blob 儲存體)，和處理程序轉換資料，使用 Azure HDInsight 等 Azure 服務機器學習。 您也可以排程已排程的方式 （每小時、 每天、 每週等） 和監視器中的資料管線 toorun 和管理它們在概覽 tooidentify 問題並採取動作。

請參閱下列文章，如果您不熟悉 Azure Data Factory 因為它有助於了解 hello 架構/hello 方案實作本文所述的 hello。  

* [Azure Data Factory 簡介](data-factory-introduction.md)
* [建置第一個資料管線](data-factory-build-your-first-pipeline.md)   

（選擇性） toolearn 深入了解 Azure Data Factory，請參閱 hello [Azure Data factory 的學習路徑](https://azure.microsoft.com/documentation/learning-paths/data-factory/)。

## <a name="data-factory-and-batch-together"></a>Data Factory 和 Batch 一起使用
資料處理站包含內建活動，例如 tooa 目的地資料存放區和 Hive 活動 tooprocess 資料在 Azure 上使用 Hadoop 叢集 (HDInsight)，從來源資料複製活動 toocopy/移動資料存放區。 如需支援的轉換活動清單，請參閱 [資料轉換活動](data-factory-data-transformation-activities.md) 。

也可讓您 toocreate 自訂.NET 活動 toomove 或處理序的資料，與您自己的邏輯，並在 Azure HDInsight 叢集上或 Azure Batch 集區的 Vm 上執行這些活動。 當您使用 Azure 批次時，您可以設定 hello 集區 tooauto 標尺 （新增或移除 hello 的工作負載的 Vm） 根據您提供的公式。     

## <a name="architecture-of-sample-solution"></a>範例解決方案架構
即使這篇文章中所描述的 hello 架構適用於簡單的解決方案，它是相關 toocomplex 案例，例如風險所涵蓋了金融服務、 映像處理和轉譯和 genomic 分析模型。

hello 圖表將說明 Data Factory 1） 如何協調資料移動，並處理和 2） 如何處理 Azure 批次的資料則會以平行方式 hello。 下載和列印 hello 圖表，以方便參考 (11x17 中。 或 A3 的大小)︰[使用 Azure Batch 和 Data Factory 的 HPC 和資料協調](http://go.microsoft.com/fwlink/?LinkId=717686)。

[![大規模資料處理圖表](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

hello 下列清單提供 hello hello 程序的基本步驟。 hello 解決方案包含程式碼和說明 toobuild hello 端對端解決方案。

1. **以計算節點的集區 (VM) 設定 Azure Batch**。 您可以指定節點的 hello 數目和每個節點的大小。
2. **建立 Azure Data Factory 執行個體** ，並為其設定代表 Azure Blob 儲存體、Azure Batch 計算服務、輸入/輸出資料和工作流程/管線的實體，並建立具有會移動和轉換資料之活動的工作流程/管線。
3. **在 hello Data Factory 管線中建立的自訂.NET 活動**。 hello 活動是您在 hello Azure Batch 集區執行的使用者程式碼。
4. **將大量的輸入資料儲存為 Azure 儲存體中的 blob**。 資料會分成邏輯配量 (通常依時間來分)。
5. **Data Factory 複製以平行方式處理資料的**toohello 次要位置。
6. **Data Factory 執行 hello 使用批次所配置的 hello 集區的自訂活動**。 Data Factory 可以同時執行多個活動。 每個活動各處理某個配量的資料。 hello 結果會儲存在 Azure 儲存體。
7. **Data Factory 移動 hello 最終結果 tooa 第三個位置**，應用程式，透過散發，或做進一步處理其他工具。

## <a name="implementation-of-sample-solution"></a>範例解決方案的實作
hello 範例方案刻意簡單，而且是 tooshow 您如何 toouse Data Factory 和批次一起 tooprocess 資料集。 hello 方案就是計算組織中的時間序列的輸入檔中的 hello 次數的搜尋詞彙 ("Microsoft")。 它會輸出 hello 計數 toooutput 檔案。

**時間**： 如果您已熟悉 Azure Data Factory 及批次中的基本概念，而且已完成的 hello 必要條件下面所列，我們會評估此解決方案會 toocomplete 1-2 小時。

### <a name="prerequisites"></a>必要條件
#### <a name="azure-subscription"></a>Azure 訂閱
如果您沒有 Azure 訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。 請參閱 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。

#### <a name="azure-storage-account"></a>Azure 儲存體帳戶
您可以使用 Azure 儲存體帳戶將 hello 資料儲存在本教學課程。 如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。 hello 範例解決方案會使用 blob 儲存體。

#### <a name="azure-batch-account"></a>Azure Batch 帳戶
建立 Azure 批次帳戶使用 hello [Azure 入口網站](http://manage.windowsazure.com/)。 請參閱 [建立和管理 Azure Batch 帳戶](../batch/batch-account-create-portal.md)。 請注意 hello Azure Batch 帳戶名稱和帳戶金鑰。 您也可以使用[新增 AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate Azure Batch 帳戶。 如需使用此 Cmdlet 的詳細指示，請參閱 [開始使用 Azure Batch PowerShell Cmdlet](../batch/batch-powershell-cmdlets-get-started.md) 。

hello 範例方案會使用 Azure 批次 （間接透過 Azure Data Factory 管線） tooprocess 資料，以平行方式的運算節點 （受管理的虛擬機器集合） 的集區上。

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Azure Batch 虛擬機器 (VM) 集區
建立至少有 2 個計算節點的 **Azure Batch 集區** 。

1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **瀏覽**在 hello 左的窗格中，然後按一下**批次帳戶**。
2. 選取您的 Azure Batch 帳戶 tooopen hello**批次帳戶**刀鋒視窗。
3. 按一下 [集區]  圖格。
4. 在 hello**集區**刀鋒視窗中，按一下 hello 工具列 tooadd 集區中的 新增 按鈕。
   1. 請輸入 hello 集區的識別碼 (**集區識別碼**)。 請注意 hello **hello 集區的識別碼**; 時，您需要它建立 hello Data Factory 方案。
   2. 指定**Windows Server 2012 R2** hello 作業系統系列設定。
   3. 選取 **節點定價層**。
   4. 輸入**2**做為 hello 值**目標專用**設定。
   5. 輸入**2**做為 hello 值**每個節點的最大工作**設定。
   6. 按一下**確定**toocreate hello 集區。

#### <a name="azure-storage-explorer"></a>Azure 儲存體總管
[Azure 儲存體總管 6 (工具)](https://azurestorageexplorer.codeplex.com/) 或 [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (來自 ClumsyLeaf 軟體)。 您可以使用這些工具來檢查及更改 Azure 儲存體專案包括雲端裝載應用程式的 hello 記錄檔中的 hello 資料。

1. 使用私用存取 (沒有匿名存取) 建立名為 **mycontainer** 的容器
2. 如果您使用**CloudXplorer**、 建立資料夾和子資料夾與 hello 下列結構：

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder` 和 `outputfolder` 是 `mycontainer` 中的最上層資料夾。 hello`inputfolder`具有與日期時間戳記 (YYYY-MM-DD-HH) 的子資料夾。

   如果您使用**Azure 儲存體總管**，在 hello 下一個步驟中，您需要 tooupload 檔名： `inputfolder/2015-11-16-00/file.txt`， `inputfolder/2015-11-16-01/file.txt` ，依此類推。 此步驟會自動建立 hello 資料夾。
3. 建立文字檔**file.txt**有 hello 關鍵字的內容與您電腦上**Microsoft**。 例如：“test custom activity Microsoft test custom activity Microsoft”。
4. 上傳 hello 檔案 toohello 下一個輸入 Azure blob 儲存體中的資料夾。

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   如果您使用**Azure 儲存體總管**，hello 檔案上傳**file.txt**太**mycontainer**。 按一下**複製**hello 工具列 toocreate hello blob 的複本上。 在 hello**複製 Blob**對話方塊中，變更 hello**目的地 blob 名稱**太`inputfolder/2015-11-16-00/file.txt`。 重複此步驟 toocreate `inputfolder/2015-11-16-01/file.txt`， `inputfolder/2015-11-16-02/file.txt`， `inputfolder/2015-11-16-03/file.txt`， `inputfolder/2015-11-16-04/file.txt` ，依此類推。 這個動作會自動建立 hello 資料夾。
5. 建立另一個容器，名為：`customactivitycontainer`。 您上傳 hello 自訂活動 zip 檔案 toothis 容器。

#### <a name="visual-studio"></a>Visual Studio
安裝 Microsoft Visual Studio 2012 或更新版本 toocreate hello 自訂批次活動 toobe hello Data Factory 方案中使用。

### <a name="high-level-steps-toocreate-hello-solution"></a>高階步驟 toocreate hello 方案
1. 建立包含 hello 資料處理邏輯的自訂活動。
2. 建立 Azure data factory，以使用自訂活動的 hello:

### <a name="create-hello-custom-activity"></a>建立 hello 自訂活動
hello Data Factory 的自訂活動是此範例方案的 hello 心。 hello 範例解決方案會使用 Azure Batch toorun hello 自訂活動。 請參閱[Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)hello 的基本資訊 toodevelop 自訂活動和使用在 Azure Data Factory 管線。

toocreate.NET 自訂活動，您可以使用 Azure Data Factory 管線中，您需要 toocreate **.NET 類別庫**所實作的類別具有專案**IDotNetActivity**介面。 這個介面只有一個方法： **執行**。 以下是 hello hello 方法簽章：

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

hello 方法都有一些您需要 toounderstand 的主要元件。

* hello 方法會採用四個參數：

  1. **linkedServices**。 連結輸入/輸出資料來源的連結服務的可列舉清單 (例如： Azure Blob 儲存體) toohello 資料 factory。 在此範例中，只有一個用於輸入和輸出的 Azure 儲存體類型連結服務。
  2. **資料集**。 這是資料集的可列舉清單。 您可以使用此參數 tooget hello 位置以及輸入和輸出資料集所定義的結構描述。
  3. **活動**。 這個參數代表 hello 目前計算實體-在此情況下，Azure 批次服務。
  4. **記錄器**。 hello 記錄器可讓您為 「 使用者 」 記錄檔以取得 hello 撰寫偵錯註解呈現的 hello 管線。
* hello 方法會傳回可使用的 toochain 自訂活動運算子 hello 未來的字典。 尚未實作這項功能，因此從 hello 方法會傳回空的字典。

#### <a name="procedure-create-hello-custom-activity"></a>程序： 建立 hello 自訂活動
1. 在 Visual Studio 中建立 .NET 類別庫專案。

   1. 啟動 **Visual Studio 2012**/**2013/2015**。
   2. 按一下**檔案**，點太**新增**，然後按一下**專案**。
   3. 展開 [範本]，然後選取 [Visual C#]**\#**。 在本逐步解說中，您可以使用 C\#，但是您可以使用任何.NET 語言 toodevelop hello 自訂活動。
   4. 選取**類別庫**從 hello hello 右上的專案類型清單。
   5. 輸入**MyDotNetActivity** hello**名稱**。
   6. 選取**c:\\ADF** hello**位置**。 建立 hello 資料夾**ADF**如果不存在。
   7. 按一下**確定**toocreate hello 專案。
2. 按一下**工具**，點太**NuGet 套件管理員**，然後按一下**Package Manager Console**。
3. 在 hello **Package Manager Console**，執行下列命令 tooimport hello **Microsoft.Azure.Management.DataFactories**。

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. 匯入 hello **Azure 儲存體**toohello 專案中的 NuGet 封裝。 因為您使用 hello Blob 儲存體 API 在這個範例中，您會需要此封裝。

    ```powershell
    Install-Package Azure.Storage
    ```
5. 新增下列 hello**使用**hello 專案中的指示詞 toohello 來源檔案。

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. 變更 hello 名稱的 hello**命名空間**太**MyDotNetActivityNS**。

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. 變更 hello hello 類別名稱太**MyDotNetActivity**從其中 hello **IDotNetActivity**介面，如底下所示。

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. 實作 （加入） hello **Execute**方法 hello **IDotNetActivity**介面 toohello **MyDotNetActivity**類別，並複製下列範例程式碼 toohello 方法的 hello。 請參閱 hello [Execute Method](#execute-method)一節說明此方法中使用的 hello 邏輯。

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. 新增下列 helper 方法 toohello 類別 hello。 這些方法會叫用 hello **Execute**方法。 最重要的是，hello **Calculate**方法隔離 hello 程式碼，可逐一查看每個 blob。

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    hello **GetFolderPath**方法會傳回 hello 路徑 toohello 資料夾該 hello 資料集點 tooand hello **GetFileName**方法會傳回 hello hello blob 檔案的名稱/的 hello 指向資料集。

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    hello **Calculate**方法會計算關鍵字的執行個體的 hello 數目**Microsoft** hello 輸入檔 (hello 資料夾中的 blob) 中。 hello 搜尋詞彙 ("Microsoft") 是硬式編碼 hello 程式碼中。

1. 編譯 hello 專案。 按一下**建置**從 hello 功能表，然後按一下**建置方案**。
2. 啟動**Windows 檔案總管**，並瀏覽過**bin\\偵錯**或**bin\\釋放**資料夾視 hello 組建類型而定。
3. 建立 zip 檔案**MyDotNetActivity.zip** ，其中包含所有的 hello 二進位碼檔案中 hello  **\\bin\\偵錯**資料夾。 您可能想 tooinclude hello MyDotNetActivity。**pdb**檔案以便讓您取得 hello hello 問題原因發生失敗時，原始程式碼中的其他詳細資料，例如行號。

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. 上傳**MyDotNetActivity.zip**為 toohello blob 容器的 blob:`customactivitycontainer`在 hello Azure blob 儲存體的 hello **StorageLinkedService**連結服務中 hello **ADFTutorialDataFactory**使用。 建立 hello blob 容器`customactivitycontainer`如果不存在。

#### <a name="execute-method"></a>Execute 方法
本章節提供更多詳細資料和 hello hello Execute 方法中的程式碼的相關注意事項。

1. 逐一查看 hello 輸入集合的 hello 成員存在於 hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx)命名空間。 逐一查看 hello blob 集合時，需要使用 hello **BlobContinuationToken**類別。 基本上，您必須使用與-while 迴圈與 hello 權杖做為結束迴圈 hello hello 機制。 如需詳細資訊，請參閱[如何 toouse 與.NET 的 Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 基本迴圈如下所示：

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   請參閱 hello 文件以 hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx)方法，如需詳細資訊。
2. hello 程式碼的 hello 內以邏輯方式處理透過 blob hello 組會做為 while 迴圈。 在 hello **Execute**方法中，執行 hello-雖然迴圈傳送 hello 的 blob 清單 tooa 方法名為**Calculate**。 hello 方法會傳回名為的字串變數**輸出**也就是需要逐一查看所有 hello blob hello 區段中的 hello 結果。

   它會傳回 hello 次數 hello 搜尋詞彙 (**Microsoft**) hello blob 中傳遞 toohello **Calculate**方法。

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. 一次 hello **Calculate** hello 工作完成的方法，則必須寫入 tooa 新 blob。 讓每一組處理的 blob，可以與 hello 結果寫入新的 blob。 toowrite tooa 新 blob，第一個尋找 hello 輸出資料集。

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. hello 程式碼也會呼叫的 helper 方法： **GetFolderPath** tooretrieve hello 資料夾路徑 （hello 儲存體容器名稱）。

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   hello **GetFolderPath**轉換 hello 資料集物件 tooan AzureBlobDataSet，有一個名為 FolderPath 屬性。

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. hello 程式碼呼叫 hello **GetFileName**方法 tooretrieve hello 檔案名稱 （blob）。 hello 程式碼是類似 toohello 上述程式碼 tooget hello 資料夾路徑。

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. 藉由建立 URI 物件寫入 hello hello 檔案名稱。 hello URI 建構函式使用 hello **BlobEndpoint**屬性 tooreturn hello 容器名稱。 hello 資料夾路徑和檔案名稱會加入 tooconstruct hello 輸出 blob URI。  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. 已寫入 hello hello 檔案名稱和您現在可以撰寫 hello 輸出字串 hello 從**Calculate**方法 tooa 新的 blob:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>建立 hello 資料處理站
在 [hello[建立 hello 自訂活動](#create-the-custom-activity)] 區段中，建立自訂活動和上傳的 hello zip 檔案與二進位檔和 hello PDB 檔案 tooan Azure blob 容器。 在本節中，您將建立 Azure**資料 factory**與**管線**使用 hello**自訂活動**。

hello 的 hello 自訂活動代表 hello 輸入資料夾中的 hello blob （檔案） 的輸入資料集 (`mycontainer\\inputfolder`) blob 儲存體中。 hello 輸出資料集，如 hello 活動代表 hello 輸出資料夾中的 hello 輸出 blob (`mycontainer\\outputfolder`) blob 儲存體中。

卸除一個或多個檔案中的 hello 輸入資料夾：

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

以 hello 內容之後到每一個 hello 資料夾，例如，卸除一個檔案 (.txt)。

```
test custom activity Microsoft test custom activity Microsoft
```

每個輸入的資料夾對應 tooa Azure Data Factory 中的配量，即使 hello 資料夾有 2 個以上的檔案。 Hello 管線處理每個配量時，該配量的 hello 輸入資料夾中的所有 hello blob 會都重複 hello 自訂活動。

您會看到五個輸出檔案以 hello 相同內容。 例如，處理 hello 2015-11-16-00 資料夾中的 hello 檔案 hello 輸出檔案具有下列內容的 hello:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

如果您卸除多個檔案 （.txt、 file2.txt、 file3.txt） 以 hello 中，相同內容 toohello 輸入的資料夾，則會看見 hello hello 輸出檔中的內容之後。 每個資料夾 (2015年-11-16-00，等等) 對應 tooa 配量在此範例中，即使 hello 資料夾有多個輸入的檔。

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

hello 輸出檔案具有三行，其中每個輸入檔案 (blob) hello 與 hello 配量 (2015年-11-16-00) 相關聯的資料夾中。

每個活動執行都會建立一個工作。 在此範例中，只有一個活動中沒有 hello 管線。 Hello 管線處理配量，hello 自訂活動會在 Azure 批次 tooprocess hello 配量上執行。 由於有 5 個配量 (每個配量可以有多個 blob 或檔案)，因此在 Azure Batch 中會建立 5 個工作。 工作將會批次上時，實際上 hello 執行自訂活動。

下列逐步解說的 hello 提供其他詳細資料。

#### <a name="step-1-create-hello-data-factory"></a>步驟 1： 建立 hello 資料處理站
1. 登入 toohello 之後[Azure 入口網站](https://portal.azure.com/)，執行下列步驟 hello:

   1. 按一下**新增**hello 左側功能表上。
   2. 按一下**資料 + 分析**在 hello**新增**刀鋒視窗。
   3. 按一下**Data Factory**上 hello**資料分析**刀鋒視窗。
2. 在 hello**新的 data factory**刀鋒視窗中，輸入**CustomActivityFactory** hello 名稱。 hello hello Azure data factory 的名稱必須是全域唯一的。 如果您收到 hello 錯誤： **Data factory 名稱"CustomActivityFactory"不是使用**，變更 hello hello data factory 名稱 (例如， **yournameCustomActivityFactory**)，然後再次嘗試建立一次。
3. 按一下 [資源群組名稱] ，並選取現有的資源群組，或建立一個群組。
4. 請確認您使用 hello 正確的訂用帳戶和您想要建立 hello 資料 factory toobe 的區域。
5. 按一下**建立**上 hello**新的 data factory**刀鋒視窗。
6. 您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站。
7. 已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>步驟 2：建立連結服務
連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。 在此步驟中，您連結您**Azure 儲存體**帳戶和**Azure Batch**帳戶 tooyour 資料 factory。

#### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
1. 按一下 hello**作者及部署**磚 hello **DATA FACTORY**刀鋒伺服器**CustomActivityFactory**。 您會看到 hello Data Factory 編輯器。
2. 按一下**新建資料存放區**在 hello 命令列，然後選擇  **Azure 儲存體。** 您應該會看見 hello JSON 指令碼來建立 Azure 儲存體已連結的 hello 編輯器中的服務。

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. 取代**帳戶名稱**hello Azure 儲存體帳戶名稱和**帳戶金鑰**hello 的 hello Azure 儲存體帳戶的存取金鑰。 toolearn 如何 tooget 您的儲存體存取金鑰，請參閱[檢視、 複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。

4. 按一下**部署**hello 命令列 toodeploy hello 連結服務。

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>建立 Azure Batch 連結服務
在此步驟中，您可以建立連結的服務，如您**Azure Batch**為使用的 toorun hello Data Factory 的自訂活動的帳戶。

1. 按一下**新計算**在 hello 命令列，然後選擇  **Azure 批次。** 您應該會看見 hello JSON 指令碼來建立 Azure Batch 連結 hello 編輯器中的服務。
2. 在 hello JSON 指令碼：

   1. 取代**帳戶名稱**hello Azure Batch 帳戶名稱。
   2. 取代**便捷鍵**hello hello Azure Batch 帳戶存取索引鍵。
   3. 輸入 hello hello 集區識別碼 hello **poolName**屬性**。** 您可以針對此屬性指定集區名稱或集區識別碼。
   4. 輸入 hello 批次 URI hello **batchUri** JSON 屬性。

      > [!IMPORTANT]
      > hello **URL**從 hello **Azure Batch 帳戶 刀鋒視窗**處於 hello 下列格式： \<accountname\>。\<區域\>。 batch.azure.com。Hello **batchUri** hello JSON 屬性，您需要太**移除"accountname。 」** 從 hello 的 URL。 範例：`"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Hello **poolName**屬性，您也可以指定 hello 識別碼 hello 集區，而不是 hello hello 集區的名稱。

      > [!NOTE]
      > hello Data Factory 服務不支援隨選項 Azure 批次的 HDInsight 的一樣。 您只能使用 Azure Data Factory 中自己的 Azure Batch 集區。
      >
      >
   5. 指定**StorageLinkedService** hello **linkedServiceName**屬性。 您 hello 上一個步驟中建立這項連結的服務。 此儲存體會做為檔案和記錄檔的預備區域。
3. 按一下**部署**hello 命令列 toodeploy hello 連結服務。

#### <a name="step-3-create-datasets"></a>步驟 3：建立資料集
在此步驟中，您可以建立資料集 toorepresent 輸入和輸出資料。

#### <a name="create-input-dataset"></a>建立輸入資料集
1. 在 hello**編輯器**hello Data Factory 中，按一下 **新的資料集**上 hello 工具列，並按一下按鈕**Azure Blob 儲存體**從 hello 下拉式選單。
2. 取代下列 JSON 片段 hello hello 右窗格中的 hello JSON:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    您稍後會在本逐步解說建立管線，開始時間為：2015-11-16T00:00:00Z，而結束時間為：2015-11-16T05:00:00Z。 它會排程的 tooproduce 資料**每小時**，因此有 5 個輸入/輸出配量 (之間**00**: 00:00-\> **05**: 00:00)。

    hello**頻率**和**間隔**hello 輸入資料集設定太**小時**和**1**，這表示該 hello 輸入配量是可用每小時。

    以下是 hello 開始時間的每個配量，由表示**SliceStart** hello 上方 JSON 片段中的系統變數。

    | **配量** | **開始時間**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**:00:00 |
    | 2         | 2015-11-16T**01**:00:00 |
    | 3         | 2015-11-16T**02**:00:00 |
    | 4         | 2015-11-16T**03**:00:00 |
    | 5         | 2015-11-16T**04**:00:00 |

    hello **folderPath**使用 hello 年、 月、 日和小時一部分 hello 配量的開始時間的計算 (**SliceStart**)。 因此，以下是輸入的資料夾的對應的 tooa 配量的方式。

    | **配量** | **開始時間**          | **輸入資料夾**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04** |

1. 按一下**部署**hello 工具列 toocreate 且部署 hello **InputDataset**資料表。

#### <a name="create-output-dataset"></a>建立輸出資料集
在此步驟中，您可以建立類型 AzureBlob toorepresent hello 輸出資料的其他資料集。

1. 在 hello**編輯器**hello Data Factory 中，按一下 **新的資料集**上 hello 工具列，並按一下按鈕**Azure Blob 儲存體**從 hello 下拉式選單。
2. 取代下列 JSON 片段 hello hello 右窗格中的 hello JSON:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    為每個輸入配量產生輸出 blob/檔案。 以下是為每個配量命名輸出檔案的方式。 所有的 hello 輸出檔案產生一個輸出資料夾中： `mycontainer\\outputfolder`。

    | **配量** | **開始時間**          | **輸出檔案**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**:00:00 | 2015-11-16-**00.txt** |
    | 2         | 2015-11-16T**01**:00:00 | 2015-11-16-**01.txt** |
    | 3         | 2015-11-16T**02**:00:00 | 2015-11-16-**02.txt** |
    | 4         | 2015-11-16T**03**:00:00 | 2015-11-16-**03.txt** |
    | 5         | 2015-11-16T**04**:00:00 | 2015-11-16-**04.txt** |

    請記住所有 hello 輸入的資料夾中的檔案 (例如： 2015年-11-16-00) 屬於 hello 的開始時間配量： 2015年-11-16-00。 此配量處理時，hello 自訂活動會掃描每個檔案，並產生 hello 與 hello 發生次數的搜尋詞彙 ("Microsoft") 的輸出檔中的資料行。 Hello 輸出檔 hello 資料夾 2015年-11-16-00 中有三個檔案，如果有三個行： 2015年-11-16-00.txt。

1. 按一下**部署**hello 工具列 toocreate 且部署 hello **OutputDataset**。

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>步驟 4： 建立和執行自訂活動與 hello 管線
在此步驟中，您可以建立管線某個活動，hello 您稍早建立的自訂活動。

> [!IMPORTANT]
> 如果尚未上傳 hello **file.txt** tooinput 資料夾在 hello blob 容器中，建立 hello 管線之前執行此動作。 hello **isPaused**屬性設定 toofalse hello 管線 JSON，因此 hello 管線便會立即執行為 hello**啟動**日期為過去的 hello。
>
>

1. 在 hello Data Factory 編輯器中，按一下 **新管線**hello 命令列上。 如果看不到 hello 命令，請按一下**...（省略符號）** toosee 它。
2. 取代下列 JSON 指令碼的 hello hello 右窗格中的 hello JSON:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   請注意下列點 hello:

   * Hello 管線中只能有一個活動，而且型別的： **DotNetActivity**。
   * **AssemblyName**設定 toohello hello DLL 名稱： **MyDotNetActivity.dll**。
   * **EntryPoint**設定得**MyDotNetActivityNS.MyDotNetActivity**。 在您的程式碼中，它基本上是 \<namespace\>.\<classname\>。
   * **PackageLinkedService**設定得**StorageLinkedService** ，以指 toohello blob 儲存體包含 hello 自訂活動的 zip 檔案。 如果您使用不同的 Azure 儲存體帳戶輸入/輸出檔案和 hello 自訂活動的 zip 檔案，您必須 toocreate 另一個 Azure 儲存體連結服務。 本文假設您使用 hello 相同的 Azure 儲存體帳戶。
   * **PackageFile**設定得**customactivitycontainer/MyDotNetActivity.zip**。 其為 hello 格式： \<containerforthezip\>/\<nameofthezip.zip\>。
   * hello 自訂活動會採用**InputDataset**做為輸入和**OutputDataset**做為輸出。
   * hello **linkedServiceName** hello 自訂活動的屬性指向 toohello **AzureBatchLinkedService**，它會告訴 Azure Data Factory 的 hello 自訂活動必須 toorun Azure 批次。
   * hello**並行**設定很重要。 如果您使用 hello 預設值為 1，即使您有 2 或多個計算節點 hello Azure Batch 集區中的，會處理 hello 配量一個接著一個。 因此，您就不可以運用 Azure 批次的 hello 平行處理功能。 如果您設定**並行**tooa 較高的值，例如 2，表示兩個配量 （對應 tootwo Azure 批次中的工作） 可以在 hello 處理相同的時間，在此情況下，這兩個 hello 中的 Vm hello Azure Batch 集區並加以使用。 因此，適當地設定 hello 並行屬性。
   * 根據預設，無論何時，一個工作 (配量) 都只會在一個 VM 上執行。 hello 原因在於，根據預設，hello**每個 VM 的最大工作**too1 Azure Batch 集區設定。 必要條件的一部分，您建立了集區與這個屬性集 too2，讓兩個 Data Factory 配量可在 hello VM 上執行相同的時間。

    -   **isPaused**屬性 toofalse 預設設定。 hello 管線執行立即在此範例中，因為 hello 配量開始在過去的 hello。 您可以設定這個屬性 tootrue toopause hello 管線，並將它回復 toofalse toorestart。

    -   hello**啟動**時間和**結束**時間是 5 小時以上距離而配量不會產生每小時，因此 hello 管線所產生五個配量。

1. 按一下**部署**hello 命令列 toodeploy hello 管線。

#### <a name="step-5-test-hello-pipeline"></a>步驟 5： 測試 hello 管線
在此步驟中，您測試管線 hello 放 hello 輸入資料夾的檔案。 讓我們開頭為測試 hello 管線每一個輸入資料夾的一個檔案。

1. 在 hello Data Factory 刀鋒視窗中 hello Azure 入口網站中，按一下 **圖表**。

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. 在 hello 圖表檢視中，按兩下 輸入資料集： **InputDataset**。

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. 您應該會看見 hello **InputDataset**刀鋒視窗的全部五個配量的準備。 請注意 hello**配量的開始時間**和**配量結束時間**每個配量。

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. 在 hello**圖表檢視**，現在按一下**OutputDataset**。
5. 您應該會看到 hello 五個輸出配量會 hello 就緒狀態，是否他們已經產生。

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. 使用 Azure 入口網站 tooview hello**工作**hello 與相關聯**配量**並查看哪些 VM 執行的每個配量。 請參閱 [Data Factory 和 Batch 整合](#data-factory-and-batch-integration) 一節，以取得詳細資料。
7. 您應該會看到 hello 輸出檔中 hello`outputfolder`的`mycontainer`在您的 Azure blob 儲存體。

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   您應會看見五個輸出檔案，每個輸入配量各一個。 每個 hello 輸出檔案應該具有內容的類似 toohello 下列輸出：

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   hello 下列圖表說明 hello Data Factory 配量將 tootasks Azure 批次中的對應。 在此範例中，一個配量只有一個執行。

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. 現在，我們要以一個資料夾包含多個檔案的方式來試試。 建立檔案： **file2.txt**， **file3.txt**， **file4.txt**，和**file5.txt** hello 與相同內容如 file.txt hello 資料夾中所示：**2015年-11-06-01**。
9. 在 hello 輸出資料夾中，**刪除**hello 輸出檔： **2015年-11-16-01.txt**。
10. 現在，在 hello **OutputDataset**刀鋒視窗中，以滑鼠右鍵按一下 hello 配量與**配量的開始時間**設定得**2015 年 11 月 16 日 01:00:00 AM**，然後按一下**執行**toorerun/重新 process hello 配量。 現在，hello 配量會有五個檔案，而不是一個檔案。

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Hello 配量執行，其狀態為之後**準備**，確認此配量的 hello 輸出檔中的 hello 內容 (**2015年-11-16-01.txt**) 在 hello`outputfolder`的`mycontainer`在您的 blob 儲存體。 應該要有每個檔案的 hello 配量的線。

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> 如果您未刪除 hello 輸出檔案 2015年-11-16-01.txt 嘗試以五個輸入檔案之前，您會看到從 hello 先前配量執行一行和五行 hello 目前配量執行中。 根據預設，hello 內容是附加的 toooutput 檔案已經存在。
>
>

#### <a name="data-factory-and-batch-integration"></a>Data Factory 和 Batch 整合
hello Data Factory 服務 Azure 批次中建立工作以 hello 名稱： `adf-poolname:job-xxx`。

![Azure Data Factory - Batch 作業](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

配量的每個活動執行時，會建立 hello 作業中的工作。 如果有 10 個配量準備 toobe 處理，10 個工作會建立 hello 作業中。 您可以有多個配量，以平行方式執行，如果您有多個計算節點區內 hello。 如果 hello 最大的工作，每個計算節點設定得 > 1，可以有超過一個配量上 hello 執行相同的計算。

此範例中有 5 個配量，所以 Azure Batch 中有 5 個工作。 以 hello**並行**設定得**5** hello 在管線中 Azure Data Factory JSON 和**每個 VM 的最大工作**設定得**2** Azure 批次中集區**2** hello 工作執行快速 （檢查工作的開始和結束時間） 的 Vm。

使用 hello 入口 tooview hello 批次工作和其相關聯之工作與 hello**配量**並查看哪些 VM 執行的每個配量。

![Azure Data Factory - Batch 作業工作](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>偵錯 hello 管線
偵錯包含一些基本技術：

1. 如果未設定 hello 輸入配量太**準備**，確認 hello 輸入的資料夾結構是否正確，以及 file.txt 存在 hello 輸入資料夾中。

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. 在 hello **Execute**方法的自訂活動，使用 hello **IActivityLogger**物件 toolog 資訊可協助您疑難排解問題。 記錄的 hello 訊息顯示在 hello 使用者\_0 記錄檔。

   在 hello **OutputDataset**刀鋒視窗中，按一下 hello 配量 toosee hello**資料配量**刀鋒視窗，該配量。 您會看到該配量的 [活動執行]。 您應該會看到一個 hello 配量執行的活動。 如果您按一下**執行**hello 命令列中，您可以啟動另一個活動執行 hello 相同配量。

   當您按一下 hello 活動執行時，請參閱 hello**活動執行詳細資料**刀鋒視窗的記錄檔的清單。 您會看到記錄的訊息，在 hello**使用者\_0 記錄**檔案。 當發生錯誤時，因為 hello 重試計數設定 too3 hello 管線/活動 JSON 中會看到三個活動執行。 當您按一下 hello 活動執行時，您會看到 hello 記錄檔，您可以檢閱 tootroubleshoot hello 錯誤。

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   在 hello 清單中的記錄檔，按一下 hello**使用者 0.log**。 Hello 右面板中會使用 hello 的 hello 結果**IActivityLogger.Write**方法。

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   檢查 system-0.log 是否有任何系統錯誤訊息和例外狀況。

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. 包含 hello **PDB**檔案 hello zip 檔案中，所以 hello 錯誤詳細資料會有這類資訊**呼叫堆疊**發生的錯誤。
4. 所有 hello hello zip 檔案中的 hello 自訂活動必須是在 hello**上層**具有任何子資料夾。

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. 請確定該 hello **assemblyName** (MyDotNetActivity.dll)， **entryPoint** (MyDotNetActivityNS.MyDotNetActivity)， **packageFile** (customactivitycontainer /MyDotNetActivity.zip) 和**packageLinkedService** (應該點 toohello Azure blob 儲存體包含 hello zip 檔案) 會設定 toocorrect 值。
6. 如果您修正錯誤，且想 tooreprocess hello 配量，以滑鼠右鍵按一下 hello 配量在 hello **OutputDataset**刀鋒視窗，然後按一下**執行**。

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > 您會在 Azure Blob 儲存體中看到一個**容器**，名為：`adfjobs`。 不會自動刪除此容器，但您在完成測試 hello 方案之後可以安全地刪除。 同樣地，hello Data Factory 方案建立 Azure 批次**作業**名為： `adf-\<pool ID/name\>:job-0000000001`。 如果您想測試 hello 方案之後，您可以刪除此作業。
   >
   >
7. hello 自訂活動不會使用 hello **app.config**檔案從您的封裝。 因此，如果您的程式碼會讀取 hello 組態檔中的任何連接字串，因此無法在執行階段。 hello 最佳作法是當使用 Azure Batch toohold 中的秘密**Azure KeyVault**、 使用憑證為基礎的服務主體 tooprotect hello 所以 keyvault，及散布 hello 憑證 tooAzure 批次集區。 hello.NET 自訂活動，則可以從 hello KeyVault 在執行階段存取機密資料。 這個解決方案是泛型，而且可以延展 tooany 類型的密碼，而不只是連接字串。

    沒有簡單的因應措施 （但不是最佳作法）： 您可以建立**Azure SQL 連結服務**與連接字串設定，建立使用 hello 連結的服務，以及鏈結 hello 資料集做為虛擬輸入資料集的資料集自訂.NET 活動 toohello。 接著，您可以存取 hello 連結服務的連接字串 hello 自訂活動程式碼中，且它應該在執行階段可以正常運作。  

#### <a name="extend-hello-sample"></a>擴充 hello 範例
您可以擴充此範例 toolearn 有關 Azure Data Factory 和 Azure 批次功能的詳細資訊。 例如，tooprocess 配量在不同的時間範圍中，請勿 hello 下列步驟：

1. 新增下列子資料夾中 hello hello `inputfolder`: 2015年-11-16-05，2015年-11-16-06，201-11-16-07，2011年-11-16-08 版 2015年-11-16-09 並放置在輸入檔在這些資料夾中的。 變更 hello 管線就會從 hello 結束時間`2015-11-16T05:00:00Z`太`2015-11-16T10:00:00Z`。 在 hello**圖表檢視**，按兩下 hello **InputDataset**，並確認已準備 hello 輸入配量。 按兩下**OuptutDataset** toosee hello 輸出配量狀態。 如果它們都處於就緒狀態，請檢查 hello hello 輸出檔的輸出資料夾。
2. 增加或減少 hello**並行**設定 toounderstand 它會如何影響您的方案，hello 效能特別 hello 處理 Azure 批次上發生。 (請參閱步驟 4： 建立和執行 hello 管線，如需有關 hello**並行**設定。)
3. 建立 [每個 VM 的工作數上限] 較低/較高的集區。 toouse hello 新集區在建立時，更新 hello hello Data Factory 方案中的 Azure Batch 連結服務。 (請參閱步驟 4： 建立和執行 hello 管線，如需有關 hello**每個 VM 的最大工作**設定。)
4. 建立具有 **自動調整** 功能的 Azure Batch 集區。 自動調整 Azure Batch 集區中的計算節點是 hello 動態調整處理能力，您的應用程式所使用。 

    hello 範例公式會達到 hello 下列行為： 一開始建立 hello 集區時，開始的 1 的 VM。 $PendingTasks 度量定義 hello 數項工作中執行 + （佇列） 的作用中狀態。  hello 公式中 hello 過去 180 秒尋找 hello 的平均數目暫止的工作，並據此設定 TargetDedicated。 它會確保 TargetDedicated 一律不會超過 25 部 VM。 因此，提交新的工作，因為集區自動成長和做為工作完成，Vm 會變成可用逐一和 hello 自動調整壓縮這些 Vm。 startingNumberOfVMs 和 maxNumberofVMs 可以調整的 tooyour 需求。
 
    自動調整公式：

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的計算節點](../batch/batch-automatic-scaling.md) 。

   如果 hello 集區使用 hello 預設[autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)，hello 批次服務可能需要 15 到 30 分鐘 tooprepare hello VM，然後再執行 hello 自訂活動。  如果 hello 集區使用不同的 autoScaleEvaluationInterval，hello 批次服務可能需要 autoScaleEvaluationInterval + 10 分鐘。
5. 在 hello 範例解決方案中，hello **Execute**方法會叫用 hello **Calculate**方法，以處理輸入的資料配量 tooproduce 輸出資料配量。 您可以撰寫您自己的方法 tooprocess 輸入資料，並以呼叫 tooyour 方法取代 hello Execute 方法中的 hello Calculate 方法呼叫。

### <a name="next-steps-consume-hello-data"></a>後續步驟： 取用 hello 資料
處理資料之後，您可以使用 **Microsoft Power BI** 之類的線上工具來取用資料。 以下是您了解 Power BI 連結 toohelp 以及 toouse 它在 Azure 中：

* [在 Power BI 中探索資料集](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [開始使用 Power BI Desktop hello](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [重新整理 Power BI 中的資料](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure 和 Power BI - 基本概觀](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>參考
* [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

  * [簡介 tooAzure Data Factory 服務](data-factory-introduction.md)
  * [開始使用 Azure Data Factory](data-factory-build-your-first-pipeline.md)
  * [在 Azure 資料處理站管線中使用自訂活動](data-factory-use-custom-activities.md)
* [Azure Batch](https://azure.microsoft.com/documentation/services/batch/)

  * [Azure Batch 的基本概念](../batch/batch-technical-overview.md)
  * [Azure Batch 功能概觀](../batch/batch-api-basics.md)
  * [建立和管理 Azure Batch 帳戶在 hello Azure 入口網站](../batch/batch-account-create-portal.md)
  * [開始使用 Azure Batch 程式庫 .NET](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
