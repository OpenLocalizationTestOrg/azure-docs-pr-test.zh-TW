---
title: "設定 SharePoint 伺服器陣列 tooAzure aaaUse Azure 備份伺服器 tooback |Microsoft 文件"
description: "使用 Azure 備份伺服器 tooback 及還原 SharePoint 資料。 本文章提供 hello 資訊 tooconfigure 您 SharePoint 伺服器陣列，讓所需的資料可以儲存在 Azure 中。 您可以從磁碟或 Azure 還原受保護的 SharePoint 資料。"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>備份 SharePoint 伺服器陣列 tooAzure
備份 SharePoint 伺服器陣列 tooMicrosoft Azure 多 hello 中使用 Microsoft Azure 備份伺服器 (MABS) 相同的方式，您可以備份其他資料來源。 Azure 備份提供具彈性的 hello 備份排程 toocreate 每日、 每週、 每月或每年備份點，並提供您各種備份點保留原則選項。 它也提供快速的復原時間目標 (RTO) hello 功能 toostore 本機磁碟的複本，並 toostore 複製 tooAzure 經濟、 長期保留的。

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>SharePoint 支援的版本與相關保護案例
DPM 的 azure 備份支援下列案例的 hello:

| 工作負載 | 版本 | SharePoint 部署 | 保護和復原 |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013、SharePoint 2010、SharePoint 2007、SharePoint 3.0 |部署為實體伺服器或 Hyper-V/VMware 虛擬機器的 SharePoint  <br> -------------- <br> SQL AlwaysOn | 保護 SharePoint 伺服器陣列復原選項：來自磁碟復原點的復原伺服器陣列、資料庫及檔案或清單項目  來自 Azure 復原點的伺服器陣列和資料庫復原。 |

## <a name="before-you-start"></a>開始之前
有幾件事您備份 SharePoint 伺服器陣列 tooAzure 之前，需要 tooconfirm。

### <a name="prerequisites"></a>必要條件
在繼續之前，請確定您有[安裝並準備好 Azure 備份伺服器 hello](backup-azure-microsoft-azure-backup.md) tooprotect 工作負載。

### <a name="protection-agent"></a>保護代理程式
hello 保護代理程式必須安裝 SharePoint、 hello 執行 SQL Server 的伺服器和所有其他 hello SharePoint 伺服陣列一部分的伺服器正在執行的 hello 伺服器上。 如需有關如何 tooset hello 保護代理程式，請參閱[安裝保護代理程式](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)。  hello 一個例外狀況是您只能在單一的 web 前端 (WFE) 伺服器上安裝 hello 代理程式。 為保護的 hello 進入點，DPM 需要在上一個 WFE 伺服器只有 tooserve hello 代理程式。

### <a name="sharepoint-farm"></a>SharePoint 伺服器陣列
Hello 伺服陣列中每隔 10 百萬個項目，必須有至少 2 GB 的空間 hello 磁碟區上 hello MABS 資料夾所在的位置。 此空間對目錄產生是必要的。 MABS toorecover 特定項目 （網站集合、 網站、 清單、 文件庫、 資料夾、 個別的文件和清單項目），類別目錄產生會建立每個內容資料庫內所包含的 hello Url 的清單。 您可以在 hello hello 可復原的項目 窗格中檢視 Url hello 清單**復原**工作 MABS 系統管理員主控台的區域。

### <a name="sql-server"></a>SQL Server
MABS 會以 LocalSystem 帳戶執行。 tooback SQL Server 資料庫，MABS hello 執行 SQL Server 的伺服器需要該帳戶上的 sysadmin 權限。 將 NT AUTHORITY\SYSTEM 太*sysadmin* hello 才能執行 SQL Server 的伺服器上加以備份。

如果 hello SharePoint 伺服器陣列已使用 SQL Server 別名設定的 SQL Server 資料庫，請 hello 前端網頁伺服器上將保護 MABS 安裝 hello SQL Server 用戶端元件。

### <a name="sharepoint-server"></a>SharePoint Server
雖然效能取決於許多因素，例如 SharePoint 伺服器陣列的大小，但一般做法是一部 MABS 可以保護一個 25 TB 的 SharePoint 伺服器陣列。

### <a name="whats-not-supported"></a>不支援的內容
* 保護 SharePoint 伺服器陣列的 MABS 不會保護搜尋索引或應用程式服務資料庫。 您將分別需要 tooconfigure hello 保護的資料庫。
* MABS 不提供相應放大檔案伺服器 (SOFS) 共用所裝載的 SharePoint SQL Server 資料庫備份。

## <a name="configure-sharepoint-protection"></a>設定 SharePoint 保護
您可以使用 MABS tooprotect SharePoint 之前，您必須設定 hello SharePoint VSS 寫入器服務 （WSS 寫入器服務） 使用**ConfigureSharePoint.exe**。

您可以找到**ConfigureSharePoint.exe** hello 前端 web 伺服器上的 [MABS 安裝路徑] hello \bin 資料夾中。 這項工具提供 hello SharePoint 伺服器陣列的 hello 與 hello 認證的保護代理程式。 您在單一 WFE 伺服器上執行。 如果您有多部 WFE 伺服器，在設定保護群組時請選取其中一部。

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>tooconfigure hello SharePoint VSS 寫入器服務
1. Hello WFE 伺服器上，在命令提示字元中，跳過 [MABS 安裝位置] \bin\
2. 輸入 ConfigureSharePoint -EnableSharePointProtection
3. 輸入 hello 伺服陣列系統管理員認證。 此帳戶應該是 hello WFE 伺服器上 hello 本機系統管理員群組的成員。 如果 hello 伺服陣列管理員不下列 hello WFE 伺服器上的權限的本機系統管理員授與 hello:
   * 授與 hello WSS_Admin_WPG 群組完全控制 toohello DPM 資料夾 （%Program Files%\Microsoft Azure Backup\DPM）。
   * 授與 hello WSS_Admin_WPG 群組讀取權限 toohello DPM 登錄機碼 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)。

> [!NOTE]
> Hello SharePoint 伺服器陣列系統管理員認證變更時，您將需要 toorerun ConfigureSharePoint.exe。
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a>使用 MABS 備份 SharePoint 伺服器陣列
設定 MABS 和 hello 與先前所述的 SharePoint 伺服陣列之後，可以由 MABS 提供保護 SharePoint。

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect SharePoint 伺服器陣列
1. 從 hello**保護**hello MABS 系統管理員主控台 索引標籤上按一下**新增**。
    ![[新增保護] 索引標籤](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. 在 hello**選取保護群組類型**hello 頁面**建立新保護群組**精靈、 選取**伺服器**，然後按一下**下一步**.

    ![選擇保護群組類型](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. 在 hello**選擇群組成員**螢幕、 選取 hello hello SharePoint 伺服器 tooprotect 然後按一下核取方塊**下一步**。

    ![選擇群組成員](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > Hello 保護代理程式安裝，您可以看到 hello hello 精靈中的伺服器。 MABS 也會顯示其結構。 由於您已執行 ConfigureSharePoint.exe，MABS 與 hello SharePoint VSS 寫入器服務和其相對應的 SQL Server 資料庫通訊，並且辨識 hello SharePoint 伺服器陣列結構，hello 相關聯的內容資料庫中和任何對應的項目。
   >
   >
4. 在 hello**選擇資料保護方式**頁面上，輸入 hello hello 名稱**保護群組**，然後選取您慣用*保護方法*。 按一下 [下一步] 。

    ![選擇資料保護方式](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > hello 磁碟保護的方法可協助 toomeet 簡短的復原時間目標。
   >
   >
5. 在 hello**指定短期目標**頁面上，選取您慣用**保留範圍**並找出您想要備份 toooccur 時。

    ![指定短期目標](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > 最常需要的是少於 5 天的資料復原，因為我們會選取在磁碟上的五天的保留範圍，並確保該 hello 備份發生在非生產時段，此範例中。
   >
   >
6. 檢閱 hello 存放集區磁碟空間配置給 hello 保護群組，然後按一下 **下一步**。
7. 對於每個保護群組，MABS 配置磁碟空間 toostore 及管理複本。 此時，MABS 必須建立 hello 選取資料的複本。 選取如何及何時您希望 hello 複本建立，然後按一下**下一步**。

    ![選擇複本的建立方式](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > toomake 確定的網路流量不會受影響，會選取生產的時間之外的時間。
   >
   >
8. MABS 執行 hello 複本上的一致性檢查，確保資料完整性。 有兩個可用的選項。 您可以定義排程 toorun 一致性檢查，或 DPM 變得不一致時執行一致性檢查，會自動在 hello 複本上的。 選取您慣用的選項，然後按 [下一步] 。

    ![一致性檢查](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. 在 hello**指定線上保護資料**頁面上，選取您想 tooprotect，，然後按一下的 hello SharePoint 伺服器陣列**下一步**。

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. 在 hello**指定線上備份排程**頁面上，選取您偏好的排程，然後按一下**下一步**。

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > MABS 可提供最高的兩個每日備份 tooAzure 在 hello] 和 [使用最新的磁碟備份點。 Azure 備份也可以控制可以用於尖峰和離峰時間中的備份所使用的 WAN 頻寬的 hello 數量[Azure 備份網路節流設定](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling)。
    >
    >
11. 根據您選取在 hello hello 備份排程**指定線上保留原則**頁面上，選取 hello 每日、 每週、 每月和每年備份點保留原則。

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > MABS 會使用 grandfather-father-son 保留配置，可讓您為不同的備份時間點選擇不同的保留原則。
    >
    >
12. 類似的 toodisk 初始的參考點複本需要 toobe 在 Azure 中建立。 選取您慣用的選項 toocreate 初始備份複本 tooAzure，，然後按一下**下一步**。

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. 檢閱您選取的設定，在 hello**摘要**頁面，然後再按一下**建立群組**。 建立 hello 保護群組之後，您會看到成功訊息。

    ![摘要](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a>使用 MABS 從磁碟還原 SharePoint 項目
在下列範例的 hello，hello*復原 SharePoint 項目*被意外刪除，而且需要 toobe 復原。
![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. 開啟 hello **DPM 系統管理員主控台**。 DPM 所保護的所有 SharePoint 伺服器陣列所都示 hello**保護** 索引標籤。

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. toobegin toorecover hello 項目，請選取 hello**復原** 索引標籤。

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. 您可以使用萬用字元型搜尋，在復原點範圍內搜尋 SharePoint 中的 *Recovering SharePoint item* 。

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. 從 hello 搜尋結果中選取 hello 適當的復原點，hello 項目，以滑鼠右鍵按一下，然後選取**復原**。
5. 您也可以瀏覽不同的復原點，並選取資料庫或項目 toorecover。 選取**日期 > 復原時間**，然後選取正確的 hello**資料庫 > SharePoint 伺服器陣列 > 復原點 > 項目**。

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Hello 項目，以滑鼠右鍵按一下，然後選取**復原**tooopen hello**復原精靈**。 按一下 [下一步] 。

    ![檢閱復原選項](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. 選取您想 tooperform，然後再按一下復原 hello 類型**下一步**。

    ![復原類型](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > hello 選取**復原 toooriginal** hello 範例會復原 hello 項目 toohello 原始 SharePoint 網站。
   >
   >
8. 選取 hello**復原程序**想 toouse。

   * 選取**復原，而不使用復原伺服器陣列**如果 hello SharePoint 伺服陣列並未變更，而且的 hello 相同 hello 復原點，進行還原。
   * 選取**使用復原伺服器陣列復原**hello SharePoint 伺服器陣列在之後建立 hello 復原點已變更。

     ![復原程序](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. 提供暫存 SQL Server 執行個體位置 toorecover hello 資料庫暫時，並提供暫存的檔案共用 MABS 和 hello SharePoint toorecover hello 項目執行的伺服器上。

    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    MABS 附加 hello 裝載 hello SharePoint 項目 toohello 暫存 SQL Server 執行個體的內容資料庫。 Hello 內容資料庫，從它復原 hello 項目，並將它放在 hello 預備 MABS 上的檔案位置。 hello 復原需求 toobe 匯出 toohello 預備 hello SharePoint 伺服器陣列上的位置位於 hello 現在預備位置的項目。

    ![Staging Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. 選取**指定復原選項**，以及套用安全性設定 toohello SharePoint 伺服器陣列，或套用 hello hello 復原點的安全性設定。 按一下 [下一步] 。

    ![修復選項](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > 您可以選擇 toothrottle hello 網路頻寬使用量。 這可降低影響 toohello 實際執行伺服器生產小時期間。
    >
    >
11. 檢閱 hello 摘要資訊，然後按一下**復原**toobegin hello 檔案復原。

    ![復原摘要](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. 現在選取 hello**監視** 索引標籤中 hello **MABS 系統管理員主控台**tooview hello**狀態**的 hello 復原。

    ![復原狀態](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > hello 檔案現已還原。 您可以重新整理 hello SharePoint 站台 toocheck hello 還原檔案。
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>使用 DPM 從 Azure 中還原 SharePoint 資料庫
1. toorecover SharePoint 內容資料庫中，瀏覽各種復原點 （如先前所示），並選取您想 toorestore hello 復原點。

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. 按兩下 hello SharePoint 復原點 tooshow hello 可用 SharePoint 類別目錄資訊。

   > [!NOTE]
   > Hello SharePoint 伺服器陣列受到保護供長期保存在 Azure 中，因為沒有類別目錄資訊 （中繼資料） 位於 MABS。 如此一來，每次的時間點的 SharePoint 內容資料庫需要 toobe 復原，您需要 toocatalog hello SharePoint 伺服陣列一次。
   >
   >
3. 按一下 [重新編目] 。

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    hello**雲端重新編目**狀態 視窗隨即開啟。

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    Hello 狀態編目完成後，變更太*成功*。 按一下 [關閉] 。

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. 按一下 顯示 hello MABS 中的 hello SharePoint 物件**復原**tooget hello 內容資料庫結構索引標籤上。 Hello 項目，以滑鼠右鍵按一下，然後按一下**復原**。

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. 此時，請遵循 hello[本文稍早的復原步驟](#restore-a-sharepoint-item-from-disk-using-dpm)toorecover 從磁碟的 SharePoint 內容資料庫。

## <a name="faqs"></a>常見問題集
問： 是否如果使用 （與在磁碟上的保護） 的 SQL AlwaysOn 設定 SharePoint 可以復原 SharePoint 項目 toohello 原始位置？<br>
答: [是]，hello 項目可以是復原的 toohello 原始的 SharePoint 網站。

問： 是否如果使用 SQL AlwaysOn 設定 SharePoint 可以復原 SharePoint 資料庫 toohello 原始位置？<br>
答： 因為 SharePoint 資料庫在 SQL AlwaysOn 設定，無法修改它們除非 hello 可用性群組。 如此一來，MABS 無法還原資料庫 toohello 原始位置。 您可以復原的 SQL Server 資料庫 tooanother SQL Server 執行個體。

## <a name="next-steps"></a>後續步驟
* 深入了解 SharePoint 的 MABS 保護 - 請參閱[影片系列 - SharePoint 的 DPM 保護 (英文)](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
