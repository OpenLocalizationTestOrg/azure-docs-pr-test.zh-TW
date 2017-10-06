---
title: "在 Azure 儲存體中斷的 hello 事件 aaaWhat toodo |Microsoft 文件"
description: "Azure 儲存體中斷的 hello 事件中的哪些 toodo"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: 93e1e831c35b96b8bf190fa2b56ab89350bbac13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>如果 Azure 儲存體中斷，就會發生何種 toodo
Microsoft 在我們處理硬 toomake 確定我們的服務永遠都可以使用。 有時候會因為不可抗拒之因素，而造成服務在一或多個區域內中斷。 toohelp 處理這些極少數的發生次數，我們提供下列 Azure 儲存體服務的高階指引 hello。

## <a name="how-tooprepare"></a>如何 tooprepare
每個客戶 tooprepare 重要他們自己的嚴重損壞復原計畫。 您的應用程式正常運作的狀態中，從儲存體中斷 hello 投入時間 toorecover 通常涉及作業人員和自動化程序順序 tooreactivate 中。 請參考您自己的災害復原計畫 toohello toobuild 下方的 Azure 文件：

* [Azure 應用程式的災害復原和高可用性](/azure/architecture/resiliency/disaster-recovery-high-availability-azure-applications.md)
* [Azure 復原技術指導](/azure/architecture/resiliency.md)
* [Azure Site Recovery 服務](https://azure.microsoft.com/services/site-recovery/)
* [Azure 儲存體複寫](storage-redundancy.md)
* [Azure 備份服務](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>如何 toodetect
hello 建議的方式 toodetermine hello Azure 服務狀態是 toosubscribe toohello [Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)。

## <a name="what-toodo-if-a-storage-outage-occurs"></a>如果儲存體中斷，就會發生何種 toodo
如果一或多個儲存體服務目前暫時無法使用一或多個區域，有兩個您 tooconsider 選項。 如果您想要立即存取 tooyour 資料，請考慮選項 2。

### <a name="option-1-wait-for-recovery"></a>選項 1︰等待復原
在此情況下，您不需要採取任何動作。 我們正努力 toorestore hello Azure 服務可用性。 您可以監視 hello 服務狀態 hello [Azure 服務健全狀況儀表板](https://azure.microsoft.com/status/)。

### <a name="option-2-copy-data-from-secondary"></a>選項 2︰從次要區域複製資料
如果您選擇[讀取權限的地理備援儲存體 (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) （建議） 使用的儲存體帳戶，您將有讀取權限 tooyour 資料從 hello 次要區域。 您可以使用工具，例如[AzCopy](storage-use-azcopy.md)， [Azure PowerShell](storage-powershell-guide-full.md)，和 hello [Azure 資料移動文件庫](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)toocopy 到另一個儲存體帳戶中的 hello 次要區域資料unimpacted 的地區，然後點，您的應用程式 toothat 儲存體帳戶的讀取和寫入的可用性。

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>如果儲存體容錯移轉，就會發生何種 tooexpect
如果您選擇[異地備援儲存體 (GRS)](storage-redundancy.md#geo-redundant-storage) 或[讀取權限異地備援儲存體 (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (建議)，Azure 儲存體會將您的資料持久保留在兩個區域 (主要和次要)。 在兩個區域中，Azure 儲存體會持續維護多個您資料的複本。

地區的災害影響時主要區域，我們會先嘗試 toorestore hello 服務在該區域中。 相依於 hello 性質 hello 災害和其影響，在某些罕見的情況下我們可能無法 toorestore hello 主要區域。 這時候，我們會執行異地複寫容錯移轉。 hello 跨區域資料複寫是非同步程序可包含延遲，因此您很可能尚未經過變更複寫 toohello 次要區域可能會遺失。 您可以查詢 hello [「 上次同步處理時間 」 的儲存體帳戶](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/)tooget hello 複寫狀態的詳細資訊。

幾個有關 hello 儲存體地理容錯移轉的要點：

* Hello Azure 儲存體團隊將只會觸發儲存體地理容錯移轉 – 不不需要任何客戶動作。
* 您現有的儲存體服務，如 blob、 資料表、 佇列和檔案端點將會保持相同 hello hello 容錯移轉; 之後hello DNS 項目將需要更新 toobe tooswitch 從 hello 主要區域 toohello 次要區域。
* 之前和在 hello 地理容錯移轉期間，您沒有寫入權限 tooyour 儲存體帳戶，因為 toohello hello 災害影響，但您仍然可以閱讀從 hello 次要儲存體帳戶已設定為 RA-GRS 如果。
* 當 hello 地理容錯移轉已完成並 hello 傳播 DNS 變更時，就會繼續讀取和寫入存取 tooyour 儲存體帳戶;這點使用 toowhat toobe 次要端點。 
* 請注意，您就可以寫入存取，是否您有 GRS 或 RA-GRS hello 儲存體帳戶設定。 
* 您可以查詢[「 最後一個地理容錯移轉時間 」 的儲存體帳戶](https://msdn.microsoft.com/library/azure/ee460802.aspx)tooget 更多詳細資訊。
* Hello 容錯移轉之後，儲存體帳戶可以完全正常運作，但在 「 降級 」 狀態，因為它會實際裝載於獨立包含的區域沒有地理複寫可行。 toomitigate 此風險，我們將會還原 hello 原始的主要區域，然後執行地理容錯回復 toorestore hello 原始狀態。 如果 hello 原始的主要區域無法復原，我們將會配置另一個次要區域。
  上的 Azure 儲存體地理複寫的 hello 基礎結構的詳細資訊，請參閱 toohello hello 儲存體團隊部落格上的發行項的相關[備援選項和 RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/)。

## <a name="best-practices-for-protecting-your-data"></a>保護資料的最佳做法
有一些建議的方法 tooback，定期儲存體資料。

* VM 磁碟 – 使用 hello [Azure 備份服務](https://azure.microsoft.com/services/backup/)tooback hello Azure 虛擬機器所使用的 VM 磁碟上。
* 區塊 blob – 建立[快照](https://msdn.microsoft.com/library/azure/hh488361.aspx)每個區塊 blob，或複製 hello blob tooanother 儲存體帳戶中另一個區域使用[AzCopy](storage-use-azcopy.md)， [Azure PowerShell](storage-powershell-guide-full.md)，或使用 hello [Azure 的資料移動文件庫](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)。
* 使用資料表 – [AzCopy](storage-use-azcopy.md) tooexport hello 資料表資料到另一個地區內的另一個儲存體帳戶。
* 檔案-使用[AzCopy](storage-use-azcopy.md)或[Azure PowerShell](storage-powershell-guide-full.md) toocopy 您檔案 tooanother 儲存體帳戶中另一個區域。

如需建立應用程式來充分善用 hello RA-GRS 功能的相關資訊，請查看[設計高可用的應用程式使用 RA-GRS 儲存體](../storage-designing-ha-apps-with-ragrs.md)

