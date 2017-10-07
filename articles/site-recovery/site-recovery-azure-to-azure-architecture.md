---
title: "aaaHow 未在 Azure Site Recovery 的 Azure 區域工作之間的 Azure 虛擬機器複寫嗎？  | Microsoft Docs"
description: "本文提供元件和複寫使用 hello Azure Site Recovery 服務的 Azure 區域之間的 Azure Vm 時使用的架構的概觀。"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a>Azure VM 複寫如何在 Site Recovery 中運作？


本文說明 hello 元件和處理序中複製及復原 Azure 虛擬機器 (Vm) 從一個區域 tooanother 涉及使用 hello [Azure Site Recovery](site-recovery-overview.md)服務。

>[!NOTE]
>Azure VM 複寫以 hello Site Recovery 服務目前為預覽狀態。

張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="architectural-components"></a>架構元件

下列圖表中的 hello 提供 Azure VM 中的環境 （在此範例中，hello 美國東部位置） 的特定區域的高層級檢視。 在 Azure VM 的環境中：
- 應用程式可以在 VM 上執行，且磁碟分散於不同的儲存體帳戶。
- hello Vm 可以包含在虛擬網路內的一個或多個子網路。

![客戶環境](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

深入了解 hello 部署必要條件和需求 hello[支援矩陣](site-recovery-support-matrix-azure-to-azure.md)。

## <a name="replication-process"></a>複寫程序

### <a name="step-1"></a>步驟 1

當您啟用 Azure VM 複寫 hello Azure 入口網站中的時，hello 示 hello 下列圖表和資料表會自動建立 hello 目標區域中的資源。 根據預設，會根據來源地區設定建立資源。 您可以自訂所需的 hello 目標設定。 [深入了解](site-recovery-replicate-azure-to-azure.md)。

![啟用複寫程序，步驟 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

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

   ![啟用複寫程序，步驟 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > 站台復原永遠不需要輸入的連線 toohello VM。 hello VM 需要的傳出連線 tooSite 復原服務 Url/IP 位址、 Office 365 驗證 Url/IP 位址，並快取儲存體帳戶的 IP 位址。 如需詳細資訊，請參閱 hello[複寫 Azure 虛擬機器的網路指引](site-recovery-azure-to-azure-networking-guidance.md)發行項。

## <a name="continuous-replication-process"></a>連續複寫程序

連續的複寫運作正常之後，磁碟寫入會立即傳送 toohello 快取儲存體帳戶。 站台復原處理 hello 資料，並將它傳送 toohello 目標儲存體帳戶。 處理 hello 資料之後，每隔幾分鐘 hello 目標儲存體帳戶會產生復原點。

## <a name="failover-process"></a>容錯移轉程序

當您起始容錯移轉時，Vm 建立 hello 目標資源群組、 目標虛擬網路、 目標子網路中的 hello 與 hello 目標可用性設定組。 在容錯移轉時，您可以使用任何復原點。

![容錯移轉程序](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a>後續步驟

- 深入了解 Azure VM 複寫的[網路](site-recovery-azure-to-azure-networking-guidance.md)。
- 依照逐步解說太[複寫 Azure Vm。](site-recovery-azure-to-azure.md)
