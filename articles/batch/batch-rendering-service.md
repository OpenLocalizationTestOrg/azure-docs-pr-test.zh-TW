---
title: "aaaUse hello Azure 批次轉譯服務 toorender hello 定域機組中的 |Microsoft 文件"
description: "Azure 虛擬機器上的轉譯作業直接由 Maya 提供且按使用次數付費。"
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a><span data-ttu-id="a494e-103">Hello 轉譯批次服務快速入門</span><span class="sxs-lookup"><span data-stu-id="a494e-103">Get started with hello Batch Rendering service</span></span>

<span data-ttu-id="a494e-104">hello Azure 批次轉譯服務提供了雲端規模支付每次使用為基礎的轉譯能力。</span><span class="sxs-lookup"><span data-stu-id="a494e-104">hello Azure Batch Rendering service offers cloud-scale rendering capabilities on a pay-per-use basis.</span></span> <span data-ttu-id="a494e-105">hello 轉譯批次服務會處理工作排程和排入佇列、 管理失敗重試次數，以及適用於您的轉譯作業的自動調整。</span><span class="sxs-lookup"><span data-stu-id="a494e-105">hello Batch Rendering service handles job scheduling and queueing, managing failures and retries, and auto-scaling for your render job.</span></span> <span data-ttu-id="a494e-106">hello 轉譯批次服務支援 Autodesk 馬雅 3ds Max 和 Arnold，即將推出的其他應用程式的支援。</span><span class="sxs-lookup"><span data-stu-id="a494e-106">hello Batch Rendering service supports Autodesk Maya, 3ds Max, and Arnold, with support for other applications coming soon.</span></span> <span data-ttu-id="a494e-107">hello 馬雅 2017年外掛程式的批次可輕鬆 toostart 轉譯作業在 Azure 上直接從您的桌面。</span><span class="sxs-lookup"><span data-stu-id="a494e-107">hello Batch plug-in for Maya 2017 makes it easy toostart a rendering job on Azure right from your desktop.</span></span> 

## <a name="supported-applications"></a><span data-ttu-id="a494e-108">支援的應用程式</span><span class="sxs-lookup"><span data-stu-id="a494e-108">Supported applications</span></span>

<span data-ttu-id="a494e-109">hello 轉譯批次服務目前支援下列應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="a494e-109">hello Batch Rendering service currently supports hello following applications:</span></span>

- <span data-ttu-id="a494e-110">Autodesk Maya</span><span class="sxs-lookup"><span data-stu-id="a494e-110">Autodesk Maya</span></span>
- <span data-ttu-id="a494e-111">Autodesk 3ds Max</span><span class="sxs-lookup"><span data-stu-id="a494e-111">Autodesk 3ds Max</span></span>
- <span data-ttu-id="a494e-112">Autodesk Arnold</span><span class="sxs-lookup"><span data-stu-id="a494e-112">Autodesk Arnold</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a494e-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="a494e-113">Prerequisites</span></span>

<span data-ttu-id="a494e-114">toouse hello 轉譯批次服務，您需要：</span><span class="sxs-lookup"><span data-stu-id="a494e-114">toouse hello Batch Rendering service, you need:</span></span>

- <span data-ttu-id="a494e-115">[Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="a494e-115">An [Azure account](https://azure.microsoft.com/free/).</span></span> 
- <span data-ttu-id="a494e-116">**Azure Batch 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a494e-116">**An Azure Batch account.**</span></span> <span data-ttu-id="a494e-117">如需 hello Azure 入口網站中建立批次帳戶的指引，請參閱[的 hello Azure 入口網站來建立批次帳戶](batch-account-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a494e-117">For guidance on creating a Batch account in hello Azure portal, see [Create a Batch account with hello Azure portal](batch-account-create-portal.md).</span></span>
- <span data-ttu-id="a494e-118">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="a494e-118">**An Azure Storage account.**</span></span> <span data-ttu-id="a494e-119">Azure 儲存體中儲存 hello 資產用於轉譯工作。</span><span class="sxs-lookup"><span data-stu-id="a494e-119">hello assets used for your rendering job are stored in Azure Storage.</span></span> <span data-ttu-id="a494e-120">當您設定 Batch 帳戶時，可以自動建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a494e-120">You can create a storage account automatically when you set up your Batch account.</span></span> <span data-ttu-id="a494e-121">您也可以使用現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a494e-121">You can also use an existing storage account.</span></span> <span data-ttu-id="a494e-122">toolearn 進一步了解儲存體帳戶，請參閱[toocreate，如何管理或刪除 hello Azure 入口網站的儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-create-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="a494e-122">toolearn more about Storage accounts, see [How toocreate, manage, or delete a storage account in hello Azure portal](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

<span data-ttu-id="a494e-123">toouse hello 批次馬雅外掛程式，必須：</span><span class="sxs-lookup"><span data-stu-id="a494e-123">toouse hello Batch plug-in for Maya, you need:</span></span>

- <span data-ttu-id="a494e-124">**Maya 2017**</span><span class="sxs-lookup"><span data-stu-id="a494e-124">**Maya 2017**</span></span>
- <span data-ttu-id="a494e-125">**Arnold for Maya**</span><span class="sxs-lookup"><span data-stu-id="a494e-125">**Arnold for Maya**</span></span>

<span data-ttu-id="a494e-126">您也可以使用 hello [Azure 入口網站](https://portal.azure.com)toocreate 集區與馬雅 3ds 預先設定的虛擬機器的最大值和 Arnold。</span><span class="sxs-lookup"><span data-stu-id="a494e-126">You can also use hello [Azure portal](https://portal.azure.com) toocreate pools of virtual machines that are pre-configured with Maya, 3ds Max, and Arnold.</span></span> <span data-ttu-id="a494e-127">您可以使用 hello 入口 toomonitor 作業並下載應用程式記錄檔，並從遠端連線使用 RDP 或 SSH tooindividual Vm 診斷失敗的工作。</span><span class="sxs-lookup"><span data-stu-id="a494e-127">You can use hello portal toomonitor jobs and diagnose failed tasks by downloading application logs and by remotely connecting tooindividual VMs using RDP or SSH.</span></span>

## <a name="basic-batch-concepts"></a><span data-ttu-id="a494e-128">基本 Batch 概念</span><span class="sxs-lookup"><span data-stu-id="a494e-128">Basic Batch concepts</span></span>

<span data-ttu-id="a494e-129">在您開始使用 hello 轉譯批次服務之前，很有幫助 toobe 熟悉幾個批次概念，包括計算節點、 集區和工作。</span><span class="sxs-lookup"><span data-stu-id="a494e-129">Before you begin using hello Batch Rendering service, it's helpful toobe familiar with a few Batch concepts, including compute nodes, pools, and jobs.</span></span> <span data-ttu-id="a494e-130">Azure 批次的相關一般情況下，請參閱的 toolearn[與批次中執行本質平行的工作負載](batch-technical-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a494e-130">toolearn more about Azure Batch in general, see [Run intrinsically parallel workloads with Batch](batch-technical-overview.md).</span></span>

### <a name="pools"></a><span data-ttu-id="a494e-131">集區</span><span class="sxs-lookup"><span data-stu-id="a494e-131">Pools</span></span>

<span data-ttu-id="a494e-132">Batch 是一項平台服務，用於在**計算節點**的**集區**上執行計算密集工作 (例如轉譯)。</span><span class="sxs-lookup"><span data-stu-id="a494e-132">Batch is a platform service for running compute-intensive work, like rendering, on a **pool** of **compute nodes**.</span></span> <span data-ttu-id="a494e-133">集區中的每個計算節點不是執行 Linux 就是執行 Windows 的 Azure 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="a494e-133">Each compute node in a pool is an Azure virtual machine (VM) running either Linux or Windows.</span></span> 

<span data-ttu-id="a494e-134">如需有關批次集區和計算節點的詳細資訊，請參閱 hello[集區](batch-api-basics.md#pool)和[計算節點](batch-api-basics.md#compute-node)中[開發大規模的平行計算與批次的解決方案](batch-api-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="a494e-134">For more information about Batch pools and compute nodes, see hello [Pool](batch-api-basics.md#pool) and [Compute node](batch-api-basics.md#compute-node) sections in [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span></span>

### <a name="jobs"></a><span data-ttu-id="a494e-135">工作</span><span class="sxs-lookup"><span data-stu-id="a494e-135">Jobs</span></span>

<span data-ttu-id="a494e-136">批次**作業**是 hello 執行的工作集合中的計算節點集區。</span><span class="sxs-lookup"><span data-stu-id="a494e-136">A Batch **job** is a collection of tasks that run on hello compute nodes in a pool.</span></span> <span data-ttu-id="a494e-137">當您提交轉譯作業時，批次將 hello 工作分割成多個工作，並將散發 hello 工作 toohello hello 集區 toorun 中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="a494e-137">When you submit a rendering job, Batch divides hello job into tasks and distributes hello tasks toohello compute nodes in hello pool toorun.</span></span>

<span data-ttu-id="a494e-138">如需有關批次作業的詳細資訊，請參閱 hello[作業](batch-api-basics.md#job)一節中[開發大規模的平行計算與批次的解決方案](batch-api-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="a494e-138">For more information about Batch jobs, see hello [Job](batch-api-basics.md#job) section in [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span></span>

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a><span data-ttu-id="a494e-139">使用 hello plug-in for 馬雅 toosubmit 轉譯作業的批次</span><span class="sxs-lookup"><span data-stu-id="a494e-139">Use hello Batch plug-in for Maya toosubmit a render job</span></span>

<span data-ttu-id="a494e-140">以 hello 馬雅外掛程式的批次，您可以提交作業 toohello 直接從馬雅轉譯批次服務。</span><span class="sxs-lookup"><span data-stu-id="a494e-140">With hello Batch plug-in for Maya, you can submit a job toohello Batch Rendering service right from Maya.</span></span> <span data-ttu-id="a494e-141">hello 下列各節說明如何 tooconfigure hello 從 hello 外掛程式的工作，並提交。</span><span class="sxs-lookup"><span data-stu-id="a494e-141">hello following sections describe how tooconfigure hello job from hello plug-in and then submit it.</span></span> 

### <a name="load-hello-batch-plug-in-in-maya"></a><span data-ttu-id="a494e-142">載入 hello 批次中馬雅外掛程式</span><span class="sxs-lookup"><span data-stu-id="a494e-142">Load hello Batch plug-in in Maya</span></span>

<span data-ttu-id="a494e-143">hello 外掛程式的批次並用於[GitHub](https://github.com/Azure/azure-batch-maya/releases)。</span><span class="sxs-lookup"><span data-stu-id="a494e-143">hello Batch plug-in is available on [GitHub](https://github.com/Azure/azure-batch-maya/releases).</span></span> <span data-ttu-id="a494e-144">解壓縮您選擇的 hello 封存 tooa 目錄。</span><span class="sxs-lookup"><span data-stu-id="a494e-144">Unzip hello archive tooa directory of your choice.</span></span> <span data-ttu-id="a494e-145">您可以直接從 hello 載入外掛程式 hello *azure_batch_maya*目錄。</span><span class="sxs-lookup"><span data-stu-id="a494e-145">You can load hello plug-in directly from hello *azure_batch_maya* directory.</span></span>

<span data-ttu-id="a494e-146">tooload hello 馬雅外掛程式：</span><span class="sxs-lookup"><span data-stu-id="a494e-146">tooload hello plug-in in Maya:</span></span>

1. <span data-ttu-id="a494e-147">執行 Maya。</span><span class="sxs-lookup"><span data-stu-id="a494e-147">Run Maya.</span></span>
2. <span data-ttu-id="a494e-148">開啟 [視窗] > [設定/喜好設定] > [外掛程式管理員]。</span><span class="sxs-lookup"><span data-stu-id="a494e-148">Open **Window** > **Settings/Preferences** > **Plug-in Manager**.</span></span>
3. <span data-ttu-id="a494e-149">按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="a494e-149">Click **Browse**.</span></span>
4. <span data-ttu-id="a494e-150">瀏覽 tooand 選取*azure_batch_maya/plug-in/AzureBatch.py*。</span><span class="sxs-lookup"><span data-stu-id="a494e-150">Navigate tooand select *azure_batch_maya/plug-in/AzureBatch.py*.</span></span>

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a><span data-ttu-id="a494e-151">驗證存取 tooyour 批次和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a494e-151">Authenticate access tooyour Batch and Storage accounts</span></span>

<span data-ttu-id="a494e-152">toouse hello 外掛程式，您必須使用您的 Azure 批次和 Azure 儲存體帳戶金鑰 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="a494e-152">toouse hello plug-in, you need tooauthenticate using your Azure Batch and Azure Storage account keys.</span></span> <span data-ttu-id="a494e-153">tooretrieve 儲存帳戶金鑰：</span><span class="sxs-lookup"><span data-stu-id="a494e-153">tooretrieve your account keys:</span></span>

1. <span data-ttu-id="a494e-154">顯示 hello 馬雅外掛程式和選取 hello **Config**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a494e-154">Display hello plug-in in Maya, and select hello **Config** tab.</span></span>
2. <span data-ttu-id="a494e-155">瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a494e-155">Navigate toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="a494e-156">選取**批次帳戶**hello 左側功能表。</span><span class="sxs-lookup"><span data-stu-id="a494e-156">Select **Batch Accounts** from hello left-hand menu.</span></span> <span data-ttu-id="a494e-157">如有必要，按一下 [更多服務]並依照 [批次] 篩選。</span><span class="sxs-lookup"><span data-stu-id="a494e-157">If necessary, click **More Services** and filter on _Batch_.</span></span>
4. <span data-ttu-id="a494e-158">Hello 清單中，找出所需的 hello Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a494e-158">Locate hello desired Batch account in hello list.</span></span>
5. <span data-ttu-id="a494e-159">選取 hello**金鑰**功能表項目 toodisplay 您的帳戶名稱、 帳戶 URL 和存取金鑰：</span><span class="sxs-lookup"><span data-stu-id="a494e-159">Select hello **Keys** menu item toodisplay your account name, account URL, and access keys:</span></span>
    - <span data-ttu-id="a494e-160">Hello 批次帳戶 URL 貼入 hello**服務**hello 外掛程式的批次中的欄位。</span><span class="sxs-lookup"><span data-stu-id="a494e-160">Paste hello Batch account URL into hello **Service** field in hello Batch plug-in.</span></span>
    - <span data-ttu-id="a494e-161">貼上的 hello 帳戶名稱貼入 hello**批次帳戶**欄位。</span><span class="sxs-lookup"><span data-stu-id="a494e-161">Paste hello account name into hello **Batch Account** field.</span></span>
    - <span data-ttu-id="a494e-162">貼上的 hello 主要帳戶金鑰貼入 hello**批次金鑰**欄位。</span><span class="sxs-lookup"><span data-stu-id="a494e-162">Paste hello primary account key into hello **Batch Key** field.</span></span>
7. <span data-ttu-id="a494e-163">從 hello 左側功能表中選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a494e-163">Select Storage Accounts from hello left-hand menu.</span></span> <span data-ttu-id="a494e-164">如有必要，按一下 [更多服務]並依照 [儲存體] 篩選。</span><span class="sxs-lookup"><span data-stu-id="a494e-164">If necessary, click **More Services** and filter on _Storage_.</span></span>
8. <span data-ttu-id="a494e-165">Hello 清單中，找出 hello 需要儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a494e-165">Locate hello desired Storage account in hello list.</span></span>
9. <span data-ttu-id="a494e-166">選取 hello**便捷鍵**功能表項目 toodisplay hello 儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="a494e-166">Select hello **Access Keys** menu item toodisplay hello storage account name and keys.</span></span>
    - <span data-ttu-id="a494e-167">貼上的 hello 儲存體帳戶名稱貼入 hello**儲存體帳戶**hello 外掛程式的批次中的欄位。</span><span class="sxs-lookup"><span data-stu-id="a494e-167">Paste hello Storage account name into hello **Storage Account** field in hello Batch plug-in.</span></span>
    - <span data-ttu-id="a494e-168">貼上的 hello 主要帳戶金鑰貼入 hello**儲存體金鑰**欄位。</span><span class="sxs-lookup"><span data-stu-id="a494e-168">Paste hello primary account key into hello **Storage Key** field.</span></span>
10. <span data-ttu-id="a494e-169">按一下**驗證**hello 外掛程式的 tooensure 可以存取這兩個帳戶。</span><span class="sxs-lookup"><span data-stu-id="a494e-169">Click **Authenticate** tooensure that hello plug-in can access both accounts.</span></span>

<span data-ttu-id="a494e-170">一旦您已順利通過驗證，hello 外掛程式設定可太 hello 狀態欄位**驗證**:</span><span class="sxs-lookup"><span data-stu-id="a494e-170">Once you have successfully authenticated, hello plug-in sets hello status field too**Authenticated**:</span></span> 

![驗證 Batch 和儲存體帳戶](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a><span data-ttu-id="a494e-172">設定轉譯作業的集區</span><span class="sxs-lookup"><span data-stu-id="a494e-172">Configure a pool for a render job</span></span>

<span data-ttu-id="a494e-173">您已驗證 Batch 和儲存體帳戶之後，請針對您的轉譯作業設定集區。</span><span class="sxs-lookup"><span data-stu-id="a494e-173">After you have authenticated your Batch and Storage accounts, set up a pool for your rendering job.</span></span> <span data-ttu-id="a494e-174">hello 外掛程式會將儲存您的工作階段之間的選擇。</span><span class="sxs-lookup"><span data-stu-id="a494e-174">hello plug-in saves your selections between sessions.</span></span> <span data-ttu-id="a494e-175">設定慣用的組態之後, 您不需要 toomodify 它除非它會變更。</span><span class="sxs-lookup"><span data-stu-id="a494e-175">Once you've set up your preferred configuration, you won't need toomodify it unless it changes.</span></span>

<span data-ttu-id="a494e-176">hello 下列各節逐步引導您完成 hello 可用的選項，用於 hello**送出** 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="a494e-176">hello following sections walk you through hello available options, available on hello **Submit** tab:</span></span>

#### <a name="specify-a-new-or-existing-pool"></a><span data-ttu-id="a494e-177">指定新的或現有集區</span><span class="sxs-lookup"><span data-stu-id="a494e-177">Specify a new or existing pool</span></span>

<span data-ttu-id="a494e-178">由 toorun hello render 作業，選取 hello 集 toospecify**送出** 索引標籤。此索引標籤會提供建立集區或選取現有集區的選項：</span><span class="sxs-lookup"><span data-stu-id="a494e-178">toospecify a pool on which toorun hello render job, select hello **Submit** tab. This tab offers options for creating a pool or selecting an existing pool:</span></span>

- <span data-ttu-id="a494e-179">您可以**自動佈建這項作業的集區**(hello 預設選項)。</span><span class="sxs-lookup"><span data-stu-id="a494e-179">You can **auto provision a pool for this job** (hello default option).</span></span> <span data-ttu-id="a494e-180">當您選擇此選項時，批次建立 hello 集區專用的 hello 目前的工作，並會自動刪除 hello 集區時 hello 轉譯工作已完成。</span><span class="sxs-lookup"><span data-stu-id="a494e-180">When you choose this option, Batch creates hello pool exclusively for hello current job, and automatically deletes hello pool when hello render job is complete.</span></span> <span data-ttu-id="a494e-181">當您有單一的轉譯作業 toocomplete 時，這個選項最適合。</span><span class="sxs-lookup"><span data-stu-id="a494e-181">This option is best when you have a single render job toocomplete.</span></span>
- <span data-ttu-id="a494e-182">您可以**重複使用現有的永續性集區**。</span><span class="sxs-lookup"><span data-stu-id="a494e-182">You can **reuse an existing persistent pool**.</span></span> <span data-ttu-id="a494e-183">如果您有現有的集區處於閒置狀態時，您可以指定該集區執行 hello render 作業從 hello 下拉式清單中選取它。</span><span class="sxs-lookup"><span data-stu-id="a494e-183">If you have an existing pool that is idle, you can specify that pool for running hello render job by selecting it from hello dropdown.</span></span> <span data-ttu-id="a494e-184">重複使用現有的持續性資料庫可節省 hello 所需時間 tooprovision hello 集區。</span><span class="sxs-lookup"><span data-stu-id="a494e-184">Reusing an existing persistent pool saves hello time required tooprovision hello pool.</span></span>  
- <span data-ttu-id="a494e-185">您可以**建立新的永續性集區**。</span><span class="sxs-lookup"><span data-stu-id="a494e-185">You can **create a new persistent pool**.</span></span> <span data-ttu-id="a494e-186">選擇此選項會建立新的集區執行 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="a494e-186">Choosing this option creates a new pool for running hello job.</span></span> <span data-ttu-id="a494e-187">它不會刪除 hello 集區 hello 工作完成時，以便您可以在未來作業重複使用。</span><span class="sxs-lookup"><span data-stu-id="a494e-187">It does not delete hello pool when hello job is complete, so that you can reuse it for future jobs.</span></span> <span data-ttu-id="a494e-188">當您有連續需要 toorun 轉譯作業時，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="a494e-188">Select this option when you have a continuous need toorun render jobs.</span></span> <span data-ttu-id="a494e-189">在後續的工作，您可以選取**重複使用現有的持續性集區**toouse hello hello 第一份工作所建立的永續性集區。</span><span class="sxs-lookup"><span data-stu-id="a494e-189">On subsequent jobs, you can select **reuse an existing persistent pool** toouse hello persistent pool that you created for hello first job.</span></span>

![指定集區、OS 映像、VM 大小和授權](./media/batch-rendering-service/submit.png)

<span data-ttu-id="a494e-191">如需有關如何產生費用 Azure Vm 的詳細資訊，請參閱 hello [Linux 價格常見問題集](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq)和[Windows 價格常見問題集](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq)。</span><span class="sxs-lookup"><span data-stu-id="a494e-191">For more information on how charges accrue for Azure VMs, see hello [Linux Pricing FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) and [Windows Pricing FAQ](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).</span></span>

#### <a name="specify-hello-os-image-tooprovision"></a><span data-ttu-id="a494e-192">指定 hello OS 映像 tooprovision</span><span class="sxs-lookup"><span data-stu-id="a494e-192">Specify hello OS image tooprovision</span></span>

<span data-ttu-id="a494e-193">您可以指定在 hello 的 hello 集區中的 hello 類型的作業系統映像 toouse tooprovision 運算節點**Env** (Environment) 索引標籤。批次目前支援下列轉譯作業的映像選項 hello:</span><span class="sxs-lookup"><span data-stu-id="a494e-193">You can specify hello type of OS image toouse tooprovision compute nodes in hello pool on hello **Env** (Environment) tab. Batch currently supports hello following image options for rendering jobs:</span></span>

|<span data-ttu-id="a494e-194">作業系統</span><span class="sxs-lookup"><span data-stu-id="a494e-194">Operating System</span></span>  |<span data-ttu-id="a494e-195">映像</span><span class="sxs-lookup"><span data-stu-id="a494e-195">Image</span></span>  |
|---------|---------|
|<span data-ttu-id="a494e-196">Linux</span><span class="sxs-lookup"><span data-stu-id="a494e-196">Linux</span></span>     |<span data-ttu-id="a494e-197">Batch CentOS 預覽</span><span class="sxs-lookup"><span data-stu-id="a494e-197">Batch CentOS Preview</span></span> |
|<span data-ttu-id="a494e-198">Windows</span><span class="sxs-lookup"><span data-stu-id="a494e-198">Windows</span></span>     |<span data-ttu-id="a494e-199">Batch Windows 預覽</span><span class="sxs-lookup"><span data-stu-id="a494e-199">Batch Windows Preview</span></span> |

#### <a name="choose-a-vm-size"></a><span data-ttu-id="a494e-200">選擇 VM 大小</span><span class="sxs-lookup"><span data-stu-id="a494e-200">Choose a VM size</span></span>

<span data-ttu-id="a494e-201">您可以指定 hello VM 大小上 hello **Env**  索引標籤。如需可用 VM 大小的詳細資訊，請參閱 [Azure 中的 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes)和 [Azure 中的 Windows VM 大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)。</span><span class="sxs-lookup"><span data-stu-id="a494e-201">You can specify hello VM size on hello **Env** tab. For more information about available VM sizes, see [Linux VM sizes in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) and [Windows VM sizes in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).</span></span> 

![Hello Env 索引標籤上指定 hello VM OS 映像和大小](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a><span data-ttu-id="a494e-203">指定授權選項</span><span class="sxs-lookup"><span data-stu-id="a494e-203">Specify licensing options</span></span>

<span data-ttu-id="a494e-204">您可以指定要在 hello toouse hello 授權**Env**  索引標籤。選項包括：</span><span class="sxs-lookup"><span data-stu-id="a494e-204">You can specify hello licenses you wish toouse on hello **Env** tab. Options include:</span></span>

- <span data-ttu-id="a494e-205">**Maya**，預設會啟用。</span><span class="sxs-lookup"><span data-stu-id="a494e-205">**Maya**, which is enabled by default.</span></span>
- <span data-ttu-id="a494e-206">**Arnold**，如果 Arnold 馬雅中的 hello 作用中的轉譯引擎偵測到啟用的。</span><span class="sxs-lookup"><span data-stu-id="a494e-206">**Arnold**, which is enabled if Arnold is detected as hello active render engine in Maya.</span></span>

 <span data-ttu-id="a494e-207">如果您想 toorender 使用自己的授權，您可以藉由新增 hello 適當的環境變數 toohello 資料表設定您授權的結束點。</span><span class="sxs-lookup"><span data-stu-id="a494e-207">If you wish toorender using your own license, you can configure your license end point by adding hello appropriate environment variables toohello table.</span></span> <span data-ttu-id="a494e-208">如果您這樣做，會確定 toodeselect hello 預設授權選項。</span><span class="sxs-lookup"><span data-stu-id="a494e-208">Be sure toodeselect hello default licensing options if you do so.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a494e-209">您所要支付 hello 授權的使用時 Vm 會 hello 集區中執行，即使 hello Vm 不目前正在使用的轉譯。</span><span class="sxs-lookup"><span data-stu-id="a494e-209">You are billed for use of hello licenses while VMs are running in hello pool, even if hello VMs are not currently being used for rendering.</span></span> <span data-ttu-id="a494e-210">tooavoid 額外費用，瀏覽 toohello**集區**索引標籤，然後調整大小 hello 集區 too0 節點直到您準備好 toorun 其他轉譯工作。</span><span class="sxs-lookup"><span data-stu-id="a494e-210">tooavoid extra charges, navigate toohello **Pools** tab and resize hello pool too0 nodes until you are ready toorun another render job.</span></span> 
>
>

#### <a name="manage-persistent-pools"></a><span data-ttu-id="a494e-211">管理永續性集區</span><span class="sxs-lookup"><span data-stu-id="a494e-211">Manage persistent pools</span></span>

<span data-ttu-id="a494e-212">您可以管理現有的持續性集區上 hello**集區** 索引標籤。從 hello 清單中選取集區會顯示 hello hello 集區的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="a494e-212">You can manage an existing persistent pool on hello **Pools** tab. Selecting a pool from hello list displays hello current state of hello pool.</span></span>

<span data-ttu-id="a494e-213">從 hello**集區**索引標籤上，您也可以刪除 hello 集區，並調整 hello hello 集區中的 Vm 數目。</span><span class="sxs-lookup"><span data-stu-id="a494e-213">From hello **Pools** tab, you can also delete hello pool and resize hello number of VMs in hello pool.</span></span> <span data-ttu-id="a494e-214">您可以調整支出成本之間的工作負載集區 too0 節點 tooavoid。</span><span class="sxs-lookup"><span data-stu-id="a494e-214">You can resize a pool too0 nodes tooavoid incurring costs in between workloads.</span></span>

![檢視、調整大小和刪除集區](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a><span data-ttu-id="a494e-216">設定轉譯作業以便提交</span><span class="sxs-lookup"><span data-stu-id="a494e-216">Configure a render job for submission</span></span>

<span data-ttu-id="a494e-217">一旦您已經指定要執行 hello render 作業 hello 集區的 hello 參數，設定 hello 工作本身。</span><span class="sxs-lookup"><span data-stu-id="a494e-217">Once you have specified hello parameters for hello pool that will run hello render job, configure hello job itself.</span></span> 

#### <a name="specify-scene-parameters"></a><span data-ttu-id="a494e-218">指定場景參數</span><span class="sxs-lookup"><span data-stu-id="a494e-218">Specify scene parameters</span></span>

<span data-ttu-id="a494e-219">hello 外掛程式的批次中馬雅偵測到您目前使用的轉譯引擎，並顯示 hello 適當呈現 hello 上的設定**送出** 索引標籤。這些設定包括 hello 開始框架、 結束框架、 輸出前置詞和框架的步驟。</span><span class="sxs-lookup"><span data-stu-id="a494e-219">hello Batch plug-in detects which rendering engine you're currently using in Maya, and displays hello appropriate render settings on hello **Submit** tab. These settings include hello start frame, end frame, output prefix, and frame step.</span></span> <span data-ttu-id="a494e-220">您可以在 hello 外掛程式中指定不同的設定，以覆寫 hello 場景檔案轉譯設定。</span><span class="sxs-lookup"><span data-stu-id="a494e-220">You can override hello scene file render settings by specifying different settings in hello plug-in.</span></span> <span data-ttu-id="a494e-221">變更 toohello 外掛程式設定不保存後 toohello 場景檔案轉譯設定，因此您可以變更工作的工作為基礎而不需要 tooreupload hello 場景檔案。</span><span class="sxs-lookup"><span data-stu-id="a494e-221">Changes you make toohello plug-in settings are not persisted back toohello scene file render settings, so you can make changes on a job-by-job basis without needing tooreupload hello scene file.</span></span>

<span data-ttu-id="a494e-222">hello 外掛程式會警告您如果 hello 呈現您選取在馬雅引擎不支援。</span><span class="sxs-lookup"><span data-stu-id="a494e-222">hello plug-in warns you if hello render engine that you selected in Maya is not supported.</span></span>

<span data-ttu-id="a494e-223">如果開啟 hello 外掛程式時，您就會載入新的場景，按一下 hello**重新整理**按鈕 toomake 確定 hello 設定會更新。</span><span class="sxs-lookup"><span data-stu-id="a494e-223">If you load a new scene while hello plug-in is open, click hello **Refresh** button toomake sure hello settings are updated.</span></span>

#### <a name="resolve-asset-paths"></a><span data-ttu-id="a494e-224">解析資產路徑</span><span class="sxs-lookup"><span data-stu-id="a494e-224">Resolve asset paths</span></span>

<span data-ttu-id="a494e-225">當您載入 hello 外掛程式時，它會掃描 hello 場景檔案的任何外部檔案參考。</span><span class="sxs-lookup"><span data-stu-id="a494e-225">When you load hello plug-in, it scans hello scene file for any external file references.</span></span> <span data-ttu-id="a494e-226">這些參考會顯示在 [hello**資產**] 索引標籤。如果無法解析參考的路徑，hello 外掛程式嘗試 toolocate hello 檔案，在少數的預設位置，包括：</span><span class="sxs-lookup"><span data-stu-id="a494e-226">These references are displayed in hello **Assets** tab. If a referenced path cannot be resolved, hello plug-in attempts toolocate hello file in a few default locations, including:</span></span>

- <span data-ttu-id="a494e-227">hello hello 場景檔案位置</span><span class="sxs-lookup"><span data-stu-id="a494e-227">hello location of hello scene file</span></span> 
- <span data-ttu-id="a494e-228">hello 目前專案的_sourceimages_目錄</span><span class="sxs-lookup"><span data-stu-id="a494e-228">hello current project's _sourceimages_ directory</span></span>
- <span data-ttu-id="a494e-229">hello 目前工作目錄。</span><span class="sxs-lookup"><span data-stu-id="a494e-229">hello current working directory.</span></span> 

<span data-ttu-id="a494e-230">如果 hello 資產仍然找不到，它會列出警告圖示：</span><span class="sxs-lookup"><span data-stu-id="a494e-230">If hello asset still cannot be located, it is listed with a warning icon:</span></span>

![遺失的資產會顯示警告圖示](./media/batch-rendering-service/missing_assets.png)

<span data-ttu-id="a494e-232">如果您知道 hello 的無法解析的檔案參考的位置，您可以按一下 hello 警告圖示 toobe 提示 tooadd 搜尋路徑。</span><span class="sxs-lookup"><span data-stu-id="a494e-232">If you know hello location of an unresolved file reference, you can click hello warning icon toobe prompted tooadd a search path.</span></span> <span data-ttu-id="a494e-233">hello 然後外掛程式會使用此搜尋路徑 tooattempt tooresolve 任何遺失的資產。</span><span class="sxs-lookup"><span data-stu-id="a494e-233">hello plug-in then uses this search path tooattempt tooresolve any missing assets.</span></span> <span data-ttu-id="a494e-234">您可以新增任意數目的其他搜尋路徑。</span><span class="sxs-lookup"><span data-stu-id="a494e-234">You can add any number of additional search paths.</span></span>

<span data-ttu-id="a494e-235">解析參考時，它會以綠燈圖示列示：</span><span class="sxs-lookup"><span data-stu-id="a494e-235">When a reference is resolved, it is listed with a green light icon:</span></span>

![解析的資產會顯示綠燈圖示](./media/batch-rendering-service/found_assets.png)

<span data-ttu-id="a494e-237">如果您場景需要其他檔案該外掛程式的 hello 未偵測到，您可以加入其他檔案或目錄。</span><span class="sxs-lookup"><span data-stu-id="a494e-237">If your scene requires other files that hello plug-in has not detected, you can add additional files or directories.</span></span> <span data-ttu-id="a494e-238">使用 hello**加入檔案**和**新增目錄**按鈕。</span><span class="sxs-lookup"><span data-stu-id="a494e-238">Use hello **Add Files** and **Add Directory** buttons.</span></span> <span data-ttu-id="a494e-239">如果開啟 hello 外掛程式時，您就會載入新的場景，是確定 tooclick**重新整理**tooupdate hello 場景的參考。</span><span class="sxs-lookup"><span data-stu-id="a494e-239">If you load a new scene while hello plug-in is open, be sure tooclick **Refresh** tooupdate hello scene's references.</span></span>

#### <a name="upload-assets-tooan-asset-project"></a><span data-ttu-id="a494e-240">上傳資產 tooan 資產專案</span><span class="sxs-lookup"><span data-stu-id="a494e-240">Upload assets tooan asset project</span></span>

<span data-ttu-id="a494e-241">當您提交 render 作業 hello 所參考的檔案顯示在 [hello**資產**] 索引標籤會自動上傳的 tooAzure 為資產專案的儲存體。</span><span class="sxs-lookup"><span data-stu-id="a494e-241">When you submit a render job, hello referenced files displayed in hello **Assets** tab are automatically uploaded tooAzure Storage as an asset project.</span></span> <span data-ttu-id="a494e-242">您也可以上傳 hello 與轉譯作業無關的資產檔案使用 hello**上傳**按鈕 hello**資產** 索引標籤 hello 資產專案的名稱指定在 hello**專案**欄位，預設為 hello 目前馬雅專案之後。</span><span class="sxs-lookup"><span data-stu-id="a494e-242">You can also upload hello asset files independently of a render job, using hello **Upload** button on hello **Assets** tab. hello asset project name is specified in hello **Project** field and is named after hello current Maya project by default.</span></span> <span data-ttu-id="a494e-243">如果資產檔案上傳時，會保留 hello 本機檔案結構。</span><span class="sxs-lookup"><span data-stu-id="a494e-243">When asset files are uploaded, hello local file structure is preserved.</span></span> 

<span data-ttu-id="a494e-244">一旦上傳，資產即可由任意數量的轉譯作業參考。</span><span class="sxs-lookup"><span data-stu-id="a494e-244">Once uploaded, assets can be referenced by any number of render jobs.</span></span> <span data-ttu-id="a494e-245">所有上傳的資產是可用 tooany 作業參考 hello 資產的專案，不論是否包含在 hello 場景。</span><span class="sxs-lookup"><span data-stu-id="a494e-245">All uploaded assets are available tooany job that references hello asset project, whether or not they are included in hello scene.</span></span> <span data-ttu-id="a494e-246">toochange hello 資產專案參考的下一個工作，變更 hello 名稱在 hello**專案**欄位 hello**資產** 索引標籤。如果您想從上傳 tooexclude 的參照的檔案時，取消選取這些電腦使用 hello 清單旁邊的綠色 hello 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a494e-246">toochange hello asset project referenced by your next job, change hello name in hello **Project** field in hello **Assets** tab. If there are referenced files that you wish tooexclude from uploading, unselect them using hello green button beside hello listing.</span></span>

#### <a name="submit-and-monitor-hello-render-job"></a><span data-ttu-id="a494e-247">提交和監視 hello 轉譯作業</span><span class="sxs-lookup"><span data-stu-id="a494e-247">Submit and monitor hello render job</span></span>

<span data-ttu-id="a494e-248">Hello 呈現工作設定在 hello 外掛程式之後，按一下 hello**提交作業**按鈕 hello**送出**toosubmit hello 作業 tooBatch 索引標籤上：</span><span class="sxs-lookup"><span data-stu-id="a494e-248">After you have configured hello render job in hello plug-in, click hello **Submit Job** button on hello **Submit** tab toosubmit hello job tooBatch:</span></span>

![送出 hello render 作業](./media/batch-rendering-service/submit_job.png)

<span data-ttu-id="a494e-250">您可以監視正在從 hello 進行作業**作業**hello 外掛程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="a494e-250">You can monitor a job that is in progress from hello **Jobs** tab on hello plug-in.</span></span> <span data-ttu-id="a494e-251">Hello 清單 toodisplay hello 目前作業的狀態 hello 從選取的作業。</span><span class="sxs-lookup"><span data-stu-id="a494e-251">Select a job from hello list toodisplay hello current state of hello job.</span></span> <span data-ttu-id="a494e-252">您也可以使用此索引標籤 toocancel 和刪除作業，以及 toodownload hello 輸出和呈現記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a494e-252">You can also use this tab toocancel and delete jobs, as well as toodownload hello outputs and rendering logs.</span></span> 

<span data-ttu-id="a494e-253">toodownload 輸出修改 hello**輸出**欄位 tooset hello 所需的目的地目錄。</span><span class="sxs-lookup"><span data-stu-id="a494e-253">toodownload outputs, modify hello **Outputs** field tooset hello desired destination directory.</span></span> <span data-ttu-id="a494e-254">按一下 hello 齒輪圖示 toostart 監看 hello 作業並下載輸出進展的背景處理序：</span><span class="sxs-lookup"><span data-stu-id="a494e-254">Click hello gear icon toostart a background process that watches hello job and downloads outputs as it progresses:</span></span> 

![檢視作業狀態並下載輸出](./media/batch-rendering-service/jobs.png)

<span data-ttu-id="a494e-256">您可以關閉馬雅而不會中斷 hello 下載程序。</span><span class="sxs-lookup"><span data-stu-id="a494e-256">You can close Maya without disrupting hello download process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a494e-257">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a494e-257">Next steps</span></span>

<span data-ttu-id="a494e-258">toolearn 進一步了解批次，請參閱[與批次中執行本質平行的工作負載](batch-technical-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a494e-258">toolearn more about Batch, see [Run intrinsically parallel workloads with Batch](batch-technical-overview.md).</span></span>
