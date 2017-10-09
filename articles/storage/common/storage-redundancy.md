---
title: "在 Azure 儲存體 aaaData 複寫 |Microsoft 文件"
description: "系統會 複製Microsoft Azure 儲存體帳戶中的資料，以維持持久性和高可用性。 複寫選項包括本地備援儲存體 (LRS)、區域備援儲存體 (ZRS)、異地備援儲存體 (GRS) 和讀取權限異地備援儲存體 (RA-GRS)。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Azure 儲存體複寫

儲存體帳戶一定是您在 Microsoft Azure 中的 hello 資料複寫 tooensure 耐久性與高可用性。 您的資料，請在 hello 相同資料中心內或 tooa 第二個資料中心，依據您選擇的複寫選項的複寫複本。 複寫會保護資料，並保留您的應用程式執行時間的暫時性硬體故障的 hello 事件中。 如果您的資料複寫的 tooa 第二個資料中心，因此會保護以避免 hello 主要位置發生災難性失敗。

複寫可確保您的儲存體帳戶符合 hello[服務等級協定 (SLA) 的儲存體](https://azure.microsoft.com/support/legal/sla/storage/)即使在 hello 字體的失敗。 如需 Azure 儲存體的 hello SLA 保證持久性和可用性，請參閱。

當您建立儲存體帳戶時，您可以選取其中一個 hello 下列複寫選項：

* [本地備援儲存體 (LRS)](#locally-redundant-storage)
* [區域備援儲存體 (ZRS)](#zone-redundant-storage)
* [異地備援儲存體 (GRS)](#geo-redundant-storage)
* [讀取權限異地備援儲存體 (RA-GRS)](#read-access-geo-redundant-storage)

當您建立儲存體帳戶時，讀取權限的地理備援儲存體 (RA-GRS) 會是 hello 預設選項。

hello 下表提供 LRS、 ZRS、 GRS 與 RA-GRS 的 hello 差異的快速概觀，而後續各節說明每一種更多詳細資料中的複寫。

| 複寫策略 | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| 可跨多個資料中心複寫資料。 |否 |是 |是 |是 |
| 資料可以從次要位置，以及 hello 主要位置讀取。 |否 |否 |否 |是 |
| 可在不同的節點上維護的資料副本數量。 |3 |3 |6 |6 |

請參閱[Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)如需定價資訊的 hello 不同備援選項。

> [!NOTE]
> 進階儲存體僅支援本地備援儲存體 (LRS)。 如需進階儲存體的相關資訊，請參閱 [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../storage-premium-storage.md)。
>

## <a name="locally-redundant-storage"></a>本地備援儲存體
本機備援儲存體 (LRS) 方式複寫三次儲存體延展單位，裝載於您要在其中建立儲存體帳戶的 hello 地區的資料中心內的資料。 只有已寫入的 tooall 三個複本後，則寫入要求會傳回成功。 這三個複本會各自位於一個儲存體縮放單位不同的容錯網域和升級網域中。

儲存體縮放單位是儲存體節點機架的集合。 容錯網域 (FD) 是一組代表失敗的實體單位，而且可以視為屬於 toohello 節點的節點相同實體機架。 升級網域 (UD) 是一群 hello 服務升級 （首展） 程序期間一起升級的節點。 hello 三個複本會散佈到 Ud 和 Fd，資料是可用的即使硬體故障影響單一機架或首展期間升級節點時將一個存放裝置延展單位 tooensure 內。

LRS 是 hello 最低的成本選項，並提供最少的持久性比較 tooother 選項。 Hello 事件的資料中心層級災害 （觸發，灌爆等） 中所有的三個複本可能遺失或無法修復。 toomitigate 此風險，對於大部分應用程式建議地理備援儲存體 (GRS)。

在某些情況下仍可能需要本地備援儲存體︰

* 提供最高的 Azure 儲存體複寫選項的最大頻寬。
* 如果您的應用程式儲存可以輕鬆重新建構的資料，則您可能會選擇使用 LRS。
* 某些應用程式是受限制的 tooreplicating 資料只在一個國家/地區，因為 toodata 控管需求。 配對區域可位於另一個國家/地區。 如需區域配對的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。

## <a name="zone-redundant-storage"></a>區域備援儲存體
區域備援儲存體 (ZRS) 以非同步方式將您的資料複寫到在加法 toostoring 三個複本類似 tooLRS，因此能提供持久性比 LRS 更高的一或兩個區域內的資料中心。 ZRS 中儲存的資料是永久性的即使 hello 主要資料中心是無法使用或無法修復。
計劃 toouse ZRS 的客戶應該注意的：

* ZRS 只適用於一般用途儲存體帳戶中的區塊 Blob，且僅支援儲存體服務版本 2014-02-14 及更新版本。
* 因為非同步複寫到延遲，它是本機災害 hello 事件中的可能尚未經過變更複寫 toohello 次要將會遺失，如果無法從主要 hello 復原 hello 資料。
* 除非 Microsoft 起始次要的容錯移轉 toohello，否則 hello 複本可能無法使用。
* 無法轉換 ZRS 帳戶，稍後 tooLRS 或 GRS。 同樣地，現有的 LRS 或 GRS 帳戶不能轉換 tooa ZRS 帳戶。
* ZRS 帳戶並沒有度量或記錄功能。

## <a name="geo-redundant-storage"></a>異地備援儲存體
地理備援儲存體 (GRS) 會將複寫您資料 tooa 次要區域相隔數百英哩 hello 主要區域。 如果儲存體帳戶已啟用 GRS，則是持久即使在 hello 的全面性地區中斷或災害中的 hello 主要區域是無法復原的情況下您的資料。

已啟用 grs 的儲存體帳戶，更新為第一個認可的 toohello 主要區域，它會在此複寫三次。 然後會以非同步方式複寫 hello 更新 toohello 次要區域，其中也複寫三次。

使用 GRS 時，這兩個 hello 主要和次要區域管理複本跨不同的容錯網域和升級述與 LRS 儲存體延展單位內的網域。

考量：

* 由於非同步複寫牽涉到 hello 事件地區性災難，就有可能變更尚未複寫的延遲，如果 hello 資料無法復原從 hello 主要區域，將會遺失 toohello 次要區域。
* hello 複本不是可用的除非 Microsoft 起始容錯移轉 toohello 次要區域。 如果 Microsoft 未起始容錯移轉 toohello 次要區域，您必須讀取和寫入存取 toothat 資料之後 hello 容錯移轉已完成。 如需詳細資訊，請參閱[災害復原指南](../storage-disaster-recovery-guidance.md)。 
* 如果應用程式要從 hello 次要區域 tooread，hello 使用者應該啟用 RA-GRS。

當您建立儲存體帳戶時，您會選取 hello hello 帳戶的主要區域。 hello 次要區域取決於 hello 主要區域，而且無法變更。 下表中的 hello 顯示 hello 主要和次要區域配對。

| 主要 | 次要 |
| --- | --- |
| 美國中北部 |美國中南部 |
| 美國中南部 |美國中北部 |
| 美國東部 |美國西部 |
| 美國西部 |美國東部 |
| 美國東部 2 |美國中部 |
| 美國中部 |美國東部 2 |
| 北歐 |西歐 |
| 西歐 |北歐 |
| 東南亞 |東亞 |
| 東亞 |東南亞 |
| 中國東部 |中國北部 |
| 中國北部 |中國東部 |
| 日本東部 |日本西部 |
| 日本西部 |日本東部 |
| 巴西南部 |美國中南部 |
| 澳洲東部 |澳大利亞東南部 |
| 澳大利亞東南部 |澳洲東部 |
| 印度南部 |印度中部 |
| 印度中部 |印度南部 |
| 印度西部 |印度南部 |
| 美國政府愛荷華州 |美國政府維吉尼亞州 |
| 美國政府維吉尼亞州 |美國政府德克薩斯州 |
| 美國政府德克薩斯州 |美國政府亞利桑那州 |
| 美國政府亞利桑那州 |美國政府德克薩斯州 |
| 加拿大中部 |加拿大東部 |
| 加拿大東部 |加拿大中部 |
| 英國西部 |英國南部 |
| 英國南部 |英國西部 |
| 德國中部 |德國東北部 |
| 德國東北部 |德國中部 |
| 美國西部 2 |美國中西部 |
| 美國中西部 |美國西部 2 |

如需有關 Azure 支援區域的最新資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/)。

>[!NOTE]  
> 美國維吉尼亞州政府次要區域是美國德克薩斯州政府。 之前，美國維吉尼亞州政府將美國愛荷華州政府視為次要區域。 儲存體帳戶次要區域是在利用並美國 Gov 稍後移轉 tooUS Gov 德州為 internaldnsname 區域。 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>讀取權限異地備援儲存體
藉由提供唯讀存取 toohello 資料在 hello 次要位置中，此外 toohello 複寫，跨兩個區域 GRS 所提供的讀取權限的地理備援儲存體 (RA-GRS) 最大化的可用性的儲存體帳戶。

當您啟用唯讀存取 tooyour 資料 hello 次要區域中的時，您的資料位於次要端點，在儲存體帳戶的加法 toohello 主要端點。 hello 次要端點類似 toohello 主要端點，但將 hello 後置詞附加`–secondary`toohello 帳戶名稱。 例如，如果您的主要端點 hello Blob 服務是`myaccount.blob.core.windows.net`，則次要端點是`myaccount-secondary.blob.core.windows.net`。 同時 hello 主要和次要端點的 hello 儲存體帳戶的存取金鑰會 hello 相同。

考量：

* 您的應用程式有 toomanage 哪一個端點使用 RA-GRS 時，與進行互動。
* 由於非同步複寫牽涉到 hello 事件地區性災難，就有可能變更尚未複寫的延遲，如果 hello 資料無法復原從 hello 主要區域，將會遺失 toohello 次要區域。
* 如果是 Microsoft 啟動容錯移轉 toohello 次要區域，您必須讀取和寫入存取 toothat 資料之後 hello 容錯移轉已完成。 如需詳細資訊，請參閱[災害復原指南](../storage-disaster-recovery-guidance.md)。 
* RA-GRS 適用於高可用性目的。 如需擴充性指引，請檢閱 hello[效能檢查清單](../storage-performance-checklist.md)。

## <a name="frequently-asked-questions"></a>常見問題集

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1.如何變更我的儲存體帳戶 hello 地理複寫類型？

   您可以變更您的儲存體帳戶之間 LRS、 GRS，hello 地理複寫類型和 RA-GRS 使用 hello [Azure 入口網站](https://portal.azure.com/)， [Azure Powershell](storage-powershell-guide-full.md)或以程式設計方式使用其中一種我們許多儲存體用戶端程式庫。 請注意，ZRS 帳戶無法轉換成 LRS 或 GRS。 同樣地，現有的 LRS 或 GRS 帳戶不能轉換 tooa ZRS 帳戶。

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2.將會有任何停機時間有所改變 hello 複寫類型的儲存體帳戶？

   否，不會有任何停機時間。

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3.將會有任何額外的成本有所改變 hello 複寫類型的儲存體帳戶？

   是。 如果您從 LRS tooGRS （或 RA-GRS） 儲存體帳戶變更，所以會發生額外的費用，做為出口參與複製現有的資料從主要位置 toohello 次要位置。 一旦複製 hello 初始資料是沒有進一步的地理複寫 hello 資料從 hello toosecondary 主要位置的其他輸出費用。 hello 頻寬費用的詳細資料位於 hello [Azure 儲存體定價頁面](https://azure.microsoft.com/pricing/details/storage/blobs/)。 如果您將變更 GRS tooLRS，沒有任何額外的成本，但您的資料將會刪除從 hello 次要位置。

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4.RA-GRS 可以給我什麼協助？
   
   GRS 的儲存體提供從相隔數百英哩 hello 主要區域的主要 tooa 次要區域資料的複寫。 在這種情況下，您的資料為永久性即使在 hello 的全面性地區中斷或災害中的 hello 主要區域是無法復原的情況下。 包含此資訊 RA-GRS 存放裝置加上它會新增 hello 能力 tooread hello 資料從 hello 次要位置。 一些有關如何針對 tooleverage 這項功能，請參閱太[設計高可用的應用程式使用 RA-GRS 儲存體](../storage-designing-ha-apps-with-ragrs.md)。 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5.是否有方法為我 toofigure 出要花多久 tooreplicate 我的資料從 hello 主要 toohello 次要區域？
   
   如果您使用 RA-GRS 儲存體，您可以檢查 hello 上次同步處理時間，您的儲存體帳戶。 上次同步處理時間為 GMT 日期/時間值，hello 上次同步處理時間之前的所有主要寫入已成功寫入 toohello 次要位置，這表示它們會讀取 hello 次要位置的可用 toobe。 上次同步處理時間可能會或可能無法供讀取尚未，主要會寫入 hello 之後。 您可以查詢此值使用 hello [Azure 入口網站](https://portal.azure.com/)， [Azure PowerShell](storage-powershell-guide-full.md)，或以程式設計方式使用 hello REST API 或其中一個 hello 儲存體用戶端程式庫。 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6.如果發生中斷時 hello 主要區域中，如何切換 toohello 次要區域？
   
   Toohello 發行項，請參閱[如果 Azure 儲存體中斷，就會發生何種 toodo](../storage-disaster-recovery-guidance.md)如需詳細資訊。

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7.什麼是 hello RPO 和 RTO GRS？
   
   復原點目標 (RPO): 在 GRS 和 RA-GRS，hello 儲存體服務以非同步方式從 hello 主要 toohello 次要位置的地理複寫 hello 資料。 如果沒有主要地區的災害，在容錯移轉已執行 toobe 尚未進行地理複寫的最新差異變更可能會遺失。 hello 潛在資料遺失的分鐘數為參照的 tooas hello RPO （亦即可以復原時間 toowhich 資料中的 hello 點）。 我們的 RPO 通常低於 15 分鐘，但目前並沒有關於異地複寫時間長短的 SLA。

   復原時間目標 (RTO): 這是多久會帶我們 toodo hello 容錯移轉和 hello 儲存體帳戶上一步要線上取得就 toodo 容錯移轉的量值。 hello 時間 toodo hello 容錯移轉包括下列 hello:
    * hello 時間我們 tooinvestigate 並判斷是否我們可以復原 hello hello 主要位置的資料，或者我們需要 toodo 容錯移轉。
    * 藉由變更 hello 主要 DNS 項目 toopoint toohello 次要位置的容錯移轉 hello 帳戶。

   我們負責 hello 非常嚴重，保留您的資料，因此如果有任何的 hello 資料復原的機會，我們會拖延上執行 hello 的容錯移轉，並專注於 hello 主要位置中的 hello 資料復原。 我們計劃在未來的 hello，tooprovide API tooallow 您 tootrigger 帳戶層級的容錯移轉時，這會讓您 toocontrol hello RTO，但這尚未提供。
   
## <a name="next-steps"></a>後續步驟
* [使用 RA-GRS 儲存體設計高可用性應用程式](../storage-designing-ha-apps-with-ragrs.md)
* [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)
* [關於 Azure 儲存體帳戶](../storage-create-storage-account.md)
* [Azure 儲存體的延展性與效能目標](storage-scalability-targets.md)
* [Microsoft Azure 儲存體備援選項和讀取權限異地備援儲存體 ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP 文件：Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

