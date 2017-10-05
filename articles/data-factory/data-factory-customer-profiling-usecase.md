---
title: "使用案例 - 客戶分析"
description: "了解如何使用 Azure Data Factory 建立資料驅動的工作流程 (管線) 以分析遊戲客戶。"
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
ms.openlocfilehash: 4ee4c3a979a3cdd7ec793d12f812e5b126a2ce94
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-case---customer-profiling"></a><span data-ttu-id="aaa1c-103">使用案例 - 客戶分析</span><span class="sxs-lookup"><span data-stu-id="aaa1c-103">Use Case - Customer Profiling</span></span>
<span data-ttu-id="aaa1c-104">Azure Data Factory 是許多服務之一，可用來實作解決方案加速器的 Cortana Intelligence 套件。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-104">Azure Data Factory is one of many services used to implement the Cortana Intelligence Suite of solution accelerators.</span></span>  <span data-ttu-id="aaa1c-105">如需 Cortana Intelligence 的詳細資訊，請瀏覽 [Cortana Intelligence 套件](http://www.microsoft.com/cortanaanalytics)。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-105">For more information about Cortana Intelligence, visit [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics).</span></span> <span data-ttu-id="aaa1c-106">在本文中，我們會說明簡單的使用案例，以幫助您開始著手了解 Azure Data Factory 如何解決常見的分析問題。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-106">In this document, we describe a simple use case to help you get started with understanding how Azure Data Factory can solve common analytics problems.</span></span>

## <a name="scenario"></a><span data-ttu-id="aaa1c-107">案例</span><span class="sxs-lookup"><span data-stu-id="aaa1c-107">Scenario</span></span>
<span data-ttu-id="aaa1c-108">Contoso 是為多個平台建立遊戲的遊戲公司，包含遊戲主機、手持裝置與個人電腦 (PC)。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-108">Contoso is a gaming company that creates games for multiple platforms: game consoles, hand held devices, and personal computers (PCs).</span></span> <span data-ttu-id="aaa1c-109">當玩家玩這些遊戲時，會產生大量追蹤使用模式、遊戲風格與使用者喜好設定的記錄檔資料。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-109">As players play these games, large volume of log data is produced that tracks the usage patterns, gaming style, and preferences of the user.</span></span>  <span data-ttu-id="aaa1c-110">結合人口統計、區域和產品資料時，Contoso 可以執行分析，引導他們如何增強每位玩家的體驗，並使他們達到升級及在遊戲中購買的目標。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-110">When combined with demographic, regional, and product data, Contoso can perform analytics to guide them about how to enhance players’ experience and target them for upgrades and in-game purchases.</span></span> 

<span data-ttu-id="aaa1c-111">Contoso 的目標是要根據其玩家的遊戲歷程記錄識別向上銷售/交叉銷售機會，並新增強大功能來推動業務成長以及為客戶提供更好的體驗。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-111">Contoso’s goal is to identify up-sell/cross-sell opportunities based on the gaming history of its players and add compelling features to drive business growth and provide a better experience to customers.</span></span> <span data-ttu-id="aaa1c-112">在此使用案例中，我們使用遊戲公司做為企業範例。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-112">For this use case, we use a gaming company as an example of a business.</span></span> <span data-ttu-id="aaa1c-113">該公司想要根據玩家的行為最佳化其遊戲。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-113">The company wants to optimize its games based on players’ behavior.</span></span> <span data-ttu-id="aaa1c-114">這些原則適用於所有想要建立客戶及產品和服務之關聯，並強化其客戶體驗的所有企業。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-114">These principles apply to any business that wants to engage its customers around its goods and services and enhance their customers’ experience.</span></span>

<span data-ttu-id="aaa1c-115">在此解決方案中，Contoso 想要評估最近推出之行銷活動的效益。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-115">In this solution, Contoso wants to evaluate the effectiveness of a marketing campaign it has recently launched.</span></span> <span data-ttu-id="aaa1c-116">我們從原始遊戲記錄檔開始、處理並添加地理位置資料、結合廣告參考資料，最後，將它們複製到 Azure SQL Database 來分析行銷活動的影響力。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-116">We start with the raw gaming logs, process and enrich them with geolocation data, join it with advertising reference data, and lastly copy them into an Azure SQL Database to analyze the campaign’s impact.</span></span>

## <a name="deploy-solution"></a><span data-ttu-id="aaa1c-117">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="aaa1c-117">Deploy Solution</span></span>
<span data-ttu-id="aaa1c-118">若要存取並嘗試這個簡單的使用案例，您只需要有 [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)、[Azure Blob 儲存體帳戶](../storage/common/storage-create-storage-account.md#create-a-storage-account)和 [Azure SQL Database](../sql-database/sql-database-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-118">All you need to access and try out this simple use case is an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/), an [Azure Blob storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), and an [Azure SQL Database](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="aaa1c-119">您從 Data Factory 首頁的 [範例管線] 圖格來部署客戶資料分析管線。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-119">You deploy the customer profiling pipeline from the **Sample pipelines** tile on the home page of your data factory.</span></span>

1. <span data-ttu-id="aaa1c-120">建立 Data Factory 或開啟現有的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-120">Create a data factory or open an existing data factory.</span></span> <span data-ttu-id="aaa1c-121">請參閱[使用 Data Factory 將資料從 Blob 儲存體複製到 SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)，以取得建立 Data Factory 的步驟。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-121">See [Copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for steps to create a data factory.</span></span>
2. <span data-ttu-id="aaa1c-122">在 Data Factory 的 [DATA FACTORY] 刀鋒視窗中，按一下 [範例管線] 磚。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-122">In the **DATA FACTORY** blade for the data factory, click the **Sample pipelines** tile.</span></span>

    ![範例管線圖格](./media/data-factory-samples/SamplePipelinesTile.png)
3. <span data-ttu-id="aaa1c-124">在 [範例管線] 刀鋒視窗中，按一下您想要部署的 [客戶資料分析]。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-124">In the **Sample pipelines** blade, click the **Customer profiling** that you want to deploy.</span></span>

    ![範例管線刀鋒視窗](./media/data-factory-samples/SampleTile.png)
4. <span data-ttu-id="aaa1c-126">指定範例的組態設定。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-126">Specify configuration settings for the sample.</span></span> <span data-ttu-id="aaa1c-127">例如，您的 Azure 儲存體帳戶名稱和金鑰、Azure SQL 伺服器名稱、資料庫、使用者 ID 和密碼。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-127">For example, your Azure storage account name and key, Azure SQL server name, database, User ID, and password.</span></span>

    ![範例刀鋒視窗](./media/data-factory-samples/SampleBlade.png)
5. <span data-ttu-id="aaa1c-129">完成指定組態設定之後，請按一下 [建立]  ，以建立/部署範例管線，以及管線所使用的連結服務/資料表。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-129">After you are done with specifying the configuration settings, click **Create** to create/deploy the sample pipelines and linked services/tables used by the pipelines.</span></span>
6. <span data-ttu-id="aaa1c-130">您會在之前於 [範例管線]  刀鋒視窗上按下的範例磚上，看到部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-130">You see the status of deployment on the sample tile you clicked earlier on the **Sample pipelines** blade.</span></span>

    ![部署狀態](./media/data-factory-samples/DeploymentStatus.png)
7. <span data-ttu-id="aaa1c-132">當您在範例磚上看到 [部署成功] 訊息時，請關閉 [範例管線] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-132">When you see the **Deployment succeeded** message on the tile for the sample, close the **Sample pipelines** blade.</span></span>  
8. <span data-ttu-id="aaa1c-133">在 [DATA FACTORY]  刀鋒視窗上，您會看到連結的服務、資料集及管線已新增到您的 Data Factory。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-133">On **DATA FACTORY** blade, you see that linked services, data sets, and pipelines are added to your data factory.</span></span>  

    ![Data Factory 刀鋒視窗](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a><span data-ttu-id="aaa1c-135">解決方案概觀</span><span class="sxs-lookup"><span data-stu-id="aaa1c-135">Solution Overview</span></span>
<span data-ttu-id="aaa1c-136">這個簡單的使用案例可以當做您如何使用 Azure Data Factory 擷取、準備、轉換、分析和發佈資料的範例。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-136">This simple use case can be used as an example of how you can use Azure Data Factory to ingest, prepare, transform, analyze, and publish data.</span></span>

![端對端工作流程](./media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

<span data-ttu-id="aaa1c-138">此圖說明部署資料管線之後，其會如何出現在 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-138">This Figure depicts how the data pipelines appear in the Azure portal after they have been deployed.</span></span>

1. <span data-ttu-id="aaa1c-139">**PartitionGameLogsPipeline** 從 Blob 儲存體讀取原始遊戲事件，並根據年、月和日建立分割區。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-139">The **PartitionGameLogsPipeline** reads the raw game events from blob storage and creates partitions based on year, month, and day.</span></span>
2. <span data-ttu-id="aaa1c-140">**EnrichGameLogsPipeline** 聯結分割的遊戲事件與地區代碼參考資料，並將 IP 位址對應到相對應的地理位置來充實資料。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-140">The **EnrichGameLogsPipeline** joins partitioned game events with geo code reference data and enriches the data by mapping IP addresses to the corresponding geo-locations.</span></span>
3. <span data-ttu-id="aaa1c-141">**AnalyzeMarketingCampaignPipeline** 管線使用已充實的資料並加上廣告資料來處理，以建立包含行銷活動成效的最終輸出。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-141">The **AnalyzeMarketingCampaignPipeline** pipeline uses the enriched data and processes it with the advertising data to create the final output that contains marketing campaign effectiveness.</span></span>

<span data-ttu-id="aaa1c-142">在此範例中，Data Factory 可用來協調數個活動，包括複製輸入資料、轉換和處理資料，以及將最後的資料輸出至 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-142">In this example, Data Factory is used to orchestrate activities that copy input data, transform, and process the data, and output the final data to an Azure SQL Database.</span></span>  <span data-ttu-id="aaa1c-143">您也可以視覺化資料管線的網路、管理它們，並從 UI 監視其狀態。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-143">You can also visualize the network of data pipelines, manage them, and monitor their status from the UI.</span></span>

## <a name="benefits"></a><span data-ttu-id="aaa1c-144">優點</span><span class="sxs-lookup"><span data-stu-id="aaa1c-144">Benefits</span></span>
<span data-ttu-id="aaa1c-145">藉由最佳化其使用者設定檔分析並將其與企業目標對齊，遊戲公司可以快速收集使用模式，並分析其行銷活動的效益。</span><span class="sxs-lookup"><span data-stu-id="aaa1c-145">By optimizing their user profile analytics and aligning it with business goals, gaming company is able to quickly collect usage patterns, and analyze the effectiveness of its marketing campaigns.</span></span>

