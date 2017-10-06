---
title: "從 Azure Blob 儲存體使用 SSIS 連接器 aaaMove 資料 tooor |Microsoft 文件"
description: "移動資料 tooor 從 Azure Blob 儲存體使用 SSIS 連接器。"
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
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a><span data-ttu-id="ba48d-103">移動資料 tooor 從 Azure Blob 儲存體使用 SSIS 連接器</span><span class="sxs-lookup"><span data-stu-id="ba48d-103">Move data tooor from Azure Blob Storage using SSIS connectors</span></span>
<span data-ttu-id="ba48d-104">hello [SQL Server Integration Services 功能套件 azure](https://msdn.microsoft.com/library/mt146770.aspx)提供元件 tooconnect tooAzure 之間傳輸資料 Azure 和內部部署資料來源，以及儲存在 Azure 中的處理序資料。</span><span class="sxs-lookup"><span data-stu-id="ba48d-104">hello [SQL Server Integration Services Feature Pack for Azure](https://msdn.microsoft.com/library/mt146770.aspx) provides components tooconnect tooAzure, transfer data between Azure and on-premises data sources, and process data stored in Azure.</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="ba48d-105">一旦客戶已將內部部署資料移到 hello 的雲端，就可以從任何 Azure 服務 tooleverage hello 的完整功能的 Azure 技術的 hello 套件來進行存取。</span><span class="sxs-lookup"><span data-stu-id="ba48d-105">Once customers have moved on-premises data into hello cloud, they can access it from any Azure service tooleverage hello full power of hello suite of Azure technologies.</span></span> <span data-ttu-id="ba48d-106">例如，可用在 Azure 機器學習服務或 HDInsight 叢集中。</span><span class="sxs-lookup"><span data-stu-id="ba48d-106">It may be used, for example, in Azure Machine Learning or on an HDInsight cluster.</span></span>

<span data-ttu-id="ba48d-107">這通常是 hello 第一個步驟是 hello [SQL](machine-learning-data-science-process-sql-walkthrough.md)和[HDInsight](machine-learning-data-science-process-hive-walkthrough.md)逐步解說。</span><span class="sxs-lookup"><span data-stu-id="ba48d-107">This is typically be hello first step for hello [SQL](machine-learning-data-science-process-sql-walkthrough.md) and [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) walkthroughs.</span></span>

<span data-ttu-id="ba48d-108">使用 SSIS tooaccomplish 商務標準案例的討論必須在混合式資料整合案例一般，請參閱[這樣做更的 SQL Server Integration Services 功能套件 azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx)部落格。</span><span class="sxs-lookup"><span data-stu-id="ba48d-108">For a discussion of canonical scenarios that use SSIS tooaccomplish business needs common in hybrid data integration scenarios, see [Doing more with SQL Server Integration Services Feature Pack for Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) blog.</span></span>

> [!NOTE]
> <span data-ttu-id="ba48d-109">完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和太[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba48d-109">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ba48d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ba48d-110">Prerequisites</span></span>
<span data-ttu-id="ba48d-111">在本文中說明 tooperform hello 工作您必須擁有 Azure 訂用帳戶和設定 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba48d-111">tooperform hello tasks described in this article, you must have an Azure subscription and an Azure storage account set up.</span></span> <span data-ttu-id="ba48d-112">您必須知道您 Azure 儲存體帳戶名稱和帳戶金鑰 tooupload 或下載資料。</span><span class="sxs-lookup"><span data-stu-id="ba48d-112">You must know your Azure storage account name and account key tooupload or download data.</span></span>

* <span data-ttu-id="ba48d-113">向上 tooset **Azure 訂用帳戶**，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ba48d-113">tooset up an **Azure subscription**, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ba48d-114">如需建立 **儲存體帳戶** 以及取得帳戶和金鑰資訊的指示，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ba48d-114">For instructions on creating a **storage account** and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

<span data-ttu-id="ba48d-115">toouse hello **SSIS 連接器**，您必須下載：</span><span class="sxs-lookup"><span data-stu-id="ba48d-115">toouse hello **SSIS connectors**, you must download:</span></span>

* <span data-ttu-id="ba48d-116">**SQL Server 2014 或 2016 標準版 (或更新版本)**：安裝包含 SQL Server 整合服務。</span><span class="sxs-lookup"><span data-stu-id="ba48d-116">**SQL Server 2014 or 2016 Standard (or above)**: Install includes SQL Server Integration Services.</span></span>
* <span data-ttu-id="ba48d-117">**Microsoft SQL Server 2014 或 azure 2016 Integration Services 功能套件**： 這些可以下載，分別從 hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366)和[SQL Server 2016 Integration服務](https://www.microsoft.com/download/details.aspx?id=49492)頁面。</span><span class="sxs-lookup"><span data-stu-id="ba48d-117">**Microsoft SQL Server 2014 or 2016 Integration Services Feature Pack for Azure**: These can be downloaded, respectively, from hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) and [SQL Server 2016 Integration Services](https://www.microsoft.com/download/details.aspx?id=49492) pages.</span></span>

> [!NOTE]
> <span data-ttu-id="ba48d-118">SSIS 已安裝與 SQL Server，但未包含在 hello Express 版本。</span><span class="sxs-lookup"><span data-stu-id="ba48d-118">SSIS is installed with SQL Server, but is not included in hello Express version.</span></span> <span data-ttu-id="ba48d-119">如需 SQL Server 各種版本中包含哪些應用程式的相關資訊，請參閱 [SQL Server 版本](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span><span class="sxs-lookup"><span data-stu-id="ba48d-119">For information on what applications are included in various editions of SQL Server, see [SQL Server Editions](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/)</span></span>
> 
> 

<span data-ttu-id="ba48d-120">如需 SSIS 的訓練教材，請參閱 [SSIS 實務訓練](http://www.microsoft.com/download/details.aspx?id=20766)</span><span class="sxs-lookup"><span data-stu-id="ba48d-120">For training materials on SSIS, see [Hands On Training for SSIS](http://www.microsoft.com/download/details.aspx?id=20766)</span></span>

<span data-ttu-id="ba48d-121">如需詳細資訊 tooget 向上運作使用 SISS toobuild 簡單擷取、 轉換和載入 (ETL) 封裝，請參閱[SSIS 教學課程： 建立簡易 ETL 封裝](https://msdn.microsoft.com/library/ms169917.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba48d-121">For information on how tooget up-and-running using SISS toobuild simple extraction, transformation, and load (ETL) packages, see [SSIS Tutorial: Creating a Simple ETL Package](https://msdn.microsoft.com/library/ms169917.aspx).</span></span>

## <a name="download-nyc-taxi-dataset"></a><span data-ttu-id="ba48d-122">下載紐約計程車資料集</span><span class="sxs-lookup"><span data-stu-id="ba48d-122">Download NYC Taxi dataset</span></span>
<span data-ttu-id="ba48d-123">hello 範例說明在此使用公開可用的資料集-hello [NYC 計程車往返](http://www.andresmh.com/nyctaxitrips/)資料集。</span><span class="sxs-lookup"><span data-stu-id="ba48d-123">hello example described here use a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="ba48d-124">hello 資料集是由約 173 百萬計程車了 NYC 中 hello 年 2013年所組成。</span><span class="sxs-lookup"><span data-stu-id="ba48d-124">hello dataset consists of about 173 million taxi rides in NYC in hello year 2013.</span></span> <span data-ttu-id="ba48d-125">資料有兩種：路線詳細資料及車費資料。</span><span class="sxs-lookup"><span data-stu-id="ba48d-125">There are two types of data: trip details data and fare data.</span></span> <span data-ttu-id="ba48d-126">由於每個月都有一個檔案，因此總共有 24 個檔案，每個檔案未壓縮的大小約 2GB。</span><span class="sxs-lookup"><span data-stu-id="ba48d-126">As there is a file for each month, we have 24 files in all, each of which is approximately 2GB uncompressed.</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="ba48d-127">上傳資料 tooAzure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="ba48d-127">Upload data tooAzure blob storage</span></span>
<span data-ttu-id="ba48d-128">使用 hello SSIS toomove 資料功能從內部部署 tooAzure blob 儲存體的套件，我們使用執行個體的 hello [ **Azure Blob 上傳工作**](https://msdn.microsoft.com/library/mt146776.aspx)，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ba48d-128">toomove data using hello SSIS feature pack from on-premises tooAzure blob storage, we use an instance of hello [**Azure Blob Upload Task**](https://msdn.microsoft.com/library/mt146776.aspx), shown here:</span></span>

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

<span data-ttu-id="ba48d-130">hello 工作使用的 hello 參數為此處所述：</span><span class="sxs-lookup"><span data-stu-id="ba48d-130">hello parameters that hello task uses are described here:</span></span>

| <span data-ttu-id="ba48d-131">欄位</span><span class="sxs-lookup"><span data-stu-id="ba48d-131">Field</span></span> | <span data-ttu-id="ba48d-132">說明</span><span class="sxs-lookup"><span data-stu-id="ba48d-132">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ba48d-133">**AzureStorageConnection**</span><span class="sxs-lookup"><span data-stu-id="ba48d-133">**AzureStorageConnection**</span></span> |<span data-ttu-id="ba48d-134">指定現有的 Azure 儲存體連線管理員，或建立新的參考點 toowhere hello blob 檔案的 tooan Azure 儲存體帳戶的其中一個裝載。</span><span class="sxs-lookup"><span data-stu-id="ba48d-134">Specifies an existing Azure Storage Connection Manager or creates a new one that refers tooan Azure storage account that points toowhere hello blob files are hosted.</span></span> |
| <span data-ttu-id="ba48d-135">**BlobContainer**</span><span class="sxs-lookup"><span data-stu-id="ba48d-135">**BlobContainer**</span></span> |<span data-ttu-id="ba48d-136">指定 hello hello 保存 hello 上傳檔案做為 blob 的 blob 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="ba48d-136">Specifies hello name of hello blob container that hold hello uploaded files as blobs.</span></span> |
| <span data-ttu-id="ba48d-137">**BlobDirectory**</span><span class="sxs-lookup"><span data-stu-id="ba48d-137">**BlobDirectory**</span></span> |<span data-ttu-id="ba48d-138">指定 hello hello 上傳的檔案儲存為區塊 blob 的 blob 目錄。</span><span class="sxs-lookup"><span data-stu-id="ba48d-138">Specifies hello blob directory where hello uploaded file is stored as a block blob.</span></span> <span data-ttu-id="ba48d-139">hello blob 目錄是虛擬的階層式結構。</span><span class="sxs-lookup"><span data-stu-id="ba48d-139">hello blob directory is a virtual hierarchical structure.</span></span> <span data-ttu-id="ba48d-140">如果 hello blob 已經存在，it ia 取代。</span><span class="sxs-lookup"><span data-stu-id="ba48d-140">If hello blob already exists, it ia replaced.</span></span> |
| <span data-ttu-id="ba48d-141">**LocalDirectory**</span><span class="sxs-lookup"><span data-stu-id="ba48d-141">**LocalDirectory**</span></span> |<span data-ttu-id="ba48d-142">指定包含 hello 檔案 toobe 上傳的 hello 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="ba48d-142">Specifies hello local directory that contains hello files toobe uploaded.</span></span> |
| <span data-ttu-id="ba48d-143">**FileName**</span><span class="sxs-lookup"><span data-stu-id="ba48d-143">**FileName**</span></span> |<span data-ttu-id="ba48d-144">指定名稱篩選 tooselect 檔案 hello 指定的名稱模式。</span><span class="sxs-lookup"><span data-stu-id="ba48d-144">Specifies a name filter tooselect files with hello specified name pattern.</span></span> <span data-ttu-id="ba48d-145">例如，MySheet\*.xls\* 包括如 MySheet001.xls 與 MySheetABC.xlsx 等檔案</span><span class="sxs-lookup"><span data-stu-id="ba48d-145">For example, MySheet\*.xls\* includes files such as MySheet001.xls and MySheetABC.xlsx</span></span> |
| <span data-ttu-id="ba48d-146">**TimeRangeFrom/TimeRangeTo**</span><span class="sxs-lookup"><span data-stu-id="ba48d-146">**TimeRangeFrom/TimeRangeTo**</span></span> |<span data-ttu-id="ba48d-147">指定時間範圍篩選器。</span><span class="sxs-lookup"><span data-stu-id="ba48d-147">Specifies a time range filter.</span></span> <span data-ttu-id="ba48d-148">會包含在 *TimeRangeFrom* 後和 *TimeRangeTo* 前修改的檔案。</span><span class="sxs-lookup"><span data-stu-id="ba48d-148">Files modified after *TimeRangeFrom* and before *TimeRangeTo* are included.</span></span> |

> [!NOTE]
> <span data-ttu-id="ba48d-149">hello **AzureStorageConnection**認證需要 toobe 正確和 hello **BlobContainer** hello 傳輸嘗試之前，必須存在。</span><span class="sxs-lookup"><span data-stu-id="ba48d-149">hello **AzureStorageConnection** credentials need toobe correct and hello **BlobContainer** must exist before hello transfer is attempted.</span></span>
> 
> 

## <a name="download-data-from-azure-blob-storage"></a><span data-ttu-id="ba48d-150">從 Azure Blob 儲存體下載資料</span><span class="sxs-lookup"><span data-stu-id="ba48d-150">Download data from Azure blob storage</span></span>
<span data-ttu-id="ba48d-151">從 Azure blob 儲存體 tooon 內部儲存體與 SSIS，toodownload 資料使用 hello 的執行個體[Azure Blob 上傳工作](https://msdn.microsoft.com/library/mt146779.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba48d-151">toodownload data from Azure blob storage tooon-premises storage with SSIS, use an instance of hello [Azure Blob Upload Task](https://msdn.microsoft.com/library/mt146779.aspx).</span></span>

## <a name="more-advanced-ssis-azure-scenarios"></a><span data-ttu-id="ba48d-152">較進階的 SSIS-Azure 案例</span><span class="sxs-lookup"><span data-stu-id="ba48d-152">More advanced SSIS-Azure scenarios</span></span>
<span data-ttu-id="ba48d-153">hello SSIS 功能套件可讓您更複雜的流程 toobe 一起由封裝工作。</span><span class="sxs-lookup"><span data-stu-id="ba48d-153">hello SSIS feature pack allows for more complex flows toobe handled by packaging tasks together.</span></span> <span data-ttu-id="ba48d-154">例如，hello blob 資料無法直接送入的 HDInsight 叢集，無法下載其輸出，回復 tooa blob，然後 tooon 內部儲存體。</span><span class="sxs-lookup"><span data-stu-id="ba48d-154">For example, hello blob data could feed directly into an HDInsight cluster, whose output could be downloaded back tooa blob and then tooon-premises storage.</span></span> <span data-ttu-id="ba48d-155">SSIS 可使用其他 SSIS 連接器在 HDInsight 叢集上執行 Hive 與 Pig 工作：</span><span class="sxs-lookup"><span data-stu-id="ba48d-155">SSIS can run Hive and Pig jobs on an HDInsight cluster using additional SSIS connectors:</span></span>

* <span data-ttu-id="ba48d-156">使用 SSIS 中使用叢集上的 Azure HDInsight Hive 指令碼的 toorun [Azure HDInsight Hive 工作](https://msdn.microsoft.com/library/mt146771.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba48d-156">toorun a Hive script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Hive Task](https://msdn.microsoft.com/library/mt146771.aspx).</span></span>
* <span data-ttu-id="ba48d-157">使用 SSIS 中使用叢集上的 Azure HDInsight Pig 指令碼的 toorun [Azure HDInsight Pig 工作](https://msdn.microsoft.com/library/mt146781.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ba48d-157">toorun a Pig script on an Azure HDInsight cluster with SSIS, use [Azure HDInsight Pig Task](https://msdn.microsoft.com/library/mt146781.aspx).</span></span>

