---
title: "從內部部署 SQL Server tooSQL Azure 與 Azure Data Factory aaaMove 資料 |Microsoft 文件"
description: "設定撰寫兩個一起移動資料採每日資料庫內部部署與在 hello 雲端的資料移轉活動 ADF 管線。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="680de-103">將資料從內部部署 SQL server tooSQL Azure 與 Azure Data Factory 移</span><span class="sxs-lookup"><span data-stu-id="680de-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="680de-104">本主題說明如何透過 Azure Blob 儲存體使用內部部署 SQL Server 資料庫 tooa SQL Azure 資料庫的 toomove 資料 hello Azure 資料處理站 (ADF)。</span><span class="sxs-lookup"><span data-stu-id="680de-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="680de-105">摘要說明各種選項移動資料 tooan Azure SQL Database 的資料表，請參閱[移動資料 tooan Azure SQL Database 的 Azure Machine Learning](machine-learning-data-science-move-sql-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="680de-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="680de-106"><a name="intro"></a>何謂 ADF 簡介： 以及何時應該使用的 toomigrate 資料？</span><span class="sxs-lookup"><span data-stu-id="680de-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="680de-107">Azure Data Factory 是完全受管理的雲端架構資料整合服務會協調及自動 hello 移動和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="680de-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="680de-108">hello hello ADF 模型中的重要概念是管線。</span><span class="sxs-lookup"><span data-stu-id="680de-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="680de-109">管線是活動的邏輯群組，其中每個定義 hello 動作 tooperform hello 包含的資料在資料集內。</span><span class="sxs-lookup"><span data-stu-id="680de-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="680de-110">連結的服務會使用的 toodefine hello 資訊所需的 Data Factory tooconnect toohello 資料資源。</span><span class="sxs-lookup"><span data-stu-id="680de-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="680de-111">ADF，與現有的資料處理服務可以組合成是高度可用且管理 hello 雲端中的資料管線。</span><span class="sxs-lookup"><span data-stu-id="680de-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="680de-112">這些資料管線可以排程的 tooingest、 準備、 轉換、 分析和發行資料時，而且 ADF 管理和協調 hello 複雜資料和處理的相依性。</span><span class="sxs-lookup"><span data-stu-id="680de-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="680de-113">方案可以快速地建置及部署中的 hello 雲端中，連接越來越多的內部部署和雲端資料來源。</span><span class="sxs-lookup"><span data-stu-id="680de-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="680de-114">請考慮使用 ADF：</span><span class="sxs-lookup"><span data-stu-id="680de-114">Consider using ADF:</span></span>

* <span data-ttu-id="680de-115">當需求 toobe 持續移轉存取兩者的混合式案例中的資料在內部部署和雲端資源</span><span class="sxs-lookup"><span data-stu-id="680de-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="680de-116">當 hello 資料交易性或需求 toobe 修改，或有商務邏輯加入 tooit 時移轉。</span><span class="sxs-lookup"><span data-stu-id="680de-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="680de-117">ADF 允許 hello 排程和監視使用簡單的 JSON 指令碼管理 hello 定期執行的資料移動作業。</span><span class="sxs-lookup"><span data-stu-id="680de-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="680de-118">ADF 也有其他功能，例如支援複雜作業。</span><span class="sxs-lookup"><span data-stu-id="680de-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="680de-119">如需有關 ADF 的詳細資訊，請參閱 hello 文件，網址[Azure 資料處理站 (ADF)](https://azure.microsoft.com/services/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="680de-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="680de-120"><a name="scenario"></a>hello 案例</span><span class="sxs-lookup"><span data-stu-id="680de-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="680de-121">我們設定了 ADF 管線來組成兩個資料移轉活動。</span><span class="sxs-lookup"><span data-stu-id="680de-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="680de-122">一起它們之間移動資料每天在內部部署 SQL database 和 Azure SQL Database hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="680de-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="680de-123">hello 兩個活動包括：</span><span class="sxs-lookup"><span data-stu-id="680de-123">hello two activities are:</span></span>

* <span data-ttu-id="680de-124">將資料從內部部署 SQL Server 資料庫 tooan Azure Blob 儲存體帳戶複製</span><span class="sxs-lookup"><span data-stu-id="680de-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="680de-125">從 hello Azure Blob 儲存體帳戶 tooan Azure SQL Database 中複製資料。</span><span class="sxs-lookup"><span data-stu-id="680de-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="680de-126">hello 示此處已經過修改從 hello hello ADF 小組所提供的教學課程的詳細步驟：[在內部部署來源和資料管理閘道與雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)參考該主題的 toohello 相關章節在適當時提供。</span><span class="sxs-lookup"><span data-stu-id="680de-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="680de-127"><a name="prereqs"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="680de-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="680de-128">本教學課程假設您有：</span><span class="sxs-lookup"><span data-stu-id="680de-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="680de-129">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="680de-129">An **Azure subscription**.</span></span> <span data-ttu-id="680de-130">如果您沒有訂用帳戶，可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="680de-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="680de-131">**Azure 儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="680de-131">An **Azure storage account**.</span></span> <span data-ttu-id="680de-132">您可以使用 Azure 儲存體帳戶將 hello 資料儲存在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="680de-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="680de-133">如果您沒有 Azure 儲存體帳戶，請參閱 hello[建立儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)發行項。</span><span class="sxs-lookup"><span data-stu-id="680de-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="680de-134">建立 hello 儲存體帳戶之後，您會需要 tooobtain hello 帳戶使用 tooaccess hello 儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="680de-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="680de-135">請參閱 [管理儲存體存取金鑰](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)。</span><span class="sxs-lookup"><span data-stu-id="680de-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="680de-136">存取 tooan **Azure SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="680de-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="680de-137">如果您必須設定 Azure SQL Database，hello tpoic[開始使用 Microsoft Azure SQL Database](../sql-database/sql-database-get-started.md)如何提供有關 tooprovision Azure SQL Database 的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="680de-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="680de-138">已在本機上安裝和設定 **Azure PowerShell** 。</span><span class="sxs-lookup"><span data-stu-id="680de-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="680de-139">如需指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="680de-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="680de-140">此程序使用 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="680de-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="680de-141"><a name="upload-data"></a>上傳 hello 資料 tooyour 內部部署 SQL Server</span><span class="sxs-lookup"><span data-stu-id="680de-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="680de-142">我們使用 hello [NYC 計程車資料集](http://chriswhong.com/open-data/foil_nyc_taxi/)toodemonstrate hello 移轉程序。</span><span class="sxs-lookup"><span data-stu-id="680de-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="680de-143">hello NYC 計程車資料集可供使用，如同該文章，在 Azure blob 儲存體中所註明[NYC 計程車資料](http://www.andresmh.com/nyctaxitrips/)。</span><span class="sxs-lookup"><span data-stu-id="680de-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="680de-144">hello 資料有兩個檔案、 hello trip_data.csv 檔案，其中包含路線詳細資料和 hello trip_far.csv 檔案，其中包含針對每個往返支付 hello 價位的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="680de-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="680de-145">這些檔案的範例和說明都會在 [NYC 計程車車程資料集說明](machine-learning-data-science-process-sql-walkthrough.md#dataset)中提供。</span><span class="sxs-lookup"><span data-stu-id="680de-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="680de-146">您可以調整此處提供您自己的資料集 tooa hello 程序，或遵循 hello 步驟所述使用 hello NYC 計程車資料集。</span><span class="sxs-lookup"><span data-stu-id="680de-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="680de-147">tooupload hello NYC 計程車資料集在內部部署 SQL Server 資料庫，請遵循 hello 程序中所述[大量匯入資料到 SQL Server 資料庫](machine-learning-data-science-process-sql-walkthrough.md#dbload)。</span><span class="sxs-lookup"><span data-stu-id="680de-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="680de-148">這些指示適用於 SQL Server 在 Azure 虛擬機器上，但是 hello 程序上傳內部部署 SQL Server 是的 toohello hello 相同。</span><span class="sxs-lookup"><span data-stu-id="680de-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="680de-149"><a name="create-adf"></a> 建立 Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="680de-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="680de-150">hello 指示用於建立新的 Azure Data Factory 和資源群組中 hello [Azure 入口網站](https://portal.azure.com/)提供[建立 Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory)。</span><span class="sxs-lookup"><span data-stu-id="680de-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="680de-151">名稱 hello ADF m_pdoctemplate *adfdsp*與名稱 hello 資源群組建立*adfdsprg*。</span><span class="sxs-lookup"><span data-stu-id="680de-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="680de-152">安裝和設定 hello 資料管理閘道器</span><span class="sxs-lookup"><span data-stu-id="680de-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="680de-153">tooenable 管線在內部部署 SQL Server 與 Azure data factory toowork，您需要 tooadd 它做為連結的服務 toohello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="680de-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="680de-154">toocreate 在內部部署 SQL server 的連結服務，您必須：</span><span class="sxs-lookup"><span data-stu-id="680de-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="680de-155">下載並安裝到 hello 在內部部署電腦上的 Microsoft 資料管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="680de-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="680de-156">設定 hello 在內部部署資料來源 toouse hello 閘道的 hello 連結服務。</span><span class="sxs-lookup"><span data-stu-id="680de-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="680de-157">hello 資料管理閘道器序列化和還原序列化 hello hello 其裝載所在的電腦上的來源和接收資料。</span><span class="sxs-lookup"><span data-stu-id="680de-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="680de-158">如需關於資料管理閘道的設定指示及詳細資料，請參閱 [利用資料管理閘道在內部部署來源和雲端之間移動資料](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="680de-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="680de-159"><a name="adflinkedservices"></a>建立連結的服務 tooconnect toohello 資料資源</span><span class="sxs-lookup"><span data-stu-id="680de-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="680de-160">連結的服務定義所需的 Azure Data Factory tooconnect tooa 資料資源的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="680de-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="680de-161">hello 用於建立連結的服務的逐步程序中提供[建立連結的服務](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services)。</span><span class="sxs-lookup"><span data-stu-id="680de-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="680de-162">此案例中的三個資源都必須使用連結服務。</span><span class="sxs-lookup"><span data-stu-id="680de-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="680de-163">內部部署 SQL Server 的連結服務</span><span class="sxs-lookup"><span data-stu-id="680de-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="680de-164">Azure Blob 儲存體的連結服務</span><span class="sxs-lookup"><span data-stu-id="680de-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="680de-165">Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="680de-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="680de-166"><a name="adf-linked-service-onprem-sql"></a>內部部署 SQL Server 資料庫的連結服務</span><span class="sxs-lookup"><span data-stu-id="680de-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="680de-167">hello toocreate hello 連結的服務內部部署 SQL Server:</span><span class="sxs-lookup"><span data-stu-id="680de-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="680de-168">按一下 hello**資料存放區**在 Azure 傳統入口網站上的 hello ADF 登陸頁面</span><span class="sxs-lookup"><span data-stu-id="680de-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="680de-169">選取**SQL** ，然後輸入 hello *username*和*密碼*認證 hello 內部部署 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="680de-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="680de-170">您需要為 tooenter hello servername**完整的 servername 反斜線執行個體名稱 (servername\instancename)**。</span><span class="sxs-lookup"><span data-stu-id="680de-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="680de-171">名稱 hello 連結服務*adfonpremsql*。</span><span class="sxs-lookup"><span data-stu-id="680de-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="680de-172"><a name="adf-linked-service-blob-store"></a>Blob 的連結服務</span><span class="sxs-lookup"><span data-stu-id="680de-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="680de-173">toocreate hello hello Azure Blob 儲存體帳戶的連結的服務：</span><span class="sxs-lookup"><span data-stu-id="680de-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="680de-174">按一下 hello**資料存放區**在 Azure 傳統入口網站上的 hello ADF 登陸頁面</span><span class="sxs-lookup"><span data-stu-id="680de-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="680de-175">選取 [Azure 儲存體帳戶] </span><span class="sxs-lookup"><span data-stu-id="680de-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="680de-176">輸入 hello Azure Blob 儲存體帳戶金鑰和容器名稱。</span><span class="sxs-lookup"><span data-stu-id="680de-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="680de-177">名稱 hello 連結的服務*adfds*。</span><span class="sxs-lookup"><span data-stu-id="680de-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="680de-178"><a name="adf-linked-service-azure-sql"></a>Azure SQL Database 的連結服務</span><span class="sxs-lookup"><span data-stu-id="680de-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="680de-179">toocreate hello hello Azure SQL Database 的連結的服務：</span><span class="sxs-lookup"><span data-stu-id="680de-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="680de-180">按一下 hello**資料存放區**在 Azure 傳統入口網站上的 hello ADF 登陸頁面</span><span class="sxs-lookup"><span data-stu-id="680de-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="680de-181">選取**Azure SQL** ，然後輸入 hello *username*和*密碼*hello Azure SQL Database 的認證。</span><span class="sxs-lookup"><span data-stu-id="680de-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="680de-182">hello *username*必須指定為* user@servername *。</span><span class="sxs-lookup"><span data-stu-id="680de-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="680de-183"><a name="adf-tables"></a>定義和建立資料表 toospecify tooaccess hello 資料集的方式</span><span class="sxs-lookup"><span data-stu-id="680de-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="680de-184">建立以 hello 下列指令碼為基礎的程序指定 hello 結構、 位置和可用性的 hello 資料集的資料表。</span><span class="sxs-lookup"><span data-stu-id="680de-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="680de-185">JSON 檔案是使用的 toodefine hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="680de-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="680de-186">如需有關這些檔案的 hello 結構的詳細資訊，請參閱[資料集](../data-factory/data-factory-create-datasets.md)。</span><span class="sxs-lookup"><span data-stu-id="680de-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="680de-187">您應該執行 hello `Add-AzureAccount` cmdlet 然後才執行 hello[新增 AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) hello 權限的 Azure 訂用帳戶的 cmdlet tooconfirm 選取 hello 命令執行。</span><span class="sxs-lookup"><span data-stu-id="680de-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="680de-188">如需此 Cmdlet 的文件，請參閱 [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0)。</span><span class="sxs-lookup"><span data-stu-id="680de-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="680de-189">hello 資料表中的 hello JSON 型定義，會使用下列名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="680de-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="680de-190">hello**資料表名稱**hello 在內部部署 SQL server 是*nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="680de-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="680de-191">hello**容器名稱**在 hello Azure Blob 儲存體帳戶是*containername*</span><span class="sxs-lookup"><span data-stu-id="680de-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="680de-192">此 ADF 管線所需的三個資料表定義為：</span><span class="sxs-lookup"><span data-stu-id="680de-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="680de-193">SQL 內部部署資料表</span><span class="sxs-lookup"><span data-stu-id="680de-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="680de-194">Blob 資料表 </span><span class="sxs-lookup"><span data-stu-id="680de-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="680de-195">SQL Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="680de-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="680de-196">這些程序會使用 Azure PowerShell toodefine，並建立 hello ADF 活動。</span><span class="sxs-lookup"><span data-stu-id="680de-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="680de-197">但是，這些工作也可以完成使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="680de-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="680de-198">如需詳細資訊，請參閱[建立資料集](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets)。</span><span class="sxs-lookup"><span data-stu-id="680de-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="680de-199"><a name="adf-table-onprem-sql"></a>SQL 內部部署資料表</span><span class="sxs-lookup"><span data-stu-id="680de-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="680de-200">hello hello 資料表定義內部 hello 下列 JSON 檔案中指定 SQL Server:</span><span class="sxs-lookup"><span data-stu-id="680de-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="680de-201">hello 資料行名稱，並沒有包含在內。</span><span class="sxs-lookup"><span data-stu-id="680de-201">hello column names were not included here.</span></span> <span data-ttu-id="680de-202">您可以子選取 hello 資料行名稱上的命令包含以下 (詳細資料] 核取 hello [ADF 文件](../data-factory/data-factory-data-movement-activities.md)主題。</span><span class="sxs-lookup"><span data-stu-id="680de-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="680de-203">將 hello hello 資料表 JSON 定義複製到檔案，稱為*onpremtabledef.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\onpremtabledef.json*)。</span><span class="sxs-lookup"><span data-stu-id="680de-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="680de-204">建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 資料表：</span><span class="sxs-lookup"><span data-stu-id="680de-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="680de-205"><a name="adf-table-blob-store"></a>Blob 資料表</span><span class="sxs-lookup"><span data-stu-id="680de-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="680de-206">Hello 的 hello 資料表定義輸出 blob 位置中 （這會對應 hello 內嵌的資料從內部部署 tooAzure blob） 的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="680de-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="680de-207">將 hello hello 資料表 JSON 定義複製到檔案，稱為*bloboutputtabledef.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\bloboutputtabledef.json*)。</span><span class="sxs-lookup"><span data-stu-id="680de-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="680de-208">建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 資料表：</span><span class="sxs-lookup"><span data-stu-id="680de-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="680de-209"><a name="adf-table-azure-sq"></a>SQL Azure 資料表</span><span class="sxs-lookup"><span data-stu-id="680de-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="680de-210">SQL Azure 輸出的 hello 的 hello 資料表定義位於 hello 下列 （此結構描述對應來自 hello blob 的 hello 資料）：</span><span class="sxs-lookup"><span data-stu-id="680de-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="680de-211">將 hello hello 資料表 JSON 定義複製到檔案，稱為*AzureSqlTable.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\AzureSqlTable.json*)。</span><span class="sxs-lookup"><span data-stu-id="680de-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="680de-212">建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 資料表：</span><span class="sxs-lookup"><span data-stu-id="680de-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="680de-213"><a name="adf-pipeline"></a>定義和建立 hello 管線</span><span class="sxs-lookup"><span data-stu-id="680de-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="680de-214">指定屬於 toohello hello 活動管線，並且使用下列指令碼為基礎的程序的 hello 建立 hello 管線。</span><span class="sxs-lookup"><span data-stu-id="680de-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="680de-215">在 JSON 檔案是使用的 toodefine hello 管線屬性。</span><span class="sxs-lookup"><span data-stu-id="680de-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="680de-216">hello 指令碼會假設該 hello**管線名稱**是*AMLDSProcessPipeline*。</span><span class="sxs-lookup"><span data-stu-id="680de-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="680de-217">也請注意，我們設定的每日為基礎，並使用 hello 預設執行 hello 工作時間 (12 am UTC) 上執行的 hello 管線 toobe hello 週期性。</span><span class="sxs-lookup"><span data-stu-id="680de-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="680de-218">hello 下列程序使用 Azure PowerShell toodefine 並建立 hello ADF 管線。</span><span class="sxs-lookup"><span data-stu-id="680de-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="680de-219">但是，此工作也可以透過 Azure 入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="680de-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="680de-220">如需詳細資訊，請參閱[建立管線](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="680de-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="680de-221">使用 hello 資料表定義前面，提供 hello 管線定義 hello ADF 的指定方式如下：</span><span class="sxs-lookup"><span data-stu-id="680de-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="680de-222">將 hello 管線的此 JSON 定義複製到檔案，稱為*pipelinedef.json*檔案，並將它儲存 tooa 已知位置 (這裡假設 toobe *C:\temp\pipelinedef.json*)。</span><span class="sxs-lookup"><span data-stu-id="680de-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="680de-223">建立下列 Azure PowerShell cmdlet 的 hello 與 ADF hello 管線：</span><span class="sxs-lookup"><span data-stu-id="680de-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="680de-224">確認您可以看到 hello 管線在 hello ADF hello Azure 傳統入口網站中的顯示如下所示 （當您按一下 hello 圖表）</span><span class="sxs-lookup"><span data-stu-id="680de-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![ADF 管線](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="680de-226"><a name="adf-pipeline-start"></a>啟動 hello 管線</span><span class="sxs-lookup"><span data-stu-id="680de-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="680de-227">hello 管線現在可以執行使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="680de-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="680de-228">hello *startdate*和*enddate*需要 toobe 取代為您想要的 hello 管線 toorun hello 實際日期的參數值。</span><span class="sxs-lookup"><span data-stu-id="680de-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="680de-229">一旦 hello 管線執行時，您應該能夠 toosee hello 資料都會顯示在所選 hello blob，每日的一個檔案的 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="680de-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="680de-230">請注意，我們不運用相當 hello 以累加方式 ADF toopipe 資料所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="680de-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="680de-231">如需有關如何 toodo 這和其他功能提供的 ADF，請參閱 hello [ADF 文件](https://azure.microsoft.com/services/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="680de-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
