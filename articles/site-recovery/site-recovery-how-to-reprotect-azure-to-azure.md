---
title: "透過 Azure 虛擬機器回復 tooprimary Azure 區域無法從 aaaHow tooReprotect |Microsoft 文件"
description: "容錯移轉之後的 Vm 從一個 Azure 區域 tooanother，您可以使用 Azure Site Recovery tooprotect hello 機器反方向。 深入了解如何 hello 步驟 toodo 的容錯移轉之前重新保護。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>從重新保護容錯移轉的 Azure 區域後 tooprimary 區域



>[!NOTE]
>
> Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。


## <a name="overview"></a>概觀
當您[容錯移轉](site-recovery-failover.md)hello 虛擬機器從一個 Azure 區域 tooanother hello 虛擬機器處於未受保護狀態。 如果您想要 toobring 送回 toohello 主要區域，您需要 toofirst 再次保護 hello 虛擬機器，然後容錯移轉。 朝任一個方向進行容錯移轉沒有任何差異。 同樣地，張貼的 hello 虛擬機器啟用保護，沒有任何容錯移轉 hello 重新保護後或 post 容錯回復之間的差異。
重新保護，以及 tooavoid 混淆 tooexplain hello 工作流程，我們將使用 hello 主要站台的 hello 受保護的電腦為東亞地區和 hello 復原站台的 hello 機器為東南亞區域。 容錯移轉期間，您將會容錯移轉 hello 虛擬機器 toohello 東南亞區域。 您的容錯回復之前，您會需要從東南亞後 tooEast 亞洲 tooreprotect hello 虛擬機器。 本文說明如何 hello 步驟 tooreprotect。

> [!WARNING]
> 如果您有[完成移轉](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)，移動的 hello 的虛擬機器 tooanother 資源群組，或已刪除 hello Azure 虛擬機器，您之後就無法容錯回復。

完成之後重新保護和 hello 受保護的虛擬機器要複寫，您可以起始 hello 虛擬機器 toobring 的容錯移轉後加以備份 tooEast 亞洲區域。

將註解或問題張貼結尾 hello 這份文件或在 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="prerequisites"></a>必要條件
1. hello 虛擬機器應該已認可。
2. hello 目標站台-在此情況下 hello 東亞 Azure 區域應該可以使用而且應該能夠 tooaccess/建立該區域中的新資源。

## <a name="steps-tooreprotect"></a>步驟 tooreprotect

下列是 hello 步驟 tooreprotect 虛擬機器使用 hello 預設值。

1. 在**保存庫** > **複寫項目**，hello 已容錯移轉的虛擬機器上按一下滑鼠右鍵，然後選取**重新保護**。 您也可以按一下電腦，並選取 hello**重新保護**hello 命令按鈕。

![以滑鼠右鍵按一下 tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. 在 hello 刀鋒視窗中，請注意的保護，該 hello 方向**東南亞 tooEast 亞洲**，已選取。

![重新保護刀鋒視窗](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. 檢閱 hello**資源群組，網路、 儲存體和可用性集**資訊並按一下 [確定]。 如果沒有任何標記 （新） 的資源，也會建立 hello 一部分重新保護。

這將會觸發程序作業重新 hello 最新的資料，保護會先植入 hello 目標站台 (在此情況下 SEA) 的工作一旦完成，請將複寫您的容錯移轉之前的 hello 差異備份 tooSoutheast 亞洲。

### <a name="reprotect-customization"></a>重新保護自訂
如果您想 toochoose hello 擷取儲存體帳戶或 hello 網路期間重新保護，因此使用 hello 自訂 hello 重新保護刀鋒視窗上提供選項，您可以執行。

![自訂選項](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

您可以自訂 hello 期間重新保護下列他目標虛擬機器的內容。

![自訂刀鋒視窗](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|屬性 |注意事項  |
|---------|---------|
|目標資源群組     | 您可以選擇將在其中建立個虛擬機器的 toochange hello 目標資源群組。 Hello 在重新保護，將刪除 hello 目標虛擬機器，因此您可以選擇新的資源群組，您可以在其下建立 hello VM post 容錯移轉         |
|目標虛擬網路     | Hello 重新保護時，就無法變更網路。 toochange hello 網路封包，重做 hello 網路對應。         |
|目標儲存體     | 您可以變更 hello toowhich hello 虛擬機器將會容錯移轉後建立的儲存體帳戶。         |
|快取儲存體     | 您可以指定將在複寫期間使用的快取儲存體帳戶。 如果您進行 hello 預設值，新的快取儲存體帳戶將會建立，如果不存在。         |
|可用性設定組     |如果 hello 東亞中的虛擬機器的可用性設定組的一部分，您可以選擇在東南亞 hello 目標虛擬機器設定可用性。 預設值會尋找 hello 現有 SEA 可用性設定組，並再試一次 toouse 它。 進行自訂時，您可以指定全新的 AV 設定組。         |


### <a name="what-happens-during-reprotect"></a>重新保護期間會發生什麼情況？

就像 hello 之後第一次啟用保護時，以下是 hello artefacts，如果您使用 hello 預設值建立的。
1. 快取儲存體帳戶取得 hello 東亞地區中建立。
2. 如果 hello 目標儲存體帳戶 （hello 原始儲存體帳戶的 hello 東南亞 VM） 不存在，則會建立一個新。 hello 名稱是後置字元為"asr"hello 東亞虛擬機器的儲存體帳戶。
3. 如果 hello 目標 AV 集不存在，而且 hello 預設值可讓您偵測它，則它會建立 hello 的一部分時，才需要的 toocreate 新 AV 設定，請重新保護工作。 如果您已自訂 hello 重新保護，然後將會使用選取的 hello AV 集。
4.

hello 下面是 hello 觸發重新保護工作時，就可能發生的步驟清單。 這是在虛擬機器存在 hello 案例 hello 目標端。

1. hello 需要 artefacts 會建立為重新保護的一部分。 如果這些項目已存在，則會重複使用。
2. hello 目標端 （東南亞） 關閉虛擬機器是第一次，如果它正在執行。
3. hello 目標端虛擬機器的磁碟會為種子 blob，Azure Site recovery 複製到容器。
4. 然後刪除 hello 目標端的虛擬機器。
5. hello 目前來源端 （東亞） 虛擬機器 tooreplicate 使用 hello 種子 blob。 這可確保僅複寫差異部份。
6. hello hello 來源磁碟和 hello 種子 blob 之間的重大變更會同步處理。 這可能需要一些時間 toocomplete。
7. Hello 重新保護工作完成，hello 差異複寫會開始建立 hello 原則根據復原點。

> [!NOTE]
> 您無法在復原計劃層級進行保護。 您只能在每個 VM 層級進行重新保護。

Hello 重新保護之後成功，hello 虛擬機器將會進入受保護的狀態。

## <a name="next-steps"></a>後續步驟

Hello 虛擬機器已進入受保護的狀態之後，您可以起始容錯移轉。 hello 容錯移轉將 hello 東亞 Azure 區域中的虛擬機器關機，然後建立並開機 hello 東南亞區域虛擬機器。 因此是短暫的停機時間 hello 應用程式。 如果您的應用程式可以容許停機時間，因此，請選擇 hello 容錯移轉時間。 建議您先測試容錯移轉 hello 虛擬機器 toomake 確定它接下來是否正確，才能起始容錯移轉。

-   [步驟 tooinitiate 測試 hello 虛擬機器容錯移轉](site-recovery-test-failover-to-azure.md)

-   [步驟 tooinitiate hello 虛擬機器容錯移轉](site-recovery-failover.md)
