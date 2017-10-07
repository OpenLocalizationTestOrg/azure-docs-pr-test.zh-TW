---
title: "做為備份目標與備份 Exec aaaStorSimple 8000 系列 |Microsoft 文件"
description: "描述搭配 Veritas 備份 Exec hello StorSimple 備份目標組態。"
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a>使用 StorSimple 做為 Backup Exec 的備份目標

## <a name="overview"></a>概觀

Azure StorSimple 是 Microsoft 提供的混合式雲端儲存體解決方案。 StorSimple 位址為指數的資料成長的 hello 複雜性為 hello 在內部部署方案，以及自動分層資料的延伸的 Azure 儲存體帳戶使用跨內部部署儲存體和雲端儲存體。

在本文中，我們會討論 StorSimple 與 Veritas Backup Exec 的整合，以及整合這兩種解決方案的最佳作法。 我們也會進行有關如何設定備份 Exec toobest tooset 整合與 StorSimple 的建議事項。 我們延遲 tooVeritas 最佳作法、 備份架構設計人員和系統管理員的 hello 最佳方式 tooset 備份 Exec toomeet 個別的備份需求以及服務等級協定 (Sla)。

雖然我們會說明設定步驟和重要概念，但本文不是逐步的設定或安裝指南。 我們假設 hello 基本元件和基礎結構是在工作順序和準備 toosupport hello 概念，我們將描述。

### <a name="who-should-read-this"></a>哪些人應閱讀本文？

本文章中的 hello 資訊將會最有幫助 toobackup 系統管理員、 存放裝置系統管理員，以及儲存體架構設計人員了解儲存體、 Windows Server 2012 R2、 乙太網路、 雲端服務和備份 Exec。

## <a name="supported-versions"></a>支援的版本

-   [備份 Exec 16 及更新版本](http://backupexec.com/compatibility)
-   [StorSimple Update 3 及更新版本](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>為什麼使用 StorSimple 做為備份目標？

StorSimple 是不錯的備份目標選擇，因為︰

-   它提供標準的本機儲存體備份應用程式 toouse 做為快速備份的目的地，不進行任何變更。 您也可以將 StorSimple 用來快速還原最新的備份。
-   其雲端層與 Azure 雲端儲存體帳戶 toouse 順暢地整合符合成本效益的 Azure 儲存體。
-   自動提供可供災害復原的異地儲存體。

## <a name="key-concepts"></a>重要概念

如同任何儲存體解決方案，hello 方案的儲存體效能 Sla，仔細評估變更與容量成長需求的速率是重大 toosuccess。 hello 主要概念是，藉由引進雲端層，您的存取時間和輸送量 toohello 雲端扮演了基本角色 StorSimple toodo hello 能力其工作。

StorSimple 是設計的 tooprovide 儲存體 tooapplications 妥善定義的工作集的資料 （熱資料） 上運作。 在此模型中，hello 工作集的資料儲存在 hello 本機層，而且 hello 剩餘非/冷/封存的資料集是階層式的 toohello 雲端。 此模型會以 hello 遵循圖表示。 hello 幾乎單層綠色線條代表 hello hello 的 hello StorSimple 裝置的本機層上儲存的資料。 hello 紅線表示 hello 總儲存在 hello StorSimple 解決方案，跨所有階層的資料量。 hello 間距 hello 單層綠色線條和 hello 指數的紅色曲線表示 hello 的 hello 雲端中儲存的資料量總計。

**StorSimple 分層**
![StorSimple 分層圖](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)

請注意這種架構，與您會發現 StorSimple 是適合的 toooperate 做為備份目標。 您可以使用 StorSimple 進行下列作業：
-   執行您最常出現的還原從 hello 本機工作集的資料。
-   使用 hello 雲端異地災害復原和較舊的資料，其中還原就都是較不頻繁。

## <a name="storsimple-benefits"></a>StorSimple 的優點

StorSimple 提供順暢地整合 Microsoft Azure 與內部部署解決方案，藉由運用無縫存取 tooon 內部部署和雲端儲存體。

StorSimple 會使用自動 hello 在內部部署裝置，具有固態裝置 (SSD) 和序列連結 SCSI (SAS) 存放裝置，與 Azure 儲存體階層處理。 自動分層維持經常存取的本機 hello SSD 和 SAS 層上的資料。 它會移動不常存取的資料 tooAzure 儲存體。

StorSimple 提供下列優點︰

-   使用 hello 雲端 tooachieve 前所未有的重複資料刪除層級的唯一重複資料刪除和壓縮演算法
-   高可用性
-   使用 Azure 異地複寫進行異地複寫
-   與 Azure 整合
-   Hello 雲端中的資料加密
-   改進災害復原和提高合規性

雖然 StorSimple 展示兩個主要的部署案例 (主要備份目標和次要備份目標)，但基本上只是一般的區塊存放裝置。 壓縮和重複資料刪除，所有有 hello StorSimple 沒有。 順暢地傳送，並擷取 hello 雲端與 hello 應用程式和檔案系統之間的資料。

如需 StorSimple 的詳細資訊，請參閱 [StorSimple 8000 系列︰混合式雲端儲存體解決方案](storsimple-overview.md)。 此外，您可以檢閱 hello[技術 StorSimple 8000 系列規格](storsimple-technical-specifications-and-compliance.md)。

> [!IMPORTANT]
> 只有 StorSimple 8000 Update 3 或更新版本才支援使用 StorSimple 裝置做為備份目標。

## <a name="architecture-overview"></a>架構概觀

hello 下列表格顯示 hello 裝置模型-架構初始指導方針。

**StorSimple 的本機和雲端儲存體容量**

| 儲存體容量       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| 本機儲存體容量 | &lt; 10 TiB\*  | &lt; 20 TiB\*  |
| 雲端儲存體容量 | &gt; 200 TiB\* | &gt; 500 TiB\* |
\* 儲存體大小假設沒有重複資料刪除或壓縮。

**StorSimple 的主要和次要備份容量**

| 備份案例  | 本機儲存體容量  | 雲端儲存體容量  |
|---|---|---|
| 主要備份  | 最新的備份儲存在本機儲存體的快速復原 toomeet 復原點目標 (RPO) | 備份歷程記錄 (RPO) 可放入雲端容量 |
| 次要備份 | 備份資料的次要複本可儲存在雲端容量  | N/A  |

## <a name="storsimple-as-a-primary-backup-target"></a>使用 StorSimple 做為主要備份目標

在此案例中，StorSimple 磁碟區會呈現為 hello 備份的唯一儲存機制的 toohello 備份應用程式。 下列圖 hello 顯示中的所有備份使用 StorSimple 都分層磁碟區的備份和還原的方案架構。

![使用 StorSimple 做為主要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>主要目標備份的邏輯步驟

1.  hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。
2.  hello 備份伺服器將資料寫入 toohello StorSimple 分層磁碟區。
3.  hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。
4.  快照集指令碼觸發 hello StorSimple 雲端快照集管理員 （啟動或刪除）。
5.  hello 備份伺服器會刪除過期的備份保留原則為基礎。


### <a name="primary-target-restore-logical-steps"></a>主要目標還原的邏輯步驟

1.  hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。
2.  hello 備份代理程式接收 hello 備份伺服器 hello 資料。
3.  hello 備份伺服器會完成 hello 還原作業。

## <a name="storsimple-as-a-secondary-backup-target"></a>使用 StorSimple 做為次要備份目標

在此案例中，StorSimple 磁碟區主要用於長期保留或封存。

hello 下圖顯示的架構中的初始備份及還原高效能的目標磁碟區。 這些備份複製並封存的 tooa StorSimple 分層磁碟區上設定的排程。

它是重要的 toosize 高效能磁碟區，好讓它可以處理保留原則容量和效能需求。

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>次要目標備份的邏輯步驟

1.  hello 備份伺服器連絡人 hello 目標備份代理程式，並報告 hello 備份代理程式傳輸資料 toohello 備份伺服器。
2.  hello 備份伺服器寫入資料 toohigh 能儲存體。
3.  hello 備份伺服器更新 hello 類別目錄資料庫，並再完成 hello 備份工作。
4.  hello 備份伺服器複製備份 tooStorSimple 根據保留原則。
5.  快照集指令碼觸發 hello StorSimple 雲端快照集管理員 （啟動或刪除）。
6.  hello 備份伺服器會刪除過期的備份保留原則為基礎。

### <a name="secondary-target-restore-logical-steps"></a>次要目標還原的邏輯步驟

1.  hello 備份伺服器，開始從 hello 存放庫還原 hello 適當的資料。
2.  hello 備份代理程式接收 hello 備份伺服器 hello 資料。
3.  hello 備份伺服器會完成 hello 還原作業。

## <a name="deploy-hello-solution"></a>部署 hello 方案

部署 hello 方案需要三個步驟：
1. 準備 hello 網路基礎結構。
2. 部署您的 StorSimple 裝置做為備份目標。
3. 部署 Backup Exec。

每個步驟是在 hello 下列各節中詳細討論。

### <a name="set-up-hello-network"></a>設定 hello 網路

StorSimple 是與 hello Azure 雲端整合解決方案，因為 StorSimple 會需要使用中且正在運作的連線 toohello Azure 雲端。 作業，像是雲端快照、 管理和中繼資料傳輸和 tootier 較舊且較少存取的資料 tooAzure 雲端存放裝置，則使用此連接。

Hello 方案 tooperform 最佳情況是，我們建議您遵循這些網路的最佳作法：

-   連接您的 StorSimple 分層 tooAzure hello 連結必須符合您的頻寬需求。 tooachieve，套用 hello 必要服務品質 (QoS) 層級 tooyour 基礎結構交換器 toomatch 您 RPO 和復原時間目標 (RTO) Sla。
-   最大的 Azure Blob 儲存體存取延遲時間應該大約 80 毫秒。

### <a name="deploy-storsimple"></a>部署 StorSimple

如需 StorSimple 部署的逐步指引，請參閱[部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough-u2.md)。

### <a name="deploy-backup-exec"></a>部署 Backup Exec

如需 Backup Exec 安裝最佳作法，請參閱 [Backup Exec 安裝的最佳作法](https://www.veritas.com/support/en_US/article.000068207)。

## <a name="set-up-hello-solution"></a>設定 hello 解決方案

在本節中，我們會示範一些組態範例。 hello 下列的範例和建議事項說明 hello 最基本也最基本的實作。 此實作中可能不適用，直接 tooyour 特定的備份需求。

### <a name="set-up-storsimple"></a>設定 StorSimple

| StorSimple 部署工作  | 其他註解 |
|---|---|
| 部署您的內部部署 StorSimple 裝置。 | 支援的版本：Update 3 及更新版本。 |
| 開啟 hello 備份目標。 | 使用這些命令 tooturn 上或備份的目標模式和 tooget 狀態為關閉。 如需詳細資訊，請參閱[遠端連線 tooa StorSimple 裝置](storsimple-remote-connect.md)。</br> 備份模式 tooturn: `Set-HCSBackupApplianceMode -enable`。 </br> 備份模式關閉 tooturn: `Set-HCSBackupApplianceMode -disable`。 </br> tooget hello 目前狀態的備份模式設定： `Get-HCSBackupApplianceMode`。 |
| 建立您將 hello 備份資料儲存的磁碟區的一般磁碟區容器。 磁碟區容器中的所有資料都已刪除重複資料。 | StorSimple 磁碟區容器定義重複資料刪除網域。  |
| 建立 StorSimple 磁碟區。 | 建立磁碟區大小為預期的關閉 toohello 使用量越好，因為磁碟區大小會影響雲端快照集的持續時間。 如需有關資訊 toosize 磁碟區，閱讀有關[保留原則](#retention-policies)。</br> </br> 使用 StorSimple 分層磁碟區，並選取 hello**對於不常存取的封存資料，使用此磁碟區**核取方塊。 </br> 不支援只使用固定在本機的磁碟區。 |
| 建立所有 hello 備份目標磁碟區的唯一 StorSimple 備份原則。 | StorSimple 的備份原則定義 hello 磁碟區一致性群組。 |
| 停用 hello 排程，因為到期 hello 快照集。 | 後處理作業會觸發快照集。 |

### <a name="set-up-hello-host-backup-server-storage"></a>設定 hello 主機備份伺服器儲存體

設定 hello 主機備份伺服器儲存體，根據 toothese 指導方針：  

- 不要使用合併磁碟區 (由 Windows 磁碟管理所建立)。 不支援合併磁碟。
- 使用 64 KB 配置大小的 NTFS 格式化磁碟區。
- 對應 hello StorSimple 磁碟區直接 toohello Exec 備份伺服器。
    - 為實體伺服器使用 iSCSI。
    - 虛擬伺服器請使用傳遞磁碟。

## <a name="best-practices-for-storsimple-and-backup-exec"></a>StorSimple 和 Backup Exec 的最佳作法

設定您的解決方案，根據下列各節的 hello toohello 指導方針。

### <a name="operating-system-best-practices"></a>作業系統最佳作法

-   停用 Windows Server 的加密和 hello NTFS 檔案系統的重複資料刪除。
-   停用 hello StorSimple 磁碟區上的 Windows 伺服器磁碟重組。
-   停用 Windows hello 索引 StorSimple 磁碟區的伺服器。
-   在 hello （不是針對 hello StorSimple 磁碟區） 的來源主機上執行的防毒掃描。
-   關閉 hello 預設[Windows Server 維護](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx)工作管理員 中。 執行下列其中一 hello 下列方法：
   - 關閉 Windows 工作排程器中的 hello 維護 configurator。
   - 從 Windows Sysinternals 下載 [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx)。 下載 PsExec 之後，請以系統管理員身分執行 Azure PowerShell：
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>StorSimple 最佳作法

  -   請務必更新該 hello StorSimple 裝置時太[Update 3 或更新版本](storsimple-install-update-3.md)。
  -   隔離 iSCSI 和雲端流量。 您可以使用專用的 iSCSI 連線的 StorSimple 與 hello 備份的伺服器之間的流量。
  -   確定 StorSimple 裝置是專用的備份目標。 不支援混合的工作負載，因為它們會影響 RTO 和 RPO。

### <a name="backup-exec-best-practices"></a>Backup Exec 最佳作法

-   Hello 伺服器的本機磁碟機上，而不是在 StorSimple 磁碟區，則必須安裝備份執行。
-   設定 hello 備份 Exec 儲存**並行寫入作業**toohello 最大允許。
    -   設定 hello 備份 Exec 儲存**區塊和緩衝區大小**too512 KB。
    -   開啟 Backup Exec 儲存體的**緩衝讀取和寫入**。
-   StorSimple 支援 Backup Exec 完整和增量備份。 建議您不要使用綜合和差異備份。
-   備份資料檔案最好只包含特定作業的資料。 例如，不允許在不同作業之間附加媒體。
-   停用作業驗證。 如有必要，都應該排程驗證 hello 最新的備份作業之後。 這項作業會影響您的備份時間範圍的重要 toounderstand 它。
-   選取 [儲存體] > 您的磁碟 > [詳細資料] > [屬性]。 關閉 [預先配置磁碟空間]。

Hello 最新的備份 Exec 設定及實作這些需求的最佳作法，請參閱[hello Veritas 網站](https://www.veritas.com)。

## <a name="retention-policies"></a>保留原則

Hello 最常見的備份保留原則類型的其中一個是祖父、 父親和 Son (GFS) 原則。 在 GFS 原則中，增量備份會每日執行，而完整備份會每週和每月進行。 此原則會產生六個 StorSimple 分層磁碟區。 一個磁碟區包含 hello 每週、 每月和每年完整備份。 hello 其他五個磁碟區儲存每日增量備份。

在下列範例的 hello，我們會使用 GFS 旋轉。 hello 範例假設 hello 下列：

-   使用非重複資料刪除或壓縮的資料。
-   每個完整備份為 1 TiB。
-   每個每日增量備份為 500 GiB。
-   四個每週備份會保留一個月。
-   十二個每月備份會保留一年。
-   一個每年備份會保留 10 年。

根據上述假設 hello，建立 26 TiB StorSimple 分層 hello 每月和每年完整備份的磁碟區。 建立 5 TiB StorSimple hello 的每日增量備份的每個分層磁碟區。

| 備份類型保留期 | 大小 (TiB) | GFS 乘數\* | 總容量 (TiB)  |
|---|---|---|---|
| 每週完整 | 1 | 4  | 4 |
| 每日增量 | 0.5 | 20 (循環數等於每個月的週數) | 12 (2 為其他配額) |
| 每月完整 | 1 | 12 | 12 |
| 每年完整 | 1  | 10 | 10 |
| GFS 需求 |   | 38 |   |
| 其他配額  | 4  |   | 42 (總計 GFS 需求)  |
\*hello GFS 乘數是 hello 的數字的複本需要 tooprotect 和保留 toomeet 您備份原則的需求。

## <a name="set-up-backup-exec-storage"></a>設定 Backup Exec 儲存體

### <a name="tooset-up-backup-exec-storage"></a>tooset 備份 Exec 存放裝置

1.  在 hello 備份 Exec 管理主控台中，選取 **儲存體** > **設定儲存體** > **磁碟型儲存裝置** >  **下一步**。

    ![Backup Exec 管理主控台，設定儲存體頁面](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  選取 [磁碟儲存體]，然後選取 [下一步]。

    ![Backup Exec 管理主控台，選取儲存體頁面](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  輸入一個代表性名稱，例如，「星期六完整」和描述。 選取 [下一步] 。

    ![Backup Exec 管理主控台，名稱和描述頁面](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  您想 toocreate hello 磁碟存放裝置，然後選取選取 hello 磁碟**下一步**。

    ![Backup Exec 管理主控台，儲存體磁碟選取頁面](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  遞增 hello 寫入作業數目太**16**，然後選取**下一步**。

    ![Backup Exec 管理主控台，並行寫入作業設定頁面](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  檢閱 hello 設定，然後選取**完成**。

    ![Backup Exec 管理主控台，儲存體組態摘要頁面](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  在每個磁碟區指派 hello 最後，變更這些建議您在 hello 存放裝置設定 toomatch [StorSimple 和備份 Exec 最佳作法](#best-practices-for-storsimple-and-backup-exec)。

    ![Backup Exec 管理主控台，存放裝置設定頁面](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  重複步驟 1 到 7，直到完成指派您的 StorSimple 磁碟區 tooBackup Exec。

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>設定 StorSimple 做為主要備份目標

> [!NOTE]
> 從已分層式的 toohello 雲端備份資料還原就會發生在雲端的速度。

hello 下圖顯示典型的磁碟區 tooa 備份工作的 hello 對應。 在此情況下，所有的 hello 每週備份對應 toohello 星期六磁碟已滿，而 hello 增量備份對應 tooMonday 星期五累加磁碟。 所有 hello 備份與還原就都是從 StorSimple 分層磁碟區。

![主要備份目標組態的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>使用 StorSimple 做為主要備份目標的 GFS 排程範例

以下是四週、每月和每年的 GFS 循環排程範例：

| 頻率/備份類型 | 完整 | 增量 (第 1-5 天)  |   
|---|---|---|
| 每週 (第 1 - 4 週) | 星期六 | 星期一至星期五 |
| 每月  | 星期六  |   |
| 每年 | 星期六  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a>指派 StorSimple 磁碟區 tooa 備份執行備份工作

hello 下列程序會假設該備份 Exec 和 hello 的目標主機設定依據 hello 備份 Exec 代理程式的指導方針。

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a>tooassign StorSimple 磁碟區 tooa 備份執行備份作業

1.  在 hello 備份 Exec 管理主控台中，選取 **主機** > **備份** > **備份 tooDisk**。

    ![備份 Exec 管理主控台中，選取主機上，備份，和備份 toodisk](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  在 hello**備份定義屬性**對話方塊的 **備份**，選取**編輯**。

    ![Backup Exec 管理主控台，備份定義屬性對話方塊](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  設定完整和增量備份，以便符合您的 RPO 和 RTO 需求並符合 tooVeritas 最佳作法。

4.  在 hello**備份選項**對話方塊中，選取**儲存體**。

    ![Backup Exec 管理主控台，備份選項、儲存體對話方塊](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  指派對應 StorSimple 磁碟區 tooyour 備份排程。

    > [!NOTE]
    > **壓縮**和**加密類型**設定得**無**。

6.  在下**確認**，選取 hello**不會驗證此作業的資料**核取方塊。 使用此選項可能會影響 StorSimple 分層。

    > [!NOTE]
    > 磁碟重組、 索引和背景驗證造成負面影響 hello StorSimple 階層處理。

    ![Backup Exec 管理主控台，備份選項、驗證設定](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  當您設定的備份選項 toomeet hello rest 您的需求時，選取**確定**toofinish。

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>設定 StorSimple 做為次要備份目標

> [!NOTE]
>從已分層式的 toohello 雲端備份資料還原發生在雲端的速度。

在此模型中，您必須擁有儲存媒體 （非 StorSimple) tooserve 暫時快取。 例如，您可以使用獨立磁碟 (RAID) 磁碟區 tooaccommodate 空間、 輸入/輸出 (I/O) 和頻寬的備援陣列。 我們建議使用 RAID 5、50 和 10。

hello 下圖顯示典型短期保留本機 （toohello 伺服器） 的磁碟區和長期的保留封存磁碟區。 在此案例中，所有備份上都執行本機 hello （toohello 伺服器） RAID 磁碟區。 定期重複這些備份和封存的 tooan 封存磁碟區。 它是本機 （toohello 伺服器） 的重要 toosize RAID 磁碟區，好讓它可以處理短期保留容量和效能需求。

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>使用 StorSimple 做為次要備份目標 GFS 範例

![使用 StorSimple 做為次要備份目標的邏輯圖](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

hello 下表顯示如何 tooset 向上備份 toorun hello 本機和 StorSimple 磁碟上。 其中包含個別和總容量需求。

### <a name="backup-configuration-and-capacity-requirements"></a>備份設定和容量需求

| 備份類型和保留期 | 設定的儲存體 | 大小 (TiB) | GFS 乘數 | 總容量\* (TiB) |
|---|---|---|---|---|
| 第 1 週 (完整和增量) |本機磁碟 (短期)| 1 | 1 | 1 |
| StorSimple 第 2-4 週 |StorSimple 磁碟 (長期) | 1 | 4 | 4 |
| 每月完整 |StorSimple 磁碟 (長期) | 1 | 12 | 12 |
| 每年完整 |StorSimple 磁碟 (長期) | 1 | 1 | 1 |
|GFS 磁碟區大小需求 |  |  |  | 18*|
\* 總容量包含 17 TiB 的 StorSimple 磁碟和 1 TiB 的本機 RAID 磁碟區。


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>GFS 範例排程：每週、每月和每年排程的 GFS 循環

| 週 | 完整 | 增量 (第 1 天) | 增量 (第 2 天) | 增量 (第 3 天) | 增量 (第 4 天) | 增量 (第 5 天) |
|---|---|---|---|---|---|---|
| 第 1 週 | 本機 RAID 磁碟區  | 本機 RAID 磁碟區 | 本機 RAID 磁碟區 | 本機 RAID 磁碟區 | 本機 RAID 磁碟區 | 本機 RAID 磁碟區 |
| 第 2 週 | StorSimple 第 2-4 週 |   |   |   |   |   |
| 第 3 週 | StorSimple 第 2-4 週 |   |   |   |   |   |
| 第 4 週 | StorSimple 第 2-4 週 |   |   |   |   |   |
| 每月 | StorSimple 每月 |   |   |   |   |   |
| 每年 | StorSimple 每年  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a>指派 StorSimple 磁碟區 tooa 備份 Exec 封存及重複資料刪除工作

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a>tooassign StorSimple 磁碟區 tooa 備份 Exec 封存和複製作業

1.  在 hello 備份 Exec 管理主控台中，以滑鼠右鍵按一下您想 tooarchive tooa StorSimple 磁碟區，然後選取 hello 作業**備份定義屬性** > **編輯**。

    ![Backup Exec 管理主控台，備份定義屬性索引標籤](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  選取**新增階段** > **重複 tooDisk** > **編輯**。

    ![Backup Exec 管理主控台，新增階段](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  在 hello**重複選項**對話方塊中，您想要針對 toouse 選取 hello 值**來源**和**排程**。

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  在 hello**儲存體**下拉式清單中，選取 hello hello 封存作業 toostore hello 資料所在的 StorSimple 磁碟區。

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  選取**確認**，然後選取 hello**不會驗證此作業的資料**核取方塊。

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  選取 [確定] 。

    ![Backup Exec 管理主控台，備份定義屬性和複製選項](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  在 hello**備份**資料行，將新的階段。 Hello 來源使用**累加**。 Hello 目標，選擇 hello hello 增量備份工作會封存位置的 StorSimple 磁碟區。 重複步驟 1 至 6。

## <a name="storsimple-cloud-snapshots"></a>StorSimple 雲端快照集

StorSimple 雲端快照集保護位於您的 StorSimple 裝置中的 hello 資料。 建立雲端快照集是對等 tooshipping 本機備份磁帶 tooan 異地設施。 如果您使用 Azure 地理備援儲存體，建立雲端快照是相等的 tooshipping 備份磁帶 toomultiple 站台。 如果您需要 toorestore 裝置在損毀之後，您可能會讓其他 StorSimple 裝置上線，並且進行容錯移轉。 Hello 容錯移轉之後，您將無法 tooaccess hello 資料 （速度雲端） 從 hello 最新的雲端快照集。

hello 下列章節描述如何 toocreate 簡短的指令碼 toostart 和 delete StorSimple 雲端快照在備份後的處理期間。

> [!NOTE]
> 手動或以程式設計方式建立的快照集未遵循 hello StorSimple 快照集的到期原則。 這些快照集必須以手動方式或以程式設計方式刪除。

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>使用指令碼啟動和刪除雲端快照集

> [!NOTE]
> 請仔細在刪除 StorSimple 快照集之前，先評估 hello 相容性和資料保留的影響。 如需有關如何 toorun 備份後指令碼，請參閱 hello[備份 Exec 文件](https://www.veritas.com/support/en_US/15047.html)。

### <a name="backup-lifecycle"></a>備份生命週期

![備份生命週期圖表](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a>需求

-   執行 hello 指令碼的 hello 伺服器必須具備存取 tooAzure 雲端資源。
-   hello 使用者帳戶必須擁有 hello 必要的權限。
-   StorSimple hello 與備份原則相關聯的 StorSimple 磁碟區必須設定，但未開啟。
-   您將需要 hello StorSimple 資源名稱、 登錄機碼、 裝置名稱和備份原則的識別碼。

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart 或刪除的雲端快照

1.  [安裝 Azure PowerShell](/powershell/azure/overview)。
2.  [下載和匯入發佈設定和訂用帳戶資訊](https://msdn.microsoft.com/library/dn385850.aspx)。
3.  在 hello Azure 傳統入口網站中取得 hello 資源名稱和[StorSimple Manager 服務登錄機碼](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key)。
4.  Hello 在伺服器上執行 hello 指令碼，請以系統管理員身分執行 PowerShell。 輸入此命令：

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    請注意 hello 備份原則的識別碼。
5.  在記事本中，請使用下列程式碼的 hello 以建立新的 PowerShell 指令碼。

    複製並貼上此程式碼片段：
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Hello PowerShell 指令碼 toohello 儲存相同的位置儲存您的 Azure 發行設定。 例如，儲存為 C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1。
6.  在備份 Exec 增加 hello 指令碼 tooyour 備份工作，請編輯您備份執行的工作選項的前置處理和後置處理指令。

    ![Backup Exec 主控台，備份選項，前處理和後處理命令索引標籤](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> 我們建議做為後置處理指令碼執行 StorSimple 雲端快照集備份原則，在您每日備份工作的 hello 結尾處。 如需有關如何向上 tooback 和還原您備份應用程式環境 toohelp 您符合您的 RPO 和 RTO，請參閱與您備份的架構設計人員。

## <a name="storsimple-as-a-restore-source"></a>使用 StorSimple 做為還原來源

從 StorSimple 裝置還原的運作方式就如同從任何區塊存放裝置還原。 還原的是階層式的 toohello 雲端的資料就會發生在雲端的速度。 對於本機資料，還原發生 hello 裝置 hello 本機磁碟速度。 如需有關資訊 tooperform 還原，請參閱 hello 備份 Exec 文件。 我們建議您符合 tooBackup Exec 還原最佳作法。

## <a name="storsimple-failover-and-disaster-recovery"></a>StorSimple 容錯移轉和災害復原

> [!NOTE]
> 對於備份目標的案例，不支援使用 StorSimple Cloud Appliance 做為還原目標。

各種因素都可能造成災害。 hello 下表列出常見的嚴重損壞修復案例。

| 案例 | 影響 | 如何 toorecover | 注意事項 |
|---|---|---|---|
| StorSimple 裝置故障 | 備份和還原作業會中斷。 | 取代 hello 失敗的裝置，並執行[StorSimple 容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。 | 如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取完整的資料工作集。 所有作業都會以雲端速度進行。 hello 編製索引及編目重新掃描程序可能會導致所有備份組 toobe 掃描並取自 hello 雲端層 toohello 本機裝置層，這可能會很費時的程序。 |
| Backup Exec 伺服器故障 | 備份和還原作業會中斷。 | 重建 hello 備份伺服器和執行中所述的資料庫還原[如何 toodo 手動備份和還原的備份 Exec (BEDB) 資料庫](http://www.veritas.com/docs/000041083)。 | 您必須重建或還原 hello 備份 Exec hello 災害復原站台伺服器。 還原 hello 資料庫 toohello 最新的點。 如果 hello 還原備份執行的資料庫不是最新的備份工作，同步索引和編目不需要。 此索引和重新掃描程序的目錄，可能會導致所有備份組 toobe 掃描，並從 hello 雲端層 toohello 本機裝置層提取。 這會更耗費時間。 |
| 站台失敗所產生的 hello 備份伺服器和 StorSimple hello 遺失。 | 備份和還原作業會中斷。 | 先還原 StorSimple，然後再還原 Backup Exec。 | 先還原 StorSimple，然後再還原 Backup Exec。 如果您需要 tooperform 還原裝置復原後，從 hello 雲端 toohello 新裝置擷取 hello 完整的資料工作集。 所有作業都會以雲端速度進行。 |

## <a name="references"></a>參考

下列文件的 hello 時參考這個發行項：

- [StorSimple 多重路徑 I/O 設定](storsimple-configure-mpio-windows-server.md)
- [儲存體案例︰精簡佈建 (英文)](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [使用 GPT 磁碟機 (英文)](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [設定共用資料夾的陰影複製](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>後續步驟

- 深入了解如何太[從備份集還原](storsimple-restore-from-backup-set-u2.md)。
- 深入了解如何 tooperform[裝置容錯移轉和災害復原](storsimple-device-failover-disaster-recovery.md)。
