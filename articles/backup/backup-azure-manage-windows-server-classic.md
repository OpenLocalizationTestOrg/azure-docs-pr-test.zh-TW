---
title: "aaaManage Azure 備份保存庫與伺服器 Azure 使用 hello 傳統部署模型 |Microsoft 文件"
description: "使用此教學課程 toolearn toomanage Azure Backup 的保存庫和伺服器。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>管理 Azure 備份保存庫使用和伺服器 hello 傳統部署模型
> [!div class="op_single_selector"]
> * [資源管理員](backup-azure-manage-windows-server.md)
> * [傳統](backup-azure-manage-windows-server-classic.md)
>
>

在本文中，您會發現 hello 備份管理工作可透過 hello Azure 傳統入口網站和 hello Microsoft Azure 備份代理程式的概觀。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

> [!IMPORTANT]
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> 2017 年 10 月 15 之後，您無法使用 PowerShell toocreate 備份保存庫。 **在 2017 年 11 月 1 日以前**：
>- 所有剩餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

## <a name="management-portal-tasks"></a>管理入口網站工作
1. 登入 toohello[管理入口網站](https://manage.windowsazure.com)。
2. 按一下**復原服務**，然後按一下 [備份保存庫 tooview hello 快速入門] 頁面的 hello 名稱。

    ![復原服務](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

藉由選取 hello 選項在 hello hello 快速入門 頁面的頂端，您可以看到 hello 可用的管理工作。

![管理索引標籤](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>儀表板
選取**儀表板**hello 伺服器 toosee hello 使用量概觀。 hello**使用量概觀**包括：

* 已登錄的 Windows 伺服器的 hello 數 toocloud
* Azure 雲端中受保護的虛擬機器的 hello 數目
* hello Azure 中已使用的總儲存體
* hello 的最近工作的狀態

在 hello hello 儀表板底部，您可以執行下列工作的 hello:

* **管理憑證**-如果憑證是使用的 tooregister hello 伺服器，請使用此 tooupdate hello 憑證。 如果使用保存庫認證，則請勿使用 [管理憑證] 。
* **刪除**-刪除 hello 目前備份保存庫。 如果不再使用備份保存庫，您可以刪除它 toofree 出儲存空間。 **刪除**hello 保存庫中刪除所有已註冊的伺服器之後，才會啟用。

![備份儀表板工作](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>已註冊的項目
選取**註冊的項目**tooview hello hello 的伺服器名稱註冊 toothis 保存庫。

![已註冊的項目](./media/backup-azure-manage-windows-server-classic/registered-items.png)

hello**類型**篩選器預設 tooAzure 虛擬機器。 tooview hello 名稱 hello 伺服器的已註冊的 toothis 保存庫中，選取**Windows server** hello 從下拉功能表。

從這裡您可以執行下列工作的 hello:

* **允許重新註冊**-時選取此選項的伺服器，您可以使用 hello**登錄精靈**hello 在內部部署 Microsoft Azure 備份代理程式 tooregister hello 伺服器 hello 備份保存庫第二個階段中. 您可能需要由於 hello 憑證或伺服器是否有 toobe 重建 tooan 錯誤 toore 暫存器。
* **刪除**-從 hello 備份保存庫刪除伺服器。 所有儲存的 hello hello 伺服器相關聯的資料會立即刪除。

    ![已註冊的項目工作](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>受保護項目
選取**受保護項目**tooview hello 項目從 hello 伺服器備份。

![受保護項目](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>設定
從 hello**設定** 索引標籤，您可以選取 hello 適當的儲存體備援選項。 建立保存庫之後，權限，而之前的任何機器註冊的 tooit hello 最佳時間 tooselect hello 儲存體備援選項。

> [!WARNING]
> 一旦項目已註冊的 toohello 保存庫，hello 儲存體備援選項已鎖定且無法修改。
>
>

![設定](./media/backup-azure-manage-windows-server-classic/configure.png)

如需 [儲存體備援](../storage/common/storage-redundancy.md)的詳細資訊，請參閱這篇文章。

## <a name="microsoft-azure-backup-agent-tasks"></a>Microsoft Azure 備份代理程式工作
### <a name="console"></a>主控台
開啟 hello **Microsoft Azure 備份代理程式**(您可以藉由搜尋電腦上找到它*Microsoft Azure 備份*)。

![備份代理程式](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

從 hello**動作**位於 hello hello 備份代理程式 」 主控台的權限可以執行下列管理工作的 hello:

* 註冊伺服器
* 排程備份
* 立即備份
* 變更屬性

![代理程式主控台動作](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> 太**復原資料**，請參閱[還原檔案 tooa Windows server 或 Windows 用戶端電腦](backup-azure-restore-windows-server.md)。
>
>

### <a name="modify-an-existing-backup"></a>修改現有備份
1. Hello Microsoft Azure Backup agent 中按一下**排程備份**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. 在 [hello**排程備份精靈**保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步]**。

    ![修改排定的備份](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. 如果您想 tooadd 或變更項目，在 hello**選取項目 tooBackup**畫面上，按一下**新增的項目**。

    您也可以設定**排除設定**在 hello 精靈的這個頁面。 如果您想要 tooexclude 檔案或檔案類型讀取 hello 加入程序[排除設定](#exclusion-settings)。
4. 選取 hello 檔案和資料夾，您想 tooback 和按一下**好**。

    ![新增項目](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. 指定 hello**備份排程**按一下**下一步**。

    您可以排程每日 (一天最多 3 次) 或每週備份。

    ![指定備份排程](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > 指定 hello 備份排程中會詳細說明此[文章](backup-azure-backup-cloud-as-tape.md)。
   >
   >
6. 選取 hello**保留原則**hello 備份複本，然後按一下**下一步**。

    ![選取保留原則](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. 在 hello**確認**畫面檢閱 hello 資訊，然後按一下**完成**。
8. 一旦 hello 精靈可讓您完成建立 hello**備份排程**，按一下 **關閉**。

    之後修改的保護，您可以確認備份正確的觸發移 toohello 由**作業** 索引標籤，並確認變更會反映在 hello 備份作業。

### <a name="enable-network-throttling"></a>啟用網路節流
hello Azure 備份代理程式提供節流索引標籤可讓您 toocontrol 資料傳輸期間的網路頻寬使用方式。 如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。 節流的資料傳輸 tooback 套用設定，並還原活動。  

tooenable 節流：

1. 在 hello **Backup agent**，按一下 **變更屬性**。
2. 選取 hello**啟用網際網路頻寬使用節流設定的備份操作**核取方塊。

    ![網路節流](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. 一旦您已啟用節流設定，指定允許頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。

    hello 頻寬值 512 kb/秒 (Kbps) 為開頭，而且可以向上 too1023 mb / 秒 (Mbps)。 您可以指定 hello 開始和完成**上班**，而 hello 一週的哪幾天會被視為工作天。 指定工作時數的 hello 之外的 hello 時間是視為的 toobe 非工作小時。
4. 按一下 [確定] 。

## <a name="exclusion-settings"></a>排除設定
1. 開啟 hello **Microsoft Azure 備份代理程式**(您可以藉由搜尋電腦上找到它*Microsoft Azure 備份*)。

    ![開啟備份代理程式](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. Hello Microsoft Azure Backup agent 中按一下**排程備份**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. 在 排程備份精靈 hello 保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步**。

    ![修改排程](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. 按一下 [排除設定] 。

    ![選取項目 tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. 按一下 [新增排除] 。

    ![新增排除項目](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. 選取 hello 位置，然後按一下 **確定**。

    ![選取要排除的位置](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Hello 檔案延伸模組增益集 hello**檔案類型**欄位。

    ![依檔案類型排除](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    新增 .mp3 副檔名

    ![檔案類型範例](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd 另一個延伸模組中，按一下**新增排除**，然後輸入另一個檔案類型副檔名 （新增.jpeg 副檔名）。

    ![另一個檔案類型範例](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. 當您新增所有 hello 擴充功能之後時，按一下**確定**。
9. 繼續透過 hello 排程備份精靈]，依序按一下**下一步**直到 hello**確認頁面**，然後按一下 [**完成**。

    ![排除確認](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>後續步驟
* [從 Azure 還原 Windows Server 或 Windows 用戶端](backup-azure-restore-windows-server.md)
* toolearn 進一步了解 Azure 備份，請參閱[Azure 備份概觀](backup-introduction-to-azure-backup.md)
* 請瀏覽 hello [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)
