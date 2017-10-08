---
title: "使用 Azure Site Recovery 的實體伺服器複寫 tooAzure aaaReview hello 架構 |Microsoft 文件"
description: "本文提供元件和複寫在內部部署實體伺服器 tooAzure 以 hello Azure Site Recovery 服務時使用的架構的概觀"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 09c9b136-35f5-465e-8d0f-f4c5d5d9f880
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 4f334c181fa6f0821adf978ebe9dbd7d36a3c753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-physical-server-replication-tooazure"></a>步驟 1： 檢閱實體伺服器複寫 tooAzure hello 架構

本文說明 hello 元件和處理序使用複寫在內部部署 Windows/Linux 實體伺服器 tooAzure，使用 hello 時[Azure Site Recovery](site-recovery-overview.md)服務。

張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="architectural-components"></a>架構元件

hello 表格摘要說明您需要的 hello 元件。

**元件** | **需求** | **詳細資料**
--- | --- | ---
**Azure** | 您需要 Azure 帳戶、Azure 儲存體帳戶及 Azure 網路。 | 複寫的資料會儲存在 hello 儲存體帳戶，並發生容錯移轉時，將會建立與 hello 複寫資料的 Azure Vm。 在建立時即，azure Vm 連接 toohello Azure 虛擬網路。
**組態伺服器** | 單一內部部署管理伺服器 （實體伺服器或 VMware VM） 執行所有 hello 內部部署站台復原元件。 這些包括組態伺服器、處理伺服器、主要目標伺服器。 | hello 組態伺服器元件會協調在內部部署與 Azure 之間的通訊並管理資料複寫。
 **處理序伺服器**  | Hello 組態伺服器上的預設安裝。 | 會做為複寫閘道器。 接收複寫資料、 最佳化與快取、 壓縮和加密，並將它傳送 tooAzure 儲存體。<br/><br/> hello 處理序伺服器也會處理推入安裝的 hello 行動服務 tooprotected 機器。<br/><br/> 您可以新增其他個別的專用處理序伺服器，toohandle 增加磁碟區的複寫流量。
 **主要目標伺服器** | Hello 在內部部署組態伺服器上的預設安裝。 | 在從 Azure 容錯回復期間，處理複寫資料。<br/><br/> 如果容錯回復的流量很高，您可以部署個別的主要目標伺服器來供容錯回復使用。
**複寫的伺服器** | hello 行動服務已安裝元件要 tooreplicate 每個 Windows/Linux 伺服器上。 它可以手動安裝在每部電腦上，或從 hello 處理序伺服器推入安裝。
**容錯回復** | 若要進行容錯回復，必須要有 VMware 基礎結構。 您不能容錯回復 tooa 實體伺服器。


**圖 1： 實體 tooAzure 元件**

![元件](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>複寫程序

1. 您設定 hello 部署，包括在內部部署和 Azure 元件。 在 hello 復原服務保存庫，您可以指定 hello 複寫來源和目標，設定 hello 組態伺服器，建立複寫原則，部署 hello 行動服務、 啟用複寫，並執行測試容錯移轉。
2.  複寫的 tooAzure 儲存區是根據 hello 複寫原則，與 hello 資料的初始複本機器複寫。
4. 初始複寫完成之後，便會開始複寫差異變更 tooAzure。 機器的追蹤變更會保存在 .hrl 檔案中。
    - 複寫機器 hello 組態與伺服器通訊連接埠 HTTPS 443 輸入複寫管理的。
    - 複寫機器複寫資料 toohello 處理序伺服器連接埠上傳送 HTTPS 9443 輸入 （可以修改）。
    - hello 組態伺服器協調使用 Azure 的複寫管理透過 HTTPS 443 輸出連接埠。
    - hello 處理序伺服器接收資料從來源機器、 最佳化及加密，並將它 tooAzure 儲存體傳送連接埠 443 輸出。
    - 如果您啟用多重 VM 一致性，然後 hello 複寫群組中的電腦與對方進行通訊透過連接埠 20004。 如果您將多部機器群組為幾個共用當機時保持一致復原點和應用程式一致復原點的複寫群組，當這些群組在進行容錯移轉時，便會使用多部 VM。 這非常有用，如果電腦執行 hello 相同的工作負載，而且需要 toobe 一致。
5. 流量會複寫的 tooAzure 儲存體公用端點，超過 hello 網際網路。 或者，您可以使用 Azure ExpressRoute [公用對等](../expressroute/expressroute-circuit-peerings.md#public-peering)。 不支援透過站對站 VPN 從內部部署站台 tooAzure 複寫流量。

**圖 2： 實體 tooAzure 複寫**

![增強](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>容錯移轉和容錯回復程序

在您確認測試容錯移轉正常運作之後，您可以視需要執行未規劃的容錯移轉 tooAzure。 當您執行容錯移轉時，系統會從複寫的資料建立 Azure VM。 接著，當您的主要內部部署站台恢復可用時，您就可以容錯回復。 請注意：

- 不支援有計劃的容錯移轉。
- 您可以容錯移轉單一電腦，或建立[復原計劃](site-recovery-create-recovery-plans.md)，toofail 在一起的多部電腦。
- 您從 Azure VM 的 hello 複本認可容錯移轉 toostart 存取 hello 工作負載。
- Hello 主要站台再次可用時，您會從 hello 次要 toohello 主要站台複寫 hello 機器。 然後，執行未規劃的容錯移轉從 hello 次要站台。 確認此容錯移轉之後，資料將會回復在內部，並再次需要 tooenable 複寫 tooAzure。

容錯回復元件包括：

- **在 Azure 中的暫存處理序伺服器**： 您需要的處理序伺服器的 Azure VM tooact、 從 Azure toohandle 複寫向上 tooset。 容錯回復完成後，您可以刪除此 VM。
- **VPN 連線**： 您需要從 hello Azure 網路 toohello 在內部部署站台 VPN 連線 （或 Azure ExpressRoute）。
- **另一個在內部部署主要目標伺服器**: hello （hello 組態伺服器上的預設安裝） 的內部部署主要目標伺服器會處理容錯回復。 如果您要容錯回復大量流量，您應該針對此目的設定個別的內部部署主要目標伺服器。
- **容錯回復原則**：您需要一個容錯回復原則。 此原則會在您建立複寫原則時自動建立。
- **VMware 基礎結構**： 您必須容錯回復 tooan 內部部署 VMware VM。 這表示您需要在內部部署 VMware 基礎結構中，即使您要複寫在內部部署實體伺服器 tooAzure。

**圖 3：實體伺服器容錯回復**

![容錯回復](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>後續步驟

跳過[步驟 2： 確認必要條件和限制](physical-walkthrough-prerequisites.md)
