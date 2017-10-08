---
title: "aaaTutorial-使用 hello Azure 批次 SDK for Python |Microsoft 文件"
description: "了解 hello Azure Batch 基本概念，並建立使用 Python 的簡易解決方案。"
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="d827c-103">開始使用 hello 批次 SDK for Python</span><span class="sxs-lookup"><span data-stu-id="d827c-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d827c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d827c-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="d827c-105">Python</span><span class="sxs-lookup"><span data-stu-id="d827c-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="d827c-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="d827c-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="d827c-107">了解 hello 基本概念的[Azure Batch] [ azure_batch]和 hello[批次 Python] [ py_azure_sdk]用戶端我們討論 Python 中撰寫的小批次應用程式。</span><span class="sxs-lookup"><span data-stu-id="d827c-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="d827c-108">我們會審視如何這兩個範例指令碼使用 hello 批次服務 tooprocess hello 雲端中的 Linux 虛擬機器上的平行工作負載以及它們如何互動與[Azure 儲存體](../storage/common/storage-introduction.md)檔案暫存和擷取。</span><span class="sxs-lookup"><span data-stu-id="d827c-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="d827c-109">您將了解常見的批次應用程式工作流程和基底的 hello 主要元件批次的工作、 工作、 集區，例如了解計算節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="d827c-110">![Batch 方案工作流程 (基本)][11]</span><span class="sxs-lookup"><span data-stu-id="d827c-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="d827c-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="d827c-111">Prerequisites</span></span>
<span data-ttu-id="d827c-112">本文假設您已具備 Python 的使用知識並熟悉 Linux。</span><span class="sxs-lookup"><span data-stu-id="d827c-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="d827c-113">它也假設您使用的是可以 toosatisfy hello 帳戶建立所指定需求的下面針對 Azure hello 批次和儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="d827c-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="d827c-114">帳戶</span><span class="sxs-lookup"><span data-stu-id="d827c-114">Accounts</span></span>
* <span data-ttu-id="d827c-115">**Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶][azure_free_account]。</span><span class="sxs-lookup"><span data-stu-id="d827c-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="d827c-116">**Batch 帳戶**：擁有 Azure 訂用帳戶後，請 [建立 Azure Batch 帳戶](batch-account-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d827c-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="d827c-117">**儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="d827c-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="d827c-118">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="d827c-118">Code sample</span></span>
<span data-ttu-id="d827c-119">hello Python 教學課程[程式碼範例][ github_article_samples]是其中一個在 hello 中找到多個批次的程式碼範例的 hello [azure 批次範例][ github_samples]上的儲存機制GitHub。</span><span class="sxs-lookup"><span data-stu-id="d827c-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="d827c-120">您可以按一下 下載所有 hello 範例**複製或都下載 > 都下載 ZIP** hello 儲存機制首頁上，或按一下 hello [azure 批次範例-master.zip] [ github_samples_zip]直接下載連結。</span><span class="sxs-lookup"><span data-stu-id="d827c-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="d827c-121">一旦您已擷取 hello hello ZIP 檔案的內容，本教學課程中的 hello 兩個指令碼位於 hello`article_samples`目錄：</span><span class="sxs-lookup"><span data-stu-id="d827c-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="d827c-122">Python 環境</span><span class="sxs-lookup"><span data-stu-id="d827c-122">Python environment</span></span>
<span data-ttu-id="d827c-123">toorun hello *python_tutorial_client.py*範例指令碼在您的本機工作站上，您需要**Python 解釋器**版本相容的**2.7**或**3.3 +**。</span><span class="sxs-lookup"><span data-stu-id="d827c-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="d827c-124">Linux 及 Windows 上，已經過測試 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d827c-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="d827c-125">密碼編譯相依項目</span><span class="sxs-lookup"><span data-stu-id="d827c-125">cryptography dependencies</span></span>
<span data-ttu-id="d827c-126">您必須安裝 hello 的相依性 hello[加密][ crypto]程式庫，所需的 hello`azure-batch`和`azure-storage`Python 封裝。</span><span class="sxs-lookup"><span data-stu-id="d827c-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="d827c-127">執行其中一個 hello 遵循適用於您的平台的作業，或參閱 toohello[加密安裝][ crypto_install]如需詳細資訊的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="d827c-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="d827c-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d827c-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="d827c-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="d827c-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="d827c-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="d827c-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="d827c-131">Windows</span><span class="sxs-lookup"><span data-stu-id="d827c-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="d827c-132">如果安裝 python 3.3 + on Linux，請使用 hello python3 對等項目 hello Python 相依性。</span><span class="sxs-lookup"><span data-stu-id="d827c-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="d827c-133">例如，在 Ubuntu 上︰ `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="d827c-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="d827c-134">Azure 套件</span><span class="sxs-lookup"><span data-stu-id="d827c-134">Azure packages</span></span>
<span data-ttu-id="d827c-135">接下來，安裝 hello **Azure Batch**和**Azure 儲存體**Python 封裝。</span><span class="sxs-lookup"><span data-stu-id="d827c-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="d827c-136">您可以使用來安裝這兩個封裝**pip**和 hello *requirements.txt*這裡找到：</span><span class="sxs-lookup"><span data-stu-id="d827c-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="d827c-137">下列問題**pip** tooinstall hello 批次和儲存封裝的命令：</span><span class="sxs-lookup"><span data-stu-id="d827c-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="d827c-138">或者，您可以安裝 hello [azure 批次][ pypi_batch]和[azure 儲存體][ pypi_storage] Python 封裝以手動方式：</span><span class="sxs-lookup"><span data-stu-id="d827c-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="d827c-139">如果您使用無特殊權限的帳戶，您可能需要 tooprefix 與命令`sudo`。</span><span class="sxs-lookup"><span data-stu-id="d827c-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="d827c-140">例如： `sudo pip install -r requirements.txt`。</span><span class="sxs-lookup"><span data-stu-id="d827c-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="d827c-141">如需有關如何安裝 Python 套件的詳細資訊，請參閱 readthedocs.io 上的[安裝套件][pypi_install]。</span><span class="sxs-lookup"><span data-stu-id="d827c-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="d827c-142">Batch Python 教學課程程式碼範例</span><span class="sxs-lookup"><span data-stu-id="d827c-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="d827c-143">hello 批次 Python 教學課程的程式碼範例是由兩個的 Python 指令碼和幾個資料檔案所組成。</span><span class="sxs-lookup"><span data-stu-id="d827c-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="d827c-144">**python_tutorial_client.py**： 互動 hello 批次和儲存體服務 tooexecute 計算節點 （虛擬機器） 上的平行工作負載。</span><span class="sxs-lookup"><span data-stu-id="d827c-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="d827c-145">hello *python_tutorial_client.py*您的本機工作站上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="d827c-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="d827c-146">**python_tutorial_task.py**: hello 執行的指令碼中的計算節點 Azure tooperform hello 實際工作。</span><span class="sxs-lookup"><span data-stu-id="d827c-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="d827c-147">在 hello 範例*python_tutorial_task.py*剖析 hello 下載自 Azure 儲存體 （hello 輸入檔） 的檔案中的文字。</span><span class="sxs-lookup"><span data-stu-id="d827c-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="d827c-148">然後它會產生文字檔案 （hello 輸出檔），其中包含出現在 hello 輸入檔中的 hello 前三個單字的清單。</span><span class="sxs-lookup"><span data-stu-id="d827c-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="d827c-149">它會建立 hello 輸出檔案之後, *python_tutorial_task.py*上傳 hello 檔案 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d827c-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="d827c-150">這可讓您的工作站上執行的下載 toohello 用戶端指令碼。</span><span class="sxs-lookup"><span data-stu-id="d827c-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="d827c-151">hello *python_tutorial_task.py*指令碼會以平行方式在多個計算 hello 批次服務中的節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="d827c-152">**./data/taskdata\*.txt**： 下列三個文字檔提供 hello 輸入 hello 上執行的 hello 工作計算節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="d827c-153">hello 下列圖表說明 hello hello 用戶端和工作指令碼所執行的主要作業。</span><span class="sxs-lookup"><span data-stu-id="d827c-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="d827c-154">此基本工作流程通常由使用 Batch 建立的許多計算方案所組成。</span><span class="sxs-lookup"><span data-stu-id="d827c-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="d827c-155">雖然它不會示範 hello 批次服務中可用的每一項功能，幾乎每個批次案例包含此工作流程的部分。</span><span class="sxs-lookup"><span data-stu-id="d827c-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="d827c-156">![Batch 範例工作流程][8]</span><span class="sxs-lookup"><span data-stu-id="d827c-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="d827c-157">**步驟 1.**</span><span class="sxs-lookup"><span data-stu-id="d827c-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="d827c-158">在 Azure Blob 儲存體中建立**容器**。</span><span class="sxs-lookup"><span data-stu-id="d827c-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="d827c-159">
[**步驟 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="d827c-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="d827c-160">上傳工作的指令碼和輸入檔案的 toocontainers。</span><span class="sxs-lookup"><span data-stu-id="d827c-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="d827c-161">
[**步驟 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="d827c-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="d827c-162">建立 Batch **集區**。</span><span class="sxs-lookup"><span data-stu-id="d827c-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="d827c-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="d827c-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="d827c-164">hello 集區**StartTask**下載 hello 工作指令碼 (python_tutorial_task.py) toonodes，因為它們加入 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="d827c-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="d827c-165">
[**步驟 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="d827c-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="d827c-166">建立 Batch **作業**。</span><span class="sxs-lookup"><span data-stu-id="d827c-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="d827c-167">
[**步驟 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="d827c-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="d827c-168">新增**工作**toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="d827c-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="d827c-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="d827c-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="d827c-170">hello 工作是排定的 tooexecute 節點上。</span><span class="sxs-lookup"><span data-stu-id="d827c-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="d827c-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="d827c-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="d827c-172">每項工作會從 Azure 儲存體下載其輸入資料，然後開始執行。</span><span class="sxs-lookup"><span data-stu-id="d827c-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="d827c-173">
[**步驟 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="d827c-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="d827c-174">監視工作。</span><span class="sxs-lookup"><span data-stu-id="d827c-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="d827c-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="d827c-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="d827c-176">工作完成後，它們上傳其輸出資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d827c-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="d827c-177">
[**步驟 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="d827c-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="d827c-178">從儲存體下載工作輸出。</span><span class="sxs-lookup"><span data-stu-id="d827c-178">Download task output from Storage.</span></span>

<span data-ttu-id="d827c-179">如上所述，並非每個 Batch 方案都會執行這些確切步驟，並且可能包含更多步驟，但此範例會示範在 Batch 方案中找到的一般程序。</span><span class="sxs-lookup"><span data-stu-id="d827c-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="d827c-180">準備用戶端指令碼</span><span class="sxs-lookup"><span data-stu-id="d827c-180">Prepare client script</span></span>
<span data-ttu-id="d827c-181">執行 hello 範例之前，請加入您的批次和儲存體帳戶認證太*python_tutorial_client.py*。</span><span class="sxs-lookup"><span data-stu-id="d827c-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="d827c-182">如果您尚未執行此動作 hello 中開啟檔案下列行，您的認證與您最愛編輯器和 update hello。</span><span class="sxs-lookup"><span data-stu-id="d827c-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="d827c-183">您可以找到您的批次和儲存體帳戶認證中的每個服務的 hello 帳戶 刀鋒視窗中 hello [Azure 入口網站][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="d827c-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="d827c-184">![批次 hello 入口網站中的認證][9]
![hello 入口網站中的儲存體認證][10]</span><span class="sxs-lookup"><span data-stu-id="d827c-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="d827c-185">在下列各節的 hello，我們分析所使用的 hello 步驟 hello 指令碼 tooprocess hello 批次服務中的工作負載。</span><span class="sxs-lookup"><span data-stu-id="d827c-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="d827c-186">我們鼓勵您 toorefer 定期 toohello 時您編輯器中的指令碼處理 hello 文章的 hello 其餘部分。</span><span class="sxs-lookup"><span data-stu-id="d827c-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="d827c-187">瀏覽下列行中的 toohello **python_tutorial_client.py** toostart 與步驟 1:</span><span class="sxs-lookup"><span data-stu-id="d827c-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="d827c-188">步驟 1：建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="d827c-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="d827c-189">![在 Azure 儲存體中建立容器][1]
</span><span class="sxs-lookup"><span data-stu-id="d827c-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="d827c-190">Batch 包含與 Azure 儲存體進行互動的內建支援。</span><span class="sxs-lookup"><span data-stu-id="d827c-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="d827c-191">在儲存體帳戶的容器會提供在您的 Batch 帳戶中執行的 hello 工作所需的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d827c-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="d827c-192">hello 容器也會提供 hello 工作產生的地方 toostore hello 輸出資料。</span><span class="sxs-lookup"><span data-stu-id="d827c-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="d827c-193">首先 hello hello *python_tutorial_client.py*指令碼會建立三個容器在[Azure Blob 儲存體](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="d827c-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="d827c-194">**應用程式**： 此容器會儲存 hello hello 工作所執行的 Python 指令碼*python_tutorial_task.py*。</span><span class="sxs-lookup"><span data-stu-id="d827c-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="d827c-195">**輸入**： 工作會從 hello 下載 hello 資料檔案 tooprocess*輸入*容器。</span><span class="sxs-lookup"><span data-stu-id="d827c-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="d827c-196">**輸出**： 當工作完成時輸入的檔案處理時，他們會將上傳 hello 結果 toohello*輸出*容器。</span><span class="sxs-lookup"><span data-stu-id="d827c-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="d827c-197">在順序 toointeract 與儲存體帳戶，並建立容器，我們使用 hello [azure 儲存體][ pypi_storage]封裝 toocreate [BlockBlobService] [ py_blockblobservice]物件--hello 「 blob 用戶端 」。</span><span class="sxs-lookup"><span data-stu-id="d827c-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="d827c-198">然後，我們會建立三個容器使用 hello blob 用戶端 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d827c-198">We then create three containers in hello Storage account using hello blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="d827c-199">一旦已建立 hello 容器，hello 應用程式現在可以將 hello 工作所使用的 hello 檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="d827c-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="d827c-200">[如何 toouse 來自 Python 的 Azure Blob 儲存體](../storage/blobs/storage-python-how-to-use-blob-storage.md)提供使用 Azure 儲存體容器和 blob 的良好概觀。</span><span class="sxs-lookup"><span data-stu-id="d827c-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="d827c-201">當您使用批次開始使用，它應該是 hello 讀取清單頂端附近。</span><span class="sxs-lookup"><span data-stu-id="d827c-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="d827c-202">步驟 2：上傳工作指令碼和資料檔案</span><span class="sxs-lookup"><span data-stu-id="d827c-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="d827c-203">![上傳工作應用程式，並輸入 （資料） 檔 toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="d827c-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="d827c-204">Hello 檔案中上傳作業， *python_tutorial_client.py*的集合會先定義**應用程式**和**輸入**存在於 hello 本機電腦上檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="d827c-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="d827c-205">然後它上傳您在 hello 上一個步驟中建立這些檔案 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="d827c-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="d827c-206">使用清單理解，hello `upload_file_to_container` hello 集合中的每個檔案和兩個呼叫函式[ResourceFile] [ py_resource_file]會填入集合。</span><span class="sxs-lookup"><span data-stu-id="d827c-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="d827c-207">hello`upload_file_to_container`函式會出現下方：</span><span class="sxs-lookup"><span data-stu-id="d827c-207">hello `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="d827c-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="d827c-208">ResourceFiles</span></span>
<span data-ttu-id="d827c-209">A [ResourceFile] [ py_resource_file]提供批次中的工作會下載的 tooa 的 Azure 儲存體中的 hello URL tooa 檔案與計算節點，才能執行該工作。</span><span class="sxs-lookup"><span data-stu-id="d827c-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="d827c-210">hello [ResourceFile][py_resource_file]。**blob_source**存在於 Azure 儲存體中，屬性會指定 hello 的 hello 檔案的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="d827c-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="d827c-211">hello URL 也可能包括提供安全的 access toohello 檔案的共用的存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="d827c-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="d827c-212">Batch 中的大部分工作類型都包含 ResourceFiles  屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="d827c-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="d827c-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="d827c-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="d827c-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="d827c-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="d827c-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="d827c-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="d827c-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="d827c-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="d827c-217">此範例不會使用 hello JobPreparationTask 或 JobReleaseTask 工作類型，但您可以深入資訊，請在[執行作業準備與完成工作上 Azure Batch 計算節點](batch-job-prep-release.md)。</span><span class="sxs-lookup"><span data-stu-id="d827c-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="d827c-218">共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="d827c-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="d827c-219">共用的存取簽章是提供安全地存取 toocontainers 和 Azure 儲存體中的 blob 的字串。</span><span class="sxs-lookup"><span data-stu-id="d827c-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="d827c-220">hello *python_tutorial_client.py*指令碼會使用這兩個 blob 和容器共用存取簽章，並示範如何 tooobtain 這些共用存取簽章字串 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="d827c-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="d827c-221">**Blob 共用的存取簽章**： 從儲存體下載 hello 工作指令碼和輸入資料檔案時，集區 hello StartTask 使用 blob 共用的存取簽章 (請參閱[步驟 #3](#step-3-create-batch-pool)下方)。</span><span class="sxs-lookup"><span data-stu-id="d827c-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="d827c-222">hello`upload_file_to_container`函式在*python_tutorial_client.py*包含 hello 程式碼會取得每個 blob 的共用的存取簽章。</span><span class="sxs-lookup"><span data-stu-id="d827c-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="d827c-223">它是藉由呼叫[BlockBlobService.make_blob_url] [ py_make_blob_url] hello Storage 模組中。</span><span class="sxs-lookup"><span data-stu-id="d827c-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="d827c-224">**容器的共用的存取簽章**： 為每項工作完成其工作 hello 計算節點上的上, 傳其輸出檔 toohello*輸出*Azure 儲存體容器中的。</span><span class="sxs-lookup"><span data-stu-id="d827c-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="d827c-225">toodo， *python_tutorial_task.py*使用容器的共用的存取簽章可提供寫入存取 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="d827c-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="d827c-226">hello`get_container_sas_token`函式在*python_tutorial_client.py*取得 hello 容器的共用的存取簽章，然後傳遞做為命令列引數 toohello 工作。</span><span class="sxs-lookup"><span data-stu-id="d827c-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="d827c-227">步驟 5，[新增工作 tooa 作業](#step-5-add-tasks-to-job)，討論 hello 使用量的 hello 容器 SAS。</span><span class="sxs-lookup"><span data-stu-id="d827c-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="d827c-228">簽出 hello 兩段式序列上的共用的存取簽章，[第 1 部分： 了解 hello SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)和[第 2 部分： 建立和使用以 hello Blob 服務 SAS](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)，toolearn 更多關於提供安全存取toodata 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d827c-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="d827c-229">步驟 3：建立 Batch 集區</span><span class="sxs-lookup"><span data-stu-id="d827c-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="d827c-230">![建立 Batch 集區][3]
</span><span class="sxs-lookup"><span data-stu-id="d827c-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="d827c-231">Batch **集區** 是 Batch 執行作業工作所在的計算節點 (虛擬機器) 集合。</span><span class="sxs-lookup"><span data-stu-id="d827c-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="d827c-232">上傳 hello 工作指令碼和資料檔案 toohello 儲存體帳戶之後, *python_tutorial_client.py*使用 hello 批次 Python 模組啟動與 hello 批次服務之間的互動。</span><span class="sxs-lookup"><span data-stu-id="d827c-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="d827c-233">toodo， [BatchServiceClient] [ py_batchserviceclient]建立：</span><span class="sxs-lookup"><span data-stu-id="d827c-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="d827c-234">接下來，建立集區的計算節點在 hello 與呼叫的批次帳戶太`create_pool`。</span><span class="sxs-lookup"><span data-stu-id="d827c-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="d827c-235">當您建立集區時，您會定義[PoolAddParameter] [ py_pooladdparam]指定 hello 集區的數個屬性：</span><span class="sxs-lookup"><span data-stu-id="d827c-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="d827c-236">**識別碼**hello 集區 (*識別碼*-必要項目)</span><span class="sxs-lookup"><span data-stu-id="d827c-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="d827c-237">如同 Batch 中的大部分實體，新的集區必須具有 Batch 帳戶內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="d827c-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="d827c-238">您的程式碼是指 toothis 集區使用其識別碼，而且它是識別 hello Azure 中的 hello 集區的方式[入口網站][azure_portal]。</span><span class="sxs-lookup"><span data-stu-id="d827c-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="d827c-239">**計算節點數目** (target_dedicated -必要)</span><span class="sxs-lookup"><span data-stu-id="d827c-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="d827c-240">此屬性會指定應該將多少 Vm 部署在 hello 集區中。</span><span class="sxs-lookup"><span data-stu-id="d827c-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="d827c-241">它是所有的批次帳戶都具有預設值的重要 toonote**配額**限制 hello 數目**核心**（和因此，計算節點） 批次帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d827c-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="d827c-242">您可以找到 hello 預設配額和指示如何太[增加配額](batch-quota-limit.md#increase-a-quota)（例如 hello 的批次帳戶中的核心數目上限） 中[hello Azure 批次服務的配額與限制](batch-quota-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="d827c-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="d827c-243">如果您發現自問「為什麼我的集區不會觸達 X 個以上的節點？</span><span class="sxs-lookup"><span data-stu-id="d827c-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="d827c-244">此核心配額可能 hello 可能的原因。</span><span class="sxs-lookup"><span data-stu-id="d827c-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="d827c-245">節點的**作業系統** (virtual_machine_configuration **或** cloud_service_configuration - 必要)</span><span class="sxs-lookup"><span data-stu-id="d827c-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="d827c-246">在 *python_tutorial_client.py*，我們會使用 [VirtualMachineConfiguration][py_vm_config] 建立 Linux 節點的集區。</span><span class="sxs-lookup"><span data-stu-id="d827c-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="d827c-247">hello`select_latest_verified_vm_image_with_node_agent_sku`函式在`common.helpers`簡化對處理[Azure 虛擬機器 Marketplace] [ vm_marketplace]映像。</span><span class="sxs-lookup"><span data-stu-id="d827c-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="d827c-248">如需使用 Marketplace 映像的詳細資訊，請參閱 [在 Azure Batch 集區中佈建 Linux 計算節點](batch-linux-nodes.md) 。</span><span class="sxs-lookup"><span data-stu-id="d827c-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="d827c-249">**計算節點的大小** (*vm_size* - 必要)</span><span class="sxs-lookup"><span data-stu-id="d827c-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="d827c-250">因為我們要針對 [VirtualMachineConfiguration][py_vm_config] 指定 Linux 節點，所以我們會從 [Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)指定 VM 大小 (在此範例中為 `STANDARD_A1`)。</span><span class="sxs-lookup"><span data-stu-id="d827c-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d827c-251">同樣地，如需詳細資訊，請參閱 [在 Azure Batch 集區中佈建 Linux 計算節點](batch-linux-nodes.md) 。</span><span class="sxs-lookup"><span data-stu-id="d827c-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="d827c-252">**啟動工作** (start_task - 非必要)</span><span class="sxs-lookup"><span data-stu-id="d827c-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="d827c-253">Hello 上方實體節點內容，以及您也可以指定[StartTask] [ py_starttask] hello 集區 （不需要）。</span><span class="sxs-lookup"><span data-stu-id="d827c-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="d827c-254">hello StartTask 執行每個節點上，該節點加入 hello 集區，以及每次重新啟動節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="d827c-255">hello StartTask 是特別適用於運算節點準備 hello 執行工作，例如安裝您的工作執行的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d827c-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="d827c-256">在此範例應用程式，hello StartTask 會複製它會從儲存體下載的 hello 檔案 (其指定使用 hello StartTask **resource_files**屬性) 從 hello StartTask *的工作目錄* toohello*共用*hello 節點上執行的所有工作可以都存取的目錄。</span><span class="sxs-lookup"><span data-stu-id="d827c-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="d827c-257">基本上，這會將複製`python_tutorial_task.py`toohello 共用目錄每個節點上的為 hello 節點加入 hello 集區，以便在 hello 節點執行任何工作可以存取它。</span><span class="sxs-lookup"><span data-stu-id="d827c-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="d827c-258">您可能會注意到 hello 呼叫 toohello `wrap_commands_in_shell` helper 函式。</span><span class="sxs-lookup"><span data-stu-id="d827c-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="d827c-259">此函式會採用不同命令的集合，並針對工作的命令列屬性建立合適的單一命令列。</span><span class="sxs-lookup"><span data-stu-id="d827c-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="d827c-260">也在 hello 上述程式碼片段的值得注意的是兩個環境中的變數 hello hello 使用**command_line** hello StartTask 屬性：`AZ_BATCH_TASK_WORKING_DIR`和`AZ_BATCH_NODE_SHARED_DIR`。</span><span class="sxs-lookup"><span data-stu-id="d827c-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="d827c-261">批次集區中每個運算節點會自動設定成有特定 tooBatch 的數個環境變數中。</span><span class="sxs-lookup"><span data-stu-id="d827c-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="d827c-262">任何處理程序所執行的工作有存取 toothese 環境變數。</span><span class="sxs-lookup"><span data-stu-id="d827c-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="d827c-263">toofind 深入了解 hello 環境變數所提供的計算節點的批次集區，以及有關工作的工作目錄，請參閱**工作的環境設定**和**檔案和目錄**在 hello [Azure Batch 功能概觀](batch-api-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="d827c-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="d827c-264">步驟 4：建立 Batch 作業</span><span class="sxs-lookup"><span data-stu-id="d827c-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="d827c-265">![建立 Batch 作業][4]</span><span class="sxs-lookup"><span data-stu-id="d827c-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="d827c-266">Batch **作業** 是與計算節點集區相關聯的工作集合。</span><span class="sxs-lookup"><span data-stu-id="d827c-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="d827c-267">作業中的 hello 工作執行相關聯的 hello 集區的計算節點上。</span><span class="sxs-lookup"><span data-stu-id="d827c-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="d827c-268">不只對組織及追蹤相關的工作負載中的工作，也諸特定條件約束-例如 hello 最大 runtime hello 作業 （和延伸模組，其工作），您可以使用工作和工作中的關聯性 tooother 工作中的優先順序 hello Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d827c-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="d827c-269">在此範例中，不過，hello 作業是只能搭配步驟 #3 中建立的 hello 集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="d827c-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="d827c-270">不會設定任何其他屬性。</span><span class="sxs-lookup"><span data-stu-id="d827c-270">No additional properties are configured.</span></span>

<span data-ttu-id="d827c-271">所有 Batch 作業都會與特定集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="d827c-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="d827c-272">這項關聯指示 hello 作業 」 工作執行哪些節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="d827c-273">您指定 hello 集區使用 hello [PoolInformation] [ py_poolinfo]屬性 hello 下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="d827c-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="d827c-274">已建立工作，工作會新增 tooperform hello 工作。</span><span class="sxs-lookup"><span data-stu-id="d827c-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="d827c-275">步驟 5： 加入工作 toojob</span><span class="sxs-lookup"><span data-stu-id="d827c-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="d827c-276">![新增工作 toojob][5]</span><span class="sxs-lookup"><span data-stu-id="d827c-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="d827c-277">
*（1） 工作已加入 toohello 作業、 （2) hello 工作是排定的 toorun 節點上，以及 （3) hello 工作下載 hello 資料檔案 tooprocess*</span><span class="sxs-lookup"><span data-stu-id="d827c-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="d827c-278">批次**工作**是 hello 個別的工作單位 hello 上所執行的計算節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="d827c-279">工作已命令列，並執行 hello 指令碼或您在該命令列中指定的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="d827c-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="d827c-280">tooactually 執行工作、 工作必須加入 tooa 作業。</span><span class="sxs-lookup"><span data-stu-id="d827c-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="d827c-281">每個[CloudTask] [ py_task]設定命令列屬性和[ResourceFiles] [ py_resource_file] （如同 hello 集區 StartTask） 該 hello自動執行它的命令列之前，工作會下載 toohello 節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="d827c-282">在 hello 範例中，每項工作會處理一個檔案。</span><span class="sxs-lookup"><span data-stu-id="d827c-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="d827c-283">因此其 ResourceFiles 集合只包含單一元素。</span><span class="sxs-lookup"><span data-stu-id="d827c-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> <span data-ttu-id="d827c-284">當他們存取環境變數這類`$AZ_BATCH_NODE_SHARED_DIR`或執行應用程式中的 hello 節點找不到`PATH`，工作的命令列必須叫用 hello 與殼層明確，例如`/bin/sh -c MyTaskApplication $MY_ENV_VAR`。</span><span class="sxs-lookup"><span data-stu-id="d827c-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="d827c-285">這項需求是不必要，如果您的工作執行應用程式中的 hello 節點`PATH`而且不會參考任何環境變數。</span><span class="sxs-lookup"><span data-stu-id="d827c-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="d827c-286">在 hello `for` hello 上述程式碼片段中的迴圈，您可以看到 hello hello 工作的命令列五個太傳遞的命令列引數與建構*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="d827c-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="d827c-287">**filepath**： 這是 hello 本機路徑 toohello 檔案存在於 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="d827c-288">當 hello 中的 ResourceFile 物件`upload_file_to_container`建立 hello 檔案名稱使用這個屬性在上述步驟 2，(hello `file_path` hello ResourceFile 建構函式中的參數)。</span><span class="sxs-lookup"><span data-stu-id="d827c-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="d827c-289">這表示該 hello 檔案位於 hello 相同 hello 節點，做為目錄*python_tutorial_task.py*。</span><span class="sxs-lookup"><span data-stu-id="d827c-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="d827c-290">**numwords**: hello 頂端*N*字詞應該寫 toohello 輸出檔。</span><span class="sxs-lookup"><span data-stu-id="d827c-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="d827c-291">**storageaccount**： 應上傳 hello hello 擁有 hello 容器 toowhich hello 工作輸出的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d827c-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="d827c-292">**storagecontainer**： 應上傳檔案輸出 hello 儲存體容器 toowhich hello hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="d827c-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="d827c-293">**sastoken**: hello 共用的存取簽章 (SAS)，提供寫入存取 toohello**輸出**Azure 儲存體容器中的。</span><span class="sxs-lookup"><span data-stu-id="d827c-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="d827c-294">hello *python_tutorial_task.py*指令碼會使用此共用的存取簽章時建立其 BlockBlobService 參考。</span><span class="sxs-lookup"><span data-stu-id="d827c-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="d827c-295">這可以提供寫入存取 toohello 容器而不需要 hello 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="d827c-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="d827c-296">步驟 6：監視工作</span><span class="sxs-lookup"><span data-stu-id="d827c-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="d827c-297">![監視工作][6]</span><span class="sxs-lookup"><span data-stu-id="d827c-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="d827c-298">
*hello 指令碼 （1） 監視 hello 工作的完成狀態，以及 （2) hello 工作上傳的結果資料 tooAzure 儲存體*</span><span class="sxs-lookup"><span data-stu-id="d827c-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="d827c-299">當工作區加入 tooa 工作時，他們會自動排入佇列，排定在 hello 與 hello 工作相關聯的集區的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="d827c-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="d827c-300">根據您指定的 hello 設定，批次工作的所有佇列、 排程、 重試和其他工作的系統管理工作會為您處理。</span><span class="sxs-lookup"><span data-stu-id="d827c-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="d827c-301">有多種方法 toomonitoring 工作執行。</span><span class="sxs-lookup"><span data-stu-id="d827c-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="d827c-302">hello`wait_for_tasks_to_complete`函式在*python_tutorial_client.py*提供簡單的範例，可監視特定狀態，在此情況下，工作 hello[完成][ py_taskstate]狀態。</span><span class="sxs-lookup"><span data-stu-id="d827c-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="d827c-303">步驟 7：下載工作輸出</span><span class="sxs-lookup"><span data-stu-id="d827c-303">Step 7: Download task output</span></span>
<span data-ttu-id="d827c-304">![從儲存體下載工作輸出][7]</span><span class="sxs-lookup"><span data-stu-id="d827c-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="d827c-305">既然 hello 作業已完成，您可以從 Azure 儲存體下載 hello hello 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="d827c-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="d827c-306">這是透過呼叫太`download_blobs_from_container`中*python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="d827c-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="d827c-307">太 hello 呼叫`download_blobs_from_container`中*python_tutorial_client.py*指定 hello 檔案應該下載的 tooyour 主目錄。</span><span class="sxs-lookup"><span data-stu-id="d827c-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="d827c-308">感覺可用 toomodify 這輸出位置。</span><span class="sxs-lookup"><span data-stu-id="d827c-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="d827c-309">步驟 8：刪除容器</span><span class="sxs-lookup"><span data-stu-id="d827c-309">Step 8: Delete containers</span></span>
<span data-ttu-id="d827c-310">因為您必須支付位於 Azure 儲存體中的資料，永遠是個不錯的主意 tooremove 不再任何 blob 所需的批次作業。</span><span class="sxs-lookup"><span data-stu-id="d827c-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="d827c-311">在*python_tutorial_client.py*，做法是使用三個呼叫太[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="d827c-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="d827c-312">步驟 9： 刪除 hello 作業和 hello 集區</span><span class="sxs-lookup"><span data-stu-id="d827c-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="d827c-313">您可以在 hello 最後一個步驟中，是提示的 toodelete hello 作業和 hello 集區所建立的 hello *python_tutorial_client.py*指令碼。</span><span class="sxs-lookup"><span data-stu-id="d827c-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="d827c-314">雖然您不需支付作業和工作的費用，但您「需」  支付計算節點的費用。</span><span class="sxs-lookup"><span data-stu-id="d827c-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="d827c-315">因此，我們建議您只在必要時配置節點。</span><span class="sxs-lookup"><span data-stu-id="d827c-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="d827c-316">刪除未使用的集區可成為您維護程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="d827c-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="d827c-317">hello BatchServiceClient 的[JobOperations] [ py_job]和[PoolOperations] [ py_pool]兩者都有對應的刪除動作方法，也就是如果您確認刪除，呼叫：</span><span class="sxs-lookup"><span data-stu-id="d827c-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="d827c-318">請記住，您需支付計算資源的費用，而刪除未使用的集區會將成本降到最低。</span><span class="sxs-lookup"><span data-stu-id="d827c-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="d827c-319">此外，請注意，刪除集區會刪除所有的運算節點區內，而且之後刪除 hello 集區 hello 節點上的任何資料將無法復原。</span><span class="sxs-lookup"><span data-stu-id="d827c-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="d827c-320">執行 hello 範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d827c-320">Run hello sample script</span></span>
<span data-ttu-id="d827c-321">當您執行 hello *python_tutorial_client.py* hello 教學課程的指令碼[程式碼範例][github_article_samples]，hello 主控台輸出是類似 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="d827c-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="d827c-322">會出現在暫停`Monitoring all tasks for 'Completed' state, timeout in 0:20:00...`時建立 hello 集區的計算節點，啟動，並執行 hello 集區的啟動工作中的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="d827c-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="d827c-323">使用 hello [Azure 入口網站][ azure_portal] toomonitor 集區、 計算節點、 工作和工作期間和之後執行。</span><span class="sxs-lookup"><span data-stu-id="d827c-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="d827c-324">使用 hello [Azure 入口網站][ azure_portal]或 hello [Microsoft Azure 儲存體總管][ storage_explorer] tooview hello 存放裝置資源 （容器和 blob）建立的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d827c-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="d827c-325">執行 hello *python_tutorial_client.py* hello 內的指令碼從`azure-batch-samples/Python/Batch/article_samples`目錄。</span><span class="sxs-lookup"><span data-stu-id="d827c-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="d827c-326">它會使用相對路徑的 hello`common.helpers`模組匯入，因此您可能會看到`ImportError: No module named 'common'`如果您不要執行從這個目錄中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d827c-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="d827c-327">一般的執行時間是**大約 5-7 分鐘**當您執行 hello 範例以預設設定。</span><span class="sxs-lookup"><span data-stu-id="d827c-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="d827c-328">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d827c-328">Next steps</span></span>
<span data-ttu-id="d827c-329">太覺得可用 toomake 變更*python_tutorial_client.py*和*python_tutorial_task.py*不同 tooexperiment 計算案例。</span><span class="sxs-lookup"><span data-stu-id="d827c-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="d827c-330">例如，再次嘗試新增執行延遲太*python_tutorial_task.py* toosimulate 長時間執行工作，並在 hello 入口網站中監視它們。</span><span class="sxs-lookup"><span data-stu-id="d827c-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="d827c-331">再試一次新增更多工作，或調整 hello 的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="d827c-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="d827c-332">新增的邏輯 toocheck，並允許 hello 使用現有的集區 toospeed 執行時間。</span><span class="sxs-lookup"><span data-stu-id="d827c-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="d827c-333">既然您已熟悉 hello 批次解決方案的基本工作流程，它是 hello 的時間 toodig 中 toohello 批次服務的額外功能。</span><span class="sxs-lookup"><span data-stu-id="d827c-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="d827c-334">檢閱 hello [Azure Batch 概觀功能](batch-api-basics.md)發行項，我們建議您是否新增 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="d827c-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="d827c-335">開始在 hello 底下其他批次開發文件**深入開發**在 hello[批次學習路徑][batch_learning_path]。</span><span class="sxs-lookup"><span data-stu-id="d827c-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="d827c-336">簽出處理 hello 「 前 n 個單字"hello 與批次工作負載的不同實作[TopNWords] [ github_topnwords]範例。</span><span class="sxs-lookup"><span data-stu-id="d827c-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "在 Azure 儲存體中建立容器"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "上傳工作應用程式，並輸入 （資料） 檔 toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "建立 Batch 集區"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "建立 Batch 作業"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "新增工作 toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "監視工作"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "從儲存體下載工作輸出"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Batch 方案工作流程 (完整圖表)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "入口網站中的 Batch 認證"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "入口網站中的儲存體認證"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Batch 方案工作流程 (最小圖表)"
