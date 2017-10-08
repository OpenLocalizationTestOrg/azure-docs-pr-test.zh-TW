---
title: "aaaRestore 資料在 Azure tooa Windows Server 或 Windows 電腦 |Microsoft 文件"
description: "了解 toorestore 資料如何儲存在 Azure tooa Windows Server 或 Windows 電腦。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a>還原檔案 tooa Windows server 或 Windows 用戶端電腦使用資源管理員部署模型
> [!div class="op_single_selector"]
> * [Azure 入口網站](backup-azure-restore-windows-server.md)
> * [傳統入口網站](backup-azure-restore-windows-server-classic.md)
>
>

這篇文章說明如何從備份保存庫 toorestore 資料。 toorestore 資料，您會使用 hello 復原資料精靈在 hello Microsoft Azure 復原服務 」 (MARS) 代理程式。 當您還原資料時，您可以︰

* 相同電腦中的 hello 備份還原資料 toohello 拍攝。
* 還原資料 tooan 其他機器。

年 1 月 2017，Microsoft 發行預覽更新 toohello MARS 代理程式。 Bug 修正，以及這項更新啟用立即還原，可讓您 toomount 可寫入的復原點快照集以復原磁碟區。 然後，您可以瀏覽 hello 復原磁碟區並將複製檔案 tooa 本機電腦藉此選擇性地還原檔案。

> [!NOTE]
> hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview)如果您想要立即還原 toorestore 資料 toouse，則需要。 也在保存庫在 hello 技術支援文件中所列的地區設定必須加以保護 hello 備份資料。 請參閱 hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) hello 支援 立即還原的地區設定的最新的清單。 「立即還原」目前**無法**在所有地區設定中使用。
>

立即還原適用於在 hello Azure 入口網站中的 復原服務保存庫中使用與備份保存庫 hello 傳統入口網站中。 如果您想 toouse 立即還原，下載 hello MARS 更新，並遵循提到立即還原 hello 程序。

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a>使用 立即還原 toorecover 資料 toohello 同一部電腦

如果您不小心刪除了檔案，並且想 toorestore 它 toohello 同一部電腦 （從哪些 hello 備份），hello 下列步驟將協助您復原 hello 資料。

1. 開啟 hello **Microsoft Azure 備份**中對齊。 如果您不知道 hello 嵌入式管理單元安裝所在，搜尋 hello 電腦或伺服器**Microsoft Azure 備份**。

    hello 桌面應用程式應該會出現在 hello 搜尋結果中。

2. 按一下**復原資料**toostart hello 精靈。

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. Hello 上**入門**窗格中，toorestore hello 資料 toohello 相同伺服器或電腦上，選取**這部伺服器 (`<server name>`)**按一下**下一步**。

    ![選擇此伺服器選項 toorestore hello 資料 toohello 同一部電腦](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. 在 hello**選取復原模式** 窗格中，選擇**個別檔案及資料夾**，然後按一下**下一步**。

    ![瀏覽檔案](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. 在 hello**選取磁碟區和日期**窗格中，選取 hello 磁碟區，其中包含 hello 檔案及/或您想要 toorestore 的資料夾。

    Hello 日曆上選取的復原點。 您可以從任何時間的復原點還原。 日期**粗體**表示 hello 至少一個復原點的可用性。 一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。

    ![磁碟區和日期](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. 一旦您已選擇 hello 復原點 toorestore，按一下 **掛接**。

    Azure 備份掛接 hello 本機復原點，並使用它做為復原磁碟區。

7. 在 hello**瀏覽和復原檔案** 窗格中，按一下 **瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。

    ![修復選項](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. 在 Windows 檔案總管 中，複製 hello 檔案及/或資料夾想 toorestore，並將它們貼 tooany 位置 toohello 本機伺服器或電腦。 您可以開啟或資料流 hello 檔案直接從 hello 復原磁碟區，並確認 hello 正確版本會復原。

    ![複製並貼上檔案和資料夾從掛接的磁碟區 toolocal 位置](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. 完成還原 hello 檔案及/或資料夾，在 hello**瀏覽和修復檔案** 窗格中，按一下 **卸載**。 然後按一下 **是**tooconfirm 想 toounmount hello 磁碟區。

    ![取消掛接 hello 磁碟區，並確認](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > 如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接 hello 裝載時的時間從 6 小時。 不過，hello 掛接時間是擴充高達 24 小時內進行中的檔案複製時的最大值。 掛上 hello 磁碟區時，將會不執行任何備份作業。 Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a>使用 立即還原 toorestore 資料 tooan 替代機器
整個伺服器遺失時，您仍然可以從 Azure Backup tooa 不同電腦中復原資料。 hello 下列步驟說明 hello 工作流程。


包含下列步驟中所使用的 hello 術語：

* *來源機器*– 拍攝 hello 從哪個 hello 備份的原始電腦，這是目前無法使用。
* *目標電腦*– hello 機器 toowhich hello 資料要復原的目的地。
* *範例保存庫*– hello 復原服務保存庫 toowhich hello*來源機器*和*目標機器*註冊。 <br/>

> [!NOTE]
> 備份無法還原的 tooa 目標電腦執行舊版的 hello 作業系統。 例如，從 Windows 7 電腦建立的備份可以還原至 Windows 8 或更新版本的電腦。 執行 Windows 8 電腦的備份無法還原的 tooa Windows 7 電腦。
>
>

1. 開啟 hello **Microsoft Azure 備份**在 hello 上對齊*目標機器*。

2. 請確定 hello*目標電腦*和 hello*來源機器*是相同的復原服務保存庫註冊的 toohello。

3. 按一下**復原資料**tooopen hello**復原資料精靈**。

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

4. 在 hello**入門**窗格中，選取**另一部伺服器**

    ![其他伺服器](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. 提供對應 toohello hello 保存庫認證檔案*範例保存庫*，然後按一下**下一步**。

    如果 hello 保存庫認證檔案無效 （或已過期），下載新的保存庫認證檔案從 hello*範例保存庫*hello Azure 入口網站中。 一旦您提供有效的保存庫認證，hello 的 hello 對應的備份保存庫會出現的名稱。


6. 在 hello**選取備份伺服器**窗格中，選取 hello*來源機器*從 hello 清單中顯示的機器，並提供 hello 複雜密碼。 然後按 [下一步] 。

    ![電腦清單](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. 在 hello**選取復原模式**窗格中，選取**個別檔案及資料夾**按一下**下一步**。

    ![搜尋](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. 在 hello**選取磁碟區和日期**窗格中，選取 hello 磁碟區，其中包含 hello 檔案及/或您想要 toorestore 的資料夾。

    Hello 日曆上選取的復原點。 您可以從任何時間的復原點還原。 日期**粗體**表示 hello 至少一個復原點的可用性。 一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。

    ![搜尋項目](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. 按一下**掛接**toolocally 掛接 hello 復原點復原磁碟區上為您*目標機器*。

10. 在 hello**瀏覽和復原檔案** 窗格中，按一下 **瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. 在 Windows 檔案總管中，將複製 hello 檔案及/或資料夾從 hello 復原磁碟區並貼 tooyour*目標機器*位置。 您可以開啟或資料流 hello 檔案直接從 hello 復原磁碟區，並確認 hello 正確版本會復原。

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. 完成還原 hello 檔案及/或資料夾，在 hello**瀏覽和修復檔案** 窗格中，按一下 **卸載**。 然後按一下 **是**tooconfirm 想 toounmount hello 磁碟區。

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > 如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接 hello 裝載時的時間從 6 小時。 不過，hello 掛接時間是擴充高達 24 小時內進行中的檔案複製時的最大值。 掛上 hello 磁碟區時，將會不執行任何備份作業。 Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。
    >

## <a name="troubleshooting"></a>疑難排解
如果 Azure 備份不成功掛接 hello 復原磁碟區的按一下的幾分鐘後，即使**掛接**或失敗 toomount hello 復原磁碟區與一個或多個錯誤，請遵循 hello toobegin 通常復原步驟。

1.  如果已執行數分鐘，請取消 hello 持續掛接程序。

2.  確認您是在 hello hello Azure 備份代理程式的最新版本。 toofind hello 版本資訊的 Azure 備份代理程式，按一下 **有關 Microsoft Azure Recovery Services Agent**上 hello**動作**窗格中的 Microsoft Azure Backup 主控台，並確保該 hello **版本**數字是相等 tooor 高於 hello 版本中所述[本文](https://go.microsoft.com/fwlink/?linkid=229525)。 您可以下載從 hello 最新版本[這裡](https://go.microsoft.com/fwLink/?LinkID=288905)

3.  跳過**裝置管理員** -> **存放裝置控制器**，並確保您可以找出**Microsoft iSCSI 啟動器**。 如果您可以找到它，直接移 toostep 7。 

4.  如果您無法找出 Microsoft iSCSI 啟動器服務，如步驟 3 中所述，檢查 toosee 是否可以尋找下的一個項目**裝置管理員** -> **存放裝置控制器**呼叫**無法辨識的裝置**硬體識別碼**ROOT\ISCSIPRT**。

5.  以滑鼠右鍵按一下 [不明裝置]，然後選取 [更新驅動程式軟體]。

6.  更新 hello 驅動程式選取 hello 選項太**自動搜尋更新的驅動程式軟體**。 應該在變更完成 hello 更新**不明裝置**太**Microsoft iSCSI 啟動器**如下所示。 

    ![加密](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  跳過**工作管理員** -> **服務 （本機）** -> **Microsoft iSCSI 啟動器服務**。 

    ![加密](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  以滑鼠右鍵按一下 hello 服務，按一下 重新啟動 hello Microsoft iSCSI 啟動器服務**停止**和進一步再次以滑鼠右鍵按一下，並按一下**啟動**。

9.  使用即時還原重試復原。 

如果 hello 復原仍然失敗，請重新啟動您的伺服器/用戶端。 如果不想要重新開機或 hello 復原仍然失敗甚至 hello 伺服器重新啟動之後，嘗試從其他機器，復原，並連絡 Azure 支援太移[Azure 入口網站](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)和提交支援要求。

## <a name="next-steps"></a>後續步驟
* 現在您已復原檔案和資料夾，接下來您可以 [管理您的備份](backup-azure-manage-windows-server.md)。
