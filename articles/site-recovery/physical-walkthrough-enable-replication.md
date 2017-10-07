---
title: "實體伺服器複寫 tooAzure 與 Azure Site Recovery 的 aaaEnable 複寫 |Microsoft 文件"
description: "摘要說明您需要 tooenable 複寫 tooAzure 對於實體伺服器，請使用 hello Azure Site Recovery 服務的 hello 步驟"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: dde4b1463023d2ccefa498f72bb51e57d60ac0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-physical-servers-tooazure"></a>步驟 10： 啟用複寫功能的實體伺服器 tooAzure


本文說明如何針對 tooenable 複寫在內部部署 Windows/Linux 實體伺服器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="before-you-start"></a>開始之前

- 伺服器必須擁有 hello[安裝行動服務元件](physical-walkthrough-install-mobility.md)。
- 如果 VM 備妥推入安裝，hello 處理序伺服器在啟用複寫時自動安裝 hello 行動服務。
- 當您啟用來複寫的電腦時，您的 Azure 使用者帳戶需要特定[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)tooensure 你可以 toouse Azure 儲存體，但建立 Azure Vm。
- 當您新增或修改伺服器的 IP 位址時，可能需要向上 too15 分鐘或更久變更 tootake 效果，以及它們 tooappear hello 入口網站中的。


## <a name="exclude-disks-from-replication"></a>從複寫排除磁碟

依預設會複寫電腦上的所有磁碟。 您可以從複寫排除磁碟。 例如您可能不想 tooreplicate 磁碟具有暫存資料或重新整理每次在電腦的資料或應用程式重新啟動 （例如 pagefile.sys 或 SQL Server tempdb）。 [深入了解](site-recovery-exclude-disk.md)

## <a name="replicate-servers"></a>複寫伺服器

1. 按一下 [步驟 2: 複寫應用程式]  >  [來源]。
2. 在**來源**，選取 hello 組態伺服器。
3. 在 [機器類型] 中，選取 [實體機器]。
4. 選取 hello 處理序伺服器。 如果您尚未建立任何額外的處理序伺服器，這會是 hello 組態伺服器。 然後按一下 [確定] 。
5. 在**目標**選取 hello 訂用帳戶，hello 想 toocreate hello 容錯移轉 Vm 的資源群組。 選擇要容錯移轉 Vm hello toouse （classic 或資源管理），Azure 中的 hello 部署模型。
6. 選取要用於複寫資料 toouse hello Azure 儲存體帳戶。 如果您不想 toouse 您已經設定的帳戶，您可以建立一個新。
7. 選取 hello **Azure 網路**和**子網路**toowhich Azure Vm 容錯移轉之後連接。 選取**現在選取的機器設定**tooapply hello 網路設定 tooall 您選取的機器進行保護。 選取**稍後設定**tooselect hello 每部機器的 Azure 網路。 如果您不想 toouse 現有網路，您可以建立一個。

    ![啟用複寫](./media/physical-walkthrough-enable-replication/targetsettings.png)

8. 在**實體機器**，按一下  **+ 實體機器**，然後輸入 hello**名稱**和**IP 位址**。 選擇 hello 作業系統要 tooreplicate 的 hello 機器。 花幾分鐘的時間之前的電腦系統會探索並 hello 清單所示。
9. 在**屬性** > **設定屬性**，選取將由 hello 處理序伺服器 tooautomatically 的 hello 帳戶 hello 機器上安裝 hello 行動服務。
10. 依預設會複寫所有磁碟。 按一下**所有磁碟**並清除您不想 tooreplicate 任何磁碟。 然後按一下 [確定] 。 您可以稍後再設定其他 VM 屬性。

    ![啟用複寫](./media/physical-walkthrough-enable-replication/enable-replication6.png)
11. 在**複寫設定** > **設定複寫設定**，確認該 hello 正確選取複寫原則。 如果您修改原則時，將變更套用的 tooreplicating 機器和 toonew 機器。
12. 啟用**多重 VM 一致性**如果 toogather 機器的複寫群組，並指定 hello 群組的名稱。 然後按一下 [確定] 。 請注意：

    * 複寫群組中的電腦會一起複寫，並且在容錯移轉時會有共用的損毀一致和應用程式一致的復原點。
    * 建議您將實體伺服器收集在一起，以便它們能夠反映您的工作負載。 啟用多重 VM 一致性可能會影響工作負載的效能，應該只用於如果機器 hello 執行相同的工作負載，且需要一致性。

13. 按一下 [啟用複寫] 。 您可以追蹤進度的 hello**啟用保護**作業中**設定** > **作業** > **站台復原作業**. 之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。

## <a name="next-steps"></a>後續步驟

跳過[步驟 11： 執行測試容錯移轉](physical-walkthrough-test-failover.md)
