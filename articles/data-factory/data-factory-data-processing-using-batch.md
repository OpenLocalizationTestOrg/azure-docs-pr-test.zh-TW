---
title: "aaaProcess 大型資料集使用 Data Factory 和批次 |Microsoft 文件"
description: "描述如何 tooprocess 大量的 Azure Data Factory 中的資料管線所使用的 Azure 批次的平行處理功能。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="ee7db-103">使用 Data Factory 和 Batch 處理大型資料集</span><span class="sxs-lookup"><span data-stu-id="ee7db-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="ee7db-104">本文說明範例解決方案的架構，此解決方案能以自動且排程的方式移動和處理大型資料集。</span><span class="sxs-lookup"><span data-stu-id="ee7db-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="ee7db-105">它也提供使用 Azure Data Factory 和 Azure 批次的端對端逐步解說 tooimplement hello 方案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="ee7db-106">這篇文章比我們的一般文章還長，因為它包含整個範例解決方案的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="ee7db-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="ee7db-107">如果您是新 tooBatch 及資料 Factory，您可以了解這些服務，它們共同運作的方式。</span><span class="sxs-lookup"><span data-stu-id="ee7db-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="ee7db-108">如果您知道 hello 服務的相關項目，會設計/架構解決方案，您可以專注於 hello 只[架構 > 一節](#architecture-of-sample-solution)的 hello 發行項，如果您正在開發原型或方案，您可能也想 tootry逐步解說中 hello[逐步解說](#implementation-of-sample-solution)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="ee7db-109">歡迎您對此內容以及您如何使用它提出看法。</span><span class="sxs-lookup"><span data-stu-id="ee7db-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="ee7db-110">首先，讓我們看看如何協助 Data Factory 和批次服務處理 hello 雲端中的大型資料集。</span><span class="sxs-lookup"><span data-stu-id="ee7db-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="ee7db-111">為何使用 Azure Batch？</span><span class="sxs-lookup"><span data-stu-id="ee7db-111">Why Azure Batch?</span></span>
<span data-ttu-id="ee7db-112">Azure 批次，可讓您有效率地在 hello 雲端中的 toorun 大規模平行和高效能運算 (HPC) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ee7db-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="ee7db-113">這是排程需要大量計算工作 toorun managed 集合上的虛擬機器的平台服務，可以自動調整計算資源 toomeet hello 需求的工作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="ee7db-114">以 hello 批次服務，您定義 Azure 計算資源 tooexecute 應用程式以平行方式，而是在標尺。</span><span class="sxs-lookup"><span data-stu-id="ee7db-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="ee7db-115">您可以依需求或排程執行作業，而不需要 toomanually 建立、 設定和管理 HPC 叢集、 個別的虛擬機器、 虛擬網路或複雜的工作和工作排程基礎結構。</span><span class="sxs-lookup"><span data-stu-id="ee7db-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="ee7db-116">請參閱下列文章，如果您不熟悉 Azure 批次因為它有助於了解 hello 架構/hello 方案實作本文所述的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="ee7db-117">Azure Batch 的基本概念</span><span class="sxs-lookup"><span data-stu-id="ee7db-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="ee7db-118">Batch 功能概觀</span><span class="sxs-lookup"><span data-stu-id="ee7db-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="ee7db-119">（選擇性） toolearn 進一步了解 Azure 批次，請參閱 hello [Azure 批次學習路徑](https://azure.microsoft.com/documentation/learning-paths/batch/)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="ee7db-120">為何使用 Azure Data Factory？</span><span class="sxs-lookup"><span data-stu-id="ee7db-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="ee7db-121">Data Factory 是以雲端為基礎的資料整合服務會協調及自動 hello 移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="ee7db-122">使用 hello Data Factory 服務，您可以建立將資料從內部部署和雲端資料儲存區 tooa 集中的資料存放區的 managed 的資料管線 (例如： Azure Blob 儲存體)，和處理程序轉換資料，使用 Azure HDInsight 等 Azure 服務機器學習。</span><span class="sxs-lookup"><span data-stu-id="ee7db-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="ee7db-123">您也可以排程已排程的方式 （每小時、 每天、 每週等） 和監視器中的資料管線 toorun 和管理它們在概覽 tooidentify 問題並採取動作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="ee7db-124">請參閱下列文章，如果您不熟悉 Azure Data Factory 因為它有助於了解 hello 架構/hello 方案實作本文所述的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="ee7db-125">Azure Data Factory 簡介</span><span class="sxs-lookup"><span data-stu-id="ee7db-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="ee7db-126">建置第一個資料管線</span><span class="sxs-lookup"><span data-stu-id="ee7db-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="ee7db-127">（選擇性） toolearn 深入了解 Azure Data Factory，請參閱 hello [Azure Data factory 的學習路徑](https://azure.microsoft.com/documentation/learning-paths/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="ee7db-128">Data Factory 和 Batch 一起使用</span><span class="sxs-lookup"><span data-stu-id="ee7db-128">Data Factory and Batch together</span></span>
<span data-ttu-id="ee7db-129">資料處理站包含內建活動，例如 tooa 目的地資料存放區和 Hive 活動 tooprocess 資料在 Azure 上使用 Hadoop 叢集 (HDInsight)，從來源資料複製活動 toocopy/移動資料存放區。</span><span class="sxs-lookup"><span data-stu-id="ee7db-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="ee7db-130">如需支援的轉換活動清單，請參閱 [資料轉換活動](data-factory-data-transformation-activities.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee7db-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="ee7db-131">也可讓您 toocreate 自訂.NET 活動 toomove 或處理序的資料，與您自己的邏輯，並在 Azure HDInsight 叢集上或 Azure Batch 集區的 Vm 上執行這些活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="ee7db-132">當您使用 Azure 批次時，您可以設定 hello 集區 tooauto 標尺 （新增或移除 hello 的工作負載的 Vm） 根據您提供的公式。</span><span class="sxs-lookup"><span data-stu-id="ee7db-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="ee7db-133">範例解決方案架構</span><span class="sxs-lookup"><span data-stu-id="ee7db-133">Architecture of sample solution</span></span>
<span data-ttu-id="ee7db-134">即使這篇文章中所描述的 hello 架構適用於簡單的解決方案，它是相關 toocomplex 案例，例如風險所涵蓋了金融服務、 映像處理和轉譯和 genomic 分析模型。</span><span class="sxs-lookup"><span data-stu-id="ee7db-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="ee7db-135">hello 圖表將說明 Data Factory 1） 如何協調資料移動，並處理和 2） 如何處理 Azure 批次的資料則會以平行方式 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="ee7db-136">下載和列印 hello 圖表，以方便參考 (11x17 中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="ee7db-137">或 A3 的大小)︰[使用 Azure Batch 和 Data Factory 的 HPC 和資料協調](http://go.microsoft.com/fwlink/?LinkId=717686)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="ee7db-138">[![大規模資料處理圖表](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="ee7db-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="ee7db-139">hello 下列清單提供 hello hello 程序的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="ee7db-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="ee7db-140">hello 解決方案包含程式碼和說明 toobuild hello 端對端解決方案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="ee7db-141">**以計算節點的集區 (VM) 設定 Azure Batch**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="ee7db-142">您可以指定節點的 hello 數目和每個節點的大小。</span><span class="sxs-lookup"><span data-stu-id="ee7db-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="ee7db-143">**建立 Azure Data Factory 執行個體** ，並為其設定代表 Azure Blob 儲存體、Azure Batch 計算服務、輸入/輸出資料和工作流程/管線的實體，並建立具有會移動和轉換資料之活動的工作流程/管線。</span><span class="sxs-lookup"><span data-stu-id="ee7db-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="ee7db-144">**在 hello Data Factory 管線中建立的自訂.NET 活動**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="ee7db-145">hello 活動是您在 hello Azure Batch 集區執行的使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="ee7db-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="ee7db-146">**將大量的輸入資料儲存為 Azure 儲存體中的 blob**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="ee7db-147">資料會分成邏輯配量 (通常依時間來分)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="ee7db-148">**Data Factory 複製以平行方式處理資料的**toohello 次要位置。</span><span class="sxs-lookup"><span data-stu-id="ee7db-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="ee7db-149">**Data Factory 執行 hello 使用批次所配置的 hello 集區的自訂活動**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="ee7db-150">Data Factory 可以同時執行多個活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="ee7db-151">每個活動各處理某個配量的資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="ee7db-152">hello 結果會儲存在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ee7db-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="ee7db-153">**Data Factory 移動 hello 最終結果 tooa 第三個位置**，應用程式，透過散發，或做進一步處理其他工具。</span><span class="sxs-lookup"><span data-stu-id="ee7db-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="ee7db-154">範例解決方案的實作</span><span class="sxs-lookup"><span data-stu-id="ee7db-154">Implementation of sample solution</span></span>
<span data-ttu-id="ee7db-155">hello 範例方案刻意簡單，而且是 tooshow 您如何 toouse Data Factory 和批次一起 tooprocess 資料集。</span><span class="sxs-lookup"><span data-stu-id="ee7db-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="ee7db-156">hello 方案就是計算組織中的時間序列的輸入檔中的 hello 次數的搜尋詞彙 ("Microsoft")。</span><span class="sxs-lookup"><span data-stu-id="ee7db-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="ee7db-157">它會輸出 hello 計數 toooutput 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="ee7db-158">**時間**： 如果您已熟悉 Azure Data Factory 及批次中的基本概念，而且已完成的 hello 必要條件下面所列，我們會評估此解決方案會 toocomplete 1-2 小時。</span><span class="sxs-lookup"><span data-stu-id="ee7db-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ee7db-159">必要條件</span><span class="sxs-lookup"><span data-stu-id="ee7db-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="ee7db-160">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="ee7db-160">Azure subscription</span></span>
<span data-ttu-id="ee7db-161">如果您沒有 Azure 訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee7db-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ee7db-162">請參閱 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="ee7db-163">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ee7db-163">Azure storage account</span></span>
<span data-ttu-id="ee7db-164">您可以使用 Azure 儲存體帳戶將 hello 資料儲存在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="ee7db-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="ee7db-165">如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="ee7db-166">hello 範例解決方案會使用 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ee7db-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="ee7db-167">Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="ee7db-167">Azure Batch account</span></span>
<span data-ttu-id="ee7db-168">建立 Azure 批次帳戶使用 hello [Azure 入口網站](http://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="ee7db-169">請參閱 [建立和管理 Azure Batch 帳戶](../batch/batch-account-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="ee7db-170">請注意 hello Azure Batch 帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ee7db-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="ee7db-171">您也可以使用[新增 AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee7db-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="ee7db-172">如需使用此 Cmdlet 的詳細指示，請參閱 [開始使用 Azure Batch PowerShell Cmdlet](../batch/batch-powershell-cmdlets-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee7db-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="ee7db-173">hello 範例方案會使用 Azure 批次 （間接透過 Azure Data Factory 管線） tooprocess 資料，以平行方式的運算節點 （受管理的虛擬機器集合） 的集區上。</span><span class="sxs-lookup"><span data-stu-id="ee7db-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="ee7db-174">Azure Batch 虛擬機器 (VM) 集區</span><span class="sxs-lookup"><span data-stu-id="ee7db-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="ee7db-175">建立至少有 2 個計算節點的 **Azure Batch 集區** 。</span><span class="sxs-lookup"><span data-stu-id="ee7db-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="ee7db-176">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **瀏覽**在 hello 左的窗格中，然後按一下**批次帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="ee7db-177">選取您的 Azure Batch 帳戶 tooopen hello**批次帳戶**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee7db-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="ee7db-178">按一下 [集區]  圖格。</span><span class="sxs-lookup"><span data-stu-id="ee7db-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="ee7db-179">在 hello**集區**刀鋒視窗中，按一下 hello 工具列 tooadd 集區中的 新增 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ee7db-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="ee7db-180">請輸入 hello 集區的識別碼 (**集區識別碼**)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="ee7db-181">請注意 hello **hello 集區的識別碼**; 時，您需要它建立 hello Data Factory 方案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="ee7db-182">指定**Windows Server 2012 R2** hello 作業系統系列設定。</span><span class="sxs-lookup"><span data-stu-id="ee7db-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="ee7db-183">選取 **節點定價層**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="ee7db-184">輸入**2**做為 hello 值**目標專用**設定。</span><span class="sxs-lookup"><span data-stu-id="ee7db-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="ee7db-185">輸入**2**做為 hello 值**每個節點的最大工作**設定。</span><span class="sxs-lookup"><span data-stu-id="ee7db-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="ee7db-186">按一下**確定**toocreate hello 集區。</span><span class="sxs-lookup"><span data-stu-id="ee7db-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="ee7db-187">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="ee7db-187">Azure Storage Explorer</span></span>
<span data-ttu-id="ee7db-188">[Azure 儲存體總管 6 (工具)](https://azurestorageexplorer.codeplex.com/) 或 [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (來自 ClumsyLeaf 軟體)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="ee7db-189">您可以使用這些工具來檢查及更改 Azure 儲存體專案包括雲端裝載應用程式的 hello 記錄檔中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="ee7db-190">使用私用存取 (沒有匿名存取) 建立名為 **mycontainer** 的容器</span><span class="sxs-lookup"><span data-stu-id="ee7db-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="ee7db-191">如果您使用**CloudXplorer**、 建立資料夾和子資料夾與 hello 下列結構：</span><span class="sxs-lookup"><span data-stu-id="ee7db-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="ee7db-192">`Inputfolder` 和 `outputfolder` 是 `mycontainer` 中的最上層資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="ee7db-193">hello`inputfolder`具有與日期時間戳記 (YYYY-MM-DD-HH) 的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="ee7db-194">如果您使用**Azure 儲存體總管**，在 hello 下一個步驟中，您需要 tooupload 檔名： `inputfolder/2015-11-16-00/file.txt`， `inputfolder/2015-11-16-01/file.txt` ，依此類推。</span><span class="sxs-lookup"><span data-stu-id="ee7db-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="ee7db-195">此步驟會自動建立 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="ee7db-196">建立文字檔**file.txt**有 hello 關鍵字的內容與您電腦上**Microsoft**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="ee7db-197">例如：“test custom activity Microsoft test custom activity Microsoft”。</span><span class="sxs-lookup"><span data-stu-id="ee7db-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="ee7db-198">上傳 hello 檔案 toohello 下一個輸入 Azure blob 儲存體中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="ee7db-199">如果您使用**Azure 儲存體總管**，hello 檔案上傳**file.txt**太**mycontainer**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="ee7db-200">按一下**複製**hello 工具列 toocreate hello blob 的複本上。</span><span class="sxs-lookup"><span data-stu-id="ee7db-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="ee7db-201">在 hello**複製 Blob**對話方塊中，變更 hello**目的地 blob 名稱**太`inputfolder/2015-11-16-00/file.txt`。</span><span class="sxs-lookup"><span data-stu-id="ee7db-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="ee7db-202">重複此步驟 toocreate `inputfolder/2015-11-16-01/file.txt`， `inputfolder/2015-11-16-02/file.txt`， `inputfolder/2015-11-16-03/file.txt`， `inputfolder/2015-11-16-04/file.txt` ，依此類推。</span><span class="sxs-lookup"><span data-stu-id="ee7db-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="ee7db-203">這個動作會自動建立 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="ee7db-204">建立另一個容器，名為：`customactivitycontainer`。</span><span class="sxs-lookup"><span data-stu-id="ee7db-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="ee7db-205">您上傳 hello 自訂活動 zip 檔案 toothis 容器。</span><span class="sxs-lookup"><span data-stu-id="ee7db-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="ee7db-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee7db-206">Visual Studio</span></span>
<span data-ttu-id="ee7db-207">安裝 Microsoft Visual Studio 2012 或更新版本 toocreate hello 自訂批次活動 toobe hello Data Factory 方案中使用。</span><span class="sxs-lookup"><span data-stu-id="ee7db-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="ee7db-208">高階步驟 toocreate hello 方案</span><span class="sxs-lookup"><span data-stu-id="ee7db-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="ee7db-209">建立包含 hello 資料處理邏輯的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="ee7db-210">建立 Azure data factory，以使用自訂活動的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7db-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="ee7db-211">建立 hello 自訂活動</span><span class="sxs-lookup"><span data-stu-id="ee7db-211">Create hello custom activity</span></span>
<span data-ttu-id="ee7db-212">hello Data Factory 的自訂活動是此範例方案的 hello 心。</span><span class="sxs-lookup"><span data-stu-id="ee7db-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="ee7db-213">hello 範例解決方案會使用 Azure Batch toorun hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="ee7db-214">請參閱[Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md)hello 的基本資訊 toodevelop 自訂活動和使用在 Azure Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="ee7db-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="ee7db-215">toocreate.NET 自訂活動，您可以使用 Azure Data Factory 管線中，您需要 toocreate **.NET 類別庫**所實作的類別具有專案**IDotNetActivity**介面。</span><span class="sxs-lookup"><span data-stu-id="ee7db-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="ee7db-216">這個介面只有一個方法： **執行**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="ee7db-217">以下是 hello hello 方法簽章：</span><span class="sxs-lookup"><span data-stu-id="ee7db-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="ee7db-218">hello 方法都有一些您需要 toounderstand 的主要元件。</span><span class="sxs-lookup"><span data-stu-id="ee7db-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="ee7db-219">hello 方法會採用四個參數：</span><span class="sxs-lookup"><span data-stu-id="ee7db-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="ee7db-220">**linkedServices**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-220">**linkedServices**.</span></span> <span data-ttu-id="ee7db-221">連結輸入/輸出資料來源的連結服務的可列舉清單 (例如： Azure Blob 儲存體) toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="ee7db-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="ee7db-222">在此範例中，只有一個用於輸入和輸出的 Azure 儲存體類型連結服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="ee7db-223">**資料集**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-223">**datasets**.</span></span> <span data-ttu-id="ee7db-224">這是資料集的可列舉清單。</span><span class="sxs-lookup"><span data-stu-id="ee7db-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="ee7db-225">您可以使用此參數 tooget hello 位置以及輸入和輸出資料集所定義的結構描述。</span><span class="sxs-lookup"><span data-stu-id="ee7db-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="ee7db-226">**活動**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-226">**activity**.</span></span> <span data-ttu-id="ee7db-227">這個參數代表 hello 目前計算實體-在此情況下，Azure 批次服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="ee7db-228">**記錄器**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-228">**logger**.</span></span> <span data-ttu-id="ee7db-229">hello 記錄器可讓您為 「 使用者 」 記錄檔以取得 hello 撰寫偵錯註解呈現的 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="ee7db-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="ee7db-230">hello 方法會傳回可使用的 toochain 自訂活動運算子 hello 未來的字典。</span><span class="sxs-lookup"><span data-stu-id="ee7db-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="ee7db-231">尚未實作這項功能，因此從 hello 方法會傳回空的字典。</span><span class="sxs-lookup"><span data-stu-id="ee7db-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="ee7db-232">程序： 建立 hello 自訂活動</span><span class="sxs-lookup"><span data-stu-id="ee7db-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="ee7db-233">在 Visual Studio 中建立 .NET 類別庫專案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="ee7db-234">啟動 **Visual Studio 2012**/**2013/2015**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="ee7db-235">按一下**檔案**，點太**新增**，然後按一下**專案**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="ee7db-236">展開 [範本]，然後選取 [Visual C#]**\#**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="ee7db-237">在本逐步解說中，您可以使用 C\#，但是您可以使用任何.NET 語言 toodevelop hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="ee7db-238">選取**類別庫**從 hello hello 右上的專案類型清單。</span><span class="sxs-lookup"><span data-stu-id="ee7db-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="ee7db-239">輸入**MyDotNetActivity** hello**名稱**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="ee7db-240">選取**c:\\ADF** hello**位置**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="ee7db-241">建立 hello 資料夾**ADF**如果不存在。</span><span class="sxs-lookup"><span data-stu-id="ee7db-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="ee7db-242">按一下**確定**toocreate hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="ee7db-243">按一下**工具**，點太**NuGet 套件管理員**，然後按一下**Package Manager Console**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="ee7db-244">在 hello **Package Manager Console**，執行下列命令 tooimport hello **Microsoft.Azure.Management.DataFactories**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="ee7db-245">匯入 hello **Azure 儲存體**toohello 專案中的 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="ee7db-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="ee7db-246">因為您使用 hello Blob 儲存體 API 在這個範例中，您會需要此封裝。</span><span class="sxs-lookup"><span data-stu-id="ee7db-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="ee7db-247">新增下列 hello**使用**hello 專案中的指示詞 toohello 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-247">Add hello following **using** directives toohello source file in hello project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="ee7db-248">變更 hello 名稱的 hello**命名空間**太**MyDotNetActivityNS**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="ee7db-249">變更 hello hello 類別名稱太**MyDotNetActivity**從其中 hello **IDotNetActivity**介面，如底下所示。</span><span class="sxs-lookup"><span data-stu-id="ee7db-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="ee7db-250">實作 （加入） hello **Execute**方法 hello **IDotNetActivity**介面 toohello **MyDotNetActivity**類別，並複製下列範例程式碼 toohello 方法的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="ee7db-251">請參閱 hello [Execute Method](#execute-method)一節說明此方法中使用的 hello 邏輯。</span><span class="sxs-lookup"><span data-stu-id="ee7db-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

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
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
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
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
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
9. <span data-ttu-id="ee7db-252">新增下列 helper 方法 toohello 類別 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="ee7db-253">這些方法會叫用 hello **Execute**方法。</span><span class="sxs-lookup"><span data-stu-id="ee7db-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="ee7db-254">最重要的是，hello **Calculate**方法隔離 hello 程式碼，可逐一查看每個 blob。</span><span class="sxs-lookup"><span data-stu-id="ee7db-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
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
    <span data-ttu-id="ee7db-255">hello **GetFolderPath**方法會傳回 hello 路徑 toohello 資料夾該 hello 資料集點 tooand hello **GetFileName**方法會傳回 hello hello blob 檔案的名稱/的 hello 指向資料集。</span><span class="sxs-lookup"><span data-stu-id="ee7db-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="ee7db-256">hello **Calculate**方法會計算關鍵字的執行個體的 hello 數目**Microsoft** hello 輸入檔 (hello 資料夾中的 blob) 中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="ee7db-257">hello 搜尋詞彙 ("Microsoft") 是硬式編碼 hello 程式碼中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="ee7db-258">編譯 hello 專案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-258">Compile hello project.</span></span> <span data-ttu-id="ee7db-259">按一下**建置**從 hello 功能表，然後按一下**建置方案**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="ee7db-260">啟動**Windows 檔案總管**，並瀏覽過**bin\\偵錯**或**bin\\釋放**資料夾視 hello 組建類型而定。</span><span class="sxs-lookup"><span data-stu-id="ee7db-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="ee7db-261">建立 zip 檔案**MyDotNetActivity.zip** ，其中包含所有的 hello 二進位碼檔案中 hello  **\\bin\\偵錯**資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="ee7db-262">您可能想 tooinclude hello MyDotNetActivity。**pdb**檔案以便讓您取得 hello hello 問題原因發生失敗時，原始程式碼中的其他詳細資料，例如行號。</span><span class="sxs-lookup"><span data-stu-id="ee7db-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="ee7db-263">上傳**MyDotNetActivity.zip**為 toohello blob 容器的 blob:`customactivitycontainer`在 hello Azure blob 儲存體的 hello **StorageLinkedService**連結服務中 hello **ADFTutorialDataFactory**使用。</span><span class="sxs-lookup"><span data-stu-id="ee7db-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="ee7db-264">建立 hello blob 容器`customactivitycontainer`如果不存在。</span><span class="sxs-lookup"><span data-stu-id="ee7db-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="ee7db-265">Execute 方法</span><span class="sxs-lookup"><span data-stu-id="ee7db-265">Execute method</span></span>
<span data-ttu-id="ee7db-266">本章節提供更多詳細資料和 hello hello Execute 方法中的程式碼的相關注意事項。</span><span class="sxs-lookup"><span data-stu-id="ee7db-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="ee7db-267">逐一查看 hello 輸入集合的 hello 成員存在於 hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx)命名空間。</span><span class="sxs-lookup"><span data-stu-id="ee7db-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="ee7db-268">逐一查看 hello blob 集合時，需要使用 hello **BlobContinuationToken**類別。</span><span class="sxs-lookup"><span data-stu-id="ee7db-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="ee7db-269">基本上，您必須使用與-while 迴圈與 hello 權杖做為結束迴圈 hello hello 機制。</span><span class="sxs-lookup"><span data-stu-id="ee7db-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="ee7db-270">如需詳細資訊，請參閱[如何 toouse 與.NET 的 Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="ee7db-271">基本迴圈如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee7db-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="ee7db-272">請參閱 hello 文件以 hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx)方法，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ee7db-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="ee7db-273">hello 程式碼的 hello 內以邏輯方式處理透過 blob hello 組會做為 while 迴圈。</span><span class="sxs-lookup"><span data-stu-id="ee7db-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="ee7db-274">在 hello **Execute**方法中，執行 hello-雖然迴圈傳送 hello 的 blob 清單 tooa 方法名為**Calculate**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="ee7db-275">hello 方法會傳回名為的字串變數**輸出**也就是需要逐一查看所有 hello blob hello 區段中的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="ee7db-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="ee7db-276">它會傳回 hello 次數 hello 搜尋詞彙 (**Microsoft**) hello blob 中傳遞 toohello **Calculate**方法。</span><span class="sxs-lookup"><span data-stu-id="ee7db-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="ee7db-277">一次 hello **Calculate** hello 工作完成的方法，則必須寫入 tooa 新 blob。</span><span class="sxs-lookup"><span data-stu-id="ee7db-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="ee7db-278">讓每一組處理的 blob，可以與 hello 結果寫入新的 blob。</span><span class="sxs-lookup"><span data-stu-id="ee7db-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="ee7db-279">toowrite tooa 新 blob，第一個尋找 hello 輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="ee7db-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="ee7db-280">hello 程式碼也會呼叫的 helper 方法： **GetFolderPath** tooretrieve hello 資料夾路徑 （hello 儲存體容器名稱）。</span><span class="sxs-lookup"><span data-stu-id="ee7db-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="ee7db-281">hello **GetFolderPath**轉換 hello 資料集物件 tooan AzureBlobDataSet，有一個名為 FolderPath 屬性。</span><span class="sxs-lookup"><span data-stu-id="ee7db-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="ee7db-282">hello 程式碼呼叫 hello **GetFileName**方法 tooretrieve hello 檔案名稱 （blob）。</span><span class="sxs-lookup"><span data-stu-id="ee7db-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="ee7db-283">hello 程式碼是類似 toohello 上述程式碼 tooget hello 資料夾路徑。</span><span class="sxs-lookup"><span data-stu-id="ee7db-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="ee7db-284">藉由建立 URI 物件寫入 hello hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="ee7db-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="ee7db-285">hello URI 建構函式使用 hello **BlobEndpoint**屬性 tooreturn hello 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="ee7db-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="ee7db-286">hello 資料夾路徑和檔案名稱會加入 tooconstruct hello 輸出 blob URI。</span><span class="sxs-lookup"><span data-stu-id="ee7db-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="ee7db-287">已寫入 hello hello 檔案名稱和您現在可以撰寫 hello 輸出字串 hello 從**Calculate**方法 tooa 新的 blob:</span><span class="sxs-lookup"><span data-stu-id="ee7db-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="ee7db-288">建立 hello 資料處理站</span><span class="sxs-lookup"><span data-stu-id="ee7db-288">Create hello data factory</span></span>
<span data-ttu-id="ee7db-289">在 [hello[建立 hello 自訂活動](#create-the-custom-activity)] 區段中，建立自訂活動和上傳的 hello zip 檔案與二進位檔和 hello PDB 檔案 tooan Azure blob 容器。</span><span class="sxs-lookup"><span data-stu-id="ee7db-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="ee7db-290">在本節中，您將建立 Azure**資料 factory**與**管線**使用 hello**自訂活動**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="ee7db-291">hello 的 hello 自訂活動代表 hello 輸入資料夾中的 hello blob （檔案） 的輸入資料集 (`mycontainer\\inputfolder`) blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="ee7db-292">hello 輸出資料集，如 hello 活動代表 hello 輸出資料夾中的 hello 輸出 blob (`mycontainer\\outputfolder`) blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="ee7db-293">卸除一個或多個檔案中的 hello 輸入資料夾：</span><span class="sxs-lookup"><span data-stu-id="ee7db-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="ee7db-294">以 hello 內容之後到每一個 hello 資料夾，例如，卸除一個檔案 (.txt)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="ee7db-295">每個輸入的資料夾對應 tooa Azure Data Factory 中的配量，即使 hello 資料夾有 2 個以上的檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="ee7db-296">Hello 管線處理每個配量時，該配量的 hello 輸入資料夾中的所有 hello blob 會都重複 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="ee7db-297">您會看到五個輸出檔案以 hello 相同內容。</span><span class="sxs-lookup"><span data-stu-id="ee7db-297">You see five output files with hello same content.</span></span> <span data-ttu-id="ee7db-298">例如，處理 hello 2015-11-16-00 資料夾中的 hello 檔案 hello 輸出檔案具有下列內容的 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7db-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="ee7db-299">如果您卸除多個檔案 （.txt、 file2.txt、 file3.txt） 以 hello 中，相同內容 toohello 輸入的資料夾，則會看見 hello hello 輸出檔中的內容之後。</span><span class="sxs-lookup"><span data-stu-id="ee7db-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="ee7db-300">每個資料夾 (2015年-11-16-00，等等) 對應 tooa 配量在此範例中，即使 hello 資料夾有多個輸入的檔。</span><span class="sxs-lookup"><span data-stu-id="ee7db-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="ee7db-301">hello 輸出檔案具有三行，其中每個輸入檔案 (blob) hello 與 hello 配量 (2015年-11-16-00) 相關聯的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="ee7db-302">每個活動執行都會建立一個工作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-302">A task is created for each activity run.</span></span> <span data-ttu-id="ee7db-303">在此範例中，只有一個活動中沒有 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="ee7db-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="ee7db-304">Hello 管線處理配量，hello 自訂活動會在 Azure 批次 tooprocess hello 配量上執行。</span><span class="sxs-lookup"><span data-stu-id="ee7db-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="ee7db-305">由於有 5 個配量 (每個配量可以有多個 blob 或檔案)，因此在 Azure Batch 中會建立 5 個工作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="ee7db-306">工作將會批次上時，實際上 hello 執行自訂活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="ee7db-307">下列逐步解說的 hello 提供其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="ee7db-308">步驟 1： 建立 hello 資料處理站</span><span class="sxs-lookup"><span data-stu-id="ee7db-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="ee7db-309">登入 toohello 之後[Azure 入口網站](https://portal.azure.com/)，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7db-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="ee7db-310">按一下**新增**hello 左側功能表上。</span><span class="sxs-lookup"><span data-stu-id="ee7db-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="ee7db-311">按一下**資料 + 分析**在 hello**新增**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee7db-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="ee7db-312">按一下**Data Factory**上 hello**資料分析**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee7db-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="ee7db-313">在 hello**新的 data factory**刀鋒視窗中，輸入**CustomActivityFactory** hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="ee7db-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="ee7db-314">hello hello Azure data factory 的名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="ee7db-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="ee7db-315">如果您收到 hello 錯誤： **Data factory 名稱"CustomActivityFactory"不是使用**，變更 hello hello data factory 名稱 (例如， **yournameCustomActivityFactory**)，然後再次嘗試建立一次。</span><span class="sxs-lookup"><span data-stu-id="ee7db-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="ee7db-316">按一下 [資源群組名稱] ，並選取現有的資源群組，或建立一個群組。</span><span class="sxs-lookup"><span data-stu-id="ee7db-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="ee7db-317">請確認您使用 hello 正確的訂用帳戶和您想要建立 hello 資料 factory toobe 的區域。</span><span class="sxs-lookup"><span data-stu-id="ee7db-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="ee7db-318">按一下**建立**上 hello**新的 data factory**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="ee7db-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="ee7db-319">您會看到 hello hello 中建立的資料處理站**儀表板**的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ee7db-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="ee7db-320">已成功建立 hello 資料處理站之後，您會看到 hello 資料 factory 頁面上，它會顯示 hello hello data factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="ee7db-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="ee7db-321">步驟 2：建立連結服務</span><span class="sxs-lookup"><span data-stu-id="ee7db-321">Step 2: Create linked services</span></span>
<span data-ttu-id="ee7db-322">連結的服務將資料存放區，或計算服務 tooan 的 Azure data factory。</span><span class="sxs-lookup"><span data-stu-id="ee7db-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="ee7db-323">在此步驟中，您連結您**Azure 儲存體**帳戶和**Azure Batch**帳戶 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="ee7db-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ee7db-324">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="ee7db-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="ee7db-325">按一下 hello**作者及部署**磚 hello **DATA FACTORY**刀鋒伺服器**CustomActivityFactory**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="ee7db-326">您會看到 hello Data Factory 編輯器。</span><span class="sxs-lookup"><span data-stu-id="ee7db-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="ee7db-327">按一下**新建資料存放區**在 hello 命令列，然後選擇  **Azure 儲存體。**</span><span class="sxs-lookup"><span data-stu-id="ee7db-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="ee7db-328">您應該會看見 hello JSON 指令碼來建立 Azure 儲存體已連結的 hello 編輯器中的服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="ee7db-329">取代**帳戶名稱**hello Azure 儲存體帳戶名稱和**帳戶金鑰**hello 的 hello Azure 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="ee7db-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="ee7db-330">toolearn 如何 tooget 您的儲存體存取金鑰，請參閱[檢視、 複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="ee7db-331">按一下**部署**hello 命令列 toodeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="ee7db-332">建立 Azure Batch 連結服務</span><span class="sxs-lookup"><span data-stu-id="ee7db-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="ee7db-333">在此步驟中，您可以建立連結的服務，如您**Azure Batch**為使用的 toorun hello Data Factory 的自訂活動的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee7db-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="ee7db-334">按一下**新計算**在 hello 命令列，然後選擇  **Azure 批次。**</span><span class="sxs-lookup"><span data-stu-id="ee7db-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="ee7db-335">您應該會看見 hello JSON 指令碼來建立 Azure Batch 連結 hello 編輯器中的服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="ee7db-336">在 hello JSON 指令碼：</span><span class="sxs-lookup"><span data-stu-id="ee7db-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="ee7db-337">取代**帳戶名稱**hello Azure Batch 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ee7db-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="ee7db-338">取代**便捷鍵**hello hello Azure Batch 帳戶存取索引鍵。</span><span class="sxs-lookup"><span data-stu-id="ee7db-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="ee7db-339">輸入 hello hello 集區識別碼 hello **poolName**屬性**。**</span><span class="sxs-lookup"><span data-stu-id="ee7db-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="ee7db-340">您可以針對此屬性指定集區名稱或集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="ee7db-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="ee7db-341">輸入 hello 批次 URI hello **batchUri** JSON 屬性。</span><span class="sxs-lookup"><span data-stu-id="ee7db-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="ee7db-342">hello **URL**從 hello **Azure Batch 帳戶 刀鋒視窗**處於 hello 下列格式： \<accountname\>。\<區域\>。 batch.azure.com。Hello **batchUri** hello JSON 屬性，您需要太**移除"accountname。 」**</span><span class="sxs-lookup"><span data-stu-id="ee7db-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="ee7db-343">從 hello 的 URL。</span><span class="sxs-lookup"><span data-stu-id="ee7db-343">from hello URL.</span></span> <span data-ttu-id="ee7db-344">範例：`"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="ee7db-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="ee7db-345">Hello **poolName**屬性，您也可以指定 hello 識別碼 hello 集區，而不是 hello hello 集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="ee7db-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ee7db-346">hello Data Factory 服務不支援隨選項 Azure 批次的 HDInsight 的一樣。</span><span class="sxs-lookup"><span data-stu-id="ee7db-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="ee7db-347">您只能使用 Azure Data Factory 中自己的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="ee7db-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="ee7db-348">指定**StorageLinkedService** hello **linkedServiceName**屬性。</span><span class="sxs-lookup"><span data-stu-id="ee7db-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="ee7db-349">您 hello 上一個步驟中建立這項連結的服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="ee7db-350">此儲存體會做為檔案和記錄檔的預備區域。</span><span class="sxs-lookup"><span data-stu-id="ee7db-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="ee7db-351">按一下**部署**hello 命令列 toodeploy hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="ee7db-352">步驟 3：建立資料集</span><span class="sxs-lookup"><span data-stu-id="ee7db-352">Step 3: Create datasets</span></span>
<span data-ttu-id="ee7db-353">在此步驟中，您可以建立資料集 toorepresent 輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="ee7db-354">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="ee7db-354">Create input dataset</span></span>
1. <span data-ttu-id="ee7db-355">在 hello**編輯器**hello Data Factory 中，按一下 **新的資料集**上 hello 工具列，並按一下按鈕**Azure Blob 儲存體**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="ee7db-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="ee7db-356">取代下列 JSON 片段 hello hello 右窗格中的 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="ee7db-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
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

    <span data-ttu-id="ee7db-357">您稍後會在本逐步解說建立管線，開始時間為：2015-11-16T00:00:00Z，而結束時間為：2015-11-16T05:00:00Z。</span><span class="sxs-lookup"><span data-stu-id="ee7db-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="ee7db-358">它會排程的 tooproduce 資料**每小時**，因此有 5 個輸入/輸出配量 (之間**00**: 00:00-\> **05**: 00:00)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="ee7db-359">hello**頻率**和**間隔**hello 輸入資料集設定太**小時**和**1**，這表示該 hello 輸入配量是可用每小時。</span><span class="sxs-lookup"><span data-stu-id="ee7db-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="ee7db-360">以下是 hello 開始時間的每個配量，由表示**SliceStart** hello 上方 JSON 片段中的系統變數。</span><span class="sxs-lookup"><span data-stu-id="ee7db-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="ee7db-361">**配量**</span><span class="sxs-lookup"><span data-stu-id="ee7db-361">**Slice**</span></span> | <span data-ttu-id="ee7db-362">**開始時間**</span><span class="sxs-lookup"><span data-stu-id="ee7db-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="ee7db-363">1</span><span class="sxs-lookup"><span data-stu-id="ee7db-363">1</span></span>         | <span data-ttu-id="ee7db-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="ee7db-365">2</span><span class="sxs-lookup"><span data-stu-id="ee7db-365">2</span></span>         | <span data-ttu-id="ee7db-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="ee7db-367">3</span><span class="sxs-lookup"><span data-stu-id="ee7db-367">3</span></span>         | <span data-ttu-id="ee7db-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="ee7db-369">4</span><span class="sxs-lookup"><span data-stu-id="ee7db-369">4</span></span>         | <span data-ttu-id="ee7db-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="ee7db-371">5</span><span class="sxs-lookup"><span data-stu-id="ee7db-371">5</span></span>         | <span data-ttu-id="ee7db-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="ee7db-373">hello **folderPath**使用 hello 年、 月、 日和小時一部分 hello 配量的開始時間的計算 (**SliceStart**)。</span><span class="sxs-lookup"><span data-stu-id="ee7db-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="ee7db-374">因此，以下是輸入的資料夾的對應的 tooa 配量的方式。</span><span class="sxs-lookup"><span data-stu-id="ee7db-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="ee7db-375">**配量**</span><span class="sxs-lookup"><span data-stu-id="ee7db-375">**Slice**</span></span> | <span data-ttu-id="ee7db-376">**開始時間**</span><span class="sxs-lookup"><span data-stu-id="ee7db-376">**Start time**</span></span>          | <span data-ttu-id="ee7db-377">**輸入資料夾**</span><span class="sxs-lookup"><span data-stu-id="ee7db-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="ee7db-378">1</span><span class="sxs-lookup"><span data-stu-id="ee7db-378">1</span></span>         | <span data-ttu-id="ee7db-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="ee7db-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="ee7db-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="ee7db-381">2</span><span class="sxs-lookup"><span data-stu-id="ee7db-381">2</span></span>         | <span data-ttu-id="ee7db-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="ee7db-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="ee7db-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="ee7db-384">3</span><span class="sxs-lookup"><span data-stu-id="ee7db-384">3</span></span>         | <span data-ttu-id="ee7db-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="ee7db-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="ee7db-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="ee7db-387">4</span><span class="sxs-lookup"><span data-stu-id="ee7db-387">4</span></span>         | <span data-ttu-id="ee7db-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="ee7db-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="ee7db-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="ee7db-390">5</span><span class="sxs-lookup"><span data-stu-id="ee7db-390">5</span></span>         | <span data-ttu-id="ee7db-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="ee7db-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="ee7db-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="ee7db-393">按一下**部署**hello 工具列 toocreate 且部署 hello **InputDataset**資料表。</span><span class="sxs-lookup"><span data-stu-id="ee7db-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="ee7db-394">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="ee7db-394">Create output dataset</span></span>
<span data-ttu-id="ee7db-395">在此步驟中，您可以建立類型 AzureBlob toorepresent hello 輸出資料的其他資料集。</span><span class="sxs-lookup"><span data-stu-id="ee7db-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="ee7db-396">在 hello**編輯器**hello Data Factory 中，按一下 **新的資料集**上 hello 工具列，並按一下按鈕**Azure Blob 儲存體**從 hello 下拉式選單。</span><span class="sxs-lookup"><span data-stu-id="ee7db-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="ee7db-397">取代下列 JSON 片段 hello hello 右窗格中的 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="ee7db-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
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

    <span data-ttu-id="ee7db-398">為每個輸入配量產生輸出 blob/檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="ee7db-399">以下是為每個配量命名輸出檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="ee7db-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="ee7db-400">所有的 hello 輸出檔案產生一個輸出資料夾中： `mycontainer\\outputfolder`。</span><span class="sxs-lookup"><span data-stu-id="ee7db-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="ee7db-401">**配量**</span><span class="sxs-lookup"><span data-stu-id="ee7db-401">**Slice**</span></span> | <span data-ttu-id="ee7db-402">**開始時間**</span><span class="sxs-lookup"><span data-stu-id="ee7db-402">**Start time**</span></span>          | <span data-ttu-id="ee7db-403">**輸出檔案**</span><span class="sxs-lookup"><span data-stu-id="ee7db-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="ee7db-404">1</span><span class="sxs-lookup"><span data-stu-id="ee7db-404">1</span></span>         | <span data-ttu-id="ee7db-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="ee7db-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="ee7db-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="ee7db-407">2</span><span class="sxs-lookup"><span data-stu-id="ee7db-407">2</span></span>         | <span data-ttu-id="ee7db-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="ee7db-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="ee7db-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="ee7db-410">3</span><span class="sxs-lookup"><span data-stu-id="ee7db-410">3</span></span>         | <span data-ttu-id="ee7db-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="ee7db-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="ee7db-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="ee7db-413">4</span><span class="sxs-lookup"><span data-stu-id="ee7db-413">4</span></span>         | <span data-ttu-id="ee7db-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="ee7db-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="ee7db-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="ee7db-416">5</span><span class="sxs-lookup"><span data-stu-id="ee7db-416">5</span></span>         | <span data-ttu-id="ee7db-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="ee7db-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="ee7db-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="ee7db-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="ee7db-419">請記住所有 hello 輸入的資料夾中的檔案 (例如： 2015年-11-16-00) 屬於 hello 的開始時間配量： 2015年-11-16-00。</span><span class="sxs-lookup"><span data-stu-id="ee7db-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="ee7db-420">此配量處理時，hello 自訂活動會掃描每個檔案，並產生 hello 與 hello 發生次數的搜尋詞彙 ("Microsoft") 的輸出檔中的資料行。</span><span class="sxs-lookup"><span data-stu-id="ee7db-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="ee7db-421">Hello 輸出檔 hello 資料夾 2015年-11-16-00 中有三個檔案，如果有三個行： 2015年-11-16-00.txt。</span><span class="sxs-lookup"><span data-stu-id="ee7db-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="ee7db-422">按一下**部署**hello 工具列 toocreate 且部署 hello **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="ee7db-423">步驟 4： 建立和執行自訂活動與 hello 管線</span><span class="sxs-lookup"><span data-stu-id="ee7db-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="ee7db-424">在此步驟中，您可以建立管線某個活動，hello 您稍早建立的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee7db-425">如果尚未上傳 hello **file.txt** tooinput 資料夾在 hello blob 容器中，建立 hello 管線之前執行此動作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="ee7db-426">hello **isPaused**屬性設定 toofalse hello 管線 JSON，因此 hello 管線便會立即執行為 hello**啟動**日期為過去的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="ee7db-427">在 hello Data Factory 編輯器中，按一下 **新管線**hello 命令列上。</span><span class="sxs-lookup"><span data-stu-id="ee7db-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="ee7db-428">如果看不到 hello 命令，請按一下**...（省略符號）** toosee 它。</span><span class="sxs-lookup"><span data-stu-id="ee7db-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="ee7db-429">取代下列 JSON 指令碼的 hello hello 右窗格中的 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="ee7db-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="ee7db-430">請注意下列點 hello:</span><span class="sxs-lookup"><span data-stu-id="ee7db-430">Note hello following points:</span></span>

   * <span data-ttu-id="ee7db-431">Hello 管線中只能有一個活動，而且型別的： **DotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="ee7db-432">**AssemblyName**設定 toohello hello DLL 名稱： **MyDotNetActivity.dll**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="ee7db-433">**EntryPoint**設定得**MyDotNetActivityNS.MyDotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="ee7db-434">在您的程式碼中，它基本上是 \<namespace\>.\<classname\>。</span><span class="sxs-lookup"><span data-stu-id="ee7db-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="ee7db-435">**PackageLinkedService**設定得**StorageLinkedService** ，以指 toohello blob 儲存體包含 hello 自訂活動的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="ee7db-436">如果您使用不同的 Azure 儲存體帳戶輸入/輸出檔案和 hello 自訂活動的 zip 檔案，您必須 toocreate 另一個 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="ee7db-437">本文假設您使用 hello 相同的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ee7db-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="ee7db-438">**PackageFile**設定得**customactivitycontainer/MyDotNetActivity.zip**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="ee7db-439">其為 hello 格式： \<containerforthezip\>/\<nameofthezip.zip\>。</span><span class="sxs-lookup"><span data-stu-id="ee7db-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="ee7db-440">hello 自訂活動會採用**InputDataset**做為輸入和**OutputDataset**做為輸出。</span><span class="sxs-lookup"><span data-stu-id="ee7db-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="ee7db-441">hello **linkedServiceName** hello 自訂活動的屬性指向 toohello **AzureBatchLinkedService**，它會告訴 Azure Data Factory 的 hello 自訂活動必須 toorun Azure 批次。</span><span class="sxs-lookup"><span data-stu-id="ee7db-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="ee7db-442">hello**並行**設定很重要。</span><span class="sxs-lookup"><span data-stu-id="ee7db-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="ee7db-443">如果您使用 hello 預設值為 1，即使您有 2 或多個計算節點 hello Azure Batch 集區中的，會處理 hello 配量一個接著一個。</span><span class="sxs-lookup"><span data-stu-id="ee7db-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="ee7db-444">因此，您就不可以運用 Azure 批次的 hello 平行處理功能。</span><span class="sxs-lookup"><span data-stu-id="ee7db-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="ee7db-445">如果您設定**並行**tooa 較高的值，例如 2，表示兩個配量 （對應 tootwo Azure 批次中的工作） 可以在 hello 處理相同的時間，在此情況下，這兩個 hello 中的 Vm hello Azure Batch 集區並加以使用。</span><span class="sxs-lookup"><span data-stu-id="ee7db-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="ee7db-446">因此，適當地設定 hello 並行屬性。</span><span class="sxs-lookup"><span data-stu-id="ee7db-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="ee7db-447">根據預設，無論何時，一個工作 (配量) 都只會在一個 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="ee7db-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="ee7db-448">hello 原因在於，根據預設，hello**每個 VM 的最大工作**too1 Azure Batch 集區設定。</span><span class="sxs-lookup"><span data-stu-id="ee7db-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="ee7db-449">必要條件的一部分，您建立了集區與這個屬性集 too2，讓兩個 Data Factory 配量可在 hello VM 上執行相同的時間。</span><span class="sxs-lookup"><span data-stu-id="ee7db-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="ee7db-450">**isPaused**屬性 toofalse 預設設定。</span><span class="sxs-lookup"><span data-stu-id="ee7db-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="ee7db-451">hello 管線執行立即在此範例中，因為 hello 配量開始在過去的 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="ee7db-452">您可以設定這個屬性 tootrue toopause hello 管線，並將它回復 toofalse toorestart。</span><span class="sxs-lookup"><span data-stu-id="ee7db-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="ee7db-453">hello**啟動**時間和**結束**時間是 5 小時以上距離而配量不會產生每小時，因此 hello 管線所產生五個配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="ee7db-454">按一下**部署**hello 命令列 toodeploy hello 管線。</span><span class="sxs-lookup"><span data-stu-id="ee7db-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="ee7db-455">步驟 5： 測試 hello 管線</span><span class="sxs-lookup"><span data-stu-id="ee7db-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="ee7db-456">在此步驟中，您測試管線 hello 放 hello 輸入資料夾的檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="ee7db-457">讓我們開頭為測試 hello 管線每一個輸入資料夾的一個檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="ee7db-458">在 hello Data Factory 刀鋒視窗中 hello Azure 入口網站中，按一下 **圖表**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="ee7db-459">在 hello 圖表檢視中，按兩下 輸入資料集： **InputDataset**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="ee7db-460">您應該會看見 hello **InputDataset**刀鋒視窗的全部五個配量的準備。</span><span class="sxs-lookup"><span data-stu-id="ee7db-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="ee7db-461">請注意 hello**配量的開始時間**和**配量結束時間**每個配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="ee7db-462">在 hello**圖表檢視**，現在按一下**OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="ee7db-463">您應該會看到 hello 五個輸出配量會 hello 就緒狀態，是否他們已經產生。</span><span class="sxs-lookup"><span data-stu-id="ee7db-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="ee7db-464">使用 Azure 入口網站 tooview hello**工作**hello 與相關聯**配量**並查看哪些 VM 執行的每個配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="ee7db-465">請參閱 [Data Factory 和 Batch 整合](#data-factory-and-batch-integration) 一節，以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="ee7db-466">您應該會看到 hello 輸出檔中 hello`outputfolder`的`mycontainer`在您的 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ee7db-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="ee7db-467">您應會看見五個輸出檔案，每個輸入配量各一個。</span><span class="sxs-lookup"><span data-stu-id="ee7db-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="ee7db-468">每個 hello 輸出檔案應該具有內容的類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ee7db-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="ee7db-469">hello 下列圖表說明 hello Data Factory 配量將 tootasks Azure 批次中的對應。</span><span class="sxs-lookup"><span data-stu-id="ee7db-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="ee7db-470">在此範例中，一個配量只有一個執行。</span><span class="sxs-lookup"><span data-stu-id="ee7db-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="ee7db-471">現在，我們要以一個資料夾包含多個檔案的方式來試試。</span><span class="sxs-lookup"><span data-stu-id="ee7db-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="ee7db-472">建立檔案： **file2.txt**， **file3.txt**， **file4.txt**，和**file5.txt** hello 與相同內容如 file.txt hello 資料夾中所示：**2015年-11-06-01**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="ee7db-473">在 hello 輸出資料夾中，**刪除**hello 輸出檔： **2015年-11-16-01.txt**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="ee7db-474">現在，在 hello **OutputDataset**刀鋒視窗中，以滑鼠右鍵按一下 hello 配量與**配量的開始時間**設定得**2015 年 11 月 16 日 01:00:00 AM**，然後按一下**執行**toorerun/重新 process hello 配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="ee7db-475">現在，hello 配量會有五個檔案，而不是一個檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="ee7db-476">Hello 配量執行，其狀態為之後**準備**，確認此配量的 hello 輸出檔中的 hello 內容 (**2015年-11-16-01.txt**) 在 hello`outputfolder`的`mycontainer`在您的 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ee7db-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="ee7db-477">應該要有每個檔案的 hello 配量的線。</span><span class="sxs-lookup"><span data-stu-id="ee7db-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="ee7db-478">如果您未刪除 hello 輸出檔案 2015年-11-16-01.txt 嘗試以五個輸入檔案之前，您會看到從 hello 先前配量執行一行和五行 hello 目前配量執行中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="ee7db-479">根據預設，hello 內容是附加的 toooutput 檔案已經存在。</span><span class="sxs-lookup"><span data-stu-id="ee7db-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="ee7db-480">Data Factory 和 Batch 整合</span><span class="sxs-lookup"><span data-stu-id="ee7db-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="ee7db-481">hello Data Factory 服務 Azure 批次中建立工作以 hello 名稱： `adf-poolname:job-xxx`。</span><span class="sxs-lookup"><span data-stu-id="ee7db-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - Batch 作業](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="ee7db-483">配量的每個活動執行時，會建立 hello 作業中的工作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="ee7db-484">如果有 10 個配量準備 toobe 處理，10 個工作會建立 hello 作業中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="ee7db-485">您可以有多個配量，以平行方式執行，如果您有多個計算節點區內 hello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="ee7db-486">如果 hello 最大的工作，每個計算節點設定得 > 1，可以有超過一個配量上 hello 執行相同的計算。</span><span class="sxs-lookup"><span data-stu-id="ee7db-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="ee7db-487">此範例中有 5 個配量，所以 Azure Batch 中有 5 個工作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="ee7db-488">以 hello**並行**設定得**5** hello 在管線中 Azure Data Factory JSON 和**每個 VM 的最大工作**設定得**2** Azure 批次中集區**2** hello 工作執行快速 （檢查工作的開始和結束時間） 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="ee7db-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="ee7db-489">使用 hello 入口 tooview hello 批次工作和其相關聯之工作與 hello**配量**並查看哪些 VM 執行的每個配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - Batch 作業工作](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="ee7db-491">偵錯 hello 管線</span><span class="sxs-lookup"><span data-stu-id="ee7db-491">Debug hello pipeline</span></span>
<span data-ttu-id="ee7db-492">偵錯包含一些基本技術：</span><span class="sxs-lookup"><span data-stu-id="ee7db-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="ee7db-493">如果未設定 hello 輸入配量太**準備**，確認 hello 輸入的資料夾結構是否正確，以及 file.txt 存在 hello 輸入資料夾中。</span><span class="sxs-lookup"><span data-stu-id="ee7db-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="ee7db-494">在 hello **Execute**方法的自訂活動，使用 hello **IActivityLogger**物件 toolog 資訊可協助您疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="ee7db-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="ee7db-495">記錄的 hello 訊息顯示在 hello 使用者\_0 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ee7db-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="ee7db-496">在 hello **OutputDataset**刀鋒視窗中，按一下 hello 配量 toosee hello**資料配量**刀鋒視窗，該配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="ee7db-497">您會看到該配量的 [活動執行]。</span><span class="sxs-lookup"><span data-stu-id="ee7db-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="ee7db-498">您應該會看到一個 hello 配量執行的活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="ee7db-499">如果您按一下**執行**hello 命令列中，您可以啟動另一個活動執行 hello 相同配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="ee7db-500">當您按一下 hello 活動執行時，請參閱 hello**活動執行詳細資料**刀鋒視窗的記錄檔的清單。</span><span class="sxs-lookup"><span data-stu-id="ee7db-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="ee7db-501">您會看到記錄的訊息，在 hello**使用者\_0 記錄**檔案。</span><span class="sxs-lookup"><span data-stu-id="ee7db-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="ee7db-502">當發生錯誤時，因為 hello 重試計數設定 too3 hello 管線/活動 JSON 中會看到三個活動執行。</span><span class="sxs-lookup"><span data-stu-id="ee7db-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="ee7db-503">當您按一下 hello 活動執行時，您會看到 hello 記錄檔，您可以檢閱 tootroubleshoot hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="ee7db-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="ee7db-504">在 hello 清單中的記錄檔，按一下 hello**使用者 0.log**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="ee7db-505">Hello 右面板中會使用 hello 的 hello 結果**IActivityLogger.Write**方法。</span><span class="sxs-lookup"><span data-stu-id="ee7db-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="ee7db-506">檢查 system-0.log 是否有任何系統錯誤訊息和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ee7db-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="ee7db-507">包含 hello **PDB**檔案 hello zip 檔案中，所以 hello 錯誤詳細資料會有這類資訊**呼叫堆疊**發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="ee7db-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="ee7db-508">所有 hello hello zip 檔案中的 hello 自訂活動必須是在 hello**上層**具有任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="ee7db-509">請確定該 hello **assemblyName** (MyDotNetActivity.dll)， **entryPoint** (MyDotNetActivityNS.MyDotNetActivity)， **packageFile** (customactivitycontainer /MyDotNetActivity.zip) 和**packageLinkedService** (應該點 toohello Azure blob 儲存體包含 hello zip 檔案) 會設定 toocorrect 值。</span><span class="sxs-lookup"><span data-stu-id="ee7db-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="ee7db-510">如果您修正錯誤，且想 tooreprocess hello 配量，以滑鼠右鍵按一下 hello 配量在 hello **OutputDataset**刀鋒視窗，然後按一下**執行**。</span><span class="sxs-lookup"><span data-stu-id="ee7db-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="ee7db-511">您會在 Azure Blob 儲存體中看到一個**容器**，名為：`adfjobs`。</span><span class="sxs-lookup"><span data-stu-id="ee7db-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="ee7db-512">不會自動刪除此容器，但您在完成測試 hello 方案之後可以安全地刪除。</span><span class="sxs-lookup"><span data-stu-id="ee7db-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="ee7db-513">同樣地，hello Data Factory 方案建立 Azure 批次**作業**名為： `adf-\<pool ID/name\>:job-0000000001`。</span><span class="sxs-lookup"><span data-stu-id="ee7db-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="ee7db-514">如果您想測試 hello 方案之後，您可以刪除此作業。</span><span class="sxs-lookup"><span data-stu-id="ee7db-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="ee7db-515">hello 自訂活動不會使用 hello **app.config**檔案從您的封裝。</span><span class="sxs-lookup"><span data-stu-id="ee7db-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="ee7db-516">因此，如果您的程式碼會讀取 hello 組態檔中的任何連接字串，因此無法在執行階段。</span><span class="sxs-lookup"><span data-stu-id="ee7db-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="ee7db-517">hello 最佳作法是當使用 Azure Batch toohold 中的秘密**Azure KeyVault**、 使用憑證為基礎的服務主體 tooprotect hello 所以 keyvault，及散布 hello 憑證 tooAzure 批次集區。</span><span class="sxs-lookup"><span data-stu-id="ee7db-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="ee7db-518">hello.NET 自訂活動，則可以從 hello KeyVault 在執行階段存取機密資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="ee7db-519">這個解決方案是泛型，而且可以延展 tooany 類型的密碼，而不只是連接字串。</span><span class="sxs-lookup"><span data-stu-id="ee7db-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="ee7db-520">沒有簡單的因應措施 （但不是最佳作法）： 您可以建立**Azure SQL 連結服務**與連接字串設定，建立使用 hello 連結的服務，以及鏈結 hello 資料集做為虛擬輸入資料集的資料集自訂.NET 活動 toohello。</span><span class="sxs-lookup"><span data-stu-id="ee7db-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="ee7db-521">接著，您可以存取 hello 連結服務的連接字串 hello 自訂活動程式碼中，且它應該在執行階段可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="ee7db-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="ee7db-522">擴充 hello 範例</span><span class="sxs-lookup"><span data-stu-id="ee7db-522">Extend hello sample</span></span>
<span data-ttu-id="ee7db-523">您可以擴充此範例 toolearn 有關 Azure Data Factory 和 Azure 批次功能的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ee7db-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="ee7db-524">例如，tooprocess 配量在不同的時間範圍中，請勿 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ee7db-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="ee7db-525">新增下列子資料夾中 hello hello `inputfolder`: 2015年-11-16-05，2015年-11-16-06，201-11-16-07，2011年-11-16-08 版 2015年-11-16-09 並放置在輸入檔在這些資料夾中的。</span><span class="sxs-lookup"><span data-stu-id="ee7db-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="ee7db-526">變更 hello 管線就會從 hello 結束時間`2015-11-16T05:00:00Z`太`2015-11-16T10:00:00Z`。</span><span class="sxs-lookup"><span data-stu-id="ee7db-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="ee7db-527">在 hello**圖表檢視**，按兩下 hello **InputDataset**，並確認已準備 hello 輸入配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="ee7db-528">按兩下**OuptutDataset** toosee hello 輸出配量狀態。</span><span class="sxs-lookup"><span data-stu-id="ee7db-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="ee7db-529">如果它們都處於就緒狀態，請檢查 hello hello 輸出檔的輸出資料夾。</span><span class="sxs-lookup"><span data-stu-id="ee7db-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="ee7db-530">增加或減少 hello**並行**設定 toounderstand 它會如何影響您的方案，hello 效能特別 hello 處理 Azure 批次上發生。</span><span class="sxs-lookup"><span data-stu-id="ee7db-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="ee7db-531">(請參閱步驟 4： 建立和執行 hello 管線，如需有關 hello**並行**設定。)</span><span class="sxs-lookup"><span data-stu-id="ee7db-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="ee7db-532">建立 [每個 VM 的工作數上限] 較低/較高的集區。</span><span class="sxs-lookup"><span data-stu-id="ee7db-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="ee7db-533">toouse hello 新集區在建立時，更新 hello hello Data Factory 方案中的 Azure Batch 連結服務。</span><span class="sxs-lookup"><span data-stu-id="ee7db-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="ee7db-534">(請參閱步驟 4： 建立和執行 hello 管線，如需有關 hello**每個 VM 的最大工作**設定。)</span><span class="sxs-lookup"><span data-stu-id="ee7db-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="ee7db-535">建立具有 **自動調整** 功能的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="ee7db-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="ee7db-536">自動調整 Azure Batch 集區中的計算節點是 hello 動態調整處理能力，您的應用程式所使用。</span><span class="sxs-lookup"><span data-stu-id="ee7db-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="ee7db-537">hello 範例公式會達到 hello 下列行為： 一開始建立 hello 集區時，開始的 1 的 VM。</span><span class="sxs-lookup"><span data-stu-id="ee7db-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="ee7db-538">$PendingTasks 度量定義 hello 數項工作中執行 + （佇列） 的作用中狀態。</span><span class="sxs-lookup"><span data-stu-id="ee7db-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="ee7db-539">hello 公式中 hello 過去 180 秒尋找 hello 的平均數目暫止的工作，並據此設定 TargetDedicated。</span><span class="sxs-lookup"><span data-stu-id="ee7db-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="ee7db-540">它會確保 TargetDedicated 一律不會超過 25 部 VM。</span><span class="sxs-lookup"><span data-stu-id="ee7db-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="ee7db-541">因此，提交新的工作，因為集區自動成長和做為工作完成，Vm 會變成可用逐一和 hello 自動調整壓縮這些 Vm。</span><span class="sxs-lookup"><span data-stu-id="ee7db-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="ee7db-542">startingNumberOfVMs 和 maxNumberofVMs 可以調整的 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="ee7db-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="ee7db-543">自動調整公式：</span><span class="sxs-lookup"><span data-stu-id="ee7db-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="ee7db-544">如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的計算節點](../batch/batch-automatic-scaling.md) 。</span><span class="sxs-lookup"><span data-stu-id="ee7db-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="ee7db-545">如果 hello 集區使用 hello 預設[autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)，hello 批次服務可能需要 15 到 30 分鐘 tooprepare hello VM，然後再執行 hello 自訂活動。</span><span class="sxs-lookup"><span data-stu-id="ee7db-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="ee7db-546">如果 hello 集區使用不同的 autoScaleEvaluationInterval，hello 批次服務可能需要 autoScaleEvaluationInterval + 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="ee7db-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="ee7db-547">在 hello 範例解決方案中，hello **Execute**方法會叫用 hello **Calculate**方法，以處理輸入的資料配量 tooproduce 輸出資料配量。</span><span class="sxs-lookup"><span data-stu-id="ee7db-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="ee7db-548">您可以撰寫您自己的方法 tooprocess 輸入資料，並以呼叫 tooyour 方法取代 hello Execute 方法中的 hello Calculate 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="ee7db-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="ee7db-549">後續步驟： 取用 hello 資料</span><span class="sxs-lookup"><span data-stu-id="ee7db-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="ee7db-550">處理資料之後，您可以使用 **Microsoft Power BI** 之類的線上工具來取用資料。</span><span class="sxs-lookup"><span data-stu-id="ee7db-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="ee7db-551">以下是您了解 Power BI 連結 toohelp 以及 toouse 它在 Azure 中：</span><span class="sxs-lookup"><span data-stu-id="ee7db-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="ee7db-552">在 Power BI 中探索資料集</span><span class="sxs-lookup"><span data-stu-id="ee7db-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="ee7db-553">開始使用 Power BI Desktop hello</span><span class="sxs-lookup"><span data-stu-id="ee7db-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="ee7db-554">重新整理 Power BI 中的資料</span><span class="sxs-lookup"><span data-stu-id="ee7db-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="ee7db-555">Azure 和 Power BI - 基本概觀</span><span class="sxs-lookup"><span data-stu-id="ee7db-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="ee7db-556">參考</span><span class="sxs-lookup"><span data-stu-id="ee7db-556">References</span></span>
* [<span data-ttu-id="ee7db-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ee7db-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="ee7db-558">簡介 tooAzure Data Factory 服務</span><span class="sxs-lookup"><span data-stu-id="ee7db-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="ee7db-559">開始使用 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ee7db-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="ee7db-560">在 Azure 資料處理站管線中使用自訂活動</span><span class="sxs-lookup"><span data-stu-id="ee7db-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="ee7db-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="ee7db-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="ee7db-562">Azure Batch 的基本概念</span><span class="sxs-lookup"><span data-stu-id="ee7db-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="ee7db-563">Azure Batch 功能概觀</span><span class="sxs-lookup"><span data-stu-id="ee7db-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="ee7db-564">建立和管理 Azure Batch 帳戶在 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ee7db-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="ee7db-565">開始使用 Azure Batch 程式庫 .NET</span><span class="sxs-lookup"><span data-stu-id="ee7db-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
