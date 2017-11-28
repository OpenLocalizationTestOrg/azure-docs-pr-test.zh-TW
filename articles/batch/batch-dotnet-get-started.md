---
title: "aaaTutorial-使用 hello Azure 批次用戶端程式庫適用於.NET |Microsoft 文件"
description: "深入了解 hello Azure Batch 基本概念，並建立使用適用於.NET 的簡易解決方案。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="5f357-103">開始建置適用於.NET 的解決方案與 hello 批次的用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="5f357-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f357-104">.NET</span><span class="sxs-lookup"><span data-stu-id="5f357-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="5f357-105">Python</span><span class="sxs-lookup"><span data-stu-id="5f357-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="5f357-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="5f357-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="5f357-107">了解 hello 基本概念的[Azure Batch] [ azure_batch]和 hello[批次.NET] [ net_api]本文章中的程式庫我們討論 C# 範例應用程式步驟的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f357-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="5f357-108">我們會審視如何 hello 範例應用程式會利用 hello 批次服務 tooprocess 平行的工作負載中 hello 雲端，以及它如何與互動[Azure 儲存體](../storage/common/storage-introduction.md)檔案暫存和擷取。</span><span class="sxs-lookup"><span data-stu-id="5f357-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="5f357-109">您將了解常見的批次應用程式工作流程和基底的 hello 主要元件批次的工作、 工作、 集區，例如了解計算節點。</span><span class="sxs-lookup"><span data-stu-id="5f357-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="5f357-110">![Batch 方案工作流程 (基本)][11]</span><span class="sxs-lookup"><span data-stu-id="5f357-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="5f357-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f357-111">Prerequisites</span></span>
<span data-ttu-id="5f357-112">本文假設您已具備 C# 和 Visual Studio 的使用知識。</span><span class="sxs-lookup"><span data-stu-id="5f357-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="5f357-113">它也假設您使用的是可以 toosatisfy hello 帳戶建立所指定需求的下面針對 Azure hello 批次和儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="5f357-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="5f357-114">帳戶</span><span class="sxs-lookup"><span data-stu-id="5f357-114">Accounts</span></span>
* <span data-ttu-id="5f357-115">**Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶][azure_free_account]。</span><span class="sxs-lookup"><span data-stu-id="5f357-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="5f357-116">**Batch 帳戶**：擁有 Azure 訂用帳戶後，請 [建立 Azure Batch 帳戶](batch-account-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="5f357-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="5f357-117">**儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="5f357-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f357-118">目前批次支援*只*hello**一般用途**儲存體帳戶類型，如步驟 5 中所述[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)中[關於 Azure儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="5f357-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="5f357-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5f357-119">Visual Studio</span></span>
<span data-ttu-id="5f357-120">您必須擁有**2015年或更新版本的 Visual Studio** toobuild hello 範例專案。</span><span class="sxs-lookup"><span data-stu-id="5f357-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="5f357-121">您可以在 hello 找到免費及試用版本的 Visual Studio[的 Visual Studio 產品概觀][visual_studio]。</span><span class="sxs-lookup"><span data-stu-id="5f357-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="5f357-122"> 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="5f357-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="5f357-123">hello [DotNetTutorial] [ github_dotnettutorial]範例是一個在 hello 中找到多個批次的程式碼範例的 hello [azure 批次範例][ github_samples]上的儲存機制GitHub。</span><span class="sxs-lookup"><span data-stu-id="5f357-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="5f357-124">您可以按一下 下載所有 hello 範例**複製或都下載 > 都下載 ZIP** hello 儲存機制首頁上，或按一下 hello [azure 批次範例-master.zip] [ github_samples_zip]直接下載連結。</span><span class="sxs-lookup"><span data-stu-id="5f357-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="5f357-125">一旦您已擷取 hello hello ZIP 檔案的內容，您可以找到下列資料夾的 hello hello 方案：</span><span class="sxs-lookup"><span data-stu-id="5f357-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="5f357-126">Azure Batch 總管 (選用)</span><span class="sxs-lookup"><span data-stu-id="5f357-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="5f357-127">hello [Azure 批次總管][ github_batchexplorer]是免費的公用程式隨附的 hello [azure 批次範例][ github_samples] GitHub 上的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="5f357-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="5f357-128">時不需要 toocomplete 本教學課程中，它可以時很實用開發及偵錯您批次的解決方案。</span><span class="sxs-lookup"><span data-stu-id="5f357-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="5f357-129">DotNetTutorial 範例專案概觀</span><span class="sxs-lookup"><span data-stu-id="5f357-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="5f357-130">hello *DotNetTutorial*程式碼範例是包含兩個專案的 Visual Studio 方案： **DotNetTutorial**和**TaskApplication**。</span><span class="sxs-lookup"><span data-stu-id="5f357-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="5f357-131">**DotNetTutorial**是平行計算節點 （虛擬機器） 上的工作負載之互動 hello 批次和儲存體服務 tooexecute hello 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f357-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="5f357-132">DotNetTutorial 會在本機工作站上執行。</span><span class="sxs-lookup"><span data-stu-id="5f357-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="5f357-133">**TaskApplication**是 hello Azure tooperform hello 實際工作中的計算節點執行的程式。</span><span class="sxs-lookup"><span data-stu-id="5f357-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="5f357-134">在 hello 範例`TaskApplication.exe`剖析 hello 下載自 Azure 儲存體 （hello 輸入檔） 的檔案中的文字。</span><span class="sxs-lookup"><span data-stu-id="5f357-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="5f357-135">然後它會產生文字檔案 （hello 輸出檔），其中包含出現在 hello 輸入檔中的 hello 前三個單字的清單。</span><span class="sxs-lookup"><span data-stu-id="5f357-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="5f357-136">它會建立 hello 輸出檔後，TaskApplication 會上傳 hello 檔案 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f357-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="5f357-137">這使得可用 toohello 下載的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f357-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="5f357-138">Hello 批次服務中的多個計算節點上，以平行方式執行 TaskApplication。</span><span class="sxs-lookup"><span data-stu-id="5f357-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="5f357-139">hello 下列圖表說明 hello hello 用戶端應用程式，所執行的主要作業*DotNetTutorial*，和 hello 應用程式所執行的 hello 工作*TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="5f357-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="5f357-140">此基本工作流程通常由使用 Batch 建立的許多計算方案所組成。</span><span class="sxs-lookup"><span data-stu-id="5f357-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="5f357-141">雖然它不會示範 hello 批次服務中可用的每一項功能，幾乎每個批次案例包含此工作流程的部分。</span><span class="sxs-lookup"><span data-stu-id="5f357-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="5f357-142">![Batch 範例工作流程][8]</span><span class="sxs-lookup"><span data-stu-id="5f357-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="5f357-143">**步驟 1.**</span><span class="sxs-lookup"><span data-stu-id="5f357-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="5f357-144">在 Azure Blob 儲存體中建立**容器**。</span><span class="sxs-lookup"><span data-stu-id="5f357-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="5f357-145">
[**步驟 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="5f357-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="5f357-146">上傳工作應用程式檔案和 toocontainers 輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="5f357-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="5f357-147">
[**步驟 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="5f357-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="5f357-148">建立 Batch **集區**。</span><span class="sxs-lookup"><span data-stu-id="5f357-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="5f357-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="5f357-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="5f357-150">hello 集區**StartTask**下載 hello 工作二進位檔案 (TaskApplication) toonodes，因為它們加入 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="5f357-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="5f357-151">
[**步驟 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="5f357-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="5f357-152">建立 Batch **作業**。</span><span class="sxs-lookup"><span data-stu-id="5f357-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="5f357-153">
[**步驟 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="5f357-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="5f357-154">新增**工作**toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="5f357-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="5f357-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="5f357-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="5f357-156">hello 工作是排定的 tooexecute 節點上。</span><span class="sxs-lookup"><span data-stu-id="5f357-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="5f357-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="5f357-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="5f357-158">每項工作會從 Azure 儲存體下載其輸入資料，然後開始執行。</span><span class="sxs-lookup"><span data-stu-id="5f357-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="5f357-159">
[**步驟 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="5f357-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="5f357-160">監視工作。</span><span class="sxs-lookup"><span data-stu-id="5f357-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="5f357-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="5f357-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="5f357-162">工作完成後，它們上傳其輸出資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5f357-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="5f357-163">
[**步驟 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="5f357-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="5f357-164">從儲存體下載工作輸出。</span><span class="sxs-lookup"><span data-stu-id="5f357-164">Download task output from Storage.</span></span>

<span data-ttu-id="5f357-165">如所述，並非每個批次解決方案會執行這些確切步驟，並可能包含更多，但 hello *DotNetTutorial*範例應用程式示範一般程序，在批次方案中找到。</span><span class="sxs-lookup"><span data-stu-id="5f357-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="5f357-166">建置 hello *DotNetTutorial*範例專案</span><span class="sxs-lookup"><span data-stu-id="5f357-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="5f357-167">您可以順利執行 hello 範例之前，您必須指定批次和儲存體帳戶認證在 hello *DotNetTutorial*專案的`Program.cs`檔案。</span><span class="sxs-lookup"><span data-stu-id="5f357-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="5f357-168">如果您尚未執行此動作 hello 方案在 Visual Studio 中按兩下開啟 hello`DotNetTutorial.sln`方案檔。</span><span class="sxs-lookup"><span data-stu-id="5f357-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="5f357-169">或從 Visual Studio 內使用開啟 hello**檔案 > 開啟 > 專案/方案**功能表。</span><span class="sxs-lookup"><span data-stu-id="5f357-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="5f357-170">開啟`Program.cs`內 hello *DotNetTutorial*專案。</span><span class="sxs-lookup"><span data-stu-id="5f357-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="5f357-171">指定 hello hello 檔案的頂端附近，然後加入您的認證：</span><span class="sxs-lookup"><span data-stu-id="5f357-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="5f357-172">如上面所述，您目前必須指定 hello 認證**一般用途**Azure 儲存體中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f357-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="5f357-173">批次應用程式使用 blob 儲存體中 hello**一般用途**儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f357-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="5f357-174">未指定儲存體帳戶所建立的選取 hello hello 認證*Blob 儲存體*帳戶類型。</span><span class="sxs-lookup"><span data-stu-id="5f357-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="5f357-175">您可以找到您的批次和儲存體帳戶認證中的每個服務的 hello 帳戶 刀鋒視窗中 hello [Azure 入口網站][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="5f357-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="5f357-176">![批次 hello 入口網站中的認證][9]
![hello 入口網站中的儲存體認證][10]</span><span class="sxs-lookup"><span data-stu-id="5f357-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="5f357-177">既然您已使用您的認證更新 hello 專案，以滑鼠右鍵按一下方案總管 中的 hello 方案，然後按一下**建置方案**。</span><span class="sxs-lookup"><span data-stu-id="5f357-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="5f357-178">如果系統提示您，確認 hello 任何的 NuGet 封裝還原。</span><span class="sxs-lookup"><span data-stu-id="5f357-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="5f357-179">如果 hello NuGet 封裝不會自動還原，或如果您看到失敗 toorestore hello 封裝相關的錯誤，請確定您擁有 hello [NuGet 套件管理員][ nuget_packagemgr]安裝。</span><span class="sxs-lookup"><span data-stu-id="5f357-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="5f357-180">再啟用 hello 下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="5f357-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="5f357-181">請參閱[啟用封裝還原建置期間][ nuget_restore] tooenable 套件下載。</span><span class="sxs-lookup"><span data-stu-id="5f357-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="5f357-182">在下列各節的 hello，我們可分為 hello 範例應用程式，它會執行 tooprocess hello 步驟 hello 批次服務中的工作負載，並討論這些步驟，在詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5f357-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="5f357-183">我們鼓勵您 toorefer toohello 開啟的方案在 Visual Studio 工作透過 hello 本文其餘部分，因為討論 hello 範例中的程式碼不是每個列時。</span><span class="sxs-lookup"><span data-stu-id="5f357-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="5f357-184">瀏覽 toohello 頂端 hello`MainAsync`方法在 hello *DotNetTutorial*專案的`Program.cs`檔案 toostart 與步驟 1。</span><span class="sxs-lookup"><span data-stu-id="5f357-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="5f357-185">然後大致如下所示 hello 進展方法的呼叫中的每個步驟下方`MainAsync`。</span><span class="sxs-lookup"><span data-stu-id="5f357-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="5f357-186">步驟 1：建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="5f357-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="5f357-187">![在 Azure 儲存體中建立容器][1]
</span><span class="sxs-lookup"><span data-stu-id="5f357-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="5f357-188">Batch 包含與 Azure 儲存體進行互動的內建支援。</span><span class="sxs-lookup"><span data-stu-id="5f357-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="5f357-189">在儲存體帳戶的容器會提供在您的 Batch 帳戶中執行的 hello 工作所需的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f357-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="5f357-190">hello 容器也會提供 hello 工作產生的地方 toostore hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="5f357-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="5f357-191">首先 hello hello *DotNetTutorial*用戶端應用程式會建立三個容器在[Azure Blob 儲存體](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="5f357-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="5f357-192">**應用程式**： 此容器會儲存 hello hello 工作，以及任何相依性，例如 Dll 所執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f357-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="5f357-193">**輸入**： 工作會從 hello 下載 hello 資料檔案 tooprocess*輸入*容器。</span><span class="sxs-lookup"><span data-stu-id="5f357-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="5f357-194">**輸出**： 當工作完成時輸入的檔案處理時，他們會將上傳 hello 結果 toohello*輸出*容器。</span><span class="sxs-lookup"><span data-stu-id="5f357-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="5f357-195">在順序 toointeract 與儲存體帳戶，並建立容器，我們使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫][net_api_storage]。</span><span class="sxs-lookup"><span data-stu-id="5f357-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="5f357-196">我們建立了具有參考 toohello 帳戶[CloudStorageAccount][net_cloudstorageaccount]，並從該建立[CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="5f357-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="5f357-197">我們使用 hello`blobClient`參考整個 hello 應用程式並將它傳遞為參數 tooseveral 方法。</span><span class="sxs-lookup"><span data-stu-id="5f357-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="5f357-198">舉例來說，這是在 hello 緊接 hello 以上版本，在呼叫的程式碼區塊`CreateContainerIfNotExistAsync`tooactually 建立 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="5f357-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="5f357-199">一旦已建立 hello 容器，hello 應用程式現在可以將 hello 工作所使用的 hello 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="5f357-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="5f357-200">[如何從.NET 的 Blob 儲存體 toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md)提供使用 Azure 儲存體容器和 blob 的良好概觀。</span><span class="sxs-lookup"><span data-stu-id="5f357-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="5f357-201">當您使用批次開始使用，它應該是 hello 讀取清單頂端附近。</span><span class="sxs-lookup"><span data-stu-id="5f357-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="5f357-202">步驟 2：上傳工作應用程式和資料檔案</span><span class="sxs-lookup"><span data-stu-id="5f357-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="5f357-203">![上傳工作應用程式，並輸入 （資料） 檔 toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="5f357-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="5f357-204">Hello 檔案中上傳作業， *DotNetTutorial*的集合會先定義**應用程式**和**輸入**存在於 hello 本機電腦上檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="5f357-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="5f357-205">然後它上傳您在 hello 上一個步驟中建立這些檔案 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="5f357-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="5f357-206">有兩種方法在`Program.cs`hello 上傳程序涉及：</span><span class="sxs-lookup"><span data-stu-id="5f357-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="5f357-207">`UploadFilesToContainerAsync`： 這個方法傳回的集合[ResourceFile] [ net_resourcefile] （討論如下） 的物件，並在內部呼叫`UploadFileToContainerAsync`tooupload 每個檔案，傳入 hello *filePaths*參數。</span><span class="sxs-lookup"><span data-stu-id="5f357-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="5f357-208">`UploadFileToContainerAsync`： 這是實際執行 hello 檔案上傳，並建立 hello hello 方法[ResourceFile] [ net_resourcefile]物件。</span><span class="sxs-lookup"><span data-stu-id="5f357-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="5f357-209">上傳之後 hello 檔案，它會取得 hello 檔案的共用的存取簽章 (SAS)，並傳回 ResourceFile 物件，表示它。</span><span class="sxs-lookup"><span data-stu-id="5f357-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="5f357-210">下面也會討論共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="5f357-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="5f357-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="5f357-211">ResourceFiles</span></span>
<span data-ttu-id="5f357-212">A [ResourceFile] [ net_resourcefile]提供批次中的工作會下載的 tooa 的 Azure 儲存體中的 hello URL tooa 檔案與計算節點，才能執行該工作。</span><span class="sxs-lookup"><span data-stu-id="5f357-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="5f357-213">hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource]存在於 Azure 儲存體中，屬性會指定 hello 的 hello 檔案的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="5f357-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="5f357-214">hello URL 也可能包括提供安全的 access toohello 檔案的共用的存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="5f357-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="5f357-215">Batch .NET 中的大部分工作類型都包含 ResourceFiles  屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="5f357-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="5f357-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="5f357-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="5f357-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="5f357-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="5f357-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="5f357-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="5f357-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="5f357-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="5f357-220">hello DotNetTutorial 範例應用程式不會使用 hello JobPreparationTask 或 JobReleaseTask 工作類型，但您可以深入資訊，請在[執行作業準備與完成工作上 Azure Batch 計算節點](batch-job-prep-release.md)。</span><span class="sxs-lookup"><span data-stu-id="5f357-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="5f357-221">共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="5f357-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="5f357-222">共用的存取簽章字串的 — 包含為 URL 的一部分時，提供安全地存取 toocontainers 和 Azure 儲存體中的 blob。</span><span class="sxs-lookup"><span data-stu-id="5f357-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="5f357-223">hello DotNetTutorial 應用程式會使用這兩個 blob 和容器共用存取簽章 Url，並示範如何 tooobtain 這些共用存取簽章字串 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="5f357-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="5f357-224">**Blob 共用的存取簽章**: hello 集區 StartTask DotNetTutorial 中的從儲存體下載 hello 應用程式二進位檔和輸入的資料檔時，請使用 blob 共用存取簽章 （請參閱下面步驟 #3）。</span><span class="sxs-lookup"><span data-stu-id="5f357-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="5f357-225">hello`UploadFileToContainerAsync`方法中 DotNetTutorial 的`Program.cs`包含 hello 程式碼會取得每個 blob 的共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="5f357-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="5f357-226">呼叫 [CloudBlob.GetSharedAccessSignature][net_sas_blob] 即可完成。</span><span class="sxs-lookup"><span data-stu-id="5f357-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="5f357-227">**容器共用存取簽章**： 為每項工作完成其工作 hello 計算節點上的上, 傳其輸出檔 toohello*輸出*Azure 儲存體容器中的。</span><span class="sxs-lookup"><span data-stu-id="5f357-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="5f357-228">toodo TaskApplication 因此，使用容器的共用的存取簽章時，會提供寫入存取 toohello 容器 hello 路徑 hello 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="5f357-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="5f357-229">取得 hello 容器共用的存取簽章是以類似的方式做為當取得 hello blob 共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="5f357-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="5f357-230">在 DotNetTutorial，您會發現該 hello `GetContainerSasUrl` helper 方法會呼叫[CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo 如此。</span><span class="sxs-lookup"><span data-stu-id="5f357-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="5f357-231">您會先深入 TaskApplication 如何使用 hello 容器共用存取簽章中的 「 步驟 6： 監視工作。 」</span><span class="sxs-lookup"><span data-stu-id="5f357-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="5f357-232">簽出 hello 兩段式序列上的共用的存取簽章，[第 1 部分： 了解 hello 共用存取簽章 (SAS) 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)和[第 2 部分： 建立和使用共用的存取簽章 (SAS) 使用 Blob 儲存體](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)，深入了解提供儲存體帳戶中的安全存取 toodata toolearn。</span><span class="sxs-lookup"><span data-stu-id="5f357-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="5f357-233">步驟 3：建立 Batch 集區</span><span class="sxs-lookup"><span data-stu-id="5f357-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="5f357-234">![建立 Batch 集區][3]
</span><span class="sxs-lookup"><span data-stu-id="5f357-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="5f357-235">Batch **集區** 是 Batch 執行作業工作所在的計算節點 (虛擬機器) 集合。</span><span class="sxs-lookup"><span data-stu-id="5f357-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="5f357-236">上傳 hello 應用程式及資料檔案 toohello 與 Azure 儲存體 Api，儲存體帳戶之後*DotNetTutorial*開始進行呼叫 toohello 批次服務的 hello 批次.NET 程式庫所提供的 Api。</span><span class="sxs-lookup"><span data-stu-id="5f357-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="5f357-237">hello 程式碼會先建立[BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="5f357-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="5f357-238">接下來，hello 範例建立集區的運算節點 hello 批次帳戶的呼叫中太`CreatePoolIfNotExistsAsync`。</span><span class="sxs-lookup"><span data-stu-id="5f357-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="5f357-239">`CreatePoolIfNotExistsAsync`使用 hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create]方法 toocreate hello 批次服務中的新集區：</span><span class="sxs-lookup"><span data-stu-id="5f357-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="5f357-240">當您建立的集區[CreatePool][net_pool_create]，您指定數個參數 hello 的運算節點數目，例如 hello [hello 節點大小](../cloud-services/cloud-services-sizes-specs.md)，和 hello 節點的作業系統系統。</span><span class="sxs-lookup"><span data-stu-id="5f357-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="5f357-241">在*DotNetTutorial*，我們使用[CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 從[雲端服務](../cloud-services/cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="5f357-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="5f357-242">您也可以建立 Azure 虛擬機器 (Vm) 的計算節點的集區，藉由指定 hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration]集區。</span><span class="sxs-lookup"><span data-stu-id="5f357-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="5f357-243">您可以從 Windows 或 [Linux 映像](batch-linux-nodes.md)建立 VM 計算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="5f357-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="5f357-244">您的 VM 映像的 hello 來源可以是：</span><span class="sxs-lookup"><span data-stu-id="5f357-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="5f357-245">hello [Azure 虛擬機器 Marketplace][vm_marketplace]，這樣會提供已備妥要使用的 Windows 和 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="5f357-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="5f357-246">您準備和提供的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="5f357-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="5f357-247">如需自訂映像的詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#pool)。</span><span class="sxs-lookup"><span data-stu-id="5f357-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f357-248">您需對 Batch 中的計算資源付費。</span><span class="sxs-lookup"><span data-stu-id="5f357-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="5f357-249">您可以降低 toominimize 成本`targetDedicatedComputeNodes`too1 之前執行 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="5f357-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="5f357-250">這些實體節點的屬性，以及您也可以指定[StartTask] [ net_pool_starttask] hello 集區。</span><span class="sxs-lookup"><span data-stu-id="5f357-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="5f357-251">hello StartTask 執行每個節點上，該節點加入 hello 集區，以及每次重新啟動節點。</span><span class="sxs-lookup"><span data-stu-id="5f357-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="5f357-252">hello StartTask 為計算節點 toohello 先前執行的工作上安裝應用程式特別有用。</span><span class="sxs-lookup"><span data-stu-id="5f357-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="5f357-253">例如，如果您的工作會使用 Python 指令碼來處理資料，您可以使用 StartTask tooinstall Python hello 計算節點上。</span><span class="sxs-lookup"><span data-stu-id="5f357-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="5f357-254">在此範例應用程式，hello StartTask 會複製它會從儲存體下載的 hello 檔案 (其指定使用 hello [StartTask][net_starttask]。[ResourceFiles] [ net_starttask_resourcefiles]屬性) 從 hello StartTask 工作目錄 toohello 共用目錄的*所有*hello 節點上執行的工作可以存取。</span><span class="sxs-lookup"><span data-stu-id="5f357-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="5f357-255">基本上，這會將複製`TaskApplication.exe`和其相依性 toohello 共用目錄，每個節點上的為 hello 節點加入 hello 集區，以便在 hello 節點執行任何工作可以存取它。</span><span class="sxs-lookup"><span data-stu-id="5f357-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="5f357-256">hello**應用程式封裝**Azure Batch 功能提供其他方式 tooget 到集區中的 hello 計算節點上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f357-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="5f357-257">請參閱[部署與批次應用程式套件的應用程式 toocompute 節點](batch-application-packages.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5f357-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="5f357-258">也在 hello 上述程式碼片段的值得注意的是兩個環境中的變數 hello hello 使用*CommandLine* hello StartTask 屬性：`%AZ_BATCH_TASK_WORKING_DIR%`和`%AZ_BATCH_NODE_SHARED_DIR%`。</span><span class="sxs-lookup"><span data-stu-id="5f357-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="5f357-259">批次集區中每個運算節點會自動設定成有特定 tooBatch 的數個環境變數中。</span><span class="sxs-lookup"><span data-stu-id="5f357-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="5f357-260">任何處理程序所執行的工作有存取 toothese 環境變數。</span><span class="sxs-lookup"><span data-stu-id="5f357-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="5f357-261">toofind 深入了解 hello 環境變數所提供的計算節點的批次集區和工作的工作目錄的詳細資訊，請參閱 「 hello[工作的環境設定](batch-api-basics.md#environment-settings-for-tasks)和[檔案和目錄](batch-api-basics.md#files-and-directories)章節 hello[批次功能概觀，讓開發人員](batch-api-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="5f357-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="5f357-262">步驟 4：建立 Batch 作業</span><span class="sxs-lookup"><span data-stu-id="5f357-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="5f357-263">![建立 Batch 作業][4]</span><span class="sxs-lookup"><span data-stu-id="5f357-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="5f357-264">Batch **作業** 是與計算節點集區相關聯的工作集合。</span><span class="sxs-lookup"><span data-stu-id="5f357-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="5f357-265">作業中的 hello 工作執行相關聯的 hello 集區的計算節點上。</span><span class="sxs-lookup"><span data-stu-id="5f357-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="5f357-266">您可以使用工作，不只對組織及追蹤相關的工作負載中的工作，也在 hello 批次中的關聯性 tooother 作業中的工作優先順序以及諸特定條件約束-例如 hello 最大 runtime hello 作業 （和延伸模組，其工作）帳戶。</span><span class="sxs-lookup"><span data-stu-id="5f357-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="5f357-267">在此範例中，不過，hello 作業是只能搭配步驟 #3 中建立的 hello 集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="5f357-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="5f357-268">不會設定任何其他屬性。</span><span class="sxs-lookup"><span data-stu-id="5f357-268">No additional properties are configured.</span></span>

<span data-ttu-id="5f357-269">所有 Batch 作業都會與特定集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="5f357-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="5f357-270">這項關聯指示 hello 作業 」 工作，也會執行哪些節點。</span><span class="sxs-lookup"><span data-stu-id="5f357-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="5f357-271">指定此使用 hello [CloudJob.PoolInformation] [ net_job_poolinfo]屬性 hello 下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="5f357-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="5f357-272">已建立工作，工作會新增 tooperform hello 工作。</span><span class="sxs-lookup"><span data-stu-id="5f357-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="5f357-273">步驟 5： 加入工作 toojob</span><span class="sxs-lookup"><span data-stu-id="5f357-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="5f357-274">![新增工作 toojob][5]</span><span class="sxs-lookup"><span data-stu-id="5f357-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="5f357-275">
*（1） 工作已加入 toohello 作業、 （2) hello 工作是排定的 toorun 節點上，以及 （3) hello 工作下載 hello 資料檔案 tooprocess*</span><span class="sxs-lookup"><span data-stu-id="5f357-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="5f357-276">批次**工作**是 hello 個別的工作單位 hello 上所執行的計算節點。</span><span class="sxs-lookup"><span data-stu-id="5f357-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="5f357-277">工作已命令列，並執行 hello 指令碼或您在該命令列中指定的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="5f357-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="5f357-278">tooactually 執行工作、 工作必須加入 tooa 作業。</span><span class="sxs-lookup"><span data-stu-id="5f357-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="5f357-279">每個[CloudTask] [ net_task]使用命令列屬性來設定和[ResourceFiles] [ net_task_resourcefiles] （如同 hello 集區 StartTask），hello 工作會在其命令列會自動在執行之前下載 toohello 節點。</span><span class="sxs-lookup"><span data-stu-id="5f357-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="5f357-280">在 hello *DotNetTutorial*範例專案，每項工作會處理一個檔案。</span><span class="sxs-lookup"><span data-stu-id="5f357-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="5f357-281">因此其 ResourceFiles 集合只包含單一元素。</span><span class="sxs-lookup"><span data-stu-id="5f357-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="5f357-282">當他們存取環境變數例如`%AZ_BATCH_NODE_SHARED_DIR%`或執行應用程式中的 hello 節點找不到`PATH`，工作的命令列必須在前面加上`cmd /c`。</span><span class="sxs-lookup"><span data-stu-id="5f357-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="5f357-283">明確地將執行 hello 命令直譯器，並指示它 tooterminate 之後執行您的命令。</span><span class="sxs-lookup"><span data-stu-id="5f357-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="5f357-284">這項需求是不必要，如果您的工作執行應用程式中的 hello 節點`PATH`(例如*robocopy.exe*或*powershell.exe*)，而且不可用任何環境變數。</span><span class="sxs-lookup"><span data-stu-id="5f357-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="5f357-285">在 hello `foreach` hello 上述程式碼片段中的迴圈，您可以看到建構 hello hello 工作的命令列時，三個命令列引數會傳遞太*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="5f357-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="5f357-286">hello**第一個引數**是 hello 檔案 tooprocess hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="5f357-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="5f357-287">這是 hello 本機路徑 toohello 檔案存在於 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="5f357-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="5f357-288">當 hello 中的 ResourceFile 物件`UploadFileToContainerAsync`初次建立上述中 hello 檔案名稱已用於此屬性 （做為參數 toohello ResourceFile 建構函式）。</span><span class="sxs-lookup"><span data-stu-id="5f357-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="5f357-289">這表示該 hello 檔案位於 hello 相同目錄做為*TaskApplication.exe*。</span><span class="sxs-lookup"><span data-stu-id="5f357-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="5f357-290">hello**第二個引數**指定該 hello 頂端*N*字詞應該寫 toohello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="5f357-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="5f357-291">在 hello 範例中，這是硬式編碼，讓 hello 前三個單字都會寫入 toohello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="5f357-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="5f357-292">hello**第三個引數**hello 共用的存取簽章 (SAS) 提供寫入存取 toohello**輸出**Azure 儲存體容器中的。</span><span class="sxs-lookup"><span data-stu-id="5f357-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="5f357-293">*TaskApplication.exe*當它上傳 hello 輸出檔案 tooAzure 儲存體時，會使用此共用存取簽章 URL。</span><span class="sxs-lookup"><span data-stu-id="5f357-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="5f357-294">您可以在 hello 這個尋找 hello 程式碼`UploadFileToContainer`方法在 hello TaskApplication 專案的`Program.cs`檔案：</span><span class="sxs-lookup"><span data-stu-id="5f357-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="5f357-295">步驟 6：監視工作</span><span class="sxs-lookup"><span data-stu-id="5f357-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="5f357-296">![監視工作][6]</span><span class="sxs-lookup"><span data-stu-id="5f357-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="5f357-297">
*hello 用戶端應用程式 （1） 監視 hello 完成及成功狀態的工作和 （2) hello 工作上傳結果資料 tooAzure 儲存體*</span><span class="sxs-lookup"><span data-stu-id="5f357-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="5f357-298">當工作區加入 tooa 工作時，他們會自動排入佇列，排定在 hello 與 hello 工作相關聯的集區的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="5f357-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="5f357-299">根據您指定的 hello 設定，批次工作的所有佇列、 排程、 重試和其他工作的系統管理工作會為您處理。</span><span class="sxs-lookup"><span data-stu-id="5f357-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="5f357-300">有多種方法 toomonitoring 工作執行。</span><span class="sxs-lookup"><span data-stu-id="5f357-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="5f357-301">DotNetTutorial 顯示了一個只報告完成和工作失敗或成功狀態的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="5f357-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="5f357-302">在 hello`MonitorTasks`中 DotNetTutorial 的方法`Program.cs`，有三個批次.NET 概念保證討論。</span><span class="sxs-lookup"><span data-stu-id="5f357-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="5f357-303">底下依其出現的順序列出：</span><span class="sxs-lookup"><span data-stu-id="5f357-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="5f357-304">**ODATADetailLevel**：一定要在清單作業 (例如取得作業的工作清單) 中指定 [ODATADetailLevel][net_odatadetaillevel]，以確保 Batch 應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="5f357-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="5f357-305">新增[有效率地查詢 hello Azure Batch 服務](batch-efficient-list-queries.md)tooyour 讀取清單，如果您計劃執行任何類型的批次應用程式中監視狀態。</span><span class="sxs-lookup"><span data-stu-id="5f357-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="5f357-306">**TaskStateMonitor**：[TaskStateMonitor][net_taskstatemonitor] 提供給 Batch .NET 應用程可用來監視工作狀態的協助公用程式。</span><span class="sxs-lookup"><span data-stu-id="5f357-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="5f357-307">在`MonitorTasks`， *DotNetTutorial*等候所有工作 tooreach [TaskState.Completed] [ net_taskstate]時間限制內。</span><span class="sxs-lookup"><span data-stu-id="5f357-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="5f357-308">然後它會終止 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="5f357-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="5f357-309">**TerminateJobAsync**： 終止與作業[JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] （或 hello 封鎖 JobOperations.TerminateJob） 將工作標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="5f357-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="5f357-310">它是不可或缺的 toodo 因此如果您的批次方案使用[JobReleaseTask][net_jobreltask]。</span><span class="sxs-lookup"><span data-stu-id="5f357-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="5f357-311">如 [作業準備和完成工作](batch-job-prep-release.md)中所述，這是一種特殊的工作類型。</span><span class="sxs-lookup"><span data-stu-id="5f357-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="5f357-312">hello`MonitorTasks`方法從*DotNetTutorial*的`Program.cs`下方會出現：</span><span class="sxs-lookup"><span data-stu-id="5f357-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="5f357-313">步驟 7：下載工作輸出</span><span class="sxs-lookup"><span data-stu-id="5f357-313">Step 7: Download task output</span></span>
<span data-ttu-id="5f357-314">![從儲存體下載工作輸出][7]</span><span class="sxs-lookup"><span data-stu-id="5f357-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="5f357-315">既然 hello 作業已完成，您可以從 Azure 儲存體下載 hello hello 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="5f357-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="5f357-316">這是透過呼叫太`DownloadBlobsFromContainerAsync`中*DotNetTutorial*的`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="5f357-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="5f357-317">太 hello 呼叫`DownloadBlobsFromContainerAsync`在 hello *DotNetTutorial*應用程式指定 hello 檔案應該下載的 tooyour`%TEMP%`資料夾。</span><span class="sxs-lookup"><span data-stu-id="5f357-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="5f357-318">感覺可用 toomodify 這輸出位置。</span><span class="sxs-lookup"><span data-stu-id="5f357-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="5f357-319">步驟 8：刪除容器</span><span class="sxs-lookup"><span data-stu-id="5f357-319">Step 8: Delete containers</span></span>
<span data-ttu-id="5f357-320">因為您必須支付位於 Azure 儲存體中的資料，永遠是個不錯的主意 tooremove blob 不再需要的批次作業。</span><span class="sxs-lookup"><span data-stu-id="5f357-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="5f357-321">在 DotNetTutorial 的`Program.cs`，做法是使用三個呼叫 toohello helper 方法`DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="5f357-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="5f357-322">hello 方法本身只會取得參考 toohello 容器，然後再呼叫[CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="5f357-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="5f357-323">步驟 9： 刪除 hello 作業和 hello 集區</span><span class="sxs-lookup"><span data-stu-id="5f357-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="5f357-324">在 hello 最後一個步驟中，您提示的 toodelete hello 作業和 hello 集區所建立的 hello DotNetTutorial 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f357-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="5f357-325">雖然您不需支付作業和工作的費用，但您「需」支付計算節點的費用。</span><span class="sxs-lookup"><span data-stu-id="5f357-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="5f357-326">因此，我們建議您只在必要時配置節點。</span><span class="sxs-lookup"><span data-stu-id="5f357-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="5f357-327">刪除未使用的集區可成為您維護程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="5f357-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="5f357-328">hello BatchClient 的[JobOperations] [ net_joboperations]和[PoolOperations] [ net_pooloperations]兩者都有對應的刪除動作方法，如果呼叫hello 使用者確認刪除項目：</span><span class="sxs-lookup"><span data-stu-id="5f357-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="5f357-329">請記住，您需支付計算資源的費用，而刪除未使用的集區會將成本降到最低。</span><span class="sxs-lookup"><span data-stu-id="5f357-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="5f357-330">此外，請注意，刪除集區會刪除所有的運算節點區內，而且之後刪除 hello 集區 hello 節點上的任何資料將無法復原。</span><span class="sxs-lookup"><span data-stu-id="5f357-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="5f357-331">執行 hello *DotNetTutorial*範例</span><span class="sxs-lookup"><span data-stu-id="5f357-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="5f357-332">當您執行 hello 範例應用程式時，hello 主控台輸出會是類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="5f357-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="5f357-333">在執行期間，就會發生在暫停`Awaiting task completion, timeout in 00:30:00...`時 hello 集區的計算節點都已啟動。</span><span class="sxs-lookup"><span data-stu-id="5f357-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="5f357-334">使用 hello [Azure 入口網站][ azure_portal] toomonitor 集區、 計算節點、 工作和工作期間和之後執行。</span><span class="sxs-lookup"><span data-stu-id="5f357-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="5f357-335">使用 hello [Azure 入口網站][ azure_portal]或 hello [Azure 儲存體總管][ storage_explorers] tooview hello 存放資源 （容器和 blob） 的hello 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="5f357-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="5f357-336">一般的執行時間是**大約 5 分鐘**當您執行 hello 應用程式在其預設組態。</span><span class="sxs-lookup"><span data-stu-id="5f357-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="5f357-337">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f357-337">Next steps</span></span>
<span data-ttu-id="5f357-338">太覺得可用 toomake 變更*DotNetTutorial*和*TaskApplication*不同 tooexperiment 計算案例。</span><span class="sxs-lookup"><span data-stu-id="5f357-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="5f357-339">例如，再次嘗試新增執行延遲太*TaskApplication*，例如如同[Thread.Sleep][net_thread_sleep]，toosimulate 長時間執行工作，並在 hello 入口網站中監視它們。</span><span class="sxs-lookup"><span data-stu-id="5f357-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="5f357-340">再試一次新增更多工作，或調整 hello 的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="5f357-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="5f357-341">新增的邏輯 toocheck 並允許 hello 使用現有的集區 toospeed 執行時間 (*提示*： 簽出`ArticleHelpers.cs`在 hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common]專案中[azure 批次範例][github_samples])。</span><span class="sxs-lookup"><span data-stu-id="5f357-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="5f357-342">既然您已熟悉 hello 批次解決方案的基本工作流程，它是 hello 的時間 toodig 中 toohello 批次服務的額外功能。</span><span class="sxs-lookup"><span data-stu-id="5f357-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="5f357-343">檢閱 hello [Azure Batch 概觀功能](batch-api-basics.md)發行項，我們建議您是否新增 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="5f357-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="5f357-344">開始在 hello 底下其他批次開發文件**深入開發**在 hello[批次學習路徑][batch_learning_path]。</span><span class="sxs-lookup"><span data-stu-id="5f357-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="5f357-345">簽出使用批次中 hello 處理 hello 「 前 n 個單字"工作負載的不同實作[TopNWords] [ github_topnwords]範例。</span><span class="sxs-lookup"><span data-stu-id="5f357-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="5f357-346">檢閱 hello 批次.NET[版本資訊](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes)hello hello 文件庫中的最新變更。</span><span class="sxs-lookup"><span data-stu-id="5f357-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "在 Azure 儲存體中建立容器"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "上傳工作應用程式，並輸入 （資料） 檔 toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "建立 Batch 集區"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "建立 Batch 作業"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "新增工作 toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "監視工作"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "從儲存體下載工作輸出"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch 方案工作流程 (完整圖表)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "入口網站中的 Batch 認證"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "入口網站中的儲存體認證"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch 方案工作流程 (最小圖表)"
