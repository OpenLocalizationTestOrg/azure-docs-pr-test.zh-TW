---
title: "使用 Data Factory 和 Batch 處理大型資料集 | Microsoft Docs"
description: "說明如何使用 Azure Batch 的平行處理功能處理 Azure Data Factory 管線中的大量資料。"
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
ms.openlocfilehash: 9defbf7a6a515740fa3b3cb1c67a2f5f9d9baa01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="58355-103">使用 Data Factory 和 Batch 處理大型資料集</span><span class="sxs-lookup"><span data-stu-id="58355-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="58355-104">本文說明範例解決方案的架構，此解決方案能以自動且排程的方式移動和處理大型資料集。</span><span class="sxs-lookup"><span data-stu-id="58355-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="58355-105">本文也提供如何使用 Azure Data Factory 和 Azure Batch 實作解決方案的端對端逐步解說。</span><span class="sxs-lookup"><span data-stu-id="58355-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="58355-106">這篇文章比我們的一般文章還長，因為它包含整個範例解決方案的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="58355-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="58355-107">如果您不熟悉 Batch 和 Data Factory，您可以了解這兩項服務以及它們如何搭配運作。</span><span class="sxs-lookup"><span data-stu-id="58355-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="58355-108">如果您已對這兩項服務有所了解，而且要設計/架構解決方案，則可以將焦點純粹放在文章內的[架構章節](#architecture-of-sample-solution)，如果您正在開發原型或解決方案，或許也會想試試[逐步解說](#implementation-of-sample-solution)中的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="58355-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="58355-109">歡迎您對此內容以及您如何使用它提出看法。</span><span class="sxs-lookup"><span data-stu-id="58355-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="58355-110">讓我們先看看 Data Factory 和 Batch 服務如何有助於處理雲端中的大型資料集。</span><span class="sxs-lookup"><span data-stu-id="58355-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="58355-111">為何使用 Azure Batch？</span><span class="sxs-lookup"><span data-stu-id="58355-111">Why Azure Batch?</span></span>
<span data-ttu-id="58355-112">Azure Batch 可讓您在雲端有效率地執行大規模的平行和高效能運算 (HPC) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58355-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="58355-113">它是一項平台服務，可排程要在一組受管理的虛擬機器上執行的計算密集型工作，而且可以調整計算資源以符合工作的需求。</span><span class="sxs-lookup"><span data-stu-id="58355-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="58355-114">在使用 Batch 服務時，您可以定義用來大規模平行執行應用程式的 Azure 計算資源。</span><span class="sxs-lookup"><span data-stu-id="58355-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="58355-115">您可以依需要或依排程的工作來執行，而不需要手動建立、設定和管理 HPC 叢集、個別的虛擬機器、虛擬網路或複雜的作業和工作排程基礎結構。</span><span class="sxs-lookup"><span data-stu-id="58355-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="58355-116">如果您不熟悉 Azure Batch，請參閱下列文章，因為其內容有助於了解本文所述解決方案的架構/實作。</span><span class="sxs-lookup"><span data-stu-id="58355-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="58355-117">Azure Batch 的基本概念</span><span class="sxs-lookup"><span data-stu-id="58355-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="58355-118">Batch 功能概觀</span><span class="sxs-lookup"><span data-stu-id="58355-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="58355-119">(選擇性) 若要深入了解 Azure Batch，請參閱 [Azure Batch 的學習路徑](https://azure.microsoft.com/documentation/learning-paths/batch/)。</span><span class="sxs-lookup"><span data-stu-id="58355-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="58355-120">為何使用 Azure Data Factory？</span><span class="sxs-lookup"><span data-stu-id="58355-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="58355-121">Data Factory 是雲端架構資料整合服務，用來協調以及自動移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="58355-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="58355-122">透過 Data Factory 服務，您可以建立受管理的資料管線，將資料從內部部署和雲端的資料存放區移動至集中式資料存放區 (例如︰Azure Blob 儲存體)，以及使用服務 (例如 Azure HDInsight 和 Azure Machine Learning) 處理/轉換資料。</span><span class="sxs-lookup"><span data-stu-id="58355-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="58355-123">您也可以利用排程方式 (每小時、每天、每週等) 排定執行資料管線，以及快速地監視和管理資料管線以找出問題並採取行動。</span><span class="sxs-lookup"><span data-stu-id="58355-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="58355-124">如果您不熟悉 Azure Data Factory，請參閱下列文章，因為其內容有助於了解本文所述解決方案的架構/實作。</span><span class="sxs-lookup"><span data-stu-id="58355-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="58355-125">Azure Data Factory 簡介</span><span class="sxs-lookup"><span data-stu-id="58355-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="58355-126">建置第一個資料管線</span><span class="sxs-lookup"><span data-stu-id="58355-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="58355-127">(選擇性) 若要深入了解 Azure Data Factory，請參閱 [Azure Data Factory 的學習路徑](https://azure.microsoft.com/documentation/learning-paths/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="58355-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="58355-128">Data Factory 和 Batch 一起使用</span><span class="sxs-lookup"><span data-stu-id="58355-128">Data Factory and Batch together</span></span>
<span data-ttu-id="58355-129">Data Factory 中有內建的活動，例如複製活動，其可將資料從來源資料存放區複製/移動到目的地資料存放區，以及 Hive 活動，其可在 Azure 上使用 Hadoop 叢集 (HDInsight) 處理資料。</span><span class="sxs-lookup"><span data-stu-id="58355-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="58355-130">如需支援的轉換活動清單，請參閱 [資料轉換活動](data-factory-data-transformation-activities.md) 。</span><span class="sxs-lookup"><span data-stu-id="58355-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="58355-131">它也可讓您建立自訂的 .NET 活動來使用您自己的邏輯移動或處理資料，以及在 Azure HDInsight 叢集上或 Azure Batch VM 集區上執行這些活動。</span><span class="sxs-lookup"><span data-stu-id="58355-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="58355-132">當您使用 Azure Batch 時，您可以將集區設定為根據您提供的公式自動調整大小 (根據工作負載新增或移除 VM)。</span><span class="sxs-lookup"><span data-stu-id="58355-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="58355-133">範例解決方案架構</span><span class="sxs-lookup"><span data-stu-id="58355-133">Architecture of sample solution</span></span>
<span data-ttu-id="58355-134">雖然本文所描述的架構是針對簡單的解決方案，但它也和複雜案例相關，例如依金融服務、映像處理和轉譯以及基因分析進行的風險模型建立。</span><span class="sxs-lookup"><span data-stu-id="58355-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="58355-135">此圖表將說明 1) Data Factory 如何協調資料移動和處理，以及 2) Azure Batch 如何以平行方式處理資料。</span><span class="sxs-lookup"><span data-stu-id="58355-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="58355-136">下載及列印圖表以便參考 (11 x 17 英吋</span><span class="sxs-lookup"><span data-stu-id="58355-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="58355-137">或 A3 的大小)︰[使用 Azure Batch 和 Data Factory 的 HPC 和資料協調](http://go.microsoft.com/fwlink/?LinkId=717686)。</span><span class="sxs-lookup"><span data-stu-id="58355-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="58355-138">[![大規模資料處理圖表](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="58355-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="58355-139">下列清單提供程序中的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="58355-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="58355-140">此解決方案包含用來建置端對端解決方案的程式碼和說明。</span><span class="sxs-lookup"><span data-stu-id="58355-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="58355-141">**以計算節點的集區 (VM) 設定 Azure Batch**。</span><span class="sxs-lookup"><span data-stu-id="58355-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="58355-142">您可以指定節點數目和每個節點的大小。</span><span class="sxs-lookup"><span data-stu-id="58355-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="58355-143">**建立 Azure Data Factory 執行個體** ，並為其設定代表 Azure Blob 儲存體、Azure Batch 計算服務、輸入/輸出資料和工作流程/管線的實體，並建立具有會移動和轉換資料之活動的工作流程/管線。</span><span class="sxs-lookup"><span data-stu-id="58355-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="58355-144">**在 Data Factory 管線建立自訂 .NET 活動**。</span><span class="sxs-lookup"><span data-stu-id="58355-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="58355-145">活動是在 Azure Batch 集區上執行的使用者程式碼。</span><span class="sxs-lookup"><span data-stu-id="58355-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="58355-146">**將大量的輸入資料儲存為 Azure 儲存體中的 blob**。</span><span class="sxs-lookup"><span data-stu-id="58355-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="58355-147">資料會分成邏輯配量 (通常依時間來分)。</span><span class="sxs-lookup"><span data-stu-id="58355-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="58355-148">**Data Factory 將要以平行方式處理的資料複製到次要位置**。</span><span class="sxs-lookup"><span data-stu-id="58355-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="58355-149">**Data Factory 使用 Batch 所配置的集區執行自訂活動**。</span><span class="sxs-lookup"><span data-stu-id="58355-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="58355-150">Data Factory 可以同時執行多個活動。</span><span class="sxs-lookup"><span data-stu-id="58355-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="58355-151">每個活動各處理某個配量的資料。</span><span class="sxs-lookup"><span data-stu-id="58355-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="58355-152">結果會儲存在 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="58355-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="58355-153">**Data Factory 會將最終結果移至第三個位置**，以透過應用程式加以散發，或由其他工具做進一步的處理。</span><span class="sxs-lookup"><span data-stu-id="58355-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="58355-154">範例解決方案的實作</span><span class="sxs-lookup"><span data-stu-id="58355-154">Implementation of sample solution</span></span>
<span data-ttu-id="58355-155">此範例解決方案是刻意簡化的，旨在為您示範如何搭配使用 Data Factory 和 Batch 來處理資料集。</span><span class="sxs-lookup"><span data-stu-id="58355-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="58355-156">此解決方案純粹計算某個搜尋詞彙 (“Microsoft”) 在以時間序列組織的輸入檔案中出現的次數。</span><span class="sxs-lookup"><span data-stu-id="58355-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="58355-157">它會將此計數輸出至輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-157">It outputs the count to output files.</span></span>

<span data-ttu-id="58355-158">**時間**：如果您熟悉 Azure、Data Factory 和 Batch 的基本概念，並且已符合下列先決條件，我們預估此解決方案需要 1-2 小時來完成。</span><span class="sxs-lookup"><span data-stu-id="58355-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="58355-159">必要條件</span><span class="sxs-lookup"><span data-stu-id="58355-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="58355-160">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="58355-160">Azure subscription</span></span>
<span data-ttu-id="58355-161">如果您沒有 Azure 訂用帳戶，則只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58355-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="58355-162">請參閱 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="58355-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="58355-163">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="58355-163">Azure storage account</span></span>
<span data-ttu-id="58355-164">在本教學課程中，您會使用 Azure 儲存體帳戶來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="58355-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="58355-165">如果您沒有 Azure 儲存體帳戶，請參閱 [建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="58355-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="58355-166">範例解決方案會使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="58355-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="58355-167">Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="58355-167">Azure Batch account</span></span>
<span data-ttu-id="58355-168">使用 [Azure 入口網站](http://manage.windowsazure.com/) 建立 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="58355-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="58355-169">請參閱 [建立和管理 Azure Batch 帳戶](../batch/batch-account-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="58355-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="58355-170">請記下 Azure Batch 帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="58355-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="58355-171">您也可以使用 [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) Cmdlet 建立 Azure Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="58355-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="58355-172">如需使用此 Cmdlet 的詳細指示，請參閱 [開始使用 Azure Batch PowerShell Cmdlet](../batch/batch-powershell-cmdlets-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="58355-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="58355-173">範例解決方案會使用 Azure Batch (透過 Azure Data Factory 管線間接使用)，以平行方式處理計算節點集區 (受管理的虛擬機器集合) 上的資料。</span><span class="sxs-lookup"><span data-stu-id="58355-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="58355-174">Azure Batch 虛擬機器 (VM) 集區</span><span class="sxs-lookup"><span data-stu-id="58355-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="58355-175">建立至少有 2 個計算節點的 **Azure Batch 集區** 。</span><span class="sxs-lookup"><span data-stu-id="58355-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="58355-176">在 [Azure 入口網站](https://portal.azure.com)中，按一下左側功能標中的 [瀏覽]，然後按一下 [Batch 帳戶]。</span><span class="sxs-lookup"><span data-stu-id="58355-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="58355-177">選取您的 Azure Batch 帳戶，以開啟 [Batch 帳戶]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="58355-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="58355-178">按一下 [集區]  圖格。</span><span class="sxs-lookup"><span data-stu-id="58355-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="58355-179">在 [集區]  刀鋒視窗中，按一下工具列上的 [新增] 按鈕以新增集區。</span><span class="sxs-lookup"><span data-stu-id="58355-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="58355-180">輸入集區的識別碼 (**集區識別碼**)。</span><span class="sxs-lookup"><span data-stu-id="58355-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="58355-181">請注意 **集區的識別碼**；您在建立 Data Factory 解決方案時需要它。</span><span class="sxs-lookup"><span data-stu-id="58355-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="58355-182">指定作業系統系列設定的 **Windows Server 2012 R2** 。</span><span class="sxs-lookup"><span data-stu-id="58355-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="58355-183">選取 **節點定價層**。</span><span class="sxs-lookup"><span data-stu-id="58355-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="58355-184">輸入 **2** 做為 [目標專用] 設定的值。</span><span class="sxs-lookup"><span data-stu-id="58355-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="58355-185">輸入 **2** 做為 [每個節點的工作上限] 設定的值。</span><span class="sxs-lookup"><span data-stu-id="58355-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="58355-186">按一下 [確定]  以建立集區。</span><span class="sxs-lookup"><span data-stu-id="58355-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="58355-187">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="58355-187">Azure Storage Explorer</span></span>
<span data-ttu-id="58355-188">[Azure 儲存體總管 6 (工具)](https://azurestorageexplorer.codeplex.com/) 或 [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (來自 ClumsyLeaf 軟體)。</span><span class="sxs-lookup"><span data-stu-id="58355-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="58355-189">您可使用這些工具來檢查及更改 Azure 儲存體專案中的資料，包括雲端架構應用程式的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="58355-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="58355-190">使用私用存取 (沒有匿名存取) 建立名為 **mycontainer** 的容器</span><span class="sxs-lookup"><span data-stu-id="58355-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="58355-191">如果您使用 **CloudXplorer**，請建立具有下列結構的資料夾和子資料夾：</span><span class="sxs-lookup"><span data-stu-id="58355-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="58355-192">`Inputfolder` 和 `outputfolder` 是 `mycontainer` 中的最上層資料夾。</span><span class="sxs-lookup"><span data-stu-id="58355-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="58355-193">`inputfolder` 具有含日期時間戳記 (YYYY-MM-DD-HH) 的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="58355-193">The `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="58355-194">如果您使用 **Azure 儲存體總管**，在下一個步驟中，您必須上傳具有下列名稱的檔案：`inputfolder/2015-11-16-00/file.txt`、`inputfolder/2015-11-16-01/file.txt` 等等。</span><span class="sxs-lookup"><span data-stu-id="58355-194">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="58355-195">此步驟會自動建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="58355-195">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="58355-196">在您的電腦上建立內容中含有關鍵字 **Microsoft** 的文字檔 **file.txt**。</span><span class="sxs-lookup"><span data-stu-id="58355-196">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="58355-197">例如：“test custom activity Microsoft test custom activity Microsoft”。</span><span class="sxs-lookup"><span data-stu-id="58355-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="58355-198">將檔案上傳至 Azure Blob 儲存體中的下列輸入資料夾。</span><span class="sxs-lookup"><span data-stu-id="58355-198">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="58355-199">如果您使用 **Azure 儲存體總管**，請將檔案 **file.txt** 上傳至 **mycontainer**。</span><span class="sxs-lookup"><span data-stu-id="58355-199">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="58355-200">在工具列上按一下 [複製]，以建立 blob 的複本。</span><span class="sxs-lookup"><span data-stu-id="58355-200">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="58355-201">在 [複製 Blob] 對話方塊中，將**目的地 Blob 名稱**變更為 `inputfolder/2015-11-16-00/file.txt`。</span><span class="sxs-lookup"><span data-stu-id="58355-201">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="58355-202">重複此步驟以建立 `inputfolder/2015-11-16-01/file.txt`、`inputfolder/2015-11-16-02/file.txt`、`inputfolder/2015-11-16-03/file.txt`、`inputfolder/2015-11-16-04/file.txt` 等等。</span><span class="sxs-lookup"><span data-stu-id="58355-202">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="58355-203">此動作會自動建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="58355-203">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="58355-204">建立另一個容器，名為：`customactivitycontainer`。</span><span class="sxs-lookup"><span data-stu-id="58355-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="58355-205">您會將自訂活動 zip 檔案上傳至此容器。</span><span class="sxs-lookup"><span data-stu-id="58355-205">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="58355-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58355-206">Visual Studio</span></span>
<span data-ttu-id="58355-207">安裝 Microsoft Visual Studio 2012 或更新版本，以建立要在 Data Factory 解決方案中使用的自訂 Batch 活動。</span><span class="sxs-lookup"><span data-stu-id="58355-207">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="58355-208">建立解決方案的高階步驟</span><span class="sxs-lookup"><span data-stu-id="58355-208">High-level steps to create the solution</span></span>
1. <span data-ttu-id="58355-209">建立包含資料處理邏輯的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="58355-209">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="58355-210">建立使用自訂活動的 Azure Data Factory：</span><span class="sxs-lookup"><span data-stu-id="58355-210">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="58355-211">建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="58355-211">Create the custom activity</span></span>
<span data-ttu-id="58355-212">Data Factory 自訂活動是此範例解決方案的核心。</span><span class="sxs-lookup"><span data-stu-id="58355-212">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="58355-213">範例解決方案會使用 Azure Batch 執行自訂活動。</span><span class="sxs-lookup"><span data-stu-id="58355-213">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="58355-214">如需開發自訂活動，並在 Azure Data Factory 管線中加以使用的基本資訊，請參閱 [在 Azure Data Factory 管線中使用自訂活動](data-factory-use-custom-activities.md) 。</span><span class="sxs-lookup"><span data-stu-id="58355-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="58355-215">若要建立您可以在 Azure Data Factory 管線中使用的 .NET 自訂活動，您必須利用實作 **IDotNetActivity** 介面的類別建立 **.NET 類別庫**專案。</span><span class="sxs-lookup"><span data-stu-id="58355-215">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="58355-216">這個介面只有一個方法： **執行**。</span><span class="sxs-lookup"><span data-stu-id="58355-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="58355-217">以下是該方法的簽章：</span><span class="sxs-lookup"><span data-stu-id="58355-217">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="58355-218">此方法有幾個您必須了解的關鍵元件。</span><span class="sxs-lookup"><span data-stu-id="58355-218">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="58355-219">此方法會採用四個參數：</span><span class="sxs-lookup"><span data-stu-id="58355-219">The method takes four parameters:</span></span>

  1. <span data-ttu-id="58355-220">**linkedServices**。</span><span class="sxs-lookup"><span data-stu-id="58355-220">**linkedServices**.</span></span> <span data-ttu-id="58355-221">將輸入/輸出資料來源 (例如：Azure Blob 儲存體) 連結到 Data Factory 的連結服務列舉清單。</span><span class="sxs-lookup"><span data-stu-id="58355-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="58355-222">在此範例中，只有一個用於輸入和輸出的 Azure 儲存體類型連結服務。</span><span class="sxs-lookup"><span data-stu-id="58355-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="58355-223">**資料集**。</span><span class="sxs-lookup"><span data-stu-id="58355-223">**datasets**.</span></span> <span data-ttu-id="58355-224">這是資料集的可列舉清單。</span><span class="sxs-lookup"><span data-stu-id="58355-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="58355-225">您可以使用這個參數取得輸入和輸出資料集定義的位置和結構描述。</span><span class="sxs-lookup"><span data-stu-id="58355-225">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="58355-226">**活動**。</span><span class="sxs-lookup"><span data-stu-id="58355-226">**activity**.</span></span> <span data-ttu-id="58355-227">這個參數代表目前的計算實體 - 在此情況下為 Azure Batch 服務。</span><span class="sxs-lookup"><span data-stu-id="58355-227">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="58355-228">**記錄器**。</span><span class="sxs-lookup"><span data-stu-id="58355-228">**logger**.</span></span> <span data-ttu-id="58355-229">記錄器可讓您撰寫會呈現為管線的「使用者」記錄檔的偵錯註解。</span><span class="sxs-lookup"><span data-stu-id="58355-229">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="58355-230">此方法會傳回未來可用來將自訂活動鏈結在一起的字典。</span><span class="sxs-lookup"><span data-stu-id="58355-230">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="58355-231">尚未實作這項功能，因此會從方法傳回空的字典。</span><span class="sxs-lookup"><span data-stu-id="58355-231">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="58355-232">程序：建立自訂活動</span><span class="sxs-lookup"><span data-stu-id="58355-232">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="58355-233">在 Visual Studio 中建立 .NET 類別庫專案。</span><span class="sxs-lookup"><span data-stu-id="58355-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="58355-234">啟動 **Visual Studio 2012**/**2013/2015**。</span><span class="sxs-lookup"><span data-stu-id="58355-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="58355-235">按一下 [檔案]，指向 [新增]，然後按一下 [專案]。</span><span class="sxs-lookup"><span data-stu-id="58355-235">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="58355-236">展開 [範本]，然後選取 [Visual C#]**\#**。</span><span class="sxs-lookup"><span data-stu-id="58355-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="58355-237">在此逐步解說中，您使用 C\# 中，但您可以使用任何 .NET 語言來開發自訂活動。</span><span class="sxs-lookup"><span data-stu-id="58355-237">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="58355-238">從右邊的專案類型清單中選取 [類別庫]。</span><span class="sxs-lookup"><span data-stu-id="58355-238">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="58355-239">針對 [名稱] 輸入 **MyDotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="58355-239">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="58355-240">在 [位置] 中選取 **C:\\ADF**。</span><span class="sxs-lookup"><span data-stu-id="58355-240">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="58355-241">建立資料夾 **ADF** (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="58355-241">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="58355-242">按一下 [確定]  以建立專案。</span><span class="sxs-lookup"><span data-stu-id="58355-242">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="58355-243">按一下 [**工具**]，指向 [**NuGet 封裝管理員**]，然後按一下 [**封裝管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="58355-243">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="58355-244">在 [封裝管理員主控台] 中，執行下列命令匯入 **Microsoft.Azure.Management.DataFactories**。</span><span class="sxs-lookup"><span data-stu-id="58355-244">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="58355-245">將 **Azure 儲存體** NuGet 封裝匯入專案中。</span><span class="sxs-lookup"><span data-stu-id="58355-245">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="58355-246">您會在此範例中使用 Blob 儲存體 API，因此需要此套件。</span><span class="sxs-lookup"><span data-stu-id="58355-246">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="58355-247">將下列 **using** 指示詞加入至專案中的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="58355-247">Add the following **using** directives to the source file in the project.</span></span>

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
6. <span data-ttu-id="58355-248">將 **namespace** 的名稱變更為 **MyDotNetActivityNS**。</span><span class="sxs-lookup"><span data-stu-id="58355-248">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="58355-249">將類別的名稱變更為 **MyDotNetActivity**，並從 **IDotNetActivity** 介面延伸它，如下所示。</span><span class="sxs-lookup"><span data-stu-id="58355-249">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="58355-250">對 **MyDotNetActivity** 類別實作 (新增) **IDotNetActivity** 介面的 **Execute** 方法，並將下列範例程式碼複製到方法。</span><span class="sxs-lookup"><span data-stu-id="58355-250">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="58355-251">請參閱 [Execute 方法](#execute-method) 一節，以了解此方法中使用的邏輯。</span><span class="sxs-lookup"><span data-stu-id="58355-251">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
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
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="58355-252">將下列協助程式方法加入至類別。</span><span class="sxs-lookup"><span data-stu-id="58355-252">Add the following helper methods to the class.</span></span> <span data-ttu-id="58355-253">這些方法可用 **Execute** 方法來叫用。</span><span class="sxs-lookup"><span data-stu-id="58355-253">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="58355-254">最重要的是， **Calculate** 方法會隔離逐一查看每個 blob 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="58355-254">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
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
    /// Gets the fileName value from the input/output dataset.
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
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
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
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="58355-255">**GetFolderPath** 方法會將路徑傳回資料集所指向的資料夾，而 **GetFileName** 方法會傳回資料集指向的 blob/檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="58355-255">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="58355-256">**Calculate** 方法會在輸入檔案 (資料夾中的 blob) 計算關鍵字 **Microsoft** 的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="58355-256">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="58355-257">搜尋詞彙 ("Microsoft") 已在程式碼中硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="58355-257">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="58355-258">編譯專案。</span><span class="sxs-lookup"><span data-stu-id="58355-258">Compile the project.</span></span> <span data-ttu-id="58355-259">按一下功能表中的 [建置]，然後按一下 [建置方案]。</span><span class="sxs-lookup"><span data-stu-id="58355-259">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="58355-260">啟動 [Windows 檔案總管]，瀏覽至 **bin\\debug** 或 **bin\\release** 資料夾 (視建置類型而定)。</span><span class="sxs-lookup"><span data-stu-id="58355-260">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="58355-261">建立 zip 檔案 **MyDotNetActivity.zip**，檔案中包含 **\\bin\\Debug** 資料夾中的所有二進位檔。</span><span class="sxs-lookup"><span data-stu-id="58355-261">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="58355-262">建議您新增 MyDotNetActivity.**pdb** 檔案，讓您可以取得額外的詳細資訊，例如在失敗發生時，原始程式碼中引起問題的程式碼行號。</span><span class="sxs-lookup"><span data-stu-id="58355-262">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="58355-263">將 **MyDotNetActivity.zip** 當作 Blob 上傳至 Blob 容器：Azure Blob 儲存體中的 `customactivitycontainer`，由 **ADFTutorialDataFactory** 中的 **StorageLinkedService** 連結服務使用。</span><span class="sxs-lookup"><span data-stu-id="58355-263">Upload **MyDotNetActivity.zip** as a blob to the blob container: `customactivitycontainer` in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="58355-264">建立 blob 容器 `customactivitycontainer` (如果尚未存在)。</span><span class="sxs-lookup"><span data-stu-id="58355-264">Create the blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="58355-265">Execute 方法</span><span class="sxs-lookup"><span data-stu-id="58355-265">Execute method</span></span>
<span data-ttu-id="58355-266">本節提供 Execute 方法中與程式碼相關的詳細資料和注意事項。</span><span class="sxs-lookup"><span data-stu-id="58355-266">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="58355-267">逐一查看輸入集合的成員可在 [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) 命名空間中找到。</span><span class="sxs-lookup"><span data-stu-id="58355-267">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="58355-268">逐一查看 blob 集合需要使用 **BlobContinuationToken** 類別。</span><span class="sxs-lookup"><span data-stu-id="58355-268">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="58355-269">基本上，您必須搭配使用 do-while 迴圈和權杖做為結束迴圈的機制。</span><span class="sxs-lookup"><span data-stu-id="58355-269">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="58355-270">如需詳細資訊，請參閱 [如何從 .NET 使用 Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="58355-270">For more information, see [How to use Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="58355-271">基本迴圈如下所示：</span><span class="sxs-lookup"><span data-stu-id="58355-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
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
   <span data-ttu-id="58355-272">請參閱 [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) 方法的文件以了解詳細資料。</span><span class="sxs-lookup"><span data-stu-id="58355-272">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="58355-273">以邏輯方式逐一查看 blob 集的程式碼會在 do-while 迴圈中執行。</span><span class="sxs-lookup"><span data-stu-id="58355-273">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="58355-274">在 **Execute** 方法中，執行 do-while 迴圈會將 blob 清單傳遞至名為 **Calculate** 的方法。</span><span class="sxs-lookup"><span data-stu-id="58355-274">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="58355-275">此方法會傳回名為 **output** 的字串變數，也就是在區段中逐一查看所有 blob 的結果。</span><span class="sxs-lookup"><span data-stu-id="58355-275">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="58355-276">它會在傳遞給 **Calculate** 方法的 blob 中，傳回搜尋詞彙 (**Microsoft**) 的出現次數。</span><span class="sxs-lookup"><span data-stu-id="58355-276">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="58355-277">一旦 **Calculate** 方法完成此工作，它必須寫入至新的 blob。</span><span class="sxs-lookup"><span data-stu-id="58355-277">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="58355-278">因此對於每個處理過的 blob 集，都可以利用結果撰寫新的 blob。</span><span class="sxs-lookup"><span data-stu-id="58355-278">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="58355-279">若要寫入新的 blob，請先找到輸出資料集。</span><span class="sxs-lookup"><span data-stu-id="58355-279">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="58355-280">程式碼也會呼叫 helper 方法： **GetFolderPath** 來擷取資料夾路徑 (儲存體容器名稱)。</span><span class="sxs-lookup"><span data-stu-id="58355-280">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="58355-281">**GetFolderPath** 會將 DataSet 物件轉換成 AzureBlobDataSet，其具有一個名為 FolderPath 的屬性。</span><span class="sxs-lookup"><span data-stu-id="58355-281">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="58355-282">程式碼會呼叫 **GetFileName** 方法來擷取檔案名稱 (blob 名稱)。</span><span class="sxs-lookup"><span data-stu-id="58355-282">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="58355-283">程式碼取得資料夾路徑的方式類似上述程式碼。</span><span class="sxs-lookup"><span data-stu-id="58355-283">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="58355-284">藉由建立 URI 物件寫入檔案的名稱。</span><span class="sxs-lookup"><span data-stu-id="58355-284">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="58355-285">URI 建構函式使用 **BlobEndpoint** 屬性傳回容器名稱。</span><span class="sxs-lookup"><span data-stu-id="58355-285">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="58355-286">新增資料夾路徑和檔案名稱以建構輸出 blob URI。</span><span class="sxs-lookup"><span data-stu-id="58355-286">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="58355-287">已寫入檔案名稱，現在您可以從 **Calculate** 方法將輸出字串寫入新的 blob：</span><span class="sxs-lookup"><span data-stu-id="58355-287">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="58355-288">建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="58355-288">Create the data factory</span></span>
<span data-ttu-id="58355-289">在 [建立自訂活動] [](#create-the-custom-activity) 區段中，您建立自訂活動，並將包含二進位檔和 PDB 檔案的 zip 檔案上傳到 Azure blob 容器。</span><span class="sxs-lookup"><span data-stu-id="58355-289">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="58355-290">在本節中，您將透過使用**自訂活動**的**管線**建立 Azure **Data Factory**。</span><span class="sxs-lookup"><span data-stu-id="58355-290">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="58355-291">自訂活動的輸入資料集代表 blob 儲存體中輸入資料夾 (`mycontainer\\inputfolder`) 的 blob (檔案)。</span><span class="sxs-lookup"><span data-stu-id="58355-291">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="58355-292">活動的輸出資料集代表 blob 儲存體中輸出資料夾 (`mycontainer\\outputfolder`) 的輸出 blob。</span><span class="sxs-lookup"><span data-stu-id="58355-292">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="58355-293">將一或多個檔案放置在輸入資料夾中：</span><span class="sxs-lookup"><span data-stu-id="58355-293">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="58355-294">例如，將含有下列內容的一個檔案 (file.txt) 放入每個資料夾中。</span><span class="sxs-lookup"><span data-stu-id="58355-294">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="58355-295">即使資料夾有 2 個以上的檔案，每個輸入資料夾還是會對應至 Azure Data Factory 中的配量。</span><span class="sxs-lookup"><span data-stu-id="58355-295">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="58355-296">管線處理每個配量時，自訂活動會為該配量逐一查看輸入資料夾中的所有 blob。</span><span class="sxs-lookup"><span data-stu-id="58355-296">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="58355-297">您可看到五個具有相同內容的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-297">You see five output files with the same content.</span></span> <span data-ttu-id="58355-298">例如，處理 2015-11-16-00 資料夾中的檔案所產生的輸出檔案包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="58355-298">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="58355-299">如果您將多個具有相同內容的檔案 (file.txt、file2.txt、file3.txt) 放置到輸入資料夾中，您會在輸出檔案中看見下列內容。</span><span class="sxs-lookup"><span data-stu-id="58355-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="58355-300">每個資料夾 (2015-11-16-00 等) 分別對應至此範例中的配量，即使資料夾有多個輸入檔案亦然。</span><span class="sxs-lookup"><span data-stu-id="58355-300">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="58355-301">輸出檔案現在會有三行，與配量相關聯的資料夾 (2015-11-16-00) 中的每個輸入檔案 (blob) 各一行。</span><span class="sxs-lookup"><span data-stu-id="58355-301">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="58355-302">每個活動執行都會建立一個工作。</span><span class="sxs-lookup"><span data-stu-id="58355-302">A task is created for each activity run.</span></span> <span data-ttu-id="58355-303">在此範例中，管線中只有一個活動。</span><span class="sxs-lookup"><span data-stu-id="58355-303">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="58355-304">由管線處理配量時，自訂活動即會在 Azure Batch 上執行，以處理配量。</span><span class="sxs-lookup"><span data-stu-id="58355-304">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="58355-305">由於有 5 個配量 (每個配量可以有多個 blob 或檔案)，因此在 Azure Batch 中會建立 5 個工作。</span><span class="sxs-lookup"><span data-stu-id="58355-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="58355-306">工作在 Batch 上執行時，它實際上就是執行中的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="58355-306">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="58355-307">下列逐步解說將提供其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="58355-307">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="58355-308">步驟 1：建立 Data Factory</span><span class="sxs-lookup"><span data-stu-id="58355-308">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="58355-309">登入 [Azure 入口網站](https://portal.azure.com/)之後，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="58355-309">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="58355-310">按一下左側功能表上的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="58355-310">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="58355-311">按一下 [新增] 刀鋒視窗中的 [資料 + 分析]。</span><span class="sxs-lookup"><span data-stu-id="58355-311">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="58355-312">按一下 [資料分析] 刀鋒視窗上的 [Data Factory]。</span><span class="sxs-lookup"><span data-stu-id="58355-312">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="58355-313">在 [新增 Data Factory] 刀鋒視窗中，輸入 **CustomActivityFactor** 做為 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="58355-313">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="58355-314">Azure Data Factory 的名稱在全域必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="58355-314">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="58355-315">如果您收到錯誤：**Data Factory 名稱 “CustomActivityFactory” 無法使用**，請變更 Data Factory 名稱 (例如 **yournameCustomActivityFactory**)，然後試著重新建立。</span><span class="sxs-lookup"><span data-stu-id="58355-315">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="58355-316">按一下 [資源群組名稱] ，並選取現有的資源群組，或建立一個群組。</span><span class="sxs-lookup"><span data-stu-id="58355-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="58355-317">請確認您使用的是要在其中建立 Data Factory 的正確訂用帳戶和區域。</span><span class="sxs-lookup"><span data-stu-id="58355-317">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="58355-318">按一下 [新增 Data Factory] 刀鋒視窗上的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="58355-318">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="58355-319">您會看到 Data Factory 建立在 Azure 入口網站的 [儀表板]  中。</span><span class="sxs-lookup"><span data-stu-id="58355-319">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="58355-320">在 Data Factory 成功建立後，您會看到 Data Factory 頁面，顯示 Data Factory 的內容。</span><span class="sxs-lookup"><span data-stu-id="58355-320">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="58355-321">步驟 2：建立連結服務</span><span class="sxs-lookup"><span data-stu-id="58355-321">Step 2: Create linked services</span></span>
<span data-ttu-id="58355-322">連結服務會將資料存放區或計算服務連結至 Azure Data Factory。</span><span class="sxs-lookup"><span data-stu-id="58355-322">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="58355-323">在此步驟中，您會將 **Azure 儲存體**帳戶和 **Azure Batch** 帳戶連結到 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="58355-323">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="58355-324">建立 Azure 儲存體連結服務</span><span class="sxs-lookup"><span data-stu-id="58355-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="58355-325">按一下 **CustomActivityFactory** 的 [DATA FACTORY] 刀鋒視窗上的 [作者和部署] 圖格。</span><span class="sxs-lookup"><span data-stu-id="58355-325">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="58355-326">您會看到 [Data Factory 編輯器]。</span><span class="sxs-lookup"><span data-stu-id="58355-326">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="58355-327">在命令列上按一下 [新增資料儲存區]，然後選擇 [Azure 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="58355-327">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="58355-328">在編輯器中，您應該會看到用來建立 Azure 儲存體連結服務的 JSON 指令碼。</span><span class="sxs-lookup"><span data-stu-id="58355-328">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="58355-329">以您的 Azure 儲存體帳戶名稱取代**帳戶名稱**，並以 Azure 儲存體帳戶的存取金鑰取代**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="58355-329">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="58355-330">若要了解如何取得儲存體存取金鑰，請參閱 [檢視、複製和重新產生儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="58355-330">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="58355-331">按一下命令列的 [部署]  ，部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="58355-331">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="58355-332">建立 Azure Batch 連結服務</span><span class="sxs-lookup"><span data-stu-id="58355-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="58355-333">在此步驟中，您會為您的 **Azure Batch** 帳戶建立用來執行 Data Factory 自訂活動的連結服務。</span><span class="sxs-lookup"><span data-stu-id="58355-333">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="58355-334">在命令列上按一下 [新增計算]，然後選擇 [Azure Batch]。</span><span class="sxs-lookup"><span data-stu-id="58355-334">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="58355-335">您應該會在編輯器中看到用來建立 Azure Batch 連結服務的 JSON 指令碼。</span><span class="sxs-lookup"><span data-stu-id="58355-335">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="58355-336">在 JSON 指令碼中：</span><span class="sxs-lookup"><span data-stu-id="58355-336">In the JSON script:</span></span>

   1. <span data-ttu-id="58355-337">使用您的 Azure Batch 帳戶名稱來取代 **帳戶名稱** 。</span><span class="sxs-lookup"><span data-stu-id="58355-337">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="58355-338">使用 Azure Batch 帳戶的存取金鑰來取代 **存取金鑰** 。</span><span class="sxs-lookup"><span data-stu-id="58355-338">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="58355-339">針對 **poolName** 屬性輸入集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="58355-339">Enter the ID of the pool for the **poolName** property**.**</span></span> <span data-ttu-id="58355-340">您可以針對此屬性指定集區名稱或集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="58355-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="58355-341">針對 **batchUri** JSON 屬性，輸入 Batch URI。</span><span class="sxs-lookup"><span data-stu-id="58355-341">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="58355-342">[Azure Batch 帳戶] 刀鋒視窗中的 **URL** 格式如下：\<accountname\>.\<region\>.batch.azure.com。針對 JSON 中的 **batchUri** 屬性，您必須從該 URL **移除 "accountname"**</span><span class="sxs-lookup"><span data-stu-id="58355-342">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com. For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="58355-343">。</span><span class="sxs-lookup"><span data-stu-id="58355-343">from the URL.</span></span> <span data-ttu-id="58355-344">範例：`"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="58355-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="58355-345">針對 **poolName** 屬性，您也可以指定該集區的 ID，而非集區名稱。</span><span class="sxs-lookup"><span data-stu-id="58355-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="58355-346">與支援 HDInsight 的情況不同，Data Factory 服務不支援 Azure Batch 的隨選選項。</span><span class="sxs-lookup"><span data-stu-id="58355-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="58355-347">您只能使用 Azure Data Factory 中自己的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="58355-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="58355-348">指定作業系統系列設定的 **StorageLinkedService** for the **StorageLinkedService** 。</span><span class="sxs-lookup"><span data-stu-id="58355-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="58355-349">您已在前述步驟中建立此連結服務。</span><span class="sxs-lookup"><span data-stu-id="58355-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="58355-350">此儲存體會做為檔案和記錄檔的預備區域。</span><span class="sxs-lookup"><span data-stu-id="58355-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="58355-351">按一下命令列的 [部署]  ，部署連結服務。</span><span class="sxs-lookup"><span data-stu-id="58355-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="58355-352">步驟 3：建立資料集</span><span class="sxs-lookup"><span data-stu-id="58355-352">Step 3: Create datasets</span></span>
<span data-ttu-id="58355-353">在此步驟中，您會建立資料集來代表輸入和輸出資料。</span><span class="sxs-lookup"><span data-stu-id="58355-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="58355-354">建立輸入資料集</span><span class="sxs-lookup"><span data-stu-id="58355-354">Create input dataset</span></span>
1. <span data-ttu-id="58355-355">在 Data Factory 的 [編輯器] 中，按一下工具列上的 [新增資料集] 按鈕，然後從下拉式功能表中選取 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="58355-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="58355-356">使用下列 JSON 程式碼片段取代右窗格中的 JSON：</span><span class="sxs-lookup"><span data-stu-id="58355-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="58355-357">您稍後會在本逐步解說建立管線，開始時間為：2015-11-16T00:00:00Z，而結束時間為：2015-11-16T05:00:00Z。</span><span class="sxs-lookup"><span data-stu-id="58355-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="58355-358">排程為**每小時**產生，因此會有 5 個輸入/輸出配量 (在 **00**:00:00 -\> **05**:00:00 之間)。</span><span class="sxs-lookup"><span data-stu-id="58355-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="58355-359">輸入資料集的 **frequency** 和 **interval** 設定為 **Hour** 和 **1**，這表示每小時皆可使用輸入配量。</span><span class="sxs-lookup"><span data-stu-id="58355-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="58355-360">以下是每個配量的開始時間，由上述 JSON 程式碼片段中的 **SliceStart** 系統變數代表。</span><span class="sxs-lookup"><span data-stu-id="58355-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="58355-361">**配量**</span><span class="sxs-lookup"><span data-stu-id="58355-361">**Slice**</span></span> | <span data-ttu-id="58355-362">**開始時間**</span><span class="sxs-lookup"><span data-stu-id="58355-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="58355-363">1</span><span class="sxs-lookup"><span data-stu-id="58355-363">1</span></span>         | <span data-ttu-id="58355-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="58355-365">2</span><span class="sxs-lookup"><span data-stu-id="58355-365">2</span></span>         | <span data-ttu-id="58355-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="58355-367">3</span><span class="sxs-lookup"><span data-stu-id="58355-367">3</span></span>         | <span data-ttu-id="58355-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="58355-369">4</span><span class="sxs-lookup"><span data-stu-id="58355-369">4</span></span>         | <span data-ttu-id="58355-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="58355-371">5</span><span class="sxs-lookup"><span data-stu-id="58355-371">5</span></span>         | <span data-ttu-id="58355-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="58355-373">**FolderPath** 是使用配量開始時間 (**SliceStart**) 的年、月、日和小時部分來計算的。</span><span class="sxs-lookup"><span data-stu-id="58355-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="58355-374">因此，輸入資料夾對應至配量的方式如下。</span><span class="sxs-lookup"><span data-stu-id="58355-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="58355-375">**配量**</span><span class="sxs-lookup"><span data-stu-id="58355-375">**Slice**</span></span> | <span data-ttu-id="58355-376">**開始時間**</span><span class="sxs-lookup"><span data-stu-id="58355-376">**Start time**</span></span>          | <span data-ttu-id="58355-377">**輸入資料夾**</span><span class="sxs-lookup"><span data-stu-id="58355-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="58355-378">1</span><span class="sxs-lookup"><span data-stu-id="58355-378">1</span></span>         | <span data-ttu-id="58355-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="58355-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="58355-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="58355-381">2</span><span class="sxs-lookup"><span data-stu-id="58355-381">2</span></span>         | <span data-ttu-id="58355-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="58355-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="58355-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="58355-384">3</span><span class="sxs-lookup"><span data-stu-id="58355-384">3</span></span>         | <span data-ttu-id="58355-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="58355-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="58355-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="58355-387">4</span><span class="sxs-lookup"><span data-stu-id="58355-387">4</span></span>         | <span data-ttu-id="58355-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="58355-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="58355-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="58355-390">5</span><span class="sxs-lookup"><span data-stu-id="58355-390">5</span></span>         | <span data-ttu-id="58355-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="58355-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="58355-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="58355-393">按一下工具列上的 [部署]，以建立並部署 **InputDataset** 資料表。</span><span class="sxs-lookup"><span data-stu-id="58355-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="58355-394">建立輸出資料集</span><span class="sxs-lookup"><span data-stu-id="58355-394">Create output dataset</span></span>
<span data-ttu-id="58355-395">在此步驟中，您會建立屬於 AzureBlob 類型的另一個資料集，來代表輸出資料。</span><span class="sxs-lookup"><span data-stu-id="58355-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="58355-396">在 Data Factory 的 [編輯器] 中，按一下工具列上的 [新增資料集] 按鈕，然後從下拉式功能表中選取 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="58355-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="58355-397">使用下列 JSON 程式碼片段取代右窗格中的 JSON：</span><span class="sxs-lookup"><span data-stu-id="58355-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="58355-398">為每個輸入配量產生輸出 blob/檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="58355-399">以下是為每個配量命名輸出檔案的方式。</span><span class="sxs-lookup"><span data-stu-id="58355-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="58355-400">所有的輸出檔案會產生於一個輸出資料夾中：`mycontainer\\outputfolder`。</span><span class="sxs-lookup"><span data-stu-id="58355-400">All the output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="58355-401">**配量**</span><span class="sxs-lookup"><span data-stu-id="58355-401">**Slice**</span></span> | <span data-ttu-id="58355-402">**開始時間**</span><span class="sxs-lookup"><span data-stu-id="58355-402">**Start time**</span></span>          | <span data-ttu-id="58355-403">**輸出檔案**</span><span class="sxs-lookup"><span data-stu-id="58355-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="58355-404">1</span><span class="sxs-lookup"><span data-stu-id="58355-404">1</span></span>         | <span data-ttu-id="58355-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="58355-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="58355-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="58355-407">2</span><span class="sxs-lookup"><span data-stu-id="58355-407">2</span></span>         | <span data-ttu-id="58355-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="58355-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="58355-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="58355-410">3</span><span class="sxs-lookup"><span data-stu-id="58355-410">3</span></span>         | <span data-ttu-id="58355-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="58355-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="58355-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="58355-413">4</span><span class="sxs-lookup"><span data-stu-id="58355-413">4</span></span>         | <span data-ttu-id="58355-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="58355-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="58355-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="58355-416">5</span><span class="sxs-lookup"><span data-stu-id="58355-416">5</span></span>         | <span data-ttu-id="58355-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="58355-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="58355-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="58355-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="58355-419">請記得，輸入資料夾 (例如：2015-11-16-00) 中的所有檔案，都是開始時間為 2015-11-16-00 之配量的一部分。</span><span class="sxs-lookup"><span data-stu-id="58355-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="58355-420">處理此配量時，自訂活動會掃描每個檔案，並利用搜尋詞彙 (“Microsoft”) 的出現次數在輸出檔案中產生資料行。</span><span class="sxs-lookup"><span data-stu-id="58355-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="58355-421">如果資料夾 2015-11-16-00 中有三個檔案，則輸出檔案中會有三行：2015-11-16-00.txt。</span><span class="sxs-lookup"><span data-stu-id="58355-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="58355-422">按一下工具列上的 [部署]，以建立並部署 **OutputDataset**。</span><span class="sxs-lookup"><span data-stu-id="58355-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="58355-423">步驟 4：建立並執行使用自訂活動的管線</span><span class="sxs-lookup"><span data-stu-id="58355-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="58355-424">在此步驟中，您會建立具有一個活動的管線，也就是您先前建立的自訂活動。</span><span class="sxs-lookup"><span data-stu-id="58355-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58355-425">如果尚未將 **file.txt** 上傳至 blob 容器中的輸入資料夾，請先執行此動作，再建立管線。</span><span class="sxs-lookup"><span data-stu-id="58355-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="58355-426">在管線 JSON 中，**IsPaused** 屬性會設定為 false，使管線會在**開始**日期到達後立即執行。</span><span class="sxs-lookup"><span data-stu-id="58355-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="58355-427">在 Data Factory 編輯器中，按一下工具列上的 [ **新增管線** ]。</span><span class="sxs-lookup"><span data-stu-id="58355-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="58355-428">如果看不到此命令，請按一下 [...] (省略符號) 就可看到。</span><span class="sxs-lookup"><span data-stu-id="58355-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="58355-429">使用下列 JSON 指令碼取代右窗格中的 JSON︰</span><span class="sxs-lookup"><span data-stu-id="58355-429">Replace the JSON in the right pane with the following JSON script:</span></span>

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
   <span data-ttu-id="58355-430">請注意下列幾點：</span><span class="sxs-lookup"><span data-stu-id="58355-430">Note the following points:</span></span>

   * <span data-ttu-id="58355-431">管線中只有一個活動，且其類型為： **DotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="58355-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="58355-432">**AssemblyName** 設定為 DLL 的名稱：**MyDotNetActivity.dll**。</span><span class="sxs-lookup"><span data-stu-id="58355-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="58355-433">**EntryPoint** 設定為 **MyDotNetActivityNS.MyDotNetActivity**。</span><span class="sxs-lookup"><span data-stu-id="58355-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="58355-434">在您的程式碼中，它基本上是 \<namespace\>.\<classname\>。</span><span class="sxs-lookup"><span data-stu-id="58355-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="58355-435">**PackageLinkedService** 設為 **StorageLinkedService**，會指向包含自訂活動 zip 檔案的 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="58355-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="58355-436">如果您將不同的 Azure 儲存體帳戶用於輸入/輸出檔案和自訂活動 zip 檔案，您必須建立另一個 Azure 儲存體連結服務。</span><span class="sxs-lookup"><span data-stu-id="58355-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="58355-437">本文假設您使用相同的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="58355-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="58355-438">**PackageFile** 設定為 **customactivitycontainer/MyDotNetActivity.zip**。</span><span class="sxs-lookup"><span data-stu-id="58355-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="58355-439">其格式為：\<containerforthezip\>/\<nameofthezip.zip\>。</span><span class="sxs-lookup"><span data-stu-id="58355-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="58355-440">自訂活動會採用 **InputDataset** 做為輸入和 **OutputDataset** 做為輸出。</span><span class="sxs-lookup"><span data-stu-id="58355-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="58355-441">自訂活動的 **linkedServiceName** 屬性會指向 **AzureBatchLinkedService**，這會告知 Azure Data Factory 自訂活動必須在 Azure Batch 上執行。</span><span class="sxs-lookup"><span data-stu-id="58355-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="58355-442">**並行** 設定很重要。</span><span class="sxs-lookup"><span data-stu-id="58355-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="58355-443">如果您使用預設值 1，則即使您在 Azure Batch 集區中有 2 個或更多計算節點，配量仍會逐一進行處理。</span><span class="sxs-lookup"><span data-stu-id="58355-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="58355-444">因此，您將無法使用 Azure Batch 的平行處理功能。</span><span class="sxs-lookup"><span data-stu-id="58355-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="58355-445">如果您將 **並行** 設定為較高的值 (例如 2)，這表示可以同時處理 2 個配量 (對應於 Azure Batch 中的 2 個工作)，在此情況下，將會同時使用 Azure Batch 集區中的兩個 VM。</span><span class="sxs-lookup"><span data-stu-id="58355-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="58355-446">因此，請適當設定並行屬性。</span><span class="sxs-lookup"><span data-stu-id="58355-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="58355-447">根據預設，無論何時，一個工作 (配量) 都只會在一個 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="58355-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="58355-448">原因是 Azure Batch 集區的 [每個 VM 的工作數上限]  預設為 1。</span><span class="sxs-lookup"><span data-stu-id="58355-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="58355-449">根據必要條件，您在建立集區時將此屬性設定為 2，因此可以同時在 VM 上執行兩個 Data Factory 配量。</span><span class="sxs-lookup"><span data-stu-id="58355-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="58355-450">**isPaused** 屬性預設為 false。</span><span class="sxs-lookup"><span data-stu-id="58355-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="58355-451">在此範例中，管線會立即執行，因為配量已在過去開始。</span><span class="sxs-lookup"><span data-stu-id="58355-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="58355-452">您可以將此屬性設為 true，以暫停管線，並將其設回 false，以重新啟動。</span><span class="sxs-lookup"><span data-stu-id="58355-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="58355-453">**start** 時間和 **end**時間相差 5 小時，而配量會每小時產生，因此管線會產生 5 個配量。</span><span class="sxs-lookup"><span data-stu-id="58355-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="58355-454">按一下命令列上的 [部署]  ，部署管線。</span><span class="sxs-lookup"><span data-stu-id="58355-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="58355-455">步驟 5：測試管線</span><span class="sxs-lookup"><span data-stu-id="58355-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="58355-456">在此步驟中，您會將檔案放置在輸入資料夾中，以測試管線。</span><span class="sxs-lookup"><span data-stu-id="58355-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="58355-457">首先，我們以每一個輸入資料夾含有一個檔案的方式來測試管線。</span><span class="sxs-lookup"><span data-stu-id="58355-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="58355-458">在 Azure 入口網站的 [Data Factory] 刀鋒視窗中，按一下 [圖表] 。</span><span class="sxs-lookup"><span data-stu-id="58355-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="58355-459">在圖表檢視中，按兩下輸入資料集：**InputDataset**。</span><span class="sxs-lookup"><span data-stu-id="58355-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="58355-460">您應會看到 **InputDataset** 刀鋒視窗中已包含所有的 5 個配量。</span><span class="sxs-lookup"><span data-stu-id="58355-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="58355-461">請留意每個配量的 [配量開始時間] 和 [配量結束時間]。</span><span class="sxs-lookup"><span data-stu-id="58355-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="58355-462">在 [圖表檢視] 中，現在按一下 [OutputDataset]。</span><span class="sxs-lookup"><span data-stu-id="58355-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="58355-463">如果已產生 5 個輸出配量，您應該會看到它們都處於就緒狀態。</span><span class="sxs-lookup"><span data-stu-id="58355-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="58355-464">使用 Azure 入口網站檢視與**配量**相關聯的**工作**，並查看每個配量在哪個 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="58355-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="58355-465">請參閱 [Data Factory 和 Batch 整合](#data-factory-and-batch-integration) 一節，以取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="58355-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="58355-466">在您的 Azure Blob 儲存體中，您應會在 `mycontainer` 的 `outputfolder` 中看見輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-466">You should see the output files in the `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="58355-467">您應會看見五個輸出檔案，每個輸入配量各一個。</span><span class="sxs-lookup"><span data-stu-id="58355-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="58355-468">每個輸出檔案應會有類似下列輸出的內容：</span><span class="sxs-lookup"><span data-stu-id="58355-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="58355-469">下圖說明 Data Factory 配量如何對應至 Azure Batch 中的工作。</span><span class="sxs-lookup"><span data-stu-id="58355-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="58355-470">在此範例中，一個配量只有一個執行。</span><span class="sxs-lookup"><span data-stu-id="58355-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="58355-471">現在，我們要以一個資料夾包含多個檔案的方式來試試。</span><span class="sxs-lookup"><span data-stu-id="58355-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="58355-472">使用與資料夾 **2015-11-06-01**中的 file.txt 相同的內容，建立檔案 **file2.txt**、**file3.txt**、**file4.txt** 和 **file5.txt**。</span><span class="sxs-lookup"><span data-stu-id="58355-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="58355-473">在輸出資料夾中，**刪除**輸出檔案：**2015-11-16-01.txt**。</span><span class="sxs-lookup"><span data-stu-id="58355-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="58355-474">現在，在 **OutputDataset** 刀鋒視窗中，以滑鼠右鍵按一下 [配量開始時間] 設定為 **11/16/2015 01:00:00 AM** 的配量，然後按一下 [執行]，以重新執行/重新處理配量。</span><span class="sxs-lookup"><span data-stu-id="58355-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="58355-475">現在，配量會有 5 個檔案，而不是 1 個檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-475">Now, the slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="58355-476">在配量執行完成，且其狀態為 [就緒] 之後，在您 Blob 儲存體之 `mycontainer` 的 `outputfolder` 中驗證此配量的輸出檔案 (**2015-11-16-01.txt**) 中的內容。</span><span class="sxs-lookup"><span data-stu-id="58355-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="58355-477">配量的每個檔案應該都有一行。</span><span class="sxs-lookup"><span data-stu-id="58355-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="58355-478">如果您未先刪除輸出檔案 2015-11-16-01.txt，即以 5 個輸入檔案來嘗試，您會看到先前的配量執行有一行，而目前的配量執行有五行。</span><span class="sxs-lookup"><span data-stu-id="58355-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="58355-479">根據預設，內容會附加至已存在的輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="58355-480">Data Factory 和 Batch 整合</span><span class="sxs-lookup"><span data-stu-id="58355-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="58355-481">Data Factory 服務會在 Azure Batch 中建立作業，其名為：`adf-poolname:job-xxx`。</span><span class="sxs-lookup"><span data-stu-id="58355-481">The Data Factory service creates a job in Azure Batch with the name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - Batch 作業](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="58355-483">配量的每個活動執行都會在作業中建立一個工作。</span><span class="sxs-lookup"><span data-stu-id="58355-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="58355-484">如果有 10 個配量就緒可供處理，作業中會建立 10 個工作。</span><span class="sxs-lookup"><span data-stu-id="58355-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="58355-485">如果您在集區中有多個計算結點，您可以同時執行多個配量。</span><span class="sxs-lookup"><span data-stu-id="58355-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="58355-486">如果每個計算結點的工作上限設為 > 1，則相同的計算上可以執行多個配量。</span><span class="sxs-lookup"><span data-stu-id="58355-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="58355-487">此範例中有 5 個配量，所以 Azure Batch 中有 5 個工作。</span><span class="sxs-lookup"><span data-stu-id="58355-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="58355-488">在 Azure Data Factory 中的管線 JSON 中將**並行**設定為 **5**，並且在具有 **2** 個 VM 的 Azure Batch 集區中將 [每個 VM 的工作數上限] 設定為 **2**，工作會執行得很快 (請檢查工作的開始和結束時間)。</span><span class="sxs-lookup"><span data-stu-id="58355-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="58355-489">使用入口網站來檢視與 **配量** 相關聯的 Batch 作業及其工作，並查看每個配量在哪個 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="58355-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - Batch 作業工作](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="58355-491">偵錯管線</span><span class="sxs-lookup"><span data-stu-id="58355-491">Debug the pipeline</span></span>
<span data-ttu-id="58355-492">偵錯包含一些基本技術：</span><span class="sxs-lookup"><span data-stu-id="58355-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="58355-493">如果輸入配量不是設定為 [就緒] ，請確認輸入資料夾結構正確，且 file.txt 存在於輸入資料夾中。</span><span class="sxs-lookup"><span data-stu-id="58355-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="58355-494">在自訂活動的 **Execute** 方法中，使用可協助您針對問題進行疑難排解的 **IActivityLogger** 物件記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="58355-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="58355-495">記錄的訊息會顯示在 user\_0.log 檔案中。</span><span class="sxs-lookup"><span data-stu-id="58355-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="58355-496">在 [OutputDataset] 刀鋒視窗中，按一下配量，以查看該配量的 [資料配量] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="58355-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="58355-497">您會看到該配量的 [活動執行]。</span><span class="sxs-lookup"><span data-stu-id="58355-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="58355-498">您會看到一個為該配量執行的活動。</span><span class="sxs-lookup"><span data-stu-id="58355-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="58355-499">如果您按一下命令列中的 [執行]，您可以為相同的配量啟動另一個活動執行。</span><span class="sxs-lookup"><span data-stu-id="58355-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="58355-500">當您按一下活動執行，您會看到包含記錄檔清單的 [活動執行詳細資料]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="58355-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="58355-501">您會在 **user\_0.log** 檔案中看到記錄的訊息。</span><span class="sxs-lookup"><span data-stu-id="58355-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="58355-502">發生錯誤時，您會看到三個活動執行，因為管線/活動 JSON 中的重試計數設定為 3。</span><span class="sxs-lookup"><span data-stu-id="58355-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="58355-503">當您按一下活動執行，您會看到您可以檢閱的記錄檔來疑難排解錯誤。</span><span class="sxs-lookup"><span data-stu-id="58355-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="58355-504">在記錄檔清單中，按一下 [user-0.log] **IActivityLogger.Write**方法的結果。</span><span class="sxs-lookup"><span data-stu-id="58355-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="58355-505">在右窗格中的是使用 **IActivityLogger.Write** 方法的結果。</span><span class="sxs-lookup"><span data-stu-id="58355-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="58355-506">檢查 system-0.log 是否有任何系統錯誤訊息和例外狀況。</span><span class="sxs-lookup"><span data-stu-id="58355-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="58355-507">在 zip 檔案中包含 **PDB** 檔案，錯誤詳細資料才會在錯誤發生時包含**呼叫堆疊**等資訊。</span><span class="sxs-lookup"><span data-stu-id="58355-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="58355-508">自訂活動之 zip 檔案中的所有檔案都必須位於 **最上層** 且不包含任何子資料夾。</span><span class="sxs-lookup"><span data-stu-id="58355-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="58355-509">確認 **assemblyName** (MyDotNetActivity.dll)、**entryPoint** (MyDotNetActivityNS.MyDotNetActivity)、**packageFile** (customactivitycontainer/MyDotNetActivity.zip) 和 **packageLinkedService** (應指向包含 zip 檔案的 Azure blob 儲存體) 都設為正確的值。</span><span class="sxs-lookup"><span data-stu-id="58355-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="58355-510">如果您修正錯誤，並想要重新處理配量，請以滑鼠右鍵按一下 [OutputDataset] 刀鋒視窗中的配量，然後按一下 [執行]。</span><span class="sxs-lookup"><span data-stu-id="58355-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="58355-511">您會在 Azure Blob 儲存體中看到一個**容器**，名為：`adfjobs`。</span><span class="sxs-lookup"><span data-stu-id="58355-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="58355-512">此容器並不會自動刪除，但您可在完成解決方案的測試後安全地加以刪除。</span><span class="sxs-lookup"><span data-stu-id="58355-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="58355-513">同樣地，Data Factory 解決方案也會建立 Azure Batch **作業**，名為：`adf-\<pool ID/name\>:job-0000000001`。</span><span class="sxs-lookup"><span data-stu-id="58355-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="58355-514">您可以在測試解決方案之後刪除此作業 (如果您要的話)。</span><span class="sxs-lookup"><span data-stu-id="58355-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="58355-515">自訂活動不會使用來自您套件的 **app.config** 檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="58355-516">因此，如果您的程式碼會從組態檔讀取任何連接字串，則在執行階段沒有作用。</span><span class="sxs-lookup"><span data-stu-id="58355-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="58355-517">最佳做法是使用 Azure Batch 將所有祕密存放在 **Azure KeyVault** 中、使用以憑證為基礎的服務主體來保護金鑰保存庫，然後將憑證發佈至 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="58355-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="58355-518">接著，.NET 自訂活動便可以在執行階段從 KeyVault 存取密碼。</span><span class="sxs-lookup"><span data-stu-id="58355-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="58355-519">此解決方案是一般解決方案，可以擴展至任何類型的祕密，不僅限於連接字串。</span><span class="sxs-lookup"><span data-stu-id="58355-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="58355-520">此外，也有較簡單的因應措施 (但並非最佳做法)︰您可以建立一個帶有連接字串設定的 **Azure SQL 連結服務** 、建立一個使用該連結服務的資料集，然後將該資料集以虛擬輸入資料集的形式鏈結至自訂 .NET 活動。</span><span class="sxs-lookup"><span data-stu-id="58355-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="58355-521">接著，您便可以在自訂活動程式碼中存取連結服務的連接字串，並且這在執行階段應該能夠發揮作用。</span><span class="sxs-lookup"><span data-stu-id="58355-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="58355-522">擴充範例</span><span class="sxs-lookup"><span data-stu-id="58355-522">Extend the sample</span></span>
<span data-ttu-id="58355-523">您可以擴充此範例，以深入了解 Azure Data Factory 和 Azure Batch 的功能。</span><span class="sxs-lookup"><span data-stu-id="58355-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="58355-524">例如，若要處理不同時間範圍的配量，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="58355-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="58355-525">在 `inputfolder`中新增下列子資料夾，然後將輸入檔案放入這些資料夾中：2015-11-16-05、2015-11-16-06、201-11-16-07、2011-11-16-08、2015-11-16-09。</span><span class="sxs-lookup"><span data-stu-id="58355-525">Add the following subfolders in the `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="58355-526">將管線的結束時間從 `2015-11-16T05:00:00Z` 變更為 `2015-11-16T10:00:00Z`。</span><span class="sxs-lookup"><span data-stu-id="58355-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="58355-527">在 [圖表檢視] 中，按兩下 **InputDataset**，並確認輸入配量已就緒。</span><span class="sxs-lookup"><span data-stu-id="58355-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="58355-528">按兩下 **OuptutDataset** ，以查看輸出配量的狀態。</span><span class="sxs-lookup"><span data-stu-id="58355-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="58355-529">如果它們都處於 [就緒] 狀態，請在輸出資料夾中查看輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="58355-529">If they are in Ready state, check the output folder for the output files.</span></span>
2. <span data-ttu-id="58355-530">增加或減少**並行**設定，以了解它對您解決方案的效能有何影響，尤其是在 Azure Batch 上執行的處理。</span><span class="sxs-lookup"><span data-stu-id="58355-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="58355-531">(請參閱「步驟 4：建立並執行管線」，以進一步了解**並行**設定。)</span><span class="sxs-lookup"><span data-stu-id="58355-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="58355-532">建立 [每個 VM 的工作數上限] 較低/較高的集區。</span><span class="sxs-lookup"><span data-stu-id="58355-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="58355-533">若要使用您所建立的新集區，請更新 Data Factory 解決方案中的 Azure Batch 連結服務。</span><span class="sxs-lookup"><span data-stu-id="58355-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="58355-534">(請參閱「步驟 4：建立並執行管線」，以進一步了解 [每個 VM 的工作數上限] 設定。)</span><span class="sxs-lookup"><span data-stu-id="58355-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="58355-535">建立具有 **自動調整** 功能的 Azure Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="58355-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="58355-536">自動調整 Azure Batch 集區中的計算節點就是動態調整應用程式所使用的處理能力。</span><span class="sxs-lookup"><span data-stu-id="58355-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="58355-537">這裡的範例公式會有下列行為：當集區一開始建立時，它會以 1 部 VM 啟動。</span><span class="sxs-lookup"><span data-stu-id="58355-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="58355-538">$PendingTasks 計量會定義執行中 + 作用中 (已排入佇列) 狀態的工作數目。</span><span class="sxs-lookup"><span data-stu-id="58355-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="58355-539">公式會尋找過去 180 秒內的平均擱置中工作數目，並據以設定 TargetDedicated。</span><span class="sxs-lookup"><span data-stu-id="58355-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="58355-540">它會確保 TargetDedicated 一律不會超過 25 部 VM。</span><span class="sxs-lookup"><span data-stu-id="58355-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="58355-541">因此，當提交新工作時，集區會自動成長而且工作會完成，VM 會依序成為可用，而且自動調整規模功能會壓縮那些 VM。</span><span class="sxs-lookup"><span data-stu-id="58355-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="58355-542">您可以視需要調整 startingNumberOfVMs 及 maxNumberofVMs。</span><span class="sxs-lookup"><span data-stu-id="58355-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="58355-543">自動調整公式：</span><span class="sxs-lookup"><span data-stu-id="58355-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="58355-544">如需詳細資訊，請參閱 [自動調整 Azure Batch 集區中的計算節點](../batch/batch-automatic-scaling.md) 。</span><span class="sxs-lookup"><span data-stu-id="58355-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="58355-545">如果集區使用預設的 [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)，Batch 服務在執行自訂活動之前，可能需要 15-30 分鐘的時間準備 VM。</span><span class="sxs-lookup"><span data-stu-id="58355-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="58355-546">如果集區使用不同的 autoScaleEvaluationInterval，Batch 服務可能需要 autoScaleEvaluationInterval + 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="58355-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="58355-547">在範例解決方案中，**Execute** 方法會叫用可處理輸入資料配量以產生輸出資料配量的 **Calculate** 方法。</span><span class="sxs-lookup"><span data-stu-id="58355-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="58355-548">您可以自行撰寫方法來處理輸入資料，然後呼叫您自己的方法，而取代 Execute 方法中的 Calculate 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="58355-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="58355-549">後續步驟：取用資料</span><span class="sxs-lookup"><span data-stu-id="58355-549">Next steps: Consume the data</span></span>
<span data-ttu-id="58355-550">處理資料之後，您可以使用 **Microsoft Power BI** 之類的線上工具來取用資料。</span><span class="sxs-lookup"><span data-stu-id="58355-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="58355-551">以下連結可協助您了解 Power BI，以及如何在 Azure 中加以使用：</span><span class="sxs-lookup"><span data-stu-id="58355-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="58355-552">在 Power BI 中探索資料集</span><span class="sxs-lookup"><span data-stu-id="58355-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="58355-553">開始使用 Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="58355-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="58355-554">重新整理 Power BI 中的資料</span><span class="sxs-lookup"><span data-stu-id="58355-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="58355-555">Azure 和 Power BI - 基本概觀</span><span class="sxs-lookup"><span data-stu-id="58355-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="58355-556">參考</span><span class="sxs-lookup"><span data-stu-id="58355-556">References</span></span>
* [<span data-ttu-id="58355-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="58355-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="58355-558">Azure Data Factory 服務簡介</span><span class="sxs-lookup"><span data-stu-id="58355-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="58355-559">開始使用 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="58355-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="58355-560">在 Azure 資料處理站管線中使用自訂活動</span><span class="sxs-lookup"><span data-stu-id="58355-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="58355-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="58355-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="58355-562">Azure Batch 的基本概念</span><span class="sxs-lookup"><span data-stu-id="58355-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="58355-563">Azure Batch 功能概觀</span><span class="sxs-lookup"><span data-stu-id="58355-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="58355-564">在 Azure 入口網站中建立和管理 Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="58355-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="58355-565">開始使用 Azure Batch 程式庫 .NET</span><span class="sxs-lookup"><span data-stu-id="58355-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
