---
title: "aaaPersist 作業和工作輸出 hello 檔案慣例程式庫的儲存體 tooAzure for.NET-Azure 批次 |Microsoft 文件"
description: "了解如何 toouse.NET toopersist 批次工作的 Azure 批次檔慣例文件庫和工作輸出 tooAzure 存放裝置和檢視 hello 保存 hello Azure 入口網站中的輸出。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>保存工作和工作資料 tooAzure 儲存體與 hello.NET toopersist 的批次檔慣例文件庫 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

其中一種方式 toopersist 工作資料為 toouse hello[適用於.NET 的 Azure 批次檔慣例程式庫][nuget_package]。 hello 檔案慣例程式庫會簡化 hello 程序儲存工作輸出的資料 tooAzure 儲存和擷取。 您可以使用工作和用戶端程式碼中的 hello 檔案慣例文件庫&mdash;保存檔案，工作的程式碼和用戶端程式碼 toolist，並將其擷取。 工作程式碼也可以使用 hello 庫 tooretrieve hello 輸出上游的工作，例如[工作相依性](batch-task-dependencies.md)案例。 

tooretrieve 輸出與 hello 檔案慣例媒體櫃的檔案，您可以找到 hello 檔案指定的工作或工作識別碼的用途中列出它們。 您不需要 tooknow hello 名稱或 hello 檔案的位置。 例如，您可以用於 hello 檔案慣例文件庫 toolist 所有中繼檔案指定的工作，或取得給定作業的預覽檔案。

> [!TIP]
> 從 2017年-05-01 版開始，hello 批次服務應用程式開發介面支援保存的輸出資料 tooAzure 儲存體工作和使用 hello 虛擬機器組態建立的集區上執行的作業管理員工作。 hello 批次服務 API 提供簡單的方式 toopersist hello 程式碼所建立的工作，並做為替代 toohello 檔案慣例的文件庫中的輸出。 您可以修改批次用戶端應用程式 toopersist 輸出，而不需要您的工作正在執行的 tooupdate hello 應用程式。 如需詳細資訊，請參閱[保存以 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體](batch-task-output-files.md)。
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>何時使用 hello 檔案慣例庫 toopersist 工作輸出？

Azure 批次提供多個單向 toopersist 工作輸出。 hello 檔案慣例是最適合的 toothese 案例：

- 您可以輕鬆地修改 hello hello 應用程式確認您的工作正在執行 toopersist 檔案使用 hello 檔案慣例程式庫的程式碼。
- Hello 工作仍在執行時，您會想 toostream 資料 tooAzure 儲存體。
- 您想要從以 hello 雲端服務組態或 hello 虛擬機器組態建立的集區的 toopersist 資料。
- 用戶端應用程式或其他工作在 hello 作業需求 toolocate 和下載工作輸出檔依識別碼或依用途。 
- 您想 tooview hello Azure 入口網站中的工作輸出。

如果您的案例與以上所列不同，您可能需要 tooconsider 不同的方法。 如需保存的工作輸出的其他選項的詳細資訊，請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)。 

## <a name="what-is-hello-batch-file-conventions-standard"></a>什麼是標準的批次檔慣例 hello？

hello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)hello 目的地容器和 blob 路徑 toowhich 輸出檔案會寫入提供的命名配置。 檔案保存的 tooAzure 遵守 toohello 檔案慣例標準的儲存體都會自動供 hello Azure 入口網站中的檢視。 hello 入口網站可感知 hello 命名慣例，而且因此可以顯示遵守 tooit 的檔案。

適用於.NET 的 hello 檔案慣例程式庫會自動命名您的儲存體容器和工作的輸出檔案根據 toohello 標準檔案慣例。 hello 檔案慣例程式庫也會提供 Azure 儲存體中的方法 tooquery 輸出檔案根據 toojob ID、 工作識別碼或用途。   

如果您正在開發以.NET 以外的語言，您可以實作 hello 檔案慣例標準自己應用程式中。 如需詳細資訊，請參閱[關於 hello 批次檔慣例標準](batch-task-output.md#about-the-batch-file-conventions-standard)。

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>連結的 Azure 儲存體帳戶 tooyour 批次帳戶

toopersist 輸出資料 tooAzure 使用 hello 檔案慣例程式庫的儲存體，您必須先連結的 Azure 儲存體帳戶 tooyour Batch 帳戶。 如果您尚未這樣做，批次帳戶的儲存體帳戶 tooyour 使用連結 hello [Azure 入口網站](https://portal.azure.com):

1. 瀏覽 tooyour hello Azure 入口網站中的批次帳戶。 
2. 在 [設定] 下，選取 [儲存體帳戶]。
3. 如果您還沒有與您的 Batch 帳戶相關聯的儲存體帳戶，請按一下 [儲存體帳戶 (無)]。
4. 從訂用帳戶的 hello 清單中選取的儲存體帳戶。 為了達到最佳效能，使用 Azure 儲存體帳戶中 hello，正在您的工作與 hello 批次帳戶相同的區域。

## <a name="persist-output-data"></a>保存輸出資料

toopersist 作業和工作使用 hello 檔案慣例程式庫輸出的資料，請建立容器，在 Azure 儲存體，然後儲存 hello 輸出 toohello 容器。 使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)您工作的程式碼 tooupload hello 工作輸出 toohello 容器中。 

如需在 Azure 儲存體中使用容器和 Blob 的詳細資訊，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。

> [!WARNING]
> 與程式庫會儲存在 hello 檔案慣例一起保存的所有作業和工作的輸出 hello 相同的容器。 如果大量的工作嘗試 toopersist 使用位於檔案 hello 相同時間[儲存體節流限制](../storage/common/storage-performance-checklist.md#blobs)可能會強制執行。
> 
> 

### <a name="create-storage-container"></a>建立儲存體容器

toopersist 工作輸出 tooAzure 儲存體，先建立容器，藉由呼叫[CloudJob][net_cloudjob]。[PrepareOutputStorageAsync][net_prepareoutputasync]。 這個擴充方法會採用 [CloudStorageAccount][net_cloudstorageaccount] 物件作為參數。 它會建立具名相應 toohello 檔案慣例標準，使其內容是可探索的 hello hello 本文稍後所述的 Azure 入口網站與 hello 擷取方法的容器。

您通常將 hello 程式碼 toocreate 容器放在用戶端應用程式&mdash;hello 建立您的集區、 工作和工作的應用程式。

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a>儲存工作輸出

既然您已備妥在 Azure 儲存體容器，工作可以使用將儲存輸出 toohello 容器 hello [TaskOutputStorage] [ net_taskoutputstorage] hello 檔案慣例文件庫中找到的類別。

在您工作的程式碼，先建立[TaskOutputStorage] [ net_taskoutputstorage]物件，然後 hello 工作已完成其工作，當呼叫 hello [TaskOutputStorage] [ net_taskoutputstorage].[SaveAsync] [ net_saveasync]方法 toosave 其輸出 tooAzure 儲存體。

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

hello `kind` hello 參數[TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx)。[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx)方法來分類 hello 保存檔案。 有四個預先定義的 [TaskOutputKind][net_taskoutputkind] 類型：`TaskOutput`、`TaskPreview`、`TaskLog` 和 `TaskIntermediate.`。您也可以定義輸出的自訂類別。

這些輸出類型可讓您 toospecify 哪種類型的輸出 toolist，當您稍後查詢 hello 批次中保存指定工作的輸出。 換句話說，當您列出 hello 輸出工作，您可以篩選 hello 清單的某個 hello 輸出類型。 例如，"給我 hello*預覽*工作輸出*109*。 」 需列出和擷取輸出的詳細資訊會出現在[擷取輸出](#retrieve-output)hello 文件中的更新版本。

> [!TIP]
> hello 輸出種類也會決定在 hello Azure 入口網站特定的檔案出現的位置： *TaskOutput*-分類的檔案會出現在**工作輸出檔**，和*TaskLog*檔案會出現在**工作記錄檔**。
> 
> 

### <a name="store-job-outputs"></a>儲存工作輸出

此外 toostoring 工作輸出，您就可以儲存 hello 整項作業相關聯的輸出。 比方說，在 hello 合併工作的影片轉譯作業中，您可能會完整呈現的 hello 影片保留做為工作輸出。 您的工作完成時，用戶端應用程式可以列出和擷取 hello hello 工作的輸出，並不需要 tooquery hello 個別工作。

儲存工作輸出呼叫 hello [JobOutputStorage][net_joboutputstorage]。[SaveAsync] [ net_joboutputstorage_saveasync]方法，並指定 hello [JobOutputKind] [ net_joboutputkind]和檔案名稱：

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

如同 hello **TaskOutputKind**類型為工作輸出，您可以使用 hello [JobOutputKind] [ net_joboutputkind]類型 toocategorize 工作的保存檔案。 這個參數可讓您 toolater （清單） 的輸出特定類型的查詢。 hello **JobOutputKind**類型包含輸出和預覽類別，並支援建立自訂的類別。

### <a name="store-task-logs"></a>儲存工作記錄檔

此外 toopersisting 檔案 toodurable 儲存體時的工作或作業完成，您可能需要 toopersist 檔案 hello 工作執行期間更新&mdash;記錄檔或`stdout.txt`和`stderr.txt`，例如。 基於此目的，hello Azure 批次檔慣例程式庫提供 hello [TaskOutputStorage][net_taskoutputstorage]。[SaveTrackedAsync] [ net_savetrackedasync]方法。 與[SaveTrackedAsync][net_savetrackedasync]，您可以追蹤 hello 節點 （在您指定的間隔內） 上的更新 tooa 檔案並保存這些更新 tooAzure 儲存體。

在下列程式碼片段的 hello，我們使用[SaveTrackedAsync] [ net_savetrackedasync] tooupdate`stdout.txt`在 Azure 儲存體 hello hello 工作執行期間每 15 秒：

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

hello 標記為註解區段`Code tooprocess data and produce output file(s)`是 hello 通常會執行您的工作的程式碼的預留位置。 例如，您可能有程式碼會從 Azure 儲存體下載資料，並對這些資料執行轉換或計算。 hello 很重要的一部分此程式碼片段會示範如何將包裝在這類程式碼`using`區塊 tooperiodically 更新的檔案[SaveTrackedAsync][net_savetrackedasync]。

hello 節點代理程式是 hello 集區中的每個節點上執行，並提供 hello 節點與 hello 批次服務之間的 hello 命令控制項介面的程式。 hello`Task.Delay`呼叫是這個 hello 結尾需要`using`hello 節點代理程式的區塊 tooensure 出 hello 節點上 toohello stdout.txt 檔案含有標準時間 tooflush hello 內容。 沒有這項延遲，就可能 toomiss hello 輸出的最後幾秒。 此延遲可能並非所有檔案都需要。

> [!NOTE]
> 當您啟用檔案與追蹤**SaveTrackedAsync**，則只*附加*toohello 追蹤的檔案會保存的 tooAzure 儲存體。 使用這個方法只可以用於追蹤非輪替記錄檔或其他檔案寫入 toowith 附加 hello 檔案作業 toohello 結尾。
> 
> 

## <a name="retrieve-output-data"></a>擷取輸出資料

當您擷取保存的輸出使用 hello Azure 批次檔慣例程式庫時，您在進行工作和工作中心的方式。 您可以要求 hello 輸出指定的工作或作業而不需要 tooknow 它在 Azure 儲存體或甚至是其檔案名稱中的路徑。 相反地，您可以依據工作或作業識別碼要求輸出檔案。

hello 下列程式碼片段逐一查看作業的工作會列印 hello hello 工作的輸出檔的一些資訊，然後從儲存體下載檔案。

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a>Hello Azure 入口網站中檢視輸出檔

hello Azure 入口網站會顯示工作輸出的檔案和記錄都會保存的 tooa 連結的 Azure 儲存體帳戶使用 hello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。 您可以實作這些慣例自行在 hello 您選擇的語言，或您可以使用.NET 應用程式中的 hello 檔案慣例程式庫。

tooenable hello 顯示 hello 入口網站中的輸出檔案，您必須滿足下列需求的 hello:

1. [Azure 儲存體帳戶連結](#requirement-linked-storage-account)tooyour Batch 帳戶。
2. 保存輸出時，請遵守 toohello 預先定義的命名慣例，儲存體容器和檔案。 您可以在 hello 檔案慣例文件庫中找到的這些慣例的 hello 定義[讀我檔案][github_file_conventions_readme]。 如果您使用 hello [Azure 批次檔慣例][ nuget_package]文件庫 toopersist 您輸出，您的檔案會保存根據 toohello 標準檔案慣例。

tooview 工作輸出檔，並登入 hello Azure 入口網站，瀏覽您感興趣，其輸出 continuación，elija toohello 工作**儲存輸出檔案**或**儲存記錄檔**。 下圖顯示 hello**儲存輸出檔案**識別碼為"007"hello 工作：

![工作輸出 刀鋒視窗中 hello Azure 入口網站][2]

## <a name="code-sample"></a>程式碼範例

hello [PersistOutputs] [ github_persistoutputs]範例專案是其中一個 hello [Azure 批次程式碼範例][ github_samples] GitHub 上。 這個 Visual Studio 方案會示範如何 toouse hello Azure 批次檔慣例的文件庫 toopersist 工作輸出 toodurable 儲存體。 toorun hello 範例，請遵循下列步驟：

1. 在開啟 hello 專案**2015年或更新版本的 Visual Studio**。
2. 新增您的批次和儲存體**帳戶認證**太**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common 專案中。
3. **建置**（但不是會執行） hello 方案。 如果出現提示，請還原任何 NuGet 封裝。
4. 使用 hello Azure 入口網站 tooupload[應用程式封裝](batch-application-packages.md)如**PersistOutputsTask**。 包含 hello `PersistOutputsTask.exe` hello.zip 套件中，設定 hello 應用程式識別碼及其相依組件太"PersistOutputsTask 」，以及 hello 應用程式封裝的版本太"1.0 的"。
5. **啟動**（執行） 的 hello **PersistOutputs**專案。
6. 當提示的 toochoose hello 持續性技術 toouse 執行 hello 範例中，輸入**1** toorun hello 範例使用 hello 檔案慣例庫 toopersist 工作輸出。 

## <a name="next-steps"></a>後續步驟

### <a name="get-hello-batch-file-conventions-library-for-net"></a>取得 hello 批次檔慣例 library for.NET

hello 批次檔慣例 library for.NET 是用於[NuGet][nuget_package]。 hello 程式庫會擴充 hello [CloudJob] [ net_cloudjob]和[CloudTask] [ net_cloudtask]類別的新方法。 另請參閱 hello[參考文件](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files)hello 檔案慣例程式庫。

hello[原始程式碼][ github_file_conventions] hello 檔案慣例程式庫會提供在 GitHub 上 hello Microsoft Azure SDK for.NET 的儲存機制。 

### <a name="explore-other-approaches-for-persisting-output-data"></a>探索保存輸出資料的其他方法

- 請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)保存的工作和作業資料的概觀。
- 請參閱[保存以 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體](batch-task-output-files.md)toolearn toouse hello 批次服務 API toopersist 資料的輸出。

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "入口網站中的 [已儲存的輸出檔案] 和 [已儲存的記錄檔] 選取器"
[2]: ./media/batch-task-output/task-output-02.png "工作輸出 刀鋒視窗中 hello Azure 入口網站"
