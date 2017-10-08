---
title: "aaaBackup] 和 [還原加密使用 Azure Backup 的 Vm"
description: "這篇文章討論關於 hello 備份和還原 Vm 經驗加密使用 Azure 磁碟加密。"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>向上 tooback 與還原加密使用 Azure 備份的虛擬機器
這篇文章討論有關步驟 toobackup 和還原虛擬機器使用 Azure Backup。 它也提供有關支援的案例、必要條件的詳細資料，以及的錯誤案例的疑難排解步驟。

## <a name="supported-scenarios"></a>支援的案例
> [!NOTE]
> * 只有 Resource Manager 部署的虛擬機器支援備份及還原加密的 VM。 傳統虛擬機器不提供支援。 <br>
> * 它支援使用 Azure 磁碟加密，此方法運用 hello 業界標準 BitLocker 功能的 Windows 和 Linux tooprovide 加密的磁碟的 DM Crypt 功能的 Windows 和 Linux 虛擬機器。 <br>
> * 只有使用「BitLocker 加密金鑰」和「金鑰加密金鑰」加密的虛擬機器才提供支援。 只使用「BitLocker 加密金鑰」加密的虛擬機器不提供支援。 <br>
>
>

## <a name="prerequisites"></a>必要條件
1. 虛擬機器已使用 [Azure 磁碟加密](../security/azure-security-disk-encryption.md)進行加密。 應使用「BitLocker 加密金鑰」和「金鑰加密金鑰」進行加密。
2. 復原服務保存庫已建立及使用設定的儲存體複寫的步驟 hello 文章中提及[準備環境以使用備份](backup-azure-arm-vms-prepare.md)。
3. Azure 備份具有[權限 tooaccess 金鑰保存庫](#provide-permissions-to-azure-backup)包含索引鍵，為機密資料加密的 Vm。

## <a name="backup-encrypted-vm"></a>備份加密的 VM
使用下列步驟 tooset 備份目標的 hello、 定義原則、 設定項目和觸發程序備份。

### <a name="configure-backup"></a>設定備份
1. 如果您已經開啟的復原服務保存庫，請繼續執行 toonext 步驟。 如果您不需要復原服務保存庫開啟之後，但在 hello hello 中樞功能表中，在 Azure 入口網站中按一下**瀏覽**。

   * 在 [hello] 清單中的資源，輸入**復原服務**。
   * 當您開始輸入 hello 清單會篩選根據您的輸入。 當您看到 [復原服務保存庫] 時，請按一下它。

      ![建立復原服務保存庫的步驟 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     復原服務保存庫 hello 清單隨即出現。 從 hello 清單的 復原服務保存庫中，選取保存庫。

     hello 選取保存庫儀表板隨即開啟。
2. 從 hello 的項目清單會出現在保存庫下，按一下 **備份**tooopen hello 備份刀鋒視窗。

      ![開啟 [備份] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup.png)
3. 在 hello 備份刀鋒視窗中，按一下 **備份目標**tooopen hello 備份目標刀鋒視窗。

      ![開啟 [案例] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. 在 hello 備份目標刀鋒視窗中，設定**您的工作負載執行**tooAzure 和**怎麼辦想 toobackup** tooVirtual 機器，然後按一下  **確定**。

   hello 備份目標刀鋒視窗關閉，並 hello 備份原則 刀鋒視窗隨即開啟。

   ![開啟 [案例] 刀鋒視窗](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Hello 備份原則 刀鋒視窗，選取您想 tooapply toohello 保存庫，然後按一下 hello 備份原則**確定**。

      ![選取備份原則](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    hello 的 hello 預設原則的詳細資料會列在 hello 詳細資料。 如果您想 toocreate 原則，請選取**新建**從 hello 下拉式選單。 一旦您按一下**確定**，hello 備份原則是 hello 保存庫相關聯。

    接下來選擇 hello Vm tooassociate hello 保存庫。
6. 選擇 hello 加密以 hello tooassociate 指定原則，按一下 虛擬機器**確定**。

      ![選取加密的 VM](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. 此頁面會顯示有關加密的相關聯的 toohello Vm 選取金鑰保存庫的訊息。 備份服務需要唯讀存取 toohello 金鑰和 hello 金鑰保存庫中的密碼。 它會使用這些權限 toobackup 金鑰和密碼，以及 hello 相關聯的 Vm。 **您必須提供權限 toobackup 服務 tooaccess 金鑰保存庫的備份 toowork**。 您可以提供使用這些權限[hello 一節所述步驟](#provide-permissions-to-azure-backup)。

      ![加密的 VM 訊息](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      既然您已定義 hello 保存庫，在 hello 備份刀鋒視窗中的所有設定都按一下 啟用在 hello hello 頁面底部的備份。 啟用備份部署 hello 原則 toohello 保存庫和 hello Vm。
8. hello 準備中的下一個階段安裝 hello VM 代理程式或進行確定 hello VM 代理程式安裝。 toodo hello 相同，請使用 hello 文章中提及的 hello 步驟[準備環境以使用備份](backup-azure-arm-vms-prepare.md)。

### <a name="triggering-backup-job"></a>觸發備份作業
使用 hello 文章中提及的 hello 步驟[備份的 Azure Vm toorecovery 服務保存庫](backup-azure-arm-vms.md)tootrigger 備份工作。

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>將啟用加密之已備份 VM 繼續備份  
如果您有已正在備份復原服務保存庫中的 Vm，並在稍後的加密已啟用，您必須針對備份 toocontinue 給予權限 toobackup 服務 tooaccess 金鑰保存庫。 您可以提供使用這些權限[hello 一節中的步驟](#provide-permissions-to-azure-backup)或使用 PowerShell 步驟中所述**啟用備份**區段[PowerShell 文件](backup-azure-vms-automation.md)。 

## <a name="provide-permissions-tooazure-backup"></a>提供的權限 tooAzure 備份
使用下列步驟 tooprovide 相關的權限 tooAzure 備份 tooaccess 金鑰保存庫的 hello 和執行備份的加密 Vm:
1. 選取 [更多服務]，然後搜尋 [金鑰保存庫]。

    ![搜尋金鑰保存庫](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. 從金鑰保存庫的 hello 清單中選取 hello 與加密的 VM，必須備份 toobe 相關聯的金鑰保存庫。

     ![選取金鑰保存庫](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. 按一下 [存取原則] 然後 [新增]。

    ![新增存取原則](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. 按一下**選取主體**和型別**備份管理服務**hello 搜尋列中。 

    ![搜尋備份服務](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. 選取 [備份管理服務]，然後按一下 [選取] 按鈕。

    ![選取備份服務](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. 在 [從範本設定] 下拉式功能表中選取 [Azure 備份]。 預先填入機碼權限中的 hello 所需權限和密碼的權限下拉式清單。 

    ![選取 Azure 備份](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. 按一下 [確定] 。 請注意「備份管理服務」會新增到 [存取原則] 刀鋒視窗中。 

    ![備份服務存取原則](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. 按一下 [儲存] 。 這可讓 hello 所需的權限 tooAzure 備份。

    ![備份服務存取原則](./media/backup-azure-vms-encryption/save-access-policy.png)

順利提供權限後，您可以繼續為已加密的 VM 啟用備份。

## <a name="restore-encrypted-vm"></a>還原已加密的 VM
toorestore 加密 VM，第一個還原的磁碟使用一個步驟中所述的章節**磁碟備份還原**中[選擇 VM 還原組態](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)。 之後，您可以使用其中一個 hello 下列選項：
* 使用所述的 hello PowerShell 步驟[從還原的硬碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate 完整 VM 從還原的磁碟。
* OR[產生做為還原的磁碟的一部分使用範本](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm)toocreate Vm 從還原的磁碟。 只可將範本用於 2017 年 4 月 26 日之後建立的復原點。

## <a name="troubleshooting-errors"></a>錯誤疑難排解
| 作業 | 錯誤詳細資料 | 解決方案 |
| --- | --- | --- |
| 備份 |驗證失敗，因為虛擬機器單獨以 BEK 進行加密。 只會對同時使用 BEK 和 KEK 加密的虛擬機器啟用備份。 |應該使用 BEK 和 KEK 來加密虛擬機器。 第一次解密 hello VM，並使用 BEK 和 KEK 將其加密。 使用 BEK 和 KEK 加密 VM 之後，啟用備份。 進一步了解如何在[解密和加密 hello VM](../security/azure-security-disk-encryption.md)  |
| 還原 |您無法還原這部已加密的 VM，因為與此 VM 相關聯的金鑰保存庫不存在。 |利用[開始使用 Azure 金鑰保存庫](../key-vault/key-vault-get-started.md)，建立金鑰保存庫。 Hello 發行項，請參閱[還原金鑰保存庫金鑰和密碼使用 Azure Backup](backup-azure-restore-key-secret.md) toorestore 金鑰和密碼是否不存在。 |
| 還原 |您無法還原這部已加密的 VM，因為與此 VM 相關聯的金鑰和密碼不存在。 |Hello 發行項，請參閱[還原金鑰保存庫金鑰和密碼使用 Azure Backup](backup-azure-restore-key-secret.md) toorestore 金鑰和密碼是否不存在。 |
| 還原 |備份服務您的訂用帳戶中沒有授權 tooaccess 資源。 |如前所述，請先使用[選擇 VM 還原組態](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration)的＜還原備份的磁碟＞一節中所述的步驟來還原磁碟。 之後，使用者 PowerShell 太[從還原的硬碟建立 VM](backup-azure-vms-automation.md#create-a-vm-from-restored-disks)。 |
|備份 | Azure 備份服務沒有足夠的權限 tooKey 保存庫適用於備份的加密虛擬機器 | 虛擬機器應該使用「BitLocker 加密金鑰」和「金鑰加密金鑰」進行加密。 之後，應該啟用備份。  備份服務應提供使用這些權限[hello 的上一節所述步驟](#provide-permissions-to-azure-backup)或使用 PowerShell 步驟所述 hello**啟用保護**hello PowerShell 區段文件，網址[虛擬機器使用 AzureRM.RecoveryServices.Backup cmdlet tooback](backup-azure-vms-automation.md#back-up-azure-vms)。 |  
