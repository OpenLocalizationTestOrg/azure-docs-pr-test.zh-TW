---
title: "教學課程 - 使用適用於 Python 的 Azure Batch SDK | Microsoft Docs"
description: "了解 Azure Batch 的基本概念和使用 Python 建置簡單的解決方案。"
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
ms.openlocfilehash: bd5a977c10d3955639beb893cd7a37581b14f7c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-batch-sdk-for-python"></a><span data-ttu-id="232df-103">開始使用適用於 Python 的 Batch SDK</span><span class="sxs-lookup"><span data-stu-id="232df-103">Get started with the Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="232df-104">.NET</span><span class="sxs-lookup"><span data-stu-id="232df-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="232df-105">Python</span><span class="sxs-lookup"><span data-stu-id="232df-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="232df-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="232df-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="232df-107">在我們討論以 Python 撰寫的小型 Batch 應用程式時，了解 [Azure Batch][azure_batch] 和 [Batch Python][py_azure_sdk] 用戶端的基本概念。</span><span class="sxs-lookup"><span data-stu-id="232df-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="232df-108">我們看看這兩個範例指令碼如何使用 Batch 服務來處理雲端中 Linux 虛擬機器上的平行工作負載，以及如何與 [Azure 儲存體](../storage/common/storage-introduction.md) 互動來預備和擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="232df-108">We look at how two sample scripts use the Batch service to process a parallel workload on Linux virtual machines in the cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="232df-109">您將了解常見的 Batch 應用程式工作流程，並取得 Batch 的主要元件，例如作業、工作、集區和計算節點。</span><span class="sxs-lookup"><span data-stu-id="232df-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="232df-110">![Batch 方案工作流程 (基本)][11]</span><span class="sxs-lookup"><span data-stu-id="232df-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="232df-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="232df-111">Prerequisites</span></span>
<span data-ttu-id="232df-112">本文假設您已具備 Python 的使用知識並熟悉 Linux。</span><span class="sxs-lookup"><span data-stu-id="232df-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="232df-113">而且假設您可以滿足針對 Azure Batch 和儲存體服務所指定的帳戶建立需求。</span><span class="sxs-lookup"><span data-stu-id="232df-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="232df-114">帳戶</span><span class="sxs-lookup"><span data-stu-id="232df-114">Accounts</span></span>
* <span data-ttu-id="232df-115">**Azure 帳戶**：如果您沒有 Azure 訂用帳戶，請[建立免費的 Azure 帳戶][azure_free_account]。</span><span class="sxs-lookup"><span data-stu-id="232df-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="232df-116">**Batch 帳戶**：擁有 Azure 訂用帳戶後，請 [建立 Azure Batch 帳戶](batch-account-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="232df-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="232df-117">**儲存體帳戶**：請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)中的[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="232df-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="232df-118">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="232df-118">Code sample</span></span>
<span data-ttu-id="232df-119">Python 教學課程[程式碼範例][github_article_samples]是在 GitHub 上 [azure-batch-samples][github_samples] 儲存機制中找到的許多 Batch 程式碼範例之一。</span><span class="sxs-lookup"><span data-stu-id="232df-119">The Python tutorial [code sample][github_article_samples] is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="232df-120">按一下儲存機制首頁上的 [複製或下載] > [下載 ZIP]，或按一下 [azure-batch-samples-master.zip][github_samples_zip] 直接下載連結，即可下載所有範例。</span><span class="sxs-lookup"><span data-stu-id="232df-120">You can download all the samples by clicking **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="232df-121">解壓縮 ZIP 檔案的內容後，在 `article_samples` 目錄中可找到本教學課程的兩個指令碼︰</span><span class="sxs-lookup"><span data-stu-id="232df-121">Once you've extracted the contents of the ZIP file, the two scripts for this tutorial are found in the `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="232df-122">Python 環境</span><span class="sxs-lookup"><span data-stu-id="232df-122">Python environment</span></span>
<span data-ttu-id="232df-123">若要在本機工作站上執行 python_tutorial_client.py 範例指令碼，您需要與版本 **2.7** 或 **3.3+** 相容的 **Python 解譯器**。</span><span class="sxs-lookup"><span data-stu-id="232df-123">To run the *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="232df-124">此指令碼已在 Linux 和 Windows 上測試。</span><span class="sxs-lookup"><span data-stu-id="232df-124">The script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="232df-125">密碼編譯相依項目</span><span class="sxs-lookup"><span data-stu-id="232df-125">cryptography dependencies</span></span>
<span data-ttu-id="232df-126">您必須為[密碼編譯][crypto]程式庫安裝 `azure-batch` 和 `azure-storage` Python 套件所需的相依項目。</span><span class="sxs-lookup"><span data-stu-id="232df-126">You must install the dependencies for the [cryptography][crypto] library, required by the `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="232df-127">針對您的平台執行下列其中一個適用作業，或參閱[密碼編譯安裝][crypto_install]詳細資料以取得詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="232df-127">Perform one of the following operations appropriate for your platform, or refer to the [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="232df-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="232df-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="232df-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="232df-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="232df-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="232df-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="232df-131">Windows</span><span class="sxs-lookup"><span data-stu-id="232df-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="232df-132">如果要在 Linux 上安裝 Python 3.3+，請使用適用於 Python 相依項目的 python3 對等項目。</span><span class="sxs-lookup"><span data-stu-id="232df-132">If installing for Python 3.3+ on Linux, use the python3 equivalents for the Python dependencies.</span></span> <span data-ttu-id="232df-133">例如，在 Ubuntu 上︰ `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="232df-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="232df-134">Azure 套件</span><span class="sxs-lookup"><span data-stu-id="232df-134">Azure packages</span></span>
<span data-ttu-id="232df-135">接下來，請安裝 **Azure Batch** 和 **Azure 儲存體** Python 套件。</span><span class="sxs-lookup"><span data-stu-id="232df-135">Next, install the **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="232df-136">使用此處找到的 **pip** 和 *requirements.txt* 即可安裝這兩個套件：</span><span class="sxs-lookup"><span data-stu-id="232df-136">You can install both packages by using **pip** and the *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="232df-137">發出下列 **pip** 命令以安裝 Batch 和儲存體封裝：</span><span class="sxs-lookup"><span data-stu-id="232df-137">Issue following **pip** command to install the Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="232df-138">或者，您可以手動方式安裝 [azure-batch][pypi_batch] 和 [azure-storage][pypi_storage] Python 套件：</span><span class="sxs-lookup"><span data-stu-id="232df-138">Or, you can install the [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="232df-139">如果您使用無特殊權限的帳戶，則可能需要在您的命令前面加上 `sudo`。</span><span class="sxs-lookup"><span data-stu-id="232df-139">If you are using an unprivileged account, you may need to prefix your commands with `sudo`.</span></span> <span data-ttu-id="232df-140">例如， `sudo pip install -r requirements.txt`。</span><span class="sxs-lookup"><span data-stu-id="232df-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="232df-141">如需有關如何安裝 Python 套件的詳細資訊，請參閱 readthedocs.io 上的[安裝套件][pypi_install]。</span><span class="sxs-lookup"><span data-stu-id="232df-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="232df-142">Batch Python 教學課程程式碼範例</span><span class="sxs-lookup"><span data-stu-id="232df-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="232df-143">Batch Python 教學課程程式碼範例是由兩個 Python 指令碼和幾個資料檔案所組成。</span><span class="sxs-lookup"><span data-stu-id="232df-143">The Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="232df-144">**python_tutorial_client.py**：與 Batch 和儲存體服務進行互動，以在計算節點 (虛擬機器) 上執行平行工作負載的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="232df-144">**python_tutorial_client.py**: Interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="232df-145">python_tutorial_client.py 指令碼會在本機工作站上執行。</span><span class="sxs-lookup"><span data-stu-id="232df-145">The *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="232df-146">**python_tutorial_task.py**：在 Azure 中的計算節點上執行進而執行實際工作的指令碼。</span><span class="sxs-lookup"><span data-stu-id="232df-146">**python_tutorial_task.py**: The script that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="232df-147">在範例中，python_tutorial_task.py 會剖析從 Azure 儲存體下載的檔案 (輸入檔) 中的文字。</span><span class="sxs-lookup"><span data-stu-id="232df-147">In the sample, *python_tutorial_task.py* parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="232df-148">然後產生文字檔 (輸出檔)，其中包含出現在輸入檔中的前三個單字清單。</span><span class="sxs-lookup"><span data-stu-id="232df-148">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="232df-149">在它建立輸出檔之後，python_tutorial_task.py 會將此檔案上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="232df-149">After it creates the output file, *python_tutorial_task.py* uploads the file to Azure Storage.</span></span> <span data-ttu-id="232df-150">這讓檔案可供下載至您的工作站上執行的用戶端指令碼。</span><span class="sxs-lookup"><span data-stu-id="232df-150">This makes it available for download to the client script running on your workstation.</span></span> <span data-ttu-id="232df-151">python_tutorial_task.py 指令碼會在 Batch 服務中的多個計算節點上平行執行。</span><span class="sxs-lookup"><span data-stu-id="232df-151">The *python_tutorial_task.py* script runs in parallel on multiple compute nodes in the Batch service.</span></span>
* <span data-ttu-id="232df-152">**./data/taskdata\*.txt**︰這三個文字檔會對在計算節點上執行的工作提供輸入。</span><span class="sxs-lookup"><span data-stu-id="232df-152">**./data/taskdata\*.txt**: These three text files provide the input for the tasks that run on the compute nodes.</span></span>

<span data-ttu-id="232df-153">下圖說明用戶端和工作指令碼所執行的主要作業。</span><span class="sxs-lookup"><span data-stu-id="232df-153">The following diagram illustrates the primary operations that are performed by the client and task scripts.</span></span> <span data-ttu-id="232df-154">此基本工作流程通常由使用 Batch 建立的許多計算方案所組成。</span><span class="sxs-lookup"><span data-stu-id="232df-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="232df-155">雖然不會示範 Batch 服務中可用的每項功能，但幾乎每個 Batch 案例都包含此工作流程的某些部分。</span><span class="sxs-lookup"><span data-stu-id="232df-155">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="232df-156">![Batch 範例工作流程][8]</span><span class="sxs-lookup"><span data-stu-id="232df-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="232df-157">**步驟 1.**</span><span class="sxs-lookup"><span data-stu-id="232df-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="232df-158">在 Azure Blob 儲存體中建立**容器**。</span><span class="sxs-lookup"><span data-stu-id="232df-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="232df-159">
[**步驟 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="232df-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="232df-160">將工作指令碼和輸入檔案上傳至容器。</span><span class="sxs-lookup"><span data-stu-id="232df-160">Upload task script and input files to containers.</span></span><br/><span data-ttu-id="232df-161">
[**步驟 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="232df-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="232df-162">建立 Batch **集區**。</span><span class="sxs-lookup"><span data-stu-id="232df-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="232df-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="232df-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="232df-164">集區 **StartTask** 會在節點加入集區時將工作指令碼 (python_tutorial_task.py) 下載至這些節點。</span><span class="sxs-lookup"><span data-stu-id="232df-164">The pool **StartTask** downloads the task script (python_tutorial_task.py) to nodes as they join the pool.</span></span><br/><span data-ttu-id="232df-165">
[**步驟 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="232df-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="232df-166">建立 Batch **作業**。</span><span class="sxs-lookup"><span data-stu-id="232df-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="232df-167">
[**步驟 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="232df-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="232df-168">將 **工作** 加入至作業。</span><span class="sxs-lookup"><span data-stu-id="232df-168">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="232df-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="232df-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="232df-170">工作會排程在節點上執行。</span><span class="sxs-lookup"><span data-stu-id="232df-170">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="232df-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="232df-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="232df-172">每項工作會從 Azure 儲存體下載其輸入資料，然後開始執行。</span><span class="sxs-lookup"><span data-stu-id="232df-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="232df-173">
[**步驟 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="232df-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="232df-174">監視工作。</span><span class="sxs-lookup"><span data-stu-id="232df-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="232df-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="232df-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="232df-176">當工作完成時，它們會將其輸出資料上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="232df-176">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="232df-177">
[**步驟 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="232df-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="232df-178">從儲存體下載工作輸出。</span><span class="sxs-lookup"><span data-stu-id="232df-178">Download task output from Storage.</span></span>

<span data-ttu-id="232df-179">如上所述，並非每個 Batch 方案都會執行這些確切步驟，並且可能包含更多步驟，但此範例會示範在 Batch 方案中找到的一般程序。</span><span class="sxs-lookup"><span data-stu-id="232df-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="232df-180">準備用戶端指令碼</span><span class="sxs-lookup"><span data-stu-id="232df-180">Prepare client script</span></span>
<span data-ttu-id="232df-181">執行範例之前，將您的 Batch 和儲存體帳戶認證新增至 python_tutorial_client.py。</span><span class="sxs-lookup"><span data-stu-id="232df-181">Before you run the sample, add your Batch and Storage account credentials to *python_tutorial_client.py*.</span></span> <span data-ttu-id="232df-182">如果您尚未這麼做，請在您喜愛的編輯器中開啟此檔案，並使用您的認證更新下列程式碼行。</span><span class="sxs-lookup"><span data-stu-id="232df-182">If you have not done so already, open the file in your favorite editor and update the following lines with your credentials.</span></span>

```python
# Update the Batch and Storage account credential strings below with the values
# unique to your accounts. These are used when constructing connection strings
# for the Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="232df-183">您可以在 [Azure 入口網站][azure_portal]中每項服務的帳戶刀鋒視窗中尋找您的 Batch 和儲存體帳戶認證：</span><span class="sxs-lookup"><span data-stu-id="232df-183">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="232df-184">![入口網站中的 Batch 認證][9]
![入口網站中的儲存體認證][10]</span><span class="sxs-lookup"><span data-stu-id="232df-184">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="232df-185">在下列各節中，我們會分析指令碼用來處理 Batch 服務中工作負載的步驟。</span><span class="sxs-lookup"><span data-stu-id="232df-185">In the following sections, we analyze the steps used by the scripts to process a workload in the Batch service.</span></span> <span data-ttu-id="232df-186">鼓勵您在進行本文的其餘部分時，定期在編輯器中參考指令碼。</span><span class="sxs-lookup"><span data-stu-id="232df-186">We encourage you to refer regularly to the scripts in your editor while you work your way through the rest of the article.</span></span>

<span data-ttu-id="232df-187">瀏覽至 **python_tutorial_client.py** 中的下列一行以開始進行步驟 1：</span><span class="sxs-lookup"><span data-stu-id="232df-187">Navigate to the following line in **python_tutorial_client.py** to start with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="232df-188">步驟 1：建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="232df-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="232df-189">![在 Azure 儲存體中建立容器][1]
</span><span class="sxs-lookup"><span data-stu-id="232df-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="232df-190">Batch 包含與 Azure 儲存體進行互動的內建支援。</span><span class="sxs-lookup"><span data-stu-id="232df-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="232df-191">儲存體帳戶內的容器會提供在您的 Batch 帳戶中執行的工作所需的檔案。</span><span class="sxs-lookup"><span data-stu-id="232df-191">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="232df-192">容器也會提供一個位置來儲存工作所產生的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="232df-192">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="232df-193">python_tutorial_client.py 首先會在 [Azure Blob 儲存體](../storage/common/storage-introduction.md#blob-storage)中建立三個容器：</span><span class="sxs-lookup"><span data-stu-id="232df-193">The first thing the *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="232df-194">**應用程式**︰此容器會儲存工作所執行的 Python 指令碼 python_tutorial_task.py。</span><span class="sxs-lookup"><span data-stu-id="232df-194">**application**: This container will store the Python script run by the tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="232df-195">**輸入**：工作會從「輸入」容器下載所要處理的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="232df-195">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="232df-196">**輸出**：當工作完成輸入檔案的處理時，它們會將結果上傳至「輸出」容器。</span><span class="sxs-lookup"><span data-stu-id="232df-196">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="232df-197">為了與儲存體帳戶進行互動並建立容器，我們使用 [azure-storage][pypi_storage] 套件來建立 [BlockBlobService][py_blockblobservice] 物件 (Blob 用戶端)。</span><span class="sxs-lookup"><span data-stu-id="232df-197">In order to interact with a Storage account and create containers, we use the [azure-storage][pypi_storage] package to create a [BlockBlobService][py_blockblobservice] object--the "blob client."</span></span> <span data-ttu-id="232df-198">然後，我們使用 Blob 用戶端在儲存體帳戶中建立三個容器。</span><span class="sxs-lookup"><span data-stu-id="232df-198">We then create three containers in the Storage account using the blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create the blob client, for use in obtaining references to
# blob storage containers and uploading files to containers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use the blob client to create the containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="232df-199">建立容器之後，應用程式現在即可上傳工作所要使用的檔案。</span><span class="sxs-lookup"><span data-stu-id="232df-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="232df-200">[如何使用 Python 的 Azure Blob 儲存體](../storage/blobs/storage-python-how-to-use-blob-storage.md)提供使用 Azure 儲存體容器和 Blob 的概觀。</span><span class="sxs-lookup"><span data-stu-id="232df-200">[How to use Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="232df-201">當您開始使用 Batch 時，此概觀應在您的閱讀清單的頂端附近。</span><span class="sxs-lookup"><span data-stu-id="232df-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="232df-202">步驟 2：上傳工作指令碼和資料檔案</span><span class="sxs-lookup"><span data-stu-id="232df-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="232df-203">![將工作應用程式和輸入 (資料) 檔案上傳至容器][2]
</span><span class="sxs-lookup"><span data-stu-id="232df-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="232df-204">在檔案上傳作業中，python_tutorial_client.py 會先定義**應用程式**和**輸入**檔案路徑的集合 (因為其存在於本機電腦上)。</span><span class="sxs-lookup"><span data-stu-id="232df-204">In the file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="232df-205">然後將這些檔案上傳到在上一個步驟中建立的容器。</span><span class="sxs-lookup"><span data-stu-id="232df-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```python
# Paths to the task script. This script will be executed by the tasks that
# run on the compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# The collection of data files that are to be processed by the tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload the application script to Azure Storage. This is the script that
# will process the data files, and is executed by each of the tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload the data files. This is the data that will be processed by each of
# the tasks executed on the compute nodes in the pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="232df-206">使用清單理解功能，針對集合中的每個檔案呼叫 `upload_file_to_container` 函式並填入兩個 [ResourceFile][py_resource_file] 集合。</span><span class="sxs-lookup"><span data-stu-id="232df-206">Using list comprehension, the `upload_file_to_container` function is called for each file in the collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="232df-207">`upload_file_to_container` 函式會如下所示：</span><span class="sxs-lookup"><span data-stu-id="232df-207">The `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file to an Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: The name of the Azure Blob storage container.
    :param str file_path: The local path to the file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} to container [{}]...'.format(path,
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

### <a name="resourcefiles"></a><span data-ttu-id="232df-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="232df-208">ResourceFiles</span></span>
<span data-ttu-id="232df-209">[ResourceFile][py_resource_file] 提供 Batch 中的工作，以及 Azure 儲存體中會在工作執行前下載到計算節點之檔案的 URL。</span><span class="sxs-lookup"><span data-stu-id="232df-209">A [ResourceFile][py_resource_file] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="232df-210">[ResourceFile][py_resource_file].**blob_source** 屬性會指定 Azure 儲存體中現有檔案的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="232df-210">The [ResourceFile][py_resource_file].**blob_source** property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="232df-211">此 URL 也可能包含可供安全存取檔案的共用存取簽章 (SAS)。</span><span class="sxs-lookup"><span data-stu-id="232df-211">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="232df-212">Batch 中的大部分工作類型都包含 ResourceFiles  屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="232df-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="232df-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="232df-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="232df-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="232df-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="232df-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="232df-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="232df-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="232df-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="232df-217">此範例不會使用 JobPreparationTask 或 JobReleaseTask 工作類型，但您可以在 [在 Azure Batch 計算節點上執行作業準備和完成工作](batch-job-prep-release.md)中深入了解。</span><span class="sxs-lookup"><span data-stu-id="232df-217">This sample does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="232df-218">共用存取簽章 (SAS)</span><span class="sxs-lookup"><span data-stu-id="232df-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="232df-219">共用存取簽章是可供安全存取 Azure 儲存體中容器和 Blob 的字串。</span><span class="sxs-lookup"><span data-stu-id="232df-219">Shared access signatures are strings that provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="232df-220">python_tutorial_client.py 指令碼會使用 Blob 和容器共用存取簽章，並示範如何從儲存體服務取得這些共用存取簽章字串。</span><span class="sxs-lookup"><span data-stu-id="232df-220">The *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="232df-221">**Blob 共用存取簽章**：集區的 StartTask 會在從儲存體下載工作指令碼和輸入資料檔案時，使用 Blob 共用存取簽章 (請參閱下面 [步驟 3](#step-3-create-batch-pool) )。</span><span class="sxs-lookup"><span data-stu-id="232df-221">**Blob shared access signatures**: The pool's StartTask uses blob shared access signatures when it downloads the task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="232df-222">python_tutorial_client.py 中的 `upload_file_to_container` 函式包含可取得各 Blob 共用存取簽章的程式碼。</span><span class="sxs-lookup"><span data-stu-id="232df-222">The `upload_file_to_container` function in *python_tutorial_client.py* contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="232df-223">在儲存體模組中呼叫 [BlockBlobService.make_blob_url][py_make_blob_url] 即可完成。</span><span class="sxs-lookup"><span data-stu-id="232df-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in the Storage module.</span></span>
* <span data-ttu-id="232df-224">**容器共用存取簽章**：每個工作在計算節點上完成其工作時，便會將其輸出檔案上傳至 Azure 儲存體中的「輸出」容器。</span><span class="sxs-lookup"><span data-stu-id="232df-224">**Container shared access signature**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="232df-225">若要這樣做，python_tutorial_task.py 會使用容器共用存取簽章，其可提供容器的寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="232df-225">To do so, *python_tutorial_task.py* uses a container shared access signature that provides write access to the container.</span></span> <span data-ttu-id="232df-226">python_tutorial_client.py 中的 `get_container_sas_token` 函式會取得容器的共用存取簽章，然後該簽章會以命令列引數的形式傳遞至工作。</span><span class="sxs-lookup"><span data-stu-id="232df-226">The `get_container_sas_token` function in *python_tutorial_client.py* obtains the container's shared access signature, which is then passed as a command-line argument to the tasks.</span></span> <span data-ttu-id="232df-227">步驟 5 [將工作新增至作業](#step-5-add-tasks-to-job)討論容器 SAS 的使用方式。</span><span class="sxs-lookup"><span data-stu-id="232df-227">Step #5, [Add tasks to a job](#step-5-add-tasks-to-job), discusses the usage of the container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="232df-228">查看有關共用存取簽章的兩部分系列[第 1 部分：了解 SAS 模型](../storage/common/storage-dotnet-shared-access-signature-part-1.md)和[第 2 部分：建立和使用 SAS 與 Blob 服務](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)，進一步了解如何提供您儲存體帳戶中資料的安全存取。</span><span class="sxs-lookup"><span data-stu-id="232df-228">Check out the two-part series on shared access signatures, [Part 1: Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with the Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="232df-229">步驟 3：建立 Batch 集區</span><span class="sxs-lookup"><span data-stu-id="232df-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="232df-230">![建立 Batch 集區][3]
</span><span class="sxs-lookup"><span data-stu-id="232df-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="232df-231">Batch **集區** 是 Batch 執行作業工作所在的計算節點 (虛擬機器) 集合。</span><span class="sxs-lookup"><span data-stu-id="232df-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="232df-232">將工作指令碼和資料檔案上傳至儲存體帳戶之後，python_tutorial_client.py 會使用 Batch Python 模組開始與 Batch 服務互動。</span><span class="sxs-lookup"><span data-stu-id="232df-232">After it uploads the task script and data files to the Storage account, *python_tutorial_client.py* starts its interaction with the Batch service by using the Batch Python module.</span></span> <span data-ttu-id="232df-233">為了這麼做，會建立 [BatchServiceClient][py_batchserviceclient]：</span><span class="sxs-lookup"><span data-stu-id="232df-233">To do so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with the Batch
# service in addition to Storage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="232df-234">接著，呼叫 `create_pool`以在 Batch 帳戶中建立計算節點集區。</span><span class="sxs-lookup"><span data-stu-id="232df-234">Next, a pool of compute nodes is created in the Batch account with a call to `create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with the specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for the new pool.
    :param list resource_files: A collection of resource files for the pool's
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

    # Specify the commands for the pool's start task. The start task is run
    # on each node as it joins the pool, and when it's rebooted or re-imaged.
    # We use the start task to prep the node for running our task script.
    task_commands = [
        # Copy the python_tutorial_task.py script to the "shared" directory
        # that all tasks that run on the node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and the dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install the azure-storage module so that the task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get the node agent SKU and image reference for the virtual machine
    # configuration.
    # For more information about the virtual machine configuration, see:
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

<span data-ttu-id="232df-235">當您建立集區時，您會定義 [PoolAddParameter][py_pooladdparam] 以指定集區的數個屬性：</span><span class="sxs-lookup"><span data-stu-id="232df-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for the pool:</span></span>

* <span data-ttu-id="232df-236">集區的**識別碼** (id - 必要)</span><span class="sxs-lookup"><span data-stu-id="232df-236">**ID** of the pool (*id* - required)</span></span><p/><span data-ttu-id="232df-237">如同 Batch 中的大部分實體，新的集區必須具有 Batch 帳戶內的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="232df-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="232df-238">您的程式碼會使用其識別碼參考此集區，而這就是您在 Azure [入口網站][azure_portal]中識別集區的方式。</span><span class="sxs-lookup"><span data-stu-id="232df-238">Your code refers to this pool using its ID, and it's how you identify the pool in the Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="232df-239">**計算節點數目** (target_dedicated -必要)</span><span class="sxs-lookup"><span data-stu-id="232df-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="232df-240">會指定應在集區中部署多少 VM。</span><span class="sxs-lookup"><span data-stu-id="232df-240">This property specifies how many VMs should be deployed in the pool.</span></span> <span data-ttu-id="232df-241">請務必注意，所有的 Batch 帳戶都具有預設**配額**，以限制 Batch 帳戶中的**核心** (因而限制計算節點) 數目。</span><span class="sxs-lookup"><span data-stu-id="232df-241">It is important to note that all Batch accounts have a default **quota** that limits the number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="232df-242">您可在 [Azure Batch 服務的配額和限制](batch-quota-limit.md)中發現預設配額以及如何[增加配額](batch-quota-limit.md#increase-a-quota) (例如 Batch 帳戶中的核心數目上限) 的說明。</span><span class="sxs-lookup"><span data-stu-id="232df-242">You can find the default quotas and instructions on how to [increase a quota](batch-quota-limit.md#increase-a-quota) (such as the maximum number of cores in your Batch account) in [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="232df-243">如果您發現自問「為什麼我的集區不會觸達 X 個以上的節點？</span><span class="sxs-lookup"><span data-stu-id="232df-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="232df-244">」，此核心配額可能是原因。</span><span class="sxs-lookup"><span data-stu-id="232df-244">this core quota may be the cause.</span></span>
* <span data-ttu-id="232df-245">節點的**作業系統** (virtual_machine_configuration **或** cloud_service_configuration - 必要)</span><span class="sxs-lookup"><span data-stu-id="232df-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="232df-246">在 *python_tutorial_client.py*，我們會使用 [VirtualMachineConfiguration][py_vm_config] 建立 Linux 節點的集區。</span><span class="sxs-lookup"><span data-stu-id="232df-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="232df-247">`common.helpers` 中的 `select_latest_verified_vm_image_with_node_agent_sku` 函式可簡化 [Azure 虛擬機器 Marketplace][vm_marketplace] 映像的使用方式。</span><span class="sxs-lookup"><span data-stu-id="232df-247">The `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="232df-248">如需使用 Marketplace 映像的詳細資訊，請參閱 [在 Azure Batch 集區中佈建 Linux 計算節點](batch-linux-nodes.md) 。</span><span class="sxs-lookup"><span data-stu-id="232df-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="232df-249">**計算節點的大小** (*vm_size* - 必要)</span><span class="sxs-lookup"><span data-stu-id="232df-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="232df-250">因為我們要針對 [VirtualMachineConfiguration][py_vm_config] 指定 Linux 節點，所以我們會從 [Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)指定 VM 大小 (在此範例中為 `STANDARD_A1`)。</span><span class="sxs-lookup"><span data-stu-id="232df-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="232df-251">同樣地，如需詳細資訊，請參閱 [在 Azure Batch 集區中佈建 Linux 計算節點](batch-linux-nodes.md) 。</span><span class="sxs-lookup"><span data-stu-id="232df-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="232df-252">**啟動工作** (start_task - 非必要)</span><span class="sxs-lookup"><span data-stu-id="232df-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="232df-253">透過上述實體節點屬性，您也可以指定集區的 [StartTask][py_starttask] (非必要)。</span><span class="sxs-lookup"><span data-stu-id="232df-253">Along with the above physical node properties, you may also specify a [StartTask][py_starttask] for the pool (it is not required).</span></span> <span data-ttu-id="232df-254">StartTask 會在每個節點加入集區以及每次重新啟動節點時，於該節點上執行。</span><span class="sxs-lookup"><span data-stu-id="232df-254">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="232df-255">StartTask 特別適合用於準備計算節點，以便執行工作，例如安裝工作所要執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="232df-255">The StartTask is especially useful for preparing compute nodes for the execution of tasks, such as installing the applications that your tasks run.</span></span><p/><span data-ttu-id="232df-256">在此範例應用程式中，StartTask 會將它從儲存體下載的檔案 (使用 StartTask 的 **resource_files** 屬性所指定)，從 StartTask「工作目錄」複製到在節點上執行的所有工作可以存取的「共用」目錄。</span><span class="sxs-lookup"><span data-stu-id="232df-256">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the StartTask's **resource_files** property) from the StartTask *working directory* to the *shared* directory that all tasks running on the node can access.</span></span> <span data-ttu-id="232df-257">基本上，這會在節點加入集區時將 `python_tutorial_task.py` 複製到每個節點上的共用目錄，以便在節點上執行的任何工作都能存取它。</span><span class="sxs-lookup"><span data-stu-id="232df-257">Essentially, this copies `python_tutorial_task.py` to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

<span data-ttu-id="232df-258">您可能會注意到對 `wrap_commands_in_shell` 協助程式函式的呼叫。</span><span class="sxs-lookup"><span data-stu-id="232df-258">You may notice the call to the `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="232df-259">此函式會採用不同命令的集合，並針對工作的命令列屬性建立合適的單一命令列。</span><span class="sxs-lookup"><span data-stu-id="232df-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="232df-260">此外，在上述程式碼片段中值得注意的是在 StartTask 的 **command_line** 屬性中使用的兩個環境變數：`AZ_BATCH_TASK_WORKING_DIR` 和 `AZ_BATCH_NODE_SHARED_DIR`。</span><span class="sxs-lookup"><span data-stu-id="232df-260">Also notable in the code snippet above is the use of two environment variables in the **command_line** property of the StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="232df-261">Batch 集區中的每個計算節點都會自動以 Batch 特有的數個環境變數進行設定。</span><span class="sxs-lookup"><span data-stu-id="232df-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="232df-262">工作所執行的任何程序都可以存取這些環境變數。</span><span class="sxs-lookup"><span data-stu-id="232df-262">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="232df-263">若要深入了解 Batch 集區中計算節點上可用的環境變數，以及有關工作的工作目錄資訊，請參閱 [Azure Batch 功能概觀](batch-api-basics.md)中的**工作的環境設定**和**檔案和目錄**。</span><span class="sxs-lookup"><span data-stu-id="232df-263">To find out more about the environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in the [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="232df-264">步驟 4：建立 Batch 作業</span><span class="sxs-lookup"><span data-stu-id="232df-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="232df-265">![建立 Batch 作業][4]</span><span class="sxs-lookup"><span data-stu-id="232df-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="232df-266">Batch **作業** 是與計算節點集區相關聯的工作集合。</span><span class="sxs-lookup"><span data-stu-id="232df-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="232df-267">作業中的工作會在相關聯集區的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="232df-267">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="232df-268">您不僅可使用作業來組織及追蹤相關工作負載中的工作，也可以強加特定條件約束，例如作業 (並延伸至其工作) 的最大執行階段，以及相對於 Batch 帳戶中其他作業的作業優先順序。</span><span class="sxs-lookup"><span data-stu-id="232df-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) and job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="232df-269">不過，在此範例中，作業只與在步驟 3 建立的集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="232df-269">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="232df-270">不會設定任何其他屬性。</span><span class="sxs-lookup"><span data-stu-id="232df-270">No additional properties are configured.</span></span>

<span data-ttu-id="232df-271">所有 Batch 作業都會與特定集區相關聯。</span><span class="sxs-lookup"><span data-stu-id="232df-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="232df-272">此關聯表示會在哪些節點上執行作業的工作。</span><span class="sxs-lookup"><span data-stu-id="232df-272">This association indicates which nodes the job's tasks execute on.</span></span> <span data-ttu-id="232df-273">您可使用 [PoolInformation][py_poolinfo] 屬性來指定此集區，如下列程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="232df-273">You specify the pool by using the [PoolInformation][py_poolinfo] property, as shown in the code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with the specified ID, associated with the specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID for the job.
    :param str pool_id: The ID for the pool.
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

<span data-ttu-id="232df-274">現已建立一個作業，便會加入工作來進行工作。</span><span class="sxs-lookup"><span data-stu-id="232df-274">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="232df-275">步驟 5：將工作加入至作業</span><span class="sxs-lookup"><span data-stu-id="232df-275">Step 5: Add tasks to job</span></span>
<span data-ttu-id="232df-276">![將工作加入至作業][5]</span><span class="sxs-lookup"><span data-stu-id="232df-276">![Add tasks to job][5]</span></span><br/><span data-ttu-id="232df-277">
*(1) 工作已新增至作業，(2) 工作已排定在節點上執行，以及 (3) 工作會下載要處理的資料檔案*</span><span class="sxs-lookup"><span data-stu-id="232df-277">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="232df-278">Batch **工作** 是在計算節點上執行的個別工作單位。</span><span class="sxs-lookup"><span data-stu-id="232df-278">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="232df-279">工作有一個命令列，可執行您在該命令列中指定的指令碼或可執行檔。</span><span class="sxs-lookup"><span data-stu-id="232df-279">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="232df-280">若要實際進行工作，必須將工作加入至作業。</span><span class="sxs-lookup"><span data-stu-id="232df-280">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="232df-281">每個 [CloudTask][py_task] 都是透過命令列屬性以及工作在其命令列自動執行前下載至節點的 [ResourceFiles][py_resource_file] (如同集區的 StartTask) 進行設定。</span><span class="sxs-lookup"><span data-stu-id="232df-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="232df-282">在此範例中，每個工作只會處理一個檔案。</span><span class="sxs-lookup"><span data-stu-id="232df-282">In the sample, each task processes only one file.</span></span> <span data-ttu-id="232df-283">因此其 ResourceFiles 集合只包含單一元素。</span><span class="sxs-lookup"><span data-stu-id="232df-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in the collection to the specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID of the job to which to add the tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: The ID of an Azure Blob storage container to
    which the tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    the specified Azure Blob storage container.
    """

    print('Adding {} tasks to job [{}]...'.format(len(input_files), job_id))

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
> <span data-ttu-id="232df-284">當工作存取環境變數 (例如 `$AZ_BATCH_NODE_SHARED_DIR`) 或執行在節點的 `PATH` 中找不到的應用程式時，工作命令列必須明確地叫用 Shell，例如透過 `/bin/sh -c MyTaskApplication $MY_ENV_VAR`。</span><span class="sxs-lookup"><span data-stu-id="232df-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in the node's `PATH`, task command lines must invoke the shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="232df-285">如果您的工作在節點的 `PATH` 中執行應用程式且未參考任何環境變數，這就不是必要條件。</span><span class="sxs-lookup"><span data-stu-id="232df-285">This requirement is unnecessary if your tasks execute an application in the node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="232df-286">在上述程式碼片段中的 `for` 迴圈內，您可以看到已建構工作的命令列，其中有五個命令列引數傳遞至 python_tutorial_task.py：</span><span class="sxs-lookup"><span data-stu-id="232df-286">Within the `for` loop in the code snippet above, you can see that the command line for the task is constructed with five command-line arguments that are passed to *python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="232df-287">**filepath**：這是節點上現有檔案的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="232df-287">**filepath**: This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="232df-288">在上述步驟 2 的 `upload_file_to_container` 中建立 ResourceFile 物件時，檔案名稱會用於此屬性 (ResourceFile 建構函式中的 `file_path` 參數)。</span><span class="sxs-lookup"><span data-stu-id="232df-288">When the ResourceFile object in `upload_file_to_container` was created in Step 2 above, the file name was used for this property (the `file_path` parameter in the ResourceFile constructor).</span></span> <span data-ttu-id="232df-289">這表示可以在節點上與 python_tutorial_task.py 相同的目錄中找到檔案。</span><span class="sxs-lookup"><span data-stu-id="232df-289">This indicates that the file can be found in the same directory on the node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="232df-290">**numwords**：最前面 N 個單字應該寫入輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="232df-290">**numwords**: The top *N* words should be written to the output file.</span></span>
3. <span data-ttu-id="232df-291">**storageaccount**︰儲存體帳戶的名稱，其擁有工作輸出應上傳至的容器。</span><span class="sxs-lookup"><span data-stu-id="232df-291">**storageaccount**: The name of the Storage account that owns the container to which the task output should be uploaded.</span></span>
4. <span data-ttu-id="232df-292">**storagecontainer**︰輸出檔應上傳至的儲存體容器名稱。</span><span class="sxs-lookup"><span data-stu-id="232df-292">**storagecontainer**: The name of the Storage container to which the output files should be uploaded.</span></span>
5. <span data-ttu-id="232df-293">**sastoken**：共用存取簽章 (SAS)，可提供 Azure 儲存體中**輸出**容器的寫入存取權。</span><span class="sxs-lookup"><span data-stu-id="232df-293">**sastoken**: The shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="232df-294">Python_tutorial_task.py 指令碼會在建立其 BlockBlobService 參考時使用此共用存取簽章。</span><span class="sxs-lookup"><span data-stu-id="232df-294">The *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="232df-295">這可提供容器的寫入存取權，而不需要儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="232df-295">This provides write access to the container without requiring an access key for the storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create the blob client using the container's SAS token.
# This allows us to create a client that provides write
# access only to the container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="232df-296">步驟 6：監視工作</span><span class="sxs-lookup"><span data-stu-id="232df-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="232df-297">![監視工作][6]</span><span class="sxs-lookup"><span data-stu-id="232df-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="232df-298">
*指令碼 (1) 會監視工作的完成狀態，以及 (2) 將結果資料上傳至 Azure 儲存體的工作*</span><span class="sxs-lookup"><span data-stu-id="232df-298">
*The script (1) monitors the tasks for completion status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="232df-299">工作新增至作業時，會自動排入佇列及排程，以便在與作業相關聯的集區中的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="232df-299">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="232df-300">根據您指定的設定，Batch 會為您處理所有工作佇列、排程、重試和其他工作管理責任。</span><span class="sxs-lookup"><span data-stu-id="232df-300">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="232df-301">監視工作執行的方法有許多種。</span><span class="sxs-lookup"><span data-stu-id="232df-301">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="232df-302">python_tutorial_client.py 中的 `wait_for_tasks_to_complete` 函式會提供監視特定工作狀態的簡單範例，在此例中為[已完成][py_taskstate]狀態。</span><span class="sxs-lookup"><span data-stu-id="232df-302">The `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, the [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in the specified job reach the Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The id of the job whose tasks should be to monitored.
    :param timedelta timeout: The duration to wait for task completion. If all
    tasks in the specified job do not reach Completed state within this time
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

## <a name="step-7-download-task-output"></a><span data-ttu-id="232df-303">步驟 7：下載工作輸出</span><span class="sxs-lookup"><span data-stu-id="232df-303">Step 7: Download task output</span></span>
<span data-ttu-id="232df-304">![從儲存體下載工作輸出][7]</span><span class="sxs-lookup"><span data-stu-id="232df-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="232df-305">現已完成作業，可以從 Azure 儲存體下載工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="232df-305">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="232df-306">在 python_tutorial_client.py 中呼叫 `download_blobs_from_container` 即可完成此操作：</span><span class="sxs-lookup"><span data-stu-id="232df-306">This is done with a call to `download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from the specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: The Azure Blob storage container from which to
     download files.
    :param directory_path: The local directory to which to download the files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] to {}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="232df-307">在 python_tutorial_client.py 中呼叫 `download_blobs_from_container`可指定檔案應下載到您的主目錄。</span><span class="sxs-lookup"><span data-stu-id="232df-307">The call to `download_blobs_from_container` in *python_tutorial_client.py* specifies that the files should be downloaded to your home directory.</span></span> <span data-ttu-id="232df-308">您可隨意修改此輸出位置。</span><span class="sxs-lookup"><span data-stu-id="232df-308">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="232df-309">步驟 8：刪除容器</span><span class="sxs-lookup"><span data-stu-id="232df-309">Step 8: Delete containers</span></span>
<span data-ttu-id="232df-310">因為您需對位於 Azure 儲存體中的資料付費，所以建議您移除您的 Batch 作業不再需要的所有 Blob。</span><span class="sxs-lookup"><span data-stu-id="232df-310">Because you are charged for data that resides in Azure Storage, it is always a good idea to remove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="232df-311">在 python_tutorial_client.py 中，做法是對 [BlockBlobService.delete_container][py_delete_container] 進行三次呼叫：</span><span class="sxs-lookup"><span data-stu-id="232df-311">In *python_tutorial_client.py*, this is done with three calls to [BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="232df-312">步驟 9：刪除作業和集區</span><span class="sxs-lookup"><span data-stu-id="232df-312">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="232df-313">在最後一個步驟中，系統會提示您刪除 python_tutorial_client.py 指令碼所建立的作業和集區。</span><span class="sxs-lookup"><span data-stu-id="232df-313">In the final step, you are prompted to delete the job and the pool that were created by the *python_tutorial_client.py* script.</span></span> <span data-ttu-id="232df-314">雖然您不需支付作業和工作的費用，但您「需」  支付計算節點的費用。</span><span class="sxs-lookup"><span data-stu-id="232df-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="232df-315">因此，我們建議您只在必要時配置節點。</span><span class="sxs-lookup"><span data-stu-id="232df-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="232df-316">刪除未使用的集區可成為您維護程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="232df-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="232df-317">BatchServiceClient 的 [JobOperations][py_job] 和 [PoolOperations][py_pool] 兩者都有對應的刪除方法 (在您確認刪除時呼叫)：</span><span class="sxs-lookup"><span data-stu-id="232df-317">The BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if the user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="232df-318">請記住，您需支付計算資源的費用，而刪除未使用的集區會將成本降到最低。</span><span class="sxs-lookup"><span data-stu-id="232df-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="232df-319">另外請注意，刪除集區也會刪除該集區內的所有計算節點，而刪除集區後，將無法復原節點上的任何資料。</span><span class="sxs-lookup"><span data-stu-id="232df-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-sample-script"></a><span data-ttu-id="232df-320">執行範例指令碼</span><span class="sxs-lookup"><span data-stu-id="232df-320">Run the sample script</span></span>
<span data-ttu-id="232df-321">當您執行教學課程[程式碼範例][github_article_samples]中的 python_tutorial_client.py 指令碼時，主控台輸出大致如下。</span><span class="sxs-lookup"><span data-stu-id="232df-321">When you run the *python_tutorial_client.py* script from the tutorial [code sample][github_article_samples], the console output is similar to the following.</span></span> <span data-ttu-id="232df-322">在 `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` 會暫停執行，然而會建立、啟動集區的計算節點，以及執行集區的啟動工作中的命令。</span><span class="sxs-lookup"><span data-stu-id="232df-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while the pool's compute nodes are created, started, and the commands in the pool's start task are executed.</span></span> <span data-ttu-id="232df-323">在執行期間和之後，使用 [Azure 入口網站][azure_portal]來監視集區、計算節點、作業和工作。</span><span class="sxs-lookup"><span data-stu-id="232df-323">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="232df-324">使用 [Azure 入口網站][azure_portal]或 [Microsoft Azure 儲存體總管][storage_explorer]來檢視應用程式所建立的儲存體資源 (容器和 Blob)。</span><span class="sxs-lookup"><span data-stu-id="232df-324">Use the [Azure portal][azure_portal] or the [Microsoft Azure Storage Explorer][storage_explorer] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

> [!TIP]
> <span data-ttu-id="232df-325">從 `azure-batch-samples/Python/Batch/article_samples` 目錄內執行 *python_tutorial_client.py* 指令碼。</span><span class="sxs-lookup"><span data-stu-id="232df-325">Run the *python_tutorial_client.py* script from within the `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="232df-326">它會使用相對路徑來匯入 `common.helpers` 模組，因此如果您沒有從此目錄內執行指令碼，您可能會看到 `ImportError: No module named 'common'`。</span><span class="sxs-lookup"><span data-stu-id="232df-326">It uses a relative path for the `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run the script from within this directory.</span></span>
>
>

<span data-ttu-id="232df-327">以預設組態執行範例時，一般的執行時間 **大約 5-7 分鐘** 。</span><span class="sxs-lookup"><span data-stu-id="232df-327">Typical execution time is **approximately 5-7 minutes** when you run the sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py to container [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt to container [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks to job [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached the 'Completed' state within the specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] to /home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] to /home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] to /home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="232df-328">後續步驟</span><span class="sxs-lookup"><span data-stu-id="232df-328">Next steps</span></span>
<span data-ttu-id="232df-329">您可隨意變更 python_tutorial_client.py 和 python_tutorial_task.py，以試驗不同的計算案例。</span><span class="sxs-lookup"><span data-stu-id="232df-329">Feel free to make changes to *python_tutorial_client.py* and *python_tutorial_task.py* to experiment with different compute scenarios.</span></span> <span data-ttu-id="232df-330">例如，嘗試將執行延遲新增至 python_tutorial_task.py，以模擬長時間執行的工作並在入口網站中監視這些工作。</span><span class="sxs-lookup"><span data-stu-id="232df-330">For example, try adding an execution delay to *python_tutorial_task.py* to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="232df-331">嘗試新增更多工作，或調整計算節點的數目。</span><span class="sxs-lookup"><span data-stu-id="232df-331">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="232df-332">新增邏輯來檢查並允許使用現有的集區，以加速執行時間。</span><span class="sxs-lookup"><span data-stu-id="232df-332">Add logic to check for and allow the use of an existing pool to speed execution time.</span></span>

<span data-ttu-id="232df-333">既然您已熟悉 Batch 方案的基本工作流程，現在可以深入了解 Batch 服務的其他功能。</span><span class="sxs-lookup"><span data-stu-id="232df-333">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="232df-334">如果您不熟悉這項服務，我們建議檢閱 [Azure Batch 功能概觀](batch-api-basics.md) 一文。</span><span class="sxs-lookup"><span data-stu-id="232df-334">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="232df-335">從 [Batch 學習路徑][batch_learning_path]中的**深入開發**之下的其他 Batch 開發文章著手。</span><span class="sxs-lookup"><span data-stu-id="232df-335">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="232df-336">在 [TopNWords][github_topnwords] 範例中，查看利用 Batch 處理「前 N 個單字」工作負載的不同實作方式。</span><span class="sxs-lookup"><span data-stu-id="232df-336">Check out a different implementation of processing the "top N words" workload with Batch in the [TopNWords][github_topnwords] sample.</span></span>

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
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "將工作應用程式和輸入 (資料) 檔案上傳至容器"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "建立 Batch 集區"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "建立 Batch 作業"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "將工作新增至作業"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "監視工作"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "從儲存體下載工作輸出"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Batch 方案工作流程 (完整圖表)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "入口網站中的 Batch 認證"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "入口網站中的儲存體認證"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Batch 方案工作流程 (最小圖表)"
