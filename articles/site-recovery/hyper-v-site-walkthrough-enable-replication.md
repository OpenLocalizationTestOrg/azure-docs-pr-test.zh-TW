---
title: "HYPER-V Vm 複寫 tooAzure （不含 System Center VMM) 與 Azure Site Recovery 的 aaaEnable 複寫 |Microsoft 文件"
description: "摘要說明您需要使用 hello Azure Site Recovery 服務的 HYPER-V Vm tooenable 複寫 tooAzure hello 步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>步驟 10： 啟用複寫功能複寫 tooAzure HYPER-V Vm


本文說明如何 tooenable 複寫在內部部署 HYPER-V 虛擬機器 （不受 System Center VMM） tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。

在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。




## <a name="before-you-start"></a>開始之前

在開始之前，請確定您的 Azure 使用者帳戶具有所需的 hello[權限](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)新的虛擬機器 tooAzure tooenable 複寫。

## <a name="exclude-disks-from-replication"></a>從複寫排除磁碟

依預設會複寫電腦上的所有磁碟。 您可以從複寫排除磁碟。 例如您可能不想 tooreplicate 磁碟具有暫存資料或重新整理每次在電腦的資料或應用程式重新啟動 （例如 pagefile.sys 或 SQL Server tempdb）。 [深入了解](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>複寫 VM

啟用 VM 複寫，如下所示︰          

1. 按一下 [複寫應用程式] > [來源]。 您已設定第一次的 hello 複寫之後，您可以按一下**+ 複寫**tooenable 其他機器複寫。

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. 在**來源**，選取 hello HYPER-V 站台。 然後按一下 [確定] 。
3. 在**目標**選取 hello 保存庫訂用帳戶，hello 想在容錯移轉之後 toouse Azure （classic 或資源管理） 中的容錯移轉模式。
4. 選取您想 toouse hello 儲存體帳戶。 如果您沒有您想要讓 toouse 帳戶，您可以[建立一個](#set-up-an-azure-storage-account)。 然後按一下 [確定] 。
5. 正在建立容錯移轉時，將會連接選取 hello Azure 網路和子網路 toowhich Azure Vm。

    - 選取 tooapply hello 網路設定 tooall 機器啟用複寫，**現在選取的機器設定**。
    - 選取**稍後設定**tooselect hello 每部機器的 Azure 網路。
    - 如果您沒有您想 toouse 網路，您可以[建立一個](#set-up-an-azure-network)。 選取適用的子網路。 然後按一下 [確定] 。

   ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. 在**虛擬機器** > **選取虛擬機器**，按一下並選取您想要 tooreplicate 每一部機器。 您只能選取可以啟用複寫的機器。 然後按一下 [確定] 。

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. 在**屬性** > **設定屬性**hello 作業系統選取的 hello 選取 Vm，hello 作業系統磁碟。
8. 確認該 hello Azure VM 名稱 （目標） 符合[Azure 虛擬機器需求](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)。
9. 依預設會選取所有 hello 磁碟的 hello VM，複寫。 清除磁碟 tooexclude 它們。
10. 按一下**確定**toosave 變更。 您可以稍後再設定其他屬性。

    ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. 在**複寫設定** > **設定複寫設定**，選取您想 tooapply hello 受保護 Vm 的 hello 複寫原則。 然後按一下 [確定] 。 您可以修改中的 hello 複寫原則**複寫原則**> 原則名稱 >**編輯設定**。 您套用的變更將用於已在複寫的機器和新的機器。


   ![啟用複寫](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

您可以追蹤進度的 hello**啟用保護**作業中**作業** > **站台復原工作**。 之後 hello**完成保護**作業執行 hello 機器是否已做好容錯移轉。


## <a name="next-steps"></a>後續步驟


跳過[步驟 11： 執行測試容錯移轉](hyper-v-site-walkthrough-test-failover.md)
