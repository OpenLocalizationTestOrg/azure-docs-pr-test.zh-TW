---
title: "Azure Vm 的 Azure 區域間的複寫 aaaReview hello 架構 |Microsoft 文件"
description: "本文提供元件和複寫使用 hello Azure Site Recovery 服務的 Azure 區域之間的 Azure Vm 時使用的架構的概觀。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a>步驟 1： 檢閱 Azure VM 之間的複寫的 Azure 地區的 hello 架構


檢閱 hello 之後[概觀步驟](azure-to-azure-walkthrough-overview.md)閱讀此文章 toounderstand hello 元件和複寫，並從一個 Azure 區域 tooanother，復原 Azure 虛擬機器 (Vm) 時所使用的處理序使用針對此部署，[Azure Site Recovery](site-recovery-overview.md)。

- 當您完成 hello 發行項時，您應該清楚了解 Azure VM 複寫 tooanother 區域的運作方式。
- 張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

>[!NOTE]
>Azure VM 複寫以 hello Site Recovery 服務目前為預覽狀態。



## <a name="architectural-components"></a>架構元件

下列圖表中的 hello 提供 Azure VM 中的環境 （在此範例中，hello 美國東部位置） 的特定區域的高層級檢視。 在 Azure VM 的環境中：
- 應用程式可以在 VM 上執行，且磁碟分散於不同的儲存體帳戶。
- hello Vm 可以包含在虛擬網路內的一個或多個子網路。

![客戶環境](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a>複寫程序

### <a name="step-1"></a>步驟 1

當您啟用 Azure VM 複寫 hello Azure 入口網站中的時，hello 示 hello 下列圖表和資料表會自動建立 hello 目標區域中的資源。 根據預設，會根據來源地區設定建立資源。 您可以自訂所需的 hello 目標設定。 [深入了解](site-recovery-replicate-azure-to-azure.md)。

![啟用複寫程序，步驟 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

**Resource** | **詳細資料**
--- | ---
**目標資源群組** | hello 複寫的 Vm 屬於容錯移轉之後的資源群組 toowhich。
**目標虛擬網路** | 在其中複寫的 Vm 位於容錯移轉之後 hello 的虛擬網路。 在來源和目標的虛擬網路之間會建立網路對應，反之亦然。
**快取儲存體帳戶** | 來源的 vm 上的變更複寫 toohello 目標儲存體帳戶之前，它們會追蹤並傳送嗨目標位置中 toohello 快取儲存體帳戶。 這可確保在 hello VM 上執行的實際執行應用程式的影響降到最低。
**目標儲存體帳戶**  | 在 hello 目標位置 toowhich hello 資料的儲存體帳戶會被複寫。
**目標可用性設定組**  | 可用性設定組中的 hello 複寫 Vm 位於容錯移轉之後。

### <a name="step-2"></a>步驟 2

因為已啟用複寫，hello Site Recovery 擴充行動服務會自動安裝在 hello VM 上。 發生 hello 下列情況：

1. hello VM 已向站台復原。

2. Hello VM 設定連續複寫。 資料寫入 hello VM 磁碟是持續傳送嗨來源位置中的 toohello 快取儲存體帳戶。

   ![啟用複寫程序，步驟 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  請注意，站台復原永遠不需要輸入連線 toohello VM。 僅輸出連接 tooSite 復原服務 Url/IP 位址、 Office 365 驗證 Url/IP 位址，以及需要快取儲存體帳戶的 IP 位址。 

## <a name="continuous-replication-process"></a>連續複寫程序

連續的複寫運作正常之後，磁碟寫入會立即傳送 toohello 快取儲存體帳戶。 站台復原處理 hello 資料，並將它傳送 toohello 目標儲存體帳戶。 處理 hello 資料之後，每隔幾分鐘 hello 目標儲存體帳戶會產生復原點。

## <a name="failover-process"></a>容錯移轉程序

當您起始容錯移轉時，Vm 建立 hello 目標資源群組、 目標虛擬網路、 目標子網路中的 hello 與 hello 目標可用性設定組。 在容錯移轉時，您可以使用任何復原點。

![容錯移轉程序](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a>後續步驟

跳過[步驟 2： 確認必要條件和限制](azure-to-azure-walkthrough-prerequisites.md)
