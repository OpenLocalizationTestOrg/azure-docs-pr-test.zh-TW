---
title: " 刪除 Azure 中的復原服務保存庫 | Microsoft Docs "
description: "如何 toodelete Azure 備份和復原服務保存庫。 備份保存庫可稱為 Azure 雲端保存庫，或 Azure 復原保存庫。 當您無法刪除備份保存庫中 hello 傳統入口網站或 Azure 入口網站時，請疑難排解問題。"
services: service-name
documentationcenter: dev-center-name
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 5fa08157-2612-4020-bd90-f9e3c3bc1806
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: 9047f50f4b2c991fbf2454ddcad08073ec7cd975
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-recovery-services-vault"></a>刪除復原服務保存庫
hello Azure 備份服務有兩種類型的保存庫-hello 備份保存庫及 hello 復原服務保存庫。 hello 備份保存庫來自第一個項目。 然後復原服務保存庫的 hello 以往 toosupport hello 展開資源管理員部署。 因為 hello 擴充的功能和必須儲存在 hello 保存庫刪除備份或復原服務保存庫中的 hello 資訊相依性可能會造成混淆。 本文說明 toodelete hello hello 傳統入口網站和 hello Azure 入口網站中的保存庫。  

| **部署類型** | **入口網站** | **保存庫名稱** |
| --- | --- | --- |
| 傳統 |傳統 |備份保存庫 |
| Resource Manager |Azure |復原服務保存庫 |

> [!NOTE]
> 備份保存庫無法保護 Resource Manager 部署的解決方案。 不過，您可以使用 復原服務保存庫 tooprotect 原本部署伺服器和 Vm。  
>

> [!IMPORTANT]
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> **2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。 <br/> **自 2017 年 11 月 1 日起**：
>- 任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

在本文中，我們將使用 hello 詞彙、 保存庫、 toorefer toohello 一般表單的 hello 備份保存庫或復原服務保存庫。 我們使用 hello 正式名稱、 備份保存庫或復原服務保存庫時，它需要 toodistinguish hello 保存庫之間。

## <a name="deleting-a-recovery-services-vault"></a>刪除復原服務保存庫
刪除復原服務保存庫是一步驟的程序- *hello 保存庫不包含任何資源提供*。 您可以刪除復原服務保存庫之前，您必須移除或刪除 hello 保存庫中的所有資源。 如果您嘗試 toodelete 包含資源的保存庫，您會取得下列映像的 hello 類似錯誤：

![保存庫刪除錯誤](./media/backup-azure-delete-vault/vault-deletion-error.png) <br/>

您已經清除 hello hello 保存庫中的資源，直到按一下**重試**產生 hello 相同的錯誤。 如果您正在卡錯誤訊息，請按一下**取消**和使用 hello 下列步驟 toodelete hello 保存庫中的 hello 資源。

### <a name="removing-hello-items-from-a-vault-protecting-a-vm"></a>移除保護 VM 的保存庫中的 hello 項目
如果您已經有 hello 復原服務保存庫開啟時，略過 toohello 第二個步驟。

1. 開啟 hello Azure 入口網站，然後 hello 儀表板開啟您想要 toodelete hello 保存庫。

   如果您沒有復原服務保存庫的 hello 釘選 toohello 儀表板，在 [hello 中樞功能表上的，按一下**更服務**hello] 清單中的資源，在輸入**復原服務**。 當您開始輸入 hello 清單會篩選根據您的輸入。 按一下 [復原服務保存庫] 。

   ![建立復原服務保存庫的步驟 1](./media/backup-azure-delete-vault/open-recovery-services-vault.png) <br/>

   復原服務保存庫的 hello 清單隨即顯示。 從 hello 清單中，選取您想要 toodelete hello 保存庫。

   ![從清單中選擇保存庫](./media/backup-azure-work-with-vaults/choose-vault-to-delete.png)
2. 在 [hello 保存庫] 檢視中，查看在 hello **Essentials**窗格。 toodelete 保存庫中，不能有任何受保護的項目。 如果您看到的數字非零，之下**備份項目**或**備份管理伺服器**，才能刪除 hello 保存庫，您必須移除這些項目。

    ![在基本窗格中查看受保護的項目](./media/backup-azure-delete-vault/contoso-bkpvault-settings.png)

    Vm 和檔案/資料夾會被視為備份的項目，而且會列在 hello**備份項目**hello Essentials 窗格的區域。 DPM 伺服器會列在 [hello**備份管理伺服器**hello Essentials] 窗格的區域。 **複製項目**相關 toohello Azure Site Recovery 服務。
3. 從 hello 保存庫中，尋找 hello 保存庫中的 hello 項目移除 hello toobegin 受保護的項目。 Hello 保存庫儀表板中按一下**設定**，然後按一下**備份項目**tooopen 該刀鋒視窗。

    ![從清單中選擇保存庫](./media/backup-azure-delete-vault/open-settings-and-backup-items.png)

    hello**備份項目**分頁有個別的清單，根據 hello 項目類型： Azure 虛擬機器或檔案資料夾 （請參閱映像）。 hello 預設項目類型清單中所示為 Azure 虛擬機器。 檔案資料夾中的項目 hello 保存庫中，選取 tooview hello 清單**檔案資料夾**從 hello 下拉式選單。
4. 您可以保護 VM 的 hello 保存庫中刪除項目之前，您必須停止 hello 項目的備份工作，並刪除 hello 復原點的資料。 Hello 保存庫中的每個項目，請遵循下列步驟：

    a. 在 hello**備份項目**刀鋒視窗中，以滑鼠右鍵按一下 hello 項目，並從 hello 內容功能表中，選取**停止備份**。

    ![停止 hello 備份工作](./media/backup-azure-delete-vault/stop-the-backup-process.png)

    hello 停止備份 刀鋒視窗隨即開啟。

    b. 在 hello**停止備份**刀鋒視窗中的，從 hello**選擇選項**功能表上，選取**刪除備份資料**> hello 項目的型別 hello 名稱 > 按一下**停止備份**。

    型別 hello 名稱 hello 項目，您想要 toodelete tooverify 它。 hello**停止備份**確認 hello 項目之後，就會啟動按鈕。 如果看不到 hello 對話方塊方塊 tootype hello hello 備份項目名稱，您會選擇 hello**保留備份資料**選項。

    ![刪除備份資料](./media/backup-azure-delete-vault/stop-backup-blade-delete-backup-data.png)

    （選擇性） 您可以提供的原因為何會刪除 hello 資料，並加入註解。 按一下 之後**停止備份**，然後再嘗試 toodelete hello 保存庫允許 hello delete 作業 toocomplete。 tooverify 的 hello 作業已完成，請檢查 hello Azure 訊息![刪除備份資料](./media/backup-azure-delete-vault/messages.png)。 <br/>
    Hello 作業完成之後，您會收到訊息，表示 hello 備份程序已停止且 hello 備份資料，該項目，已刪除。

    c. 刪除在 hello hello 清單中的項目之後**備份項目**功能表上，按一下 **重新整理**toosee hello 剩餘 hello 保存庫中的項目。

      ![刪除備份資料](./media/backup-azure-delete-vault/empty-items-list.png)

      當 hello 清單中有任何項目時，捲動 toohello **Essentials** hello 備份保存庫刀鋒視窗中的窗格。 清單中不應該有任何 [備份項目]、[備份管理伺服器] 或 [複寫的項目]。 如果項目仍然顯示 hello 保存庫中，傳回 toostep 三，然後選擇另一個項目型別清單。  
5. 當 hello 保存庫工具列中沒有項目，請按一下**刪除**。

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-vault.png)
6. 按一下您想 toodelete hello 保存庫，tooverify**是**。

    就 hello 保存庫刪除並 hello 入口網站傳回 toohello**新增**服務功能表。

## <a name="what-if-i-stopped-hello-backup-process-but-retained-hello-data"></a>如果停止 hello 備份程序，而保留的 hello 資料，該怎麼辦？
如果您停止 hello 備份程序，但是不小心*保留*hello 資料，您必須刪除 hello 備份資料，才能刪除 hello 保存庫。 toodelete hello 備份資料：

1. 在 hello**備份項目**刀鋒視窗中，以滑鼠右鍵按一下 hello 項目，並且 hello 操作功能表上按一下**刪除備份資料**。

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-backup-data-menu.png)

    hello**刪除備份資料**刀鋒視窗隨即開啟。
2. 在 hello**刪除備份資料**刀鋒視窗中，輸入 hello 名稱 hello 項目，然後按一下**刪除**。

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-retained-vault.png)

    一旦您已刪除 hello 資料，傳回 toostep 4c 並繼續執行 hello 程序。

## <a name="delete-a-vault-used-tooprotect-a-dpm-server"></a>刪除保存庫使用 tooprotect DPM 伺服器
您可以刪除保存庫使用 tooprotect DPM 伺服器之前，您必須清除任何已建立的復原點，然後取消註冊 hello hello 保存庫中的伺服器。

保護群組相關聯的 toodelete hello 資料：

1. 在 hello DPM 系統管理員主控台中，按一下 **保護**> 選取保護群組 > 選取 hello 保護群組成員 > 在 hello 工具功能區中，按一下**移除**。

  選取 hello 保護群組成員 tooactivate hello**移除**hello 工具功能區中的按鈕。 Hello 成員是在 hello 範例**dummyvm9**。 tooselect hello 保護群組中的多個成員按住 hello Ctrl 鍵同時按一下 hello 成員上。

    ![刪除備份資料](./media/backup-azure-delete-vault/az-portal-delete-protection-group.png)

    hello**停止保護** 對話方塊隨即開啟。
2. 在 hello**停止保護**對話方塊中，選取**刪除受保護的資料**，然後按一下**停止保護**。

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-dpm-protection-group.png)

    toodelete 保存庫，您必須清除，或刪除，hello 保存庫的受保護的資料。 根據 hello 復原點數目以及 hello 保護群組中的資料，它可能需要幾秒 tooseveral 分鐘 toodelete hello 資料。 hello**停止保護**hello 作業完成時，對話方塊會顯示 hello 狀態。

    ![刪除備份資料](./media/backup-azure-delete-vault/success-deleting-protection-group.png)
3. 對所有保護群組中的所有成員執行此程序。

    移除所有受保護的資料與保護群組。
4. 刪除所有成員從 hello 保護群組之後, 切換 toohello Azure 入口網站。 開啟 hello 保存庫儀表板，並確定沒有任何**備份項目**，**備份管理伺服器**，或**複寫項目**。 Hello 保存庫在工具列上，按一下 **刪除**。

    ![刪除備份資料](./media/backup-azure-delete-vault/delete-vault.png)

    如果沒有備份管理伺服器登錄 toohello 保存庫，您無法刪除 hello 保存庫，即使在 hello 保存庫中沒有資料。 如果您刪除 hello 與 hello 保存庫相關聯的備份管理伺服器，但沒有所列的 hello 伺服器**Essentials**  窗格中，請參閱[尋找 hello 備份管理伺服器已註冊的 toohello 保存庫](backup-azure-delete-vault.md#find-the-backup-management-servers-registered-to-the-vault).
5. 按一下您想 toodelete hello 保存庫，tooverify**是**。

    就 hello 保存庫刪除並 hello 入口網站傳回 toohello**新增**服務功能表。

## <a name="delete-a-vault-used-tooprotect-a-production-server"></a>刪除保存庫使用 tooprotect 實際執行伺服器
您可以刪除保存庫使用 tooprotect 實際執行伺服器之前，您必須先刪除或 hello 保存庫中的 hello 伺服器取消登錄。

toodelete hello 的實際執行伺服器 hello 保存庫相關聯：

1. 在 hello Azure 入口網站，開啟 hello 保存庫儀表板，然後按一下**設定** > **備份基礎結構** > **實際執行伺服器**。

    ![開啟生產伺服器刀鋒視窗](./media/backup-azure-delete-vault/delete-production-server.png)

    hello**實際執行伺服器**刀鋒視窗會開啟，並列出所有的實際執行伺服器 hello 保存庫中。

    ![生產伺服器的清單](./media/backup-azure-delete-vault/list-of-production-servers.png)
2. 在 hello**實際執行伺服器**刀鋒視窗中，以滑鼠右鍵按一下 hello 伺服器上，按一下 **刪除**。

    ![刪除生產伺服器 ](./media/backup-azure-delete-vault/delete-server-on-production-server-blade.png)

    hello**刪除**刀鋒視窗隨即開啟。

    ![刪除生產伺服器 ](./media/backup-azure-delete-vault/delete-blade.png)
3. 在 hello**刪除**刀鋒視窗中，確認 hello 伺服器名稱，然後按一下**刪除**。 您必須正確命名 hello server，tooactivate hello**刪除** 按鈕。

    一旦刪除 hello 保存庫時，您會收到訊息，指出已刪除 hello 保存庫。 刪除 hello 保存庫中的所有伺服器之後, 捲動後 toohello Essentials 窗格 hello 保存庫儀表板中。
4. 在 hello 保存庫儀表板，請確認沒有任何**備份項目**，**備份管理伺服器**，或**複寫項目**。 Hello 保存庫在工具列上，按一下 **刪除**。
5. 按一下您想 toodelete hello 保存庫，tooverify**是**。

    就 hello 保存庫刪除並 hello 入口網站傳回 toohello**新增**服務功能表。

## <a name="delete-a-backup-vault-in-classic-portal"></a>刪除傳統入口網站中的備份保存庫
hello 以下指示會刪除備份保存庫 hello 傳統入口網站中。 您可以刪除 hello 備份保存庫之前，您必須刪除 hello 的復原點，或備份的項目，然後移除 hello 註冊伺服器。 hello 已註冊的伺服器為 hello Windows 伺服器、 工作站上或已註冊的 toohello 保存庫的虛擬機器。

1. 開啟 hello[傳統入口網站](https://manage.windowsazure.com)。

2. 從 hello 清單中的備份保存庫，選取您想要 toodelete hello 保存庫。

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-open-vault.png)

    hello 保存庫儀表板隨即開啟。 查看 hello 與 hello 保存庫相關聯的 Windows 伺服器及/或 Azure 的虛擬機器的數目。 此外，看看 hello Azure 中已使用的總儲存體。 停止所有的備份工作，並刪除所有資料，然後再刪除 hello 保存庫。

3. 按一下 hello**受保護項目**索引標籤，然後再按一下**停止保護**

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-stop-protect.png)

    hello**停止保護 '您的保存庫'**對話方塊隨即出現。
4. 在 hello**停止保護 '您的保存庫'**  對話方塊中，核取**刪除相關聯的備份資料**按一下![核取記號](./media/backup-azure-delete-vault/checkmark.png)。 <br/>
    或者，您可以選擇停止保護的原因，並提供註解。

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-verify-stop-protect.png)

    在刪除之後 hello hello 保存庫中的項目，hello 保存庫是空的。

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-post-delete-data.png)
5. 在 hello 索引標籤的清單中，按一下 **註冊的項目**。 hello**類型**下拉式選單，可讓您 toochoose hello 類型的已註冊的伺服器 toohello 保存庫。 hello 類型可以是 Windows Server 或 Azure 虛擬機器。 在下列範例的 hello，選取 hello 虛擬機器已註冊的 toohello 保存庫，然後按一下**取消註冊**。

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-unregister.png)

  如果您想 toodelete hello 註冊的 Windows 伺服器，從 hello**類型**下拉式選單中，選取**Windows Server**，按一下 ![核取記號](./media/backup-azure-delete-vault/checkmark.png)toorefresh 囉 」 畫面，然後按一下**刪除**。 <br/>

  ![選取 Windows Server](./media/backup-azure-delete-vault/select-windows-server.png)

6. 在 hello 索引標籤的清單中，按一下 **儀表板**tooopen 的索引標籤。請確認沒有任何已註冊的伺服器或 Azure hello 雲端中受保護的虛擬機器。 此外，也確認儲存體中沒有資料。 按一下**刪除**toodelete hello 保存庫。

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-list-of-tabs-dashboard.png)

    hello 刪除備份保存庫確認畫面隨即開啟。 選取的選項為何，您要刪除 hello 保存庫，然後按一下 ![勾選記號](./media/backup-azure-delete-vault/checkmark.png)。 <br/>

    ![刪除備份資料](./media/backup-azure-delete-vault/classic-portal-delete-vault-confirmation-1.png)

    就 hello 保存庫刪除，並傳回 toohello 傳統的入口網站儀表板。

### <a name="find-hello-backup-management-servers-registered-toohello-vault"></a>尋找 hello 備份管理伺服器已註冊的 toohello 保存庫
如果您有多個已註冊的伺服器 tooa 保存庫時，可能很難 tooremember 它們。 toosee hello 伺服器註冊 toohello 保存庫，並加以刪除：

1. 開啟 hello 保存庫儀表板。
2. 在 hello **Essentials**  窗格中，按一下 **設定**tooopen 該刀鋒視窗。

    ![開啟設定刀鋒視窗](./media/backup-azure-delete-vault/backup-vault-click-settings.png)
3. 在 hello**設定 刀鋒視窗**，按一下 **備份基礎結構**。
4. 在 hello**備份基礎結構**刀鋒視窗中，按一下 **備份管理伺服器**。 hello 備份管理伺服器刀鋒視窗隨即開啟。

    ![備份管理伺服器的清單](./media/backup-azure-delete-vault/list-of-backup-management-servers.png)
5. toodelete hello 清單中，從伺服器 hello hello 伺服器名稱上按一下滑鼠右鍵，然後按一下**刪除**。
    hello**刪除**刀鋒視窗隨即開啟。
6. 在 hello**刪除**刀鋒視窗中，提供 hello hello 伺服器名稱。 如果是完整名稱，您可以複製並貼上 hello 備份管理伺服器清單。 然後按一下 [刪除] 。  
