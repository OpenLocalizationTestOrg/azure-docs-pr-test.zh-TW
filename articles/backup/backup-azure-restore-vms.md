---
title: "從備份虛擬機器的 aaaRestore |Microsoft 文件"
description: "了解如何 toorestore Azure 虛擬機器的復原點"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "還原備份;如何 toorestore;復原點。"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>還原 Azure 中的虛擬機器
> [!div class="op_single_selector"]
> * [在 Azure 入口網站中還原 VM](backup-azure-arm-restore-vms.md)
> * [在傳統入口網站中還原 VM](backup-azure-restore-vms.md)
>
>

還原虛擬機器 tooa hello 遵循與儲存在 Azure 備份保存庫中的 hello 備份中的新 VM 的步驟。

> [!IMPORTANT]
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> **2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。 <br/> **自 2017 年 11 月 1 日起**：
>- 任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

## <a name="restore-workflow"></a>還原工作流程
### <a name="step-1-choose-an-item-toorestore"></a>步驟 1： 選擇的項目 toorestore
1. 瀏覽 toohello**受保護項目** 索引標籤，然後選取 hello 想 toorestore tooa 虛擬機器新的 VM。

    ![受保護項目](./media/backup-azure-restore-vms/protected-items.png)

    hello**復原點**hello 中的資料行**受保護項目**頁面會告訴您 hello 的虛擬機器的復原點數目。 hello **Newest 復原點**資料行告訴您 hello hello 在還原虛擬機器的最新備份的時間。
2. 按一下**還原**tooopen hello**還原的項目**精靈。

    ![還原項目](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>步驟 2：挑選復原點
1. 在 [hello**選取的復原點**] 畫面上，您可以還原從 hello 最新復原點，或從先前的點的時間。 hello 選取當精靈開啟時的預設選項是*Newest 復原點*。

    ![選取復原點](./media/backup-azure-restore-vms/select-recovery-point.png)
2. 較早的時間點 toopick 選擇 hello**選取日期**hello 下拉式清單中的選項和 hello 月曆控制項中選取日期，按一下 hello**行事曆圖示**。 Hello 控制項中所有復原點的日期會以淺灰色陰影填滿，並選取 hello 使用者。

    ![選取日期](./media/backup-azure-restore-vms/select-date.png)

    一旦您按一下 hello 月曆控制項中的日期的 hello 復原點可以使用上表的復原點中，將會顯示日期。 hello**時間**資料行會指出 hello 的 hello 在擷取快照當時的時間。 hello**類型**資料行會顯示 hello[一致性](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points)hello 復原點。 hello 資料表標頭會顯示在括號括住的那一天的 hello 可用的復原點的數目。

    ![復原點](./media/backup-azure-restore-vms/recovery-points.png)
3. 選取 hello 復原點從 hello**復原點**資料表，並按一下 hello 下一步 箭號 toogo toohello 下一個畫面。

### <a name="step-3-specify-a-destination-location"></a>步驟 3：指定目的地位置
1. 在 hello**選取還原執行個體**螢幕指定 toorestore hello 虛擬機器的位置詳細資料。

   * 指定 hello 虛擬機器名稱： 在指定的雲端服務中，hello 虛擬機器名稱應該是唯一的。 我們不支援覆寫現有的 VM。
   * 選取 hello VM 的雲端服務： 這是必要的用於建立 VM。 您可以選擇 tooeither 使用現有的雲端服務，或建立新的雲端服務。

        挑選的雲端服務名稱應具有全域唯一性。 通常，hello 雲端服務名稱會取得 [cloudservice] hello 形式公開 URL 相關聯。.cloudapp.net。 Azure 不允許您 toocreate 新的雲端服務如果 hello 名稱已經使用。 如果您選擇 toocreate 新的雲端服務，它會指定為 hello 虛擬機器 – 在哪一個案例的 hello VM 名稱相同的 hello 挑選的名稱應該是唯一不足，無法套用的 toobe toohello 相關聯雲端服務。

        我們只會顯示雲端服務和虛擬網路不在 hello 任何同質群組相關聯的還原執行個體詳細資料。 [深入了解](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。
2. 選取 hello VM 的存放裝置帳戶： 這是必要的建立 hello VM。 您可以選擇從現有的儲存體帳戶 hello 相同 hello Azure 備份保存庫與區域。 我們不支援區域備援或進階儲存體類型的儲存體帳戶。

    如果有任何儲存體帳戶，以支援的組態，請建立儲存體帳戶的支援的設定先前 toostarting 還原作業。

    ![選取虛擬網路](./media/backup-azure-restore-vms/restore-sa.png)
3. 選取虛擬網路： hello 虛擬網路 (VNET) 的 hello 虛擬機器應建立的 hello 次選取 hello VM。 hello 還原 UI 會顯示可以使用此訂用帳戶內的所有 hello Vnet。 不是強制性 tooselect VNET 的 hello 還原 VM – 您可以 tooconnect toohello 還原虛擬機器可透過 hello 網際網路即使 hello VNET 不會套用。

    如果 hello 雲端服務選取是相關聯的虛擬網路，您無法變更 hello 虛擬網路。

    ![選取虛擬網路](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. 選取子網路： hello VNET 有子網路，以免預設 hello 第一個子網路會選取。 從 hello 下拉式清單選項中選擇您所選擇的 hello 子網路。 子網路的詳細資訊，請在 hello tooNetworks 延伸模組[入口網站首頁](https://manage.windowsazure.com/)，跳過**虛擬網路**選取 hello 虛擬網路和向下切入至 設定 toosee 子網路的詳細資料。

    ![選取子網路](./media/backup-azure-restore-vms/select-subnet.png)
5. 按一下 hello**送出**圖示 hello 精靈 toosubmit hello 詳細資料，並建立還原工作。

## <a name="track-hello-restore-operation"></a>追蹤 hello 還原作業
一旦您已輸入到 hello 還原精靈的所有 hello 資訊並將它提交 Azure 備份將會嘗試 toocreate 作業 tootrack hello 還原作業。

![正在建立還原工作](./media/backup-azure-restore-vms/create-restore-job.png)

如果建立 hello 工作成功時，您會看到快顯通知，表示該 hello 作業已建立。 您可以取得更多詳細資料，只要按一下 hello**檢視工作**按鈕會引導您太**作業** 索引標籤。

![已建立還原工作](./media/backup-azure-restore-vms/restore-job-created.png)

在 hello 還原作業完成時，它將會標示為已完成在**作業** 索引標籤。

![已完成還原工作](./media/backup-azure-restore-vms/restore-job-complete.png)

還原 hello 您可能需要 toore 安裝 hello 擴充功能上的現有虛擬機器之後 hello 原始 VM 和[修改 hello 端點](../virtual-machines/windows/classic/setup-endpoints.md)hello hello Azure 入口網站中的虛擬機器。

## <a name="post-restore-steps"></a>還原後的步驟
如果您使用 cloud-init 型 Linux 散發套件 (例如 Ubuntu)，為求安全，還原後將會封鎖密碼。 請使用 VMAccess 擴充功能上 hello 還原 VM 太[重設 hello 密碼](../virtual-machines/linux/classic/reset-access.md)。 我們建議使用重設密碼後還原這些散發 tooavoid 上的 SSH 金鑰。

## <a name="backup-for-restored-vms"></a>備份還原 VM
如果您已還原為原始備份 VM 名稱相同的 hello 與 VM toosame 雲端服務，VM 後還原 hello 會繼續備份。 如果您有還原 VM tooa 不同雲端服務，或指定不同的名稱還原的 VM，這將會被視為新的 VM，以及您還原的 VM 需要 toosetup 備份。

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>在 Azure 資料中心發生災害時還原 VM
Azure Backup 可讓以防 hello 主要資料中心 Vm 正在執行體驗災害而設定備份保存庫 toobe 異地備援，還原備份 Vm toohello 成對的資料中心。 在這種情況下，您需要 tooselect 成對的資料中心內提供的儲存體帳戶與 hello 還原程序的其餘部分會保持相同。 Azure Backup 使用從配對的地理 toocreate hello 還原虛擬機器的計算服務。 深入了解 [Azure 資料中心復原](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>還原網域控制站 VM
備份網域控制站 (DC) 虛擬機器是 Azure 備份支援的案例。 不過，必須小心 hello 還原程序。 hello 正確的還原程序取決於 hello hello 網域結構。 在 hello 簡單的案例中，您會有單一 DC 在單一網域。 而在生產環境的負載中，較常見的情況是您擁有單一網域且內含多個 DC，其中有些 DC 可能位於內部部署環境。 最後，您也可能擁有內含多個網域的樹系。

從 Active Directory 的觀點來看 hello Azure VM 是像現代支援的 hypervisor 上的其他 VM。 hello 與內部 hypervisor 的主要差異是，沒有任何 VM 主控台在 Azure 中可用。 在某些情況下，您必須使用主控台，例如使用裸機復原 (BMR) 類型的備份進行復原。 不過，hello 備份保存庫中的 VM 還原是完整取代用於執行 BMR。 我們也提供了 Active Directory 還原模式 (DSRM)，因此，您可以進行所有的 Active Directory 復原案例。 如需更多背景資訊，請參閱[虛擬網域控制站的備份和還原考量](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)以及[規劃 Active Directory 樹系復原](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)。

### <a name="single-dc-in-a-single-domain"></a>單一網域中的單一 DC
hello VM 可以還原 （就像任何其他 VM) 從 hello Azure 入口網站或使用 PowerShell。

### <a name="multiple-dcs-in-a-single-domain"></a>單一網域中的多個 DC
當 hello 可以達到相同的網域，透過其他 Dc hello 網路時，可以像任何 VM 還原 hello DC。 如果它是 hello hello 網域中最後一個剩餘的 DC，或執行在隔離網路中的復原時，必須遵循的樹系修復程序。

### <a name="multiple-domains-in-one-forest"></a>單一樹系中的多個網域
當 hello 可以達到相同的網域，透過其他 Dc hello 網路時，可以像任何 VM 還原 hello DC。 不過，若是其他情況，則建議進行樹系復原。

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>還原具有特殊網路組態的 VM
Azure 備份支援備份虛擬機器的以下特殊網路組態。

* 負載平衡器底下的 VM (內部與外部)
* 具有多個保留的 IP 的 VM
* 具有多個 NIC 的 VM

這些組態可在還原組態時授權以下考量項目。

> [!TIP]
> 請使用 PowerShell 還原流程 toorecreate hello 特殊的網路組態的 Vm 後還原。
>
>

### <a name="restoring-from-hello-ui"></a>還原從 hello UI:
從 UI 還原時，請 **一律選擇新的雲端服務**。 請注意，由於入口網站只使用強制參數期間還原流程，使用 UI 來還原的 Vm 將會遺失他們擁有 hello 特殊的網路組態。 也就是說，還原後的 VM 將會是一般的 VM，不具有負載平衡器組態、多個 NIC 或多個保留的 IP。

### <a name="restoring-from-powershell"></a>從 PowerShell 還原：
PowerShell 的 hello 能力 toojust 從備份還原 hello VM 磁碟，並建立 hello 虛擬機器。 在還原需要上述特殊網路組態的虛擬機器時，這很有用。

順序 toofully 重新建立 hello 還原磁碟的虛擬機器後，請遵循下列步驟：

1. 從備份保存庫使用還原 hello 磁碟[Azure 備份的 PowerShell](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. 建立 hello VM 組態所需的負載平衡器/多個 NIC 或多個保留 IP 使用 hello PowerShell 指令程式，並用它 toocreate hello VM 所需的組態。

   * 使用 [內部負載平衡器 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * 建立 VM tooconnect 太[網際網路對向負載平衡器](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * 建立具有 [多個 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * 建立具有 [多個保留的 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>後續步驟
* [錯誤疑難排解](backup-azure-vms-troubleshoot.md#restore)
* [管理虛擬機器](backup-azure-manage-vms.md)
