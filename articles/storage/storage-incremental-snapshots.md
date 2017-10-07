---
title: "備份及復原的未受管理的 Azure VM 磁碟 aaaUse 增量快照 |Microsoft 文件"
description: "使用增量快照，建立備份和復原 Azure 虛擬機器磁碟的自訂解決方案。"
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: 3524b987-bd65-4e35-83e7-fbc2136643e5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: aungoo
ms.openlocfilehash: 6d3e6d78e953f77a1028ac35dcde1ef046dbc3bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>以遞增快照集備份 Azure 非受控 VM 磁碟
## <a name="overview"></a>概觀
Azure 儲存體提供 hello 功能 tootake 快照集的 blob。 快照集時間中該時間點擷取 hello blob 狀態。 在本文中，我們將說明如何使用快照維護虛擬機器磁碟備份的案例。 您可以使用這種方法，當您選擇不 toouse Azure 備份和復原服務，以及想 toocreate 自訂備份策略的虛擬機器磁碟。

Azure 虛擬機器磁碟在 Azure 儲存體中會儲存為分頁 Blob。 因為我們指在這篇文章中的虛擬機器磁碟的備份策略，我們將參考 toosnapshots hello 的分頁 blob 的內容中。 toolearn 進一步了解快照集，請參閱太[建立 Blob 的快照集](https://msdn.microsoft.com/library/azure/hh488361.aspx)。

## <a name="what-is-a-snapshot"></a>什麼是快照？
Blob 快照是在某個時間點擷取的 Blob 唯讀版本。 一旦建立快照集後，即可加以讀取、複製或刪除，但不能修改。 快照集提供 blob 向上方式 tooback 出現在時間點。 直到 REST 版本 2015年-04-05，您必須 hello 能力 toocopy 完整快照集。 Hello REST 2015-07-08 版或更新版本，您也可以複製增量快照。

## <a name="full-snapshot-copy"></a>完整快照複製
可以是快照集以 hello 基底 blob 的 blob tookeep 備份複製 tooanother 儲存體帳戶。 您也可以透過其基底 blob，就像還原 hello blob tooan 複製快照集較舊版本。 從一個儲存體帳戶 tooanother 複製快照集時，它會佔用的 hello 相同空間為 hello 基底的分頁 blob。 因此，從一個儲存體帳戶 tooanother 複製整個快照集將會降低，而且也會耗用大量的 hello 目標儲存體帳戶中的空間。

> [!NOTE]
> 如果您複製 hello 基底 blob tooanother 目的地，以及它將不會複製 hello hello blob 的快照集。 同樣地，如果您要覆寫基底 blob 的複本，與 hello 基底 blob 相關聯的快照集不會受到影響，並保持不變，基底 blob 的名稱。
> 
> 

### <a name="back-up-disks-using-snapshots"></a>使用快照集備份磁碟
做為虛擬機器磁碟備份策略，您可以建立定期的 hello 磁碟或分頁 blob 的快照集，並將其複製 tooanother 儲存體帳戶使用的 puttygen 等工具[複製 Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx)作業或[AzCopy](storage-use-azcopy.md)。 您可以複製的快照集 tooa 目的地分頁 blob 以不同的名稱。 可寫入分頁 blob 而不是快照集 hello 結果的目的地分頁 blob。 本文中稍後我們將說明步驟 tootake 備份的虛擬機器磁碟使用快照集。

### <a name="restore-disks-using-snapshots"></a>使用快照還原磁碟
時間 toorestore 磁碟 tooa 穩定舊版擷取其中一種 hello 備份快照集時，您可以透過 hello 基底的分頁 blob 複製快照集。 Hello 快照集升級的 toohello 基底的分頁 blob 之後，hello 快照集會保留，但會覆寫其來源的副本，可以同時讀取和寫入。 本文中稍後我們將說明步驟 toorestore 舊版您從其快照集的磁碟。

### <a name="implementing-full-snapshot-copy"></a>實作完整快照複製
您可以藉由 hello 下列實作完整的快照集複製

* 首先，建立使用 hello hello 基底 blob 的快照[快照集 Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx)作業。
* 然後，複製 hello 快照 tooa 目標儲存體帳戶使用[複製 Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx)。
* 重複此程序 toomaintain 備份您的基底 blob。

## <a name="incremental-snapshot-copy"></a>增量快照複製
中的新功能 hello [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) API 提供更更好的方式 tooback 向上 hello 分頁 blob 或磁碟的快照集。 hello API 會傳回變更 hello 清單之間 hello 基底 blob 和 hello 快照集。 這會減少 hello 用於 hello 備份帳戶的儲存空間的數量。 hello 應用程式開發介面支援進階儲存體，以及標準儲存體上的分頁 blob。 您現在可以使用此 API，為 Azure VM 建置更快速且有效率的備份解決方案。 這會是適用於 hello REST 2015-07-08 版及更高版本。

累加快照集複製可讓您從儲存體帳戶 tooanother hello 之間的差異在於 toocopy

* 基底 Blob 及其快照，或
* Hello 基底 blob 的任何兩個快照集

提供符合下列條件的 hello，

* Jan 1 2016年或更新版本建立 hello blob。
* 不 hello blob 會覆寫與[PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx)或[複製 Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx)兩個快照之間。

**注意**︰此功能適用於進階和標準 Azure 分頁 Blob。

當您有自訂的備份策略會使用快照集，從一個儲存體帳戶 tooanother 複製 hello 快照集可能會非常慢，並消耗更多的儲存空間。 而不需要複製 hello 整個快照集 tooa 備份儲存體帳戶，您可以撰寫 hello 連續快照集 tooa 備份的分頁 blob 的差異。 如此一來，大幅減少 hello 時間 toocopy 和空間 toostore 備份。

### <a name="implementing-incremental-snapshot-copy"></a>實作增量快照複製
您可以藉由 hello 下列實作累加快照集複製

* 擷取快照的 hello 基底 blob 使用[快照集 Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx)。
* 複製 hello 快照 toohello 目標備份儲存體帳戶使用[複製 Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx)。 這會是 hello 備份的分頁 blob。 建立此備份分頁 Blob 的快照集，並將其儲存在備份帳戶中。
* 取得另一個使用快照集 Blob hello 基底 blob 的快照集。
* 取得使用基底 blob 的第一個和第二個快照之間的 hello 差異[GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx)。 使用新參數的 hello **prevsnapshot** toospecify hello hello 想與 tooget hello 差異的快照集的日期時間值。 這個參數時，hello REST 回應將包含目標快照與上一個快照，包括清除頁面之間已經變更的 hello 頁面。
* 使用[PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) tooapply 這些變更 toohello 備份的分頁 blob。
* 最後，建立 hello 備份的分頁 blob 的快照，然後將它儲存在 hello 備份儲存體帳戶。

Hello 下一節，我們將更詳細描述可以維護備份的磁碟使用累加快照集複製的方式

## <a name="scenario"></a>案例
在本節中，我們將使用快照說明涉及虛擬機器磁碟的自訂備份策略的案例。

請考慮使用連接進階儲存體 P30 磁碟的 DS 系列 Azure VM。 名為 hello P30 磁碟*mypremiumdisk*儲存在名為 premium 儲存體帳戶*mypremiumaccount*。 標準儲存體帳戶呼叫*mybackupstdaccount*會用來儲存備份 hello *mypremiumdisk*。 我們希望 tookeep 快照集的*mypremiumdisk*每隔 12 小時。

toolearn 有關建立儲存體帳戶和磁碟，請參閱太[關於 Azure 儲存體帳戶](storage-create-storage-account.md)。

關於備份 Azure Vm toolearn 參照太[計劃 Azure VM 備份](../backup/backup-azure-vms-introduction.md)。

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>步驟 toomaintain 備份的磁碟，使用累加快照集
hello 如下所述的步驟將建立的快照集*mypremiumdisk*和維護中的 hello 備份*mybackupstdaccount*。 hello 備份會是標準的分頁 blob 呼叫*mybackupstdpageblob*。 hello 備份的分頁 blob 永遠會反映為 hello 最後一次快照的相同狀態的 hello *mypremiumdisk*。

1. 首先，建立您的 premium 儲存體磁碟 hello 備份分頁二進位大型物件。 toodo 的快照，採用*mypremiumdisk*呼叫*mypremiumdisk_ss1*。
2. 將此快照集 toomybackupstdaccount 複製為分頁 blob 呼叫*mybackupstdpageblob*。
3. 使用[快照集 Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx) 建立稱為 *mybackupstdpageblob_ss1* 的 *mybackupstdpageblob* 快照集，並將其儲存在 *mybackupstdaccount* 中。
4. Hello 備份時間範圍期間建立的另一個快照*mypremiumdisk*、 說*mypremiumdisk_ss2*，並將它存放在*mypremiumaccount*。
5. 取得 hello hello 兩個快照之間的累加變更*mypremiumdisk_ss2*和*mypremiumdisk_ss1*，並使用[GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx)上*mypremiumdisk_ss2*與**prevsnapshot**參數設定 toohello 時間戳記*mypremiumdisk_ss1*。 撰寫這些累加變更 toohello 備份的分頁 blob *mybackupstdpageblob*中*mybackupstdaccount*。 如果 hello 累加變更有已刪除的範圍，他們必須從 hello 備份的分頁 blob 中清除。 使用[PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) toowrite 累加變更 toohello 備份的分頁 blob。
6. Hello 備份的分頁 blob 的快照*mybackupstdpageblob*，稱為*mybackupstdpageblob_ss2*。 刪除上一個快照的 hello *mypremiumdisk_ss1*進階儲存體帳戶。
7. 在每個備份時間範圍期間重複步驟 4-6。 如此一來，您可以維護標準儲存體帳戶中的 *mypremiumdisk* 備份。

![使用增量快照集備份磁碟](./media/storage-incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>步驟 toorestore 從快照集的磁碟
hello 如下所述的步驟將會還原 premium 磁碟*mypremiumdisk*稍早的快照集從 hello 備份儲存體帳戶的 tooan *mybackupstdaccount*。

1. 識別 hello 時間點您想要 toorestore hello 高階磁碟。 假設，為 snapshot *mybackupstdpageblob_ss2*，儲存在 hello 備份儲存體帳戶*mybackupstdaccount*。
2. Mybackupstdaccount，在將升級 hello 快照*mybackupstdpageblob_ss2* hello 新備份的基底分頁 blob 當做*mybackupstdpageblobrestored*。
3. 建立稱為 *mybackupstdpageblobrestored_ss1* 的這個已還原備份分頁 Blob 的快照集。
4. 複製 hello 還原分頁 blob *mybackupstdpageblobrestored*從*mybackupstdaccount*太*mypremiumaccount*為 hello 新 premium 磁碟*mypremiumdiskrestored*。
5. 建立稱為 *mypremiumdiskrestored_ss1* 的 *mypremiumdiskrestored* 快照集，以進行未來的增量備份。
6. 點 hello DS 系列 VM toohello 還原磁碟*mypremiumdiskrestored*和卸離舊 hello *mypremiumdisk*從 hello VM。
7. 開始 hello hello 還原磁碟上一節中所述的備份程序*mypremiumdiskrestored*，使用 hello *mybackupstdpageblobrestored*為 hello 備份的分頁 blob。

![從快照還原磁碟](./media/storage-incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>後續步驟
深入了解建立 blob 的快照集，並規劃 VM 備份基礎結構使用 hello 下方的連結。

* [建立 Blob 的快照集](https://msdn.microsoft.com/library/azure/hh488361.aspx)
* [規劃 VM 備份基礎結構](../backup/backup-azure-vms-introduction.md)

