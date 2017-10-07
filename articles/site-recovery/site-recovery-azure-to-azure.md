---
title: "複寫 Azure 區域之間的 Azure Vm 的災害復原需求： Azure tooAzure |Microsoft 文件"
description: "摘要說明您需要 tooreplicate Azure Vm 與嚴重損壞修復所需的 hello Azure Site Recovery 服務的 Azure 區域 (Azure-Azure) 之間的 hello 步驟。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>使用 Azure Site Recovery 在區域之間椱寫 Azure VM

>[!NOTE]
>
> Azure 虛擬機器 (VM) 的 Azure Site Recovery 複寫目前為預覽狀態。

本文說明如何使用 Azure 的區域之間的 Azure Vm tooreplicate hello [Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在這份文件或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。

## <a name="disaster-recovery-in-azure"></a>Azure 的災害復原

內建的 Azure 基礎結構的功能和功能都在 Azure Vm 執行的工作負載的 tooa 健全且彈性的可用性策略。 不過，有許多為什麼您需要 tooplan 之間的 Azure 地區的災害復原自己的原因：

- 您需要特定的應用程式和工作負載所需的業務續航力和災害復原 (BCDR) 策略 toomeet 規範指導方針。
- 您想 hello 能力 tooprotect 並復原 Azure Vm，根據您的商務決策而不只根據內建的 Azure 功能。
- 根據您的商務與相容性需求，而不會影響生產環境中需要 tootest 容錯移轉和復原。
- 您需要 toofail toohello hello 災害事件中的復原區域，並順暢地容錯回復 toohello 原始的來源地區。

使用站台復原您的 Azure-Azure VM 複寫 toohelp 所有這些工作。


## <a name="why-use-site-recovery"></a>為什麼要使用 Site Recovery？      

站台復原提供簡單的方式 tooreplicate Azure Vm 之間的區域：

- **自動部署**。 不是主動-主動複寫模型，像沒有需要高而且非常複雜的基礎結構 hello 次要區域中。 當您啟用複寫時，站台復原會自動建立所需的 hello 資源在 hello 目標區域中，取決於來源地區設定。
- **控制區域**。 使用站台復原，也可以從中的任何區域 tooany 區域大陸複寫。 使用讀取權限異地備援儲存體 (僅以非同步方式在標準[配對區域](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)之間複寫) 比較此項。 讀取權限的地理備援儲存體提供唯讀存取 toohello 資料在 hello 目標區域中。
- **自動化複寫**。 Site Recovery 提供自動化連續複寫。 按一下即可觸發容錯移轉和容錯回復。
- **RTO 和 RPO**。 站台復原會利用連接區域 tookeep hello Azure 網路基礎結構 RTO 和 RPO 非常低。
- **測試**。 您可藉由隨選測試容錯移轉視需要執行災害復原演練，完全不影響生產工作負載或進行中的複寫。
- **復原計劃**。 您可以使用復原計劃 tooorchestrate 容錯移轉和容錯回復 hello 整個應用程式在多個 Vm 上執行。 hello 復原計劃功能具有豐富的第一級整合與 Azure 自動化 runbook。


## <a name="deployment-summary"></a>部署摘要

以下是所需的摘要 toodo tooset Vm 的 Azure 區域之間的複寫設定：

1. 建立復原服務保存庫。 hello 保存庫包含組態設定，並且會協調複寫。
2. 啟用複寫 hello Azure Vm。
3. 執行測試容錯移轉 toomake 確定所有內容都如預期運作。

>[!IMPORTANT]
>
> 您可以檢查 hello[支援比對 Azure VM 複寫](./site-recovery-support-matrix-azure-to-azure.md)。

>[!IMPORTANT]
>
> 如需如何 tooconfigure hello 複寫所需輸出的網路連線的 Azure Vm 的站台復原資訊，請參閱 hello[網路指引文件](./site-recovery-azure-to-azure-networking-guidance.md)。

### <a name="before-you-start"></a>開始之前

* 您的 Azure 使用者帳戶需要 toohave 特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooenable 的 Azure 虛擬機器的複寫。
* 您的 Azure 訂用帳戶應啟用的 toocreate Vm，您想為 hello 災害復原區域 toouse hello 目標位置中。 請連絡客戶支援 tooenable hello 必要的配額。

## <a name="create-a-recovery-services-vault"></a>建立復原服務保存庫

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> 我們建議您在您想要 Vm tooreplicate hello 位置建立 hello 復原服務保存庫。 例如，如果您的目標位置是 hello 中央而我們，建立 hello 保存庫中的**美國中部**。

## <a name="enable-replication"></a>啟用複寫

在**復原服務保存庫**，按一下 hello 保存庫名稱。 在 hello 保存庫中，按一下 hello **+ 複寫** 按鈕。

### <a name="step-1-configure-hello-source"></a>步驟 1. 設定 hello 來源
1. 在 [來源] 中，選取 [Azure-PREVIEW]。
2. 在**來源位置**，選取 hello 來源 Vm 目前的執行所在的 Azure 區域。
3. 選取 hello 的 Vm 的部署模型：**資源管理員**或**傳統**。
4. 選取 hello**來源資源群組**資源管理員 vm 或**雲端服務**用於傳統的 Vm。

    ![設定 hello 來源](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>步驟 2. 選取虛擬機器

* 選取您想 tooreplicate，然後再按一下 hello Vm**確定**。

    ![選取 VM](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>步驟 3. 配置設定

1. toooverride hello 預設設定為目標，並指定 hello 設定您的選擇，按一下**自訂**。 如需詳細資訊，請參閱[自訂目標資源](site-recovery-replicate-azure-to-azure.md##customize-target-resources)。

    ![配置設定](./media/site-recovery-azure-to-azure/settings.png)


2. 根據預設，Site Recovery 會建立複寫原則，每隔 4 小時會製作應用程式一致快照，並將復原點保留 24 小時。 按一下 toocreate 具有不同的設定原則**自訂**下一步太**複寫原則**。

    ![自訂原則](./media/site-recovery-azure-to-azure/customize-policy.png)

3. 按一下 佈建 hello 目標資源 toostart，**建立目標資源**。 佈建約需要一分鐘左右。 不要關閉 hello 刀鋒視窗中，佈建，期間或您需要 toostart 比。

4. hello tootrigger 複寫選取 VM，請按一下**啟用複寫**。

5. 您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**.

6. 在**設定** > **複寫的項目**，您可以檢視 hello 狀態的 Vm 和 hello 初始複寫正在進行。 向下一直按 hello VM toodrill，其設定。

## <a name="run-a-test-failover"></a>執行測試容錯移轉

您設定的所有項目之後，執行測試容錯移轉 toomake 確定一切如預期般運作：

1. 透過單一電腦、 toofail 中**設定** > **複寫的項目**，按一下 hello VM **+ 測試容錯移轉**圖示。

2. toofail 透過復原計劃，在**設定** > **復原計劃**，以滑鼠右鍵按一下 hello 計劃**測試容錯移轉**。 復原方案，toocreate[遵循這些指示](site-recovery-create-recovery-plans.md)。 

3. 在**測試容錯移轉**，選取 hello 容錯移轉發生後連接 hello 目標 Azure 虛擬網路 toowhich Azure Vm。

4. toostart hello 容錯移轉，請按一下**確定**。 tootrack 進度，請按一下 hello VM tooopen 其屬性。 或者您可以按一下 hello**測試容錯移轉**作業在 hello 保存庫名稱 >**設定** > **作業** > **的站台復原工作**.

5. Hello 之後容錯移轉完成時，hello 複本 Azure 的機器會出現在 hello Azure 入口網站 >**虛擬機器**。 請確定該 hello VM hello 適當的大小，它已連接 toohello 適當的網路，而且它正在執行。

6. 按一下 toodelete hello hello 測試容錯移轉期間所建立的 Vm**清除測試容錯移轉**hello 上複寫項目或 hello 復原計劃。 在**備忘稿**、 記錄及儲存與 hello 測試容錯移轉相關聯的任何觀察。 

[深入了解](site-recovery-test-failover-to-azure.md)測試容錯移轉。


## <a name="next-steps"></a>後續步驟

之後，您會測試 hello 部署：

- [進一步了解](site-recovery-failover.md)有關不同類型的容錯移轉以及 toorun 它們。
- 深入了解[使用復原計劃](site-recovery-create-recovery-plans.md)tooreduce RTO。
