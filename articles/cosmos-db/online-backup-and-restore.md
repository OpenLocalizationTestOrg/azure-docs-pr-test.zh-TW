---
title: "aaaOnline 利用 Azure Cosmos DB 備份和還原 |Microsoft 文件"
description: "深入了解如何 tooperform 自動備份和還原 Azure Cosmos DB 資料庫上。"
keywords: "備份與還原, 線上備份"
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>使用 Azure Cosmos DB 進行自動線上備份及還原
Azure Cosmos DB 可以定期自動備份您的所有資料。 hello 自動備份而不會影響 hello 效能或可用性資料庫作業。 所有備份會儲存在另一個儲存體服務中，而且這些備份會全域複寫用於為區域性災害提供復原功能。 當您不小心刪除 Comos DB 容器，而稍後需要資料復原或災害復原解決方案 hello 自動備份適用於案例。  

本文章重述的 hello 資料備援和可用性 Cosmos DB 中的開頭，並接著討論備份。 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Cosmos DB 的高可用性 - 回顧
Cosmos DB 是設計的 toobe[分散](distribute-data-globally.md)– 可讓您 tooscale 輸送量到多個 Azure 區域，以及原則導向容錯移轉和透明多路連接的應用程式開發介面。 資料庫系統供應項目為[99.99%可用性 Sla](https://azure.microsoft.com/support/legal/sla/cosmos-db)，Cosmos DB 中的所有 hello 寫入都都由本機資料中心內的複本的仲裁內容經過永久認可的 toolocal 磁碟之前認可 toohello 用戶端。 請注意 hello 高可用性的 Cosmos DB 依賴本機儲存體，而不需依賴任何外部儲存體技術。 此外，如果您的資料庫帳戶與多個 Azure 區域相關聯，您的寫入也會在其他區域複寫。 tooscale 在低延遲的輸送量和存取資料，您可以有許多讀取要與您的資料庫帳戶相關聯的區域。 每個讀取區域 hello （複寫） 資料永久保存複本組中。  

Hello 下列圖表所示，單一 Cosmos DB 容器是[水平分割](partition-data.md)。 「 分割 」 會在下列圖表中的 hello 圓圈來標註，且每個資料分割會產生複本集透過高可用性。 這是在單一 Azure 區域 （以 hello X 軸表示） 的 hello 本機發佈。 此外，每個資料分割 （使用其對應的複本集） 然後會全域發佈到您的資料庫帳戶 （例如，在此圖 hello 三個區域 – 美國東部、 美國西部和印度中部） 相關聯的多個區域。 hello 「 資料分割集 」 是全域散發實體組成的多個複本 （hello Y 軸所表示） 的每個區域中的資料。 您可以將優先順序指派 toohello 區域與您的資料庫帳戶相關聯，而且 Cosmos DB 以透明的方式將容錯移轉 toohello 下一個區域發生嚴重損壞。 您也可以手動可以模擬容錯移轉 tootest hello 端對端應用程式可用性。  

hello 圖顯示高度以 Cosmos DB 備援 hello。

![Cosmos DB 的高度備援性](./media/online-backup-and-restore/redundancy.png)

![Cosmos DB 的高度備援性](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>完整自動線上備份
糟糕，我刪掉容器或資料庫了！ 以 Cosmos DB 不僅資料，但是 hello 備份資料也會有高備援和恢復功能 tooregional 損毀。 目前，這些自動化備份大約每四個小時備份一次，並隨時儲存 2 個最新的備份。 如果 hello 資料意外卸除或損毀，請[連絡 Azure 支援](https://azure.microsoft.com/support/options/)8 小時內。 

hello 備份而不會影響 hello 效能或可用性資料庫作業。 Cosmos DB hello 背景會 hello 備份，而不需要使用您已佈建之俄文或 hello 效能影響，而不影響 hello 可用性資料庫。 

不同於您儲存 Cosmos DB 內部的資料，hello 自動備份會儲存在 Azure Blob 儲存體服務。 tooguarantee hello 低效率延遲/上載 hello 快照集的備份是上傳的 tooan 執行個體，Azure Blob 儲存體中的 hello 與 hello 目前寫入區域 Cosmos DB 資料庫帳戶的相同的區域。 針對地區的災害復原時，備份資料 Azure Blob 儲存體中的每個快照集是一次複寫透過地理備援儲存體 (GRS) tooanother 區域。 hello 下列圖表顯示 hello 整個 Cosmos DB 容器 （具有所有三個主要磁碟分割在美國西部，在此範例中） 備份到遠端的 Azure Blob 儲存體帳戶，在美國西部然後 GRS 複寫 tooEast 我們。 

hello 下列影像說明 GRS Azure 儲存體中的所有 Cosmos DB 實體的定期完整備份。

![GRS Azure 儲存體中所有 Cosmos DB 實體的定期完整備份](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>備份保留期限
如上面所述，Azure Cosmos DB 每四個小時會採用您資料的快照集，並保留 30 天 hello 的每個資料分割的最後兩個快照集。 依我們的合規性規定，會在 90 天後清除快照集。

如果您想 toomaintain 您自己的快照集，您可以使用 hello 匯出 tooJSON 選項在 hello Azure Cosmos DB[資料移轉工具](import-data.md#export-to-json-file)tooschedule 其他備份。 

## <a name="restoring-a-database-from-an-online-backup"></a>從線上備份還原資料庫
如果您不小心刪除您的資料庫或集合，您可以[提出支援票證](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)或[連絡 Azure 支援](https://azure.microsoft.com/support/options/)toorestore hello hello 最後一次自動備份的資料。 如果您需要 toorestore 資料庫因為資料損毀問題，請參閱[處理資料損毀](#handling-data-corruption)tootake 其他所需步驟從穿透 hello 備份 tooprevent hello 損毀資料。 還原您備份 toobe 是特定快照集，Cosmos DB 需要 hello 資料無法 hello hello 該快照集備份週期期間。

## <a name="handling-data-corruption"></a>處理資料損毀
Azure Cosmos DB hello 系統中保留 hello 的每個資料分割的最後兩個備份。 （的文件、 圖形、 表格集合） 的容器或資料庫意外刪除，因為其中一個 hello 最後一個版本可以還原時，非常適合此模型。 不過，hello 的情況下如果當使用者可能會造成資料損毀問題，Azure Cosmos DB 可能不知道 hello 資料損毀，並就有可能在 hello 損毀，可能會有滲入 hello 備份。 一旦偵測到損毀，您應該刪除損毀的 hello 容器 （集合/圖表/資料表），因此備份已損毀的資料遭到覆寫受到保護。 因為 hello 最後一個備份可能是四個小時，可以運用 hello 使用者[變更摘要](change-feed.md)toocapture 和市集 hello 最後四個小時的資料之前刪除 hello 容器。

## <a name="next-steps"></a>後續步驟

tooreplicate 資料庫中多個資料中心，請參閱[分散您的資料以 Cosmos DB 全域](distribute-data-globally.md)。 

toofile 連絡 Azure 支援人員，[檔案 hello Azure 入口網站票證](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。

