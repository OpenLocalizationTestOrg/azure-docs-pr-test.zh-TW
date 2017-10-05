---
title: "教學課程 - 使用適用於 .NET 的 Azure Batch 用戶端程式庫 | Microsoft Docs"
description: "了解 Azure Batch 的基本概念和使用 .NET 建置簡單的解決方案。"
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
ms.openlocfilehash: cf8fdca51a6a4ad1b7cd4fe6980543199f6b36e0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-building-solutions-with-the-batch-client-library-for-net"></a><span data-ttu-id="c40dc-103">開始使用適用於.NET 的 Batch 用戶端程式庫來建置解決方案</span><span class="sxs-lookup"><span data-stu-id="c40dc-103">Get started building solutions with the Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c40dc-104">.NET</span><span class="sxs-lookup"><span data-stu-id="c40dc-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="c40dc-105">Python</span><span class="sxs-lookup"><span data-stu-id="c40dc-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="c40dc-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="c40dc-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="c40dc-107">在我們逐步討論 C# 範例應用程式時，了解本文中 [Azure Batch][azure_batch] 和 [Batch .NET][net_api] 程式庫的基本概念。</span><span class="sxs-lookup"><span data-stu-id="c40dc-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="c40dc-108">我們將看看此範例應用程式如何利用 Batch 服務來處理雲端的平行工作負載，和如何與 [Azure 儲存體](../storage/common/storage-introduction.md)互動來預備和擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-108">We look at how the sample application leverages the Batch service to process a parallel workload in the cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="c40dc-109">您將了解常見的 Batch 應用程式工作流程，並取得 Batch 的主要元件，例如作業、工作、集區和計算節點。</span><span class="sxs-lookup"><span data-stu-id="c40dc-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="c40dc-110">![Batch 方案工作流程 (基本)][11]</span><span class="sxs-lookup"><span data-stu-id="c40dc-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="c40dc-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="c40dc-111">Prerequisites</span></span>
<span data-ttu-id="c40dc-112">本文假設您已具備 C# 和 Visual Studio 的使用知識。</span><span class="sxs-lookup"><span data-stu-id="c40dc-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="c40dc-113">而且假設您可以滿足針對 Azure Batch 和儲存體服務所指定的帳戶建立需求。</span><span class="sxs-lookup"><span data-stu-id="c40dc-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="c40dc-114">帳戶</span><span class="sxs-lookup"><span data-stu-id="c40dc-114">Accounts</span></span>
* <span data-ttu-id="c40dc-115">**Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶][azure_free_account]。</span><span class="sxs-lookup"><span data-stu-id="c40dc-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="c40dc-116">**Batch 帳戶**：擁有 Azure 訂用帳戶後，請 [建立 Azure Batch 帳戶](batch-account-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="c40dc-117">**儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c40dc-118">Batch 目前「僅」支援**一般用途**的儲存體帳戶類型，如[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的步驟 #5 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)所述。</span><span class="sxs-lookup"><span data-stu-id="c40dc-118">Batch currently supports *only* the **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="c40dc-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c40dc-119">Visual Studio</span></span>
<span data-ttu-id="c40dc-120">您必須擁有 **Visual Studio 2015 或更新版本**才能建置範例專案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-120">You must have **Visual Studio 2015 or newer** to build the sample project.</span></span> <span data-ttu-id="c40dc-121">您可以在 [Visual Studio 產品概觀][visual_studio]中找到免費試用版的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c40dc-121">You can find free and trial versions of Visual Studio in the [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="c40dc-122"> 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="c40dc-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="c40dc-123">[DotNetTutorial][github_dotnettutorial] 範例是在 GitHub 上 [azure-batch-samples][github_samples] 儲存機制中找到的許多程式碼範例之一。</span><span class="sxs-lookup"><span data-stu-id="c40dc-123">The [DotNetTutorial][github_dotnettutorial] sample is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="c40dc-124">按一下儲存機制首頁上的 [複製或下載] > [下載 ZIP]，或按一下 [azure-batch-samples-master.zip][github_samples_zip] 直接下載連結，即可下載所有範例。</span><span class="sxs-lookup"><span data-stu-id="c40dc-124">You can download all the samples by clicking  **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="c40dc-125">將 ZIP 檔案的內容解壓縮後，您可以在下列資料夾中找到方案：</span><span class="sxs-lookup"><span data-stu-id="c40dc-125">Once you've extracted the contents of the ZIP file, you can find the solution in the following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="c40dc-126">Azure Batch 總管 (選用)</span><span class="sxs-lookup"><span data-stu-id="c40dc-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="c40dc-127">[Azure Batch Explorer][github_batchexplorer] 是 GitHub 上 [azure-batch-samples][github_samples] 儲存機制隨附的免費公用程式。</span><span class="sxs-lookup"><span data-stu-id="c40dc-127">The [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="c40dc-128">雖然不一定要完成此教學課程，但是在您開發和偵錯 Batch 解決方案時卻很實用。</span><span class="sxs-lookup"><span data-stu-id="c40dc-128">While not required to complete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="c40dc-129">DotNetTutorial 範例專案概觀</span><span class="sxs-lookup"><span data-stu-id="c40dc-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="c40dc-130">DotNetTutorial 程式碼範例是由兩個專案所組成的 Visual Studio 方案：**DotNetTutorial** 和 **TaskApplication**。</span><span class="sxs-lookup"><span data-stu-id="c40dc-130">The *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="c40dc-131">**DotNetTutorial** 是與 Batch 和儲存體服務進行互動，以在計算節點 (虛擬機器) 上執行平行工作負載的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="c40dc-131">**DotNetTutorial** is the client application that interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="c40dc-132">DotNetTutorial 會在本機工作站上執行。</span><span class="sxs-lookup"><span data-stu-id="c40dc-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="c40dc-133">**TaskApplication** 是在 Azure 中的計算節點上執行進而執行實際工作的程式。</span><span class="sxs-lookup"><span data-stu-id="c40dc-133">**TaskApplication** is the program that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="c40dc-134">在範例中， `TaskApplication.exe` 會剖析從 Azure 儲存體下載的檔案 (輸入檔) 中的文字。</span><span class="sxs-lookup"><span data-stu-id="c40dc-134">In the sample, `TaskApplication.exe` parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="c40dc-135">然後產生文字檔 (輸出檔)，其中包含出現在輸入檔中的前三個單字清單。</span><span class="sxs-lookup"><span data-stu-id="c40dc-135">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="c40dc-136">在它建立輸出檔之後，TaskApplication 會將檔案上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c40dc-136">After it creates the output file, TaskApplication uploads the file to Azure Storage.</span></span> <span data-ttu-id="c40dc-137">如此檔案即可供用戶端應用程式下載。</span><span class="sxs-lookup"><span data-stu-id="c40dc-137">This makes it available to the client application for download.</span></span> <span data-ttu-id="c40dc-138">TaskApplication 會在 Batch 服務中的多個計算節點上平行執行。</span><span class="sxs-lookup"><span data-stu-id="c40dc-138">TaskApplication runs in parallel on multiple compute nodes in the Batch service.</span></span>

<span data-ttu-id="c40dc-139">下圖說明用戶端應用程式 (DotNetTutorial) 所執行的主要作業，以及工作所執行的應用程式 (TaskApplication)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-139">The following diagram illustrates the primary operations that are performed by the client application, *DotNetTutorial*, and the application that is executed by the tasks, *TaskApplication*.</span></span> <span data-ttu-id="c40dc-140">此基本工作流程通常由使用 Batch 建立的許多計算方案所組成。</span><span class="sxs-lookup"><span data-stu-id="c40dc-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="c40dc-141">雖然不會示範 Batch 服務中可用的每項功能，但幾乎每個 Batch 案例都包含此工作流程的某些部分。</span><span class="sxs-lookup"><span data-stu-id="c40dc-141">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="c40dc-142">![Batch 範例工作流程][8]</span><span class="sxs-lookup"><span data-stu-id="c40dc-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="c40dc-143">**步驟 1.**</span><span class="sxs-lookup"><span data-stu-id="c40dc-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="c40dc-144">在 Azure Blob 儲存體中建立**容器**。</span><span class="sxs-lookup"><span data-stu-id="c40dc-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="c40dc-145">
[**步驟 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="c40dc-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="c40dc-146">將工作應用程式和輸入檔案上傳至容器。</span><span class="sxs-lookup"><span data-stu-id="c40dc-146">Upload task application files and input files to containers.</span></span><br/><span data-ttu-id="c40dc-147">
[**步驟 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="c40dc-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="c40dc-148">建立 Batch **集區**。</span><span class="sxs-lookup"><span data-stu-id="c40dc-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="c40dc-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="c40dc-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="c40dc-150">集區 **StartTask** 會在節點加入集區時將工作二進位檔 (TaskApplication) 下載至這些節點。</span><span class="sxs-lookup"><span data-stu-id="c40dc-150">The pool **StartTask** downloads the task binary files (TaskApplication) to nodes as they join the pool.</span></span><br/><span data-ttu-id="c40dc-151">
[**步驟 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="c40dc-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="c40dc-152">建立 Batch **作業**。</span><span class="sxs-lookup"><span data-stu-id="c40dc-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="c40dc-153">
[**步驟 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="c40dc-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="c40dc-154">將 **工作** 加入至作業。</span><span class="sxs-lookup"><span data-stu-id="c40dc-154">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="c40dc-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="c40dc-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="c40dc-156">工作會排程在節點上執行。</span><span class="sxs-lookup"><span data-stu-id="c40dc-156">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="c40dc-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="c40dc-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="c40dc-158">每項工作會從 Azure 儲存體下載其輸入資料，然後開始執行。</span><span class="sxs-lookup"><span data-stu-id="c40dc-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="c40dc-159">
[**步驟 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="c40dc-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="c40dc-160">監視工作。</span><span class="sxs-lookup"><span data-stu-id="c40dc-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="c40dc-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="c40dc-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="c40dc-162">當工作完成時，它們會將其輸出資料上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c40dc-162">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="c40dc-163">
[**步驟 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="c40dc-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="c40dc-164">從儲存體下載工作輸出。</span><span class="sxs-lookup"><span data-stu-id="c40dc-164">Download task output from Storage.</span></span>

<span data-ttu-id="c40dc-165">如上所述，並非每個 Batch 方案都會執行這些確切步驟，也有可能包含更多步驟，但 DotNetTutorial  範例應用程式會示範在 Batch 方案中找到的一般程序。</span><span class="sxs-lookup"><span data-stu-id="c40dc-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but the *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-the-dotnettutorial-sample-project"></a><span data-ttu-id="c40dc-166">建置 DotNetTutorial  範例專案</span><span class="sxs-lookup"><span data-stu-id="c40dc-166">Build the *DotNetTutorial* sample project</span></span>
<span data-ttu-id="c40dc-167">您必須先在 DotNetTutorial*`Program.cs` 專案的*  檔案中指定 Batch 和儲存體帳戶認證，才可以成功執行範例。</span><span class="sxs-lookup"><span data-stu-id="c40dc-167">Before you can successfully run the sample, you must specify both Batch and Storage account credentials in the *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="c40dc-168">如果您尚未這麼做，請在 `DotNetTutorial.sln` 方案檔案上連按兩下，以在 Visual Studio 中開啟方案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-168">If you have not done so already, open the solution in Visual Studio by double-clicking the `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="c40dc-169">或者使用 [檔案] > [開啟] > [專案/方案] 功能表，在 Visual Studio 中開啟方案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-169">Or open it from within Visual Studio by using the **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="c40dc-170">開啟 DotNetTutorial 專案中的 `Program.cs`。</span><span class="sxs-lookup"><span data-stu-id="c40dc-170">Open `Program.cs` within the *DotNetTutorial* project.</span></span> <span data-ttu-id="c40dc-171">然後，如檔案頂端附近所指定新增您的認證：</span><span class="sxs-lookup"><span data-stu-id="c40dc-171">Then add your credentials as specified near the top of the file:</span></span>

```csharp
// Update the Batch and Storage account credential strings below with the values
// unique to your accounts. These are used when constructing connection strings
// for the Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="c40dc-172">如上所述，目前您必須在 Azure 儲存體中指定**一般用途**儲存體帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="c40dc-172">As mentioned above, you must currently specify the credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="c40dc-173">Batch 應用程式會使用**一般用途**儲存體帳戶中的 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="c40dc-173">Your Batch applications use blob storage within the **general-purpose** storage account.</span></span> <span data-ttu-id="c40dc-174">請勿指定透過選取「Blob 儲存體」  帳戶類型所建立的儲存體帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="c40dc-174">Do not specify the credentials for a Storage account that was created by selecting the *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="c40dc-175">您可以在 [Azure 入口網站][azure_portal]中每項服務的帳戶刀鋒視窗中尋找您的 Batch 和儲存體帳戶認證：</span><span class="sxs-lookup"><span data-stu-id="c40dc-175">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="c40dc-176">![入口網站中的 Batch 認證][9]
![入口網站中的儲存體認證][10]</span><span class="sxs-lookup"><span data-stu-id="c40dc-176">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="c40dc-177">您現已使用認證更新專案，以滑鼠右鍵按一下 [方案總管] 中的方案，然後按一下 [建置方案] 。</span><span class="sxs-lookup"><span data-stu-id="c40dc-177">Now that you've updated the project with your credentials, right-click the solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="c40dc-178">出現提示時，請確認任何 NuGet 封裝的還原。</span><span class="sxs-lookup"><span data-stu-id="c40dc-178">Confirm the restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="c40dc-179">如果未自動還原 NuGet 套件，或看到有關套件還原失敗的錯誤，請確定您已安裝 [NuGet 套件管理員][nuget_packagemgr]。</span><span class="sxs-lookup"><span data-stu-id="c40dc-179">If the NuGet packages are not automatically restored, or if you see errors about a failure to restore the packages, ensure that you have the [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="c40dc-180">然後啟用遺失封裝的下載。</span><span class="sxs-lookup"><span data-stu-id="c40dc-180">Then enable the download of missing packages.</span></span> <span data-ttu-id="c40dc-181">若要啟用套件下載，請參閱[在建置期間啟用套件還原][nuget_restore]。</span><span class="sxs-lookup"><span data-stu-id="c40dc-181">See [Enabling Package Restore During Build][nuget_restore] to enable package download.</span></span>
>
>

<span data-ttu-id="c40dc-182">在下列各節中，我們會將範例應用程式細分為用來處理 Batch 服務中工作負載的數個步驟，並詳細討論這些步驟。</span><span class="sxs-lookup"><span data-stu-id="c40dc-182">In the following sections, we break down the sample application into the steps that it performs to process a workload in the Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="c40dc-183">建議您在進行本文的其餘部分時參閱 Visual Studio 中開啟的方案，因為並不會討論範例中的每一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="c40dc-183">We encourage you to refer to the open solution in Visual Studio while you work your way through the rest of this article, since not every line of code in the sample is discussed.</span></span>

<span data-ttu-id="c40dc-184">瀏覽至 DotNetTutorial*`Program.cs` 專案的*  檔案中 `MainAsync` 方法的頂端，開始進行步驟 1。</span><span class="sxs-lookup"><span data-stu-id="c40dc-184">Navigate to the top of the `MainAsync` method in the *DotNetTutorial* project's `Program.cs` file to start with Step 1.</span></span> <span data-ttu-id="c40dc-185">以下每個步驟大致會依 `MainAsync`中的方法呼叫進展而定。</span><span class="sxs-lookup"><span data-stu-id="c40dc-185">Each step below then roughly follows the progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="c40dc-186">步驟 1：建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="c40dc-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="c40dc-187">![在 Azure 儲存體中建立容器][1]
</span><span class="sxs-lookup"><span data-stu-id="c40dc-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="c40dc-188">Batch 包含與 Azure 儲存體進行互動的內建支援。</span><span class="sxs-lookup"><span data-stu-id="c40dc-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="c40dc-189">儲存體帳戶內的容器會提供在您的 Batch 帳戶中執行的工作所需的檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-189">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="c40dc-190">容器也會提供一個位置來儲存工作所產生的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="c40dc-190">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="c40dc-191">DotNetTutorial  用戶端應用程式首先會在 [Azure Blob 儲存體](../storage/common/storage-introduction.md)中建立三個容器：</span><span class="sxs-lookup"><span data-stu-id="c40dc-191">The first thing the *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="c40dc-192">**應用程式**：此容器將存放工作所執行的應用程式，以及其相依性 (如 DLL)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-192">**application**: This container will store the application run by the tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="c40dc-193">**輸入**：工作會從「輸入」容器下載所要處理的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-193">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="c40dc-194">**輸出**：當工作完成輸入檔案的處理時，它們會將結果上傳至「輸出」容器。</span><span class="sxs-lookup"><span data-stu-id="c40dc-194">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="c40dc-195">為了與儲存體帳戶進行互動並建立容器，我們使用 [Azure Storage Client Library for .NET][net_api_storage]。</span><span class="sxs-lookup"><span data-stu-id="c40dc-195">In order to interact with a Storage account and create containers, we use the [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="c40dc-196">我們使用 [CloudStorageAccount][net_cloudstorageaccount] 建立帳戶的參考，並從中建立 [CloudBlobClient][net_cloudblobclient]：</span><span class="sxs-lookup"><span data-stu-id="c40dc-196">We create a reference to the account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct the Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve the storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create the blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="c40dc-197">我們在整個應用程式中使用 `blobClient` 參考，並將它當作參數傳遞給數個方法。</span><span class="sxs-lookup"><span data-stu-id="c40dc-197">We use the `blobClient` reference throughout the application and pass it as a parameter to several methods.</span></span> <span data-ttu-id="c40dc-198">此範例是在緊接上述的程式碼區塊中，我們會在其中呼叫 `CreateContainerIfNotExistAsync` 以實際建立容器。</span><span class="sxs-lookup"><span data-stu-id="c40dc-198">An example of this is in the code block that immediately follows the above, where we call `CreateContainerIfNotExistAsync` to actually create the containers.</span></span>

```csharp
// Use the blob client to create the containers in Azure Storage if they don't
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

<span data-ttu-id="c40dc-199">建立容器之後，應用程式現在即可上傳工作所要使用的檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="c40dc-200">[如何使用 .NET 的 Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)提供使用 Azure 儲存體容器和 Blob 的概觀。</span><span class="sxs-lookup"><span data-stu-id="c40dc-200">[How to use Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="c40dc-201">當您開始使用 Batch 時，此概觀應在您的閱讀清單的頂端附近。</span><span class="sxs-lookup"><span data-stu-id="c40dc-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="c40dc-202">步驟 2：上傳工作應用程式和資料檔案</span><span class="sxs-lookup"><span data-stu-id="c40dc-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="c40dc-203">![將工作應用程式和輸入 (資料) 檔案上傳至容器][2]
</span><span class="sxs-lookup"><span data-stu-id="c40dc-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="c40dc-204">在檔案上傳作業中，DotNetTutorial 會先定義**應用程式**和**輸入**檔案路徑的集合 (因為其存在於本機電腦上)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-204">In the file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="c40dc-205">然後將這些檔案上傳到在上一個步驟中建立的容器。</span><span class="sxs-lookup"><span data-stu-id="c40dc-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```csharp
// Paths to the executable and its dependencies that will be executed by the tasks
List<string> applicationFilePaths = new List<string>
{
    // The DotNetTutorial project includes a project reference to TaskApplication,
    // allowing us to determine the path of the task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// The collection of data files that are to be processed by the tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload the application and its dependencies to Azure Storage. This is the
// application that will process the data files, and will be executed by each
// of the tasks on the compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload the data files. This is the data that will be processed by each of
// the tasks that are executed on the compute nodes within the pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="c40dc-206">`Program.cs` 中有個方法涉及上傳程序：</span><span class="sxs-lookup"><span data-stu-id="c40dc-206">There are two methods in `Program.cs` that are involved in the upload process:</span></span>

* <span data-ttu-id="c40dc-207">`UploadFilesToContainerAsync`：此方法會傳回 [ResourceFile][net_resourcefile] 物件的集合 (下面討論)，並在內部呼叫 `UploadFileToContainerAsync` 以上傳在 filePaths 參數中傳入的每個檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` to upload each file that is passed in the *filePaths* parameter.</span></span>
* <span data-ttu-id="c40dc-208">`UploadFileToContainerAsync`：這是實際執行檔案上傳並建立 [ResourceFile][net_resourcefile] 物件的方法。</span><span class="sxs-lookup"><span data-stu-id="c40dc-208">`UploadFileToContainerAsync`: This is the method that actually performs the file upload and creates the [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="c40dc-209">上傳檔案之後，它會取得此檔案的共用存取簽章 (SAS) 並傳回代表它的 ResourceFile 物件。</span><span class="sxs-lookup"><span data-stu-id="c40dc-209">After uploading the file, it obtains a shared access signature (SAS) for the file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="c40dc-210">下面也會討論共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="c40dc-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} to container [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set the expiry time and permissions for the blob shared access signature.
        // In this case, no start time is specified, so the shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct the SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="c40dc-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="c40dc-211">ResourceFiles</span></span>
<span data-ttu-id="c40dc-212">[ResourceFile][net_resourcefile] 提供 Batch 中的工作，以及 Azure 儲存體中會在工作執行前下載到計算節點之檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="c40dc-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="c40dc-213">[ResourceFile.BlobSource][net_resourcefile_blobsource] 屬性會指定 Azure 儲存體中現有檔案的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="c40dc-213">The [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="c40dc-214">此 URL 也可能包含可供安全存取檔案的共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-214">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="c40dc-215">Batch .NET 中的大部分工作類型都包含 ResourceFiles  屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="c40dc-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="c40dc-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="c40dc-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="c40dc-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="c40dc-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="c40dc-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="c40dc-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="c40dc-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="c40dc-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="c40dc-220">DotNetTutorial 範例應用程式不會使用 JobPreparationTask 或 JobReleaseTask 工作類型，但您可以在 [在 Azure Batch 計算節點上執行作業準備和完成工作](batch-job-prep-release.md)中深入了解。</span><span class="sxs-lookup"><span data-stu-id="c40dc-220">The DotNetTutorial sample application does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="c40dc-221">共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="c40dc-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="c40dc-222">共用存取簽章納入為 URL 的一部分時，便可安全存取 Azure 儲存體中容器和 Blob 的字串。</span><span class="sxs-lookup"><span data-stu-id="c40dc-222">Shared access signatures are strings which—when included as part of a URL—provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="c40dc-223">DotNetTutorial 應用程式會使用 Blob 和容器共用存取簽章 URL，並示範如何從儲存體服務取得這些共用存取簽章字串。</span><span class="sxs-lookup"><span data-stu-id="c40dc-223">The DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="c40dc-224">**Blob 共用存取簽章**：DotNetTutorial 中集區的 StartTask 會在從儲存體下載應用程式二進位檔和輸入資料檔案時，使用 Blob 共用存取簽章 (請參閱下面步驟 3)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-224">**Blob shared access signatures**: The pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads the application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="c40dc-225">DotNetTutorial 的 `Program.cs` 中的 `UploadFileToContainerAsync` 方法包含可取得各 Blob 共用存取簽章的程式碼。</span><span class="sxs-lookup"><span data-stu-id="c40dc-225">The `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="c40dc-226">呼叫 [CloudBlob.GetSharedAccessSignature][net_sas_blob] 即可完成。</span><span class="sxs-lookup"><span data-stu-id="c40dc-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="c40dc-227">**容器共用存取簽章**：每個工作在計算節點上完成其工作時，便會將其輸出檔案上傳至 Azure 儲存體中的「輸出」容器。</span><span class="sxs-lookup"><span data-stu-id="c40dc-227">**Container shared access signatures**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="c40dc-228">若要這樣做，TaskApplication 會使用容器共用存取簽章，其在上傳檔案時提供寫入容器以成為路徑的一部分的存取權。</span><span class="sxs-lookup"><span data-stu-id="c40dc-228">To do so, TaskApplication uses a container shared access signature that provides write access to the container as part of the path when it uploads the file.</span></span> <span data-ttu-id="c40dc-229">取得容器共用存取簽章與取得 Blob 共用存取簽章的方式很類似。</span><span class="sxs-lookup"><span data-stu-id="c40dc-229">Obtaining the container shared access signature is done in a similar fashion as when obtaining the blob shared access signature.</span></span> <span data-ttu-id="c40dc-230">在 DotNetTutorial 中，您會發現 `GetContainerSasUrl` 協助程式方法會呼叫 [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] 來進行此操作。</span><span class="sxs-lookup"><span data-stu-id="c40dc-230">In DotNetTutorial, you will find that the `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] to do so.</span></span> <span data-ttu-id="c40dc-231">您將在「步驟 6：監視工作」中進一步了解 TaskApplication 如何使用容器共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="c40dc-231">You'll read more about how TaskApplication uses the container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="c40dc-232">查看有關共用存取簽章的兩部分系列[第 1 部分：了解共用存取簽章 (SAS) 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)和[第 2 部分：建立和使用共用存取簽章 (SAS) 與 Blob 儲存體](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)，進一步了解如何提供您儲存體帳戶中資料的安全存取。</span><span class="sxs-lookup"><span data-stu-id="c40dc-232">Check out the two-part series on shared access signatures, [Part 1: Understanding the shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="c40dc-233">步驟 3：建立 Batch 集區</span><span class="sxs-lookup"><span data-stu-id="c40dc-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="c40dc-234">![建立 Batch 集區][3]
</span><span class="sxs-lookup"><span data-stu-id="c40dc-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="c40dc-235">Batch **集區** 是 Batch 執行作業工作所在的計算節點 (虛擬機器) 集合。</span><span class="sxs-lookup"><span data-stu-id="c40dc-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="c40dc-236">透過 Azure 儲存體 API 將應用程式和資料檔案上傳至儲存體帳戶之後，DotNetTutorial 會透過 Batch .NET 程式庫所提供的 API 開始呼叫 Batch 服務。</span><span class="sxs-lookup"><span data-stu-id="c40dc-236">After uploading the application and data files to the Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls to the Batch service with APIs provided by the Batch .NET library.</span></span> <span data-ttu-id="c40dc-237">程式碼會先建立 [BatchClient][net_batchclient]：</span><span class="sxs-lookup"><span data-stu-id="c40dc-237">The code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="c40dc-238">接著，範例會呼叫 `CreatePoolIfNotExistsAsync` 以在 Batch 帳戶中建立計算節點集區。</span><span class="sxs-lookup"><span data-stu-id="c40dc-238">Next, the sample creates a pool of compute nodes in the Batch account with a call to `CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="c40dc-239">`CreatePoolIfNotExistsAsync` 會使用 [BatchClient.PoolOperations.CreatePool][net_pool_create] 方法在 Batch 服務中建立新集區：</span><span class="sxs-lookup"><span data-stu-id="c40dc-239">`CreatePoolIfNotExistsAsync` uses the [BatchClient.PoolOperations.CreatePool][net_pool_create] method to create a new pool in the Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create the unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign the StartTask that will be executed when compute nodes join the pool.
        // In this case, we copy the StartTask's resource files (that will be automatically downloaded
        // to the node by the StartTask) into the shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for the StartTask that copies the task application files to the
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need to manually exit with a 0 for Batch to recognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow the specific error code PoolExists since that is expected if the pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("The pool {0} already existed when we tried to create it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="c40dc-240">利用 [CreatePool][net_pool_create] 建立集區時，您會指定數個參數，例如計算節點數目、[節點大小](../cloud-services/cloud-services-sizes-specs.md)以及節點的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c40dc-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as the number of compute nodes, the [size of the nodes](../cloud-services/cloud-services-sizes-specs.md), and the nodes' operating system.</span></span> <span data-ttu-id="c40dc-241">在 DotNetTutorial 中，我們使用 [CloudServiceConfiguration][net_cloudserviceconfiguration] 以從[雲端服務](../cloud-services/cloud-services-guestos-update-matrix.md)指定 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="c40dc-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] to specify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="c40dc-242">您也可以為集區指定 [VirtualMachineConfiguration][net_virtualmachineconfiguration]，以建立 Azure 虛擬機器 (VM) 計算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="c40dc-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying the [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="c40dc-243">您可以從 Windows 或 [Linux 映像](batch-linux-nodes.md)建立 VM 計算節點的集區。</span><span class="sxs-lookup"><span data-stu-id="c40dc-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="c40dc-244">VM 映像的來源可以是：</span><span class="sxs-lookup"><span data-stu-id="c40dc-244">The source for your VM images can be either:</span></span>

- <span data-ttu-id="c40dc-245">[Azure 虛擬機器 Marketplace][vm_marketplace]，其中提供立即可用的 Windows 和 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="c40dc-245">The [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="c40dc-246">您準備和提供的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="c40dc-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="c40dc-247">如需自訂映像的詳細資訊，請參閱[使用 Batch 開發大規模的平行計算解決方案](batch-api-basics.md#pool)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c40dc-248">您需對 Batch 中的計算資源付費。</span><span class="sxs-lookup"><span data-stu-id="c40dc-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="c40dc-249">若要將成本降到最低，您可以在執行範例前，將 `targetDedicatedComputeNodes` 降為 1。</span><span class="sxs-lookup"><span data-stu-id="c40dc-249">To minimize costs, you can lower `targetDedicatedComputeNodes` to 1 before you run the sample.</span></span>
>
>

<span data-ttu-id="c40dc-250">透過這些實體節點屬性，您也可以指定集區的 [StartTask][net_pool_starttask]。</span><span class="sxs-lookup"><span data-stu-id="c40dc-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for the pool.</span></span> <span data-ttu-id="c40dc-251">StartTask 會在每個節點加入集區以及每次重新啟動節點時，於該節點上執行。</span><span class="sxs-lookup"><span data-stu-id="c40dc-251">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="c40dc-252">StartTask 特別適合用於在工作執行前，在計算節點上安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="c40dc-252">The StartTask is especially useful for installing applications on compute nodes prior to the execution of tasks.</span></span> <span data-ttu-id="c40dc-253">例如，如果您的工作使用 Python 指令碼來處理資料，您可以使用 StartTask 在計算節點上安裝 Python。</span><span class="sxs-lookup"><span data-stu-id="c40dc-253">For example, if your tasks process data by using Python scripts, you could use a StartTask to install Python on the compute nodes.</span></span>

<span data-ttu-id="c40dc-254">在此範例應用程式中，StartTask 會將它從儲存體下載的檔案 (使用 [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] 屬性所指定)，從 StartTask 工作目錄複製到在節點上執行的「所有」工作可以存取的共用目錄。</span><span class="sxs-lookup"><span data-stu-id="c40dc-254">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from the StartTask working directory to the shared directory that *all* tasks running on the node can access.</span></span> <span data-ttu-id="c40dc-255">基本上，這會在節點加入集區時複製 `TaskApplication.exe` 和其相依性到每個節點上的共用目錄，以便在節點上執行的任何工作都能存取它。</span><span class="sxs-lookup"><span data-stu-id="c40dc-255">Essentially, this copies `TaskApplication.exe` and its dependencies to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="c40dc-256">Azure Batch 的 **應用程式封裝** 功能提供了另一種方式來將應用程式放到集區中的計算節點上。</span><span class="sxs-lookup"><span data-stu-id="c40dc-256">The **application packages** feature of Azure Batch provides another way to get your application onto the compute nodes in a pool.</span></span> <span data-ttu-id="c40dc-257">如需詳細資訊，請參閱[使用 Batch 應用程式套件將應用程式部署至計算節點](batch-application-packages.md)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-257">See [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="c40dc-258">此外，在上述程式碼片段中值得注意的是在 StartTask 的 CommandLine 屬性中使用的兩個環境變數：`%AZ_BATCH_TASK_WORKING_DIR%` 和 `%AZ_BATCH_NODE_SHARED_DIR%`。</span><span class="sxs-lookup"><span data-stu-id="c40dc-258">Also notable in the code snippet above is the use of two environment variables in the *CommandLine* property of the StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="c40dc-259">Batch 集區中的每個計算節點都會自動以 Batch 特有的數個環境變數進行設定。</span><span class="sxs-lookup"><span data-stu-id="c40dc-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="c40dc-260">工作所執行的任何程序都可以存取這些環境變數。</span><span class="sxs-lookup"><span data-stu-id="c40dc-260">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="c40dc-261">若要深入了解 Batch 集區中計算節點上可用的環境變數，以及有關工作的工作目錄資訊，請參閱[適用於開發人員的 Batch 功能概觀](batch-api-basics.md)中的[工作的環境設定](batch-api-basics.md#environment-settings-for-tasks)和[檔案和目錄](batch-api-basics.md#files-and-directories)章節。</span><span class="sxs-lookup"><span data-stu-id="c40dc-261">To find out more about the environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see the [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in the [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="c40dc-262">步驟 4：建立 Batch 作業</span><span class="sxs-lookup"><span data-stu-id="c40dc-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="c40dc-263">![建立 Batch 作業][4]</span><span class="sxs-lookup"><span data-stu-id="c40dc-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="c40dc-264">Batch **作業** 是與計算節點集區相關聯的工作集合。</span><span class="sxs-lookup"><span data-stu-id="c40dc-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="c40dc-265">作業中的工作會在相關聯集區的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="c40dc-265">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="c40dc-266">您不僅可使用作業來組織及追蹤相關工作負載中的工作，也可以強加特定條件約束，例如作業 (並延伸至其工作) 的最大執行階段，以及相對於 Batch 帳戶中其他作業的作業優先順序。</span><span class="sxs-lookup"><span data-stu-id="c40dc-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) as well as job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="c40dc-267">不過，在此範例中，作業只與在步驟 3 建立的集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="c40dc-267">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="c40dc-268">不會設定任何其他屬性。</span><span class="sxs-lookup"><span data-stu-id="c40dc-268">No additional properties are configured.</span></span>

<span data-ttu-id="c40dc-269">所有 Batch 作業都會與特定集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="c40dc-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="c40dc-270">此關聯表示將會在哪些節點上執行作業的工作。</span><span class="sxs-lookup"><span data-stu-id="c40dc-270">This association indicates which nodes the job's tasks will execute on.</span></span> <span data-ttu-id="c40dc-271">您可使用 [CloudJob.PoolInformation][net_job_poolinfo] 屬性來指定此關聯，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="c40dc-271">You specify this by using the [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in the code snippet below.</span></span>

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

<span data-ttu-id="c40dc-272">現已建立一個作業，便會加入工作來進行工作。</span><span class="sxs-lookup"><span data-stu-id="c40dc-272">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="c40dc-273">步驟 5：將工作加入至作業</span><span class="sxs-lookup"><span data-stu-id="c40dc-273">Step 5: Add tasks to job</span></span>
<span data-ttu-id="c40dc-274">![將工作加入至作業][5]</span><span class="sxs-lookup"><span data-stu-id="c40dc-274">![Add tasks to job][5]</span></span><br/><span data-ttu-id="c40dc-275">
*(1) 工作已新增至作業，(2) 工作已排定在節點上執行，以及 (3) 工作會下載要處理的資料檔案*</span><span class="sxs-lookup"><span data-stu-id="c40dc-275">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="c40dc-276">Batch **工作** 是在計算節點上執行的個別工作單位。</span><span class="sxs-lookup"><span data-stu-id="c40dc-276">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="c40dc-277">工作有一個命令列，可執行您在該命令列中指定的指令碼或可執行檔。</span><span class="sxs-lookup"><span data-stu-id="c40dc-277">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="c40dc-278">若要實際進行工作，必須將工作加入至作業。</span><span class="sxs-lookup"><span data-stu-id="c40dc-278">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="c40dc-279">每個 [CloudTask][net_task] 都是使用命令列屬性以及工作在其命令列自動執行前下載至節點的 [ResourceFiles][net_task_resourcefiles] (如同集區的 StartTask) 進行設定。</span><span class="sxs-lookup"><span data-stu-id="c40dc-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="c40dc-280">在 DotNetTutorial  範例專案中，每個工作只會處理一個檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-280">In the *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="c40dc-281">因此其 ResourceFiles 集合只包含單一元素。</span><span class="sxs-lookup"><span data-stu-id="c40dc-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks to job [{1}]...", inputFiles.Count, jobId);

    // Create a collection to hold the tasks that we'll be adding to the job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of the tasks. Because we copied the task application to the
    // node's shared directory with the pool's StartTask, we can access it via
    // the shared directory on the node that the task runs on.
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

    // Add the tasks as a collection, as opposed to issuing a separate AddTask call
    // for each. Bulk task submission helps to ensure efficient underlying API calls
    // to the Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="c40dc-282">當工作存取環境變數 (例如 `%AZ_BATCH_NODE_SHARED_DIR%`) 或執行在節點的 `PATH` 中找不到的應用程式時，工作命令列的前面必須加上 `cmd /c`。</span><span class="sxs-lookup"><span data-stu-id="c40dc-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in the node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="c40dc-283">這麼做可明確地執行命令解譯器，並指示它在執行命令之後終止。</span><span class="sxs-lookup"><span data-stu-id="c40dc-283">This will explicitly execute the command interpreter and instruct it to terminate after carrying out your command.</span></span> <span data-ttu-id="c40dc-284">如果您的工作在節點的 `PATH` 中執行應用程式 (例如 robocopy.exe 或 powershell.exe)，而且未使用任何環境變數，這就不是必要條件。</span><span class="sxs-lookup"><span data-stu-id="c40dc-284">This requirement is unnecessary if your tasks execute an application in the node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="c40dc-285">在上述程式碼片段中的 `foreach` 迴圈內，您可以看到已建構工作的命令列，以致有三個命令列引數傳遞至 TaskApplication.exe：</span><span class="sxs-lookup"><span data-stu-id="c40dc-285">Within the `foreach` loop in the code snippet above, you can see that the command line for the task is constructed such that three command-line arguments are passed to *TaskApplication.exe*:</span></span>

1. <span data-ttu-id="c40dc-286">**第一個引數** 是要處理之檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="c40dc-286">The **first argument** is the path of the file to process.</span></span> <span data-ttu-id="c40dc-287">這是節點上現有檔案的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="c40dc-287">This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="c40dc-288">第一次在上述 `UploadFileToContainerAsync` 中建立 ResourceFile 物件時，檔案名稱會用於此屬性 (做為 ResourceFile 建構函式的參數)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-288">When the ResourceFile object in `UploadFileToContainerAsync` was first created above, the file name was used for this property (as a parameter to the ResourceFile constructor).</span></span> <span data-ttu-id="c40dc-289">這表示可以在與 TaskApplication.exe 相同的目錄中找到檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-289">This indicates that the file can be found in the same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="c40dc-290">**第二個引數**指定最前面 N 個單字應該寫入輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-290">The **second argument** specifies that the top *N* words should be written to the output file.</span></span> <span data-ttu-id="c40dc-291">在此範例中，此為硬式編碼，所以前 3 個單字會寫入輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="c40dc-291">In the sample, this is hard-coded so that the top three words are written to the output file.</span></span>
3. <span data-ttu-id="c40dc-292">**第三個引數**是共用存取簽章 (SAS)，可提供 Azure 儲存體中**輸出**容器的寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="c40dc-292">The **third argument** is the shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="c40dc-293"> 將輸出檔上傳至 Azure 儲存體時，會使用此共用存取簽章 URL。</span><span class="sxs-lookup"><span data-stu-id="c40dc-293">*TaskApplication.exe* uses this shared access signature URL when it uploads the output file to Azure Storage.</span></span> <span data-ttu-id="c40dc-294">您可以在 TaskApplication 專案的 `Program.cs` 檔案的 `UploadFileToContainer` 方法中找到其程式碼：</span><span class="sxs-lookup"><span data-stu-id="c40dc-294">You can find the code for this in the `UploadFileToContainer` method in the TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference to the container using the SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload the file (as a new blob) to the container
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

                // Indicate that a failure has occurred so that when the Batch service
                // sets the CloudTask.ExecutionInformation.ExitCode for the task that
                // executed this application, it properly indicates that there was a
                // problem with the task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="c40dc-295">步驟 6：監視工作</span><span class="sxs-lookup"><span data-stu-id="c40dc-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="c40dc-296">![監視工作][6]</span><span class="sxs-lookup"><span data-stu-id="c40dc-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="c40dc-297">
*用戶端應用程式 (1) 會監視工作的完成和成功狀態，以及 (2) 將結果資料上傳至 Azure 儲存體的工作*</span><span class="sxs-lookup"><span data-stu-id="c40dc-297">
*The client application (1) monitors the tasks for completion and success status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="c40dc-298">工作新增至作業時，會自動排入佇列及排程，以便在與作業相關聯的集區中的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="c40dc-298">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="c40dc-299">根據您指定的設定，Batch 會為您處理所有工作佇列、排程、重試和其他工作管理責任。</span><span class="sxs-lookup"><span data-stu-id="c40dc-299">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="c40dc-300">監視工作執行的方法有許多種。</span><span class="sxs-lookup"><span data-stu-id="c40dc-300">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="c40dc-301">DotNetTutorial 顯示了一個只報告完成和工作失敗或成功狀態的簡單範例。</span><span class="sxs-lookup"><span data-stu-id="c40dc-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="c40dc-302">DotNetTutorial 的 `Program.cs` 中的 `MonitorTasks` 方法內，有三個 Batch .NET 概念值得討論。</span><span class="sxs-lookup"><span data-stu-id="c40dc-302">Within the `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="c40dc-303">底下依其出現的順序列出：</span><span class="sxs-lookup"><span data-stu-id="c40dc-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="c40dc-304">**ODATADetailLevel**：一定要在清單作業 (例如取得作業的工作清單) 中指定 [ODATADetailLevel][net_odatadetaillevel]，以確保 Batch 應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="c40dc-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="c40dc-305">如果您計劃在 Batch 應用程式內進行任何類型的狀態監視，請將 [有效率地查詢 Azure Batch 服務](batch-efficient-list-queries.md) 加入至您的閱讀清單。</span><span class="sxs-lookup"><span data-stu-id="c40dc-305">Add [Query the Azure Batch service efficiently](batch-efficient-list-queries.md) to your reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="c40dc-306">**TaskStateMonitor**：[TaskStateMonitor][net_taskstatemonitor] 提供給 Batch .NET 應用程可用來監視工作狀態的協助公用程式。</span><span class="sxs-lookup"><span data-stu-id="c40dc-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="c40dc-307">在 `MonitorTasks` 中，DotNetTutorial 會等候所有工作在時限內達到 [TaskState.Completed][net_taskstate]。</span><span class="sxs-lookup"><span data-stu-id="c40dc-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks to reach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="c40dc-308">然後終止作業。</span><span class="sxs-lookup"><span data-stu-id="c40dc-308">Then it terminates the job.</span></span>
3. <span data-ttu-id="c40dc-309">**TerminateJobAsync**：透過 [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] 終止作業 (或封鎖 JobOperations.TerminateJob) 會將該作業標記為已完成。</span><span class="sxs-lookup"><span data-stu-id="c40dc-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or the blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="c40dc-310">如果您的 Batch 方案使用 [JobReleaseTask][net_jobreltask]，請務必這樣做。</span><span class="sxs-lookup"><span data-stu-id="c40dc-310">It is essential to do so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="c40dc-311">如 [作業準備和完成工作](batch-job-prep-release.md)中所述，這是一種特殊的工作類型。</span><span class="sxs-lookup"><span data-stu-id="c40dc-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="c40dc-312">DotNetTutorial 的 `Program.cs` 中的 `MonitorTasks` 方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="c40dc-312">The `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed to reach the Completed state within the timeout period.";

    // Obtain the collection of tasks currently managed by the job. Note that we use
    // a detail level to  specify that only the "id" property of each task should be
    // populated. Using a detail level for all list operations helps to lower
    // response time from the Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor to monitor the state of our tasks. In this case, we
    // will wait for all tasks to reach the Completed state.
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

    // All tasks have reached the "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property to ensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update the detail level to populate only the task id and executionInfo
    // properties. We refresh the tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate the task's properties with the latest info from the Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with the task. It is important to note that
            // the task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that the application executed by the task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within the specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="c40dc-313">步驟 7：下載工作輸出</span><span class="sxs-lookup"><span data-stu-id="c40dc-313">Step 7: Download task output</span></span>
<span data-ttu-id="c40dc-314">![從儲存體下載工作輸出][7]</span><span class="sxs-lookup"><span data-stu-id="c40dc-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="c40dc-315">現已完成作業，可以從 Azure 儲存體下載工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="c40dc-315">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="c40dc-316">在 DotNetTutorial*`Program.cs` 的*  中呼叫 `DownloadBlobsFromContainerAsync` 即可完成此操作：</span><span class="sxs-lookup"><span data-stu-id="c40dc-316">This is done with a call to `DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference to a previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all the block blobs in the specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference to the current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents to a file in the specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded to {0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="c40dc-317">在 DotNetTutorial 應用程式中呼叫 `DownloadBlobsFromContainerAsync`，可讓您指定檔案應下載到您的 `%TEMP%` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c40dc-317">The call to `DownloadBlobsFromContainerAsync` in the *DotNetTutorial* application specifies that the files should be downloaded to your `%TEMP%` folder.</span></span> <span data-ttu-id="c40dc-318">您可隨意修改此輸出位置。</span><span class="sxs-lookup"><span data-stu-id="c40dc-318">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="c40dc-319">步驟 8：刪除容器</span><span class="sxs-lookup"><span data-stu-id="c40dc-319">Step 8: Delete containers</span></span>
<span data-ttu-id="c40dc-320">因為您需對位於 Azure 儲存體中的資料付費，所以建議您移除您的 Batch 作業不再需要的 Blob。</span><span class="sxs-lookup"><span data-stu-id="c40dc-320">Because you are charged for data that resides in Azure Storage, it's always a good idea to remove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="c40dc-321">在 DotNetTutorial 的 `Program.cs` 中，呼叫協助程式方法 `DeleteContainerAsync` 三次即可辦到：</span><span class="sxs-lookup"><span data-stu-id="c40dc-321">In DotNetTutorial's `Program.cs`, this is done with three calls to the helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="c40dc-322">此方法本身只會取得容器的參考，然後呼叫 [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]：</span><span class="sxs-lookup"><span data-stu-id="c40dc-322">The method itself merely obtains a reference to the container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

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

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="c40dc-323">步驟 9：刪除作業和集區</span><span class="sxs-lookup"><span data-stu-id="c40dc-323">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="c40dc-324">在最後一個步驟中，系統會提示您刪除 DotNetTutorial 應用程式所建立的作業和集區。</span><span class="sxs-lookup"><span data-stu-id="c40dc-324">In the final step, you're prompted to delete the job and the pool that were created by the DotNetTutorial application.</span></span> <span data-ttu-id="c40dc-325">雖然您不需支付作業和工作的費用，但您「需」支付計算節點的費用。</span><span class="sxs-lookup"><span data-stu-id="c40dc-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="c40dc-326">因此，我們建議您只在必要時配置節點。</span><span class="sxs-lookup"><span data-stu-id="c40dc-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="c40dc-327">刪除未使用的集區可成為您維護程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="c40dc-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="c40dc-328">BatchClient 的 [JobOperations][net_joboperations] 和 [PoolOperations][net_pooloperations] 兩者都有對應的刪除方法 (在使用者確認刪除時呼叫)：</span><span class="sxs-lookup"><span data-stu-id="c40dc-328">The BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if the user confirms deletion:</span></span>

```csharp
// Clean up the resources we've created in the Batch account if the user so chooses
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
> <span data-ttu-id="c40dc-329">請記住，您需支付計算資源的費用，而刪除未使用的集區會將成本降到最低。</span><span class="sxs-lookup"><span data-stu-id="c40dc-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="c40dc-330">另外請注意，刪除集區也會刪除該集區內的所有計算節點，而刪除集區後，將無法復原節點上的任何資料。</span><span class="sxs-lookup"><span data-stu-id="c40dc-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-dotnettutorial-sample"></a><span data-ttu-id="c40dc-331">執行 DotNetTutorial  範例</span><span class="sxs-lookup"><span data-stu-id="c40dc-331">Run the *DotNetTutorial* sample</span></span>
<span data-ttu-id="c40dc-332">當您執行範例應用程式時，主控台輸出大致如下。</span><span class="sxs-lookup"><span data-stu-id="c40dc-332">When you run the sample application, the console output will be similar to the following.</span></span> <span data-ttu-id="c40dc-333">在執行期間，啟動集區的計算節點時，您將在 `Awaiting task completion, timeout in 00:30:00...` 遇到暫停。</span><span class="sxs-lookup"><span data-stu-id="c40dc-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while the pool's compute nodes are started.</span></span> <span data-ttu-id="c40dc-334">在執行期間和之後，使用 [Azure 入口網站][azure_portal]來監視集區、計算節點、作業和工作。</span><span class="sxs-lookup"><span data-stu-id="c40dc-334">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="c40dc-335">使用 [Azure 入口網站][azure_portal]或 [Azure 儲存體總管][storage_explorers]來檢視應用程式所建立的儲存體資源 (容器和 Blob)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-335">Use the [Azure portal][azure_portal] or the [Azure Storage Explorer][storage_explorers] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

<span data-ttu-id="c40dc-336">以預設設定執行應用程式時，一般的執行時間 **大約 5 分鐘** 。</span><span class="sxs-lookup"><span data-stu-id="c40dc-336">Typical execution time is **approximately 5 minutes** when you run the application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe to container [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll to container [application]...
Uploading file ..\..\taskdata1.txt to container [input]...
Uploading file ..\..\taskdata2.txt to container [input]...
Uploading file ..\..\taskdata3.txt to container [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks to job [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within the specified timeout period.
Downloading all files from container [output]...
All files downloaded to C:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="c40dc-337">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c40dc-337">Next steps</span></span>
<span data-ttu-id="c40dc-338">您可隨意變更 DotNetTutorial 和 TaskApplication，以試驗不同的計算案例。</span><span class="sxs-lookup"><span data-stu-id="c40dc-338">Feel free to make changes to *DotNetTutorial* and *TaskApplication* to experiment with different compute scenarios.</span></span> <span data-ttu-id="c40dc-339">例如，嘗試將執行延遲新增至 TaskApplication (例如使用 [Thread.Sleep][net_thread_sleep])，以模擬長時間執行的工作並在入口網站中監視這些工作。</span><span class="sxs-lookup"><span data-stu-id="c40dc-339">For example, try adding an execution delay to *TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="c40dc-340">嘗試新增更多工作，或調整計算節點的數目。</span><span class="sxs-lookup"><span data-stu-id="c40dc-340">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="c40dc-341">新增邏輯來檢查並允許使用現有的集區加速執行時間 (提示：簽出 [azure-batch-samples][github_samples] 中 [Microsoft.Azure.Batch.Samples.Common][github_samples_common] 專案的 `ArticleHelpers.cs`)。</span><span class="sxs-lookup"><span data-stu-id="c40dc-341">Add logic to check for and allow the use of an existing pool to speed execution time (*hint*: check out `ArticleHelpers.cs` in the [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="c40dc-342">既然您已熟悉 Batch 方案的基本工作流程，現在可以深入了解 Batch 服務的其他功能。</span><span class="sxs-lookup"><span data-stu-id="c40dc-342">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="c40dc-343">如果您不熟悉這項服務，我們建議檢閱 [Azure Batch 功能概觀](batch-api-basics.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="c40dc-343">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="c40dc-344">從 [Batch 學習路徑][batch_learning_path]中的**深入開發**之下的其他 Batch 開發文章著手。</span><span class="sxs-lookup"><span data-stu-id="c40dc-344">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="c40dc-345">使用 [TopNWords][github_topnwords] 範例，查看處理「前 N 個單字」工作負載的不同實作方式。</span><span class="sxs-lookup"><span data-stu-id="c40dc-345">Check out a different implementation of processing the "top N words" workload by using Batch in the [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="c40dc-346">檢閱 Batch .NET [版本資訊](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes)，以取得文件庫中的最新變更。</span><span class="sxs-lookup"><span data-stu-id="c40dc-346">Review the Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for the latest changes in the library.</span></span>

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
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "將工作應用程式和輸入 (資料) 檔案上傳至容器"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "建立 Batch 集區"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "建立 Batch 作業"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "將工作新增至作業"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "監視工作"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "從儲存體下載工作輸出"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Batch 方案工作流程 (完整圖表)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "入口網站中的 Batch 認證"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "入口網站中的儲存體認證"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Batch 方案工作流程 (最小圖表)"
