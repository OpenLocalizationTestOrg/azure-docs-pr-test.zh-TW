---
title: "使用 DPM 的 SQL Server 工作負載的 aaaAzure 備份 |Microsoft 文件"
description: "SQL Server 資料庫使用 hello Azure 備份服務簡介 toobacking"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli
editor: 
ms.assetid: 59df5bec-d959-457d-8731-7b20f7f1013e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: ba78dbf1c7934a259a7bd0bdb7d4467ac75d05a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-as-a-dpm-workload"></a>備份 SQL Server tooAzure 做為 DPM 工作負載
這篇文章會引導您完成 hello 組態步驟，使用 Azure 備份的 SQL Server 資料庫的備份。

設定 SQL Server 資料庫 tooAzure tooback，您需要 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

SQL Server 資料庫備份 tooAzure 和復原，從 Azure 的 hello 管理包含三個步驟：

1. 建立備份原則 tooprotect SQL Server 資料庫 tooAzure。
2. 建立備份副本，視 tooAzure。
3. 從 Azure 復原 hello 資料庫。

## <a name="before-you-start"></a>開始之前
開始之前，請確定所有 hello[必要條件](backup-azure-dpm-introduction.md#prerequisites)tooprotect 工作負載已符合使用 Microsoft Azure 備份。 hello 必要條件會涵蓋這類工作： 建立備份保存庫、 下載保存庫認證，安裝 Azure 備份代理程式，並與 hello 保存庫註冊 hello 伺服器 hello。

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>建立備份原則 tooprotect SQL Server 資料庫 tooAzure
1. Hello DPM 伺服器上，按一下 hello**保護**工作區。
2. 在 hello 工具功能區中，按一下 **新增**toocreate 新的保護群組。

    ![建立保護群組](./media/backup-azure-backup-sql/protection-group.png)
3. DPM 會顯示 hello 指南 hello [開始] 畫面上建立**保護群組**。 按一下 [下一步] 。
4. 選取 [伺服器] 。

    ![選取保護群組類型 - 伺服器](./media/backup-azure-backup-sql/pg-servers.png)
5. 展開 hello 存在 hello 資料庫 toobe 備份所在的 SQL Server 電腦。 DPM 顯示可從該伺服器備份的各種資料來源。 展開 hello**所有 SQL 共用**選取 hello 選取的資料庫 （在此情況下我們 ReportServer$ MSDPM2012 和 ReportServer$ MSDPM2012TempDB） toobe 備份。 按一下 [下一步] 。

    ![選取 SQL DB](./media/backup-azure-backup-sql/pg-databases.png)
6. 提供 hello 保護群組的名稱，並選取 hello**我要執行線上保護**核取方塊。

    ![資料保護方式 - 短期磁碟和線上 Azure](./media/backup-azure-backup-sql/pg-name.png)
7. 在 hello**指定短期目標**畫面上，包括 hello 必要輸入 toocreate 備份點 toodisk。

    我們在這裡看到的**保留範圍**設定得*5 天*，**同步處理頻率**tooonce 設定每個*15 分鐘*即 hello取得備份的頻率。 **快速完整備份**設定得*8:00 P.M.*。

    ![短期目標](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > 下午 8:00 （依據 toohello 螢幕輸入） 備份點由每日傳送 hello hello 資料已修改的前一天的下午 8:00 備份點。 這個程序稱為 [快速完整備份] 。 Hello 交易記錄檔會同步處理時，則會重新顯示 hello hello 記錄檔建立 hello 點，如果在下午 9:00 – 需要 toorecover hello 資料庫每隔 15 分鐘上一次快速完整備份點 (在此情況下的 8 pm)。
   >
   >

8. 按一下 [下一步] 

    DPM 會顯示 hello 可用的整體儲存空間和 hello 潛在磁碟空間使用量。

    ![磁碟配置](./media/backup-azure-backup-sql/pg-storage.png)

    根據預設，DPM 會建立一個磁碟區，每個資料來源 （SQL Server 資料庫） 是用於 hello 初始備份複本。 Hello 邏輯磁碟管理員 (LDM) 會使用這個方法，限制 DPM 保護 too300 資料來源 （SQL Server 資料庫）。 這項限制，選取 hello toowork **DPM 存放集區中的資料共置**，選項。 如果您使用此選項時，DPM 會使用單一磁碟區的多個資料來源，可讓 DPM tooprotect too2000 SQL 資料庫。

    如果**自動擴大 hello 磁碟區**選取選項，則 DPM 可以考量增加 hello 備份磁碟區隨著 hello 實際執行資料。 如果**自動擴大 hello 磁碟區**選項並未選取，DPM 會限制 hello 備份儲存體使用 toohello hello 保護群組中的資料來源。
9. Hello 選擇的傳輸此初始備份以手動方式 （網路） 關閉 tooavoid 頻寬壅塞或 hello 網路時，會給予系統管理員。 他們也可以設定初始區域轉送，可以發生在哪一個 hello hello 時間。 按一下 [下一步] 。

    ![初始複寫方法](./media/backup-azure-backup-sql/pg-manual.png)

    hello 初始備份複本會從實際執行伺服器 （SQL Server 電腦） toohello DPM 伺服器需要傳送嗨整個資料來源 （SQL Server 資料庫）。 這項資料可能會很大，並透過 hello 網路傳輸的 hello 資料可能會超出頻寬。 基於這個理由，系統管理員可以選擇 tootransfer hello 初始備份：**手動**（使用卸除式媒體） tooavoid 頻寬壅塞或**自動透過網路 hello** （在指定時間）。

    Hello 初始備份完成之後，請 hello rest 的 hello 備份是增量備份 hello 初始備份複本。 增量備份通常 toobe 小，而且可輕鬆地轉移 hello 網路上。
10. 選擇當您想 hello 一致性檢查 toorun，然後按一下**下一步**。

    ![一致性檢查](./media/backup-azure-backup-sql/pg-consistent.png)

    DPM 可以執行一致性檢查 toocheck hello 的完整性 hello 備份點。 它會計算 hello 備份檔案的 hello 實際執行伺服器 （在此案例中的 SQL Server 電腦） 和 hello 備份資料用於該檔案位於 DPM hello 總和檢查碼。 在發生衝突的 hello 情況下，它會假設該 hello 在 DPM 的備份檔案已損毀。 DPM 改正了 hello 備份資料，藉由傳送嗨區塊對應 toohello 總和檢查碼不符。 因為 hello 一致性檢查的效能密集作業，管理員可以在 hello 選擇的排程 hello 一致性檢查或自動執行它。
11. toospecify hello 多數目的資料來源的線上保護，選取 hello 資料庫 toobe 受保護的 tooAzure 和按一下**下一步**。

    ![選取資料來源](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. 系統管理員可以選擇備份排程以及符合其組織原則的保留原則。

    ![排程和保留](./media/backup-azure-backup-sql/pg-schedule.png)

    在此範例中，備份每天進行一次在下午 12:00 和下午 8 （囉 」 畫面中的下半部）

    > [!NOTE]
    > 它是很好的作法 toohave 少數的短期復原點，在磁碟上，以便快速復原。 這些復原點可用於「操作復原」。 Azure 可做為具有較高 SLA 和保證可用性的良好離站位置。
    >
    >

    **最佳作法**： 請確定 Azure 備份已排定 hello 使用 DPM 的本機磁碟備份完成後。 這可讓最新磁碟複製備份 toobe tooAzure hello。

13. 選擇 hello 保留原則排程。 在提供 hello hello 保留原則的運作方式的詳細資訊[使用 Azure Backup tooreplace 您磁帶基礎結構的文章](backup-azure-backup-cloud-as-tape.md)。

    ![保留原則](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    在此範例中：

    * 備份在下午 12:00 和下午 8 （下半部囉 」 畫面） 是一天一次，並且會保留為 180 天。
    * 星期六的下午 12:00 的 hello 備份 會保留 104 週
    * 最後一個星期六的下午 12:00 的 hello 備份 會保留 60 週
    * 在最後一個星期六的下午 12:00 的 3 月 hello 備份 會保留 10 年
14. 按一下**下一步**和選取 hello 傳送嗨初始備份複本 tooAzure 適當的選項。 您可以選擇**自動透過網路 hello**或**離線備份**。

    * **自動透過網路 hello**傳輸 hello 依據 hello 排程備份選擇的備份資料 tooAzure。
    * [在 Azure 備份中離線備份工作流程](backup-azure-backup-import-export.md)說明 [離線備份] 的運作方式。

    選擇 hello 相關傳輸機制 toosend hello 初始備份複本 tooAzure 按一下**下一步**。
15. 一旦您檢閱 hello 原則詳細資料，在 hello**摘要**畫面上，按一下 hello**建立群組**按鈕 toocomplete hello 工作流程。 您可以按一下 hello**關閉**在 [監視] 工作區的按鈕和監視器 hello 工作進度。

    ![保護群組的建立正在進行中](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>SQL Server 資料庫的隨選備份
當 hello 先前的步驟建立備份原則時，hello 第一次備份，就會發生時，才建立的復原點 」。 而不是等待中的 hello 排程器 tookick，hello 步驟觸發程序 hello 建立復原點以手動方式。

1. 等待 hello 保護群組狀態顯示**確定**hello 資料庫，再建立 hello 復原點。

    ![保護群組成員](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Hello 資料庫上按一下滑鼠右鍵，然後選取**建立復原點**。

    ![建立線上復原點](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. 選擇**線上保護**hello 下拉式選單中按一下**確定**。 這是在 Azure 中啟動 hello 建立復原點。

    ![建立復原點](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. 您可以檢視 hello 工作進度中 hello**監視**工作區，您可以在其中找到正在進行中作業，像是 hello hello 下圖所示的其中一個。

    ![監視主控台](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>從 Azure 復原 SQL Server 資料庫
hello 下列步驟是必要的 toorecover 從 Azure 的受保護實體 （SQL Server 資料庫）。

1. 開啟 hello DPM 伺服器管理主控台。 瀏覽過**復原**您可以在其中看到 hello 伺服器工作區由 DPM 備份。 瀏覽 hello 必要的資料庫 （在此案例 ReportServer$ MSDPM2012)。 選取以 [線上] 結尾的 [復原自] 時間。

    ![選取復原點](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Hello 資料庫名稱上按一下滑鼠右鍵，然後按一下**復原**。

    ![從 Azure 復原](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. DPM 會顯示 hello hello 復原點詳細資料。 按一下 [下一步] 。 toooverwrite hello 資料庫中，選取 hello 復原類型**復原 toooriginal SQL Server 執行個體**。 按一下 [下一步] 。

    ![復原 tooOriginal 位置](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    在此範例中，DPM 可讓復原的 hello 資料庫 tooanother SQL Server 執行個體或 tooa 獨立網路 資料夾。
4. 在 [hello**指定復原選項**] 畫面上，您可以選取 hello 復原選項，例如網路頻寬使用節流設定使用復原 toothrottle hello 頻寬。 按一下 [下一步] 。
5. 在 hello**摘要**畫面上，看到所有的 hello 復原設定，提供到目前為止。 按一下 [復原] 。

    hello 復原狀態會顯示 hello 資料庫恢復中。 您可以按一下**關閉**tooclose hello 精靈和檢視 hello 進度中 hello**監視**工作區。

    ![起始復原程序](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Hello 復原完成後，hello 還原資料庫是一致的應用程式。

### <a name="next-steps"></a>後續步驟：
•    [Azure 備份常見問題集](backup-azure-backup-faq.md)
