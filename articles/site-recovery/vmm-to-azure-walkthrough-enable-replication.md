---
title: "在 VMM 中的 HYPER-V Vm 的 aaaEnable 複寫 tooAzure 雲端與 Azure Site Recovery |Microsoft 文件"
description: "說明在 VMM 中的 HYPER-V Vm 的 tooenable 複寫 tooAzure 的雲端方式，與 hello Azure Site Recovery 服務"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>步驟 11： 啟用複寫 tooAzure 的 VMM 雲端中的 HYPER-V Vm

您已設定的複寫原則之後，請使用此發行項 tooenable 複寫在內部部署 HYPER-V 虛擬機器 (Vm) 的 System Center Virtual Machine Manager (VMM) 雲端中受管理），tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md)hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。


## <a name="before-you-start"></a>開始之前

請確定您的 Azure 帳戶具有正確的 hello[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure Vm。 [深入了解](../active-directory/role-based-access-built-in-roles.md) Azure 角色型存取控制。

## <a name="exclude-disks-from-replication"></a>從複寫排除磁碟

依預設會複寫電腦上的所有磁碟。 您可以從複寫排除磁碟。 例如您可能不想 tooreplicate 磁碟具有暫存資料或重新整理每次在電腦的資料或應用程式重新啟動 （例如 pagefile.sys 或 SQL Server tempdb）。 [深入了解](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>複寫 VM

啟用 VM 複寫，如下所示︰  

1. 按一下 [步驟 2: 複寫應用程式]  >  [來源]。 您已啟用複寫 hello 第一次之後，請按一下**+ 複寫**中的其他機器 hello 保存庫 tooenable 複寫。

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. 在 hello**來源**刀鋒視窗中，選取 hello VMM 伺服器和 hello 雲端中的 hello HYPER-V 主機位於。 然後按一下 [確定] 。

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. 在**目標**、 選取 hello 訂用帳戶，容錯移轉後的部署模型，以及 hello 您所使用的複寫資料的儲存體帳戶。

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. 選取您想 toouse hello 儲存體帳戶。 如果您想 toouse 您有不同的儲存體帳戶以外，您可以[建立一個](#set-up-an-azure-storage-account)。 如果您使用進階儲存體帳戶複寫資料，您需要 tooselect 額外標準儲存體帳戶 toostore 複寫記錄檔擷取進行中的變更 tooon 內部 data.toocreate 使用 hello 資源管理員模型的儲存體帳戶按一下**建立新**。 如果您想 toocreate 使用 hello 傳統模型的儲存體帳戶，這樣做， [hello Azure 入口網站中](../storage/common/storage-create-storage-account.md)。 然後按一下 [確定] 。
5. 在建立時即容錯移轉之後，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。 選取**現在選取的機器設定**，tooapply hello 網路設定 tooall 您選取的機器進行保護。 選取**稍後設定**，tooselect hello 每部機器的 Azure 網路。 如果您想 toouse 與您有不同的網路，您可以[建立一個](#set-up-an-azure-network)。 網路使用 toocreate hello 資源管理員模型中，按一下**建立新**。 如果您想 toocreate 網路使用 hello 傳統模式，這樣做， [hello Azure 入口網站中](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。 選取適用的子網路。 然後按一下 [確定] 。
6. 在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。 您只能選取可以啟用複寫的機器。 然後按一下 [確定] 。

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. 在**屬性** > **設定屬性**hello 作業系統選取的 hello 選取 Vm，hello 作業系統磁碟。

    - 確認該 hello Azure VM 名稱 （目標） 符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。   
    - 根據預設，所有 hello 磁碟的 hello VM 都選取複寫，但是您可以清除磁碟 tooexclude 它們。

        - 您可能想 tooexclude 磁碟 tooreduce 複寫的頻寬。 例如，您可能不想 tooreplicate 磁碟取代為暫存資料，或重新整理每次在電腦或應用程式的資料會重新啟動 （例如 pagefile.sys 或 Microsoft SQL Server tempdb）。 您可以取消選取 hello 磁碟從複寫排除 hello 磁碟。
        - 只有基本磁碟可以排除。 您無法排除作業系統磁碟。
        - 我們建議不要排除動態磁碟。 Site Recovery 無法識別客體 VM 內的虛擬硬碟為基本還是動態磁碟。 如果所有相依的動態磁碟區磁碟不排除，hello 受保護的動態磁碟會顯示失敗的磁碟時 hello VM 容錯移轉，而且您無法存取該磁碟上的 hello 資料。
        - 啟用複寫後，您無法加入或移除複寫的磁碟。 如果您想 tooadd 或排除磁碟，您需要 toodisable 保護 hello VM，並重新啟用它。
        - 您以手動方式在 Azure 中建立的磁碟將不會容錯回復。 比方說，如果您無法超過三個磁碟，並建立兩個直接在 Azure VM 中，只有 hello 三個磁碟已容錯移轉將無法從 Azure tooHyper-V。 您不能包含在容錯回復，或從 HYPER-V tooAzure 的反向複寫以手動方式建立的磁碟。
        - 如果您排除的應用程式 toooperate 所需的磁碟，在容錯移轉 tooAzure 之後您需要的 toocreate 它以手動方式在 Azure 中，因此該 hello 複寫應用程式可以執行。 或者，您無法將 Azure 自動化整合至復原計劃，hello 機器容錯移轉期間 toocreate hello 磁碟。

    按一下**確定**toosave 變更。 您可以稍後再設定其他屬性。

    ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. 在**複寫設定** > **設定複寫設定**，選取您想 tooapply hello 受保護 Vm 的 hello 複寫原則。 然後按一下 [確定] 。 您可以修改中的 hello 複寫原則**複寫原則**> 原則名稱 >**編輯設定**。 您套用的變更用於已在複寫的機器和新的機器。

   ![啟用複寫](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

您可以追蹤進度的 hello**啟用保護**作業中**作業** > **站台復原工作**。 之後 hello**完成保護**作業會執行，hello 機器是否已做好容錯移轉。



## <a name="next-steps"></a>後續步驟

跳過[步驟 12： 執行測試容錯移轉](vmm-to-azure-walkthrough-test-failover.md)
