---
title: "aaaAzure SQL 資料倉儲常見問題集 |Microsoft 文件"
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
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="42d82-103">SQL 資料倉儲常見問題集</span><span class="sxs-lookup"><span data-stu-id="42d82-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="42d82-104">一般</span><span class="sxs-lookup"><span data-stu-id="42d82-104">General</span></span>

<span data-ttu-id="42d82-105">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-105">Q.</span></span> <span data-ttu-id="42d82-106">針對資料安全性，SQL DW 能提供什麼？</span><span class="sxs-lookup"><span data-stu-id="42d82-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="42d82-107">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-107">A.</span></span> <span data-ttu-id="42d82-108">SQL DW 提供數個解決方案來保護資料，例如 TDE 和稽核。</span><span class="sxs-lookup"><span data-stu-id="42d82-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="42d82-109">如需詳細資訊，請參閱[安全性]。</span><span class="sxs-lookup"><span data-stu-id="42d82-109">For more information, see [Security].</span></span>

<span data-ttu-id="42d82-110">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-110">Q.</span></span> <span data-ttu-id="42d82-111">哪裡可以了解 SQL DW 符合規範的法規或企業標準？</span><span class="sxs-lookup"><span data-stu-id="42d82-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="42d82-112">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-112">A.</span></span> <span data-ttu-id="42d82-113">請瀏覽 hello [Microsoft 相容性]為不同的相容性供應項目依產品，例如 SOC 和 ISO 頁。</span><span class="sxs-lookup"><span data-stu-id="42d82-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="42d82-114">先選擇相容性標題，然後依序展開 [Azure hello Microsoft 範圍中雲端服務] 區段中 hello 右側的 hello 頁面 toosee 何種服務是 Azure 服務都相容。</span><span class="sxs-lookup"><span data-stu-id="42d82-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="42d82-115">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-115">Q.</span></span> <span data-ttu-id="42d82-116">可以連接 PowerBI 嗎？</span><span class="sxs-lookup"><span data-stu-id="42d82-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="42d82-117">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-117">A.</span></span> <span data-ttu-id="42d82-118">可以！</span><span class="sxs-lookup"><span data-stu-id="42d82-118">Yes!</span></span> <span data-ttu-id="42d82-119">雖然 PowerBI 針對 SQL DW 支援直接查詢，但它並不適用於具有大量使用者或即時資料的情況。</span><span class="sxs-lookup"><span data-stu-id="42d82-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="42d82-120">針對 PowerBI 的生產用途，建議您在 Azure Analysis Services 或 Analysis Service IaaS 之上使用 PowerBI。</span><span class="sxs-lookup"><span data-stu-id="42d82-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="42d82-121">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-121">Q.</span></span> <span data-ttu-id="42d82-122">SQL 資料倉儲的容量限制為何？</span><span class="sxs-lookup"><span data-stu-id="42d82-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="42d82-123">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-123">A.</span></span> <span data-ttu-id="42d82-124">請參閱我們目前的[容量限制]頁面。</span><span class="sxs-lookup"><span data-stu-id="42d82-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="42d82-125">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-125">Q.</span></span> <span data-ttu-id="42d82-126">為何我的延展/暫停/繼續需要花很久的時間？</span><span class="sxs-lookup"><span data-stu-id="42d82-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="42d82-127">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-127">A.</span></span> <span data-ttu-id="42d82-128">有許多因素可能會影響 hello 計算管理作業的時間。</span><span class="sxs-lookup"><span data-stu-id="42d82-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="42d82-129">一個導致長時間執行作業的常見原因是交易式回復。</span><span class="sxs-lookup"><span data-stu-id="42d82-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="42d82-130">初始化延展或暫停作業時，系統會封鎖所有傳入的工作階段，並清空查詢。</span><span class="sxs-lookup"><span data-stu-id="42d82-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="42d82-131">穩定的狀態中的順序 tooleave hello 系統，必須備份作業開始之前先回復交易。</span><span class="sxs-lookup"><span data-stu-id="42d82-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="42d82-132">hello 大量 hello 和較大的交易的 hello 記錄檔大小、 hello 長 hello 作業將會停止還原 hello 系統 tooa 穩定的狀態。</span><span class="sxs-lookup"><span data-stu-id="42d82-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="42d82-133">使用者支援</span><span class="sxs-lookup"><span data-stu-id="42d82-133">User support</span></span>

<span data-ttu-id="42d82-134">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-134">Q.</span></span> <span data-ttu-id="42d82-135">我有一個功能要求，應該在哪裡提交？</span><span class="sxs-lookup"><span data-stu-id="42d82-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="42d82-136">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-136">A.</span></span> <span data-ttu-id="42d82-137">如果您有功能要求，請在我們的 [UserVoice] 頁面上提交</span><span class="sxs-lookup"><span data-stu-id="42d82-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="42d82-138">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-138">Q.</span></span> <span data-ttu-id="42d82-139">我要如何執行某項作業？</span><span class="sxs-lookup"><span data-stu-id="42d82-139">How can I do x?</span></span>

<span data-ttu-id="42d82-140">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-140">A.</span></span> <span data-ttu-id="42d82-141">如需使用 SQL 資料倉儲進行開發的說明，您可以在我們的 [Stack Overflow] 頁面上提問。</span><span class="sxs-lookup"><span data-stu-id="42d82-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="42d82-142">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-142">Q.</span></span> <span data-ttu-id="42d82-143">我要如何提交支援票證？</span><span class="sxs-lookup"><span data-stu-id="42d82-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="42d82-144">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-144">A.</span></span> <span data-ttu-id="42d82-145">[支援票證]可以透過 Azure 入口網站提出。</span><span class="sxs-lookup"><span data-stu-id="42d82-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="42d82-146">SQL 語言/功能支援</span><span class="sxs-lookup"><span data-stu-id="42d82-146">SQL language/feature support</span></span> 

<span data-ttu-id="42d82-147">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-147">Q.</span></span> <span data-ttu-id="42d82-148">SQL 資料倉儲支援的資料類型為何？</span><span class="sxs-lookup"><span data-stu-id="42d82-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="42d82-149">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-149">A.</span></span> <span data-ttu-id="42d82-150">請參閱 SQL 資料倉儲[資料類型]。</span><span class="sxs-lookup"><span data-stu-id="42d82-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="42d82-151">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-151">Q.</span></span> <span data-ttu-id="42d82-152">支援哪些資料表功能？</span><span class="sxs-lookup"><span data-stu-id="42d82-152">What table features do you support?</span></span>

<span data-ttu-id="42d82-153">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-153">A.</span></span> <span data-ttu-id="42d82-154">SQL 資料倉儲支援許多功能，不支援的功能都已記錄在[不支援的資料表功能]之中。</span><span class="sxs-lookup"><span data-stu-id="42d82-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="42d82-155">工具和系統管理</span><span class="sxs-lookup"><span data-stu-id="42d82-155">Tooling and administration</span></span>

<span data-ttu-id="42d82-156">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-156">Q.</span></span> <span data-ttu-id="42d82-157">在 Visual Studio 中是否支援資料庫專案？</span><span class="sxs-lookup"><span data-stu-id="42d82-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="42d82-158">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-158">A.</span></span> <span data-ttu-id="42d82-159">針對 SQL 資料倉儲，我們目前在 Visual Studio 中不支援資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="42d82-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="42d82-160">如果您想要 toocast 投票 tooget 這項功能，請造訪我們的 User Voice[資料庫專案功能要求]。</span><span class="sxs-lookup"><span data-stu-id="42d82-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="42d82-161">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-161">Q.</span></span> <span data-ttu-id="42d82-162">SQL 資料倉儲是否支援 REST API？</span><span class="sxs-lookup"><span data-stu-id="42d82-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="42d82-163">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-163">A.</span></span> <span data-ttu-id="42d82-164">是。</span><span class="sxs-lookup"><span data-stu-id="42d82-164">Yes.</span></span> <span data-ttu-id="42d82-165">大部分可以搭配 SQL Database 使用的 REST 功能也可搭配 SQL 資料倉儲使用。</span><span class="sxs-lookup"><span data-stu-id="42d82-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="42d82-166">您可以在 REST 文件頁面或 [MSDN] 內找到 API 資訊。</span><span class="sxs-lookup"><span data-stu-id="42d82-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="42d82-167">載入</span><span class="sxs-lookup"><span data-stu-id="42d82-167">Loading</span></span>

<span data-ttu-id="42d82-168">問：</span><span class="sxs-lookup"><span data-stu-id="42d82-168">Q.</span></span> <span data-ttu-id="42d82-169">支援哪些用戶端驅動程式？</span><span class="sxs-lookup"><span data-stu-id="42d82-169">What client drivers do you support?</span></span>

<span data-ttu-id="42d82-170">A.</span><span class="sxs-lookup"><span data-stu-id="42d82-170">A.</span></span> <span data-ttu-id="42d82-171">可以在 hello 找到驅動程式支援的 DW[連接字串]頁面</span><span class="sxs-lookup"><span data-stu-id="42d82-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="42d82-172">問︰PolyBase 針對 SQL 資料倉儲支援何種檔案格式？</span><span class="sxs-lookup"><span data-stu-id="42d82-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="42d82-173">答︰Orc、RC、Parquet，以及一般分隔的文字</span><span class="sxs-lookup"><span data-stu-id="42d82-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="42d82-174">問： 我可以連接 toofrom SQL DW 使用 PolyBase？</span><span class="sxs-lookup"><span data-stu-id="42d82-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="42d82-175">答︰[Azure Data Lake Store] 和 [Azure 儲存體 Blob]</span><span class="sxs-lookup"><span data-stu-id="42d82-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="42d82-176">問： 是否計算下推可能連接儲存體 Blob 或 ADLS tooAzure 時？</span><span class="sxs-lookup"><span data-stu-id="42d82-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="42d82-177">答： 否，SQL DW PolyBase 僅互動 hello 儲存元件。</span><span class="sxs-lookup"><span data-stu-id="42d82-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="42d82-178">問： 是否可以連線 tooHDI？</span><span class="sxs-lookup"><span data-stu-id="42d82-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="42d82-179">答： HDI 可以使用 ADLS 或 WASB hello HDFS 圖層。</span><span class="sxs-lookup"><span data-stu-id="42d82-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="42d82-180">如果您使用其中之一作為您的 HDFS 層，則您可以將該資料載入到 SQL DW。</span><span class="sxs-lookup"><span data-stu-id="42d82-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="42d82-181">不過，您無法產生下推計算 toohello HDI 執行個體。</span><span class="sxs-lookup"><span data-stu-id="42d82-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="42d82-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42d82-182">Next steps</span></span>
<span data-ttu-id="42d82-183">如需整體 SQL 資料倉儲的詳細資訊，請參閱我們的[概觀]頁面。</span><span class="sxs-lookup"><span data-stu-id="42d82-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[連接字串]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[支援票證]: ./sql-data-warehouse-get-started-create-support-ticket.md
[安全性]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft 相容性]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[容量限制]: ./sql-data-warehouse-service-capacity-limits.md
[資料類型]: ./sql-data-warehouse-tables-data-types.md
[不支援的資料表功能]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure 儲存體 Blob]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[資料庫專案功能要求]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[概觀]: ./sql-data-warehouse-overview-faq.md