---
title: "aaaManage 資源管理員部署虛擬機器備份 |Microsoft 文件"
description: "深入了解如何 toomanage 和監視資源管理員部署虛擬機器備份"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>管理 Azure 虛擬機器備份
> [!div class="op_single_selector"]
> * [管理 Azure VM 備份](backup-azure-manage-vms.md)
> * [管理傳統 VM 備份](backup-azure-manage-vms-classic.md)
>
>

這篇文章提供有關管理 VM 備份的指引，並說明可用 hello 入口網站儀表板中的 hello 備份警示資訊。 這篇文章中的 hello 指導方針適用於向復原服務保存庫 toousing Vm。 這份文件未涵蓋 hello 建立的虛擬機器，或它不會說明如何 tooprotect 虛擬機器。 保護與復原服務保存庫在 Azure 中的 Azure Resource Manager 部署 Vm 的入門，請參閱[第一印象： 備份復原服務保存庫的 Vm tooa](backup-azure-vms-first-look-arm.md)。

## <a name="manage-vaults-and-protected-virtual-machines"></a>管理保存庫與受保護的虛擬機器
Hello Azure 入口網站，在 hello 復原服務保存庫儀表板會提供存取 tooinformation 有關 hello 保存庫包括：

* hello 最新的備份快照集，這也是最新還原點 hello < b\>
* hello 備份原則 < b\>
* 所有備份快照的大小總計 <br\>
* hello 保存庫所保護的虛擬機器的數目 < b\>

許多管理工作，與虛擬機器的備份開始與 hello 儀表板中開啟 hello 保存庫。 不過，由於保存庫可能 tooview 詳細特定 VM 中，開啟多個項目 （或多個 Vm） 使用的 tooprotect hello 保存庫項目儀表板。 hello 下列程序為您示範如何 tooopen hello*保存庫儀表板*然後繼續 toohello*保存庫項目儀表板*。 指出如何 tooadd hello 保存庫和保存庫項目 toohello Azure 儀表板使用 hello 的 Pin toodashboard 命令兩個程序中有 「 提示 」。 Pin toodashboard 是一種建立快顯 toohello 保存庫或項目。 您也可以從 hello 捷徑執行常用命令。

> [!TIP]
> 如果您有多個儀表板並刀鋒視窗開啟時，使用 hello 深藍色滑動軸在 hello hello 視窗 tooslide hello 來回 Azure 儀表板底部。
>
>

![使用滑桿以完整檢視](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>開啟 復原服務保存庫 hello 儀表板中：
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在 hello 中樞功能表中，按一下 **瀏覽**hello 清單中的資源，在輸入**復原服務**。 當您開始輸入 hello 清單會篩選根據您的輸入。 按一下 [復原服務保存庫] 。

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    會顯示復原服務保存庫 hello 清單。

    ![復原服務保存庫清單 ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > 如果您釘選的保存庫 toohello Azure 儀表板，該保存庫時，立即存取開啟 hello Azure 入口網站。 toopin 保存庫 toohello 儀表板，在 hello 保存庫清單中，hello 保存庫，以滑鼠右鍵按一下並選取**Pin toodashboard**。
   >
   >
3. 從 hello 的保存庫的清單，請選取 hello 保存庫 tooopen 其儀表板。 當您選取 hello 保存庫、 hello 保存庫儀表板和 hello**設定**刀鋒視窗中開啟。 在下列映像的 hello，hello **Contoso 保存庫**儀表板會反白顯示。

    ![開啟保存庫儀表板和設定刀鋒視窗](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>開啟保存庫項目儀表板
Hello 前程序中，您會開啟 hello 保存庫儀表板。 tooopen hello 保存庫項目儀表板：

1. Hello 保存庫儀表板] 上 hello**備份項目**磚中，按一下 [ **Azure 虛擬機器**。

    ![開啟備份項目備份圖格](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    hello**備份項目**刀鋒視窗會列出 hello 最後一個備份作業每個項目。 在此範例中，有一個受此保存庫保護的虛擬機器：demovm markgal。  

    ![備份項目圖格](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > 為了方便存取，您可以釘選的保存庫項目 toohello Azure 儀表板。 保存庫中的項目，hello 保存庫項目清單中，以滑鼠右鍵按一下 hello 項目並選取 toopin **Pin toodashboard**。
   >
   >
2. 在 hello**備份項目**刀鋒視窗中，按一下 hello 項目 tooopen hello 保存庫項目的儀表板。

    ![備份項目圖格](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    hello 保存庫項目儀表板及其**設定**刀鋒視窗中開啟。

    ![搭配設定刀鋒視窗的備份項目儀表板](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    從 hello 保存庫項目儀表板，您可以完成許多金鑰管理工作，例如：

   * 變更原則或建立新的備份原則 <br\>
   * 檢視還原點並查看其一致性狀態 <br\>
   * 虛擬機器的隨選備份 <br\>
   * 停止保護虛擬機器 <br\>
   * 繼續保護虛擬機器 <br\>
   * 刪除備份資料 (或復原點) <br\>
   * [還原備份磁碟](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\>

下列程序的 hello，hello 開始點就是 hello 保存庫項目儀表板。

## <a name="manage-backup-policies"></a>管理備份原則
1. 在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **所有設定**tooopen hello**設定**刀鋒視窗。

    ![備份原則刀鋒視窗](./media/backup-azure-manage-vms/all-settings-button.png)
2. 在 hello**設定**刀鋒視窗中，按一下 **備份原則**tooopen 該刀鋒視窗。

    在 hello 刀鋒視窗中，會顯示 hello 備份頻率和保留範圍詳細資料。

    ![備份原則刀鋒視窗](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. 從 hello**選擇備份原則**功能表：

   * toochange 原則中，選取不同的原則，然後按一下**儲存**。 hello 新原則會立即套用的 toohello 保存庫。 <br\>
   * toocreate 原則，選取**新建**。

     ![虛擬機器備份](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     如需建立備份原則的指示，請參閱 [定義備份原則](backup-azure-manage-vms.md#defining-a-backup-policy)。

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> 管理備份原則，請確定 toofollow hello[最佳做法](backup-azure-vms-introduction.md#best-practices)的最佳化備份效能
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>虛擬機器的隨選備份
設定保護後，您可以執行虛擬機器的隨選備份。 Hello 初始備份暫止時，隨備份會建立的 hello 復原服務保存庫中的 hello 虛擬機器的完整複本。 如果 hello 初始備份完成時，隨備份才會傳送變更從 hello 上一個快照，toohello 復原服務保存庫。 亦即，後續備份一律是增量備份。

> [!NOTE]
> 指定備份的 hello 保留範圍是 hello hello 每日備份的點 hello 原則中所指定的保留值。 如果不選取任何每日備份點，則會使用 hello 每週備份點。
>
>

虛擬機器的 tootrigger 隨備份：

* 在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **備份現在**。

    ![立即備份按鈕](./media/backup-azure-manage-vms/backup-now-button.png)

    hello 入口網站可確保您想 toostart 視備份工作。 按一下**是**toostart hello 備份工作。

    ![立即備份按鈕](./media/backup-azure-manage-vms/backup-now-check.png)

    hello 備份建立復原點。 hello hello 復原點的保留範圍是 hello 與 hello hello 虛擬機器相關聯的原則中指定的保留範圍相同。 tootrack hello 進行 hello 保存庫儀表板中的 hello 工作按一下 hello **Backup 工作**磚。  

## <a name="stop-protecting-virtual-machines"></a>停止保護虛擬機器
如果您選擇 toostop 保護虛擬機器，您會問您是否 tooretain hello 復原點。 有兩種方式 toostop 保護的虛擬機器：

* 停止所有未來的備份作業並刪除所有復原點，或
* 停止所有未來備份工作，但保留 hello 復原點 <br/>

沒有儲存體中留下 hello 復原點的相關成本。 不過，復原點可能會留下 hello hello 好處是稍後，您可以還原 hello 虛擬機器有需要。 復原點可能會留下 hello hello 成本的相關資訊，請參閱 hello[定價詳細資料](https://azure.microsoft.com/pricing/details/backup/)。 如果您選擇 toodelete 所有復原點，您無法還原 hello 虛擬機器。

toostop 虛擬機器的保護：

1. 在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **停止備份**。

    ![停止備份按鈕](./media/backup-azure-manage-vms/stop-backup-button.png)

    hello 停止備份 刀鋒視窗隨即開啟。

    ![停止備份刀鋒視窗](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. 在 hello**停止備份**刀鋒視窗中，選擇 tooretain 或 delete hello 備份資料。 hello 資訊 方塊會提供有關您所選擇的詳細資料。

    ![停止保護](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. 如果您選擇 tooretain hello 備份資料，請略過 toostep 4。 如果您選擇 toodelete 備份資料，請確認您想 toostop hello 備份工作，並刪除 hello 的復原點類型 hello hello 項目名稱。

    ![停止驗證](./media/backup-azure-manage-vms/item-verification-box.png)

    如果您不確定的 hello 項目名稱，將滑鼠停留在 hello 驚嘆號 tooview hello 名稱。 此外，hello hello 項目名稱會低於**停止備份**在 hello hello 刀鋒視窗最上方。
4. 選擇性地提供 [原因] 或 [註解]。
5. toostop hello 備份工作 hello 目前項目，請按一下![停止備份 按鈕](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    通知訊息，可讓您知道 hello 備份工作都已停止。

    ![確認停止保護](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>繼續保護虛擬機器
如果 hello**保留備份資料**選項選擇 hello 虛擬機器的保護已停止時，就可能 tooresume 保護。 如果 hello**刪除備份資料**選擇選項，則無法繼續 hello 虛擬機器的保護。

tooresume hello 虛擬機器的保護

1. 在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **繼續備份**。

    ![繼續保護](./media/backup-azure-manage-vms/resume-backup-button.png)

    hello 備份原則 刀鋒視窗隨即開啟。

   > [!NOTE]
   > 當重新保護 hello 虛擬機器時，您可以選擇不同的原則，小於 hello 原則與虛擬機器已受保護一開始。
   >
   >
2. 中的 hello 步驟[管理備份原則](backup-azure-manage-vms.md#manage-backup-policies)tooassign hello 原則 hello 虛擬機器。

    一旦 hello 備份原則套用的 toohello 虛擬機器，您會看到下列訊息的 hello。

    ![已成功保護 VM](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>刪除備份資料
您可以刪除 hello 期間 hello 與虛擬機器相關聯的備份資料**停止備份**作業，或每當 hello 之後備份工作已完成。 它甚至可能有幫助 toowait 天或週之前刪除 hello 復原點。 不同於還原復原點，當您刪除備份資料時，您無法選擇特定的復原點 toodelete。 如果您選擇 toodelete 備份資料，您會刪除與 hello 項目相關聯的所有復原點。

hello 下列程序假設 hello hello 虛擬機器的備份工作已停止或停用。 一旦 hello 備份工作已停用，hello**繼續備份**和**刪除備份**hello 保存庫項目儀表板中可用選項。

![繼續和刪除按鈕](./media/backup-azure-manage-vms/resume-delete-buttons.png)

toodelete hello 與虛擬機器上的備份資料*備份已停用*:

1. 在 hello[保存庫項目儀表板](backup-azure-manage-vms.md#open-a-vault-item-dashboard)，按一下 **刪除備份**。

    ![VM 類型](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    hello**刪除備份資料**刀鋒視窗隨即開啟。

    ![VM 類型](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. 型別 hello 名稱要的 hello 項目 tooconfirm toodelete hello 復原點。

    ![停止驗證](./media/backup-azure-manage-vms/item-verification-box.png)

    如果您不確定的 hello 項目名稱，將滑鼠停留在 hello 驚嘆號 tooview hello 名稱。 此外，hello hello 項目名稱會低於**刪除備份資料**在 hello hello 刀鋒視窗最上方。
3. 選擇性地提供 [原因] 或 [註解]。
4. toodelete hello 備份資料 hello 目前項目，請按一下![停止備份 按鈕](./media/backup-azure-manage-vms/delete-button.png)

    通知訊息，可讓您知道 hello 備份資料都已刪除。

## <a name="next-steps"></a>後續步驟
如需從復原點重新建立虛擬機器的詳細資訊，請參閱 [還原 Azure VM](backup-azure-restore-vms.md)。 如果您需要保護虛擬機器的詳細資訊，請參閱[第一印象： 備份復原服務保存庫的 Vm tooa](backup-azure-vms-first-look-arm.md)。 如需監視事件的相關資訊，請參閱 [監視 Azure 虛擬機器備份的警示](backup-azure-monitor-vms.md)。
