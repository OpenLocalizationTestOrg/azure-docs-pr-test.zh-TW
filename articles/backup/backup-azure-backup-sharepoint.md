---
title: "SharePoint 伺服器陣列至 Azure 的 DPM/Azure 備份伺服器保護 | Microsoft Docs"
description: "這篇文章概述 SharePoint 伺服器陣列至 Azure 的 DPM/Azure 備份伺服器保護"
services: backup
documentationcenter: 
author: adigan
manager: Nkolli1
editor: 
ms.assetid: e0c0c252-dc1d-4072-b777-7222c13950b0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: adigan;giridham;jimpark;trinadhk;markgal
ms.openlocfilehash: 1bbf3233169fa9966e3dd0fac18ee448f26caa6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-a-sharepoint-farm-to-azure"></a>將 SharePoint 伺服器陣列備份到 Azure
您可以使用 System Center Data Protection Manager (DPM)，將 SharePoint 伺服器陣列備份到 Microsoft Azure，其方法與備份其他資料來源極為類似。 Azure 備份提供靈活的備份排程來建立每日、每週、每月或每年備份點，並可讓您針對各種備份點執行保留原則選項。 DPM 可讓您儲存本機磁碟複本來快速達成復原時間目標 (RTO)，也可以將複本儲存到 Azure 來進行經濟實惠的長期保留。

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>SharePoint 支援的版本與相關保護案例
DPM 的 Azure 備份支援下列案例：

| 工作負載 | 版本 | SharePoint 部署 | DPM 部署類型 | DPM - System Center 2012 R2 | 保護和復原 |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013、SharePoint 2010、SharePoint 2007、SharePoint 3.0 |部署為實體伺服器或 Hyper-V/VMware 虛擬機器的 SharePoint  <br> -------------- <br> SQL AlwaysOn |實體伺服器或內部部署 Hyper-V 虛擬機器 |支援從更新彙總套件 5 備份至 Azure |保護 SharePoint 伺服器陣列復原選項：來自磁碟復原點的復原伺服器陣列、資料庫及檔案或清單項目  來自 Azure 復原點的伺服器陣列和資料庫復原。 |

## <a name="before-you-start"></a>開始之前
您需要先確定幾件事，再將 SharePoint 伺服器陣列備份至 Azure。

### <a name="prerequisites"></a>必要條件
繼續之前，請確定 [使用 Microsoft Azure 備份來保護工作負載的所有必要條件](backup-azure-dpm-introduction.md#prerequisites) 已滿足。 一些滿足必要條件的工作包括︰建立備份保存庫、下載保存庫認證、安裝 Azure 備份代理程式，以及向保存庫註冊 DPM/Azure 備份伺服器。

### <a name="dpm-agent"></a>DPM 代理程式
DPM 代理程式必須安裝在執行 SharePoint 的伺服器、執行 SQL Server 的伺服器，以及隸屬於 SharePoint 伺服器陣列的其他任何伺服器上。 如需設定保護代理程式的詳細資訊，請參閱[設定保護代理程式](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx)。  唯一的例外是您只能在單一 Web 前端 (WFE) 伺服器上安裝代理程式。 DPM 只需要將 WFE 伺服器上的代理程式做為保護的進入點。

### <a name="sharepoint-farm"></a>SharePoint 伺服器陣列
針對伺服器陣列中每 1000 萬個項目，必須有至少 2 GB 的磁碟區空間來放置 DPM 資料夾。 此空間對目錄產生是必要的。 若要讓 DPM 復原特定項目 (網站集合、網站、清單、文件庫、資料夾、個別的文件與清單項目)，目錄產生會建立一份包含在每個內容資料庫內的 URL 清單。 您可以在 DPM 系統管理員主控台的 [復原]  工作區中，檢視 [可復原項目] 窗格中的 URL 清單。

### <a name="sql-server"></a>SQL Server
DPM 會以 LocalSystem 帳戶身分執行。 若要備份 SQL Server 資料庫，DPM 需要執行 SQL Server 之伺服器上該帳戶的 sysadmin 權限。 備份之前，將執行 SQL Server 之伺服器上的 NT AUTHORITY\SYSTEM 設定為 *sysadmin*。

如果 SharePoint 伺服器陣列有使用 SQL Server 別名設定的 SQL Server 資料庫，請在 DPM 將保護的前端 Web 伺服器上安裝 SQL Server 用戶端元件。

### <a name="sharepoint-server"></a>SharePoint Server
雖然效能取決於許多因素，例如 SharePoint 伺服器陣列的大小，但一般的做法是將一部 DPM 伺服器用來保護 25 TB SharePoint 伺服器陣列。

### <a name="dpm-update-rollup-5"></a>DPM 更新彙總套件 5
若要開始針對 Azure 保護 SharePoint 伺服器，您需要安裝 DPM 更新彙總套件 5 或更新版本。 更新彙總套件 5 提供針對 Azure 保護 SharePoint 伺服器陣列的功能 (如果已使用 SQL AlwaysOn 設定伺服器陣列)。
如需詳細資訊，請參閱介紹 [DPM 更新彙總套件 5](http://blogs.technet.com/b/dpm/archive/2015/02/11/update-rollup-5-for-system-center-2012-r2-data-protection-manager-is-now-available.aspx)

### <a name="whats-not-supported"></a>不支援的內容
* 保護 SharePoint 伺服器陣列的 DPM 不會保護搜尋索引或應用程式服務資料庫。 您必須個別設定這些資料庫的保護。
* DPM 不提供相應放大檔案伺服器 (SOFS) 共用所裝載的 SharePoint SQL Server 資料庫備份。

## <a name="configure-sharepoint-protection"></a>設定 SharePoint 保護
您必須先使用 **ConfigureSharePoint.exe**來設定「SharePoint VSS 寫入器」服務 (「WSS 寫入器」服務)，才能使用 DPM 來保護 SharePoint。

您可以在前端 Web 伺服器的 [DPM 安裝路徑]\bin 資料夾中找到 **ConfigureSharePoint.exe**。 這項工具可將 SharePoint 伺服器陣列的認證提供給保護代理程式。 您在單一 WFE 伺服器上執行。 如果您有多部 WFE 伺服器，在設定保護群組時請選取其中一部。

### <a name="to-configure-the-sharepoint-vss-writer-service"></a>設定 SharePoint VSS 寫入器服務
1. 在 WFE 伺服器上，在命令提示字元中移至 [DPM 安裝位置]\bin\
2. 輸入 ConfigureSharePoint -EnableSharePointProtection
3. 輸入伺服器陣列系統管理員認證。 這個帳戶應該是 WFE 伺服器上本機 Administrator 群組的成員。 如果伺服器陣列系統管理員不是本機系統管理員，請授與 WFE 伺服器上的下列權限：
   * 授與 DPM 資料夾的 WSS_Admin_WPG 群組完整控制權 (%Program Files%\Microsoft Data Protection Manager\DPM)。
   * 將 DPM 登錄機碼的讀取權授與 WSS_Admin_WPG 群組 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager)。

> [!NOTE]
> 每當 SharePoint 伺服器陣列系統管理員認證變更時，就必須重新執行 ConfigureSharePoint.exe。
> 
> 

## <a name="back-up-a-sharepoint-farm-by-using-dpm"></a>使用 DPM 備份 SharePoint 伺服器陣列
在設定 DPM 和 SharePoint 伺服器陣列 (如上所述) 之後，SharePoint 就可以受 DPM 保護。

### <a name="to-protect-a-sharepoint-farm"></a>保護 SharePoint 伺服器陣列
1. 從 [DPM 管理主控台] 的 [保護] 索引標籤中，按一下 [新增]。
    ![[新增保護] 索引標籤](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. 在 [建立新保護群組] 精靈的 [選擇保護群組類型] 頁面上，選取 [伺服器]，然後按 [下一步]。
   
    ![選擇保護群組類型](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. 在 [選擇群組成員] 畫面上，選取您想要保護的 SharePoint 伺服器的核取方塊，然後按 [下一步]。
   
    ![選擇群組成員](./media/backup-azure-backup-sharepoint/select-group-members2.png)
   
   > [!NOTE]
   > 在已安裝 DPM 代理程式的情況下，您會在精靈中看到伺服器。 DPM 也會顯示其結構。 由於已執行 ConfigureSharePoint.exe，DPM 會與 SharePoint VSS 寫入器服務及其對應的 SQL 資料庫通訊，並辨識 SharePoint 伺服器陣列結構、相關聯的內容資料庫和任何對應的項目。
   > 
   > 
4. 在 [選擇資料保護方式] 頁面上，輸入**保護群組**的名稱，然後選取您偏好的*保護方式*。 按一下 [下一步] 。
   
    ![選擇資料保護方式](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)
   
   > [!NOTE]
   > 磁碟保護方法有助於達成短暫的復原時間目標。 相較於磁帶，Azure 是經濟實惠的長期保護目標。 如需詳細資訊，請參閱 [使用 Azure 備份來取代您的磁帶基礎結構](https://azure.microsoft.com/documentation/articles/backup-azure-backup-cloud-as-tape/)
   > 
   > 
5. 在 [指定短期目標] 頁面上，選取您偏好的**保留範圍**，然後識別您想要進行備份的時間。
   
    ![指定短期目標](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)
   
   > [!NOTE]
   > 由於復原大部分是針對少於五天的資料進行，因此我們針對此範例選取磁碟上五天保留範圍，並確保在非生產時段進行備份。
   > 
   > 
6. 檢閱為保護群組配置的存放集區磁碟空間，然後按 [下一步] 。
7. 針對每個保護群組，DPM 會配置磁碟空間來儲存和管理複本。 此時，DPM 必須建立所選資料的複本。 選取您希望建立複本的方式和時間，然後按 [下一步] 。
   
    ![選擇複本的建立方式](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)
   
   > [!NOTE]
   > 若要確保不影響網路流量，請選取生產時段之外的時間。
   > 
   > 
8. DPM 可為複本執行一致性檢查，以確保資料完整性。 有兩個可用的選項。 您可以定義執行一致性檢查的排程，DPM 也可以在複本變得不一致時自動執行一致性檢查。 選取您慣用的選項，然後按 [下一步] 。
   
    ![一致性檢查](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. 在 [指定線上保護資料] 頁面上，選取您想要保護的 SharePoint 伺服器陣列，然後按 [下一步]。
   
    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. 在 [指定線上備份排程] 頁面上，選取您慣用的排程，然後按 [下一步]。
    
    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)
    
    > [!NOTE]
    > DPM 允許您在每天不同時間以 Azure 為目標執行兩次備份。 Azure 備份也可以利用 [Azure 備份網路節流](https://azure.microsoft.com/en-in/documentation/articles/backup-configure-vault/#enable-network-throttling)來控制尖峰和離峰時間用於備份的 WAN 頻寬。
    > 
    > 
11. 依選取的備份排程，請在 [ **指定線上保留原則** ] 頁面上，選取每日、每週、每月和每年備份點的保留原則。
    
    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)
    
    > [!NOTE]
    > DPM 會使用 grandfather-father-son 配置，可讓您為不同的備份時間點選擇不同的保留原則。
    > 
    > 
12. 類似於磁碟，需要在 Azure 中建立初始參考點複本。 選取用於在 Azure 中建立初始備份複本的慣用選項，然後按 [下一步] 。
    
    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. 在 [摘要] 頁面上檢閱您選取的設定，然後按一下 [建立群組]。 建立保護群組之後，您會看到成功訊息。
    
    ![摘要](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-dpm"></a>使用 DPM 從磁碟還原 SharePoint 項目
在下列範例中， *Recovering SharePoint item* 已被意外刪除，而需要復原。
![DPM SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. 開啟 [DPM 管理主控台] 。 DPM 保護的所有 SharePoint 伺服器陣列都會顯示在 [保護]  索引標籤中。
   
    ![DPM SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. 若要開始復原項目，請選取 [復原]  索引標籤。
   
    ![DPM SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. 您可以使用萬用字元型搜尋，在復原點範圍內搜尋 SharePoint 中的 *Recovering SharePoint item* 。
   
    ![DPM SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. 從搜尋結果中選取適當的復原點，以滑鼠右鍵按一下項目，然後選取 [復原]。
5. 您也可以瀏覽不同的復原點，並選取要復原的資料庫或項目。 選取 [日期] > [復原時間]，然後選取正確的 [資料庫] > [SharePoint 伺服器陣列] > [復原點] > [項目]。
   
    ![DPM SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. 在該項目上按一下滑鼠右鍵，然後選取 [復原] 以開啟 [復原精靈]。 按一下 [下一步] 。
   
    ![檢閱復原選項](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. 選取您想要執行的復原類型，然後按 [下一步] 。
   
    ![復原類型](./media/backup-azure-backup-sharepoint/select-recovery-type.png)
   
   > [!NOTE]
   > 範例中選取的 [復原到原始] 會將項目復原到原始的 SharePoint 網站。
   > 
   > 
8. 選取您想要使用的 [復原程序]  。
   
   * 如果 SharePoint 伺服器陣列並未變更，並且與正在還原的復原點相同，請選取 [不使用復原伺服器陣列執行復原]  。
   * 如果 SharePoint 伺服器陣列自建立復原點後已變更，請選取 [使用復原伺服器陣列執行復原]  。
     
     ![復原程序](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. 提供暫時復原資料庫的預備 SQL Server 執行個體位置，並在要復原項目的 DPM 伺服器和執行 SharePoint 的伺服器上提供預備檔案共用。
   
    ![Staging Location1](./media/backup-azure-backup-sharepoint/staging-location1.png)
   
    DPM 會將裝載 SharePoint 項目的內容資料庫附加至暫存 SQL Server 執行個體。 從內容資料庫，DPM 伺服器會復原項目，並將它放在 DPM 伺服器上的預備檔案位置。 在 DPM 伺服器預備位置上的復原項目，現在需要匯出至 SharePoint 伺服器陣列上的預備位置。
   
    ![Staging Location2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. 選取 [指定復原選項] ，並將安全性設定套用至 SharePoint 伺服器陣列，或套用復原點的安全性設定。 按一下 [下一步] 。
    
    ![修復選項](./media/backup-azure-backup-sharepoint/recovery-options.png)
    
    > [!NOTE]
    > 您可以選擇調節網路頻寬使用量。 這會對生產時段的生產伺服器產生最小的影響。
    > 
    > 
11. 檢閱摘要資訊，然後按一下 [復原]  以開始復原檔案。
    
    ![復原摘要](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. 現在，在 [DPM 管理主控台] 中選取 [監視] 索引標籤，以檢視復原的**狀態**。
    
    ![復原狀態](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)
    
    > [!NOTE]
    > 現在即可還原檔案。 您可以重新整理 SharePoint 網站來檢查已還原的檔案。
    > 
    > 

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>使用 DPM 從 Azure 中還原 SharePoint 資料庫
1. 若要復原 SharePoint 內容資料庫，請瀏覽各種復原點 (如上所示)，並選取要還原的復原點。
   
    ![DPM SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. 按兩下 SharePoint 復原點以顯示可用的 SharePoint 目錄資訊。
   
   > [!NOTE]
   > 由於 SharePoint 伺服器陣列在 Azure 中受長期保留保護，因此 DPM 伺服器上沒有可用的目錄資訊 (元資料)。 如此一來，每當需要復原時間點 SharePoint 內容資料庫，您就需要重新編目 SharePoint 伺服器陣列。
   > 
   > 
3. 按一下 [重新編目] 。
   
    ![DPM SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)
   
    [雲端重新編目]  狀態視窗隨即會開啟。
   
    ![DPM SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)
   
    完成編目後，狀態會變更為 [成功] 。 按一下 [關閉] 。
   
    ![DPM SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. 按一下 DPM [復原]  索引標籤中顯示的 SharePoint 物件，以取得內容資料庫結構。 在項目上按一下滑鼠右鍵，然後按一下 [復原] 。
   
    ![DPM SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. 此時，依照 [本文前述的復原步驟](#restore-a-sharepoint-item-from-disk-using-dpm) ，從磁碟復原 Sharepoint 內容資料庫。

## <a name="faqs"></a>常見問題集
問︰哪些版本的 DPM 支援 SQL Server 2014 和 SQL 2012 (SP2)？<br>
答︰DPM 2012 R2 更新彙總套件 4 支援兩者。

問：如果使用 SQL AlwaysOn (使用磁碟上保護) 設定 SharePoint，我是否能將 SharePoint 項目復原到原始位置？<br>
答：可以，項目可以復原到原始的 SharePoint 網站。

問：如果使用 SQL AlwaysOn 設定 SharePoint，我是否能將 SharePoint 資料庫復原到原始位置？<br>
答：由於 SharePoint 資料庫是在 SQL AlwaysOn 中設定，所以除非移除可用性群組，否則無法修改它們。 因此，DPM 無法將資料庫還原到原始位置。 您可以將 SQL Server 資料庫復原到其他 SQL Server 執行個體。

## <a name="next-steps"></a>後續步驟
* 深入了解 DPM 的 SharePoint 保護 - 請參閱 [影片系列 - DPM 的 SharePoint 保護](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
* 檢閱 [System Center 2012 - Data Protection Manager 版本資訊](https://technet.microsoft.com/library/jj860415.aspx)
* 檢閱 [System Center 2012 SP1 的 Data Protection Manager 版本資訊](https://technet.microsoft.com/library/jj860394.aspx)

