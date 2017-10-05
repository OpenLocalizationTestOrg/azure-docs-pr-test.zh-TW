---
title: "使用 SSIS 連接器從 Azure Blob 儲存體來回移動資料 | Microsoft Docs"
description: "使用 SSIS 連接器從 Azure Blob 儲存體來回移動資料。"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 575beaea5443919bd9728016bf100b43de8e4aab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-or-from-azure-blob-storage-using-ssis-connectors"></a><span data-ttu-id="6276f-103">使用 SSIS 連接器從 Azure Blob 儲存體來回移動資料</span><span class="sxs-lookup"><span data-stu-id="6276f-103">Move data to or from Azure Blob Storage using SSIS connectors</span></span>
<span data-ttu-id="6276f-104">[SQL Server Integration Services Feature Pack for Azure](https://msdn.microsoft.com/library/mt146770.aspx) 中的元件可供連線至 Azure、在 Azure 與內部部署資源來源之間傳輸資料，以及處理儲存在 Azure 中的資料。</span><span class="sxs-lookup"><span data-stu-id="6276f-104">The [SQL Server Integration Services Feature Pack for Azure](https://msdn.microsoft.com/library/mt146770.aspx) provides components to connect to Azure, transfer data between Azure and on-premises data sources, and process data stored in Azure.</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="6276f-105">客戶將內部部署資料移至雲端後，便能從任何 Azure 服務存取該資料，以利用 Azure 技術套件的完整功能。</span><span class="sxs-lookup"><span data-stu-id="6276f-105">Once customers have moved on-premises data into the cloud, they can access it from any Azure service to leverage the full power of the suite of Azure technologies.</span></span> <span data-ttu-id="6276f-106">例如，可用在 Azure 機器學習服務或 HDInsight 叢集中。</span><span class="sxs-lookup"><span data-stu-id="6276f-106">It may be used, for example, in Azure Machine Learning or on an HDInsight cluster.</span></span>

<span data-ttu-id="6276f-107">這通常是 [SQL](machine-learning-data-science-process-sql-walkthrough.md) 與 [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) 逐步解說的第一步。</span><span class="sxs-lookup"><span data-stu-id="6276f-107">This is typically be the first step for the [SQL](machine-learning-data-science-process-sql-walkthrough.md) and [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) walkthroughs.</span></span>

<span data-ttu-id="6276f-108">有關使用 SSIS 完成混合式資料整合案例中常見業務需求的典型案例討論，請參閱 [使用 Azure 適用的 SQL Server 整合服務功能套件事半功倍](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) 部落格。</span><span class="sxs-lookup"><span data-stu-id="6276f-108">For a discussion of canonical scenarios that use SSIS to accomplish business needs common in hybrid data integration scenarios, see [Doing more with SQL Server Integration Services Feature Pack for Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.</span></span>

> [!NOTE]
> <span data-ttu-id="6276f-109">如需 Azure Blob 儲存體的完整介紹，請參閱 [Azure Blob 基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和 [Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6276f-109">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6276f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6276f-110">Prerequisites</span></span>
<span data-ttu-id="6276f-111">若要執行本文所述的工作，您必須有設好的 Azure 訂用帳戶與 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6276f-111">To perform the tasks described in this article, you must have an Azure subscription and an Azure storage account set up.</span></span> <span data-ttu-id="6276f-112">您必須知道您的 Azure 儲存體帳戶名稱與帳戶金鑰，才能上傳或下載資料。</span><span class="sxs-lookup"><span data-stu-id="6276f-112">You must know your Azure storage account name and account key to upload or download data.</span></span>

* <span data-ttu-id="6276f-113">若要設定 **Azure 訂用帳戶**，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6276f-113">To set up an **Azure subscription**, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6276f-114">如需建立 **儲存體帳戶** 以及取得帳戶和金鑰資訊的指示，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="6276f-114">For instructions on creating a **storage account** and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="6276f-115">若要使用 **SSIS 連接器**，您必須下載:</span><span class="sxs-lookup"><span data-stu-id="6276f-115">To use the **SSIS connectors**, you must download:</span></span>

* <span data-ttu-id="6276f-116">**SQL Server 2014 或 2016 標準版 (或更新版本)**：安裝包含 SQL Server 整合服務。</span><span class="sxs-lookup"><span data-stu-id="6276f-116">**SQL Server 2014 or 2016 Standard (or above)**: Install includes SQL Server Integration Services.</span></span>
* <span data-ttu-id="6276f-117">**適用於 Azure 的 Microsoft SQL Server 2014 或 2016 整合服務 Feature Pack**：您可以個別從 [SQL Server 2014 整合服務](http://www.microsoft.com/download/details.aspx?id=47366)和 [SQL Server 2016 整合服務頁面](https://www.microsoft.com/download/details.aspx?id=49492)下載。</span><span class="sxs-lookup"><span data-stu-id="6276f-117">**Microsoft SQL Server 2014 or 2016 Integration Services Feature Pack for Azure**: These can be downloaded, respectively, from the [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) and [SQL Server 2016 Integration Services](https://www.microsoft.com/download/details.aspx?id=49492) pages.</span></span>

> [!NOTE]
> <span data-ttu-id="6276f-118">SSIS 會隨同 SQL Server 安裝，但未包含在 Express 版本中。</span><span class="sxs-lookup"><span data-stu-id="6276f-118">SSIS is installed with SQL Server, but is not included in the Express version.</span></span> <span data-ttu-id="6276f-119">如需 SQL Server 各種版本中包含哪些應用程式的相關資訊，請參閱 [SQL Server 版本](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span><span class="sxs-lookup"><span data-stu-id="6276f-119">For information on what applications are included in various editions of SQL Server, see [SQL Server Editions](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span></span>
> 
> 

<span data-ttu-id="6276f-120">如需 SSIS 的訓練教材，請參閱 [SSIS 實務訓練](http://www.microsoft.com/download/details.aspx?id=20766)</span><span class="sxs-lookup"><span data-stu-id="6276f-120">For training materials on SSIS, see [Hands On Training for SSIS](http://www.microsoft.com/download/details.aspx?id=20766)</span></span>

<span data-ttu-id="6276f-121">如需如何使用 SISS 啟動與執行，以建置簡單擷取、轉換與載入 (ETL) 封裝的相關資訊，請參閱 [SSIS 教學課程：建立簡易 ETL 封裝](https://msdn.microsoft.com/library/ms169917.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6276f-121">For information on how to get up-and-running using SISS to build simple extraction, transformation, and load (ETL) packages, see [SSIS Tutorial: Creating a Simple ETL Package](https://msdn.microsoft.com/library/ms169917.aspx).</span></span>

## <a name="download-nyc-taxi-dataset"></a><span data-ttu-id="6276f-122">下載紐約計程車資料集</span><span class="sxs-lookup"><span data-stu-id="6276f-122">Download NYC Taxi dataset</span></span>
<span data-ttu-id="6276f-123">此處描述的範例使用供大眾使用的資料集 -- [紐約計程車路線](http://www.andresmh.com/nyctaxitrips/) 資料集。</span><span class="sxs-lookup"><span data-stu-id="6276f-123">The example described here use a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="6276f-124">此資料集收集了 2013 年紐約 1 億 7 千 3 百萬筆計程車行程資料。</span><span class="sxs-lookup"><span data-stu-id="6276f-124">The dataset consists of about 173 million taxi rides in NYC in the year 2013.</span></span> <span data-ttu-id="6276f-125">資料有兩種：路線詳細資料及車費資料。</span><span class="sxs-lookup"><span data-stu-id="6276f-125">There are two types of data: trip details data and fare data.</span></span> <span data-ttu-id="6276f-126">由於每個月都有一個檔案，因此總共有 24 個檔案，每個檔案未壓縮的大小約 2GB。</span><span class="sxs-lookup"><span data-stu-id="6276f-126">As there is a file for each month, we have 24 files in all, each of which is approximately 2GB uncompressed.</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="6276f-127">將資料上傳至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="6276f-127">Upload data to Azure blob storage</span></span>
<span data-ttu-id="6276f-128">為了使用 SSIS 功能封裝將資料從內部部署移至 Azure Blob 儲存體，我們使用 [**Azure Blob 上傳工作**](https://msdn.microsoft.com/library/mt146776.aspx)執行個體，如這裡所示：</span><span class="sxs-lookup"><span data-stu-id="6276f-128">To move data using the SSIS feature pack from on-premises to Azure blob storage, we use an instance of the [**Azure Blob Upload Task**](https://msdn.microsoft.com/library/mt146776.aspx), shown here:</span></span>

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

<span data-ttu-id="6276f-130">此工作使用的參數如下所述：</span><span class="sxs-lookup"><span data-stu-id="6276f-130">The parameters that the task uses are described here:</span></span>

| <span data-ttu-id="6276f-131">欄位</span><span class="sxs-lookup"><span data-stu-id="6276f-131">Field</span></span> | <span data-ttu-id="6276f-132">說明</span><span class="sxs-lookup"><span data-stu-id="6276f-132">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6276f-133">**AzureStorageConnection**</span><span class="sxs-lookup"><span data-stu-id="6276f-133">**AzureStorageConnection**</span></span> |<span data-ttu-id="6276f-134">指定現有的或建立新的 Azure 儲存體連線管理員，以參照 Azure 儲存體帳戶；該帳戶指向託管 Blob 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="6276f-134">Specifies an existing Azure Storage Connection Manager or creates a new one that refers to an Azure storage account that points to where the blob files are hosted.</span></span> |
| <span data-ttu-id="6276f-135">**BlobContainer**</span><span class="sxs-lookup"><span data-stu-id="6276f-135">**BlobContainer**</span></span> |<span data-ttu-id="6276f-136">指定會將上傳的檔案保存為 Blob 的 Blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="6276f-136">Specifies the name of the blob container that hold the uploaded files as blobs.</span></span> |
| <span data-ttu-id="6276f-137">**BlobDirectory**</span><span class="sxs-lookup"><span data-stu-id="6276f-137">**BlobDirectory**</span></span> |<span data-ttu-id="6276f-138">指定上傳的檔案會儲存在哪一個 Blob 目錄中以儲存成區塊 Blob。</span><span class="sxs-lookup"><span data-stu-id="6276f-138">Specifies the blob directory where the uploaded file is stored as a block blob.</span></span> <span data-ttu-id="6276f-139">Blob 目錄是虛擬的階層式結構。</span><span class="sxs-lookup"><span data-stu-id="6276f-139">The blob directory is a virtual hierarchical structure.</span></span> <span data-ttu-id="6276f-140">如果 Blob 已經存在，則會被取代。</span><span class="sxs-lookup"><span data-stu-id="6276f-140">If the blob already exists, it ia replaced.</span></span> |
| <span data-ttu-id="6276f-141">**LocalDirectory**</span><span class="sxs-lookup"><span data-stu-id="6276f-141">**LocalDirectory**</span></span> |<span data-ttu-id="6276f-142">指定包含要上傳的檔案的本機目錄。</span><span class="sxs-lookup"><span data-stu-id="6276f-142">Specifies the local directory that contains the files to be uploaded.</span></span> |
| <span data-ttu-id="6276f-143">**FileName**</span><span class="sxs-lookup"><span data-stu-id="6276f-143">**FileName**</span></span> |<span data-ttu-id="6276f-144">指定名稱篩選器以選取採用指定名稱模式的檔案。</span><span class="sxs-lookup"><span data-stu-id="6276f-144">Specifies a name filter to select files with the specified name pattern.</span></span> <span data-ttu-id="6276f-145">例如，MySheet\*.xls\* 包括如 MySheet001.xls 與 MySheetABC.xlsx 等檔案</span><span class="sxs-lookup"><span data-stu-id="6276f-145">For example, MySheet\*.xls\* includes files such as MySheet001.xls and MySheetABC.xlsx</span></span> |
| <span data-ttu-id="6276f-146">**TimeRangeFrom/TimeRangeTo**</span><span class="sxs-lookup"><span data-stu-id="6276f-146">**TimeRangeFrom/TimeRangeTo**</span></span> |<span data-ttu-id="6276f-147">指定時間範圍篩選器。</span><span class="sxs-lookup"><span data-stu-id="6276f-147">Specifies a time range filter.</span></span> <span data-ttu-id="6276f-148">會包含在 *TimeRangeFrom* 後和 *TimeRangeTo* 前修改的檔案。</span><span class="sxs-lookup"><span data-stu-id="6276f-148">Files modified after *TimeRangeFrom* and before *TimeRangeTo* are included.</span></span> |

> [!NOTE]
> <span data-ttu-id="6276f-149">**AzureStorageConnection** 認證必須更正且 **BlobContainer** 必須存在，才能嘗試傳輸。</span><span class="sxs-lookup"><span data-stu-id="6276f-149">The **AzureStorageConnection** credentials need to be correct and the **BlobContainer** must exist before the transfer is attempted.</span></span>
> 
> 

## <a name="download-data-from-azure-blob-storage"></a><span data-ttu-id="6276f-150">從 Azure Blob 儲存體下載資料</span><span class="sxs-lookup"><span data-stu-id="6276f-150">Download data from Azure blob storage</span></span>
<span data-ttu-id="6276f-151">若要透過 SSIS 將資料從 Azure Blob 儲存體下載到內部部署儲存體，請使用 [Azure Blob 上傳工作](https://msdn.microsoft.com/library/mt146779.aspx)的執行個體。</span><span class="sxs-lookup"><span data-stu-id="6276f-151">To download data from Azure blob storage to on-premises storage with SSIS, use an instance of the [Azure Blob Upload Task](https://msdn.microsoft.com/library/mt146779.aspx).</span></span>

## <a name="more-advanced-ssis-azure-scenarios"></a><span data-ttu-id="6276f-152">較進階的 SSIS-Azure 案例</span><span class="sxs-lookup"><span data-stu-id="6276f-152">More advanced SSIS-Azure scenarios</span></span>
<span data-ttu-id="6276f-153">SSIS 功能套件藉由將工作封裝在一起，處理更複雜的流程。</span><span class="sxs-lookup"><span data-stu-id="6276f-153">The SSIS feature pack allows for more complex flows to be handled by packaging tasks together.</span></span> <span data-ttu-id="6276f-154">例如，Blob 資料可直接饋送到 HDInsight 叢集，其輸出可以回頭下載到 Blob，然後下載到內部部署儲存體。</span><span class="sxs-lookup"><span data-stu-id="6276f-154">For example, the blob data could feed directly into an HDInsight cluster, whose output could be downloaded back to a blob and then to on-premises storage.</span></span> <span data-ttu-id="6276f-155">SSIS 可使用其他 SSIS 連接器在 HDInsight 叢集上執行 Hive 與 Pig 工作：</span><span class="sxs-lookup"><span data-stu-id="6276f-155">SSIS can run Hive and Pig jobs on an HDInsight cluster using additional SSIS connectors:</span></span>

* <span data-ttu-id="6276f-156">若要使用 SSIS 在 Azure HDInsight 叢集上執行 Hive 指令碼，請使用 [Azure HDInsight Hive 工作](https://msdn.microsoft.com/library/mt146771.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6276f-156">To run a Hive script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Hive Task](https://msdn.microsoft.com/library/mt146771.aspx).</span></span>
* <span data-ttu-id="6276f-157">若要使用 SSIS 在 Azure HDInsight 叢集上執行 Pig 指令碼，請使用 [Azure HDInsight Pig 工作](https://msdn.microsoft.com/library/mt146781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6276f-157">To run a Pig script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Pig Task](https://msdn.microsoft.com/library/mt146781.aspx).</span></span>

