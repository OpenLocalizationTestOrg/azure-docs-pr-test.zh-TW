---
title: "aaaUse 案例的客戶程式碼剖析"
description: "了解 Azure Data Factory 的使用的資料驅動的 toocreate 工作流程 （管線） tooprofile 遊戲客戶的方式。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 47f5e77242366c80cce2a2db65e3c696505b3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-case---customer-profiling"></a><span data-ttu-id="c800c-103">使用案例 - 客戶分析</span><span class="sxs-lookup"><span data-stu-id="c800c-103">Use Case - Customer Profiling</span></span>
<span data-ttu-id="c800c-104">Azure Data Factory 是許多使用服務 tooimplement hello 解決方案加速器 Cortana 智慧套件。</span><span class="sxs-lookup"><span data-stu-id="c800c-104">Azure Data Factory is one of many services used tooimplement hello Cortana Intelligence Suite of solution accelerators.</span></span>  <span data-ttu-id="c800c-105">如需 Cortana Intelligence 的詳細資訊，請瀏覽 [Cortana Intelligence 套件](http://www.microsoft.com/cortanaanalytics)。</span><span class="sxs-lookup"><span data-stu-id="c800c-105">For more information about Cortana Intelligence, visit [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics).</span></span> <span data-ttu-id="c800c-106">我們在本文件說明簡單的使用案例的 toohelp 開始了解如何 Azure Data Factory 可以解決常見分析的問題。</span><span class="sxs-lookup"><span data-stu-id="c800c-106">In this document, we describe a simple use case toohelp you get started with understanding how Azure Data Factory can solve common analytics problems.</span></span>

## <a name="scenario"></a><span data-ttu-id="c800c-107">案例</span><span class="sxs-lookup"><span data-stu-id="c800c-107">Scenario</span></span>
<span data-ttu-id="c800c-108">Contoso 是為多個平台建立遊戲的遊戲公司，包含遊戲主機、手持裝置與個人電腦 (PC)。</span><span class="sxs-lookup"><span data-stu-id="c800c-108">Contoso is a gaming company that creates games for multiple platforms: game consoles, hand held devices, and personal computers (PCs).</span></span> <span data-ttu-id="c800c-109">因為播放程式播放這些遊戲，大量的記錄檔資料會產生追蹤 hello 使用模式、 遊戲樣式和 hello 使用者喜好設定。</span><span class="sxs-lookup"><span data-stu-id="c800c-109">As players play these games, large volume of log data is produced that tracks hello usage patterns, gaming style, and preferences of hello user.</span></span>  <span data-ttu-id="c800c-110">結合人口統計的地區和產品的資料，Contoso 可以執行分析 tooguide 如何 tooenhance 玩家的體驗和升級的目標以及遊戲中購買。</span><span class="sxs-lookup"><span data-stu-id="c800c-110">When combined with demographic, regional, and product data, Contoso can perform analytics tooguide them about how tooenhance players’ experience and target them for upgrades and in-game purchases.</span></span> 

<span data-ttu-id="c800c-111">Contoso 的目標是根據其播放程式的 hello 遊戲記錄 tooidentify 向上銷售/交叉銷售商機加入令人信服功能 toodrive 業務成長和提供更好的體驗 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="c800c-111">Contoso’s goal is tooidentify up-sell/cross-sell opportunities based on hello gaming history of its players and add compelling features toodrive business growth and provide a better experience toocustomers.</span></span> <span data-ttu-id="c800c-112">在此使用案例中，我們使用遊戲公司做為企業範例。</span><span class="sxs-lookup"><span data-stu-id="c800c-112">For this use case, we use a gaming company as an example of a business.</span></span> <span data-ttu-id="c800c-113">hello 公司想 toooptimize 根據玩家的行為及其遊戲。</span><span class="sxs-lookup"><span data-stu-id="c800c-113">hello company wants toooptimize its games based on players’ behavior.</span></span> <span data-ttu-id="c800c-114">這些原則套用想 tooengage tooany 商務周圍其產品和服務客戶，並增強其客戶的經驗。</span><span class="sxs-lookup"><span data-stu-id="c800c-114">These principles apply tooany business that wants tooengage its customers around its goods and services and enhance their customers’ experience.</span></span>

<span data-ttu-id="c800c-115">在此解決方案中，Contoso 希望 tooevaluate hello 有效性的行銷活動，它最近已啟動。</span><span class="sxs-lookup"><span data-stu-id="c800c-115">In this solution, Contoso wants tooevaluate hello effectiveness of a marketing campaign it has recently launched.</span></span> <span data-ttu-id="c800c-116">我們開始 hello 未經處理的遊戲記錄檔，處理程序和擴充它們與地理位置資料、 聯結與廣告參考資料，最後將其複製到 Azure SQL Database tooanalyze hello 活動造成影響。</span><span class="sxs-lookup"><span data-stu-id="c800c-116">We start with hello raw gaming logs, process and enrich them with geolocation data, join it with advertising reference data, and lastly copy them into an Azure SQL Database tooanalyze hello campaign’s impact.</span></span>

## <a name="deploy-solution"></a><span data-ttu-id="c800c-117">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="c800c-117">Deploy Solution</span></span>
<span data-ttu-id="c800c-118">所有您需要 tooaccess，試用這個簡單的使用案例是[Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)、 [Azure Blob 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)，和[Azure SQL Database](../sql-database/sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c800c-118">All you need tooaccess and try out this simple use case is an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/), an [Azure Blob storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), and an [Azure SQL Database](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="c800c-119">部署程式碼剖析管線就會從 hello hello 客戶**範例管線**的 data factory 的 hello 首頁上並排顯示。</span><span class="sxs-lookup"><span data-stu-id="c800c-119">You deploy hello customer profiling pipeline from hello **Sample pipelines** tile on hello home page of your data factory.</span></span>

1. <span data-ttu-id="c800c-120">建立 Data Factory 或開啟現有的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="c800c-120">Create a data factory or open an existing data factory.</span></span> <span data-ttu-id="c800c-121">請參閱[從 Blob 儲存體 tooSQL 資料庫使用 Data Factory 複製資料](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)如步驟 toocreate data factory。</span><span class="sxs-lookup"><span data-stu-id="c800c-121">See [Copy data from Blob Storage tooSQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for steps toocreate a data factory.</span></span>
2. <span data-ttu-id="c800c-122">在 hello **DATA FACTORY** hello data factory，刀鋒視窗中按一下 hello**範例管線**磚。</span><span class="sxs-lookup"><span data-stu-id="c800c-122">In hello **DATA FACTORY** blade for hello data factory, click hello **Sample pipelines** tile.</span></span>

    ![範例管線圖格](./media/data-factory-samples/SamplePipelinesTile.png)
3. <span data-ttu-id="c800c-124">在 hello**範例管線**刀鋒視窗中，按一下 hello**客戶程式碼剖析**想 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="c800c-124">In hello **Sample pipelines** blade, click hello **Customer profiling** that you want toodeploy.</span></span>

    ![範例管線刀鋒視窗](./media/data-factory-samples/SampleTile.png)
4. <span data-ttu-id="c800c-126">指定 hello 範例的組態設定。</span><span class="sxs-lookup"><span data-stu-id="c800c-126">Specify configuration settings for hello sample.</span></span> <span data-ttu-id="c800c-127">例如，您的 Azure 儲存體帳戶名稱和金鑰、Azure SQL 伺服器名稱、資料庫、使用者 ID 和密碼。</span><span class="sxs-lookup"><span data-stu-id="c800c-127">For example, your Azure storage account name and key, Azure SQL server name, database, User ID, and password.</span></span>

    ![範例刀鋒視窗](./media/data-factory-samples/SampleBlade.png)
5. <span data-ttu-id="c800c-129">您指定 hello 組態設定完成之後，請按一下**建立**toocreate/部署 hello 範例管線與連結的服務/資料表 hello 管線所使用。</span><span class="sxs-lookup"><span data-stu-id="c800c-129">After you are done with specifying hello configuration settings, click **Create** toocreate/deploy hello sample pipelines and linked services/tables used by hello pipelines.</span></span>
6. <span data-ttu-id="c800c-130">您會看到部署的 hello 狀態 hello 範例磚，在您按一下先前 hello**範例管線**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c800c-130">You see hello status of deployment on hello sample tile you clicked earlier on hello **Sample pipelines** blade.</span></span>

    ![部署狀態](./media/data-factory-samples/DeploymentStatus.png)
7. <span data-ttu-id="c800c-132">當您看到 hello**部署成功**hello 磚 hello 範例中，關閉 hello 訊息**範例管線**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c800c-132">When you see hello **Deployment succeeded** message on hello tile for hello sample, close hello **Sample pipelines** blade.</span></span>  
8. <span data-ttu-id="c800c-133">在**DATA FACTORY**您刀鋒視窗中，查看已連結的服務、 資料集和管線新增 tooyour 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="c800c-133">On **DATA FACTORY** blade, you see that linked services, data sets, and pipelines are added tooyour data factory.</span></span>  

    ![Data Factory 刀鋒視窗](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a><span data-ttu-id="c800c-135">解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="c800c-135">Solution Overview</span></span>
<span data-ttu-id="c800c-136">這個簡單的使用案例可以用做為範例，如何使用 Azure Data Factory tooingest、 準備、 轉換、 分析，並將資料發行。</span><span class="sxs-lookup"><span data-stu-id="c800c-136">This simple use case can be used as an example of how you can use Azure Data Factory tooingest, prepare, transform, analyze, and publish data.</span></span>

![端對端工作流程](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

<span data-ttu-id="c800c-138">此圖說明 hello 資料管線之後出現的樣子 hello 在 Azure 入口網站已部署。</span><span class="sxs-lookup"><span data-stu-id="c800c-138">This Figure depicts how hello data pipelines appear in hello Azure portal after they have been deployed.</span></span>

1. <span data-ttu-id="c800c-139">hello **PartitionGameLogsPipeline**從 blob 儲存體讀取 hello 未經處理的遊戲事件，並建立根據年、 月和日的資料分割。</span><span class="sxs-lookup"><span data-stu-id="c800c-139">hello **PartitionGameLogsPipeline** reads hello raw game events from blob storage and creates partitions based on year, month, and day.</span></span>
2. <span data-ttu-id="c800c-140">hello **EnrichGameLogsPipeline**聯結與地理程式碼參考資料的資料分割遊戲事件，並藉由對應 IP 位址 toohello 相對應的地理位置豐富 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="c800c-140">hello **EnrichGameLogsPipeline** joins partitioned game events with geo code reference data and enriches hello data by mapping IP addresses toohello corresponding geo-locations.</span></span>
3. <span data-ttu-id="c800c-141">hello **AnalyzeMarketingCampaignPipeline**管線使用豐富的 hello 資料，並處理以 hello 廣告資料 toocreate hello 最終輸出包含行銷活動效果。</span><span class="sxs-lookup"><span data-stu-id="c800c-141">hello **AnalyzeMarketingCampaignPipeline** pipeline uses hello enriched data and processes it with hello advertising data toocreate hello final output that contains marketing campaign effectiveness.</span></span>

<span data-ttu-id="c800c-142">在此範例中，資料處理站會是複製輸入的資料、 轉換和處理 hello 資料，並輸出 hello 最終資料 tooan Azure SQL Database 的使用的 tooorchestrate 活動。</span><span class="sxs-lookup"><span data-stu-id="c800c-142">In this example, Data Factory is used tooorchestrate activities that copy input data, transform, and process hello data, and output hello final data tooan Azure SQL Database.</span></span>  <span data-ttu-id="c800c-143">您也可以視覺化的資料管線 hello 網路、 管理它們，和監視其狀態從 hello UI。</span><span class="sxs-lookup"><span data-stu-id="c800c-143">You can also visualize hello network of data pipelines, manage them, and monitor their status from hello UI.</span></span>

## <a name="benefits"></a><span data-ttu-id="c800c-144">優點</span><span class="sxs-lookup"><span data-stu-id="c800c-144">Benefits</span></span>
<span data-ttu-id="c800c-145">藉由最佳化其使用者設定檔的分析，並符合商務目標、 遊戲公司無法 tooquickly 收集的使用模式，並分析 hello 行銷活動最佳化其效能。</span><span class="sxs-lookup"><span data-stu-id="c800c-145">By optimizing their user profile analytics and aligning it with business goals, gaming company is able tooquickly collect usage patterns, and analyze hello effectiveness of its marketing campaigns.</span></span>

