---
title: "使用 Azure Batch 服務 API 將作業和工作輸出保存到 Azure 儲存體 | Microsoft Docs"
description: "了解如何使用 Batch 服務 API 將工作和作業輸出保存到 Azure 儲存體。"
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
ms.openlocfilehash: 2530b7c20347b9fb58aee4dfe693847cf3911741
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="persist-task-data-to-azure-storage-with-the-batch-service-api"></a><span data-ttu-id="7fdc0-103">使用 Batch 服務 API 將工作資料保存到 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="7fdc0-103">Persist task data to Azure Storage with the Batch service API</span></span>

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="7fdc0-104">從 2017-05-01 版開始，Batch 服務 API 針對使用虛擬機器設定在集區上執行的工作和作業管理員工作，支援將輸出資料保存到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-104">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools with the virtual machine configuration.</span></span> <span data-ttu-id="7fdc0-105">當您新增工作時，可以指定 Azure 儲存體中的容器作為工作輸出的目的地。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-105">When you add a task, you can specify a container in Azure Storage as the destination for the task's output.</span></span> <span data-ttu-id="7fdc0-106">當工作完成時，Batch 服務就會將任何輸出資料寫入該容器中。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-106">The Batch service then writes any output data to that container when the task is complete.</span></span>

<span data-ttu-id="7fdc0-107">使用 Batch 服務 API 來保存工作輸出的好處，是您不需要修改工作正在執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-107">An advantage to using the Batch service API to persist task output is that you do not need to modify the application that the task is running.</span></span> <span data-ttu-id="7fdc0-108">相反地，您可以對用戶端應用程式進行幾個簡單的修改，從建立工作的程式碼內保存工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-108">Instead, with a few simple modifications to your client application, you can persist the task's output from within the code that creates the task.</span></span>   

## <a name="when-do-i-use-the-batch-service-api-to-persist-task-output"></a><span data-ttu-id="7fdc0-109">何時使用 Batch 服務 API 來保存工作輸出？</span><span class="sxs-lookup"><span data-stu-id="7fdc0-109">When do I use the Batch service API to persist task output?</span></span>

<span data-ttu-id="7fdc0-110">Azure Batch 提供多個方法來保存工作輸出。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-110">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="7fdc0-111">使用 Batch 服務 API 是一個便利方式，最適合下列情節：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-111">Using the Batch service API is a convenient approach that's best suited to these scenarios:</span></span>

- <span data-ttu-id="7fdc0-112">您需要撰寫程式碼，以從用戶端應用程式內保存工作輸出，而不需要修改您工作正在執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-112">You want to write code to persist task output from within your client application, without modifying the application that your task is running.</span></span>
- <span data-ttu-id="7fdc0-113">您需要保存的輸出，是來自使用虛擬機器設定在集區中建立的 Batch 工作和作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-113">You want to persist output from Batch tasks and job manager tasks in pools created with the virtual machine configuration.</span></span>
- <span data-ttu-id="7fdc0-114">您需要將輸出保存到具有任意名稱的 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-114">You want to persist output to an Azure Storage container with an arbitrary name.</span></span>
- <span data-ttu-id="7fdc0-115">您需要將輸出保存到根據 [Batch 檔案慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)命名的 Azure 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-115">You want to persist output to an Azure Storage container named according to the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> 

<span data-ttu-id="7fdc0-116">如果您的情節與以上所列不同，可能需要考慮不同的方法。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-116">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="7fdc0-117">例如，Batch 服務 API 目前不支援在工作執行時將輸出串流至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-117">For example, the Batch service API does not currently support streaming output to Azure Storage while the task is running.</span></span> <span data-ttu-id="7fdc0-118">若要將輸出串流，請考慮使用適用於 .NET 的 Batch 檔案慣例程式庫。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-118">To stream output, consider using the Batch File Conventions library, available for .NET.</span></span> <span data-ttu-id="7fdc0-119">針對其他語言，您必須實作自己的解決方案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-119">For other languages, you'll need to implement your own solution.</span></span> <span data-ttu-id="7fdc0-120">如需保存工作輸出之其他選項的詳細資訊，請參閱[將作業和工作輸出保存到 Azure 儲存體](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-120">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="create-a-container-in-azure-storage"></a><span data-ttu-id="7fdc0-121">在 Azure 儲存體中建立容器</span><span class="sxs-lookup"><span data-stu-id="7fdc0-121">Create a container in Azure Storage</span></span>

<span data-ttu-id="7fdc0-122">若要將工作輸出保存到 Azure 儲存體，您必須建立容器來作為輸出檔案的目的地。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-122">To persist task output to Azure Storage, you'll need to create a container that serves as the destination for your output files.</span></span> <span data-ttu-id="7fdc0-123">在執行工作之前，最好是在提交作業之前建立容器。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-123">Create the container before you run your task, preferably before you submit your job.</span></span> <span data-ttu-id="7fdc0-124">若要建立容器，請使用適當的 Azure 儲存體用戶端程式庫或 SDK。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-124">To create the container, use the appropriate Azure Storage client library or SDK.</span></span> <span data-ttu-id="7fdc0-125">如需有關「Azure 儲存體 API」的資訊，請參閱 [Azure 儲存體文件](https://docs.microsoft.com/azure/storage/)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-125">For more information about Azure Storage APIs, see the [Azure Storage documentation](https://docs.microsoft.com/azure/storage/).</span></span>

<span data-ttu-id="7fdc0-126">例如，如果您要以 C# 撰寫應用程式，請使用[適用於 .NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage/)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-126">For example, if you are writing your application in C#, use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="7fdc0-127">下列範例說明如何建立容器：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-127">The following example shows how to create a container:</span></span>

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-the-container"></a><span data-ttu-id="7fdc0-128">取得容器的共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="7fdc0-128">Get a shared access signature for the container</span></span>

<span data-ttu-id="7fdc0-129">建立容器之後，可使用寫入容器的存取權取得共用的存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-129">After you create the container, get a shared access signature (SAS) with write access to the container.</span></span> <span data-ttu-id="7fdc0-130">SAS 會提供委派存取權給容器。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-130">A SAS provides delegated access to the container.</span></span> <span data-ttu-id="7fdc0-131">SAS 會使用一組指定的權限，以及一段指定的時間間隔來授與存取權。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-131">The SAS grants access with a specified set of permissions and over a specified time interval.</span></span> <span data-ttu-id="7fdc0-132">Batch 服務需要具有寫入權限的 SAS，才能將工作輸出寫入容器中。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-132">The Batch service needs a SAS with write permissions to write task output to the container.</span></span> <span data-ttu-id="7fdc0-133">如需關於 SAS 的詳細資訊，請參閱[在 Azure 儲存體中使用共用存取簽章 \(SAS\)](../storage/common/storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-133">For more information about SAS, see [Using shared access signatures \(SAS\) in Azure Storage](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

<span data-ttu-id="7fdc0-134">當您使用 Azure 儲存體 API 取得 SAS 時，API 會傳回 SAS 權杖字串。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-134">When you get a SAS using the Azure Storage APIs, the API returns a SAS token string.</span></span> <span data-ttu-id="7fdc0-135">這個權杖字串會包含 SAS 的所有參數，包括權限和 SAS 有效的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-135">This token string includes all parameters of the SAS, including the permissions and the interval over which the SAS is valid.</span></span> <span data-ttu-id="7fdc0-136">若要使用 SAS 存取 Azure 儲存體中的容器，您必須將 SAS 權杖字串附加至資源 URI。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-136">To use the SAS to access a container in Azure Storage, you need to append the SAS token string to the resource URI.</span></span> <span data-ttu-id="7fdc0-137">資源的 URI 以及附加的 SAS 權杖會共同提供 Azure 儲存體的已驗證存取。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-137">The resource URI, together with the appended SAS token, provides authenticated access to Azure Storage.</span></span>

<span data-ttu-id="7fdc0-138">下列範例說明如何取得容器的唯寫 SAS 權杖字串，然後會將 SAS 附加至容器 URI：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-138">The following example shows how to get a write-only SAS token string for the container, then appends the SAS to the container URI:</span></span>

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a><span data-ttu-id="7fdc0-139">指定工作輸出的輸出檔案</span><span class="sxs-lookup"><span data-stu-id="7fdc0-139">Specify output files for task output</span></span>

<span data-ttu-id="7fdc0-140">若要指定工作的輸出檔案，請建立 [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) 物件的集合，並當您建立這項工作時，將它指派給 [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) 屬性。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-140">To specify output files for a task, create a collection of [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) objects and assign it to the [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) property when you create the task.</span></span> 

<span data-ttu-id="7fdc0-141">下列 .NET 程式碼範例所建立的工作，會將隨機數字寫入名為 `output.txt` 的檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-141">The following .NET code example creates a task that writes random numbers to a file named `output.txt`.</span></span> <span data-ttu-id="7fdc0-142">此範例會建立要寫入容器中的 `output.txt` 之輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-142">The example creates an output file for `output.txt` to be written to the container.</span></span> <span data-ttu-id="7fdc0-143">此範例也會建立任何比對檔案模式之記錄檔的輸出檔案`std*.txt` (_例如_ 、`stdout.txt` 和 `stderr.txt`)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-143">The example also creates output files for any log files that match the file pattern `std*.txt` (_e.g._, `stdout.txt` and `stderr.txt`).</span></span> <span data-ttu-id="7fdc0-144">容器 URL 需要先前針對容器建立的 SAS。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-144">The container URL requires the SAS that was created previously for the container.</span></span> <span data-ttu-id="7fdc0-145">Batch 服務會使用 SAS 來驗證容器的存取權：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-145">The Batch service uses the SAS to authenticate access to the container:</span></span> 

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

### <a name="specify-a-file-pattern-for-matching"></a><span data-ttu-id="7fdc0-146">指定要進行比對的檔案模式</span><span class="sxs-lookup"><span data-stu-id="7fdc0-146">Specify a file pattern for matching</span></span>

<span data-ttu-id="7fdc0-147">當您指定輸出檔案時，可以使用 [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) 屬性來指定要進行比對的檔案模式。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-147">When you specify an output file, you can use the [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) property to specify a file pattern for matching.</span></span> <span data-ttu-id="7fdc0-148">檔案模式可能會比對零個檔案、單一檔案或工作所建立的一組檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-148">The file pattern may match zero files, a single file, or a set of files that are created by the task.</span></span>

<span data-ttu-id="7fdc0-149">**FilePattern** 屬性會支援標準檔案系統萬用字元，例如 `*` (適用於非遞迴比對) 和 `**` (適用於遞迴比對)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-149">The **FilePattern** property supports standard filesystem wildcards such as `*` (for non-recursive matches) and `**` (for recursive matches).</span></span> <span data-ttu-id="7fdc0-150">例如，上述程式碼範例會指定檔案模式以非遞迴的方式比對 `std*.txt`：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-150">For example, the code sample above specifies the file pattern to match `std*.txt` non-recursively:</span></span> 

`filePattern: @"..\std*.txt"`

<span data-ttu-id="7fdc0-151">若要上傳單一檔案，請指定不包含萬用字元的檔案模式。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-151">To upload a single file, specify a file pattern with no wildcards.</span></span> <span data-ttu-id="7fdc0-152">例如，上述程式碼範例會指定檔案模式比對 `output.txt`：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-152">For example, the code sample above specifies the file pattern to match `output.txt`:</span></span>

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a><span data-ttu-id="7fdc0-153">指定上傳條件</span><span class="sxs-lookup"><span data-stu-id="7fdc0-153">Specify an upload condition</span></span>

<span data-ttu-id="7fdc0-154">[OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) 屬性允許條件式上傳輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-154">The [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) property permits conditional uploading of output files.</span></span> <span data-ttu-id="7fdc0-155">常見的情節是，如果工作成功就上傳一組檔案，如果失敗就上傳一組不同的檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-155">A common scenario is to upload one set of files if the task succeeds, and a different set of files if it fails.</span></span> <span data-ttu-id="7fdc0-156">例如，只有在工作失敗且以非零結束代碼結束時，您才需要將詳細資訊記錄檔上傳。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-156">For example, you may want to upload verbose log files only when the task fails and exits with a nonzero exit code.</span></span> <span data-ttu-id="7fdc0-157">同樣地，只有當工作成功時，您才需要將結果檔案上載，因為如果工作失敗，這些檔案可能就會遺失或不完整。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-157">Similarly, you may want to upload result files only if the task succeeds, as those files may be missing or incomplete if the task fails.</span></span>

<span data-ttu-id="7fdc0-158">上述程式碼範例會將 **UploadCondition** 屬性設為 **TaskCompletion**。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-158">The code sample above sets the **UploadCondition** property to **TaskCompletion**.</span></span> <span data-ttu-id="7fdc0-159">此設定會指定在工作完成之後才將檔案上傳，無論結束代碼的值為何。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-159">This setting specifies that the file is to be uploaded after the tasks completes, regardless of the value of the exit code.</span></span> 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

<span data-ttu-id="7fdc0-160">如需其他設定，請參閱 [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) 列舉。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-160">For other settings, see the [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.</span></span>

### <a name="disambiguate-files-with-the-same-name"></a><span data-ttu-id="7fdc0-161">釐清具有相同名稱的檔案</span><span class="sxs-lookup"><span data-stu-id="7fdc0-161">Disambiguate files with the same name</span></span>

<span data-ttu-id="7fdc0-162">作業中的工作可能會產生具有相同名稱的檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-162">The tasks in a job may produce files that have the same name.</span></span> <span data-ttu-id="7fdc0-163">例如，`stdout.txt` 和 `stderr.txt` 是針對作業中執行的每項工作所建立。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-163">For example, `stdout.txt` and `stderr.txt` are created for every task that runs in a job.</span></span> <span data-ttu-id="7fdc0-164">每項工作都會在自己的內容中執行，因此這些檔案在節點的檔案系統上不會產生衝突。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-164">Because each task runs in its own context, these files don't conflict on the node's file system.</span></span> <span data-ttu-id="7fdc0-165">不過，當您從多個工作將檔案上傳至共用的容器時，必須將具有相同名稱的檔案加以釐清。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-165">However, when you upload files from multiple tasks to a shared container, you'll need to disambiguate files with the same name.</span></span>

<span data-ttu-id="7fdc0-166">[OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) 屬性會指定目的地 blob 或輸出檔案的虛擬目錄。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-166">The [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) property specifies the destination blob or virtual directory for output files.</span></span> <span data-ttu-id="7fdc0-167">您可以使用 **Path** 屬性來命名 blob 或虛擬目錄，方法是將具有相同名稱的輸出檔案在 Azure 儲存體中以唯一方式命名。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-167">You can use the **Path** property to name the blob or virtual directory in such a way that output files with the same name are uniquely named in Azure Storage.</span></span> <span data-ttu-id="7fdc0-168">在路徑中使用工作識別碼，是確保唯一名稱並可輕鬆識別檔案的好方法。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-168">Using the task ID in the path is a good way to ensure unique names and easily identify files.</span></span>

<span data-ttu-id="7fdc0-169">如果 **FilePattern** 屬性設為萬用字元運算式，則比對模式的所有檔案都會上傳到 **Path** 屬性所指定的虛擬目錄中。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-169">If the **FilePattern** property is set to a wildcard expression, then all files that match the pattern are uploaded to the virtual directory specified by the **Path** property.</span></span> <span data-ttu-id="7fdc0-170">例如，如果容器是 `mycontainer`、工作識別碼是 `mytask`，以及檔案模式是 `..\std*.txt`，Azure 儲存體中輸出檔案的絕對 URI 就會類似於：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-170">For example, if the container is `mycontainer`, the task ID is `mytask`, and the file pattern is `..\std*.txt`, then the absolute URIs to the output files in Azure Storage will be similar to:</span></span>

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

<span data-ttu-id="7fdc0-171">如果將 **FilePattern** 屬性設定為符合單一檔案名稱，表示它不包含任何萬用字元，**Path** 屬性的值就會指定完整的 blob 名稱。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-171">If the **FilePattern** property is set to match a single file name, meaning it does not contain any wildcard characters, then the value of the **Path** property specifies the fully qualified blob name.</span></span> <span data-ttu-id="7fdc0-172">如果您預期會與多個工作的單一檔案發生命名衝突，則可包含虛擬目錄的名稱作為檔案名稱的一部分，以釐清這些檔案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-172">If you anticipate naming conflicts with a single file from multiple tasks, then include the name of the virtual directory as part of the file name to disambiguate those files.</span></span> <span data-ttu-id="7fdc0-173">例如，設定 **Path** 屬性，可包括工作識別碼、分隔符號字元 (通常是正斜線)，以及檔案名稱：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-173">For example, set the **Path** property to include the task ID, the delimiter character (typically a forward slash), and the file name:</span></span>

`path: taskId + @"/output.txt"`

<span data-ttu-id="7fdc0-174">一組工作之輸出檔案的絕對 URI 將類似於：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-174">The absolute URIs to the output files for a set of tasks will be similar to:</span></span>

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

<span data-ttu-id="7fdc0-175">如需有關 Azure 儲存體中虛擬目錄的詳細資訊，請參閱[列出容器中的 blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-175">For more information about virtual directories in Azure Storage, see [List the blobs in a container](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).</span></span>


## <a name="diagnose-file-upload-errors"></a><span data-ttu-id="7fdc0-176">診斷檔案上傳錯誤</span><span class="sxs-lookup"><span data-stu-id="7fdc0-176">Diagnose file upload errors</span></span>

<span data-ttu-id="7fdc0-177">如果將輸出檔案上傳至 Azure 儲存體失敗，工作就會移至「**已完成**」狀態，且會設定 [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) 屬性。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-177">If uploading output files to Azure Storage fails, then the task moves to the **Completed** state and the [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) property is set.</span></span> <span data-ttu-id="7fdc0-178">檢查 **FailureInformation** 屬性來判斷所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-178">Examine the **FailureInformation** property to determine what error occurred.</span></span> <span data-ttu-id="7fdc0-179">例如，如果找不到容器，就會在檔案上傳時發生以下錯誤：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-179">For example, here is an error that occurs on file upload if the container cannot be found:</span></span> 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of the specified Azure container(s) was not found while attempting to upload an output file
```

<span data-ttu-id="7fdc0-180">在每次檔案上傳時，Batch 會將 `fileuploadout.txt` 和 `fileuploaderr.txt` 兩個記錄檔寫入計算節點中。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-180">On every file upload, Batch writes two log files to the compute node, `fileuploadout.txt` and `fileuploaderr.txt`.</span></span> <span data-ttu-id="7fdc0-181">若要進一步了解特定錯誤，您可以檢查這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-181">You can examine these log files to learn more about a specific failure.</span></span> <span data-ttu-id="7fdc0-182">在從未嘗試檔案上傳的案例中 (例如因為工作本身無法執行)，這些記錄檔就不會存在。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-182">In cases where the file upload was never attempted, for example because the task itself couldn’t run, then these log files will not exist.</span></span>

## <a name="diagnose-file-upload-performance"></a><span data-ttu-id="7fdc0-183">診斷檔案上傳效能</span><span class="sxs-lookup"><span data-stu-id="7fdc0-183">Diagnose file upload performance</span></span>

<span data-ttu-id="7fdc0-184">`fileuploadout.txt` 檔案會記錄上傳進度。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-184">The `fileuploadout.txt` file logs upload progress.</span></span> <span data-ttu-id="7fdc0-185">您可以檢查這個檔案，進一步了解您檔案上傳所需的時間。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-185">You can examine this file to learn more about how long your file uploads are taking.</span></span> <span data-ttu-id="7fdc0-186">請注意，上傳效能有許多促成因素，包括節點大小、上傳時節點上的其他活動、目標容器是否在相同區域中作為 Batch 集區、同時上傳至儲存體帳戶的節點數等等。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-186">Keep in mind that there are many contributing factors to upload performance, including the size of the node, other activity on the node at the time of the upload, whether the target container is in the same region as the Batch pool, how many nodes are uploading to the storage account at the same time, and so on.</span></span>

## <a name="use-the-batch-service-api-with-the-batch-file-conventions-standard"></a><span data-ttu-id="7fdc0-187">使用 Batch 服務 API 搭配 Batch 檔案慣例標準</span><span class="sxs-lookup"><span data-stu-id="7fdc0-187">Use the Batch service API with the Batch File Conventions standard</span></span>

<span data-ttu-id="7fdc0-188">當您使用 Batch 服務 API 來保存工作輸出時，可以隨您所好命名您的目的地容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-188">When you persist task output with the Batch service API, you can name your destination container and blobs however you like.</span></span> <span data-ttu-id="7fdc0-189">您也可以選擇根據 [Batch 檔案慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) 將它們命名。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-189">You can also choose to name them according to the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="7fdc0-190">檔案慣例標準會以作業和工作名稱作為基礎，針對給定之輸出檔案，決定 Azure 儲存體中的目的地容器和 blob 的名稱。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-190">The File Conventions standard determines the names of the destination container and blob in Azure Storage for a given output file based on the names of the job and task.</span></span> <span data-ttu-id="7fdc0-191">如果您要針對命名輸出檔案使用檔案慣例標準，您的輸出檔案就可在 [Azure 入口網站](https://portal.azure.com)中檢視。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-191">If you do use the File Conventions standard for naming output files, then your output files are available for viewing in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7fdc0-192">如果您要以 C# 進行開發，可以使用[適用於 .NET 的 Batch 檔案慣例程式庫](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files)的內建方法。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-192">If you are developing in C#, you can use the methods built into the [Batch File Conventions library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files).</span></span> <span data-ttu-id="7fdc0-193">此程式庫會為您建立正確命名的容器和 blob 路徑。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-193">This library creates the properly named containers and blob paths for you.</span></span> <span data-ttu-id="7fdc0-194">例如，您可以作業名稱作為基礎呼叫 API，來取得容器的正確名稱：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-194">For example, you can call the API to get the correct name for the container, based on the job name:</span></span>

```csharp
string containerName = job.OutputStorageContainerName();
```

<span data-ttu-id="7fdc0-195">您可以使用 [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) 方法，將用來寫入容器的共用存取簽章 (SAS) URL 傳回。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-195">You can use the [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) method to return a shared access signature (SAS) URL that is used to write to the container.</span></span> <span data-ttu-id="7fdc0-196">然後，您可以將此 SAS 傳遞到 [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) 建構函式。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-196">You can then pass this SAS to the [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) constructor.</span></span>

<span data-ttu-id="7fdc0-197">如果您要以 C# 以外的語言進行開發，必須自行實作檔案慣例標準。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-197">If you are developing in a language other than C#, you will need to implement the File Conventions standard yourself.</span></span>

## <a name="code-sample"></a><span data-ttu-id="7fdc0-198">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="7fdc0-198">Code sample</span></span>

<span data-ttu-id="7fdc0-199">[PersistOutputs][github_persistoutputs] 範例專案是 GitHub 上的其中一個 [Azure Batch 程式碼範例][github_samples]。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-199">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="7fdc0-200">此 Visual Studio 解決方案示範如何使用適用於 .NET 的 Batch 用戶端程式庫，將工作輸出保存到永久性儲存體。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-200">This Visual Studio solution demonstrates how to use the Batch client library for .NET to persist task output to durable storage.</span></span> <span data-ttu-id="7fdc0-201">若要執行範例，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7fdc0-201">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="7fdc0-202">在 **Visual Studio 2015 或更新版本**中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-202">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="7fdc0-203">將您 Batch 和儲存體的**帳戶認證**新增到 Microsoft.Azure.Batch.Samples.Common 專案中的 **AccountSettings.settings**。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-203">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="7fdc0-204"> (但不要執行) 該解決方案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-204">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="7fdc0-205">如果出現提示，請還原任何 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-205">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="7fdc0-206">使用 Azure 入口網站來為 [PersistOutputsTask](batch-application-packages.md) 上傳 **應用程式封裝**。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-206">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="7fdc0-207">將 `PersistOutputsTask.exe` 及其相依性組件包含在 .zip 封裝中，將應用程式識別碼和應用程式封裝版本分別設為 "PersistOutputsTask" 和 "1.0"。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-207">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="7fdc0-208">**啟動** (執行) **PersistOutputs** 專案。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-208">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="7fdc0-209">當系統提示您選擇要用於執行範例的持續性技術時，輸入 **2** 可使用 Batch 服務 API 保存工作輸出來執行範例。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-209">When prompted to choose the persistence technology to use for running the sample, enter **2** to run the sample using the Batch service API to persist task output.</span></span>
7. <span data-ttu-id="7fdc0-210">如需要，請再次執行範例，輸入 **3** 可使用 Batch 服務 API 保存輸出，並根據檔案慣例標準命名目的地容器和 blob 路徑。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-210">If desired, run the sample again, entering **3** to persist output with the Batch service API, and also to name the destination container and blob path according to the File Conventions standard.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fdc0-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7fdc0-211">Next steps</span></span>

- <span data-ttu-id="7fdc0-212">如需使用適用於 .NET 的檔案慣例程式庫來保存工作輸出的詳細資訊，請參閱[使用適用於 .NET 的 Batch 檔案慣例程式庫，將作業和工作資料保存到 Azure 儲存體](batch-task-output-file-conventions.md)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-212">For more information on persisting task output with the File Conventions library for .NET, see [Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist ](batch-task-output-file-conventions.md).</span></span>
- <span data-ttu-id="7fdc0-213">如需在 Azure Batch 中保存輸出資料之其他方法的相關資訊，請參閱[將作業和工作輸出保存到 Azure 儲存體](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="7fdc0-213">For information on other approaches for persisting output data in Azure Batch, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span>

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
