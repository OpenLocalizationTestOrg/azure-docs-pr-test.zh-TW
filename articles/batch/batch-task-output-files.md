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
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a><span data-ttu-id="55e80-103">保存與 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體</span><span class="sxs-lookup"><span data-stu-id="55e80-103">Persist task data tooAzure Storage with hello Batch service API</span></span>

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="55e80-104">從 2017年-05-01 版開始，hello 批次服務應用程式開發介面支援保存的輸出資料 tooAzure 儲存體工作和集區與 hello 虛擬機器組態上執行的作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="55e80-104">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools with hello virtual machine configuration.</span></span> <span data-ttu-id="55e80-105">當您新增工作時，您可以指定 Azure 儲存體中的容器做為 hello hello 工作輸出的目的地。</span><span class="sxs-lookup"><span data-stu-id="55e80-105">When you add a task, you can specify a container in Azure Storage as hello destination for hello task's output.</span></span> <span data-ttu-id="55e80-106">hello 批次服務然後會將任何輸出資料 toothat 容器寫入 hello 工作完成時。</span><span class="sxs-lookup"><span data-stu-id="55e80-106">hello Batch service then writes any output data toothat container when hello task is complete.</span></span>

<span data-ttu-id="55e80-107">利用 toousing hello 批次服務 API toopersist 工作輸出，則不需要 hello 工作 toomodify hello 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="55e80-107">An advantage toousing hello Batch service API toopersist task output is that you do not need toomodify hello application that hello task is running.</span></span> <span data-ttu-id="55e80-108">相反地，有幾個簡單的修改 tooyour 用戶端應用程式中，您可以保存建立 hello 工作的 hello 程式碼中的 hello 工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="55e80-108">Instead, with a few simple modifications tooyour client application, you can persist hello task's output from within hello code that creates hello task.</span></span>   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a><span data-ttu-id="55e80-109">何時使用 hello 批次服務 API toopersist 工作輸出？</span><span class="sxs-lookup"><span data-stu-id="55e80-109">When do I use hello Batch service API toopersist task output?</span></span>

<span data-ttu-id="55e80-110">Azure 批次提供多個單向 toopersist 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="55e80-110">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="55e80-111">一個是最適合的 toothese 案例的便利方式，則使用 hello 批次服務 API:</span><span class="sxs-lookup"><span data-stu-id="55e80-111">Using hello Batch service API is a convenient approach that's best suited toothese scenarios:</span></span>

- <span data-ttu-id="55e80-112">您想從 toowrite 程式碼 toopersist 工作輸出內用戶端應用程式，而不需要修改您的工作正在執行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="55e80-112">You want toowrite code toopersist task output from within your client application, without modifying hello application that your task is running.</span></span>
- <span data-ttu-id="55e80-113">您想從批次工作及建立 hello 虛擬機器組態與集區中的作業管理員工作 toopersist 輸出。</span><span class="sxs-lookup"><span data-stu-id="55e80-113">You want toopersist output from Batch tasks and job manager tasks in pools created with hello virtual machine configuration.</span></span>
- <span data-ttu-id="55e80-114">您想使用任意名稱 toopersist 輸出 tooan Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="55e80-114">You want toopersist output tooan Azure Storage container with an arbitrary name.</span></span>
- <span data-ttu-id="55e80-115">您想要 toopersist 輸出 tooan Azure 儲存體容器名稱相應 toohello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。</span><span class="sxs-lookup"><span data-stu-id="55e80-115">You want toopersist output tooan Azure Storage container named according toohello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> 

<span data-ttu-id="55e80-116">如果您的案例與以上所列不同，您可能需要 tooconsider 不同的方法。</span><span class="sxs-lookup"><span data-stu-id="55e80-116">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="55e80-117">例如，hello 批次服務 API 目前不支援資料流輸出 tooAzure 儲存體 hello 工作執行時。</span><span class="sxs-lookup"><span data-stu-id="55e80-117">For example, hello Batch service API does not currently support streaming output tooAzure Storage while hello task is running.</span></span> <span data-ttu-id="55e80-118">toostream 輸出，請考慮使用 hello 批次檔慣例程式庫，適用於.NET。</span><span class="sxs-lookup"><span data-stu-id="55e80-118">toostream output, consider using hello Batch File Conventions library, available for .NET.</span></span> <span data-ttu-id="55e80-119">至於其他語言，您將需要 tooimplement 自己的解決方案。</span><span class="sxs-lookup"><span data-stu-id="55e80-119">For other languages, you'll need tooimplement your own solution.</span></span> <span data-ttu-id="55e80-120">如需保存的工作輸出的其他選項的詳細資訊，請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="55e80-120">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="create-a-container-in-azure-storage"></a><span data-ttu-id="55e80-121">在 Azure 儲存體中建立容器</span><span class="sxs-lookup"><span data-stu-id="55e80-121">Create a container in Azure Storage</span></span>

<span data-ttu-id="55e80-122">toopersist 工作輸出 tooAzure 儲存體，您將需要 toocreate 做為輸出檔的 hello 目的地容器。</span><span class="sxs-lookup"><span data-stu-id="55e80-122">toopersist task output tooAzure Storage, you'll need toocreate a container that serves as hello destination for your output files.</span></span> <span data-ttu-id="55e80-123">建立 hello 容器，然後再執行工作，最好是先將工作提交。</span><span class="sxs-lookup"><span data-stu-id="55e80-123">Create hello container before you run your task, preferably before you submit your job.</span></span> <span data-ttu-id="55e80-124">toocreate hello 容器、 使用 hello 適當 Azure 儲存體用戶端程式庫或 SDK。</span><span class="sxs-lookup"><span data-stu-id="55e80-124">toocreate hello container, use hello appropriate Azure Storage client library or SDK.</span></span> <span data-ttu-id="55e80-125">如需有關 Azure 儲存體 Api 的詳細資訊，請參閱 hello [Azure 儲存體文件](https://docs.microsoft.com/azure/storage/)。</span><span class="sxs-lookup"><span data-stu-id="55e80-125">For more information about Azure Storage APIs, see hello [Azure Storage documentation](https://docs.microsoft.com/azure/storage/).</span></span>

<span data-ttu-id="55e80-126">例如，如果您要撰寫您的應用程式，在 C# 中，使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)。</span><span class="sxs-lookup"><span data-stu-id="55e80-126">For example, if you are writing your application in C#, use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="55e80-127">下列範例會示範如何 hello toocreate 容器：</span><span class="sxs-lookup"><span data-stu-id="55e80-127">hello following example shows how toocreate a container:</span></span>

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a><span data-ttu-id="55e80-128">取得 hello 容器的共用的存取簽章</span><span class="sxs-lookup"><span data-stu-id="55e80-128">Get a shared access signature for hello container</span></span>

<span data-ttu-id="55e80-129">建立 hello 容器之後，取得寫入權限 toohello 容器的共用的存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="55e80-129">After you create hello container, get a shared access signature (SAS) with write access toohello container.</span></span> <span data-ttu-id="55e80-130">SAS 提供委派的存取 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="55e80-130">A SAS provides delegated access toohello container.</span></span> <span data-ttu-id="55e80-131">hello SAS 授與一組指定的權限，以及一段指定的時間間隔的存取權。</span><span class="sxs-lookup"><span data-stu-id="55e80-131">hello SAS grants access with a specified set of permissions and over a specified time interval.</span></span> <span data-ttu-id="55e80-132">hello 批次服務必須具有寫入權限 toowrite 工作輸出 toohello 容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="55e80-132">hello Batch service needs a SAS with write permissions toowrite task output toohello container.</span></span> <span data-ttu-id="55e80-133">如需關於 SAS 的詳細資訊，請參閱[在 Azure 儲存體中使用共用存取簽章 \(SAS\)](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="55e80-133">For more information about SAS, see [Using shared access signatures \(SAS\) in Azure Storage](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

<span data-ttu-id="55e80-134">當您取得使用 hello Azure 儲存體 Api 的 SAS 時，hello API 傳回的 SAS 權杖字串。</span><span class="sxs-lookup"><span data-stu-id="55e80-134">When you get a SAS using hello Azure Storage APIs, hello API returns a SAS token string.</span></span> <span data-ttu-id="55e80-135">這個語彙基元字串包含 hello SAS，包括 hello 權限和哪些 hello 透過 SAS 的有效的 hello 間隔的所有參數。</span><span class="sxs-lookup"><span data-stu-id="55e80-135">This token string includes all parameters of hello SAS, including hello permissions and hello interval over which hello SAS is valid.</span></span> <span data-ttu-id="55e80-136">toouse hello SAS tooaccess Azure 儲存體中的容器，您需要 tooappend hello SAS 權杖字串 toohello 資源 URI。</span><span class="sxs-lookup"><span data-stu-id="55e80-136">toouse hello SAS tooaccess a container in Azure Storage, you need tooappend hello SAS token string toohello resource URI.</span></span> <span data-ttu-id="55e80-137">hello 資源的 URI，連同 hello 附加 SAS 權杖，並提供已驗證的存取 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="55e80-137">hello resource URI, together with hello appended SAS token, provides authenticated access tooAzure Storage.</span></span>

<span data-ttu-id="55e80-138">hello 下列範例顯示如何 tooget 唯寫 SAS 權杖字串 hello 容器，然後再附加 hello SAS toohello 容器的 URI:</span><span class="sxs-lookup"><span data-stu-id="55e80-138">hello following example shows how tooget a write-only SAS token string for hello container, then appends hello SAS toohello container URI:</span></span>

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a><span data-ttu-id="55e80-139">指定工作輸出的輸出檔案</span><span class="sxs-lookup"><span data-stu-id="55e80-139">Specify output files for task output</span></span>

<span data-ttu-id="55e80-140">對於工作而言 toospecify 輸出檔案建立的集合[OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile)物件，並將它指派 toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles)建立 hello 工作時的屬性。</span><span class="sxs-lookup"><span data-stu-id="55e80-140">toospecify output files for a task, create a collection of [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) objects and assign it toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) property when you create hello task.</span></span> 

<span data-ttu-id="55e80-141">hello 下列.NET 程式碼範例建立的工作寫入名為隨機數字 tooa 檔`output.txt`。</span><span class="sxs-lookup"><span data-stu-id="55e80-141">hello following .NET code example creates a task that writes random numbers tooa file named `output.txt`.</span></span> <span data-ttu-id="55e80-142">hello 範例建立輸出檔案以供`output.txt`toobe 寫入 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="55e80-142">hello example creates an output file for `output.txt` toobe written toohello container.</span></span> <span data-ttu-id="55e80-143">hello 範例也會建立任何符合 hello 檔案模式的記錄檔的輸出檔`std*.txt`(_例如_，`stdout.txt`和`stderr.txt`)。</span><span class="sxs-lookup"><span data-stu-id="55e80-143">hello example also creates output files for any log files that match hello file pattern `std*.txt` (_e.g._, `stdout.txt` and `stderr.txt`).</span></span> <span data-ttu-id="55e80-144">hello 容器 URL 需要 hello 所建立的 SAS 先前 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="55e80-144">hello container URL requires hello SAS that was created previously for hello container.</span></span> <span data-ttu-id="55e80-145">hello 批次服務會使用 hello SAS tooauthenticate 存取 toohello 容器：</span><span class="sxs-lookup"><span data-stu-id="55e80-145">hello Batch service uses hello SAS tooauthenticate access toohello container:</span></span> 

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

### <a name="specify-a-file-pattern-for-matching"></a><span data-ttu-id="55e80-146">指定要進行比對的檔案模式</span><span class="sxs-lookup"><span data-stu-id="55e80-146">Specify a file pattern for matching</span></span>

<span data-ttu-id="55e80-147">當您指定的輸出檔時，您可以使用 hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern)屬性 toospecify 檔案模式進行比對。</span><span class="sxs-lookup"><span data-stu-id="55e80-147">When you specify an output file, you can use hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) property toospecify a file pattern for matching.</span></span> <span data-ttu-id="55e80-148">hello 檔案模式可能會比對零檔案、 單一檔案或一組 hello 工作所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="55e80-148">hello file pattern may match zero files, a single file, or a set of files that are created by hello task.</span></span>

<span data-ttu-id="55e80-149">hello **FilePattern**屬性支援標準 filesystem 萬用字元，例如`*`（適用於非遞迴會比對） 和`**`（適用於遞迴會比對）。</span><span class="sxs-lookup"><span data-stu-id="55e80-149">hello **FilePattern** property supports standard filesystem wildcards such as `*` (for non-recursive matches) and `**` (for recursive matches).</span></span> <span data-ttu-id="55e80-150">例如，上述的 hello 程式碼範例指定 hello 檔案模式 toomatch`std*.txt`非遞迴的方式：</span><span class="sxs-lookup"><span data-stu-id="55e80-150">For example, hello code sample above specifies hello file pattern toomatch `std*.txt` non-recursively:</span></span> 

`filePattern: @"..\std*.txt"`

<span data-ttu-id="55e80-151">tooupload 單一檔案，且不包含萬用字元指定檔案模式。</span><span class="sxs-lookup"><span data-stu-id="55e80-151">tooupload a single file, specify a file pattern with no wildcards.</span></span> <span data-ttu-id="55e80-152">例如，上述的 hello 程式碼範例指定 hello 檔案模式 toomatch `output.txt`:</span><span class="sxs-lookup"><span data-stu-id="55e80-152">For example, hello code sample above specifies hello file pattern toomatch `output.txt`:</span></span>

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a><span data-ttu-id="55e80-153">指定上傳條件</span><span class="sxs-lookup"><span data-stu-id="55e80-153">Specify an upload condition</span></span>

<span data-ttu-id="55e80-154">hello [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition)屬性允許條件式的輸出檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="55e80-154">hello [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) property permits conditional uploading of output files.</span></span> <span data-ttu-id="55e80-155">如果失敗，常見的案例是 tooupload 一組檔案，如果 hello 工作成功和一組不同的檔案。</span><span class="sxs-lookup"><span data-stu-id="55e80-155">A common scenario is tooupload one set of files if hello task succeeds, and a different set of files if it fails.</span></span> <span data-ttu-id="55e80-156">比方說，您可能在 hello 工作失敗而結束，則為非零結束代碼時，才想 tooupload 詳細資訊記錄檔。</span><span class="sxs-lookup"><span data-stu-id="55e80-156">For example, you may want tooupload verbose log files only when hello task fails and exits with a nonzero exit code.</span></span> <span data-ttu-id="55e80-157">同樣地，您可能想 tooupload 結果檔案才 hello 工作成功，因為這些檔案可能會遺失或不完整，如果 hello 工作失敗。</span><span class="sxs-lookup"><span data-stu-id="55e80-157">Similarly, you may want tooupload result files only if hello task succeeds, as those files may be missing or incomplete if hello task fails.</span></span>

<span data-ttu-id="55e80-158">hello 上述程式碼範例會設定 hello **UploadCondition**屬性太**TaskCompletion**。</span><span class="sxs-lookup"><span data-stu-id="55e80-158">hello code sample above sets hello **UploadCondition** property too**TaskCompletion**.</span></span> <span data-ttu-id="55e80-159">此設定會指定該 hello 檔案是 toobe 上傳之後 hello 工作完成時，不論 hello hello 結束代碼值。</span><span class="sxs-lookup"><span data-stu-id="55e80-159">This setting specifies that hello file is toobe uploaded after hello tasks completes, regardless of hello value of hello exit code.</span></span> 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

<span data-ttu-id="55e80-160">如需其他設定，請參閱 hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition)列舉。</span><span class="sxs-lookup"><span data-stu-id="55e80-160">For other settings, see hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.</span></span>

### <a name="disambiguate-files-with-hello-same-name"></a><span data-ttu-id="55e80-161">釐清具有 hello 檔案相同的名稱</span><span class="sxs-lookup"><span data-stu-id="55e80-161">Disambiguate files with hello same name</span></span>

<span data-ttu-id="55e80-162">作業中的 hello 工作可能會產生具有 hello 檔案相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="55e80-162">hello tasks in a job may produce files that have hello same name.</span></span> <span data-ttu-id="55e80-163">例如，`stdout.txt` 和 `stderr.txt` 是針對作業中執行的每項工作所建立。</span><span class="sxs-lookup"><span data-stu-id="55e80-163">For example, `stdout.txt` and `stderr.txt` are created for every task that runs in a job.</span></span> <span data-ttu-id="55e80-164">因為在它自己的內容中，執行每項工作，這些檔案不衝突 hello 節點的檔案系統上。</span><span class="sxs-lookup"><span data-stu-id="55e80-164">Because each task runs in its own context, these files don't conflict on hello node's file system.</span></span> <span data-ttu-id="55e80-165">不過，當您上傳檔案，從多個工作 tooa 共用容器，您必須先以 hello toodisambiguate 檔案相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="55e80-165">However, when you upload files from multiple tasks tooa shared container, you'll need toodisambiguate files with hello same name.</span></span>

<span data-ttu-id="55e80-166">hello [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path)屬性會指定 hello 目的地 blob 或輸出檔的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="55e80-166">hello [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) property specifies hello destination blob or virtual directory for output files.</span></span> <span data-ttu-id="55e80-167">您可以使用 hello**路徑**屬性 tooname hello blob 或虛擬目錄的方式輸出檔案具有相同的名稱為唯一名稱在 Azure 儲存體中的 hello。</span><span class="sxs-lookup"><span data-stu-id="55e80-167">You can use hello **Path** property tooname hello blob or virtual directory in such a way that output files with hello same name are uniquely named in Azure Storage.</span></span> <span data-ttu-id="55e80-168">使用 hello 路徑中的 hello 工作識別碼的好方法 tooensure 唯一名稱，並輕鬆地找出檔案。</span><span class="sxs-lookup"><span data-stu-id="55e80-168">Using hello task ID in hello path is a good way tooensure unique names and easily identify files.</span></span>

<span data-ttu-id="55e80-169">如果 hello **FilePattern**屬性設定 tooa 萬用字元運算式，則符合 hello 模式的所有檔案都必須上傳的 toohello hello 所指定的虛擬目錄**路徑**屬性。</span><span class="sxs-lookup"><span data-stu-id="55e80-169">If hello **FilePattern** property is set tooa wildcard expression, then all files that match hello pattern are uploaded toohello virtual directory specified by hello **Path** property.</span></span> <span data-ttu-id="55e80-170">例如，如果 hello 容器是`mycontainer`，hello 工作識別碼是`mytask`，hello 檔案模式，且`..\std*.txt`，然後 hello 的絕對 Uri toohello 輸出檔，在 Azure 儲存體將會類似於：</span><span class="sxs-lookup"><span data-stu-id="55e80-170">For example, if hello container is `mycontainer`, hello task ID is `mytask`, and hello file pattern is `..\std*.txt`, then hello absolute URIs toohello output files in Azure Storage will be similar to:</span></span>

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

<span data-ttu-id="55e80-171">如果 hello **FilePattern**屬性集 toomatch 單一檔案名稱，亦即它不包含任何萬用字元的字元，然後 hello 值 hello**路徑**屬性會指定 hello 完整格式的 blob 名稱.</span><span class="sxs-lookup"><span data-stu-id="55e80-171">If hello **FilePattern** property is set toomatch a single file name, meaning it does not contain any wildcard characters, then hello value of hello **Path** property specifies hello fully qualified blob name.</span></span> <span data-ttu-id="55e80-172">如果您預期會發生命名衝突，使用多個工作的單一檔案，然後將 hello hello 虛擬目錄名稱的一部分 hello 檔案名稱 toodisambiguate 這些檔案。</span><span class="sxs-lookup"><span data-stu-id="55e80-172">If you anticipate naming conflicts with a single file from multiple tasks, then include hello name of hello virtual directory as part of hello file name toodisambiguate those files.</span></span> <span data-ttu-id="55e80-173">比方說，集 hello**路徑**屬性 tooinclude hello 工作 ID、 hello 分隔符號字元 （通常是正斜線），以及 hello 檔案名稱：</span><span class="sxs-lookup"><span data-stu-id="55e80-173">For example, set hello **Path** property tooinclude hello task ID, hello delimiter character (typically a forward slash), and hello file name:</span></span>

`path: taskId + @"/output.txt"`

<span data-ttu-id="55e80-174">hello 絕對 Uri toohello 輸出檔的一組工作將會類似於：</span><span class="sxs-lookup"><span data-stu-id="55e80-174">hello absolute URIs toohello output files for a set of tasks will be similar to:</span></span>

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

<span data-ttu-id="55e80-175">如需有關 Azure 儲存體中的虛擬目錄的詳細資訊，請參閱[列出容器中的 hello blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container)。</span><span class="sxs-lookup"><span data-stu-id="55e80-175">For more information about virtual directories in Azure Storage, see [List hello blobs in a container](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).</span></span>


## <a name="diagnose-file-upload-errors"></a><span data-ttu-id="55e80-176">診斷檔案上傳錯誤</span><span class="sxs-lookup"><span data-stu-id="55e80-176">Diagnose file upload errors</span></span>

<span data-ttu-id="55e80-177">如果上傳輸出檔案 tooAzure 存放裝置失敗，則 hello 工作可將移 toohello**已完成**狀態和 hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation)屬性設定。</span><span class="sxs-lookup"><span data-stu-id="55e80-177">If uploading output files tooAzure Storage fails, then hello task moves toohello **Completed** state and hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) property is set.</span></span> <span data-ttu-id="55e80-178">檢查 hello **FailureInformation**屬性 toodetermine 發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="55e80-178">Examine hello **FailureInformation** property toodetermine what error occurred.</span></span> <span data-ttu-id="55e80-179">比方說，以下是發生在檔案上傳，如果找不到 hello 容器發生錯誤：</span><span class="sxs-lookup"><span data-stu-id="55e80-179">For example, here is an error that occurs on file upload if hello container cannot be found:</span></span> 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

<span data-ttu-id="55e80-180">在每個檔案上傳，批次寫入這兩個記錄檔 toohello 計算節點，`fileuploadout.txt`和`fileuploaderr.txt`。</span><span class="sxs-lookup"><span data-stu-id="55e80-180">On every file upload, Batch writes two log files toohello compute node, `fileuploadout.txt` and `fileuploaderr.txt`.</span></span> <span data-ttu-id="55e80-181">您可以檢查這些記錄檔 toolearn 更多關於特定錯誤。</span><span class="sxs-lookup"><span data-stu-id="55e80-181">You can examine these log files toolearn more about a specific failure.</span></span> <span data-ttu-id="55e80-182">在其中 hello 檔案上傳永遠不會嘗試，例如因為 hello 工作本身無法執行的情況下，然後這些記錄檔不會存在。</span><span class="sxs-lookup"><span data-stu-id="55e80-182">In cases where hello file upload was never attempted, for example because hello task itself couldn’t run, then these log files will not exist.</span></span>

## <a name="diagnose-file-upload-performance"></a><span data-ttu-id="55e80-183">診斷檔案上傳效能</span><span class="sxs-lookup"><span data-stu-id="55e80-183">Diagnose file upload performance</span></span>

<span data-ttu-id="55e80-184">hello`fileuploadout.txt`檔案記錄上傳進度。</span><span class="sxs-lookup"><span data-stu-id="55e80-184">hello `fileuploadout.txt` file logs upload progress.</span></span> <span data-ttu-id="55e80-185">您可以檢查這個檔案 toolearn，花費更多有關您的檔案上傳的時間長度。</span><span class="sxs-lookup"><span data-stu-id="55e80-185">You can examine this file toolearn more about how long your file uploads are taking.</span></span> <span data-ttu-id="55e80-186">記住有許多促成因素 tooupload 效能，hello hello 目標容器是否包括 hello 大小 hello 節點，hello 節點上的 hello 上載 hello 次的其他活動與 hello 批次集區有相同的區域，多少節點是正在上傳相同的時間、 和等的 hello toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="55e80-186">Keep in mind that there are many contributing factors tooupload performance, including hello size of hello node, other activity on hello node at hello time of hello upload, whether hello target container is in hello same region as hello Batch pool, how many nodes are uploading toohello storage account at hello same time, and so on.</span></span>

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a><span data-ttu-id="55e80-187">使用標準的批次檔慣例 hello hello 批次服務 API</span><span class="sxs-lookup"><span data-stu-id="55e80-187">Use hello Batch service API with hello Batch File Conventions standard</span></span>

<span data-ttu-id="55e80-188">當您在工作輸出以 hello 批次服務 API 時，您可以命名您的目的地容器和 blob 不過嗎。</span><span class="sxs-lookup"><span data-stu-id="55e80-188">When you persist task output with hello Batch service API, you can name your destination container and blobs however you like.</span></span> <span data-ttu-id="55e80-189">您也可以選擇 tooname 它們根據 toohello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。</span><span class="sxs-lookup"><span data-stu-id="55e80-189">You can also choose tooname them according toohello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="55e80-190">hello 檔案慣例標準決定 hello 名稱 hello 目的地容器和 blob 在 Azure 儲存體 hello 的 hello 作業和工作的名稱為基礎的給定的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="55e80-190">hello File Conventions standard determines hello names of hello destination container and blob in Azure Storage for a given output file based on hello names of hello job and task.</span></span> <span data-ttu-id="55e80-191">如果您使用 hello 標準檔案慣例來命名輸出檔案，則輸出檔可供檢視之 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="55e80-191">If you do use hello File Conventions standard for naming output files, then your output files are available for viewing in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="55e80-192">如果您正在開發在 C# 中，您可以使用內建 hello 的 hello 方法[批次檔慣例.NET 程式庫](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files)。</span><span class="sxs-lookup"><span data-stu-id="55e80-192">If you are developing in C#, you can use hello methods built into hello [Batch File Conventions library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files).</span></span> <span data-ttu-id="55e80-193">此程式庫建立 hello 正確命名為您的容器和 blob 路徑。</span><span class="sxs-lookup"><span data-stu-id="55e80-193">This library creates hello properly named containers and blob paths for you.</span></span> <span data-ttu-id="55e80-194">例如，您可以呼叫 hello API tooget hello 正確 hello 容器名稱，根據 hello 工作名稱：</span><span class="sxs-lookup"><span data-stu-id="55e80-194">For example, you can call hello API tooget hello correct name for hello container, based on hello job name:</span></span>

```csharp
string containerName = job.OutputStorageContainerName();
```

<span data-ttu-id="55e80-195">您可以使用 hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl)方法 tooreturn 是使用的 toowrite toohello 容器的共用的存取簽章 (SAS) URL。</span><span class="sxs-lookup"><span data-stu-id="55e80-195">You can use hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) method tooreturn a shared access signature (SAS) URL that is used toowrite toohello container.</span></span> <span data-ttu-id="55e80-196">接著，您可以將此 SAS toohello [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination)建構函式。</span><span class="sxs-lookup"><span data-stu-id="55e80-196">You can then pass this SAS toohello [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) constructor.</span></span>

<span data-ttu-id="55e80-197">如果您正在開發 C# 以外的語言，您將自己需要 tooimplement hello 檔案慣例標準。</span><span class="sxs-lookup"><span data-stu-id="55e80-197">If you are developing in a language other than C#, you will need tooimplement hello File Conventions standard yourself.</span></span>

## <a name="code-sample"></a><span data-ttu-id="55e80-198">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="55e80-198">Code sample</span></span>

<span data-ttu-id="55e80-199">hello [PersistOutputs] [ github_persistoutputs]範例專案是其中一個 hello [Azure 批次程式碼範例][ github_samples] GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="55e80-199">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="55e80-200">這個 Visual Studio 方案會示範如何 toouse hello 批次用戶端程式庫.NET toopersist 工作輸出 toodurable 儲存體。</span><span class="sxs-lookup"><span data-stu-id="55e80-200">This Visual Studio solution demonstrates how toouse hello Batch client library for .NET toopersist task output toodurable storage.</span></span> <span data-ttu-id="55e80-201">toorun hello 範例，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="55e80-201">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="55e80-202">在開啟 hello 專案**2015年或更新版本的 Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="55e80-202">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="55e80-203">新增您的批次和儲存體**帳戶認證**太**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common 專案中。</span><span class="sxs-lookup"><span data-stu-id="55e80-203">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="55e80-204">**建置**（但不是會執行） hello 方案。</span><span class="sxs-lookup"><span data-stu-id="55e80-204">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="55e80-205">如果出現提示，請還原任何 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="55e80-205">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="55e80-206">使用 hello Azure 入口網站 tooupload[應用程式封裝](batch-application-packages.md)如**PersistOutputsTask**。</span><span class="sxs-lookup"><span data-stu-id="55e80-206">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="55e80-207">包含 hello `PersistOutputsTask.exe` hello.zip 套件中，設定 hello 應用程式識別碼及其相依組件太"PersistOutputsTask 」，以及 hello 應用程式封裝的版本太"1.0 的"。</span><span class="sxs-lookup"><span data-stu-id="55e80-207">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="55e80-208">**啟動**（執行） 的 hello **PersistOutputs**專案。</span><span class="sxs-lookup"><span data-stu-id="55e80-208">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="55e80-209">當提示的 toochoose hello 持續性技術 toouse 執行 hello 範例中，輸入**2** toorun hello 範例使用批次服務 API hello toopersist 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="55e80-209">When prompted toochoose hello persistence technology toouse for running hello sample, enter **2** toorun hello sample using hello Batch service API toopersist task output.</span></span>
7. <span data-ttu-id="55e80-210">如有需要，hello 範例再次執行，輸入**3** toopersist hello 批次服務 API，以及 tooname hello 目的地容器和 blob 路徑根據 toohello 檔案慣例標準輸出。</span><span class="sxs-lookup"><span data-stu-id="55e80-210">If desired, run hello sample again, entering **3** toopersist output with hello Batch service API, and also tooname hello destination container and blob path according toohello File Conventions standard.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55e80-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="55e80-211">Next steps</span></span>

- <span data-ttu-id="55e80-212">For.NET 上保存的工作輸出與 hello 檔案慣例媒體櫃資訊，請參閱[保存作業和工作資料 tooAzure 儲存體與 hello.NET toopersist 的批次檔慣例文件庫](batch-task-output-file-conventions.md)。</span><span class="sxs-lookup"><span data-stu-id="55e80-212">For more information on persisting task output with hello File Conventions library for .NET, see [Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist ](batch-task-output-file-conventions.md).</span></span>
- <span data-ttu-id="55e80-213">在 Azure 批次中保存的輸出資料的其他方法的資訊，請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="55e80-213">For information on other approaches for persisting output data in Azure Batch, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span>

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
