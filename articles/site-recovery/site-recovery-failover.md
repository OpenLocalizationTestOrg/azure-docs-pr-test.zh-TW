---
title: "在站台復原 aaaFailover |Microsoft 文件"
description: "Azure Site Recovery 會協調 hello 複寫、 容錯移轉和復原的虛擬機器和實體伺服器。 深入了解容錯移轉 tooAzure 或次要資料中心。"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Site Recovery 中的容錯移轉
本文說明如何 toofailover 虛擬機器和實體伺服器受 Site Recovery 保護。

## <a name="prerequisites"></a>必要條件
1. 執行容錯移轉之前，請執行[測試容錯移轉](site-recovery-test-failover-to-azure.md)tooensure 的一切如預期般運作。
1. [準備 hello 網路](site-recovery-network-design.md)在目標位置，然後再進行容錯移轉。  


## <a name="run-a-failover"></a>執行容錯移轉
此程序描述如何容錯移轉的 toorun[復原計劃](site-recovery-create-recovery-plans.md)。 或者您可以執行單一虛擬機器或實體伺服器 hello 容錯移轉從 hello**複寫項目**頁面


![容錯移轉](./media/site-recovery-failover/Failover.png)

1. 選取 [復原方案]  >  *recoveryplan_name*。 按一下 [容錯移轉]
2. 在 hello**容錯移轉**畫面上，選取**復原點**toofailover 至。 您可以使用其中一個 hello 下列選項：
    1.  **最新**（預設值）： 此選項會先處理所有 hello 資料它們容錯移轉 tooit 之前已傳送的 tooSite 復原服務 toocreate 每部虛擬機器的復原點。 此選項提供 hello 觸發 hello 容錯移轉時，最低的 RPO （復原點目標） hello 建立虛擬機器容錯移轉擁有 hello 的所有資料後，已為複寫 tooSite 復原服務。
    1.  **最新版處理**: hello 復原計劃 toohello 最新復原點的站台復原服務已經處理的所有虛擬機器都容錯移轉這個選項。 當您在進行測試容錯移轉的虛擬機器時，也會顯示 hello 最新的已處理的復原點的時間戳記。 如果您要復原計劃的容錯移轉，您可以移 tooindividual 虛擬機器，並查看**最新復原點**磚 tooget 這項資訊。 當沒有時間 tooprocess hello 未處理的資料時，此選項提供低 RTO （復原時間目標） 容錯移轉選項。
    1.  **最新的應用程式一致**: hello 復原計劃 toohello 最新應用程式一致復原點的站台復原服務已經處理的所有虛擬機器都容錯移轉這個選項。 當您在進行測試容錯移轉的虛擬機器時，也會顯示 hello 最新的應用程式一致復原點的時間戳記。 如果您要復原計劃的容錯移轉，您可以移 tooindividual 虛擬機器，並查看**最新復原點**磚 tooget 這項資訊。
    1.  **已處理最近的多部虛擬機器**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。 虛擬機器屬於複寫群組容錯移轉 toohello 最新通用多重 VM 一致性復原點。 其他虛擬機器容錯移轉 tootheir 最近處理過的復原點。  
    1.  **最近的多部虛擬機器應用程式一致**：此選項僅適用於至少一部虛擬機器已啟動多部虛擬機器一致性的復原計劃。 虛擬機器屬於複寫群組容錯移轉 toohello 最新通用多部 VM 應用程式一致復原點。 其他虛擬機器容錯移轉 tootheir 最新應用程式一致復原點。
    1.  **自訂**： 如果您在進行測試容錯移轉的虛擬機器，則您可以使用此選項 toofailover tooa 特定的復原點。

    > [!NOTE]
    > 當您容錯移轉 tooAzure hello 選項 toochoose 復原點才可用。
    >
    >


1. 如果某些 hello hello 復原計劃中的虛擬機器已在先前執行容錯移轉，而且現在 hello 虛擬機器正在作用中來源和目標位置上，您可以使用**變更方向**選項 toodecide hello 方向應該會 hello 容錯移轉。
1. 如果您要容錯移轉 tooAzure 與 hello （只有在您保護 hyper-v 虛擬機器從 VMM 伺服器時，才適用） 的雲端啟用資料加密，請在**加密金鑰**選取 hello 已發行憑證，當您啟用在 hello VMM 伺服器上的安裝期間的資料加密。
1. 選取**機器關機再開始容錯移轉**關機之前觸發的來源虛擬機器的 Site Recovery tooattempt toodo 只要 hello 容錯移轉。 即使關機失敗，仍會繼續容錯移轉。  

    > [!NOTE]
    > 如果 hyper-v 虛擬機器，此選項也會嘗試不尚未傳送 toohello 服務觸發 hello 容錯移轉之前的 toosynchronize hello 在內部部署資料。
    >
    >

1. 您可以依照 hello hello 容錯移轉的進度**作業**頁面。 即使未規劃的容錯移轉期間發生錯誤，hello 復原方案執行，直到完成為止。
1. Hello 容錯移轉之後，請登入以 tooit 驗證 hello 虛擬機器。 如果您想要 toogo 另一個復原點 hello 虛擬機器，然後您可以使用**變更復原點**選項。
1. 一旦您滿意 hello 容錯移轉虛擬機器時，您可以**認可**hello 容錯移轉。 這會刪除所有 hello 可用復原點與 hello 服務和**變更復原點**選項將無法再使用。

## <a name="planned-failover"></a>計劃性容錯移轉
除了容錯移轉，使用 Site Recovery 保護的 Hyper-V 虛擬機器也支援**計劃性容錯移轉**。 這是完全不會遺失資料的容錯移轉選項。 觸發已規劃的容錯移轉時，第一次 hello 虛擬機器已關閉，hello 資料尚未同步處理的 toobe 已同步處理，則會觸發容錯移轉的來源。

> [!NOTE]
> 當您容錯移轉的 hyper-v 虛擬機器從一個內部部署站台 tooanother 在內部部署站台，toocome 後 toohello 內部主要站台有 toofirst**反向複寫**hello 虛擬機器回復 tooprimary 站台和然後觸發容錯移轉。 如果主要虛擬機器 hello 就無法使用，然後之前啟動太**反向複寫**您有從備份 toorestore hello 虛擬機器。   
>
>

## <a name="failover-job"></a>容錯移轉作業

![容錯移轉](./media/site-recovery-failover/FailoverJob.png)

觸發容錯移轉時會執行下列步驟︰

1. 先決條件檢查︰這個步驟可確保符合容錯移轉所需的所有條件
1. 容錯移轉： 此步驟中處理 hello 資料，並讓它準備好，以便可以建立 Azure 虛擬機器，不使用。 如果您已選擇**最新**復原點，此步驟中建立的復原點從 toohello 服務已傳送的 hello 資料。
1. 開始： 此步驟中建立 Azure 虛擬機器使用 hello hello 上一個步驟中處理的資料。

> [!WARNING]
> **不會取消正在進行中容錯移轉**： 在啟動容錯移轉之前，已停止的 hello 虛擬機器複寫。 如果您**取消**進度作業中容錯移轉會停止，但 hello 虛擬機器將不會啟動 tooreplicate。 無法重新開始複寫。
>
>

## <a name="time-taken-for-failover-tooazure"></a>容錯移轉 tooAzure 的時間

在某些情況下，虛擬機器的容錯移轉需要其他中繼步驟的程序通常需要約 8 too10 分鐘 toocomplete。 這些情況如下所示︰

* VMware 虛擬機器使用的行動服務版本早於 9.8 版
* 實體伺服器 
* VMware Linux 虛擬機器
* 如同實體伺服器般受到保護的 Hyper-V 虛擬機器
* 沒有以下驅動程式作為開機驅動程式的 VMware 虛擬機器 
    * storvsc 
    * vmbus 
    * storflt 
    * intelide 
    * atapi
* 沒有啟用 DHCP 服務的 VMware 虛擬機器，無論其是否正在使用 DHCP 或靜態 IP 位址

在所有 hello 其他情況下此中繼步驟並不需要與 hello hello 容錯移轉所花費的時間會顯著降低。 





## <a name="using-scripts-in-failover"></a>在容錯移轉中使用指令碼
您可能想要 tooautomate 特定動作時執行的容錯移轉。 您可以使用指令碼或[Azure 自動化 runbook](site-recovery-runbook-automation.md)中[復原計劃](site-recovery-create-recovery-plans.md)toodo 的。

## <a name="other-considerations"></a>其他考量
* **磁碟機代號**— tooretain hello 磁碟機代號在容錯移轉後的虛擬機器上，您可以設定 hello **SAN 原則**hello 虛擬機器太**OnlineAll**。 [閱讀更多資訊](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure)。



## <a name="next-steps"></a>後續步驟
一旦您已容錯移轉虛擬機器，而 hello 在內部部署資料中心，您應該[**重新保護**](site-recovery-how-to-reprotect.md) VMware 虛擬機器備份 toohello 在內部部署資料中心。

使用[**規劃的容錯移轉**](site-recovery-failback-from-azure-to-hyper-v.md)太選項**容錯回復**hyper-v 虛擬機器從 Azure 備份 tooon 內部部署。

如果您無法透過 hyper-v 虛擬機器 tooanother 在內部部署資料中心受 VMM 伺服器與 hello 主要資料中心使用，然後使用**反轉複寫**選項 toostart hello 複寫後 toohello主要資料中心。
