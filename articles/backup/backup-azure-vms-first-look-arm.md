---
title: "初步了解：使用復原服務保存庫保護 Azure VM | Microsoft Docs"
description: "使用復原服務保存庫保護 Azure VM。 使用資源管理員部署的 Vm、 傳統部署 Vm 和 Premium 儲存體的 Vm，加密的 Vm，Vm 上管理磁碟 tooprotect 備份您的資料。 建立和註冊復原服務保存庫。 在 Azure 中註冊 VM、建立原則和保護 VM。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>備份 Azure 虛擬機器 tooRecovery 服務保存庫
> [!div class="op_single_selector"]
> * [使用復原服務保存庫保護 VM](backup-azure-vms-first-look-arm.md)
> * [使用備份保存庫保護 VM](backup-azure-vms-first-look.md)
>
>

本教學課程會帶領您完成建立復原服務保存庫，以及備份 Azure 虛擬機器 (VM) 的 hello 步驟。 復原服務保存庫可保護︰

* Azure Resource Manager 部署的 VM
* 傳統 VM
* 標準儲存體 VM
* 進階儲存體 VM
* 在受控磁碟上執行的 VM
* 使用 Azure 磁碟加密，搭配 BEK 與 KEK 來加密的 VM
* 使用 VSS 之 Windows VM 和使用自訂快照前與快照後指令碼之 Linux VM 的應用程式一致備份

如需有關保護進階儲存體 Vm 的詳細資訊，請參閱 hello 文件，[備份和還原 Premium 儲存體 Vm](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup)。 如需受控磁碟 VM 支援的詳細資訊，請參閱[備份及還原受控磁碟上的 VM](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)。 如需有關 Linux VM 備份之前置和後置指令碼架構的詳細資訊，請參閱 [使用前置指令碼和後置指令碼的應用程式一致 Linux VM 備份] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)。

toofind 出更多有關您備份也不能請參閱[這裡](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> 本教學課程假設您的 Azure 訂用帳戶中已有 VM，並採取措施 tooallow hello 備份服務 tooaccess hello VM。
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

Hello 的虛擬機器的數目視您想 tooprotect，您就可以開始從不同的起始點。 如果您想 tooback 多個虛擬機器在一個作業中，請移至 toohello 復原服務保存庫和[起始 hello 備份工作，從 hello 保存庫儀表板](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault)。 如果您想 tooback 單一的虛擬機器，您可以起始 hello 備份作業從 VM 管理刀鋒視窗。

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>設定從 hello VM 管理刀鋒視窗的 hello 備份工作

使用 hello hello hello Azure 入口網站中虛擬機器管理刀鋒視窗中的下列步驟 tooconfigure hello 備份工作。 這些步驟不會套用 toohello hello 傳統入口網站中的虛擬機器。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 中樞功能表中，按一下 **更服務**在 hello 篩選對話方塊中，輸入**虛擬機器**。 當您輸入時，篩選 hello 的資源清單。 當您看到虛擬機器時，請選取它。

  ![在中樞功能表中，按一下 [更多服務 tooopen 文字] 對話方塊，然後輸入虛擬機器](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  中的虛擬機器 (VM) hello 訂閱 hello 清單隨即出現。

  ![Vm 的 hello 訂用帳戶中的 hello 清單隨即出現。](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. 從 hello 清單中，選取 VM tooback。

  ![Vm 的 hello 訂用帳戶中的 hello 清單隨即出現。](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  當您選取 hello VM 時，hello 清單中的虛擬機器會進入 toohello 左和 hello 虛擬機器管理刀鋒視窗，hello 虛擬機器儀表板中，開啟。 </br>
 ![VM 管理刀鋒視窗](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. 在 hello VM 管理刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。 </br>

  ![VM 管理刀鋒視窗中的備份選項](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  hello 啟用備份刀鋒視窗隨即開啟。

  ![VM 管理刀鋒視窗中的備份選項](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Hello 復原服務保存庫中，按一下 **選取現有**hello 下拉式清單中選擇 hello 保存庫。

  ![啟用備份精靈](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  如果沒有復原服務保存庫，或您想要 toouse 新的保存庫，請按一下**建立新**並提供 hello hello 新的保存庫名稱。 新的保存庫中建立 hello 相同資源群組，而且與 hello 虛擬機器相同的位置。 如果您想 toocreate 復原服務保存庫使用不同的值，請參閱 hello 一節有關太[建立復原服務保存庫](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm)。

6. 按一下 tooview hello hello 備份原則詳細資料**備份原則**。

  hello**備份原則**刀鋒視窗會開啟，並提供 hello 選取原則的 hello 詳細資料。 如果其他原則存在，請使用 hello 下拉式功能表 toochoose 不同的備份原則。 如果您想 toocreate 原則，請選取**新建**從 hello 下拉式選單。 如需定義備份原則的指示，請參閱 [定義備份原則](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)。 toosave hello 變更 toohello 備份原則，並傳回 toohello 啟用備份刀鋒視窗中，按一下**確定**。

  ![選取備份原則](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. 在 hello 啟用備份刀鋒視窗中，按一下 **啟用備份**toodeploy hello 原則。 部署的 hello 原則與 hello 保存庫和 hello 虛擬機器關聯。

  ![啟用備份按鈕](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. 您可以追蹤 hello 通知 hello 入口網站中的 hello 設定進行。 下列範例中的 hello 顯示部署的開始。

  ![啟用備份通知](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Hello 組態進度完成後，請在 hello VM 管理刀鋒視窗中，按一下**備份**tooopen hello 備份項目刀鋒視窗，然後檢視 hello 詳細資料。

  ![VM 備份項目檢視](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Hello 初始備份完成為止，**上次備份狀態**顯示為**警告 （暫止的初始備份）**。 toosee hello 下一個排程的備份工作時，就會發生，在**備份原則**按一下 hello hello 原則名稱。 hello 備份原則 刀鋒視窗隨即開啟，並顯示 hello hello 排程備份的時間。

10. toorun 備份工作並建立 hello 初始的復原點，請在 hello 備份保存庫刀鋒視窗中按一下**備份現在**。

  ![按一下 備份現在 toorun hello 初始備份](./media/backup-azure-vms-first-look-arm/backup-now.png)

  hello 立即備份 刀鋒視窗隨即開啟。

  ![顯示 hello 立即備份 刀鋒視窗](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Hello 立即備份刀鋒視窗上，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。

  ![設定 hello 最後一天 hello 備份現在會保留復原點](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  部署通知可讓您知道已觸發 hello 備份工作，而且您可以監視 hello hello 備份工作 頁面上的 hello 作業進度。

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>設定從 復原服務保存庫的 hello hello 備份工作
tooconfigure hello 備份工作，您完成下列步驟的 hello。  

1. 建立虛擬機器的復原服務保存庫。
2. 使用 hello Azure 入口網站 tooselect 案例中，設定備份原則，並找出項目 tooprotect。
3. 執行 hello 初始備份。

## <a name="create-a-recovery-services-vault-for-a-vm"></a>建立 VM 的復原服務保存庫。
復原服務保存庫是儲存所有的 hello 備份和復原點已建立一段時間的實體。 hello 復原服務保存庫也包含 hello 備份原則套用 toohello 受保護 Vm。

> [!NOTE]
> 備份 VM 是本機程序。 您無法從一個位置 tooa 復原服務保存庫，在另一個位置來備份 Vm。 因此，對於每個已備份的 Vm toobe 的 Azure 位置，至少一個復原服務保存庫必須存在於該位置。
>
>

toocreate 復原服務保存庫：

1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。
2. 在 hello 中樞功能表中，按一下 **更多服務**在 hello 篩選對話方塊類型**復原服務**。 當您輸入時，篩選 hello 的資源清單。 當您看到 復原服務保存庫 hello 清單中的時，按一下它。

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    如果 hello 訂用帳戶中沒有復原服務保存庫，則會列出 hello 保存庫。

    ![建立復原服務保存庫的步驟 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. 在 hello**復原服務保存庫**功能表上，按一下 **新增**。

    ![建立復原服務保存庫的步驟 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    hello 復原服務保存庫刀鋒視窗隨即開啟，提示您 tooprovide**名稱**，**訂用帳戶**，**資源群組**，和**位置**。

    ![建立復原服務保存庫的步驟 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. 如**名稱**，輸入好記名稱 tooidentify hello 保存庫。 hello 名稱必須 toobe 唯一 hello Azure 訂用帳戶。 輸入包含 2 到 50 個字元的名稱。 該名稱必須以字母開頭，而且只可以包含字母、數字和連字號。

5. 在 hello**訂用帳戶**區段中，使用 hello 下拉式功能表 toochoose hello Azure 訂用帳戶。 如果您使用只有一個訂用帳戶時，會出現該訂用帳戶，所以您可以跳 toohello 下一個步驟。 如果您不確定哪一個訂用帳戶 toouse，使用預設的 hello （或建議） 訂用帳戶。 只有在您的組織帳戶與多個 Azure 訂用帳戶相關聯時，才會有多個選擇。

6. 在 hello**資源群組**> 一節：

    * 選取**建立新**如果您想 toocreate 資源群組。
    或
    * 選取**使用現有**按一下 hello 下拉式功能表 toosee hello 可用的資源群組清單。

  完整資源群組的詳細資訊，請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)。

7. 按一下**位置**hello 保存庫的 tooselect hello 地理區域。 這個選擇會決定您的備份資料的傳送目標的 hello 地理區域。

  > [!IMPORTANT]
  > 如果您不確定的 hello 您 VM 所在的位置，退出 hello 保存庫建立對話方塊，並移 hello 入口網站中的虛擬機器 toohello 清單。 如果您在多個區域中有虛擬機器，請在每個區域中建立復原服務保存庫。 建立 hello 第一個位置中的 hello 保存庫，再繼續 toohello 下一個位置。 沒有任何需要 toospecify hello 使用儲存體帳戶 toostore hello 備份資料--hello 復原服務保存庫，而且 hello Azure 備份服務會自動處理 hello 儲存體。
  >

8. 在 hello hello 復原服務保存庫刀鋒視窗底部，按一下 **建立**。

    可能需要幾分鐘的時間復原服務保存庫建立 toobe hello。 監視 hello 上方右側的區域中的 hello 入口網站的 hello 狀態通知。 一旦建立您的保存庫，它會出現在 hello 清單復原服務保存庫。 在數分鐘之後﹐如果您沒有看到您的保存庫，請按一下 [重新整理]。

    ![按一下 [重新整理] 按鈕。](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    一旦您看到您的保存庫中的 復原服務保存庫的 hello 清單，您就準備好 tooset hello 儲存體備援。

既然您已建立您的保存庫，了解如何 tooset hello 儲存體複寫。

### <a name="set-storage-replication"></a>設定儲存體複寫
hello 儲存體複寫選項可讓您 toochoose 地理備援儲存體和本機備援儲存體之間。 根據預設，保存庫具有異地備援儲存體。 如果您主要的備份復原服務保存庫的 hello，保留 hello 儲存體複寫選項集 toogeo 備援儲存體。 如果您想要更便宜但不持久的選項，請選擇本地備援儲存體。 深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本機備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存選項的 hello [Azure 儲存體複寫概觀](../storage/common/storage-redundancy.md)。

tooedit hello 儲存體複寫設定：

1. 從 hello**復原服務保存庫**刀鋒視窗中，選取 hello 新的保存庫。

  ![從 hello 復原服務保存庫清單中選取 hello 新的保存庫](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  當您選取 hello 保存庫時，hello 設定 刀鋒視窗 (*hello 頂端具有 hello 保存庫名稱*) 和 hello 保存庫詳細資料 刀鋒視窗開啟。

  ![檢視新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. 在 hello 新的保存庫的設定 刀鋒視窗中，使用 hello 垂直投影片 tooscroll toohello 管理 區段中，關閉，然後按一下**備份基礎結構**。
    hello 備份基礎結構刀鋒視窗隨即開啟。
3. 在 hello 備份基礎結構刀鋒視窗中，按一下 **備份設定**tooopen hello**備份設定**刀鋒視窗。

    ![設定新的保存庫的 hello 儲存體設定](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. 選擇您的保存庫的 hello 適當的儲存體複寫選項。

    ![儲存體組態選項](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    根據預設，保存庫具有異地備援儲存體。 如果您使用 Azure 做為備份的主要儲存體端點時，繼續 toouse**異地備援**。 如果您不使用 Azure 做為備份的主要儲存體端點，然後選擇 **本機備援**，進而降低 hello Azure 儲存體成本。 在此[儲存體備援概觀](../storage/common/storage-redundancy.md)中，深入了解[異地備援](../storage/common/storage-redundancy.md#geo-redundant-storage)和[本地備援](../storage/common/storage-redundancy.md#locally-redundant-storage)儲存體選項。


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>選取備份目標、 設定原則，並定義項目 tooprotect
向保存庫註冊的 VM，之前請先執行 hello 探索程序 tooensure toohello 訂用帳戶已加入任何新虛擬機器所識別。 hello 處理序會查詢 Azure hello hello 訂用帳戶，以及其他資訊中的虛擬機器清單，例如 hello 雲端服務名稱與 hello 區域。 在 hello Azure 入口網站，案例是指 toowhat 要 tooput 到 hello 復原服務保存庫。 原則是 hello 排程的頻率如何及何時建立復原點。 原則也包括 hello hello 的復原點的保留範圍。

1. 如果您已經開啟保存庫復原服務，繼續 toostep 2。 否則，請在 [hello 中樞功能表中，按一下**更多服務**hello] 清單中的資源，在輸入**復原服務**按一下**復原服務保存庫**。

    ![建立復原服務保存庫的步驟 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    復原服務保存庫 hello 清單隨即出現。

    ![檢視的 hello 復原服務保存庫清單](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    從 hello 清單中的 復原服務保存庫，請選取保存庫 tooopen 其儀表板。

     ![開啟 [保存庫] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Hello 保存庫儀表板功能表上，按一下**備份**tooopen hello 備份刀鋒視窗。

    ![開啟 [備份] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/backup-button.png)

    hello 備份及備份目標刀鋒視窗開啟。

    ![開啟 [案例] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. 在 hello 備份目標刀鋒視窗中，從 hello**您的工作負載執行**下拉式選單中，選擇 Azure。 從 hello**您該怎麼想 toobackup**下拉式清單，請選擇虛擬機器，然後按一下**確定**。

    這些動作 hello 保存庫中註冊 hello VM 延伸模組。 hello 關閉刀鋒視窗中的備份目標和 hello**備份原則**刀鋒視窗隨即開啟。

    ![開啟 [案例] 刀鋒視窗](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. 在 hello 備份原則 刀鋒視窗，選取您想 tooapply toohello 保存庫的 hello 備份原則。

    ![選取備份原則](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    hello 的 hello 預設原則的詳細資料列在 hello 下拉式選單。 如果您想 toocreate 原則，請選取**新建**從 hello 下拉式選單。 如需定義備份原則的指示，請參閱 [定義備份原則](backup-azure-vms-first-look-arm.md#defining-a-backup-policy)。
    按一下**確定**tooassociate hello 備份原則與 hello 保存庫。

    備份原則 刀鋒視窗關閉和 hello hello**選取虛擬機器**刀鋒視窗隨即開啟。
5. 在 hello**選取虛擬機器**刀鋒視窗中，選擇將虛擬機器 tooassociate hello 以 hello 指定原則，然後按一下**確定**。

    ![選取工作負載](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    hello 選取虛擬機器會進行驗證。 如果您沒有看到 hello 虛擬機器的預期 toosee，存在於的核取 hello 相同的 Azure 位置，如 hello 復原服務保存庫。 hello 保存庫儀表板上顯示的 復原服務保存庫的 hello 的 hello 位置。

6. 既然您已經定義 hello 保存庫的所有設定在 hello 備份刀鋒視窗中，按一下**啟用備份**toodeploy hello 原則 toohello 保存庫和 hello Vm。 部署的 hello 備份原則不會建立 hello hello 虛擬機器的初始的復原點。

    ![啟用備份](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

已成功啟用 hello 備份之後，您的備份原則也會執行排程。 不過，繼續 tooinitiate hello 的第一個備份工作。

## <a name="initial-backup"></a>初始備份
一旦備份原則已部署在 hello 虛擬機器，並不表示 hello 已備份的資料。 根據預設，hello 第一個排定的備份 （如 hello 備份原則中所定義） 是 hello 初始備份。 Hello 初始備份，就會發生，直到 hello 上次備份的狀態上 hello**備份工作**刀鋒視窗中顯示為**警告 （已暫止的初始備份）**。

![待備份](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

除非您初始的備份是到期 toobegin 過期，建議您執行**立即備份**。

toorun hello 初始備份作業：

1. Hello 保存庫儀表板上按一下下的 hello 號碼**備份項目**，或按一下 hello**備份項目**磚。 <br/>
  ![設定圖示](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  hello**備份項目**刀鋒視窗隨即開啟。

  ![備份項目](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. 在 hello**備份項目**刀鋒視窗中，選取 hello 項目。

  ![設定圖示](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  hello**備份項目**清單隨即開啟。 <br/>

  ![備份作業已觸發](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. 在 hello**備份項目**清單中，按一下 hello 省略符號**...** tooopen hello 操作功能表。

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu.png)

  hello 操作功能表隨即出現。

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Hello 操作功能表上，按一下 **備份現在**。

  ![內容功能表](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  hello 立即備份 刀鋒視窗隨即開啟。

  ![顯示 hello 立即備份 刀鋒視窗](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Hello 立即備份刀鋒視窗上，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。

  ![設定 hello 最後一天 hello 備份現在會保留復原點](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  部署通知可讓您知道已觸發 hello 備份工作，而且您可以監視 hello hello 備份工作 頁面上的 hello 作業進度。 根據您的 VM hello 大小，建立 hello 初始備份可能需要一些時間。

6. hello 初始備份，hello 保存庫儀表板上，在 hello tooview 或追蹤 hello 狀態**備份工作**磚按一下**正在**。

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  hello 備份作業 刀鋒視窗隨即開啟。

  ![備份工作圖格](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  在 hello**備份作業**刀鋒視窗中，您可以查看所有工作的 hello 狀態。 請檢查 VM 的 hello 備份工作是否仍在進行中，或若它已完成。 Hello 狀態的備份工作完成時，是*已完成*。

  > [!NOTE]
  > Hello 備份作業的一部分 hello Azure 備份服務發出的命令 toohello 備份擴充功能中每個 VM tooflush 所有寫入，並採取一致的快照集。
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Hello 虛擬機器上安裝 VM 代理程式 hello
如果需要便會提供此資訊。 hello Azure VM 代理程式必須安裝在 Azure 虛擬機器以 hello 備份副檔名 toowork hello。 不過，如果您的 VM 建立從 hello Azure 組件庫，然後 hello VM 代理程式已經存在於 hello 虛擬機器。 從移轉內部部署資料中心會沒有 hello VM 代理程式安裝的 Vm。 在這種情況下，hello VM 代理程式需要安裝 toobe。 如果您有備份 hello Azure VM 的問題，確認 hello Azure VM 代理程式已正確安裝 hello 虛擬機器上 （請參閱下表中的 hello）。 如果您建立自訂的 VM，[確保 hello**安裝 hello VM 代理程式**核取方塊已選取](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)hello 虛擬機器已佈建之前。

深入了解 hello [VM 代理程式](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409)和[如何 tooinstall 它](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

下表中的 hello 提供 hello VM 代理程式用於 Windows 及 Linux Vm 的其他資訊。

| **作業** | **Windows** | **Linux** |
| --- | --- | --- |
| 安裝 VM 代理程式 hello |<li>下載並安裝 hello[代理程式 MSI 以](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 您需要系統管理員權限 toocomplete hello 安裝。 <li>[更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。 |<li> 安裝最新的 hello [Linux 代理程式](https://github.com/Azure/WALinuxAgent)從 GitHub。 您需要系統管理員權限 toocomplete hello 安裝。 <li> [更新 hello VM 屬性](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx)tooindicate hello 代理程式的安裝。 |
| 更新 hello VM 代理程式 |更新 hello VM 代理程式的很簡單，重新安裝 hello [VM 代理程式二進位檔](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409)。 <br>請確認在 hello VM 代理程式在更新時，執行任何備份作業。 |依 hello 指示[更新 hello Linux VM 代理程式](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 <br>確定沒有備份作業正在執行時 hello VM 代理程式正在更新。 |
| 正在驗證 hello VM 代理程式安裝 |<li>瀏覽 toohello *C:\WindowsAzure\Packages* hello Azure VM 中的資料夾。 <li>您應該尋找 hello WaAppAgent.exe 檔案存在。<li> 以滑鼠右鍵按一下 hello 檔案，請移過**屬性**，然後選取 hello**詳細資料**hello 產品版本 索引標籤 欄位應該是 2.6.1198.718 或更高版本。 |N/A |

### <a name="backup-extension"></a>備份擴充功能
一次 hello hello Azure 備份服務 hello 虛擬機器安裝 VM 代理程式會安裝 hello 備用分機號碼 toohello VM 代理程式。 hello Azure 備份服務順暢地升級和修補程式不需要額外的使用者介入的 hello 備用分機號碼。

hello 備份服務會安裝 hello 備用分機號碼，即使 hello VM 未執行。 執行中的 VM 提供 hello 取得應用程式一致復原點的最大的機會。 不過，hello Azure 備份服務會繼續向上 hello VM tooback 即使它已關閉，而且 hello 擴充功能無法安裝。 這種類型的備份也就是離線的 VM，並且 hello 的復原點*絕對一致*。

## <a name="troubleshooting-information"></a>疑難排解資訊
如果您有一些在這篇文章中的 hello 工作完成的問題，請參閱[疑難排解指引](backup-azure-vms-troubleshoot.md)。

## <a name="pricing"></a>價格
備份 Azure Vm 的 hello 成本根據 hello 受保護的執行個體數目。 如需受保護執行個體的定義，請參閱[什麼是受保護執行個體](backup-introduction-to-azure-backup.md#what-is-a-protected-instance)。 如需計算備份虛擬機器的 hello 成本的範例，請參閱[如何計算受保護的執行個體](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances)。 請參閱 hello Azure 備份定價頁面的相關資訊[備份定價](https://azure.microsoft.com/pricing/details/backup/)。

## <a name="questions"></a>有疑問嗎？
如果您有任何問題，或如果沒有任何功能，您想要納入，toosee[傳送意見反應](http://aka.ms/azurebackup_feedback)。
