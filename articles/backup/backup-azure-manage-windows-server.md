---
title: "aaaManage Azure 復原服務保存庫與伺服器 |Microsoft 文件"
description: "使用此教學課程 toolearn toomanage Azure 復原服務保存庫的方式和伺服器。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>監視和管理 Windows 電腦的 Azure 復原服務保存庫和伺服器
> [!div class="op_single_selector"]
> * [資源管理員](backup-azure-manage-windows-server.md)
> * [傳統](backup-azure-manage-windows-server-classic.md)
>
>

在本文中您會發現備份監視和管理工作可透過 Azure 入口網站和 hello Microsoft Azure 備份代理程式 hello hello 的概觀。 本文假設您已經有 Azure 訂用帳戶，並至少建立了一個復原服務保存庫。

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>開啟復原服務保存庫

hello 復原服務保存庫儀表板會顯示 hello 詳細資料] 或 [復原服務保存庫的屬性。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)使用您的 Azure 訂用帳戶。
2. 在 hello 中樞功能表中，按一下 **更服務**。

    ![開啟復原服務保存庫清單的步驟 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. 您想 tooopen 復原服務保存庫。 在 [hello] 對話方塊中，開始輸入**復原服務**。 當您開始輸入 hello 清單會篩選器根據您的輸入。 按一下**復原服務保存庫**toodisplay hello 清單的 復原服務保存庫中您訂用帳戶。

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    此時會開啟 復原服務保存庫的 hello 清單。

    ![建立復原服務保存庫的步驟 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. 從保存庫的 hello 清單中，選取 hello hello 想 tooopen 復原服務保存庫名稱。 hello 復原服務保存庫儀表板 刀鋒視窗隨即開啟。

    ![復原服務保存庫儀表板](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    既然您已開啟 hello 復原服務保存庫，再試一次任一 hello 監視或管理工作。

## <a name="monitor-backup-jobs-and-alerts"></a>監視備份作業和警示

監視作業，並從 hello 警示復原服務保存庫儀表板，了解：

* 備份警示詳細資料
* 檔案和資料夾，以及 Azure hello 雲端中受保護的虛擬機器
* Azure 中已使用的儲存體總計
* 備份作業狀態

![備份儀表板工作](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

按一下每個這些磚中的 hello 資訊會開啟 hello 關聯刀鋒視窗，讓您管理相關的工作。

從 hello hello 儀表板頂端：

* [設定] 可供存取可用的備份工作。
* 備份-可協助您將新的檔案和資料夾 （或 Azure Vm） toohello 復原服務保存庫。
* 不再使用 delete-如果復原服務保存庫，您可以將它刪除 toofree 出儲存空間。 Hello 保存庫中刪除所有受保護的伺服器之後，才會啟用刪除。

![備份儀表板工作](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>針對使用 Azure 備份代理程式之備份的警示：
| 警示層級 | 傳送的警示 |
| --- | --- |
| 重要 |備份失敗、復原失敗 |
| 警告 |備份 （當少於一百檔案則不會備份到期 toocorruption 問題，且超過 1 百萬個檔案已成功備份），已完成但出現警告 |
| 資訊 |None |

## <a name="manage-backup-alerts"></a>管理備份警示
按一下 hello**備份警示**磚 tooopen hello**備份警示**刀鋒視窗及管理警示。

![備份警示](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

hello 備份警示磚顯示 hello 數目：

* 過去 24 小時內未解決的重大警示
* 過去 24 小時內未解決的警告警示

按一下這些連結會帶您 toohello**備份警示**刀鋒視窗的 篩選檢視的這些警示 （重大或警告）。

Hello 備份警示刀鋒視窗中，從您：

* 選擇將適當的資訊 tooinclude hello 與您的通知。

    ![選擇資料行](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* 針對嚴重性、狀態和開始/結束時間篩選警示。

    ![篩選警示](./media/backup-azure-manage-windows-server/filter-alerts.png)
* 針對嚴重性、頻率和接收者設定通知，以及開啟或關閉警示。

    ![篩選警示](./media/backup-azure-manage-windows-server/configure-notifications.png)

如果**每個警示**當做 hello**通知**不進行任何群組或減少電子郵件的頻率。 每個警示會產生 1 則通知。 這是 hello 預設設定，而且 hello 解析電子郵件也會立即送出。

如果**每小時摘要**當做 hello**通知**傳送 toohello 使用者告訴他們有一個電子郵件的頻率無法解析產生 hello 在過去一小時內的新警示。 解析電子郵件送出 hello hello 小時結尾處。

警示可以傳送 hello 下列嚴重性層級：

* 重要
* 警告
* 資訊

以 hello hello 警示中停用**中停用**hello 工作詳細資料 刀鋒視窗中的按鈕。 當您按一下 [停用] 時，您可以提供解決方式資訊。

您選擇 hello 資料行要作為組件以 hello hello 警示的 tooappear**選擇資料行** 按鈕。

> [!NOTE]
> 從 hello**設定**刀鋒視窗中，選取 管理備份警示**監視與報表 > 警示與事件 > 備份警示**，然後按一下**篩選**或**設定通知**。
>
>

## <a name="manage-backup-items"></a>管理備份項目
管理內部部署備份現已推出 hello 管理入口網站。 在 hello 備份區段中的 hello 儀表板，hello**備份項目**磚會顯示受保護的備份項目的 hello 數目 toohello 保存庫。

按一下**檔案資料夾**hello 備份項目磚中。

![備份項目圖格](./media/backup-azure-manage-windows-server/backup-items-tile.png)

刀鋒視窗會開啟以 hello hello 備份項目來篩選，您會看到每個項目列出的特定備份組 tooFile 資料夾。

![備份項目](./media/backup-azure-manage-windows-server/backup-item-list.png)

如果您從 hello 清單中選取特定的備份項目，您會看到該項目 hello 基本詳細資料。

> [!NOTE]
> 從 hello**設定**刀鋒視窗中，您可以管理檔案和資料夾選取**受保護項目 > 備份項目**，然後選取 **檔案資料夾**hello 從下拉功能表。
>
>

![從設定備份項目](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>管理備份作業
在內部部署 （當 hello 在內部部署伺服器備份 tooAzure） 及 Azure 備份的備份工作會顯示 hello 儀表板中。

Hello hello 儀表板的 備份 區段中，在 hello 備份工作 磚會顯示 hello 作業數目：

* 進行中
* 無法在 hello 過去 24 小時。

toomanage 的備份作業中，按一下 hello**備份工作**磚，以開啟刀鋒視窗中的備份工作 hello。

![從設定備份項目](./media/backup-azure-manage-windows-server/backup-jobs.png)

修改以 hello hello Backup 工作刀鋒視窗中可用的 hello 資訊**選擇資料行**hello hello 頁頂端的按鈕。

使用 hello**篩選**按鈕 tooselect 之間的檔案和資料夾以及 Azure 虛擬機器備份。

如果您沒有看到您的備份檔案及資料夾，按一下**篩選**在 hello hello 頁面並選取最上方的按鈕**檔案和資料夾**功能表 hello 項目類型。

> [!NOTE]
> 從 hello**設定**刀鋒視窗中，您選取 管理備份工作**監視與報表 > 作業 > 備份工作**，然後選取 **檔案資料夾**從 hello 拖放關閉功能表。
>
>

## <a name="monitor-backup-usage"></a>監視備份使用量
Hello hello 儀表板的 [備份] 區段中，在 hello 備份 [使用量] 磚會顯示 hello Azure 中已使用的存放裝置。 提供下列各項的儲存體使用量︰

* Hello 保存庫相關聯的雲端 LRS 儲存體使用量
* 雲端 GRS hello 保存庫相關聯的存放裝置使用量

## <a name="manage-your-production-servers"></a>管理您的生產伺服器
您的實際執行伺服器，按一下 toomanage**設定**。

按一下 [管理] 之下的 [備份基礎結構] > [生產伺服器]。

hello 實際執行伺服器刀鋒視窗中列出的所有可用的實際執行伺服器。 按一下 在 hello 清單 tooopen hello 伺服器詳細資料的伺服器上。

![受保護項目](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>開啟 hello Azure Backup agent
開啟 hello **Microsoft Azure 備份代理程式**(藉由搜尋電腦找到它*Microsoft Azure 備份*)。

![Windows Server 備份排程](./media/backup-azure-manage-windows-server/snap-in-search.png)

從 hello**動作**位於 hello hello 備份代理程式 」 主控台的權限執行下列管理工作的 hello:

* 註冊伺服器
* 排程備份
* 立即備份
* 變更屬性

![Microsoft Azure 備份代理程式主控台動作](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> 太**復原資料**，請參閱[還原檔案 tooa Windows server 或 Windows 用戶端電腦](backup-azure-restore-windows-server.md)。
>
>

## <a name="modify-hello-backup-schedule"></a>修改備份排程，hello
1. Hello Microsoft Azure Backup agent 中按一下**排程備份**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. 在 [hello**排程備份精靈**保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步]**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. 如果您想 tooadd 或變更項目，在 hello**選取項目 tooBackup**畫面上，按一下**新增的項目**。

    您也可以設定**排除設定**在 hello 精靈的這個頁面。 如果您想要 tooexclude 檔案或檔案類型讀取 hello 加入程序[排除設定](#manage-exclusion-settings)。
4. 選取 hello 檔案和資料夾，您想 tooback 和按一下**好**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. 指定 hello**備份排程**按一下**下一步**。

    您可以排程每日 (一天最多 3 次) 或每週備份。

    ![Windows Server 備份項目](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > 指定 hello 備份排程中會詳細說明此[文章](backup-azure-backup-cloud-as-tape.md)。
   >

6. 選取 hello**保留原則**hello 備份複本，然後按一下**下一步**。

    ![Windows Server 備份項目](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. 在 hello**確認**畫面檢閱 hello 資訊，然後按一下**完成**。
8. 一旦 hello 精靈可讓您完成建立 hello**備份排程**，按一下 **關閉**。

    之後修改的保護，您可以確認備份正確的觸發移 toohello 由**作業** 索引標籤，並確認變更會反映在 hello 備份作業。

## <a name="enable-network-throttling"></a>啟用網路節流

hello Azure 備份代理程式提供節流索引標籤可讓您 toocontrol 資料傳輸期間的網路頻寬使用方式。 如果您需要 tooback 資料在工作時間，但不是想將備份程序 toointerfere hello 與其他的網際網路流量，此控制項可以是很有幫助。 節流的資料傳輸 tooback 套用設定，並還原活動。  

tooenable 節流：

1. 在 hello **Backup agent**，按一下 **變更屬性**。
2. 在 [hello * * 節流] 索引標籤，選取**啟用網際網路頻寬使用節流設定的備份操作**。

    ![網路節流](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    一旦您已啟用節流設定，指定允許頻寬的備份資料傳輸期間的 hello**上班**和**非工作小時**。

    hello 頻寬值 512 kb/秒 (Kbps) 為開頭，而且可以向上 too1023 mb / 秒 (Mbps)。 您可以指定 hello 開始和完成**上班**，而 hello 一週的哪幾天會被視為工作天。 指定工作時數的 hello 之外的 hello 時間是視為的 toobe 非工作小時。
3. 按一下 [確定] 。

## <a name="manage-exclusion-settings"></a>管理排除設定
1. 開啟 hello **Microsoft Azure 備份代理程式**(您可以藉由搜尋電腦上找到它*Microsoft Azure 備份*)。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. Hello Microsoft Azure Backup agent 中按一下**排程備份**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. 在 排程備份精靈 hello 保留 hello**變更 toobackup 項目或時間**選取的選項，然後按一下**下一步**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. 按一下 [排除設定] 。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. 按一下 [新增排除] 。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. 選取 hello 位置，然後按一下 **確定**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Hello 檔案延伸模組增益集 hello**檔案類型**欄位。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    新增 .mp3 副檔名

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd 另一個延伸模組中，按一下**新增排除**，然後輸入另一個檔案類型副檔名 （新增.jpeg 副檔名）。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. 當您新增所有 hello 擴充功能之後時，按一下**確定**。
9. 繼續透過 hello 排程備份精靈]，依序按一下**下一步**直到 hello**確認頁面**，然後按一下 [**完成**。

    ![Windows Server 備份排程](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>常見問題集
**Q1。hello 備份工作狀態會顯示為已完成在 hello Azure 備份代理程式為何不它取得會立即反映在入口網站？**

A1. 那里會在延遲時間上限為 15 分鐘之間 hello 備份作業的狀態反映在 hello Azure 備份代理程式 」 和 「 hello Azure 入口網站。

**Q.2 備份工作失敗時，時間長度花費 tooraise 警示？**

A.2 警示就會引發 hello Azure 備份失敗的 20 分鐘內。

**Q3.是否會有已設定通知但不會傳送電子郵件的情況？**

A3. 不會傳送 hello 通知順序 tooreduce hello 警示的干擾中時，以下是 hello 案例：

* 如果每小時設定通知，並引發並 hello 一小時內已解決的警示
* 作業便會取消。
* 第二個備份作業會失敗，因為原始的備份作業正在進行中。

## <a name="troubleshooting-monitoring-issues"></a>疑難排解監視問題
**問題：**作業和/或 hello Azure Backup agent 的警示不會出現在 hello 入口網站。

**疑難排解步驟：** hello 程序， ```OBRecoveryServicesManagementAgent```，傳送 hello 作業和警示資料 toohello Azure 備份服務。 此程序可能偶爾會卡住或關閉。

1. tooverify hello 程序並未執行，請開啟**工作管理員**，檢查是否 hello```OBRecoveryServicesManagementAgent```處理序正在執行。
2. 假設 hello 程序不在執行中，開啟**控制台**並瀏覽 hello 服務清單。 啟動或重新啟動 **Microsoft Azure 復原服務管理代理程式**。

    如需詳細資訊，瀏覽 hello 記錄檔，位於：<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` 例如：<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>後續步驟
* [從 Azure 還原 Windows Server 或 Windows 用戶端](backup-azure-restore-windows-server.md)
* toolearn 進一步了解 Azure 備份，請參閱[Azure 備份概觀](backup-introduction-to-azure-backup.md)
* 請瀏覽 hello [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)
