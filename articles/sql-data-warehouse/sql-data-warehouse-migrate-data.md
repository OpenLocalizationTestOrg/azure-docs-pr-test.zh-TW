---
title: "aaaMigrate 您資料 tooSQL 資料倉儲 |Microsoft 文件"
description: "移轉您的資料 tooAzure SQL 資料倉儲來開發方案的提示。"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="2562f-103">移轉資料</span><span class="sxs-lookup"><span data-stu-id="2562f-103">Migrate Your Data</span></span>
<span data-ttu-id="2562f-104">資料可以藉由各種工具，從不同的來源移到您的「SQL 資料倉儲」中。</span><span class="sxs-lookup"><span data-stu-id="2562f-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="2562f-105">ADF 複製、 SSIS 和 bcp 因素都可使用的 tooachieve 此目標。</span><span class="sxs-lookup"><span data-stu-id="2562f-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="2562f-106">不過，hello 資料量增加時應考慮分解成步驟 hello 資料移轉程序。</span><span class="sxs-lookup"><span data-stu-id="2562f-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="2562f-107">這可以提供您 hello 機會 toooptimize 的效能與可靠度 tooensure smooth 資料移轉的每個步驟。</span><span class="sxs-lookup"><span data-stu-id="2562f-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="2562f-108">第一次這篇文章會討論 ADF 複製、 SSIS 和 bcp hello 簡單的移轉案例。</span><span class="sxs-lookup"><span data-stu-id="2562f-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="2562f-109">它然後看起來更到 hello 移轉可以最佳化的方式。</span><span class="sxs-lookup"><span data-stu-id="2562f-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="2562f-110">Azure Data Factory (ADF) 複製</span><span class="sxs-lookup"><span data-stu-id="2562f-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="2562f-111">[ADF 複製][ADF Copy]是 [Azure Data Factory][Azure Data Factory] 的一部分。</span><span class="sxs-lookup"><span data-stu-id="2562f-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="2562f-112">您可以使用 ADF 複製 tooexport 資料 tooflat 檔案位於本機儲存體，tooremote 一般檔案保留在 Azure blob 儲存體，或直接將 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2562f-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="2562f-113">如果在一般檔案中，啟動您的資料，則您首先需要 tootransfer 它 tooAzure 儲存體 blob，才能起始載入到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2562f-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="2562f-114">一旦 hello 資料傳輸到 Azure blob 儲存體，您可以選擇 toouse [ADF 複製][ ADF Copy]再次 toopush hello 資料到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2562f-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="2562f-115">PolyBase 還提供高效能選項 hello 資料載入。</span><span class="sxs-lookup"><span data-stu-id="2562f-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="2562f-116">不過，這表示要使用兩種工具，而不止一種工具。</span><span class="sxs-lookup"><span data-stu-id="2562f-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="2562f-117">如果您需要 hello 達到最佳效能，請使用 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="2562f-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="2562f-118">如果您想要的單一工具體驗 （和 hello 資料不是大量） ADF 是您的答案。</span><span class="sxs-lookup"><span data-stu-id="2562f-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="2562f-119">透過下列某些優越的文章 toohello 前端[ADF 範例][ADF samples]。</span><span class="sxs-lookup"><span data-stu-id="2562f-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="2562f-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="2562f-120">Integration Services</span></span>
<span data-ttu-id="2562f-121">Integration Services (SSIS) 是一個功能強大且靈活的擷取轉換和載入 (ETL) 工具，支援複雜的工作流程、資料轉換，以及數個資料載入選項。</span><span class="sxs-lookup"><span data-stu-id="2562f-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="2562f-122">使用 SSIS toosimply 傳輸資料 tooAzure 或是更廣泛的移轉的一部分。</span><span class="sxs-lookup"><span data-stu-id="2562f-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="2562f-123">SSIS 可以匯出 tooUTF-8 沒有 hello 檔案中的 hello 位元組順序標記。</span><span class="sxs-lookup"><span data-stu-id="2562f-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="2562f-124">您必須先使用 hello 這衍生資料行元件 tooconvert hello 中的字元資料的 tooconfigure hello 資料流程 toouse hello 65001 utf-8 字碼頁。</span><span class="sxs-lookup"><span data-stu-id="2562f-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="2562f-125">一旦已轉換 hello 資料行，將寫入 hello 資料 toohello 一般檔案目的地配接器確保 65001 為 hello hello 檔案的字碼頁中也已選取。</span><span class="sxs-lookup"><span data-stu-id="2562f-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="2562f-126">SSIS 連接 tooSQL 資料倉儲，就如同其所要連接 tooa SQL Server 部署。</span><span class="sxs-lookup"><span data-stu-id="2562f-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="2562f-127">不過，您的連線需要 toobe 使用 ADO.NET 連接管理員。</span><span class="sxs-lookup"><span data-stu-id="2562f-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="2562f-128">您應該也要負責 tooconfigure hello"的話就使用大量插入 」 設定 toomaximize 輸送量。</span><span class="sxs-lookup"><span data-stu-id="2562f-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="2562f-129">請參閱 toohello [ADO.NET 目的地配接器][ ADO.NET destination adapter]文章 toolearn 更多關於此屬性</span><span class="sxs-lookup"><span data-stu-id="2562f-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="2562f-130">不支援使用 OLEDB 連接 tooAzure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="2562f-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="2562f-131">此外，總是會 hello 可能性封裝可能會失敗，因為 toothrottling 或網路問題。</span><span class="sxs-lookup"><span data-stu-id="2562f-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="2562f-132">設計封裝，讓他們可以繼續在 hello 失敗點，而不重做 hello 失敗前完成的工作。</span><span class="sxs-lookup"><span data-stu-id="2562f-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="2562f-133">如需詳細資訊，請參閱 hello [SSIS 文件][SSIS documentation]。</span><span class="sxs-lookup"><span data-stu-id="2562f-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="2562f-134">bcp</span><span class="sxs-lookup"><span data-stu-id="2562f-134">bcp</span></span>
<span data-ttu-id="2562f-135">bcp 是專為一般檔案資料匯入和匯出所設計的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="2562f-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="2562f-136">資料匯出期間可能進行某些轉換。</span><span class="sxs-lookup"><span data-stu-id="2562f-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="2562f-137">使用查詢 tooselect tooperform 簡單轉換，並轉換 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2562f-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="2562f-138">一旦匯出，然後可以載入 hello 一般檔案直接到 hello 目標 hello SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="2562f-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="2562f-139">它通常是個不錯的主意 tooencapsulate hello hello 來源系統上的檢視匯出資料期間所使用的轉換。</span><span class="sxs-lookup"><span data-stu-id="2562f-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="2562f-140">這可確保 hello 邏輯會保留，但 hello 程序可重複。</span><span class="sxs-lookup"><span data-stu-id="2562f-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="2562f-141">bcp 的優點包括：</span><span class="sxs-lookup"><span data-stu-id="2562f-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="2562f-142">簡單。</span><span class="sxs-lookup"><span data-stu-id="2562f-142">Simplicity.</span></span> <span data-ttu-id="2562f-143">會簡單 toobuild bcp 命令，並執行</span><span class="sxs-lookup"><span data-stu-id="2562f-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="2562f-144">可重新啟動的載入程序。</span><span class="sxs-lookup"><span data-stu-id="2562f-144">Re-startable load process.</span></span> <span data-ttu-id="2562f-145">一次匯出的 hello 負載可能會執行任何次數</span><span class="sxs-lookup"><span data-stu-id="2562f-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="2562f-146">bcp 的限制包括：</span><span class="sxs-lookup"><span data-stu-id="2562f-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="2562f-147">bcp 只能使用列表式一般檔案。</span><span class="sxs-lookup"><span data-stu-id="2562f-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="2562f-148">無法使用 xml 或 JSON 之類的檔案</span><span class="sxs-lookup"><span data-stu-id="2562f-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="2562f-149">資料轉換功能只有有限的 toohello 匯出階段，而簡單的本質</span><span class="sxs-lookup"><span data-stu-id="2562f-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="2562f-150">bcp 已調整的 toobe 強固時將資料載入透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="2562f-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="2562f-151">任何網路不穩定狀況都可能造成載入錯誤。</span><span class="sxs-lookup"><span data-stu-id="2562f-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="2562f-152">bcp 依賴出現在 hello 目標資料庫預先 toohello 負載中的 hello 結構描述</span><span class="sxs-lookup"><span data-stu-id="2562f-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="2562f-153">如需詳細資訊，請參閱[使用 bcp tooload 資料到 SQL 資料倉儲][Use bcp tooload data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="2562f-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="2562f-154">最佳化資料移轉</span><span class="sxs-lookup"><span data-stu-id="2562f-154">Optimizing data migration</span></span>
<span data-ttu-id="2562f-155">SQLDW 資料移轉程序可以有效地分成三個獨立的步驟：</span><span class="sxs-lookup"><span data-stu-id="2562f-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="2562f-156">匯出來源資料</span><span class="sxs-lookup"><span data-stu-id="2562f-156">Export of source data</span></span>
2. <span data-ttu-id="2562f-157">傳輸的資料 tooAzure</span><span class="sxs-lookup"><span data-stu-id="2562f-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="2562f-158">載入 hello 目標 SQLDW 資料庫</span><span class="sxs-lookup"><span data-stu-id="2562f-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="2562f-159">每個步驟可以是個別最佳化的 toocreate 達到最大效能，在每個步驟的強固、 重新啟動且有彈性的移轉程序。</span><span class="sxs-lookup"><span data-stu-id="2562f-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="2562f-160">最佳化資料載入</span><span class="sxs-lookup"><span data-stu-id="2562f-160">Optimizing data load</span></span>
<span data-ttu-id="2562f-161">查看這些以反向順序的時間。hello 最快方式 tooload 資料是透過 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="2562f-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="2562f-162">PolyBase 載入程序最佳化放置於必要條件 hello 先前步驟是最佳 toounderstand 這前方。</span><span class="sxs-lookup"><span data-stu-id="2562f-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="2562f-163">如下：</span><span class="sxs-lookup"><span data-stu-id="2562f-163">They are:</span></span>

1. <span data-ttu-id="2562f-164">資料檔案的編碼</span><span class="sxs-lookup"><span data-stu-id="2562f-164">Encoding of data files</span></span>
2. <span data-ttu-id="2562f-165">資料檔案的格式</span><span class="sxs-lookup"><span data-stu-id="2562f-165">Format of data files</span></span>
3. <span data-ttu-id="2562f-166">資料檔案的位置</span><span class="sxs-lookup"><span data-stu-id="2562f-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="2562f-167">編碼</span><span class="sxs-lookup"><span data-stu-id="2562f-167">Encoding</span></span>
<span data-ttu-id="2562f-168">PolyBase 需要資料檔案 toobe utf-8 或 UTF-16 16FE。</span><span class="sxs-lookup"><span data-stu-id="2562f-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="2562f-169">資料檔案的格式</span><span class="sxs-lookup"><span data-stu-id="2562f-169">Format of data files</span></span>
<span data-ttu-id="2562f-170">PolyBase 規定要有固定的資料列結束字元 \n 或新行。</span><span class="sxs-lookup"><span data-stu-id="2562f-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="2562f-171">您的資料檔案都必須符合 toothis 標準。</span><span class="sxs-lookup"><span data-stu-id="2562f-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="2562f-172">字串或資料行結束字元沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="2562f-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="2562f-173">您必須 toodefine 每個資料行 hello 檔案中做為外部資料表中 PolyBase 的一部分。</span><span class="sxs-lookup"><span data-stu-id="2562f-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="2562f-174">請確定所有匯出的資料行所需，且 hello 類型符合所需的 toohello 標準。</span><span class="sxs-lookup"><span data-stu-id="2562f-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="2562f-175">請參閱上一步 toohello [移轉您的結構描述] 文件以取得有關支援的資料類型的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2562f-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="2562f-176">資料檔案的位置</span><span class="sxs-lookup"><span data-stu-id="2562f-176">Location of data files</span></span>
<span data-ttu-id="2562f-177">SQL 資料倉儲以獨佔方式使用 PolyBase tooload 資料從 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2562f-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="2562f-178">因此，hello 資料必須已先傳送到 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="2562f-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="2562f-179">最佳化資料傳輸</span><span class="sxs-lookup"><span data-stu-id="2562f-179">Optimizing data transfer</span></span>
<span data-ttu-id="2562f-180">Hello 傳送嗨資料 tooAzure hello 名最慢的部分資料移轉的其中一個。</span><span class="sxs-lookup"><span data-stu-id="2562f-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="2562f-181">不只網路頻寬可能是個問題，網路可靠性也可能嚴重阻礙進度。</span><span class="sxs-lookup"><span data-stu-id="2562f-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="2562f-182">預設情況下移轉資料 tooAzure 是透過 hello 網際網路因此 hello 發生可能相當的傳輸錯誤的機會。</span><span class="sxs-lookup"><span data-stu-id="2562f-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="2562f-183">不過，這些錯誤可能需要重新傳送整個或部分資料 toobe。</span><span class="sxs-lookup"><span data-stu-id="2562f-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="2562f-184">幸運的是您有數個選項 tooimprove hello 速度和恢復功能，此程序：</span><span class="sxs-lookup"><span data-stu-id="2562f-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="2562f-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="2562f-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="2562f-186">您可以使用 tooconsider [ExpressRoute] [ ExpressRoute] toospeed hello 傳輸設定。</span><span class="sxs-lookup"><span data-stu-id="2562f-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="2562f-187">[ExpressRoute] [ ExpressRoute]提供您已建立私人連線 tooAzure 讓 hello 連接不會通過 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="2562f-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="2562f-188">這絕不是必要的步驟。</span><span class="sxs-lookup"><span data-stu-id="2562f-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="2562f-189">不過，它將會改善輸送量時發送資料 tooAzure 從內部部署或共置設備。</span><span class="sxs-lookup"><span data-stu-id="2562f-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="2562f-190">hello 優點[ExpressRoute] [ ExpressRoute]是：</span><span class="sxs-lookup"><span data-stu-id="2562f-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="2562f-191">更高的可靠性</span><span class="sxs-lookup"><span data-stu-id="2562f-191">Increased reliability</span></span>
2. <span data-ttu-id="2562f-192">更快的網路速度</span><span class="sxs-lookup"><span data-stu-id="2562f-192">Faster network speed</span></span>
3. <span data-ttu-id="2562f-193">更短的網路延遲</span><span class="sxs-lookup"><span data-stu-id="2562f-193">Lower network latency</span></span>
4. <span data-ttu-id="2562f-194">更高的網路安全性</span><span class="sxs-lookup"><span data-stu-id="2562f-194">higher network security</span></span>

<span data-ttu-id="2562f-195">[ExpressRoute] [ ExpressRoute]很有幫助的案例數目，不只是 hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="2562f-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="2562f-196">有興趣嗎？</span><span class="sxs-lookup"><span data-stu-id="2562f-196">Interested?</span></span> <span data-ttu-id="2562f-197">如需詳細資訊，請定價請瀏覽 hello [ExpressRoute 文件][ExpressRoute documentation]。</span><span class="sxs-lookup"><span data-stu-id="2562f-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="2562f-198">Azure 匯入和匯出服務</span><span class="sxs-lookup"><span data-stu-id="2562f-198">Azure Import and Export Service</span></span>
<span data-ttu-id="2562f-199">hello Azure 匯入和匯出服務是針對大型 （GB + +） toomassive （TB + +） 的資料傳輸至 Azure 的資料傳輸程序。</span><span class="sxs-lookup"><span data-stu-id="2562f-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="2562f-200">它牽涉到撰寫資料 toodisks 和傳送它們 tooan Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="2562f-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="2562f-201">然後會代替您到 Azure 儲存體 Blob 載入 hello 磁碟內容。</span><span class="sxs-lookup"><span data-stu-id="2562f-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="2562f-202">Hello 匯入匯出程序的高層級檢視如下所示：</span><span class="sxs-lookup"><span data-stu-id="2562f-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="2562f-203">設定 Azure Blob 儲存體容器 tooreceive hello 資料</span><span class="sxs-lookup"><span data-stu-id="2562f-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="2562f-204">匯出資料 toolocal 儲存體</span><span class="sxs-lookup"><span data-stu-id="2562f-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="2562f-205">複製 hello 資料 too3.5 英吋 SATA II/III 硬碟機使用 hello [Azure 匯入/匯出工具]</span><span class="sxs-lookup"><span data-stu-id="2562f-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="2562f-206">建立使用 hello Azure 匯入和匯出的服務提供 hello [Azure 匯入/匯出工具] 所產生的 hello 日誌檔案匯入工作</span><span class="sxs-lookup"><span data-stu-id="2562f-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="2562f-207">寄送 hello 磁碟機指定 Azure 資料中心</span><span class="sxs-lookup"><span data-stu-id="2562f-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="2562f-208">您的資料會傳送的 tooyour Azure Blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="2562f-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="2562f-209">Hello 資料載入 SQLDW 使用 PolyBase</span><span class="sxs-lookup"><span data-stu-id="2562f-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="2562f-210">[AZCopy][AZCopy] 公用程式</span><span class="sxs-lookup"><span data-stu-id="2562f-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="2562f-211">hello [AZCopy][AZCopy]公用程式會取得您的資料傳輸至 Azure 儲存體 Blob 的絕佳工具。</span><span class="sxs-lookup"><span data-stu-id="2562f-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="2562f-212">它可供小型 （MB + +） toovery 大型 （GB + +） 資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="2562f-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="2562f-213">[AZCopy]也已設計的 tooprovide 彈性輸送量時傳送資料 tooAzure，所以是不錯的選擇，hello 資料傳輸的步驟。</span><span class="sxs-lookup"><span data-stu-id="2562f-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="2562f-214">您可以使用 SQL 資料倉儲 PolyBase hello 資料載入一次傳送。</span><span class="sxs-lookup"><span data-stu-id="2562f-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="2562f-215">您也可以使用「執行程序」工作，將 AZCopy 納入 SSIS 封裝。</span><span class="sxs-lookup"><span data-stu-id="2562f-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="2562f-216">toouse AZCopy 您第一次將會需要 toodownload 並安裝它。</span><span class="sxs-lookup"><span data-stu-id="2562f-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="2562f-217">有[生產版本][production version]和[預覽版本][preview version]可用。</span><span class="sxs-lookup"><span data-stu-id="2562f-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="2562f-218">tooupload 檔案從檔案系統，您需要一個 hello 類似的命令如下：</span><span class="sxs-lookup"><span data-stu-id="2562f-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="2562f-219">高階程序摘要如下：</span><span class="sxs-lookup"><span data-stu-id="2562f-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="2562f-220">設定 Azure 儲存體 blob 容器 tooreceive hello 資料</span><span class="sxs-lookup"><span data-stu-id="2562f-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="2562f-221">匯出資料 toolocal 儲存體</span><span class="sxs-lookup"><span data-stu-id="2562f-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="2562f-222">AZCopy hello Azure Blob 儲存體容器中的資料</span><span class="sxs-lookup"><span data-stu-id="2562f-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="2562f-223">Hello 資料載入使用 PolyBase 的 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="2562f-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="2562f-224">有完整的文件：[AZCopy][AZCopy]。</span><span class="sxs-lookup"><span data-stu-id="2562f-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="2562f-225">最佳化資料匯出</span><span class="sxs-lookup"><span data-stu-id="2562f-225">Optimizing data export</span></span>
<span data-ttu-id="2562f-226">此外 tooensuring hello 匯出符合 toohello 需求配置 PolyBase 您也可以搜尋 hello 資料 tooimprove hello 程序的進一步 toooptimize hello 匯出。</span><span class="sxs-lookup"><span data-stu-id="2562f-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="2562f-227">資料壓縮</span><span class="sxs-lookup"><span data-stu-id="2562f-227">Data compression</span></span>
<span data-ttu-id="2562f-228">PolyBase 可以讀取 gzip 壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="2562f-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="2562f-229">如果您無法 toocompress 資料 toogzip 檔案，則會減少 hello 被推倒 hello 網路資料數量。</span><span class="sxs-lookup"><span data-stu-id="2562f-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="2562f-230">多個檔案</span><span class="sxs-lookup"><span data-stu-id="2562f-230">Multiple files</span></span>
<span data-ttu-id="2562f-231">分割成數個檔案的大型資料表有助於 tooimprove 匯出速度，它也可協助使用傳輸 re-startability，和 hello hello 中的資料一次 hello Azure blob 儲存體的整體管理能力。</span><span class="sxs-lookup"><span data-stu-id="2562f-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="2562f-232">其中有許多不錯的 PolyBase 功能是它會讀取所有的 hello hello 資料夾內的檔案，並視為一個資料表。</span><span class="sxs-lookup"><span data-stu-id="2562f-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="2562f-233">因此，這是個不錯的主意 tooisolate hello 檔案的每個資料表至其自身的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2562f-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="2562f-234">PolyBase 也支援一項稱為「遞迴資料夾周遊」的功能。</span><span class="sxs-lookup"><span data-stu-id="2562f-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="2562f-235">您可以使用這項功能 toofurther 增強的匯出的資料 tooimprove hello 組織您的資料管理。</span><span class="sxs-lookup"><span data-stu-id="2562f-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="2562f-236">toolearn 詳細資料載入資料，使用 PolyBase，請參閱[使用 PolyBase tooload 資料到 SQL 資料倉儲][Use PolyBase tooload data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="2562f-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2562f-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2562f-237">Next steps</span></span>
<span data-ttu-id="2562f-238">如需有關移轉的詳細資訊，請參閱[移轉您的方案 tooSQL 資料倉儲][Migrate your solution tooSQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="2562f-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="2562f-239">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="2562f-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
