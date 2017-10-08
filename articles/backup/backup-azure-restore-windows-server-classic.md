---
title: "aaaRestore 資料 tooa Windows Server 或 Windows 用戶端從 Azure 中，使用 hello 傳統部署模型 |Microsoft 文件"
description: "深入了解如何從 Windows Server 或 Windows 用戶端 toorestore。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a>還原檔案 tooa Windows server 或 Windows 用戶端電腦使用 hello 傳統部署模型
> [!div class="op_single_selector"]
> * [傳統入口網站](backup-azure-restore-windows-server-classic.md)
> * [Azure 入口網站](backup-azure-restore-windows-server.md)
>
>

本文說明如何 toorecover 資料從備份保存庫，並將它還原 tooa 伺服器或電腦。 自 2017 年 3 月開始，您可以再建立備份保存庫 hello 傳統入口網站中。

> [!IMPORTANT]
> 您現在可以升級您備份保存庫 tooRecovery 服務保存庫。 如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。 Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。<br/> **2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。 <br/> **自 2017 年 11 月 1 日起**：
>- 任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。
>- 您將無法 tooaccess hello 傳統入口網站中無法備份資料。 相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。
>

toorestore 資料，您會使用 hello 復原資料精靈在 hello Microsoft Azure 復原服務 」 (MARS) 代理程式。 當您還原資料時，您可以︰

* 相同電腦中的 hello 備份還原資料 toohello 拍攝。
* 還原資料 tooan 其他機器。

年 1 月 2017，Microsoft 發行預覽更新 toohello MARS 代理程式。 Bug 修正，以及這項更新啟用立即還原，可讓您 toomount 可寫入的復原點快照集以復原磁碟區。 然後，您可以瀏覽 hello 復原磁碟區並將複製檔案 tooa 本機電腦藉此選擇性地還原檔案。

> [!NOTE]
> hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview)如果您想要立即還原 toorestore 資料 toouse，則需要。 也在保存庫在 hello 技術支援文件中所列的地區設定必須加以保護 hello 備份資料。 請參閱 hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) hello 支援 立即還原的地區設定的最新的清單。 「立即還原」目前**無法**在所有地區設定中使用。
>

立即還原適用於在 hello Azure 入口網站中的 復原服務保存庫中使用與備份保存庫 hello 傳統入口網站中。 如果您想 toouse 立即還原，下載 hello MARS 更新，並遵循提到立即還原 hello 程序。


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
    > 如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接六個小時，從 hello 裝載時的時間。 掛上 hello 磁碟區時，將會不執行任何備份作業。 Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。
    >


## <a name="recover-data-toohello-same-machine"></a>復原資料 toohello 同一部電腦
如果您不小心刪除了檔案，並且想 toorestore 它 toohello 同一部電腦 （從哪些 hello 備份），hello 下列步驟將協助您復原 hello 資料。

1. 開啟 hello **Microsoft Azure 備份**中對齊。
2. 按一下**復原資料**tooinitiate hello 工作流程。

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)
3. 選取 hello **這部伺服器 (*yourmachinename*) * * 選項 toorestore hello 備份上 hello 檔案相同的電腦。

    ![相同電腦](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. 選擇太**瀏覽檔案**或**搜尋檔案**。

    如果，保留單元 hello 預設選項您計劃 toorestore 已知其路徑的一個或多個檔案。 如果您不確定 hello 資料夾結構，但希望 toosearch 檔案，挑選 hello**搜尋檔案**選項。 為了 hello 這一節，我們將繼續使用 hello 預設選項。

    ![瀏覽檔案](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. 選取您想要從中 toorestore hello 檔案 hello 磁碟區。

    您可以從任何時間點還原。 它會出現在日期**粗體**hello 月曆控制項中指出的還原點的 hello 可用性。 一旦選取日期之後，根據您的備份排程 （和 hello 成功備份作業的），您可以選取的時間點從 hello**時間**下拉式清單。

    ![磁碟區和日期](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. 選取 hello 項目 toorecover。 您可以將多選資料夾/檔案想 toorestore。

    ![選取檔案](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. 指定 hello 復原參數。

    ![修復選項](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * 您可以選擇還原 toohello （中的 hello 檔案/資料夾可能會被覆寫） 的原始位置] 或 [hello tooanother 位置的同一部電腦。
   * 如果 hello 檔案/資料夾，您想 toorestore 存在於 hello 目標位置，您可以建立複本 (hello 的兩個版本相同的檔案)、 覆寫 hello 檔案在 hello 目標位置，或略過的 hello 檔案存在 hello 目標中的 hello 復原。
   * 強烈建議您保持還原 hello hello 復原的檔案 Acl 的 hello 預設選項。
8. 提供這些輸入之後，按一下 [下一步] 。 hello 復原工作流程，後者還原 hello 檔案 toothis 機器，就會開始。

## <a name="recover-tooan-alternate-machine"></a>Tooan 替代機器復原
整個伺服器遺失時，您仍然可以從 Azure Backup tooa 不同電腦中復原資料。 hello 下列步驟說明 hello 工作流程。  

包含下列步驟中所使用的 hello 術語：

* *來源機器*– 拍攝 hello 從哪個 hello 備份的原始電腦，這是目前無法使用。
* *目標電腦*– hello 機器 toowhich hello 資料要復原的目的地。
* *範例保存庫*– hello 備份保存庫 toowhich hello*來源機器*和*目標機器*註冊。 <br/>

> [!NOTE]
> 從機器的備份無法還原在執行舊版的 hello 作業系統的電腦上。 例如，如果從 Windows 7 電腦進行備份，則可以在 Windows 8 或更新版電腦上進行還原。 不過，hello 反之亦然並未維持 true。
>
>

1. 開啟 hello **Microsoft Azure 備份**在 hello 上對齊*目標機器*。
2. 請確定該 hello*目標電腦*和 hello*來源機器*是已註冊的 toohello 相同的備份保存庫。
3. 按一下**復原資料**tooinitiate hello 工作流程。

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)
4. 選取 [其他伺服器] 

    ![其他伺服器](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. 提供對應 toohello hello 保存庫認證檔案*範例保存庫*。 如果 hello 保存庫認證檔案無效 （或已過期） 下載新的保存庫認證檔案從 hello*範例保存庫*hello Azure 傳統入口網站中。 一旦提供 hello 保存庫認證檔案，則會顯示 hello 針對 hello 保存庫認證檔案的備份保存庫。
6. 選取 hello*來源機器*從 hello 顯示的電腦清單。

    ![電腦清單](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. 選取任一 hello**搜尋檔案**或**瀏覽檔案**選項。 本節 hello 目的，我們將使用 hello**搜尋檔案**選項。

    ![搜尋](./media/backup-azure-restore-windows-server-classic/search.png)
8. Hello 下一個畫面中，選取 hello 磁碟區和日期。 搜尋您想 toorestore hello 資料夾/檔案名稱。

    ![搜尋項目](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. 選取需要 hello 檔案還原 toobe hello 位置。

    ![還原位置](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. 提供在過程中提供的 hello 加密複雜密碼*來源機器*註冊太*範例保存庫*。

    ![加密](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. 一旦提供 hello 輸入，按一下 **復原**，此觸發程序 hello hello 檔案 toohello 目的地提供備份的還原。

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
    > 如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接六個小時，從 hello 裝載時的時間。 掛上 hello 磁碟區時，將會不執行任何備份作業。 Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。
    >


## <a name="next-steps"></a>後續步驟
* [Azure 備份常見問題集](backup-azure-backup-faq.md)
* 請瀏覽 hello [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)。

## <a name="learn-more"></a>詳細資訊
* [Azure 備份概觀](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [備份 Azure 虛擬機器](backup-azure-vms-introduction.md)
* [備份 Microsoft 工作負載](backup-azure-dpm-introduction.md)
