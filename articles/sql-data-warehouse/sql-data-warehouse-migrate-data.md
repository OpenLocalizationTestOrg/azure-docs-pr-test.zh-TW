---
title: "將您的資料移轉至 SQL 資料倉儲 | Microsoft Docs"
description: "將您的資料移轉至 Azure SQL 資料倉儲來開發解決方案的秘訣。"
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
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="26827-103">移轉資料</span><span class="sxs-lookup"><span data-stu-id="26827-103">Migrate Your Data</span></span>
<span data-ttu-id="26827-104">資料可以藉由各種工具，從不同的來源移到您的「SQL 資料倉儲」中。</span><span class="sxs-lookup"><span data-stu-id="26827-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="26827-105">ADF 複製、SSIS 和 bcp 都可用來達成此目標。</span><span class="sxs-lookup"><span data-stu-id="26827-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="26827-106">不過，隨著資料量增加，您應該考慮將資料移轉程序細分成步驟。</span><span class="sxs-lookup"><span data-stu-id="26827-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="26827-107">這樣讓您有機會來最佳化每個步驟的效能和彈性，以確保順暢移轉資料。</span><span class="sxs-lookup"><span data-stu-id="26827-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="26827-108">本文首先討論 ADF 複製、SSIS 和 bcp 的簡單移轉案例。</span><span class="sxs-lookup"><span data-stu-id="26827-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="26827-109">接著稍微深入討論如何將移轉最佳化。</span><span class="sxs-lookup"><span data-stu-id="26827-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="26827-110">Azure Data Factory (ADF) 複製</span><span class="sxs-lookup"><span data-stu-id="26827-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="26827-111">[ADF 複製][ADF Copy]是 [Azure Data Factory][Azure Data Factory] 的一部分。</span><span class="sxs-lookup"><span data-stu-id="26827-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="26827-112">您可以使用 ADF 複製將資料匯出到位於本機儲存體的一般檔案、匯出到到保留在 Azure blob 儲存體中的遠端一般檔案，或直接匯出到 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="26827-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="26827-113">如果資料是從一般檔案開始，則在開始將資料載入 SQL 資料倉儲之前，您首先要將資料傳輸到 Azure 儲存體 blob。</span><span class="sxs-lookup"><span data-stu-id="26827-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="26827-114">一旦資料傳輸到 Azure Blob 儲存體，您可以選擇再次使用 [ADF 複製][ADF Copy]，將資料推送至 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="26827-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="26827-115">PolyBase 還提供高效能選項來載入資料。</span><span class="sxs-lookup"><span data-stu-id="26827-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="26827-116">不過，這表示要使用兩種工具，而不止一種工具。</span><span class="sxs-lookup"><span data-stu-id="26827-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="26827-117">如果您需要達到最佳效能，請使用 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="26827-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="26827-118">如果只想要使用單一工具 (且資料量不大)，則 ADF 就是答案。</span><span class="sxs-lookup"><span data-stu-id="26827-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="26827-119">下列文章中有一些很好的 [ADF 範例][ADF samples]。</span><span class="sxs-lookup"><span data-stu-id="26827-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="26827-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="26827-120">Integration Services</span></span>
<span data-ttu-id="26827-121">Integration Services (SSIS) 是一個功能強大且靈活的擷取轉換和載入 (ETL) 工具，支援複雜的工作流程、資料轉換，以及數個資料載入選項。</span><span class="sxs-lookup"><span data-stu-id="26827-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="26827-122">使用 SSIS 來單純將資料傳輸至 Azure，或做為更廣泛移轉的一部分。</span><span class="sxs-lookup"><span data-stu-id="26827-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="26827-123">SSIS 可以匯出為 UTF-8，檔案中不需要有位元組順序標示。</span><span class="sxs-lookup"><span data-stu-id="26827-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="26827-124">若要這樣設定，您必須先使用衍生的資料行元件，轉換資料流程中的字元資料來使用 65001 UTF-8 字碼頁。</span><span class="sxs-lookup"><span data-stu-id="26827-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="26827-125">一旦轉換資料行之後，接著將資料寫入一般檔案目的地配接器，但要確定也已選取 65001 做為檔案的字碼頁。</span><span class="sxs-lookup"><span data-stu-id="26827-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="26827-126">SSIS 會連接到 SQL 資料倉儲，就像連接到 SQL Server 部署一樣。</span><span class="sxs-lookup"><span data-stu-id="26827-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="26827-127">不過，您的連線必須使用 ADO.NET 連接管理員。</span><span class="sxs-lookup"><span data-stu-id="26827-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="26827-128">您也應該小心設定「可用時使用大量插入」設定，以最大化輸送量。</span><span class="sxs-lookup"><span data-stu-id="26827-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="26827-129">請參閱 [ADO.NET 目的地配接器][ADO.NET destination adapter]文章，以深入了解該屬性</span><span class="sxs-lookup"><span data-stu-id="26827-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="26827-130">不支援使用 OLEDB 連接到 Azure SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="26827-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="26827-131">此外，封裝經常可能因為節流或網路問題而失敗。</span><span class="sxs-lookup"><span data-stu-id="26827-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="26827-132">請將封裝設計成可以從失敗點繼續，而不必重做失敗之前已完成的工作。</span><span class="sxs-lookup"><span data-stu-id="26827-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="26827-133">如需詳細資訊，請參閱 [SSIS 文件][SSIS documentation]。</span><span class="sxs-lookup"><span data-stu-id="26827-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="26827-134">bcp</span><span class="sxs-lookup"><span data-stu-id="26827-134">bcp</span></span>
<span data-ttu-id="26827-135">bcp 是專為一般檔案資料匯入和匯出所設計的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="26827-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="26827-136">資料匯出期間可能進行某些轉換。</span><span class="sxs-lookup"><span data-stu-id="26827-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="26827-137">若要執行簡單的轉換，請使用查詢來選取和轉換資料。</span><span class="sxs-lookup"><span data-stu-id="26827-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="26827-138">一旦匯出之後，一般檔案就可以直接載入到目標 SQL 資料倉儲資料庫。</span><span class="sxs-lookup"><span data-stu-id="26827-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="26827-139">通常建議將資料匯出時使用的轉換封裝在來源系統上的檢視表中。</span><span class="sxs-lookup"><span data-stu-id="26827-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="26827-140">這可確保邏輯得以保留，且程序是可重複。</span><span class="sxs-lookup"><span data-stu-id="26827-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="26827-141">bcp 的優點包括：</span><span class="sxs-lookup"><span data-stu-id="26827-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="26827-142">簡單。</span><span class="sxs-lookup"><span data-stu-id="26827-142">Simplicity.</span></span> <span data-ttu-id="26827-143">bcp 命令十分容易建置和執行</span><span class="sxs-lookup"><span data-stu-id="26827-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="26827-144">可重新啟動的載入程序。</span><span class="sxs-lookup"><span data-stu-id="26827-144">Re-startable load process.</span></span> <span data-ttu-id="26827-145">一旦匯出，即可不限次數執行載入</span><span class="sxs-lookup"><span data-stu-id="26827-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="26827-146">bcp 的限制包括：</span><span class="sxs-lookup"><span data-stu-id="26827-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="26827-147">bcp 只能使用列表式一般檔案。</span><span class="sxs-lookup"><span data-stu-id="26827-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="26827-148">無法使用 xml 或 JSON 之類的檔案</span><span class="sxs-lookup"><span data-stu-id="26827-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="26827-149">資料轉換功能僅限於匯出階段且性質簡單</span><span class="sxs-lookup"><span data-stu-id="26827-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="26827-150">當透過網際網路載入資料時，bcp 的設計尚不夠健全。</span><span class="sxs-lookup"><span data-stu-id="26827-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="26827-151">任何網路不穩定狀況都可能造成載入錯誤。</span><span class="sxs-lookup"><span data-stu-id="26827-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="26827-152">bcp 依賴載入之前存在於目標資料庫中的結構描述</span><span class="sxs-lookup"><span data-stu-id="26827-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="26827-153">如需詳細資訊，請參閱[使用 bcp 將資料載入 SQL 資料倉儲][Use bcp to load data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="26827-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="26827-154">最佳化資料移轉</span><span class="sxs-lookup"><span data-stu-id="26827-154">Optimizing data migration</span></span>
<span data-ttu-id="26827-155">SQLDW 資料移轉程序可以有效地分成三個獨立的步驟：</span><span class="sxs-lookup"><span data-stu-id="26827-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="26827-156">匯出來源資料</span><span class="sxs-lookup"><span data-stu-id="26827-156">Export of source data</span></span>
2. <span data-ttu-id="26827-157">將資料傳輸至 Azure</span><span class="sxs-lookup"><span data-stu-id="26827-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="26827-158">載入到目標 SQLDW 資料庫</span><span class="sxs-lookup"><span data-stu-id="26827-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="26827-159">每個步驟可以個別進行最佳化，建立健全、可重新啟動且富有彈性的移轉程序，讓每個步驟發揮最高的效能。</span><span class="sxs-lookup"><span data-stu-id="26827-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="26827-160">最佳化資料載入</span><span class="sxs-lookup"><span data-stu-id="26827-160">Optimizing data load</span></span>
<span data-ttu-id="26827-161">稍微反過來看。載入資料最快的方式是透過 PolyBase。</span><span class="sxs-lookup"><span data-stu-id="26827-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="26827-162">最佳化 PolyBase 載入程序對上述步驟設下必要條件，最好先了解這一點。</span><span class="sxs-lookup"><span data-stu-id="26827-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="26827-163">如下：</span><span class="sxs-lookup"><span data-stu-id="26827-163">They are:</span></span>

1. <span data-ttu-id="26827-164">資料檔案的編碼</span><span class="sxs-lookup"><span data-stu-id="26827-164">Encoding of data files</span></span>
2. <span data-ttu-id="26827-165">資料檔案的格式</span><span class="sxs-lookup"><span data-stu-id="26827-165">Format of data files</span></span>
3. <span data-ttu-id="26827-166">資料檔案的位置</span><span class="sxs-lookup"><span data-stu-id="26827-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="26827-167">編碼</span><span class="sxs-lookup"><span data-stu-id="26827-167">Encoding</span></span>
<span data-ttu-id="26827-168">PolyBase 規定資料檔案必須為 UTF-8 或 UTF-16FE。</span><span class="sxs-lookup"><span data-stu-id="26827-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="26827-169">資料檔案的格式</span><span class="sxs-lookup"><span data-stu-id="26827-169">Format of data files</span></span>
<span data-ttu-id="26827-170">PolyBase 規定要有固定的資料列結束字元 \n 或新行。</span><span class="sxs-lookup"><span data-stu-id="26827-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="26827-171">您的資料檔必須符合此標準。</span><span class="sxs-lookup"><span data-stu-id="26827-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="26827-172">字串或資料行結束字元沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="26827-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="26827-173">在 PolyBase 中，您必須將檔案中的每個資料行定義為外部資料表的一部分。</span><span class="sxs-lookup"><span data-stu-id="26827-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="26827-174">請確定所有匯出的資料行都是必要，且型別符合必要的標準。</span><span class="sxs-lookup"><span data-stu-id="26827-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="26827-175">如需有關支援的資料類型的詳細資料，請回頭參閱 [移轉您的結構描述] 文章。</span><span class="sxs-lookup"><span data-stu-id="26827-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="26827-176">資料檔案的位置</span><span class="sxs-lookup"><span data-stu-id="26827-176">Location of data files</span></span>
<span data-ttu-id="26827-177">SQL 資料倉儲只使用 PolyBase 從 Azure Blob 儲存體載入資料。</span><span class="sxs-lookup"><span data-stu-id="26827-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="26827-178">因此，資料必須先傳輸到 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="26827-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="26827-179">最佳化資料傳輸</span><span class="sxs-lookup"><span data-stu-id="26827-179">Optimizing data transfer</span></span>
<span data-ttu-id="26827-180">資料移轉過程中，最慢的一部分是將資料傳輸到 Azure。</span><span class="sxs-lookup"><span data-stu-id="26827-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="26827-181">不只網路頻寬可能是個問題，網路可靠性也可能嚴重阻礙進度。</span><span class="sxs-lookup"><span data-stu-id="26827-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="26827-182">依預設，將資料移轉至 Azure 是透過網際網路，因此相當可能發生傳輸錯誤。</span><span class="sxs-lookup"><span data-stu-id="26827-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="26827-183">不過，這些錯誤可能需要重新傳送整個或部分的資料。</span><span class="sxs-lookup"><span data-stu-id="26827-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="26827-184">所幸您有數個選項可以提升此程序的速度及恢復力：</span><span class="sxs-lookup"><span data-stu-id="26827-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="26827-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="26827-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="26827-186">您可以考慮使用 [ExpressRoute][ExpressRoute] 來加速傳輸。</span><span class="sxs-lookup"><span data-stu-id="26827-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="26827-187">[ExpressRoute][ExpressRoute] 會為您提供已建立的 Azure 私人連線，如此連線就不會經過公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="26827-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="26827-188">這絕不是必要的步驟。</span><span class="sxs-lookup"><span data-stu-id="26827-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="26827-189">不過，從內部部署或共置設備推送資料到 Azure 時，將會改善輸送量。</span><span class="sxs-lookup"><span data-stu-id="26827-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="26827-190">使用 [ExpressRoute][ExpressRoute] 的優點包括：</span><span class="sxs-lookup"><span data-stu-id="26827-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="26827-191">更高的可靠性</span><span class="sxs-lookup"><span data-stu-id="26827-191">Increased reliability</span></span>
2. <span data-ttu-id="26827-192">更快的網路速度</span><span class="sxs-lookup"><span data-stu-id="26827-192">Faster network speed</span></span>
3. <span data-ttu-id="26827-193">更短的網路延遲</span><span class="sxs-lookup"><span data-stu-id="26827-193">Lower network latency</span></span>
4. <span data-ttu-id="26827-194">更高的網路安全性</span><span class="sxs-lookup"><span data-stu-id="26827-194">higher network security</span></span>

<span data-ttu-id="26827-195">[ExpressRoute][ExpressRoute] 有利於許多情況，而不只是移轉。</span><span class="sxs-lookup"><span data-stu-id="26827-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="26827-196">有興趣嗎？</span><span class="sxs-lookup"><span data-stu-id="26827-196">Interested?</span></span> <span data-ttu-id="26827-197">如需詳細資訊和價格，請瀏覽 [ExpressRoute 文件][ExpressRoute documentation]。</span><span class="sxs-lookup"><span data-stu-id="26827-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="26827-198">Azure 匯入和匯出服務</span><span class="sxs-lookup"><span data-stu-id="26827-198">Azure Import and Export Service</span></span>
<span data-ttu-id="26827-199">Azure 匯入和匯出服務是針對大量 (GB++) 到巨量 (TB++) 的資料傳輸至 Azure 而設計的資料傳輸程序。</span><span class="sxs-lookup"><span data-stu-id="26827-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="26827-200">它牽涉到將您的資料寫入磁碟及傳送至 Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="26827-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="26827-201">然後會代替您將磁碟內容載入 Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="26827-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="26827-202">匯入匯出程序的高階觀點如下：</span><span class="sxs-lookup"><span data-stu-id="26827-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="26827-203">設定要接收資料的 Azure Blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="26827-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="26827-204">將資料匯出到本機儲存體</span><span class="sxs-lookup"><span data-stu-id="26827-204">Export your data to local storage</span></span>
3. <span data-ttu-id="26827-205">使用 [Azure 匯入/匯出工具] 將資料複製到 3.5 英吋 SATA II/III 硬碟機</span><span class="sxs-lookup"><span data-stu-id="26827-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="26827-206">使用 Azure 匯入和匯出服務，並提供 [Azure 匯入/匯出工具] 所產生的日誌檔案，建立匯入工作</span><span class="sxs-lookup"><span data-stu-id="26827-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="26827-207">將磁碟機寄送到指定的 Azure 資料中心</span><span class="sxs-lookup"><span data-stu-id="26827-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="26827-208">您的資料傳輸至 Azure Blob 儲存體容器</span><span class="sxs-lookup"><span data-stu-id="26827-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="26827-209">使用 PolyBase 將資料載入 SQLDW</span><span class="sxs-lookup"><span data-stu-id="26827-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="26827-210">[AZCopy][AZCopy] 公用程式</span><span class="sxs-lookup"><span data-stu-id="26827-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="26827-211">[AZCopy][AZCopy] 公用程式是將資料傳輸至 Azure 儲存體 Blob 的一個極佳工具。</span><span class="sxs-lookup"><span data-stu-id="26827-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="26827-212">它是針對少量 (MB++) 到非常大量 (GB++) 資料傳輸而設計。</span><span class="sxs-lookup"><span data-stu-id="26827-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="26827-213">[AZCopy] 也設計成將資料傳輸到 Azure 時提供絕佳彈性的輸送量，因此是資料傳輸步驟的理想選擇。</span><span class="sxs-lookup"><span data-stu-id="26827-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="26827-214">一旦傳輸之後，您就可以使用 PolyBase 將資料載入 SQL 資料倉儲。</span><span class="sxs-lookup"><span data-stu-id="26827-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="26827-215">您也可以使用「執行程序」工作，將 AZCopy 納入 SSIS 封裝。</span><span class="sxs-lookup"><span data-stu-id="26827-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="26827-216">若要使用 AZCopy，您必須先下載並安裝它。</span><span class="sxs-lookup"><span data-stu-id="26827-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="26827-217">有[生產版本][production version]和[預覽版本][preview version]可用。</span><span class="sxs-lookup"><span data-stu-id="26827-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="26827-218">若要從檔案系統上傳檔案，您需要如下所示的命令：</span><span class="sxs-lookup"><span data-stu-id="26827-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="26827-219">高階程序摘要如下：</span><span class="sxs-lookup"><span data-stu-id="26827-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="26827-220">設定要接收資料的 Azure 儲存體 blob 容器</span><span class="sxs-lookup"><span data-stu-id="26827-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="26827-221">將資料匯出到本機儲存體</span><span class="sxs-lookup"><span data-stu-id="26827-221">Export your data to local storage</span></span>
3. <span data-ttu-id="26827-222">AZCopy 您在 Azure Blob 儲存體容器中的資料</span><span class="sxs-lookup"><span data-stu-id="26827-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="26827-223">使用 PolyBase 將資料載入 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="26827-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="26827-224">有完整的文件：[AZCopy][AZCopy]。</span><span class="sxs-lookup"><span data-stu-id="26827-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="26827-225">最佳化資料匯出</span><span class="sxs-lookup"><span data-stu-id="26827-225">Optimizing data export</span></span>
<span data-ttu-id="26827-226">除了確保匯出符合 PolyBase 所規定的需求，您也可以設法最佳化資料匯出，以進一步改善程序。</span><span class="sxs-lookup"><span data-stu-id="26827-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="26827-227">資料壓縮</span><span class="sxs-lookup"><span data-stu-id="26827-227">Data compression</span></span>
<span data-ttu-id="26827-228">PolyBase 可以讀取 gzip 壓縮的資料。</span><span class="sxs-lookup"><span data-stu-id="26827-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="26827-229">如果您可以將資料壓縮成 gzip 檔案，就能將網路上推送的資料量減到最少。</span><span class="sxs-lookup"><span data-stu-id="26827-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="26827-230">多個檔案</span><span class="sxs-lookup"><span data-stu-id="26827-230">Multiple files</span></span>
<span data-ttu-id="26827-231">將大型資料表分割成數個檔案，不僅有助於改善匯出速度，也有助於重新開始傳輸，以及資料進入 Azure blob 儲存體之後的整體管理能力。</span><span class="sxs-lookup"><span data-stu-id="26827-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="26827-232">PolyBase 的眾多優點之一是它會讀取資料夾內的所有檔案，並視為一個資料表來處理。</span><span class="sxs-lookup"><span data-stu-id="26827-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="26827-233">因此，最好將每個資料表的檔案隔離到它自己的資料夾。</span><span class="sxs-lookup"><span data-stu-id="26827-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="26827-234">PolyBase 也支援一項稱為「遞迴資料夾周遊」的功能。</span><span class="sxs-lookup"><span data-stu-id="26827-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="26827-235">您可以使用這項功能來進一步加強組織您匯出的資料，以改善資料管理。</span><span class="sxs-lookup"><span data-stu-id="26827-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="26827-236">若要深入了解使用 PolyBase 載入資料，請參閱[使用 PolyBase 將資料載入 SQL 資料倉儲][Use PolyBase to load data into SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="26827-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="26827-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26827-237">Next steps</span></span>
<span data-ttu-id="26827-238">如需有關移轉的詳細資訊，請參閱[將您的解決方案移轉至 SQL 資料倉儲][Migrate your solution to SQL Data Warehouse]。</span><span class="sxs-lookup"><span data-stu-id="26827-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="26827-239">如需更多開發秘訣，請參閱[開發概觀][development overview]。</span><span class="sxs-lookup"><span data-stu-id="26827-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
