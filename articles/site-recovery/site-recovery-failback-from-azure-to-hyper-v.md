---
title: "hyper-v 虛擬機器的 Azure Site Recovery 中 aaaFailback |Microsoft 文件"
description: "Azure Site Recovery 會協調 hello 複寫、 容錯移轉和復原的虛擬機器和實體伺服器。 深入了解從 Azure tooon 內部部署資料中心容錯回復。"
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
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>在 Site Recovery 中容錯回復 Hyper-V 虛擬機器

本文說明 toofailback 虛擬機器保護站台復原的方式。

## <a name="prerequisites"></a>必要條件
1. 確定該 hello 主要站台 VMM 伺服器/HYPER-V 伺服器已連接。
2. 您應該已經執行**認可**hello 虛擬機器上。

## <a name="why-is-there-no-button-called-failback"></a>為什麼沒有一個叫做容錯回復的按鈕？
在 hello 入口網站上沒有明確呼叫容錯回復的動作。 容錯回復是步驟，其中您回顧 toohello 主要站台。 根據定義，容錯移轉時，您容錯移轉 hello primary(on-premises) 網站 toorecovery (Azure)，與容錯回復的虛擬機器時，您容錯移轉 hello 虛擬機器從復原備份 tooprimary。

當您起始容錯移轉時，hello 刀鋒視窗會通知您關於 hello 方向的 hello 作業。 如果 hello 方向是從 Azure tooOn 單位，則容錯回復。

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>為什麼會有只規劃的容錯移轉筆勢 toofailback？
Azure 是高可用性環境，虛擬機器永遠可用。 容錯回復是計劃的活動，以便 hello 工作負載可以在內部部署執行一次開始，會決定 tootake 短暫的停機時間。 這樣不會遺失資料。 因此規劃的容錯移轉動作，將會關閉在 Azure 中的 hello Vm，請下載 hello 最新的變更並確保不會遺失任何資料。

## <a name="initiate-failback"></a>起始容錯回復
容錯移轉之後從 hello toosecondary 主要位置，複寫的虛擬機器未受保護的網站復原，且將 hello 次要位置現在作為 hello 作用中的位置。 請遵循這些程序 toofail 後 toohello 原始主要站台。 此程序描述如何 toorun 規劃的容錯移轉的復原計劃。 或者您可以執行 hello 容錯移轉的單一虛擬機器上 hello**虛擬機器** 索引標籤。

1. 選取 [復原方案]  >  *recoveryplan_name*。 按一下 [容錯移轉] **容錯移轉** > **Planned 容錯移轉**中張貼意見或問題。
2. 在 hello * * 確認計劃的容錯移轉 * * 頁面上，選擇 hello 來源和目標位置。 請注意 hello 容錯移轉方向。 如果 hello 容錯移轉，從主要工作為預期，而且所有虛擬機器都都在 hello 次要位置，這是僅提供資訊。
3. 如果您正從 Azure 進行容錯回復，請選取 [資料同步處理] 中的設定：

   * **在容錯移轉前同步處理資料 (僅同步處理差異變更)** - 這個選項可將虛擬機器的停機時間縮到最短，因為不需關閉虛擬機器即可進行同步處理。 它沒有 hello 遵循：
     * 階段 1： 在 Azure 中採用 hello 虛擬機器的快照並複製 toohello 在內部部署 HYPER-V 主機。 hello 機器會繼續在 Azure 中執行。
     * 階段 2： 關閉 hello Azure 中的虛擬機器，如此那里發生任何新的變更。 hello 最後差異變更一組是傳送的 toohello 在內部部署伺服器，hello 在內部部署虛擬機器完全啟動。

    - **僅在容錯移轉期間同步處理資料 (完整下載)**—如果您已經在 Azure 上長時間執行，請使用這個選項。 這個選項會更快，因為我們預期大部分 hello 磁碟的已變更，我們不希望 toospend 總和檢查碼計算中的時間。 它會執行 hello 磁碟的下載。 因此，也適用於 hello 由內部部署虛擬機器已被刪除。

    >[!NOTE]
    >我們建議您使用此選項，如果您已執行 Azure 時間 （每月或更多） 或已刪除 hello 由內部部署虛擬機器。這個選項不會執行任何總和檢查碼計算。
    >
    >




4. 如果已啟用資料加密 hello 雲端中**加密金鑰**選取 hello 啟用 hello VMM 伺服器上的提供者安裝期間的資料加密時發出的憑證。
5. 起始 hello 容錯移轉。 您可以依照 hello hello 容錯移轉的進度**作業** 索引標籤。
6. 如果您選取 hello 選項 toosynchronize hello 資料 hello 容錯移轉之前，一次 hello 初始資料同步處理完成，且您已準備好 tooshut 向 hello Azure 虛擬機器中，按一下**作業**規劃的容錯移轉作業名稱**完成容錯移轉**。 這會關閉 hello Azure 機器、 傳送嗨最新變更 toohello 在內部部署虛擬機器，並啟動 hello VM 內部。
7. 您現在可以記錄到 hello 虛擬機器 toovalidate 會如預期般出現。
8. hello 虛擬機器處於認可擱置狀態。 按一下**認可**toocommit hello 容錯移轉。
9. 現在順序按一下 toocomplete hello 容錯回復**反向複寫**toostart 保護 hello hello 主要網站中的虛擬機器。

## <a name="failback-tooan-alternate-location"></a>容錯回復 tooan 替代位置
如果您部署之間的保護[HYPER-V 站台與 Azure](site-recovery-hyper-v-site-to-azure.md) tooability toofailback 有來自 Azure tooan 替代的內部部署位置。 這是您需要新的內部部署硬體 tooset 時相當實用。 以下是執行此動作的方式。

1. 如果您正要設定新的硬體安裝 Windows Server 2012 R2 和 hello hello 伺服器上的 HYPER-V 角色。
2. 建立虛擬網路交換器以相同的名稱，您必須在 hello 原始伺服器上的 hello。
3. 選取**受保護項目** -> **保護群組** ->  <ProtectionGroupName>  ->  <VirtualMachineName> toofail，再選取**已計劃容錯移轉**。
4. 在 [記事]  select 中張貼意見或問題。
5. 在**主機名稱**選取 hello 想 tooplace hello 虛擬機器的新 HYPER-V 主機伺服器。
6. 資料同步處理中我們建議您選取 hello 選項**hello hello 容錯移轉之前的資料同步處理**。 這個選項可以將虛擬機器的停機時間降至最低，因為不需關閉虛擬機器即可進行同步處理。 它沒有 hello 遵循：

   * 階段 1： 在 Azure 中採用 hello 虛擬機器的快照並複製 toohello 在內部部署 HYPER-V 主機。 hello 機器會繼續在 Azure 中執行。
   * 階段 2： 關閉 hello Azure 中的虛擬機器，如此那里發生任何新的變更。 最後一組變更傳送的 toohello 在內部部署伺服器與 hello 在內部部署虛擬機器完全啟動 hello。
7. 按一下 hello 核取記號 toobegin hello 容錯移轉 （回復）。
8. Hello 初始同步處理完成，您已經準備好 tooshut 關閉 hello Azure 中的虛擬機器之後，請按一下**作業** > <planned failover job> > **完成容錯移轉**。 這關閉 hello Azure 機器、 傳送嗨最新變更 toohello 在內部部署虛擬機器並啟動它。
9. 您可以登入 hello 在內部部署虛擬機器 tooverify 一切如預期般運作。 然後按一下 **認可**toofinish hello 容錯移轉。
10. 按一下**反向複寫**toostart 保護 hello 在內部部署虛擬機器。

    > [!NOTE]
    > 如果在資料同步處理步驟時，您可以取消 hello 容錯回復作業，hello 內部 VM 將會損毀的狀態。 這是因為資料同步處理從 Azure VM 磁碟 toohello 內部資料磁碟，複製 hello 最新的資料，並 hello 同步處理完成之前，hello 磁碟資料可能未處於一致的狀態。 如果開機 hello 內部 VM 取消資料同步處理之後，它可能會無法開機。 重新觸發容錯移轉 toocomplete hello 資料同步處理。
    >
    >



## <a name="next-steps"></a>後續步驟

當您完成 hello 容錯回復作業，**認可**hello 虛擬機器。 認可刪除 hello Azure 虛擬機器和其磁碟，並準備 hello VM toobe 再次保護。

之後**認可**，您可以起始 hello*反向複寫*。 這會啟動保護從內部部署後 tooAzure hello 虛擬機器。 請注意這會複寫 hello 所做的變更，因為 VM 在 Azure 中已關閉，並因此將傳送差異 hello 只變更。
