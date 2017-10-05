---
title: "Azure SQL 資料倉儲常見問題集 | Microsoft Docs"
description: "此文章列出客戶和開發人員針對 Azure SQL 資料倉儲的常見問題集"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 4c00710ecc0c91f8407eca81b78176075fcbd6ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="b4a6b-103">SQL 資料倉儲常見問題集</span><span class="sxs-lookup"><span data-stu-id="b4a6b-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="b4a6b-104">一般</span><span class="sxs-lookup"><span data-stu-id="b4a6b-104">General</span></span>

<span data-ttu-id="b4a6b-105">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-105">Q.</span></span> <span data-ttu-id="b4a6b-106">針對資料安全性，SQL DW 能提供什麼？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="b4a6b-107">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-107">A.</span></span> <span data-ttu-id="b4a6b-108">SQL DW 提供數個解決方案來保護資料，例如 TDE 和稽核。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="b4a6b-109">如需詳細資訊，請參閱[安全性]。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-109">For more information, see [Security].</span></span>

<span data-ttu-id="b4a6b-110">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-110">Q.</span></span> <span data-ttu-id="b4a6b-111">哪裡可以了解 SQL DW 符合規範的法規或企業標準？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="b4a6b-112">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-112">A.</span></span> <span data-ttu-id="b4a6b-113">請造訪 [Microsoft 合規性]頁面，依產品取得不同的合規性供應項目，例如 SOC 和 ISO。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-113">Visit the [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="b4a6b-114">首先依「合規性」標題選擇，然後在頁面右側的 [Microsoft 範圍內雲端服務] 區段中展開 [Azure]，以查看 Azure 服務符合規範的服務。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-114">First choose by Compliance title, then expand Azure in the Microsoft in-scope cloud services section on the right side of the page to see what services are Azure services are compliant.</span></span>

<span data-ttu-id="b4a6b-115">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-115">Q.</span></span> <span data-ttu-id="b4a6b-116">可以連接 PowerBI 嗎？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="b4a6b-117">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-117">A.</span></span> <span data-ttu-id="b4a6b-118">可以！</span><span class="sxs-lookup"><span data-stu-id="b4a6b-118">Yes!</span></span> <span data-ttu-id="b4a6b-119">雖然 PowerBI 針對 SQL DW 支援直接查詢，但它並不適用於具有大量使用者或即時資料的情況。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="b4a6b-120">針對 PowerBI 的生產用途，建議您在 Azure Analysis Services 或 Analysis Service IaaS 之上使用 PowerBI。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="b4a6b-121">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-121">Q.</span></span> <span data-ttu-id="b4a6b-122">SQL 資料倉儲的容量限制為何？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="b4a6b-123">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-123">A.</span></span> <span data-ttu-id="b4a6b-124">請參閱我們目前的[容量限制]頁面。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="b4a6b-125">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-125">Q.</span></span> <span data-ttu-id="b4a6b-126">為何我的延展/暫停/繼續需要花很久的時間？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="b4a6b-127">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-127">A.</span></span> <span data-ttu-id="b4a6b-128">有很多因素可能會影響計算管理作業的時間。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-128">A variety of factors can influence the time for compute management operations.</span></span> <span data-ttu-id="b4a6b-129">一個導致長時間執行作業的常見原因是交易式回復。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="b4a6b-130">初始化延展或暫停作業時，系統會封鎖所有傳入的工作階段，並清空查詢。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="b4a6b-131">為了使系統能處於穩定的狀態，必須先回復交易才能開始作業。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-131">In order to leave the system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="b4a6b-132">交易數目越多，或是交易記錄檔的大小越大，將系統還原至穩定的狀態所需的時間便越長，因此使作業停止的時間變得更久。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-132">The greater the number and larger the log size of transactions, the longer the operation will be stalled restoring the system to a stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="b4a6b-133">使用者支援</span><span class="sxs-lookup"><span data-stu-id="b4a6b-133">User support</span></span>

<span data-ttu-id="b4a6b-134">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-134">Q.</span></span> <span data-ttu-id="b4a6b-135">我有一個功能要求，應該在哪裡提交？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="b4a6b-136">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-136">A.</span></span> <span data-ttu-id="b4a6b-137">如果您有功能要求，請在我們的 [UserVoice] 頁面上提交</span><span class="sxs-lookup"><span data-stu-id="b4a6b-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="b4a6b-138">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-138">Q.</span></span> <span data-ttu-id="b4a6b-139">我要如何執行某項作業？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-139">How can I do x?</span></span>

<span data-ttu-id="b4a6b-140">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-140">A.</span></span> <span data-ttu-id="b4a6b-141">如需使用 SQL 資料倉儲進行開發的說明，您可以在我們的 [Stack Overflow] 頁面上提問。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="b4a6b-142">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-142">Q.</span></span> <span data-ttu-id="b4a6b-143">我要如何提交支援票證？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="b4a6b-144">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-144">A.</span></span> <span data-ttu-id="b4a6b-145">[支援票證]可以透過 Azure 入口網站提出。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="b4a6b-146">SQL 語言/功能支援</span><span class="sxs-lookup"><span data-stu-id="b4a6b-146">SQL language/feature support</span></span> 

<span data-ttu-id="b4a6b-147">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-147">Q.</span></span> <span data-ttu-id="b4a6b-148">SQL 資料倉儲支援的資料類型為何？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="b4a6b-149">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-149">A.</span></span> <span data-ttu-id="b4a6b-150">請參閱 SQL 資料倉儲[資料類型]。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="b4a6b-151">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-151">Q.</span></span> <span data-ttu-id="b4a6b-152">支援哪些資料表功能？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-152">What table features do you support?</span></span>

<span data-ttu-id="b4a6b-153">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-153">A.</span></span> <span data-ttu-id="b4a6b-154">SQL 資料倉儲支援許多功能，不支援的功能都已記錄在[不支援的資料表功能]之中。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="b4a6b-155">工具和系統管理</span><span class="sxs-lookup"><span data-stu-id="b4a6b-155">Tooling and administration</span></span>

<span data-ttu-id="b4a6b-156">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-156">Q.</span></span> <span data-ttu-id="b4a6b-157">在 Visual Studio 中是否支援資料庫專案？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="b4a6b-158">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-158">A.</span></span> <span data-ttu-id="b4a6b-159">針對 SQL 資料倉儲，我們目前在 Visual Studio 中不支援資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="b4a6b-160">如果您希望投票以取得此功能，請造訪我們的 User Voice [資料庫專案功能要求]。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-160">If you'd like to cast a vote to get this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="b4a6b-161">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-161">Q.</span></span> <span data-ttu-id="b4a6b-162">SQL 資料倉儲是否支援 REST API？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="b4a6b-163">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-163">A.</span></span> <span data-ttu-id="b4a6b-164">是。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-164">Yes.</span></span> <span data-ttu-id="b4a6b-165">大部分可以搭配 SQL Database 使用的 REST 功能也可搭配 SQL 資料倉儲使用。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="b4a6b-166">您可以在 REST 文件頁面或 [MSDN] 內找到 API 資訊。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="b4a6b-167">載入</span><span class="sxs-lookup"><span data-stu-id="b4a6b-167">Loading</span></span>

<span data-ttu-id="b4a6b-168">問：</span><span class="sxs-lookup"><span data-stu-id="b4a6b-168">Q.</span></span> <span data-ttu-id="b4a6b-169">支援哪些用戶端驅動程式？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-169">What client drivers do you support?</span></span>

<span data-ttu-id="b4a6b-170">A.</span><span class="sxs-lookup"><span data-stu-id="b4a6b-170">A.</span></span> <span data-ttu-id="b4a6b-171">如需 DW 的驅動程式支援，請參閱[連接字串]頁面</span><span class="sxs-lookup"><span data-stu-id="b4a6b-171">Driver support for DW can be found on the [Connection Strings] page</span></span>

<span data-ttu-id="b4a6b-172">問︰PolyBase 針對 SQL 資料倉儲支援何種檔案格式？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="b4a6b-173">答︰Orc、RC、Parquet，以及一般分隔的文字</span><span class="sxs-lookup"><span data-stu-id="b4a6b-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="b4a6b-174">問︰我可以從 SQL DW 使用 PolyBase 連線到哪裡？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-174">Q: What can I connect to from SQL DW using PolyBase?</span></span> 

<span data-ttu-id="b4a6b-175">答︰[Azure Data Lake Store] 和 [Azure 儲存體 Blob]</span><span class="sxs-lookup"><span data-stu-id="b4a6b-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="b4a6b-176">問︰連線到 Azure 儲存體 Blob 或 ADLS 時，是否有可能進行計算下推？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-176">Q: Is computation pushdown possible  when connecting to Azure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="b4a6b-177">答︰否，SQL DW PolyBase 只能和儲存元件互動。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-177">A: No, SQL DW PolyBase only interacts the storage components.</span></span> 

<span data-ttu-id="b4a6b-178">問︰是否可以連線到 HDI？</span><span class="sxs-lookup"><span data-stu-id="b4a6b-178">Q: Can I connect to HDI?</span></span>

<span data-ttu-id="b4a6b-179">答︰HDI 可以使用 ADLS 或 WASB 作為 HDFS 層。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-179">A: HDI can use either ADLS or WASB as the HDFS layer.</span></span> <span data-ttu-id="b4a6b-180">如果您使用其中之一作為您的 HDFS 層，則您可以將該資料載入到 SQL DW。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="b4a6b-181">不過，您無法針對 HDI 執行個體產生下推計算。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-181">However, you cannot generate pushdown computation to the HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b4a6b-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4a6b-182">Next steps</span></span>
<span data-ttu-id="b4a6b-183">如需整體 SQL 資料倉儲的詳細資訊，請參閱我們的[概觀]頁面。</span><span class="sxs-lookup"><span data-stu-id="b4a6b-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
<span data-ttu-id="b4a6b-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span><span class="sxs-lookup"><span data-stu-id="b4a6b-184">[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse</span></span>
<span data-ttu-id="b4a6b-185">[連接字串]: ./sql-data-warehouse-connection-strings.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-185">[Connection Strings]: ./sql-data-warehouse-connection-strings.md</span></span>
<span data-ttu-id="b4a6b-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span><span class="sxs-lookup"><span data-stu-id="b4a6b-186">[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw</span></span>
<span data-ttu-id="b4a6b-187">[支援票證]: ./sql-data-warehouse-get-started-create-support-ticket.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-187">[Support Tickets]: ./sql-data-warehouse-get-started-create-support-ticket.md</span></span>
<span data-ttu-id="b4a6b-188">[安全性]: ./sql-data-warehouse-overview-manage-security.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-188">[Security]: ./sql-data-warehouse-overview-manage-security.md</span></span>
<span data-ttu-id="b4a6b-189">[Microsoft 合規性]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span><span class="sxs-lookup"><span data-stu-id="b4a6b-189">[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings</span></span>
<span data-ttu-id="b4a6b-190">[容量限制]: ./sql-data-warehouse-service-capacity-limits.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-190">[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md</span></span>
<span data-ttu-id="b4a6b-191">[資料類型]: ./sql-data-warehouse-tables-data-types.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-191">[data types]: ./sql-data-warehouse-tables-data-types.md</span></span>
<span data-ttu-id="b4a6b-192">[不支援的資料表功能]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span><span class="sxs-lookup"><span data-stu-id="b4a6b-192">[Unsupported Table Features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features</span></span>
<span data-ttu-id="b4a6b-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-193">[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md</span></span>
<span data-ttu-id="b4a6b-194">[Azure 儲存體 Blob]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-194">[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md</span></span>
<span data-ttu-id="b4a6b-195">[資料庫專案功能要求]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span><span class="sxs-lookup"><span data-stu-id="b4a6b-195">[Database projects feature request]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu</span></span>
<span data-ttu-id="b4a6b-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span><span class="sxs-lookup"><span data-stu-id="b4a6b-196">[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx</span></span>
<span data-ttu-id="b4a6b-197">[概觀]: ./sql-data-warehouse-overview-faq.md</span><span class="sxs-lookup"><span data-stu-id="b4a6b-197">[Overview]: ./sql-data-warehouse-overview-faq.md</span></span>