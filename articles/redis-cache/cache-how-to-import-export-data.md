---
title: "aaaImport 和匯出 Azure Redis 快取中的資料 |Microsoft 文件"
description: "深入了解如何從 premium 的 Azure Redis 快取執行個體的 blob 儲存體 tooimport 和匯出資料 tooand"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 4a68ac38-87af-4075-adab-569d37d7cc9e
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: sdanie
ms.openlocfilehash: f17464b207f1c652952f4da63ca147473fee2759
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="1c5ce-103">在 Azure Redis 快取中匯入與匯出資料</span><span class="sxs-lookup"><span data-stu-id="1c5ce-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="1c5ce-104">匯入/匯出為 Azure Redis 快取資料管理作業，可讓您 tooimport 資料至 Azure Redis 快取或匯出資料，從 Azure Redis 快取所匯入和匯出從 premium 快取 tooa blob 在 Azure Redis 快取資料庫 (RDB) 快照集儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-104">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="1c5ce-105">**匯出**-您可以匯出您的 Azure Redis 快取 RDB 快照 tooa 分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-105">**Export** - you can export your Azure Redis Cache RDB snapshots tooa Page Blob.</span></span>
- <span data-ttu-id="1c5ce-106">**匯入** - 您可以從分頁 Blob 或區塊 Blob 匯入您的 Redis 快取 RDB 快照集。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="1c5ce-107">匯入/匯出可讓您 toomigrate 不同的 Azure Redis 快取執行個體之間，或填入 hello 快取，以使用之前的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-107">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="1c5ce-108">本文提供的匯入和匯出與 Azure Redis 快取資料的指南，並提供 hello 答案 toocommonly 常見問題。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides hello answers toocommonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c5ce-109">匯入/匯出僅供預覽，只供 [進階層](cache-premium-tier-intro.md) 快取使用。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="1c5ce-110">Import</span><span class="sxs-lookup"><span data-stu-id="1c5ce-110">Import</span></span>
<span data-ttu-id="1c5ce-111">匯入可為使用的 toobring Redis 相容 RDB 檔案從任何執行中的任何雲端或環境，包括 Linux、 Windows 或任何雲端提供者，例如 Amazon Web Services 等項目上執行的 Redis 的 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-111">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="1c5ce-112">匯入資料是簡單的方式 toocreate 預先填入資料的快取。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-112">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="1c5ce-113">在 hello 匯入過程中，Azure Redis 快取 Azure 儲存體中的 hello RDB 檔案載入記憶體，然後插入 hello 快取中的 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-113">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory and then inserts hello keys into hello cache.</span></span>

> [!NOTE]
> <span data-ttu-id="1c5ce-114">開始之前 hello 匯入作業，請確定您的 Redis 資料庫 (RDB) 檔案上傳到頁面上，或區塊 blob 在 Azure 儲存體，在 hello 相同地區和訂用帳戶與您的 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-114">Before beginning hello import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in hello same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="1c5ce-115">如需詳細資訊，請參閱 [開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="1c5ce-116">如果您匯出 RDB 檔案使用 hello [Azure Redis 快取匯出](#export)功能 RDB 檔案已儲存在分頁 blob 的和可供匯入。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-116">If you exported your RDB file using hello [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="1c5ce-117">一或多個 tooimport 匯出快取 blob[瀏覽 tooyour 快取](cache-configure.md#configure-redis-cache-settings)在 hello Azure 入口網站，然後按一下**匯入資料**hello 從**資源功能表**。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-117">tooimport one or more exported cache blobs, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Import data** from hello **Resource menu**.</span></span>

    ![匯入資料][cache-import-data]
2. <span data-ttu-id="1c5ce-119">按一下**選擇 blob**並選取包含 hello 資料 tooimport hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-119">Click **Choose Blob(s)** and select hello storage account that contains hello data tooimport.</span></span>

    ![Choose storage account][cache-import-choose-storage-account]
3. <span data-ttu-id="1c5ce-121">按一下包含 hello 資料 tooimport hello 容器。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-121">Click hello container that contains hello data tooimport.</span></span>

    ![選擇容器][cache-import-choose-container]
4. <span data-ttu-id="1c5ce-123">選取一或多個 blob tooimport 按一下 hello 區域 toohello hello blob 名稱左邊，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-123">Select one or more blobs tooimport by clicking hello area toohello left of hello blob name, and then click **Select**.</span></span>

    ![選擇 blob][cache-import-choose-blobs]
5. <span data-ttu-id="1c5ce-125">按一下**匯入**toobegin hello 匯入程序。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-125">Click **Import** toobegin hello import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1c5ce-126">hello 快取的快取用戶端可存取 hello 匯入程序，並不會刪除任何現有資料 hello 快取中。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-126">hello cache is not accessible by cache clients during hello import process, and any existing data in hello cache is deleted.</span></span>
   >
   >

    ![Import][cache-import-blobs]

    <span data-ttu-id="1c5ce-128">您可以在 hello Azure 入口網站的下列 hello 通知或藉由在 hello 檢視 hello 事件監視 hello hello 匯入作業的進度[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-128">You can monitor hello progress of hello import operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![匯入進度][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="1c5ce-130">匯出</span><span class="sxs-lookup"><span data-stu-id="1c5ce-130">Export</span></span>
<span data-ttu-id="1c5ce-131">匯出可讓您 tooexport hello 資料儲存在 Azure Redis 快取 tooRedis 相容 RDB 檔案中。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-131">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB file(s).</span></span> <span data-ttu-id="1c5ce-132">您可以使用此功能 toomove 資料從一個 Azure Redis 快取執行個體 tooanother 或 tooanother Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-132">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="1c5ce-133">在 hello 匯出程序，hello VM 的主機 hello Azure Redis 快取伺服器執行個體，而且 hello 檔案上傳的 toohello 指定儲存體帳戶上建立暫存檔。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-133">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="1c5ce-134">Hello 匯出作業完成時為其中一個狀態為成功或失敗，則會刪除 hello 暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-134">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

1. <span data-ttu-id="1c5ce-135">tooexport hello 目前內容的 hello 快取 toostorage，[瀏覽 tooyour 快取](cache-configure.md#configure-redis-cache-settings)在 hello Azure 入口網站，然後按一下**匯出資料**從 hello**資源功能表**。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-135">tooexport hello current contents of hello cache toostorage, [browse tooyour cache](cache-configure.md#configure-redis-cache-settings) in hello Azure portal and click **Export data** from hello **Resource menu**.</span></span>

    ![選擇儲存體容器][cache-export-data-choose-storage-container]
2. <span data-ttu-id="1c5ce-137">按一下**選擇儲存體容器**及選取所需的 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-137">Click **Choose Storage Container** and select hello desired storage account.</span></span> <span data-ttu-id="1c5ce-138">hello hello 儲存體帳戶必須是相同的訂用帳戶和與您的快取的區域。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-138">hello storage account must be in hello same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1c5ce-139">匯出使用分頁 Blob，傳統和 Resource Manager 儲存體帳戶支援這些 Blob，但 [Blob 儲存體帳戶](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)目前不支援。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![儲存體帳戶][cache-export-data-choose-account]
3. <span data-ttu-id="1c5ce-141">選擇 hello 預期 blob 容器，然後按一下**選取**。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-141">Choose hello desired blob container and click **Select**.</span></span> <span data-ttu-id="1c5ce-142">toouse 新的容器，按一下**Add Container** tooadd 它第一次，然後選取從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-142">toouse new a container, click **Add Container** tooadd it first and then select it from hello list.</span></span>

    ![選擇儲存體容器][cache-export-data-container]
4. <span data-ttu-id="1c5ce-144">輸入**Blob 名稱前置詞**按一下**匯出**toostart hello 匯出程序。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-144">Type a **Blob name prefix** and click **Export** toostart hello export process.</span></span> <span data-ttu-id="1c5ce-145">hello blob 名稱前置詞是使用的 tooprefix hello 這個匯出作業所產生的檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-145">hello blob name prefix is used tooprefix hello names of files generated by this export operation.</span></span>

    ![匯出][cache-export-data]

    <span data-ttu-id="1c5ce-147">您可以在 hello Azure 入口網站的下列 hello 通知或藉由在 hello 檢視 hello 事件監視 hello hello 匯出作業的進度[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-147">You can monitor hello progress of hello export operation by following hello notifications from hello Azure portal, or by viewing hello events in hello [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![匯出資料完成][cache-export-data-export-complete]

    <span data-ttu-id="1c5ce-149">Hello 匯出程序期間，快取保持可供使用。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-149">Caches remain available for use during hello export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="1c5ce-150">匯入/匯出常見問題集</span><span class="sxs-lookup"><span data-stu-id="1c5ce-150">Import/Export FAQ</span></span>
<span data-ttu-id="1c5ce-151">本節中的 hello 匯入/匯出功能的相關常見問題的解答。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-151">This section contains frequently asked questions about hello Import/Export feature.</span></span>

* [<span data-ttu-id="1c5ce-152">哪些定價層可以使用匯入/匯出？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="1c5ce-153">我是否可以從任何 Redis 伺服器匯入資料？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="1c5ce-154">我可以匯入哪些 RDB 版本？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="1c5ce-155">在匯入/匯出作業期間，是否可以使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="1c5ce-156">我可以使用匯入/匯出搭配 Redis 叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="1c5ce-157">匯入/匯出如何對自訂資料庫設定運作？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="1c5ce-158">匯入/匯出和 Redis 永續性有何不同？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="1c5ce-159">我可以使用 PowerShell、CLI 或其他管理用戶端自動化匯入/匯出嗎？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="1c5ce-160">我在匯入/匯出作業期間收到逾時錯誤。這代表什麼意思？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="1c5ce-161">匯出我資料 tooAzure Blob 儲存體時，我會收到錯誤。發生什麼情形？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-161">I got an error when exporting my data tooAzure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="1c5ce-162">哪些定價層可以使用匯入/匯出？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="1c5ce-163">只有在 hello premium 定價層中使用匯入/匯出。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-163">Import/Export is available only in hello premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="1c5ce-164">我是否可以從任何 Redis 伺服器匯入資料？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="1c5ce-165">是，除了 tooimporting Azure Redis 快取執行個體從匯出的資料，您可以匯入 RDB 檔案從任何執行中的任何雲端或環境，例如 Linux、 Windows 或雲端提供者，例如 Amazon Web Services 的 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-165">Yes, in addition tooimporting data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="1c5ce-166">toodo 此上傳 hello RDB 檔案從預期的 hello Redis 伺服器分頁或區塊 blob 中的 Azure 儲存體帳戶，然後匯入它至 premium Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-166">toodo this, upload hello RDB file from hello desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="1c5ce-167">比方說，您可能想要從您的實際執行快取的 tooexport hello 資料，並匯入做為預備環境的一部分用於測試或移轉快取。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-167">For example, you may want tooexport hello data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c5ce-168">toosuccessfully 匯入資料時使用分頁 blob、 hello 分頁 blob 大小必須對齊 512 位元組界限上，從非 Azure Redis 快取的 Redis 伺服器匯出。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-168">toosuccessfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, hello page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="1c5ce-169">如範例程式碼 tooperform 任何所需的位元組填補，請參閱[範例頁面部落格上傳](https://github.com/JimRoberts-MS/SamplePageBlobUpload)。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-169">For sample code tooperform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="1c5ce-170">我可以匯入哪些 RDB 版本？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-170">What RDB versions can I import?</span></span>

<span data-ttu-id="1c5ce-171">Azure Redis 快取最多可支援到 RDB 第 7 版的 RDB 匯入。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="1c5ce-172">在匯入/匯出作業期間，是否可以使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="1c5ce-173">**匯出**-快取保持可用狀態，並可以匯出作業期間繼續 toouse 您的快取。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-173">**Export** - Caches remain available and you can continue toouse your cache during an export operation.</span></span>
* <span data-ttu-id="1c5ce-174">**匯入**-匯入作業啟動時，會變成無法使用，且會變成可供使用，hello 匯入作業完成時的快取。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when hello import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="1c5ce-175">我可以使用匯入/匯出搭配 Redis 叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="1c5ce-176">可以，您可以在叢集快取和非叢集快取之間匯入/匯出。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="1c5ce-177">由於 Redis 叢集[僅支援資料庫 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)，因此不會匯入資料庫中 0 以外的任何資料。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="1c5ce-178">匯入叢集的快取資料時，hello 金鑰會重新分配 hello 叢集的 hello 分區之間。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-178">When clustered cache data is imported, hello keys are redistributed among hello shards of hello cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="1c5ce-179">匯入/匯出如何對自訂資料庫設定運作？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="1c5ce-180">某些定價層會具有不同[資料庫限制](cache-configure.md#databases)，因此有一些考量當匯入，如果您設定自訂值的 hello`databases`快取建立期間設定。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for hello `databases` setting during cache creation.</span></span>

* <span data-ttu-id="1c5ce-181">匯入 tooa 定價層與較低時`databases`與從中匯出的 hello 層的限制：</span><span class="sxs-lookup"><span data-stu-id="1c5ce-181">When importing tooa pricing tier with a lower `databases` limit than hello tier from which you exported:</span></span>
  * <span data-ttu-id="1c5ce-182">如果您使用 hello 預設數目`databases`、，也就是 16 個所有定價層不會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-182">If you are using hello default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="1c5ce-183">如果您使用自訂的數字的`databases`，便在 2008 年 hello 的限制範圍內的 hello 層的 toowhich 您要匯入，會遺失任何資料。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-183">If you are using a custom number of `databases` that falls within hello limits for hello tier toowhich you are importing, no data is lost.</span></span>
  * <span data-ttu-id="1c5ce-184">如果您匯出的資料包含超過 hello hello 新層的資料庫中的資料，這些較高的資料庫中的 hello 資料不會匯入。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-184">If your exported data contained data in a database that exceeds hello limits of hello new tier, hello data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="1c5ce-185">匯入/匯出和 Redis 永續性有何不同？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="1c5ce-186">Azure Redis 快取持續性可讓您 toopersist Redis tooAzure 儲存體中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-186">Azure Redis Cache persistence allows you toopersist data stored in Redis tooAzure Storage.</span></span> <span data-ttu-id="1c5ce-187">設定持續性時，Azure Redis 快取會保存在根據可設定的備份頻率 Redis 二進位格式 toodisk hello Redis 快取的快照集。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-187">When persistence is configured, Azure Redis Cache persists a snapshot of hello Redis cache in a Redis binary format toodisk based on a configurable backup frequency.</span></span> <span data-ttu-id="1c5ce-188">發生重大事件，會停用 hello 主要和複本快取，會自動使用 hello 最新的快照集還原 hello 快取資料。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-188">If a catastrophic event occurs that disables both hello primary and replica cache, hello cache data is restored automatically using hello most recent snapshot.</span></span> <span data-ttu-id="1c5ce-189">如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取的資料持續性](cache-how-to-premium-persistence.md)。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-189">For more information, see [How tooconfigure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="1c5ce-190">匯入 / 匯出可讓您將 toobring 資料或是從 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-190">Import/ Export allows you toobring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="1c5ce-191">它無法設定備份和還原使用 Redis 永續性。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="1c5ce-192">我可以使用 PowerShell、CLI 或其他管理用戶端自動化匯入/匯出嗎？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="1c5ce-193">是，適用於 PowerShell 指示看到[tooimport Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache)和[tooexport Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache)。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-193">Yes, for PowerShell instructions see [tooimport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [tooexport a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="1c5ce-194">我在匯入/匯出作業期間收到逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="1c5ce-195">這代表什麼意思？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-195">What does it mean?</span></span>
<span data-ttu-id="1c5ce-196">如果您保留在 hello 上**匯入資料**或**匯出資料**刀鋒視窗中的時間超過 15 分鐘初始化 hello 作業之前，您收到錯誤訊息與下列範例錯誤的訊息類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="1c5ce-196">If you remain on hello **Import data** or **Export data** blade for longer than 15 minutes before initiating hello operation, you receive an error with an error message similar toohello following example:</span></span>

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

<span data-ttu-id="1c5ce-197">tooresolve，起始 hello 匯入或匯出作業之前經過 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-197">tooresolve this, initiate hello import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a><span data-ttu-id="1c5ce-198">匯出我資料 tooAzure Blob 儲存體時，我會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-198">I got an error when exporting my data tooAzure Blob Storage.</span></span> <span data-ttu-id="1c5ce-199">發生什麼情形？</span><span class="sxs-lookup"><span data-stu-id="1c5ce-199">What happened?</span></span>
<span data-ttu-id="1c5ce-200">匯出只能使用儲存為分頁 blob 的 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="1c5ce-201">目前不支援其他的 Blob 類型，包括經常存取及不常存取層的 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="1c5ce-202">如需詳細資訊，請參閱 [Blob 儲存體帳戶](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c5ce-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c5ce-203">Next steps</span></span>
<span data-ttu-id="1c5ce-204">了解如何更進階的 toouse 快取功能。</span><span class="sxs-lookup"><span data-stu-id="1c5ce-204">Learn how toouse more premium cache features.</span></span>

* [<span data-ttu-id="1c5ce-205">簡介 toohello Azure Redis 快取進階層</span><span class="sxs-lookup"><span data-stu-id="1c5ce-205">Introduction toohello Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

<!-- IMAGES -->
[cache-settings-import-export-menu]: ./media/cache-how-to-import-export-data/cache-settings-import-export-menu.png
[cache-export-data-choose-account]: ./media/cache-how-to-import-export-data/cache-export-data-choose-account.png
[cache-export-data-choose-storage-container]: ./media/cache-how-to-import-export-data/cache-export-data-choose-storage-container.png
[cache-export-data-container]: ./media/cache-how-to-import-export-data/cache-export-data-container.png
[cache-export-data-export-complete]: ./media/cache-how-to-import-export-data/cache-export-data-export-complete.png
[cache-export-data]: ./media/cache-how-to-import-export-data/cache-export-data.png
[cache-import-data]: ./media/cache-how-to-import-export-data/cache-import-data.png
[cache-import-choose-storage-account]: ./media/cache-how-to-import-export-data/cache-import-choose-storage-account.png
[cache-import-choose-container]: ./media/cache-how-to-import-export-data/cache-import-choose-container.png
[cache-import-choose-blobs]: ./media/cache-how-to-import-export-data/cache-import-choose-blobs.png
[cache-import-blobs]: ./media/cache-how-to-import-export-data/cache-import-blobs.png
[cache-import-data-import-complete]: ./media/cache-how-to-import-export-data/cache-import-data-import-complete.png
