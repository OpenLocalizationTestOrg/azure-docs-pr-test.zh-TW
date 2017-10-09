---
title: "aaaPersist 作業和工作的輸出以 hello Azure Batch 服務 API tooAzure 儲存體 |Microsoft 文件"
description: "了解 toouse 批次服務 API toopersist 批次工作與工作輸出 tooAzure 儲存體。"
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>保存與 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

從 2017年-05-01 版開始，hello 批次服務應用程式開發介面支援保存的輸出資料 tooAzure 儲存體工作和集區與 hello 虛擬機器組態上執行的作業管理員工作。 當您新增工作時，您可以指定 Azure 儲存體中的容器做為 hello hello 工作輸出的目的地。 hello 批次服務然後會將任何輸出資料 toothat 容器寫入 hello 工作完成時。

利用 toousing hello 批次服務 API toopersist 工作輸出，則不需要 hello 工作 toomodify hello 應用程式正在執行。 相反地，有幾個簡單的修改 tooyour 用戶端應用程式中，您可以保存建立 hello 工作的 hello 程式碼中的 hello 工作的輸出。   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>何時使用 hello 批次服務 API toopersist 工作輸出？

Azure 批次提供多個單向 toopersist 工作輸出。 一個是最適合的 toothese 案例的便利方式，則使用 hello 批次服務 API:

- 您想從 toowrite 程式碼 toopersist 工作輸出內用戶端應用程式，而不需要修改您的工作正在執行的 hello 應用程式。
- 您想從批次工作及建立 hello 虛擬機器組態與集區中的作業管理員工作 toopersist 輸出。
- 您想使用任意名稱 toopersist 輸出 tooan Azure 儲存體容器。
- 您想要 toopersist 輸出 tooan Azure 儲存體容器名稱相應 toohello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。 

如果您的案例與以上所列不同，您可能需要 tooconsider 不同的方法。 例如，hello 批次服務 API 目前不支援資料流輸出 tooAzure 儲存體 hello 工作執行時。 toostream 輸出，請考慮使用 hello 批次檔慣例程式庫，適用於.NET。 至於其他語言，您將需要 tooimplement 自己的解決方案。 如需保存的工作輸出的其他選項的詳細資訊，請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)。 

## <a name="create-a-container-in-azure-storage"></a>在 Azure 儲存體中建立容器

toopersist 工作輸出 tooAzure 儲存體，您將需要 toocreate 做為輸出檔的 hello 目的地容器。 建立 hello 容器，然後再執行工作，最好是先將工作提交。 toocreate hello 容器、 使用 hello 適當 Azure 儲存體用戶端程式庫或 SDK。 如需有關 Azure 儲存體 Api 的詳細資訊，請參閱 hello [Azure 儲存體文件](https://docs.microsoft.com/azure/storage/)。

例如，如果您要撰寫您的應用程式，在 C# 中，使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)。 下列範例會示範如何 hello toocreate 容器：

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>取得 hello 容器的共用的存取簽章

建立 hello 容器之後，取得寫入權限 toohello 容器的共用的存取簽章 (SAS)。 SAS 提供委派的存取 toohello 容器。 hello SAS 授與一組指定的權限，以及一段指定的時間間隔的存取權。 hello 批次服務必須具有寫入權限 toowrite 工作輸出 toohello 容器 SAS。 如需關於 SAS 的詳細資訊，請參閱[在 Azure 儲存體中使用共用存取簽章 \(SAS\)](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。

當您取得使用 hello Azure 儲存體 Api 的 SAS 時，hello API 傳回的 SAS 權杖字串。 這個語彙基元字串包含 hello SAS，包括 hello 權限和哪些 hello 透過 SAS 的有效的 hello 間隔的所有參數。 toouse hello SAS tooaccess Azure 儲存體中的容器，您需要 tooappend hello SAS 權杖字串 toohello 資源 URI。 hello 資源的 URI，連同 hello 附加 SAS 權杖，並提供已驗證的存取 tooAzure 儲存體。

hello 下列範例顯示如何 tooget 唯寫 SAS 權杖字串 hello 容器，然後再附加 hello SAS toohello 容器的 URI:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>指定工作輸出的輸出檔案

對於工作而言 toospecify 輸出檔案建立的集合[OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile)物件，並將它指派 toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles)建立 hello 工作時的屬性。 

hello 下列.NET 程式碼範例建立的工作寫入名為隨機數字 tooa 檔`output.txt`。 hello 範例建立輸出檔案以供`output.txt`toobe 寫入 toohello 容器。 hello 範例也會建立任何符合 hello 檔案模式的記錄檔的輸出檔`std*.txt`(_例如_，`stdout.txt`和`stderr.txt`)。 hello 容器 URL 需要 hello 所建立的 SAS 先前 hello 容器。 hello 批次服務會使用 hello SAS tooauthenticate 存取 toohello 容器： 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>指定要進行比對的檔案模式

當您指定的輸出檔時，您可以使用 hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern)屬性 toospecify 檔案模式進行比對。 hello 檔案模式可能會比對零檔案、 單一檔案或一組 hello 工作所建立的檔案。

hello **FilePattern**屬性支援標準 filesystem 萬用字元，例如`*`（適用於非遞迴會比對） 和`**`（適用於遞迴會比對）。 例如，上述的 hello 程式碼範例指定 hello 檔案模式 toomatch`std*.txt`非遞迴的方式： 

`filePattern: @"..\std*.txt"`

tooupload 單一檔案，且不包含萬用字元指定檔案模式。 例如，上述的 hello 程式碼範例指定 hello 檔案模式 toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>指定上傳條件

hello [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition)屬性允許條件式的輸出檔案上傳。 如果失敗，常見的案例是 tooupload 一組檔案，如果 hello 工作成功和一組不同的檔案。 比方說，您可能在 hello 工作失敗而結束，則為非零結束代碼時，才想 tooupload 詳細資訊記錄檔。 同樣地，您可能想 tooupload 結果檔案才 hello 工作成功，因為這些檔案可能會遺失或不完整，如果 hello 工作失敗。

hello 上述程式碼範例會設定 hello **UploadCondition**屬性太**TaskCompletion**。 此設定會指定該 hello 檔案是 toobe 上傳之後 hello 工作完成時，不論 hello hello 結束代碼值。 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

如需其他設定，請參閱 hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition)列舉。

### <a name="disambiguate-files-with-hello-same-name"></a>釐清具有 hello 檔案相同的名稱

作業中的 hello 工作可能會產生具有 hello 檔案相同的名稱。 例如，`stdout.txt` 和 `stderr.txt` 是針對作業中執行的每項工作所建立。 因為在它自己的內容中，執行每項工作，這些檔案不衝突 hello 節點的檔案系統上。 不過，當您上傳檔案，從多個工作 tooa 共用容器，您必須先以 hello toodisambiguate 檔案相同的名稱。

hello [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path)屬性會指定 hello 目的地 blob 或輸出檔的虛擬目錄。 您可以使用 hello**路徑**屬性 tooname hello blob 或虛擬目錄的方式輸出檔案具有相同的名稱為唯一名稱在 Azure 儲存體中的 hello。 使用 hello 路徑中的 hello 工作識別碼的好方法 tooensure 唯一名稱，並輕鬆地找出檔案。

如果 hello **FilePattern**屬性設定 tooa 萬用字元運算式，則符合 hello 模式的所有檔案都必須上傳的 toohello hello 所指定的虛擬目錄**路徑**屬性。 例如，如果 hello 容器是`mycontainer`，hello 工作識別碼是`mytask`，hello 檔案模式，且`..\std*.txt`，然後 hello 的絕對 Uri toohello 輸出檔，在 Azure 儲存體將會類似於：

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

如果 hello **FilePattern**屬性集 toomatch 單一檔案名稱，亦即它不包含任何萬用字元的字元，然後 hello 值 hello**路徑**屬性會指定 hello 完整格式的 blob 名稱. 如果您預期會發生命名衝突，使用多個工作的單一檔案，然後將 hello hello 虛擬目錄名稱的一部分 hello 檔案名稱 toodisambiguate 這些檔案。 比方說，集 hello**路徑**屬性 tooinclude hello 工作 ID、 hello 分隔符號字元 （通常是正斜線），以及 hello 檔案名稱：

`path: taskId + @"/output.txt"`

hello 絕對 Uri toohello 輸出檔的一組工作將會類似於：

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

如需有關 Azure 儲存體中的虛擬目錄的詳細資訊，請參閱[列出容器中的 hello blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container)。


## <a name="diagnose-file-upload-errors"></a>診斷檔案上傳錯誤

如果上傳輸出檔案 tooAzure 存放裝置失敗，則 hello 工作可將移 toohello**已完成**狀態和 hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation)屬性設定。 檢查 hello **FailureInformation**屬性 toodetermine 發生的錯誤。 比方說，以下是發生在檔案上傳，如果找不到 hello 容器發生錯誤： 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

在每個檔案上傳，批次寫入這兩個記錄檔 toohello 計算節點，`fileuploadout.txt`和`fileuploaderr.txt`。 您可以檢查這些記錄檔 toolearn 更多關於特定錯誤。 在其中 hello 檔案上傳永遠不會嘗試，例如因為 hello 工作本身無法執行的情況下，然後這些記錄檔不會存在。

## <a name="diagnose-file-upload-performance"></a>診斷檔案上傳效能

hello`fileuploadout.txt`檔案記錄上傳進度。 您可以檢查這個檔案 toolearn，花費更多有關您的檔案上傳的時間長度。 記住有許多促成因素 tooupload 效能，hello hello 目標容器是否包括 hello 大小 hello 節點，hello 節點上的 hello 上載 hello 次的其他活動與 hello 批次集區有相同的區域，多少節點是正在上傳相同的時間、 和等的 hello toohello 儲存體帳戶。

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>使用標準的批次檔慣例 hello hello 批次服務 API

當您在工作輸出以 hello 批次服務 API 時，您可以命名您的目的地容器和 blob 不過嗎。 您也可以選擇 tooname 它們根據 toohello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。 hello 檔案慣例標準決定 hello 名稱 hello 目的地容器和 blob 在 Azure 儲存體 hello 的 hello 作業和工作的名稱為基礎的給定的輸出檔案。 如果您使用 hello 標準檔案慣例來命名輸出檔案，則輸出檔可供檢視之 hello [Azure 入口網站](https://portal.azure.com)。

如果您正在開發在 C# 中，您可以使用內建 hello 的 hello 方法[批次檔慣例.NET 程式庫](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files)。 此程式庫建立 hello 正確命名為您的容器和 blob 路徑。 例如，您可以呼叫 hello API tooget hello 正確 hello 容器名稱，根據 hello 工作名稱：

```csharp
string containerName = job.OutputStorageContainerName();
```

您可以使用 hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl)方法 tooreturn 是使用的 toowrite toohello 容器的共用的存取簽章 (SAS) URL。 接著，您可以將此 SAS toohello [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination)建構函式。

如果您正在開發 C# 以外的語言，您將自己需要 tooimplement hello 檔案慣例標準。

## <a name="code-sample"></a>程式碼範例

hello [PersistOutputs] [ github_persistoutputs]範例專案是其中一個 hello [Azure 批次程式碼範例][ github_samples] GitHub 上。 這個 Visual Studio 方案會示範如何 toouse hello 批次用戶端程式庫.NET toopersist 工作輸出 toodurable 儲存體。 toorun hello 範例，請遵循下列步驟：

1. 在開啟 hello 專案**2015年或更新版本的 Visual Studio**。
2. 新增您的批次和儲存體**帳戶認證**太**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common 專案中。
3. **建置**（但不是會執行） hello 方案。 如果出現提示，請還原任何 NuGet 封裝。
4. 使用 hello Azure 入口網站 tooupload[應用程式封裝](batch-application-packages.md)如**PersistOutputsTask**。 包含 hello `PersistOutputsTask.exe` hello.zip 套件中，設定 hello 應用程式識別碼及其相依組件太"PersistOutputsTask 」，以及 hello 應用程式封裝的版本太"1.0 的"。
5. **啟動**（執行） 的 hello **PersistOutputs**專案。
6. 當提示的 toochoose hello 持續性技術 toouse 執行 hello 範例中，輸入**2** toorun hello 範例使用批次服務 API hello toopersist 工作輸出。
7. 如有需要，hello 範例再次執行，輸入**3** toopersist hello 批次服務 API，以及 tooname hello 目的地容器和 blob 路徑根據 toohello 檔案慣例標準輸出。

## <a name="next-steps"></a>後續步驟

- For.NET 上保存的工作輸出與 hello 檔案慣例媒體櫃資訊，請參閱[保存作業和工作資料 tooAzure 儲存體與 hello.NET toopersist 的批次檔慣例文件庫](batch-task-output-file-conventions.md)。
- 在 Azure 批次中保存的輸出資料的其他方法的資訊，請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)。

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
