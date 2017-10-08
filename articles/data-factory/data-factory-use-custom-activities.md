---
title: "aaaUse Azure Data Factory 管線中的自訂活動"
description: "深入了解如何 toocreate 自訂活動和在 Azure Data Factory 管線中使用它們。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a>在 Azure 資料處理站管線中使用自訂活動

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 活動](data-factory-hive-activity.md) 
> * [Pig 活動](data-factory-pig-activity.md)
> * [MapReduce 活動](data-factory-map-reduce.md)
> * [Hadoop 串流活動](data-factory-hadoop-streaming-activity.md)
> * [Spark 活動](data-factory-spark.md)
> * [Machine Learning Batch 執行活動](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 更新資源活動](data-factory-azure-ml-update-resource-activity.md)
> * [預存程序活動](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 活動](data-factory-usql-activity.md)
> * [.NET 自訂活動](data-factory-use-custom-activities.md)

您可以在 Azure Data Factory 管線中使用兩種活動。

- [資料移動活動](data-factory-data-movement-activities.md)toomove 資料之間[支援來源和接收的資料存放區](data-factory-data-movement-activities.md#supported-data-stores-and-formats)。
- [資料轉換活動](data-factory-data-transformation-activities.md)tootransform 資料使用 compute 的 Azure HDInsight、 Azure Batch 和 Azure Machine Learning 等服務。 

toomove 資料，從 Data Factory 不支援，資料存放區建立**自訂活動**您自己的資料移動邏輯和使用 hello 活動的管線。 同樣地，tootransform/處理的方式不支援的 Data Factory 中的資料建立您自己的資料轉換邏輯的自訂活動，並在管線中使用 hello 活動。 

您可以設定自訂活動 toorun **Azure Batch**的虛擬機器，或以 Windows 為基礎的集區**Azure HDInsight**叢集。 當使用 Azure Batch 時，您只可以使用現有的 Azure Batch 集區。 然而，使用 HDInsight 時，您可以使用現有的 HDInsight 叢集或針對您在執行階段的隨選自動建立叢集。  

hello 下列逐步解說提供逐步指示，建立自訂的.NET 活動和管線中使用 hello 自訂活動。 hello 逐步解說會使用**Azure Batch**連結服務。 請改用 toouse Azure HDInsight 連結服務，您可以建立連結的服務型別的**HDInsight** （您自己的 HDInsight 叢集） 或**HDInsightOnDemand** （Data Factory 建立的 HDInsight 叢集依需求）。 然後，設定自訂活動 toouse hello HDInsight 連結服務。 請參閱[使用 Azure HDInsight 連結服務](#use-hdinsight-compute-service)一節以取得有關使用 Azure HDInsight toorun hello 自訂活動的詳細資料。

> [!IMPORTANT]
> - 只在 Windows 為基礎的 HDInsight 叢集上執行自訂.NET 活動 hello。 這項限制的因應措施為 toouse hello 對應減少活動 toorun 自訂 Java 程式碼以 Linux 為基礎的 HDInsight 叢集上。 另一個選項是 toouse Vm toorun 自訂活動而不是使用 HDInsight 叢集的 Azure Batch 集區。
> - 不可能 toouse 從自訂活動 tooaccess 在內部部署資料來源的資料管理閘道。 目前，[資料管理閘道器](data-factory-data-management-gateway.md)僅支援 hello 複製活動和預存程序活動 Data Factory 中。   

## <a name="walkthrough-create-a-custom-activity"></a>逐步解說：建立自訂活動
### <a name="prerequisites"></a>必要條件
* Visual Studio 2012/2013/2015
* 下載並安裝 [Azure .NET SDK](https://azure.microsoft.com/downloads/)

### <a name="azure-batch-prerequisites"></a>Azure Batch 的必要條件
Hello 逐步解說中，您可以執行您使用 Azure Batch 計算資源做的自訂.NET 活動。 **Azure 批次**是平台服務的執行大規模的平行和高效能運算 (HPC) 應用程式有效率地在 hello 雲端中的。 Azure 批次排程需要大量計算工作 toorun 上 managed**的虛擬機器集合**，並可自動調整計算資源 toomeet hello 需求的工作。 請參閱[Azure Batch 基本概念][ batch-technical-overview] hello Azure 批次服務的發行項的詳細概觀。

Hello 教學課程中，建立 Azure 批次帳戶與 Vm 的集區。 Hello 步驟如下：

1. 建立**Azure Batch 帳戶**使用 hello [Azure 入口網站](http://portal.azure.com)。 請參閱[建立和管理 Azure Batch 帳戶][batch-create-account]一文以取得指示。
2. 記下 hello Azure Batch 帳戶名稱、 帳戶金鑰，URI 和集區名稱。 您需要它們 toocreate Azure Batch 連結服務。
    1. 在 Azure Batch 帳戶的 hello 首頁上，您會看到**URL**在 hello 下列格式： `https://myaccount.westus.batch.azure.com`。 在此範例中， **myaccount** hello hello Azure Batch 帳戶名稱。 您在連結的 hello 服務定義中使用的 URI 是 hello 的 URL 不 hello hello 帳戶名稱。 例如： `https://<region>.batch.azure.com`。
    2. 按一下**金鑰**hello 左的窗格中，以及複製 hello**主要存取金鑰**。
    3. toouse 現有集區，按一下**集區**上 hello 功能表上，並記下 hello**識別碼**hello 集區。 如果您沒有現有的集區，移動 toohello 下一個步驟。     
2. 建立 **Azure Batch 集區**。

   1. 在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **瀏覽**在 hello 左的窗格中，然後按一下**批次帳戶**。
   2. 選取您的 Azure Batch 帳戶 tooopen hello**批次帳戶**刀鋒視窗。
   3. 按一下 [集區]  圖格。
   4. 在 hello**集區**刀鋒視窗中，按一下 hello 工具列 tooadd 集區中的 新增 按鈕。
      1. 請輸入 hello 集區 （集區識別碼） 的識別碼。 請注意 hello **hello 集區的識別碼**; 時，您需要它建立 hello Data Factory 方案。
      2. 指定**Windows Server 2012 R2** hello 作業系統系列設定。
      3. 選取 **節點定價層**。
      4. 輸入**2**做為 hello 值**目標專用**設定。
      5. 輸入**2**做為 hello 值**每個節點的最大工作**設定。
   5. 按一下**確定**toocreate hello 集區。
   6. 記下 hello**識別碼**hello 集區。 



### <a name="high-level-steps"></a>高階步驟
以下是兩個 hello 您執行本逐步解說中為概要步驟： 

1. 建立包含簡單資料轉換/處理邏輯的自訂活動。
2. 建立 Azure data factory 管線，使用 hello 自訂活動。

### <a name="create-a-custom-activity"></a>建立自訂活動
toocreate.NET 自訂活動，建立**.NET 類別庫**所實作的類別具有專案**IDotNetActivity**介面。 這個介面只有一個方法： [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) ，其簽章為：

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


hello 方法會採用四個參數：

- **linkedServices**。 這個屬性是 hello 活動的輸入/輸出資料集所參考的資料存放區連結服務的可列舉清單。   
- **資料集**。 這個屬性是 hello 活動的輸入/輸出資料集的可列舉清單。 您可以使用此參數 tooget hello 位置以及輸入和輸出資料集所定義的結構描述。
- **活動**。 這個屬性代表 hello 目前活動。 它可以是使用的 tooaccess 擴充 hello 自訂活動相關聯的屬性。 如需詳細資訊，請參閱[存取延伸屬性](#access-extended-properties)。
- **記錄器**。 此物件可讓您撰寫偵錯註解的設定，該介面 hello 使用者記錄檔中的 hello 管線。

hello 方法會傳回可使用的 toochain 自訂活動運算子 hello 未來的字典。 尚未實作這項功能，因此從 hello 方法會傳回空的字典。  

### <a name="procedure"></a>程序
1. 建立 **.NET 類別庫** 專案。
   <ol type="a">
     <li>啟動 <b>Visual Studio 2017</b> 或 <b>Visual Studio 2015</b> 或 <b>Visual Studio 2013</b> 或 <b>Visual Studio 2012</b>。</li>
     <li>按一下<b>檔案</b>，點太<b>新增</b>，然後按一下<b>專案</b>。</li>
     <li>展開 [範本]<b></b>，然後選取 [Visual C#]<b></b>。 在本逐步解說，您使用 C# 中，但您可以使用任何.NET 語言 toodevelop hello 自訂活動。</li>
     <li>選取<b>類別庫</b>從 hello hello 右上的專案類型清單。 在 VS 2017 中，選擇 <b>類別庫 (.NET Framework)</b> </li>
     <li>輸入<b>MyDotNetActivity</b> hello<b>名稱</b>。</li>
     <li>選取<b>C:\ADFGetStarted</b> hello<b>位置</b>。</li>
     <li>按一下<b>確定</b>toocreate hello 專案。</li>
   </ol>
2.按一下**工具**，點太**NuGet 套件管理員**，然後按一下**Package Manager Console**。
3. 在 hello Package Manager Console 中，執行下列命令 tooimport hello **Microsoft.Azure.Management.DataFactories**。

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. 匯入 hello **Azure 儲存體**toohello 專案中的 NuGet 封裝。

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > 資料處理站服務啟動器需要 WindowsAzure.Storage hello 4.3 版本。 如果您加入參考 tooa 更新您的自訂活動專案中的 Azure 儲存體組件的版本，您看到錯誤 hello 活動執行時。 tooresolve hello 錯誤，請參閱[Appdomain 隔離](#appdomain-isolation)> 一節。 
5. 新增下列 hello**使用**hello 專案中的陳述式 toohello 來源檔案。

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. 變更 hello 名稱的 hello**命名空間**太**MyDotNetActivityNS**。

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. 變更 hello hello 類別名稱太**MyDotNetActivity**從其中 hello **IDotNetActivity**介面 hello 下列程式碼片段所示：

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. 實作 （加入） hello **Execute**方法 hello **IDotNetActivity**介面 toohello **MyDotNetActivity**類別，並複製下列範例程式碼 toohello 方法的 hello。

    hello 下列範例會計算 hello 次數 hello 搜尋詞彙 ("Microsoft") 中相關聯的資料配量每個 blob。

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
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
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
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
9. 新增下列 helper 方法的 hello: 

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

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
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
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
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

    hello GetFolderPath 方法傳回 hello 路徑 toohello 資料夾 hello 資料集點 tooand hello GetFileName 方法傳回 hello hello blob 檔案的名稱/的 hello 指向資料集。 如果您 havefolderPath 定義使用變數，例如 {Year}，{Month}，{Day} 等等 hello 方法傳回 hello 字串，因為它是不使用執行階段值來取代它們。 如需存取 SliceStart、SliceEnd 等的詳細資料，請參閱 [存取延伸屬性](#access-extended-properties) 一節。    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    hello Calculate 方法計算 hello 關鍵字 Microsoft hello 輸入檔 (hello 資料夾中的 blob) 中的執行個體數目。 hello 搜尋詞彙 ("Microsoft") 是硬式編碼 hello 程式碼中。
10. 編譯 hello 專案。 按一下**建置**從 hello 功能表，然後按一下**建置方案**。

    > [!IMPORTANT]
    > 集合 4.5.2 做 hello 專案的目標 framework 的.NET Framework 版本： hello 專案上按一下滑鼠右鍵，然後按一下**屬性**tooset hello 目標架構。 Data Factory 不支援針對 .NET Framework 4.5.2 版之後的版本編譯的自訂活動。

11. 啟動**Windows 檔案總管**，並瀏覽過**bin\debug**或**bin\release**資料夾視 hello 組建類型而定。
12. 建立 zip 檔案**MyDotNetActivity.zip** ，其中包含所有的 hello 二進位碼檔案中 hello <project folder>\bin\Debug 資料夾。 包含 hello **MyDotNetActivity.pdb**檔案，以便您在 hello hello 問題的原因，如果發生失敗的程式碼中取得其他詳細資料，例如行號。 

    > [!IMPORTANT]
    > 所有 hello hello zip 檔案中的 hello 自訂活動必須是在 hello**上層**與任何子資料夾。

    ![二進位輸出檔案](./media/data-factory-use-custom-activities/Binaries.png)
14. 如果名為 **customactivitycontainer** 的 Blob 容器不存在，請自行建立。 
15. 以 blob toohello customactivitycontainer 中上傳 MyDotNetActivity.zip**一般用途**稱為 AzureStorageLinkedService 的 Azure blob 儲存體 （不熱/cool Blob 儲存）。  

> [!IMPORTANT]
> 如果您將.NET 活動專案 tooa 方案加入包含 Data Factory 專案的 Visual Studio 中，並新增參考 too.NET activity 專案從 hello Data Factory 應用程式專案，您不需要手動建立 tooperform hello 最後兩個的步驟hello zip 檔案，並將它上傳 toohello 一般用途的 Azure blob 儲存體。 當您發佈使用 Visual Studio 的 Data Factory 實體時，會自動由 hello 發佈程序完成這些步驟。 如需詳細資訊，請參閱[Visual Studio 中的 Data Factory 專案](#data-factory-project-in-visual-studio)一節。

## <a name="create-a-pipeline-with-custom-activity"></a>建立具有自訂活動的管線
您已建立的自訂活動，並上傳與二進位檔 tooa blob 容器中的 hello zip 檔案**一般用途**Azure 儲存體帳戶。 本節中，在中，您可以建立 Azure data factory 管線，使用 hello 自訂活動。

hello hello 自訂活動的輸入資料集代表 adftutorial hello blob 儲存體容器中的 hello customactivityinput 資料夾中的 blob （檔案）。 hello hello 活動的輸出資料集代表 adftutorial hello blob 儲存體容器中的 hello customactivityoutput 資料夾中輸出 blob。

建立**file.txt**檔案以下列內容，並將它上傳太 hello**customactivityinput**資料夾 hello **adftutorial**容器。 如果它已不存在，請建立 hello adftutorial 容器。 

```
test custom activity Microsoft test custom activity Microsoft
```

hello 輸入的資料夾對應 tooa Azure Data Factory 中的配量，即使 hello 資料夾有兩個或多個檔案。 Hello 管線處理每個配量時，該配量的 hello 輸入資料夾中的所有 hello blob 會都重複 hello 自訂活動。

您會看到一個輸出與 hello adftutorial\customactivityoutput 資料夾中的檔案與一或多行 （與 hello 輸入資料夾中的 blob 數目相同）：

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


執行本節中的 hello 步驟如下：

1. 建立 **Data Factory**。
2. 建立**連結的服務**hello Azure Batch 集區的 Vm 上的 hello 自訂活動會執行並 hello 保存 hello 輸入/輸出 blob 的 Azure 儲存體。
3. 建立輸入和輸出**資料集**代表輸入和輸出 hello 自訂活動。
4. 建立**管線**使用 hello 自訂活動。

> [!NOTE]
> 建立 hello **file.txt**並將它上載 tooa blob 容器，如果您還沒有。 請參閱 hello 前面一節中的指示。   

### <a name="step-1-create-hello-data-factory"></a>步驟 1： 建立 hello 資料處理站
1. 登入之後 toohello Azure 入口網站，請勿 hello 下列步驟：
   1. 按一下**新增**hello 左側功能表上。
   2. 按一下**資料 + 分析**在 hello**新增**刀鋒視窗。
   3. 按一下**Data Factory**上 hello**資料分析**刀鋒視窗。
   
    ![新增 Azure Data Factory 功能表](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. 在 hello**新的 data factory**刀鋒視窗中，輸入**CustomActivityFactory** hello 名稱。 hello hello Azure data factory 的名稱必須是全域唯一的。 如果您收到 hello 錯誤： **Data factory 名稱"CustomActivityFactory"不是使用**，變更 hello hello data factory 名稱 (例如， **yournameCustomActivityFactory**)，然後再次嘗試建立一次。

    ![新增 Azure Data Factory 刀鋒視窗](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. 按一下 [資源群組名稱] ，並選取現有的資源群組，或建立一個群組。
4. 確認您是否使用正確的 hello**訂用帳戶**和**區域**您想要建立 hello 資料 factory toobe。
5. 按一下**建立**上 hello**新的 data factory**刀鋒視窗。
6. 您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站。
7. 已成功建立 hello 資料處理站之後，您會看到 hello Data Factory 刀鋒視窗中，它會顯示 hello hello data factory 的內容。
    
    ![Data Factory 刀鋒視窗](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a>步驟 2：建立連結服務
連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。 在此步驟中，您必須連結您的 Azure 儲存體帳戶和 Azure Batch 帳戶 tooyour 資料 factory。

#### <a name="create-azure-storage-linked-service"></a>建立 Azure 儲存體連結服務
1. 按一下 hello**作者及部署**磚 hello **DATA FACTORY**刀鋒伺服器**CustomActivityFactory**。 您會看到 hello Data Factory 編輯器。
2. 按一下**新建資料存放區**在 hello 命令列，然後選擇  **Azure 儲存體**。 您應該會看見 hello JSON 指令碼來建立 Azure 儲存體已連結的 hello 編輯器中的服務。
    
    ![新增資料存放區 - Azure 儲存體](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. 取代`<accountname>`與您的 Azure 儲存體帳戶名稱和`<accountkey>`hello Azure 儲存體帳戶的存取金鑰。 toolearn 如何 tooget 您的儲存體存取金鑰，請參閱[檢視、 複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。

    ![Azure 儲存體類型的連結服務](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. 按一下**部署**hello 命令列 toodeploy hello 連結服務。

#### <a name="create-azure-batch-linked-service"></a>建立 Azure Batch 連結服務
1. 在 hello Data Factory 編輯器中，按一下  **...多個**hello 命令列上，按一下**新計算**，然後選取**Azure Batch** hello 功能表。

    ![[新增計算]-[Azure 批次]](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. 進行下列變更 toohello JSON 指令碼的 hello:

   1. 指定 Azure Batch 帳戶名稱 hello **accountName**屬性。 hello **URL**從 hello **Azure Batch 帳戶 刀鋒視窗**處於 hello 下列格式： `http://accountname.region.batch.azure.com`。 Hello **batchUri**屬性在 hello JSON，您需要 tooremove`accountname.`從 hello URL 和使用 hello `accountname` hello `accountName` JSON 屬性。
   2. 指定 hello hello Azure Batch 帳戶金鑰**accessKey**屬性。
   3. Hello hello 您所建立的集區名稱指定為組件的必要條件 hello **poolName**屬性。 您也可以指定 hello 識別碼 hello 集區，而不是 hello hello 集區的名稱。
   4. 指定 Azure 批次 URI hello **batchUri**屬性。 範例：`https://westus.batch.azure.com`.  
   5. 指定 hello **AzureStorageLinkedService** hello **linkedServiceName**屬性。

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       Hello **poolName**屬性，您也可以指定 hello 識別碼 hello 集區，而不是 hello hello 集區的名稱。

      > [!IMPORTANT]
      > hello Data Factory 服務不支援隨選項 Azure 批次的 HDInsight 的一樣。 您只能使用 Azure Data Factory 中自己的 Azure Batch 集區。   
    

### <a name="step-3-create-datasets"></a>步驟 3：建立資料集
在此步驟中，您可以建立資料集 toorepresent 輸入和輸出資料。

#### <a name="create-input-dataset"></a>建立輸入資料集
1. 在 hello**編輯器**hello Data Factory 中，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**從 hello 下拉式選單。
2. 取代下列 JSON 片段 hello hello 右窗格中的 hello JSON:

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
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

   您稍後會在本逐步解說建立管線，開始時間為：2016-11-16T00:00:00Z，而結束時間為：2016-11-16T05:00:00Z。 它是排程的 tooproduce 資料每小時，因此有五個輸入/輸出配量 (之間**00**: 00:00]-> [ **05**: 00:00)。

   hello**頻率**和**間隔**hello 輸入資料集設定太**小時**和**1**，這表示該 hello 輸入配量是可用每小時。 在此範例中，它是相同的 hello hello intputfolder 中的檔案 (.txt)。

   以下是 hello SliceStart hello 上方 JSON 片段中的系統變數由每個配量的開始時間。
3. 按一下**部署**hello 工具列 toocreate 且部署 hello **InputDataset**。 確認您看到 hello**資料表成功建立**hello 編輯器 hello 標題列上的訊息。

#### <a name="create-an-output-dataset"></a>建立輸出資料表
1. 在 hello **Data Factory 編輯器**，按一下  **...多個**hello 命令列上，按一下**新的資料集**，然後選取**Azure Blob 儲存體**。
2. 取代下列 JSON 指令碼的 hello hello 右窗格中的 hello JSON 指令碼：

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
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

     輸出位置是**adftutorial/customactivityoutput/**和輸出檔名稱是 yyyy 公釐-dd HH.txt，其中 yyyy 公釐-dd HH 是 hello 年、 月、 日、 小時 hello 配量所產生。 如需詳細資訊，請參閱[開發人員參考資料][adf-developer-reference]。

    為每個輸入配量產生輸出 blob/檔案。 以下是為每個配量命名輸出檔案的方式。 所有的 hello 輸出檔案產生一個輸出資料夾中： **adftutorial\customactivityoutput**。

   | 配量 | 開始時間 | 輸出檔案 |
   |:--- |:--- |:--- |
   | 1 |2016-11-16T00:00:00 |2016-11-16-00.txt |
   | 2 |2016-11-16T01:00:00 |2016-11-16-01.txt |
   | 3 |2016-11-16T02:00:00 |2016-11-16-02.txt |
   | 4 |2016-11-16T03:00:00 |2016-11-16-03.txt |
   | 5 |2016-11-16T04:00:00 |2016-11-16-04.txt |

    請記住，所有輸入的資料夾中的 hello 檔案會與上面提到的 hello 開始時間配量的一部分。 此配量處理時，hello 自訂活動會掃描每個檔案，並產生 hello 與 hello 發生次數的搜尋詞彙 ("Microsoft") 的輸出檔中的資料行。 每個每小時的配量的 hello 輸出檔 hello inputfolder 中有三個檔案，如果有三個行： 2016年-11-16-00.txt，2016年-11-16:01:00:00.txt，等等。
3. toodeploy hello **OutputDataset**，按一下 **部署**hello 命令列上。

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a>建立並執行管線的使用 hello 自訂活動
1. 在 hello Data Factory 編輯器中，按一下  **...多個**，然後選取**新管線**hello 命令列上。 
2. 取代下列 JSON 指令碼的 hello hello 右窗格中的 hello JSON:

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    請注意下列點 hello:

   * **並行**設定得**2**以便由 2 個 Vm hello Azure Batch 集區中，兩個配量會平行處理。
   * Hello 活動 > 一節中一個活動，而且它是型別： **DotNetActivity**。
   * **AssemblyName**設定 toohello hello DLL 名稱： **MyDotnetActivity.dll**。
   * **EntryPoint**設定得**MyDotNetActivityNS.MyDotNetActivity**。
   * **PackageLinkedService**設定得**AzureStorageLinkedService** ，以指 toohello blob 儲存體包含 hello 自訂活動的 zip 檔案。 如果您使用不同的 Azure 儲存體帳戶，來輸入/輸出檔案而且 hello 自訂活動 zip 檔，您建立另一個 Azure 儲存體連結服務。 本文假設您使用 hello 相同的 Azure 儲存體帳戶。
   * **PackageFile**設定得**customactivitycontainer/MyDotNetActivity.zip**。 其為 hello 格式： containerforthezip/nameofthezip.zip。
   * hello 自訂活動會採用**InputDataset**做為輸入和**OutputDataset**做為輸出。
   * hello 自訂活動的 hello linkedServiceName 屬性指向 toohello **AzureBatchLinkedService**，它會告訴 Azure Data Factory 的 hello 自訂活動必須 toorun Azure 批次 Vm 上的。
   * **isPaused**屬性設定太**false**預設。 hello 管線執行立即在此範例中，因為 hello 配量開始在過去的 hello。 您可以設定這個屬性 tootrue toopause hello 管線，並將它回復 toofalse toorestart。
   * hello**啟動**時間和**結束**時間**五個**相距的時數和配量所產生每小時，因此 hello 管線所產生五個配量。
3. toodeploy hello 管線中，按一下 **部署**hello 命令列上。

### <a name="monitor-hello-pipeline"></a>監視 hello 管線
1. 在 hello Data Factory 刀鋒視窗中 hello Azure 入口網站中，按一下 **圖表**。

    ![[圖表] 磚](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. 在 hello 圖表檢視，現在按一下 hello OutputDataset。

    ![圖表檢視](./media/data-factory-use-custom-activities/diagram.png)
3. 您應該會看到五個輸出配量 hello 位於 hello 就緒狀態。 如果它們不是在 hello 就緒狀態，它們沒有被尚未產生。 

   ![輸出配量](./media/data-factory-use-custom-activities/OutputSlices.png)
4. 確認 hello 輸出檔會產生在 hello blob 儲存體中 hello **adftutorial**容器。

   ![自訂活動的輸出][image-data-factory-ouput-from-custom-activity]
5. 如果您開啟 hello 輸出檔，您應該會看到 hello 輸出類似 toohello 下列輸出：

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. 使用 hello [Azure 入口網站][ azure-preview-portal]或 Azure PowerShell cmdlet toomonitor 您的資料處理站、 管線和資料集。 您可以查看來自 hello 訊息**ActivityLogger**在 hello hello hello 記錄檔 (特別是 0.log 使用者)，您可以下載從 hello 入口網站或使用 cmdlet 的自訂活動的程式碼。

   ![從自訂活動下載記錄檔][image-data-factory-download-logs-from-custom-activity]

如需有關監視資料集和管線的詳細步驟，請參閱 [監視和管理管線](data-factory-monitor-manage-pipelines.md) 。      

## <a name="data-factory-project-in-visual-studio"></a>Visual Studio 中的 Data Factory 專案  
您可以使用 Visual Studio (而不是使用 Azure 入口網站) 來建立並發佈 Data Factory 實體。 詳細的資訊建立和使用 Visual Studio 發行 Data Factory 實體，請參閱[建置您使用 Visual Studio 的第一個管線](data-factory-build-your-first-pipeline-using-vs.md)和[資料複製到 Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md)文件。

請勿 hello 下列其他步驟，如果您要在 Visual Studio 中建立 Data Factory 專案：
 
1. 新增 hello Data Factory 專案 toohello 包含 hello 自訂活動專案的 Visual Studio 方案。 
2. 將 hello Data Factory 專案參考 toohello.NET 活動專案。 Data Factory 專案上按一下滑鼠右鍵，指向太**新增**，然後按一下**參考**。 
3. 在 hello**加入參考**對話方塊中，選取 hello **MyDotNetActivity**專案，然後按一下**確定**。
4. 建置並發行 hello 方案。

    > [!IMPORTANT]
    > 當您發行 Data Factory 實體時，zip 檔案會自動為您建立和上傳的 toohello blob 容器： customactivitycontainer。 如果 hello blob 容器不存在，它會自動建立太。  


## <a name="data-factory-and-batch-integration"></a>Data Factory 和 Batch 整合
hello Data Factory 服務 Azure 批次中建立工作以 hello 名稱： **adf poolname： 工作 xxx**。 按一下**作業**hello 左側功能表中。 

![Azure Data Factory - Batch 作業](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

配量的每個活動執行都會建立一個作業。 如果有五個處理的配量準備 toobe，有五個工作會建立此作業中。 Hello 批次集區中有多個計算節點，如果兩個或多個配量可以平行執行。 如果 hello 最大的工作，每個計算節點集太 > 1，您也可以有多個配量上 hello 執行相同的計算。

![Azure Data Factory - Batch 作業工作](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

hello 下列圖表說明 hello Azure Data Factory 和批次工作之間的關聯性。

![Data Factory & Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a>疑難排解失敗
疑難排解包含一些基本技術：

1. 如果您看到下列錯誤 hello，您可能正在使用的作用/Cool blob 儲存體而不使用一般用途的 Azure blob 儲存體。 上傳 hello zip 檔案 tooa**一般用途的 Azure 儲存體帳戶**。 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. 如果您看到下列錯誤 hello，確認您指定 hello CS 檔案相符項目 hello 名稱中的 hello 類別 hello 名稱**EntryPoint** hello 管線 JSON 中的屬性。 Hello 逐步解說中，在 hello 類別名稱是： MyDotNetActivity，並在 hello JSON 中的 hello 進入點是： MyDotNetActivityNS。**MyDotNetActivity**。

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   如果 hello 名稱相符，確認所有 hello 二進位檔都位於 hello**根資料夾**hello zip 檔案。 也就是說，當您開啟 hello zip 檔案，您應該會看到所有的 hello 檔案 hello 根資料夾中，在任何子資料夾中。   
3. 如果未設定 hello 輸入配量太**準備**，確認 hello 輸入的資料夾結構是否正確和**file.txt**存在 hello 輸入資料夾中。
3. 在 hello **Execute**方法的自訂活動，使用 hello **IActivityLogger**物件 toolog 資訊可協助您疑難排解問題。 記錄的 hello 訊息顯示在 hello 使用者記錄檔 (名為的一個或多個檔案： 使用者 0.log、 使用者 1.log、 使用者 2.log 等。)。

   在 hello **OutputDataset**刀鋒視窗中，按一下 hello 配量 toosee hello**資料配量**刀鋒視窗，該配量。 您會看到該配量的 [活動執行]。 您應該會看到一個 hello 配量執行的活動。 如果您按一下 執行 hello 命令列中，您可以啟動另一個活動執行 hello 相同配量。

   當您按一下 hello 活動執行時，請參閱 hello**活動執行詳細資料**刀鋒視窗的記錄檔的清單。 您會看到 hello user_0.log 檔中記錄的訊息。 當發生錯誤時，因為 hello 重試計數設定 too3 hello 管線/活動 JSON 中會看到三個活動執行。 當您按一下 hello 活動執行時，您會看到 hello 記錄檔，您可以檢閱 tootroubleshoot hello 錯誤。

   在 hello 清單中的記錄檔，按一下 hello**使用者 0.log**。 Hello 右面板中會使用 hello 的 hello 結果**IActivityLogger.Write**方法。 如果您無法看到所有訊息，請檢查是否有名為 user_1.log、user_2.log 等等多個記錄檔。否則，hello 一次登入訊息之後，可能會失敗 hello 程式碼。

   此外，檢查 **system-0.log** 是否有任何系統錯誤訊息和例外狀況。
4. 包含 hello **PDB**檔案 hello zip 檔案中，所以 hello 錯誤詳細資料會有這類資訊**呼叫堆疊**發生的錯誤。
5. 所有 hello hello zip 檔案中的 hello 自訂活動必須是在 hello**上層**與任何子資料夾。
6. 請確定該 hello **assemblyName** (MyDotNetActivity.dll)， **entryPoint**(MyDotNetActivityNS.MyDotNetActivity)， **packageFile** (customactivitycontainer /MyDotNetActivity.zip) 和**packageLinkedService** (應該指向 toohello**一般用途**包含 hello zip 檔案的 Azure blob 儲存體) 會設定 toocorrect 值。
7. 如果您修正錯誤，且想 tooreprocess hello 配量，以滑鼠右鍵按一下 hello 配量在 hello **OutputDataset**刀鋒視窗，然後按一下**執行**。
8. 如果您看到下列錯誤 hello，您使用版本 > 4.3.0 hello Azure 儲存體的封裝。 資料處理站服務啟動器需要 WindowsAzure.Storage hello 4.3 版本。 請參閱[Appdomain 隔離](#appdomain-isolation)區段的解決方法是，如果您必須使用 hello 新版的 Azure 儲存體組件。 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    如果您可以使用 Azure 儲存體套件 hello 4.3.0 版，移除 hello 現有參考 tooAzure 儲存封裝的版本 > 4.3.0。 然後，執行下列命令，NuGet Package Manager Console 中的 hello。 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    建置 hello 專案。 刪除版本 > 4.3.0 Azure.Storage 組件從 hello bin\Debug 資料夾。 建立 zip 檔案與二進位檔和 hello PDB 檔案。 取代這一個 hello blob 容器 (customactivitycontainer) 中的 hello 舊的 zip 檔案。 重新執行 hello 配量失敗 （配量，以滑鼠右鍵按一下並按一下 [執行]）。   
8. hello 自訂活動不會使用 hello **app.config**檔案從您的封裝。 因此，如果您的程式碼會讀取 hello 組態檔中的任何連接字串，因此無法在執行階段。 hello 最佳作法是當使用 Azure Batch toohold 中的秘密**Azure KeyVault**，使用憑證為基礎的服務主體 tooprotect hello **keyvault**，並散佈 hello 憑證tooAzure 批次集區。 hello.NET 自訂活動，則可以從 hello KeyVault 在執行階段存取機密資料。 這個解決方案是一般的解決方案，而且可以延展 tooany 類型的密碼，而不只是連接字串。

   沒有簡單的因應措施 （但不是最佳作法）： 您可以建立**Azure SQL 連結服務**與連接字串設定，建立使用 hello 連結的服務，以及鏈結 hello 資料集做為虛擬輸入資料集的資料集自訂.NET 活動 toohello。 接著，您可以存取 hello 連結服務的連接字串 hello 自訂活動程式碼中。  

## <a name="update-custom-activity"></a>更新自訂活動
如果您更新 hello hello 自訂活動的程式碼時，建置它，並上傳 hello zip 檔案包含新的二進位檔 toohello blob 儲存體。

## <a name="appdomain-isolation"></a>Appdomain 隔離
請參閱[跨 AppDomain 範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample)會示範如何 toocreate 的自訂活動不是，限制 hello Data Factory 啟動器所使用的 tooassembly 版本 (範例： WindowsAzure.Storage v4.3.0、 Newtonsoft.Json v6.0.x 等。)。

## <a name="access-extended-properties"></a>存取延伸屬性
Hello 下列範例所示，您可以在 hello 活動 JSON 中宣告擴充的屬性：

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


在 hello 範例中，有兩個的擴充的屬性： **SliceStart**和**DataFactoryName**。 hello SliceStart 的值根據 hello SliceStart 系統變數。 如需支援的系統變數清單，請參閱 [系統變數](data-factory-functions-variables.md) 。 DataFactoryName hello 值為硬式編碼 tooCustomActivityFactory。

這些擴充屬性中 hello tooaccess **Execute**方法，下列程式碼使用程式碼類似 toohello:

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a>Azure Batch 的自動調整
您也可以建立具有 **自動調整** 功能的 Azure Batch 集區。 例如，您可以建立 azure 批次集區 0 專用的 Vm 與 hello 數字的暫止工作為基礎的自動調整公式。 

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

## <a name="use-hdinsight-compute-service"></a>使用 HDInsight 計算服務
在 hello 逐步解說中，您可以使用 Azure Batch 計算 toorun hello 自訂活動。 您也可以使用 Windows 為基礎的 HDInsight 叢集，或已建立隨 Windows 為基礎的 HDInsight 叢集，並以 hello hello HDInsight 叢集上執行的自訂活動的 Data Factory。 以下是使用的 HDInsight 叢集的 hello 高層級步驟。

> [!IMPORTANT]
> 只在 Windows 為基礎的 HDInsight 叢集上執行自訂.NET 活動 hello。 這項限制的因應措施為 toouse hello 對應減少活動 toorun 自訂 Java 程式碼以 Linux 為基礎的 HDInsight 叢集上。 另一個選項是 toouse Vm toorun 自訂活動而不是使用 HDInsight 叢集的 Azure Batch 集區。
 

1. 建立 Azure HDInsight 連結服務。   
2. 使用 HDInsight 連結服務取代**AzureBatchLinkedService** hello 在管線 JSON。

如果您想 tootest hello 逐步解說中，變更與**啟動**和**結束**時間 hello 管線，讓您可以測試以 hello Azure HDInsight 服務的 hello 案例。

#### <a name="create-azure-hdinsight-linked-service"></a>建立 Azure HDInsight 連結服務
hello Azure Data Factory 服務支援建立隨叢集，並將它 tooprocess 輸入的 tooproduce 輸出資料。 您也可以使用自己的叢集 tooperform hello 相同。 當您使用隨選 HDInsight 叢集時，系統會為每個配量建立叢集。 而如果您使用 HDInsight 叢集，hello 叢集已準備好 tooprocess hello 立即配量。 因此，當您使用隨叢集，您可能無法看見 hello 輸出資料做為當您使用自己的叢集快速。

> [!NOTE]
> 在執行階段，.NET 活動的執行個體只會在執行一個背景工作節點在 hello HDInsight 叢集。它不能在多個節點上的縮放的 toorun。 多個執行個體的.NET 活動可以平行執行 hello HDInsight 叢集的不同節點上。
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a>toouse 隨選 HDInsight 叢集
1. 在 hello **Azure 入口網站**，按一下 **作者及部署**hello Data Factory 首頁中。
2. 在 hello Data Factory 編輯器中，按一下 **新計算**hello 命令列，並選取從**-隨選 HDInsight 叢集**hello 功能表。
3. 進行下列變更 toohello JSON 指令碼的 hello:

   1. Hello **clusterSize**屬性，指定 hello hello HDInsight 叢集大小。
   2. Hello **timeToLive**屬性，指定時間於刪除之前 hello 客戶可處於閒置狀態。
   3. Hello**版本**屬性，指定您想要 toouse hello HDInsight 版本。 如果您排除這個屬性時，會使用 hello 最新版本。  
   4. Hello **linkedServiceName**，指定**AzureStorageLinkedService**。

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > 只在 Windows 為基礎的 HDInsight 叢集上執行自訂.NET 活動 hello。 這項限制的因應措施為 toouse hello 對應減少活動 toorun 自訂 Java 程式碼以 Linux 為基礎的 HDInsight 叢集上。 另一個選項是 toouse Vm toorun 自訂活動而不是使用 HDInsight 叢集的 Azure Batch 集區。

4. 按一下**部署**hello 命令列 toodeploy hello 連結服務。

##### <a name="toouse-your-own-hdinsight-cluster"></a>toouse HDInsight 叢集：
1. 在 hello **Azure 入口網站**，按一下 **作者及部署**hello Data Factory 首頁中。
2. 在 hello **Data Factory 編輯器**，按一下**新計算**hello 命令列，並選取從**HDInsight 叢集**hello 功能表。
3. 進行下列變更 toohello JSON 指令碼的 hello:

   1. Hello **clusterUri**屬性中，輸入您的 HDInsight hello URL。 例如：https://<clustername>.azurehdinsight.net/     
   2. Hello **UserName**屬性中，輸入 hello 使用者名稱擁有存取 toohello HDInsight 叢集。
   3. Hello**密碼**屬性中，輸入 hello 使用者 hello 密碼。
   4. Hello **LinkedServiceName**屬性中，輸入**AzureStorageLinkedService**。
4. 按一下**部署**hello 命令列 toodeploy hello 連結服務。

請參閱 [計算連結服務](data-factory-compute-linked-services.md) 以取得詳細資料。

在 hello**管線 JSON**，使用 HDInsight (點播或您自己) 連結服務：

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a>使用 .NET SDK 建立自訂活動
在本文中的 hello 逐步解說，您可以建立 data factory 管線，藉由使用 hello Azure 入口網站使用 hello 自訂活動。 下列程式碼的 hello 顯示 toocreate 改為使用.NET SDK hello 資料處理站的方式。 您可以找到更多詳細使用 SDK tooprogrammatically hello 中建立管線[建立與複製活動的管線，使用.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)發行項。 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

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
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

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
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
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
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
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

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
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
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

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
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a>在 Visual Studio 中針對自訂活動進行偵錯
hello [Azure Data Factory 的本機環境](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment)GitHub 上的範例包含一個工具，可讓您在 Visual Studio 內 toodebug 自訂.NET 活動。  


## <a name="sample-custom-activities-on-github"></a>GitHub 上的範例自訂活動
| 範例 | 自訂活動的工作內容 |
| --- | --- |
| [HTTP 資料下載程式](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)。 |從 HTTP 端點 tooAzure Data Factory 中使用 C# 自訂活動的 Blob 儲存體下載資料。 |
| [Twitter 情感分析範例](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |叫用 Azure ML 模型，執行情感分析、評分、預測等等。 |
| [執行 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)。 |在已安裝 R 的 HDInsight 叢集上執行 RScript.exe 來叫用 R 指令碼。 |
| [跨 AppDomain.NET 活動](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |使用從 hello Data Factory 啟動器所使用的不同組件版本 |
| [重新處理 Azure Analysis Services 中的模型](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  重新處理 Azure Analysis Services 中的模型。 |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
