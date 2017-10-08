---
title: "Azure 備份： 還原虛擬機器使用 hello Azure 入口網站 |Microsoft 文件"
description: "使用 Azure 入口網站從復原點還原 Azure 虛擬機器"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "還原備份;如何 toorestore;復原點。"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>使用 Azure 入口網站 toorestore 虛擬機器
> [!div class="op_single_selector"]
> * [在傳統入口網站中還原 VM](backup-azure-restore-vms.md)
> * [在 Azure 入口網站中還原 VM](backup-azure-arm-restore-vms.md)
>
>

於定義的間隔進行資料快照，來保護您的資料。 這些快照稱為復原點，而且儲存在復原服務保存庫中。 如果或必要 toorepair 或重新建立 VM 時，您可以從任何 hello 儲存復原點還原 hello VM。 當您還原的復原點時，您可以建立新的 VM，也就是您的備份 VM 的時間點表示法或還原磁碟，並使用它隨附 hello 範本 toocustomize hello 還原 VM，或執行個別的檔案復原。 這篇文章說明如何 toorestore VM tooa 新的 VM 或還原所有備份的磁碟。 個別檔案的修復，請參閱太[從 Azure VM 的備份復原檔案](backup-azure-restore-files-from-vm.md)

![從 VM 備份還原的 3 種方法](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure 有兩種用來建立和使用資源的部署模型： [Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文章提供 hello 資訊和程序來還原使用 hello 資源管理員的模型部署的 Vm。
>
>

從 VM 備份還原一個 VM 或所有磁碟需要兩個步驟︰

1. 選取要還原的還原點
2. 選取 hello 還原類型-建立新的 VM 或還原磁碟，並指定必要的參數。 

## <a name="select-restore-point-for-restore"></a>選取要還原的還原點
1. 登入 toohello [Azure 入口網站](http://portal.azure.com/)
2. 在 hello Azure 功能表，按一下 **瀏覽**在 hello 服務清單中，輸入**復原服務**。 服務的 hello 清單調整的 toowhat 您輸入。 當您看到 [復原服務保存庫] 時，請選取它。

    ![開啟復原服務保存庫](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    保存庫 hello 訂用帳戶中的 hello 清單隨即顯示。

    ![復原服務保存庫清單](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. 從 [hello] 清單中，選取 hello 保存庫相關聯 hello 想 toorestore 的 VM。 當您按一下 hello 保存庫時，會開啟其儀表板。

    ![復原服務保存庫清單](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. 既然您 hello 保存庫儀表板中。 在 hello**備份項目**磚中，按一下  **Azure 虛擬機器**toodisplay hello Vm 與 hello 保存庫關聯。

    ![保存庫儀表板](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    hello**備份項目**刀鋒視窗會開啟並顯示 hello Azure 的虛擬機器清單。

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. 從 [hello] 清單中，選取 [VM tooopen hello 儀表板]。 hello VM 儀表板隨即開啟 toohello 監視區域中，包含 hello 還原點磚。

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Hello VM 儀表板功能表上，按一下**還原**

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    hello 還原刀鋒視窗隨即開啟。

    ![還原刀鋒視窗](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. 在 hello**還原**刀鋒視窗中，按一下 **還原點**tooopen hello**選取還原點**刀鋒視窗。

    ![還原刀鋒視窗](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    根據預設，hello 對話方塊會顯示過去 30 天內從 hello 的所有還原點。 使用 hello**篩選**hello tooalter hello 時間範圍的還原點顯示。 根據預設，系統會顯示所有一致性的還原點。 修改**所有還原點**篩選 tooselect 特定一致性還原點。 如需每種類型的還原點的詳細資訊，請參閱 hello 說明[資料一致性](backup-azure-vms-introduction.md#data-consistency)。  

   *  選擇以下清單︰
     * 當機時保持一致還原點，
     * 應用程式保持一致還原點，
     * 系統檔案保持一致還原點，
     * 所有還原點。  
8. 選擇還原點，然後按一下 [確定] 。

    ![選擇還原點](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    hello**還原**刀鋒視窗會顯示 hello 還原點設定。

    ![已設定還原點](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. 在 hello**還原**刀鋒視窗中，**還原組態**設定還原點之後自動開啟。

## <a name="choosing-a-vm-restore-configuration"></a>選擇 VM 還原組態
既然您已選取 hello 還原點，請選擇 為您還原的 VM 組態。 您的選擇設定 hello 還原 VM 是 toouse: Azure 入口網站或 PowerShell。

1. 如果您已不存在，請移至 toohello**還原**刀鋒視窗。 確保[選取 還原點](#select-restore-point-for-restore)，然後按一下**還原組態**tooopen hello**復原組態**刀鋒視窗。

    ![已設定復原組態精靈](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. 在 hello**還原組態**刀鋒視窗中，有兩個選擇：
   * 還原完整虛擬機器
   * 還原備份的磁碟

入口網站提供還原 VM 專用的「快速建立」選項。 如果您想 toocustomize hello VM 組態，或建立過程中的 hello 資源的名稱建立新的 VM 選項，使用 PowerShell 或入口網站 toorestore 備份磁碟並使用 PowerShell 命令 tooattach 它們 toochoice 的 VM 組態或使用範本，來自還原磁碟 toocustomize hello 還原 VM。 請參閱[還原具有特殊的網路組態的 VM](#restoring-vms-with-special-network-configurations)的詳細資料 toorestore 的 vm 具有多個 Nic，或在負載平衡器。 如果您的 Windows VM 使用[中樞授權](../virtual-machines/windows/hybrid-use-benefit-licensing.md)，您需要 toorestore 磁碟使用 PowerShell/範本作為下列 toocreate hello VM 指定並確定您指定 LicenseType 為"Windows_Server"在建立 VM tooavail 集線器時在還原的 VM 上的優點。 
 
## <a name="create-a-new-vm-from-restore-point"></a>從還原點建立新的 VM
如果您已不存在，請[選擇還原點](#restoring-vms-with-special-network-configurations)之前繼續 toocreating 新的 VM，從還原點。 一旦選取還原點之後，在 hello**還原組態**刀鋒視窗中，輸入或選取 hello 遵循欄位的每個值：

* **還原類型** - 建立虛擬機器。
* **虛擬機器名稱**-提供 hello VM 的名稱。 hello 名稱必須是唯一的 toohello （針對資源管理員部署的 VM) 的資源群組或雲端服務 （適用於傳統的 VM)。 如果已經存在 hello 訂用帳戶中，您不能取代 hello 虛擬機器。
* **資源群組** - 使用現有資源群組，或建立新的群組。 如果您要還原傳統 VM，使用此欄位 toospecify hello 名稱的新的雲端服務。 如果您要建立新的資源群組/雲端服務，hello 名稱必須是全域唯一的。 一般而言，hello 雲端服務名稱是相關聯的公開 URL-例如: [cloudservice]。.cloudapp.net。 如果您嘗試 toouse hello 雲端資源群組/雲端服務名稱已在使用時，Azure 將指派 hello 資源群組/雲端服務在為 hello VM hello 相同的名稱。 Azure 會顯示未與任何同質群組相關聯的資源群組/雲端服務和 VM。 如需詳細資訊，請參閱[如何從同質群組 tooa 區域虛擬網路 (VNet) toomigrate](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。
* **虛擬網路**-選取 hello 虛擬網路 (VNET) 時建立 hello VM。 hello 欄位會提供所有 hello 訂用帳戶相關聯的 Vnet。 Hello VM 的資源群組會顯示在括號中。
* **子網路**-如果 hello VNET 子網路，預設會選取第一個子網路 hello。 如果有其他子網路，請選取所需的 hello 子網路。
* **儲存體帳戶**-這個功能表會列出 hello 儲存體帳戶的 hello hello 與相同的位置復原服務保存庫。 不支援區域備援的儲存體帳戶。 如果沒有儲存體帳戶與 hello hello 與相同的位置復原服務保存庫，您必須建立一個開始 hello 還原作業之前。 在括號中提及 hello 儲存體帳戶的複寫類型。

![已設定還原組態精靈](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. 如果您正在還原資源管理員部署的 VM，您必須識別虛擬網路 (VNET)。 針對傳統型 VM，虛擬網路 (VNET) 是選擇性的。
> 2. 如果您要還原具有受控磁碟的 VM，請確定所選取的儲存體帳戶未在其存留期內啟用儲存體服務加密 (SSE)。
> 3. 根據 hello 儲存儲存體帳戶類型選取 （高階或標準），還原的所有磁碟將會都是高階或標準磁碟。 我們目前不支援在還原時使用混合的磁碟模式。  
>
>

在 hello**還原組態**刀鋒視窗中，按一下  **確定** toofinalize hello 還原設定。 在 hello**還原**刀鋒視窗中，按一下 **還原**tootrigger hello 還原作業。

## <a name="restore-backed-up-disks"></a>還原備份的磁碟
如果您想要 toocustomize hello 虛擬機器您想要從 toocreate 備份的磁碟而中還原組態刀鋒視窗中，選取**還原磁碟**como valor para**還原類型**。 此選擇需要儲存體帳戶，以存放從備份複製的磁碟。 在選擇儲存體帳戶時，選取 共用 hello 相同的位置，如 hello 復原服務保存庫的帳戶。 不支援區域備援的儲存體帳戶。 如果沒有儲存體帳戶與 hello hello 與相同的位置復原服務保存庫，您必須建立一個開始 hello 還原作業之前。 在括號中提及 hello 儲存體帳戶的複寫類型。

還原作業完成之後，您可以︰
* [使用範本 toocustomize hello 還原 VM](#use-templates-to-customize-restore-vm)
* [使用 hello 還原磁碟 tooattach tooan 現有虛擬機器](../virtual-machines/windows/attach-managed-disk-portal.md)
* [使用 PowerShell 從還原的磁碟建立新的虛擬機器。](./backup-azure-vms-automation.md#restore-an-azure-vm)

在 hello**還原組態**刀鋒視窗中，按一下  **確定** toofinalize hello 還原設定。 在 hello**還原**刀鋒視窗中，按一下 **還原**tootrigger hello 還原作業。

![已完成復原設定](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>追蹤 hello 還原作業
一旦觸發 hello 還原作業時，hello 備份服務會建立追蹤 hello 還原作業的作業。 hello 備份服務也會建立，而且暫時的入口網站的通知區域中顯示 hello 通知。 如果看不到 hello 通知，您可以隨時按一下 hello 通知圖示 tooview 您的通知。

![已觸發還原](./media/backup-azure-arm-restore-vms/restore-notification.png)

tooview hello 作業，當它正在處理時或當它完成，tooview 開啟 hello 備份工作清單。

1. 在 hello Azure 功能表，按一下 **瀏覽**在 hello 服務清單中，輸入**復原服務**。 服務的 hello 清單調整的 toowhat 您輸入。 當您看到 [復原服務保存庫] 時，請選取它。

    ![開啟復原服務保存庫](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    保存庫 hello 訂用帳戶中的 hello 清單隨即顯示。

    ![復原服務保存庫清單](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. 從 [hello] 清單中，選取 hello 保存庫相關聯 hello 您還原的 VM。 當您按一下 hello 保存庫時，會開啟其儀表板。
3. 在 hello 保存庫儀表板上 hello**備份作業**磚中，按一下  **Azure 虛擬機器**toodisplay hello 作業 hello 保存庫相關聯。

    ![保存庫儀表板](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    hello **Backup 工作**刀鋒視窗會開啟並顯示 hello 工作清單。

    ![保存庫中的 VM 清單](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>使用範本 toocustomize 還原的 vm
一次[完成還原磁碟操作](#Track-the-restore-operation)，您可以使用產生的 hello 範本做為還原作業 toocreate 與備份設定] 或 [toocustomize 名稱不同的資源設定的新 VM 的一部分建立還原點從建立新的 vm。 

> [!NOTE]
> 對於 2017年 3 月 1 日之後建立的復原點，範本會新增為還原磁碟的一部分。 這些範本適用於非加密和非受控磁碟 VM。 即將發行的版本中支援加密的 VM 和受控磁碟 VM。 
>
>

還原磁碟選項時，產生 tooget hello 範本

1. 移 toorestore 對應 toohello 作業的工作詳細資料。 
2. 在 [hello 還原作業詳細資料] 畫面上，按一下*部署範本*按鈕 tooinitiate 範本部署。 

     ![還原作業向下鑽研](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Hello 自訂部署的部署範本刀鋒視窗，在使用範本部署太[編輯並部署 hello 範本](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template)或附加多個自訂內容[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)部署之前。 

   ![載入範本部署](./media/backup-azure-arm-restore-vms/loading-template.png)
   
輸入所需的 hello 值之後, 接受 hello*條款和條件*，然後按一下 **購買**。

   ![提交範本部署](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>還原後的步驟
* 如果您使用 cloud-init 型 Linux 散發套件 (例如 Ubuntu)，基於安全理由，還原後會封鎖密碼。 請使用 VMAccess 擴充功能上 hello 還原 VM 太[重設 hello 密碼](../virtual-machines/linux/classic/reset-access.md)。 我們建議使用重設密碼後還原這些散發 tooavoid 上的 SSH 金鑰。
* 將會安裝延伸模組 hello 備份設定期間出現，不過他們將無法使用。 如果您看到任何問題，請重新安裝擴充功能。 
* 如果 hello 備份 VM 的靜態 IP 時，post 還原，還原的 VM 會動態 IP tooavoid 衝突時建立還原 VM。 進一步了解如何在[新增靜態 IP toorestored VM](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* 還原的 VM 不會有可用性設定值組。 從 PowerShell 建立 VM 或使用還原的磁碟建立範本時，我們建議使用還原磁碟選項和[新增可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md)。 


## <a name="backup-for-restored-vms"></a>備份已還原的 VM
如果您已還原為原始備份 VM 名稱相同的 hello 與 VM toosame 資源群組，備份會繼續 hello VM 後還原。 如果您有還原 VM tooa 不同資源群組，或指定不同的名稱還原的 VM，這會被視為新的 VM，以及您還原的 VM 需要 toosetup 備份。

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>在 Azure 資料中心發生災害時還原 VM
Azure Backup 可讓以防 hello 主要資料中心 Vm 正在執行體驗災害而設定備份保存庫 toobe 異地備援，還原備份 Vm toohello 成對的資料中心。 在這種情況下，您需要 tooselect 儲存體帳戶，也就是出現在配對的資料中心與 hello 還原程序的其餘部分會保持相同。 Azure Backup 使用從配對的地理 toocreate hello 還原虛擬機器的計算服務。 深入了解 [Azure 資料中心復原](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>還原網域控制站 VM
備份網域控制站 (DC) 虛擬機器是 Azure 備份支援的案例。 不過，必須小心 hello 還原程序。 hello 正確的還原程序取決於 hello hello 網域結構。 在 hello 簡單的案例中，您會有單一 DC 在單一網域。 而在生產環境的負載中，較常見的情況是您擁有單一網域且內含多個 DC，其中有些 DC 可能位於內部部署環境。 最後，您也可能擁有內含多個網域的樹系。 

從 Active Directory 的觀點來看 hello Azure VM 是像現代支援的 hypervisor 上的其他 VM。 hello 與內部 hypervisor 的主要差異是，沒有任何 VM 主控台在 Azure 中可用。 在某些情況下，您必須使用主控台，例如使用裸機復原 (BMR) 類型的備份進行復原。 不過，hello 備份保存庫中的 VM 還原是完整取代用於執行 BMR。 我們也提供了 Active Directory 還原模式 (DSRM)，因此，您可以進行所有的 Active Directory 復原案例。 如需更多背景資訊，請參閱[虛擬網域控制站的備份和還原考量](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers)以及[規劃 Active Directory 樹系復原](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx)。

### <a name="single-dc-in-a-single-domain"></a>單一網域中的單一 DC
hello VM 可以還原 （就像任何其他 VM) 從 hello Azure 入口網站或使用 PowerShell。

### <a name="multiple-dcs-in-a-single-domain"></a>單一網域中的多個 DC
當 hello 可以達到相同的網域，透過其他 Dc hello 網路時，可以像任何 VM 還原 hello DC。 如果它是 hello hello 網域中最後一個剩餘的 DC，或執行在隔離網路中的復原時，必須遵循的樹系修復程序。

### <a name="multiple-domains-in-one-forest"></a>單一樹系中的多個網域
當 hello 可以達到相同的網域，透過其他 Dc hello 網路時，可以像任何 VM 還原 hello DC。 不過，若是其他情況，則建議進行樹系復原。

## <a name="restoring-vms-with-special-network-configurations"></a>還原具有特殊網路組態的 VM
很可能 tooback 向上並還原 Vm 與 hello 特殊的網路設定。 不過，這些設定需要一些特殊考量時經過 hello 還原程序。

* 負載平衡器底下的 VM (內部與外部)
* 具有多個保留的 IP 的 VM
* 具有多個 NIC 的 VM

> [!IMPORTANT]
> 在建立 vm 的 hello 特殊的網路設定時，您必須使用 PowerShell toocreate Vm 從 hello 磁碟還原。
>
>

toofully 重新建立 hello 虛擬機器之後還原 toodisk，請遵循下列步驟：

1. 復原服務保存庫使用還原 hello 磁碟[PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. 建立 hello VM 組態所需的負載平衡器/多個 NIC 或多個保留 IP 使用 hello PowerShell 指令程式，並用它 toocreate hello VM 所需的組態。

   * 使用 [內部負載平衡器 ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * 建立 VM tooconnect 太[網際網路對向負載平衡器](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * 建立具有 [多個 NIC](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * 建立具有 [多個保留的 IP](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>後續步驟
現在，您可以還原您的 Vm，請參閱 hello 疑難排解文件以取得 Vm 的常見錯誤的詳細資訊。 此外，簽出 hello 發行項有關管理工作與您的 Vm。

* [錯誤疑難排解](backup-azure-vms-troubleshoot.md#restore)
* [管理虛擬機器](backup-azure-manage-vms.md)
