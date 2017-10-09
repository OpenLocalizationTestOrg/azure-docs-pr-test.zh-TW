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
# <a name="import-and-export-data-in-azure-redis-cache"></a>在 Azure Redis 快取中匯入與匯出資料
匯入/匯出為 Azure Redis 快取資料管理作業，可讓您 tooimport 資料至 Azure Redis 快取或匯出資料，從 Azure Redis 快取所匯入和匯出從 premium 快取 tooa blob 在 Azure Redis 快取資料庫 (RDB) 快照集儲存體帳戶。 

- **匯出**-您可以匯出您的 Azure Redis 快取 RDB 快照 tooa 分頁 Blob。
- **匯入** - 您可以從分頁 Blob 或區塊 Blob 匯入您的 Redis 快取 RDB 快照集。

匯入/匯出可讓您 toomigrate 不同的 Azure Redis 快取執行個體之間，或填入 hello 快取，以使用之前的資料。

本文提供的匯入和匯出與 Azure Redis 快取資料的指南，並提供 hello 答案 toocommonly 常見問題。

> [!IMPORTANT]
> 匯入/匯出僅供預覽，只供 [進階層](cache-premium-tier-intro.md) 快取使用。
>
>

## <a name="import"></a>Import
匯入可為使用的 toobring Redis 相容 RDB 檔案從任何執行中的任何雲端或環境，包括 Linux、 Windows 或任何雲端提供者，例如 Amazon Web Services 等項目上執行的 Redis 的 Redis 伺服器。 匯入資料是簡單的方式 toocreate 預先填入資料的快取。 在 hello 匯入過程中，Azure Redis 快取 Azure 儲存體中的 hello RDB 檔案載入記憶體，然後插入 hello 快取中的 hello 索引鍵。

> [!NOTE]
> 開始之前 hello 匯入作業，請確定您的 Redis 資料庫 (RDB) 檔案上傳到頁面上，或區塊 blob 在 Azure 儲存體，在 hello 相同地區和訂用帳戶與您的 Azure Redis 快取執行個體。 如需詳細資訊，請參閱 [開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。 如果您匯出 RDB 檔案使用 hello [Azure Redis 快取匯出](#export)功能 RDB 檔案已儲存在分頁 blob 的和可供匯入。
>
>

1. 一或多個 tooimport 匯出快取 blob[瀏覽 tooyour 快取](cache-configure.md#configure-redis-cache-settings)在 hello Azure 入口網站，然後按一下**匯入資料**hello 從**資源功能表**。

    ![匯入資料][cache-import-data]
2. 按一下**選擇 blob**並選取包含 hello 資料 tooimport hello 儲存體帳戶。

    ![Choose storage account][cache-import-choose-storage-account]
3. 按一下包含 hello 資料 tooimport hello 容器。

    ![選擇容器][cache-import-choose-container]
4. 選取一或多個 blob tooimport 按一下 hello 區域 toohello hello blob 名稱左邊，然後按一下**選取**。

    ![選擇 blob][cache-import-choose-blobs]
5. 按一下**匯入**toobegin hello 匯入程序。

   > [!IMPORTANT]
   > hello 快取的快取用戶端可存取 hello 匯入程序，並不會刪除任何現有資料 hello 快取中。
   >
   >

    ![Import][cache-import-blobs]

    您可以在 hello Azure 入口網站的下列 hello 通知或藉由在 hello 檢視 hello 事件監視 hello hello 匯入作業的進度[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)。

    ![匯入進度][cache-import-data-import-complete]

## <a name="export"></a>匯出
匯出可讓您 tooexport hello 資料儲存在 Azure Redis 快取 tooRedis 相容 RDB 檔案中。 您可以使用此功能 toomove 資料從一個 Azure Redis 快取執行個體 tooanother 或 tooanother Redis 伺服器。 在 hello 匯出程序，hello VM 的主機 hello Azure Redis 快取伺服器執行個體，而且 hello 檔案上傳的 toohello 指定儲存體帳戶上建立暫存檔。 Hello 匯出作業完成時為其中一個狀態為成功或失敗，則會刪除 hello 暫存檔案。

1. tooexport hello 目前內容的 hello 快取 toostorage，[瀏覽 tooyour 快取](cache-configure.md#configure-redis-cache-settings)在 hello Azure 入口網站，然後按一下**匯出資料**從 hello**資源功能表**。

    ![選擇儲存體容器][cache-export-data-choose-storage-container]
2. 按一下**選擇儲存體容器**及選取所需的 hello 儲存體帳戶。 hello hello 儲存體帳戶必須是相同的訂用帳戶和與您的快取的區域。

   > [!IMPORTANT]
   > 匯出使用分頁 Blob，傳統和 Resource Manager 儲存體帳戶支援這些 Blob，但 [Blob 儲存體帳戶](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)目前不支援。
   >
   >

    ![儲存體帳戶][cache-export-data-choose-account]
3. 選擇 hello 預期 blob 容器，然後按一下**選取**。 toouse 新的容器，按一下**Add Container** tooadd 它第一次，然後選取從 hello 清單。

    ![選擇儲存體容器][cache-export-data-container]
4. 輸入**Blob 名稱前置詞**按一下**匯出**toostart hello 匯出程序。 hello blob 名稱前置詞是使用的 tooprefix hello 這個匯出作業所產生的檔案名稱。

    ![匯出][cache-export-data]

    您可以在 hello Azure 入口網站的下列 hello 通知或藉由在 hello 檢視 hello 事件監視 hello hello 匯出作業的進度[稽核記錄檔](../azure-resource-manager/resource-group-audit.md)。

    ![匯出資料完成][cache-export-data-export-complete]

    Hello 匯出程序期間，快取保持可供使用。

## <a name="importexport-faq"></a>匯入/匯出常見問題集
本節中的 hello 匯入/匯出功能的相關常見問題的解答。

* [哪些定價層可以使用匯入/匯出？](#what-pricing-tiers-can-use-importexport)
* [我是否可以從任何 Redis 伺服器匯入資料？](#can-i-import-data-from-any-redis-server)
* [我可以匯入哪些 RDB 版本？](#what-rdb-versions-can-i-import)
* [在匯入/匯出作業期間，是否可以使用我的快取？](#is-my-cache-available-during-an-importexport-operation)
* [我可以使用匯入/匯出搭配 Redis 叢集嗎？](#can-i-use-importexport-with-redis-cluster)
* [匯入/匯出如何對自訂資料庫設定運作？](#how-does-importexport-work-with-a-custom-databases-setting)
* [匯入/匯出和 Redis 永續性有何不同？](#how-is-importexport-different-from-redis-persistence)
* [我可以使用 PowerShell、CLI 或其他管理用戶端自動化匯入/匯出嗎？](#can-i-automate-importexport-using-powershell-cli-or-other-management-clients)
* [我在匯入/匯出作業期間收到逾時錯誤。這代表什麼意思？](#i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean)
* [匯出我資料 tooAzure Blob 儲存體時，我會收到錯誤。發生什麼情形？](#i-got-an-error-when-exporting-my-data-to-azure-blob-storage-what-happened)

### <a name="what-pricing-tiers-can-use-importexport"></a>哪些定價層可以使用匯入/匯出？
只有在 hello premium 定價層中使用匯入/匯出。

### <a name="can-i-import-data-from-any-redis-server"></a>我是否可以從任何 Redis 伺服器匯入資料？
是，除了 tooimporting Azure Redis 快取執行個體從匯出的資料，您可以匯入 RDB 檔案從任何執行中的任何雲端或環境，例如 Linux、 Windows 或雲端提供者，例如 Amazon Web Services 的 Redis 伺服器。 toodo 此上傳 hello RDB 檔案從預期的 hello Redis 伺服器分頁或區塊 blob 中的 Azure 儲存體帳戶，然後匯入它至 premium Azure Redis 快取執行個體。 比方說，您可能想要從您的實際執行快取的 tooexport hello 資料，並匯入做為預備環境的一部分用於測試或移轉快取。

> [!IMPORTANT]
> toosuccessfully 匯入資料時使用分頁 blob、 hello 分頁 blob 大小必須對齊 512 位元組界限上，從非 Azure Redis 快取的 Redis 伺服器匯出。 如範例程式碼 tooperform 任何所需的位元組填補，請參閱[範例頁面部落格上傳](https://github.com/JimRoberts-MS/SamplePageBlobUpload)。
> 
> 

### <a name="what-rdb-versions-can-i-import"></a>我可以匯入哪些 RDB 版本？

Azure Redis 快取最多可支援到 RDB 第 7 版的 RDB 匯入。

### <a name="is-my-cache-available-during-an-importexport-operation"></a>在匯入/匯出作業期間，是否可以使用我的快取？
* **匯出**-快取保持可用狀態，並可以匯出作業期間繼續 toouse 您的快取。
* **匯入**-匯入作業啟動時，會變成無法使用，且會變成可供使用，hello 匯入作業完成時的快取。

### <a name="can-i-use-importexport-with-redis-cluster"></a>我可以使用匯入/匯出搭配 Redis 叢集嗎？
可以，您可以在叢集快取和非叢集快取之間匯入/匯出。 由於 Redis 叢集[僅支援資料庫 0](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)，因此不會匯入資料庫中 0 以外的任何資料。 匯入叢集的快取資料時，hello 金鑰會重新分配 hello 叢集的 hello 分區之間。

### <a name="how-does-importexport-work-with-a-custom-databases-setting"></a>匯入/匯出如何對自訂資料庫設定運作？
某些定價層會具有不同[資料庫限制](cache-configure.md#databases)，因此有一些考量當匯入，如果您設定自訂值的 hello`databases`快取建立期間設定。

* 匯入 tooa 定價層與較低時`databases`與從中匯出的 hello 層的限制：
  * 如果您使用 hello 預設數目`databases`、，也就是 16 個所有定價層不會遺失任何資料。
  * 如果您使用自訂的數字的`databases`，便在 2008 年 hello 的限制範圍內的 hello 層的 toowhich 您要匯入，會遺失任何資料。
  * 如果您匯出的資料包含超過 hello hello 新層的資料庫中的資料，這些較高的資料庫中的 hello 資料不會匯入。

### <a name="how-is-importexport-different-from-redis-persistence"></a>匯入/匯出和 Redis 永續性有何不同？
Azure Redis 快取持續性可讓您 toopersist Redis tooAzure 儲存體中儲存的資料。 設定持續性時，Azure Redis 快取會保存在根據可設定的備份頻率 Redis 二進位格式 toodisk hello Redis 快取的快照集。 發生重大事件，會停用 hello 主要和複本快取，會自動使用 hello 最新的快照集還原 hello 快取資料。 如需詳細資訊，請參閱[如何 tooconfigure Premium Azure Redis 快取的資料持續性](cache-how-to-premium-persistence.md)。

匯入 / 匯出可讓您將 toobring 資料或是從 Azure Redis 快取。 它無法設定備份和還原使用 Redis 永續性。

### <a name="can-i-automate-importexport-using-powershell-cli-or-other-management-clients"></a>我可以使用 PowerShell、CLI 或其他管理用戶端自動化匯入/匯出嗎？
是，適用於 PowerShell 指示看到[tooimport Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-import-a-redis-cache)和[tooexport Redis 快取](cache-howto-manage-redis-cache-powershell.md#to-export-a-redis-cache)。

### <a name="i-received-a-timeout-error-during-my-importexport-operation-what-does-it-mean"></a>我在匯入/匯出作業期間收到逾時錯誤。 這代表什麼意思？
如果您保留在 hello 上**匯入資料**或**匯出資料**刀鋒視窗中的時間超過 15 分鐘初始化 hello 作業之前，您收到錯誤訊息與下列範例錯誤的訊息類似 toohello:

    hello request tooimport data into cache 'contoso55' failed with status 'error' and error 'One of hello SAS URIs provided could not be used for hello following reason: hello SAS token end time (se) must be at least 1 hour from now and hello start time (st), if given, must be at least 15 minutes in hello past.

tooresolve，起始 hello 匯入或匯出作業之前經過 15 分鐘。

### <a name="i-got-an-error-when-exporting-my-data-tooazure-blob-storage-what-happened"></a>匯出我資料 tooAzure Blob 儲存體時，我會收到錯誤。 發生什麼情形？
匯出只能使用儲存為分頁 blob 的 RDB 檔案。 目前不支援其他的 Blob 類型，包括經常存取及不常存取層的 Blob 儲存體帳戶。 如需詳細資訊，請參閱 [Blob 儲存體帳戶](../storage/blobs/storage-blob-storage-tiers.md#blob-storage-accounts)。

## <a name="next-steps"></a>後續步驟
了解如何更進階的 toouse 快取功能。

* [簡介 toohello Azure Redis 快取進階層](cache-premium-tier-intro.md)    

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
