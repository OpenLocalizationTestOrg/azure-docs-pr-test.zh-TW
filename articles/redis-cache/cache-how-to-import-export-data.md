---
title: "在 Azure Redis 快取中匯入與匯出資料 | Microsoft Docs"
description: "了解如何使用進階 Azure Redis 快取執行個體將資料匯入至 blob 儲存體並從其中匯出資料"
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
ms.openlocfilehash: 5e6d731f0a1cecc1a191c74a45e37a9b94fd98ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="import-and-export-data-in-azure-redis-cache"></a><span data-ttu-id="941cd-103">在 Azure Redis 快取中匯入與匯出資料</span><span class="sxs-lookup"><span data-stu-id="941cd-103">Import and Export data in Azure Redis Cache</span></span>
<span data-ttu-id="941cd-104">匯入/匯出是 Azure Redis 快取資料管理作業，可讓您將資料匯入 Azure Redis 快取或將資料從 Azure Redis 快取匯出，方法是從進階快取將 Redis 快取資料庫 (RDB) 快照匯入和匯出至 Azure 儲存體帳戶中的 blob。</span><span class="sxs-lookup"><span data-stu-id="941cd-104">Import/Export is an Azure Redis Cache data management operation, which allows you to import data into Azure Redis Cache or export data from Azure Redis Cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a blob in an Azure Storage Account.</span></span> 

- <span data-ttu-id="941cd-105">**匯出** - 您可以將您的 Azure Redis 快取 RDB 快照集匯出至分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="941cd-105">**Export** - you can export your Azure Redis Cache RDB snapshots to a Page Blob.</span></span>
- <span data-ttu-id="941cd-106">**匯入** - 您可以從分頁 Blob 或區塊 Blob 匯入您的 Redis 快取 RDB 快照集。</span><span class="sxs-lookup"><span data-stu-id="941cd-106">**Import** - you can import your Redis Cache RDB snapshots from either a Page Blob or a Block Blob.</span></span>

<span data-ttu-id="941cd-107">匯入/匯出可讓您在不同的 Azure Redis 快取執行個體之間移轉，或在使用前將資料填入快取。</span><span class="sxs-lookup"><span data-stu-id="941cd-107">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="941cd-108">本文提供使用 Azure Redis 快取匯入和匯出資料的指南，並提供常見問題的解答。</span><span class="sxs-lookup"><span data-stu-id="941cd-108">This article provides a guide for importing and exporting data with Azure Redis Cache and provides the answers to commonly asked questions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="941cd-109">匯入/匯出僅供預覽，只供 [進階層](cache-premium-tier-intro.md) 快取使用。</span><span class="sxs-lookup"><span data-stu-id="941cd-109">Import/Export is in preview and is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span>
>
>

## <a name="import"></a><span data-ttu-id="941cd-110">Import</span><span class="sxs-lookup"><span data-stu-id="941cd-110">Import</span></span>
<span data-ttu-id="941cd-111">匯入可以用來從任何雲端或環境中執行的 Redis 伺服器 (包含在 Linux、Windows 上執行的 Redis，或任何雲端提供者，例如 Amazon Web Services 等) 引入 Redis 相容 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="941cd-111">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="941cd-112">匯入資料是使用預先填入資料建立快取的輕鬆方式。</span><span class="sxs-lookup"><span data-stu-id="941cd-112">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="941cd-113">在匯入程序期間，Azure Redis 快取會從 Azure 儲存體將 RDB 檔案載入記憶體，然後將金鑰插入快取。</span><span class="sxs-lookup"><span data-stu-id="941cd-113">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory and then inserts the keys into the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="941cd-114">開始匯入作業之前，請確定您的 Redis 資料庫 (RDB) 檔案已上傳到 Azure 儲存體中的分頁或區塊 blob，位於和 Azure Redis 快取執行個體相同的區域和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="941cd-114">Before beginning the import operation, ensure that your Redis Database (RDB) file or files are uploaded into page or block blobs in Azure storage, in the same region and subscription as your Azure Redis Cache instance.</span></span> <span data-ttu-id="941cd-115">如需詳細資訊，請參閱 [開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="941cd-115">For more information, see [Get started with Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="941cd-116">如果您使用 [Azure Redis 快取匯出](#export) 功能匯出 RDB 檔案，表示 RDB 檔案已儲存在分頁 blob，並且可供匯入。</span><span class="sxs-lookup"><span data-stu-id="941cd-116">If you exported your RDB file using the [Azure Redis Cache Export](#export) feature, your RDB file is already stored in a page blob and is ready for importing.</span></span>
>
>

1. <span data-ttu-id="941cd-117">若要匯入一或多個匯出的快取 Blob，請[瀏覽至 Azure 入口網站中的快取](cache-configure.md#configure-redis-cache-settings)，然後從 [資源功能表] 按一下 [匯入資料]。</span><span class="sxs-lookup"><span data-stu-id="941cd-117">To import one or more exported cache blobs, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Import data** from the **Resource menu**.</span></span>

    ![匯入資料][cache-import-data]
2. <span data-ttu-id="941cd-119">按一下 [選擇 Blob]  ，然後選取包含要匯入之資料的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="941cd-119">Click **Choose Blob(s)** and select the storage account that contains the data to import.</span></span>

    ![Choose storage account][cache-import-choose-storage-account]
3. <span data-ttu-id="941cd-121">按一下包含要匯入之資料的容器。</span><span class="sxs-lookup"><span data-stu-id="941cd-121">Click the container that contains the data to import.</span></span>

    ![選擇容器][cache-import-choose-container]
4. <span data-ttu-id="941cd-123">按一下 blob 名稱左側的區域以選取一或多個 blob，即可加以匯入，然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="941cd-123">Select one or more blobs to import by clicking the area to the left of the blob name, and then click **Select**.</span></span>

    ![選擇 blob][cache-import-choose-blobs]
5. <span data-ttu-id="941cd-125">按一下 [匯入]  開始匯入程序。</span><span class="sxs-lookup"><span data-stu-id="941cd-125">Click **Import** to begin the import process.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="941cd-126">快取用戶端無法在匯入程序期間存取快取，而且在快取中的所有現有資料都會刪除。</span><span class="sxs-lookup"><span data-stu-id="941cd-126">The cache is not accessible by cache clients during the import process, and any existing data in the cache is deleted.</span></span>
   >
   >

    ![Import][cache-import-blobs]

    <span data-ttu-id="941cd-128">您可以遵循 Azure 入口網站的通知，或檢視 [稽核記錄檔](../azure-resource-manager/resource-group-audit.md)中的事件來監視匯入作業的進度。</span><span class="sxs-lookup"><span data-stu-id="941cd-128">You can monitor the progress of the import operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![匯入進度][cache-import-data-import-complete]

## <a name="export"></a><span data-ttu-id="941cd-130">匯出</span><span class="sxs-lookup"><span data-stu-id="941cd-130">Export</span></span>
<span data-ttu-id="941cd-131">匯出可讓您將儲存在 Azure Redis 快取中的資料匯出至 Redis 相容 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="941cd-131">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB file(s).</span></span> <span data-ttu-id="941cd-132">您可以使用這項功能，將資料從一個 Azure Redis 快取執行個體移到另一個或其他 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="941cd-132">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="941cd-133">在匯出程序期間，會在裝載 Azure Redis 快取伺服器執行個體的 VM 上建立站存檔案，並將檔案上傳至指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="941cd-133">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="941cd-134">當匯出作業完成時的狀態為成功或失敗時，都會刪除暫存檔案。</span><span class="sxs-lookup"><span data-stu-id="941cd-134">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

1. <span data-ttu-id="941cd-135">若要將目前的快取內容匯出至儲存體，請[瀏覽至 Azure 入口網站中的快取](cache-configure.md#configure-redis-cache-settings)，然後從 [資源功能表] 按一下 [匯出資料]。</span><span class="sxs-lookup"><span data-stu-id="941cd-135">To export the current contents of the cache to storage, [browse to your cache](cache-configure.md#configure-redis-cache-settings) in the Azure portal and click **Export data** from the **Resource menu**.</span></span>

    ![選擇儲存體容器][cache-export-data-choose-storage-container]
2. <span data-ttu-id="941cd-137">按一下 [選擇儲存體容器]  ，然後選取所需的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="941cd-137">Click **Choose Storage Container** and select the desired storage account.</span></span> <span data-ttu-id="941cd-138">儲存體帳戶必須與您的快取位於相同的訂用帳戶和區域中。</span><span class="sxs-lookup"><span data-stu-id="941cd-138">The storage account must be in the same subscription and region as your cache.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="941cd-139">匯出使用分頁 Blob，傳統和 Resource Manager 儲存體帳戶支援這些 Blob，但 [Blob 儲存體帳戶](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)目前不支援。</span><span class="sxs-lookup"><span data-stu-id="941cd-139">Export works with page blobs, which are supported by both classic and Resource Manager storage accounts, but are not supported by [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts) at this time.</span></span>
   >
   >

    ![儲存體帳戶][cache-export-data-choose-account]
3. <span data-ttu-id="941cd-141">選擇所需的 blob 容器，然後按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="941cd-141">Choose the desired blob container and click **Select**.</span></span> <span data-ttu-id="941cd-142">若要使用新的容器，請按一下 [新增容器]  先加以新增，然後從清單中選取它。</span><span class="sxs-lookup"><span data-stu-id="941cd-142">To use new a container, click **Add Container** to add it first and then select it from the list.</span></span>

    ![選擇儲存體容器][cache-export-data-container]
4. <span data-ttu-id="941cd-144">輸入 [Blob 名稱前置詞]，然後按一下 [匯出] 以啟動匯出程序。</span><span class="sxs-lookup"><span data-stu-id="941cd-144">Type a **Blob name prefix** and click **Export** to start the export process.</span></span> <span data-ttu-id="941cd-145">Blob 名稱前置詞可用來做為此匯出作業所產生之檔案名稱的前置詞。</span><span class="sxs-lookup"><span data-stu-id="941cd-145">The blob name prefix is used to prefix the names of files generated by this export operation.</span></span>

    ![匯出][cache-export-data]

    <span data-ttu-id="941cd-147">您可以遵循 Azure 入口網站的通知，或檢視[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)中的事件來監視匯出作業的進度。</span><span class="sxs-lookup"><span data-stu-id="941cd-147">You can monitor the progress of the export operation by following the notifications from the Azure portal, or by viewing the events in the [audit log](../azure-resource-manager/resource-group-audit.md).</span></span>

    ![匯出資料完成][cache-export-data-export-complete]

    <span data-ttu-id="941cd-149">在匯出程序期間快取隨時可供使用。</span><span class="sxs-lookup"><span data-stu-id="941cd-149">Caches remain available for use during the export process.</span></span>

## <a name="importexport-faq"></a><span data-ttu-id="941cd-150">匯入/匯出常見問題集</span><span class="sxs-lookup"><span data-stu-id="941cd-150">Import/Export FAQ</span></span>
<span data-ttu-id="941cd-151">本節包含匯入/匯出功能的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="941cd-151">This section contains frequently asked questions about the Import/Export feature.</span></span>

* [<span data-ttu-id="941cd-152">哪些定價層可以使用匯入/匯出？</span><span class="sxs-lookup"><span data-stu-id="941cd-152">What pricing tiers can use Import/Export?</span></span>](#what-pricing-tiers-can-use-importexport)
* [<span data-ttu-id="941cd-153">我是否可以從任何 Redis 伺服器匯入資料？</span><span class="sxs-lookup"><span data-stu-id="941cd-153">Can I import data from any Redis server?</span></span>](#can-i-import-data-from-any-redis-server)
* [<span data-ttu-id="941cd-154">我可以匯入哪些 RDB 版本？</span><span class="sxs-lookup"><span data-stu-id="941cd-154">What RDB versions can I import?</span></span>](#what-rdb-versions-can-i-import)
* [<span data-ttu-id="941cd-155">在匯入/匯出作業期間，是否可以使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="941cd-155">Is my cache available during an Import/Export operation?</span></span>](#is-my-cache-available-during-an-importexport-operation)
* [<span data-ttu-id="941cd-156">我可以使用匯入/匯出搭配 Redis 叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="941cd-156">Can I use Import/Export with Redis cluster?</span></span>](#can-i-use-importexport-with-redis-cluster)
* [<span data-ttu-id="941cd-157">匯入/匯出如何對自訂資料庫設定運作？</span><span class="sxs-lookup"><span data-stu-id="941cd-157">How does Import/Export work with a custom databases setting?</span></span>](#how-does-importexport-work-with-a-custom-databases-setting)
* [<span data-ttu-id="941cd-158">匯入/匯出和 Redis 永續性有何不同？</span><span class="sxs-lookup"><span data-stu-id="941cd-158">How is Import/Export different from Redis persistence?</span></span>](#how-is-importexport-different-from-redis-persistence)
* [<span data-ttu-id="941cd-159">我可以使用 PowerShell、CLI 或其他管理用戶端自動化匯入/匯出嗎？</span><span class="sxs-lookup"><span data-stu-id="941cd-159">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [<span data-ttu-id="941cd-160">我在匯入/匯出作業期間收到逾時錯誤。這代表什麼意思？</span><span class="sxs-lookup"><span data-stu-id="941cd-160">I received a timeout error during my Import/Export operation. What does it mean?</span></span>](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [<span data-ttu-id="941cd-161">我將資料匯出至 Azure Blob 儲存體時收到錯誤。發生什麼情形？</span><span class="sxs-lookup"><span data-stu-id="941cd-161">I got an error when exporting my data to Azure Blob Storage. What happened?</span></span>](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a><span data-ttu-id="941cd-162">哪些定價層可以使用匯入/匯出？</span><span class="sxs-lookup"><span data-stu-id="941cd-162">What pricing tiers can use Import/Export?</span></span>
<span data-ttu-id="941cd-163">匯入/匯出僅適用於進階定價層。</span><span class="sxs-lookup"><span data-stu-id="941cd-163">Import/Export is available only in the premium pricing tier.</span></span>

### <a name="can-i-import-data-from-any-redis-server"></a><span data-ttu-id="941cd-164">我是否可以從任何 Redis 伺服器匯入資料？</span><span class="sxs-lookup"><span data-stu-id="941cd-164">Can I import data from any Redis server?</span></span>
<span data-ttu-id="941cd-165">是，除了匯入從 Azure Redis 快取執行個體匯出的資料之外，您還可以從執行於雲端或環境 (例如 Linux、Windows 或雲端提供者，例如 Amazon Web Services) 中的任何 Redis 伺服器匯入 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="941cd-165">Yes, in addition to importing data exported from Azure Redis Cache instances, you can import RDB files from any Redis server running in any cloud or environment, such as Linux, Windows, or cloud providers such as Amazon Web Services.</span></span> <span data-ttu-id="941cd-166">若要這樣做，請將 RDB 檔案從所需的 Redis 伺服器上傳至 Azure 儲存體帳戶中的分頁或區塊 blob，然後將它匯入到您的進階 Azure Redis 快取執行個體。</span><span class="sxs-lookup"><span data-stu-id="941cd-166">To do this, upload the RDB file from the desired Redis server into a page or block blob in an Azure Storage Account, and then import it into your premium Azure Redis Cache instance.</span></span> <span data-ttu-id="941cd-167">例如，建議您從生產快取匯出資料，並將其匯入至快取，用於測試活移轉做為預備環境的一部分。</span><span class="sxs-lookup"><span data-stu-id="941cd-167">For example, you may want to export the data from your production cache and import it into a cache used as part of a staging environment for testing or migration.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="941cd-168">若要在使用分頁 blob 時成功匯入從非 Azure Redis 快取的 Redis 伺服器匯出的資料，分頁 blob 大小必須在 512 個位元組的界限上對齊。</span><span class="sxs-lookup"><span data-stu-id="941cd-168">To successfully import data exported from Redis servers other than Azure Redis Cache when using a page blob, the page blob size must be aligned on a 512 byte boundary.</span></span> <span data-ttu-id="941cd-169">如需執行任何所需的位元組填補的範例程式碼，請參閱[範例分頁 blob 上傳 (英文)](https://github.com/JimRoberts-MS/SamplePageBlobUpload)。</span><span class="sxs-lookup"><span data-stu-id="941cd-169">For sample code to perform any required byte padding, see [Sample page blog upload](https://github.com/JimRoberts-MS/SamplePageBlobUpload).</span></span>
> 
> 

### <a name="what-rdb-versions-can-i-import"></a><span data-ttu-id="941cd-170">我可以匯入哪些 RDB 版本？</span><span class="sxs-lookup"><span data-stu-id="941cd-170">What RDB versions can I import?</span></span>

<span data-ttu-id="941cd-171">Azure Redis 快取最多可支援到 RDB 第 7 版的 RDB 匯入。</span><span class="sxs-lookup"><span data-stu-id="941cd-171">Azure Redis Cache supports RDB import up through RDB version 7.</span></span>

### <a name="is-my-cache-available-during-an-importexport-operation"></a><span data-ttu-id="941cd-172">在匯入/匯出作業期間，是否可以使用我的快取？</span><span class="sxs-lookup"><span data-stu-id="941cd-172">Is my cache available during an Import/Export operation?</span></span>
* <span data-ttu-id="941cd-173">**匯出** - 快取持續可供使用，而且您可以繼續在匯出作業期間使用快取。</span><span class="sxs-lookup"><span data-stu-id="941cd-173">**Export** - Caches remain available and you can continue to use your cache during an export operation.</span></span>
* <span data-ttu-id="941cd-174">**匯入** - 匯入作業啟動時會無法使用快取，當匯入作業完成時，快取即可供使用。</span><span class="sxs-lookup"><span data-stu-id="941cd-174">**Import** - Caches become unavailable when an import operation starts, and become available for use when the import operation completes.</span></span>

### <a name="can-i-use-importexport-with-redis-cluster"></a><span data-ttu-id="941cd-175">我可以使用匯入/匯出搭配 Redis 叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="941cd-175">Can I use Import/Export with Redis cluster?</span></span>
<span data-ttu-id="941cd-176">可以，您可以在叢集快取和非叢集快取之間匯入/匯出。</span><span class="sxs-lookup"><span data-stu-id="941cd-176">Yes, and you can import/export between a clustered cache and a non-clustered cache.</span></span> <span data-ttu-id="941cd-177">由於 Redis 叢集[僅支援資料庫 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)，因此不會匯入資料庫中 0 以外的任何資料。</span><span class="sxs-lookup"><span data-stu-id="941cd-177">Since Redis cluster [only supports database 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering), any data in databases other than 0 isn't imported.</span></span> <span data-ttu-id="941cd-178">匯入叢集快取資料時，金鑰會在叢集的分區之間重新分配。</span><span class="sxs-lookup"><span data-stu-id="941cd-178">When clustered cache data is imported, the keys are redistributed among the shards of the cluster.</span></span>

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a><span data-ttu-id="941cd-179">匯入/匯出如何對自訂資料庫設定運作？</span><span class="sxs-lookup"><span data-stu-id="941cd-179">How does Import/Export work with a custom databases setting?</span></span>
<span data-ttu-id="941cd-180">某些定價層具有不同的[資料庫限制](cache-configure.md#databases)，因此，在匯入時，如果您在快取建立期間為 `databases` 設定設定了自訂值，則有一些考量。</span><span class="sxs-lookup"><span data-stu-id="941cd-180">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when importing if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="941cd-181">匯入到與您從中匯出的階層具有較低 `databases` 限制的定價層時：</span><span class="sxs-lookup"><span data-stu-id="941cd-181">When importing to a pricing tier with a lower `databases` limit than the tier from which you exported:</span></span>
  * <span data-ttu-id="941cd-182">如果您使用預設數字 `databases`，即所有定價層為 16，則不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="941cd-182">If you are using the default number of `databases`, which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="941cd-183">如果您要使用的自訂數字 `databases` ，落在您要匯入之階層限制範圍內，則不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="941cd-183">If you are using a custom number of `databases` that falls within the limits for the tier to which you are importing, no data is lost.</span></span>
  * <span data-ttu-id="941cd-184">如果您的匯出資料包含位於超出新階層限制之資料庫中的資料，則不會匯入來自這些較高階層資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="941cd-184">If your exported data contained data in a database that exceeds the limits of the new tier, the data from those higher databases is not imported.</span></span>

### <a name="how-is-importexport-different-from-redis-persistence"></a><span data-ttu-id="941cd-185">匯入/匯出和 Redis 永續性有何不同？</span><span class="sxs-lookup"><span data-stu-id="941cd-185">How is Import/Export different from Redis persistence?</span></span>
<span data-ttu-id="941cd-186">Azure Redis 快取永續性讓您將儲存在 Redis 快取中的資料存留至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="941cd-186">Azure Redis Cache persistence allows you to persist data stored in Redis to Azure Storage.</span></span> <span data-ttu-id="941cd-187">設定永續性後，Azure Redis 快取會依據可設定的備份頻率，在磁碟中保存一份 Redis 二進位格式的 Redis 快取快照。</span><span class="sxs-lookup"><span data-stu-id="941cd-187">When persistence is configured, Azure Redis Cache persists a snapshot of the Redis cache in a Redis binary format to disk based on a configurable backup frequency.</span></span> <span data-ttu-id="941cd-188">如果發生同時停用主要和複本快取的災難性事件，即可使用最新的快照自動還原快取資料。</span><span class="sxs-lookup"><span data-stu-id="941cd-188">If a catastrophic event occurs that disables both the primary and replica cache, the cache data is restored automatically using the most recent snapshot.</span></span> <span data-ttu-id="941cd-189">如需詳細資訊，請參閱 [如何設定進階 Azure Redis 快取的資料永續性](cache-how-to-premium-persistence.md)。</span><span class="sxs-lookup"><span data-stu-id="941cd-189">For more information, see [How to configure data persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>

<span data-ttu-id="941cd-190">匯入/匯出可讓您將資料引入 Azure Redis 快取或從其中匯出。</span><span class="sxs-lookup"><span data-stu-id="941cd-190">Import/ Export allows you to bring data into or export from Azure Redis Cache.</span></span> <span data-ttu-id="941cd-191">它無法設定備份和還原使用 Redis 永續性。</span><span class="sxs-lookup"><span data-stu-id="941cd-191">It does not configure backup and restore using Redis persistence.</span></span>

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a><span data-ttu-id="941cd-192">我可以使用 PowerShell、CLI 或其他管理用戶端自動化匯入/匯出嗎？</span><span class="sxs-lookup"><span data-stu-id="941cd-192">Can I automate Import/Export using PowerShell, CLI, or other management clients?</span></span>
<span data-ttu-id="941cd-193">可以。如需 PowerShell 指示，請參閱[匯入 Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache)和[匯出 Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache)。</span><span class="sxs-lookup"><span data-stu-id="941cd-193">Yes, for PowerShell instructions see [To import a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache) and [To export a Redis cache](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache).</span></span>

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a><span data-ttu-id="941cd-194">我在匯入/匯出作業期間收到逾時錯誤。</span><span class="sxs-lookup"><span data-stu-id="941cd-194">I received a timeout error during my Import/Export operation.</span></span> <span data-ttu-id="941cd-195">這代表什麼意思？</span><span class="sxs-lookup"><span data-stu-id="941cd-195">What does it mean?</span></span>
<span data-ttu-id="941cd-196">如果您在初始化作業之前停留在 [匯入資料] 或 [匯出資料] 刀鋒視窗超過 15 分鐘，您會收到類似下列範例錯誤訊息的錯誤：</span><span class="sxs-lookup"><span data-stu-id="941cd-196">If you remain on the **Import data** or **Export data** blade for longer than 15 minutes before initiating the operation, you receive an error with an error message similar to the following example:</span></span>

    The request to import data into cache 'contoso55' failed with status 'error' and error 'One of the SAS URIs provided could not be used for the following reason: The SAS token end time (se) must be at least 1 hour from now and the start time (st), if given, must be at least 15 minutes in the past.

<span data-ttu-id="941cd-197">若要解決此問題，請在經過 15 分鐘之前起始匯入或匯出作業。</span><span class="sxs-lookup"><span data-stu-id="941cd-197">To resolve this, initiate the import or export operation before 15 minutes has elapsed.</span></span>

### <a name="i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened"></a><span data-ttu-id="941cd-198">我將資料匯出至 Azure Blob 儲存體時收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="941cd-198">I got an error when exporting my data to Azure Blob Storage.</span></span> <span data-ttu-id="941cd-199">發生什麼情形？</span><span class="sxs-lookup"><span data-stu-id="941cd-199">What happened?</span></span>
<span data-ttu-id="941cd-200">匯出只能使用儲存為分頁 blob 的 RDB 檔案。</span><span class="sxs-lookup"><span data-stu-id="941cd-200">Export works only with RDB files stored as page blobs.</span></span> <span data-ttu-id="941cd-201">目前不支援其他的 Blob 類型，包括經常存取及不常存取層的 Blob 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="941cd-201">Other blob types are not currently supported, including blob storage accounts with hot and cool tiers.</span></span> <span data-ttu-id="941cd-202">如需詳細資訊，請參閱 [Blob 儲存體帳戶](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)。</span><span class="sxs-lookup"><span data-stu-id="941cd-202">For more information, see [Blob storage accounts](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts).</span></span>

## <a name="next-steps"></a><span data-ttu-id="941cd-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="941cd-203">Next steps</span></span>
<span data-ttu-id="941cd-204">了解如何使用更多進階快取功能。</span><span class="sxs-lookup"><span data-stu-id="941cd-204">Learn how to use more premium cache features.</span></span>

* [<span data-ttu-id="941cd-205">Azure Redis Cache 高階層簡介</span><span class="sxs-lookup"><span data-stu-id="941cd-205">Introduction to the Azure Redis Cache Premium tier</span></span>](cache-premium-tier-intro.md)    

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
