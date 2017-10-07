---
title: "測試容錯移轉與 Azure Site Recovery 的 Azure VM 複寫 aaaRun |Microsoft 文件"
description: "摘要說明您需要執行測試容錯移轉的 Azure Vm 複寫 tooanother Azure 區域使用 hello Azure Site Recovery 服務的 hello 步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>步驟 6：執行 Azure VM 複寫的測試容錯移轉

您已啟用的 Azure 虛擬機器 (Vm) 複寫之後，請依照本文中，從一個 Azure 區域 tooanother，使用 hello toorun 測試容錯移轉中的 hello 步驟[Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

- 當您完成 hello 發行項時，您應該已經確認與測試容錯移轉時，至少一個 Azure VM 可以容錯移轉 tooyour 次要 Azure 地區。 
- 張貼於 hello 下方的本文中，任何註解或詢問問題中 hello [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Azure VM 複寫目前為預覽狀態。


## <a name="before-you-start"></a>開始之前

- 在執行測試容錯移轉之前，我們建議您確認 hello VM 內容，然後進行您需要的任何變更。 您可以存取在 hello VM 屬性**複寫項目**。 hello **Essentials**刀鋒視窗會顯示電腦設定狀態的資訊。
- 建議您針對 hello 測試容錯移轉，而且不要 hello 網路使用不同的 Azure VM 網路 （預設或自訂），設定為實際執行容錯移轉。
- hello 測試容錯移轉容錯移轉 Azure Vm （和其存放裝置） toohello 次要 Azure 地區。 它不會複寫任何相依的應用程式或資源。 如果上執行應用程式失敗的 Vm 上有相依於其他資源，例如 Active Directory 或 DNS，您需要 tooreplicate 這些，如果它們不提供次要區域中。 [深入了解](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- 如果您想要將 tooaccess 複寫 Vm 從內部部署站台的容錯移轉之後，您需要太[準備 tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese Vm。

## <a name="run-a-test-failover"></a>執行測試容錯移轉

1. 在**設定** > **複寫的項目**，按一下 hello VM **+ 測試容錯移轉**圖示。 

2. 在**測試容錯移轉**，選取復原點 toouse hello 容錯移轉：

    - **最新版處理**： 失敗 hello VM toohello 最新復原點上方 hello Site Recovery 服務所處理。 會顯示 hello 時間戳記。 使用此選項時，無須花費時間處理資料，因此它會提供低 RTO (復原時間目標)。
    - **最新的應用程式一致**： 容錯移轉所有 Vm toohello 最新的應用程式一致復原點的這個選項。 會顯示 hello 時間戳記。 
    - **自訂**：選取任何復原點。
 
3. Hello 容錯移轉發生後，將會連接選取 hello 目標 Azure 虛擬網路 toowhich hello 次要區域中的 Azure Vm。
4. toostart hello 容錯移轉，請按一下**確定**。 tootrack 進度，請按一下 hello VM tooopen 其屬性。 或者，您可以按一下 hello**測試容錯移轉**作業在 hello 保存庫名稱 >**設定** > **作業** > **的站台復原工作**.
5. Hello 之後容錯移轉完成時，Azure VM 的 hello 複本會出現在 hello Azure 入口網站 >**虛擬機器**。 請確定該 hello VM hello 適當的大小，它已連接 toohello 適當的網路，而且它正在執行。
6. 按一下 toodelete hello hello 測試容錯移轉期間所建立的 Vm**清除測試容錯移轉**hello 上複寫項目或 hello 復原計劃。 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 

[深入了解](site-recovery-test-failover-to-azure.md)測試容錯移轉。

## <a name="next-steps"></a>後續步驟

測試容錯移轉之後，即完成本逐步解說。 現在，深入了解在生產環境中執行容錯移轉：

- [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉，以及如何 toorun 它們。
- 深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)容錯移轉多個 VM。
- 深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)。
- 深入了解容錯移轉之後[重新保護 Azure VM](site-recovery-how-to-reprotect.md)。

