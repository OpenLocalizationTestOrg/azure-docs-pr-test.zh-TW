---
title: "aaaSQL Server 可用性群組-Azure 虛擬機器-教學課程 |Microsoft 文件"
description: "本教學課程示範如何 toocreate SQL Server Alwayson 可用性群組在 Azure 虛擬機器。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>在 Azure VM 中手動設定 Always On 可用性群組

本教學課程示範如何 toocreate SQL Server Alwayson 可用性群組在 Azure 虛擬機器。 hello 完整的教學課程與兩個 SQL 伺服器上的資料庫複本建立可用性群組。

**估計時間**： 滿足 hello 必要條件之後，會採用約 30 分鐘 toocomplete。

hello 圖表說明您在 hello 教學課程中所建置。

![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>必要條件

hello 教學課程假設您有基本了解 SQL Server Always On 可用性群組。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組概觀 (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx)。

hello 下表列出您在開始本教學課程之前，需要 toocomplete hello 必要條件：

|  |需求 |說明 |
|----- |----- |----- |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | 兩部 SQL Server | - 在 Azure 可用性設定組中 <br/> - 在單一網域中 <br/> - 已安裝「容錯移轉叢集」功能 |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | 叢集見證的檔案共用 |  
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server 服務帳戶 | 網域帳戶 |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|SQL Server Agent 服務帳戶 | 網域帳戶 |  
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|防火牆連接埠開啟 | - SQL Server：**1433** (用於預設執行個體) <br/> - 資料庫鏡像端點：**5022** 或任何可用的連接埠 <br/> - Azure Load Balancer 探查：**59999** 或任何可用的連接埠 |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|新增容錯移轉叢集功能 | 兩部 SQL Server 都需要此功能 |
|![正方形](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|安裝網域帳戶 | - 每部 SQL Server 上的本機系統管理員 <br/> - 每個 SQL Server 執行個體之 SQL Server sysadmin 固定伺服器角色的成員  |


在開始 hello 教學課程之前，您需要太[完成建立 Azure 虛擬機器中的 Alwayson 可用性群組的必要條件](virtual-machines-windows-portal-sql-availability-group-prereq.md)。 如果這些必要元件都已完成之後，您可以跳過[建立叢集](#CreateCluster)。


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##建立 hello 叢集

Hello 完成必要條件之後, hello 第一個步驟是 toocreate Windows Server 容錯移轉叢集，其中包含兩個 SQL 伺服器和見證伺服器。  

1. RDP toohello 第一個 SQL Server 使用 SQL 伺服器和 hello 見證伺服器的系統管理員的網域帳戶。

   >[!TIP]
   >如果您遵循 hello[先決條件的文件](virtual-machines-windows-portal-sql-availability-group-prereq.md)，建立名為帳戶**CORP\Install**。 請使用此帳戶。

2. 在 hello**伺服器管理員**儀表板，選取**工具**，然後按一下**容錯移轉叢集管理員**。
3. Hello 左窗格中，以滑鼠右鍵按一下**容錯移轉叢集管理員**，然後按一下**建立叢集**。
   ![建立叢集](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. 在 hello 建立叢集精靈 」 中建立單一節點叢集逐步進行 hello 頁面中的 hello 下表中的 hello 設定：

   | Page | 設定 |
   | --- | --- |
   | 開始之前 |使用預設值 |
   | 選取伺服器 |中的第一個 SQL Server 名稱的型別 hello**輸入伺服器名稱**按一下**新增**。 |
   | 驗證警告 |選取**否。 我不需要此群集中，來自 Microsoft 的支援和不想 toorun hello 驗證測試。當我按 [下一步] 時，繼續建立 hello 叢集**。 |
   | 用於管理 hello 叢集存取點 |在 [叢集名稱] 中輸入叢集名稱，例如 **SQLAGCluster1**。|
   | 確認 |除非您使用的是儲存空間，否則請使用預設值。 請參閱本表格後的 hello 附註。 |

### <a name="set-hello-cluster-ip-address"></a>設定 hello 叢集 IP 位址

1. 在**容錯移轉叢集管理員**，向下捲動太**叢集核心資源**展開 hello 叢集詳細資料。 您應該會看到這兩個 hello**名稱**和 hello **IP 位址**hello 中的資源**失敗**狀態。 hello IP 位址資源無法上線 hello 叢集指派 hello 因為 IP 位址為 hello 機器本身相同，因此它是重複的位址。

2. 以滑鼠右鍵按一下失敗的 hello **IP 位址**資源，然後再按一下**屬性**。

   ![叢集屬性](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. 選取**靜態 IP 位址**並指定從 hello SQL Server 會處於 hello 位址 文字方塊中的子網路的可用位址。 然後按 [下一步] 。
4. 在 hello**叢集核心資源**區段中以滑鼠右鍵按一下叢集名稱，然後按一下**上線**。 然後等待兩個資源上線。 當 hello 叢集名稱資源上線時，它會以新的 AD 電腦帳戶更新 hello DC 伺服器。 使用這個 AD 帳戶 toorun hello 稍後可用性群組的叢集服務。

### <a name="addNode"></a>新增 hello 其他 SQL Server toocluster

新增 hello 其他 SQL Server toohello 叢集。

1. Hello 瀏覽器樹狀目錄中，以滑鼠右鍵按一下 hello 叢集，然後按一下**加入節點**。

    ![新增節點 toohello 叢集](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. 在 hello**新增節點精靈**，按一下 **下一步**。 在 hello**選取伺服器**頁面上，新增 hello 第二個 SQL Server。 中的型別 hello 伺服器名稱**輸入伺服器名稱**，然後按一下**新增**。 完成之後，按 [下一步]。

1. 在 hello**驗證警告**頁面上，按一下**否**（在生產案例中您應該執行 hello 驗證測試）。 然後按 [下一步] 。

8. 在 hello**確認**頁面上，如果您使用儲存空間，清除 hello 核取方塊標示為**新增所有合格的存放裝置 toohello 叢集。**

   ![新增節點確認](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >如果您使用儲存空間，且未取消選取**新增所有合格的存放裝置 toohello 叢集**，Windows hello 叢集程序期間中斷 hello 虛擬磁碟。 如此一來，它們沒有出現在 磁碟管理員 或 檔案總管，直到從 hello 叢集中移除 hello 儲存空間，並使用 PowerShell 將其重新附加。 儲存空間將 toostorage 集區中的多個磁碟。 如需詳細資訊，請參閱[儲存空間](https://technet.microsoft.com/library/hh831739)。

1. 按一下 [下一步] 。

1. 按一下 [完成] 。

   容錯移轉叢集管理員 會顯示您的叢集有新的節點，並列出在 hello**節點**容器。

10. 登出 hello 遠端桌面工作階段。

### <a name="add-a-cluster-quorum-file-share"></a>新增叢集仲裁檔案共用

在此範例中 hello Windows 叢集會使用檔案共用 toocreate 叢集仲裁。 本教學課程使用「節點與檔案共用多數」仲裁。 如需詳細資訊，請參閱[了解容錯移轉叢集中的仲裁設定](http://technet.microsoft.com/library/cc731739.aspx)。

1. 使用遠端桌面工作階段連線 toohello 檔案共用見證成員伺服器。

1. 在 [伺服器管理員] 上，按一下 [工具]。 開啟 [電腦管理]。

1. 按一下 [共用資料夾]。

1. 在 共用 上按一下滑鼠右鍵，然後按一下新增共用。

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   使用**建立共用資料夾精靈**toocreate 共用。

1. 在**資料夾路徑**，按一下 **瀏覽**並找出或建立 hello 共用資料夾的路徑。 按一下 [下一步] 。

1. 在**名稱、 描述和設定**確認 hello 共用名稱和路徑。 按一下 [下一步] 。

1. 在 [共用資料夾權限] 上，設定 [自訂權限]。 按一下 [自訂]。

1. 在 [自訂權限] 上，按一下 [新增]。

1. 請確定該 hello 使用帳戶 toocreate hello 叢集中擁有完整控制權。

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. 按一下 [確定] 。

1. 在 [共用資料夾權限] 中，按一下 [完成]。 再次按一下 [完成]。  

1. 登出伺服器 hello

### <a name="configure-cluster-quorum"></a>設定叢集仲裁

接下來，設定 hello 叢集仲裁。

1. 使用遠端桌面連線 toohello 第一個叢集節點。

1. 在**容錯移轉叢集管理員**hello 叢集上按一下滑鼠右鍵，指向太**其他動作**，然後按一下**設定叢集仲裁設定...**.

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. 在「設定叢集仲裁精靈」中，按 [下一步]。

1. 在**選取仲裁設定選項**，選擇**選取 hello 仲裁見證**，然後按一下**下一步**。

1. 在 [選取仲裁見證] 上，按一下 [設定檔案共用見證]。

   >[!TIP]
   >Windows Server 2016 支援雲端見證。 如果您選擇此類型的見證，就不需要檔案共用見證。 如需詳細資訊，請參閱[為容錯移轉叢集部署雲端見證 (Deploy a cloud witness for a Failover Cluster)](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)。 本教學課程使用檔案共用見證，這是舊版作業系統所支援的類型。

1. 在**設定檔案共用見證**，您所建立的 hello 共用的型別 hello 路徑。 按一下 [下一步] 。

1. 在確認 hello 設定**確認**。 按一下 [下一步] 。

1. 按一下 [完成] 。

hello 叢集核心資源設定檔案共用見證。

## <a name="enable-availability-groups"></a>啟用可用性群組

接下來，啟用 hello **AlwaysOn 可用性群組**功能。 在兩部 SQL Server 上執行這些步驟。

1. 從 hello**啟動**畫面上，啟動**SQL Server 組態管理員**。
2. 在 hello 瀏覽器樹狀目錄中，按一下  **SQL Server 服務**，然後以滑鼠右鍵按一下 hello **SQL Server (MSSQLSERVER)**服務，然後按一下**屬性**。
3. 按一下 hello **AlwaysOn 高可用性**索引標籤，然後選取**啟用 AlwaysOn 可用性群組**、，如下所示：

    ![啟用 AlwaysOn 可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. 按一下 [Apply (套用)] 。 按一下**確定**hello 快顯對話方塊中。

5. 重新啟動 hello SQL Server 服務。

上重複這些步驟 hello 其他 SQL Server。

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Hello 上建立資料庫第一次的 SQL Server

1. 第一個 SQL Server 的網域帳戶也就是啟動 hello RDP 檔案 toohello 屬於 sysadmin 固定伺服器角色。
1. 開啟 SQL Server Management Studio 並連接 toohello 第一個 SQL Server。
7. 在 物件總管 中，於 資料庫 上按一下滑鼠右鍵，然後按一下新增資料庫。
8. 在 [資料庫名稱] 中，輸入 **MyDB1**，然後按一下 [確定]。

### <a name="backupshare"></a> 建立備份共用

1. 在 hello 中的第一個 SQL Server**伺服器管理員**，按一下 **工具**。 開啟 [電腦管理]。

1. 按一下 [共用資料夾]。

1. 在 共用 上按一下滑鼠右鍵，然後按一下新增共用。

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   使用**建立共用資料夾精靈**toocreate 共用。

1. 在**資料夾路徑**，按一下 **瀏覽**並找出或建立 hello 資料庫的備份共用資料夾的路徑。 按一下 [下一步] 。

1. 在**名稱、 描述和設定**確認 hello 共用名稱和路徑。 按一下 [下一步] 。

1. 在 [共用資料夾權限] 上，設定 [自訂權限]。 按一下 [自訂]。

1. 在 [自訂權限] 上，按一下 [新增]。

1. 請確定這兩部伺服器的 hello SQL Server 和 SQL Server Agent 服務帳戶具有完整控制權。

   ![新增共用](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. 按一下 [確定] 。

1. 在 [共用資料夾權限] 中，按一下 [完成]。 再次按一下 [完成]。  

### <a name="take-a-full-backup-of-hello-database"></a>進行完整備份的 hello 資料庫

您需要 tooback hello 新資料庫 tooinitialize hello 記錄鏈結。 如果您不會取得 hello 新資料庫的備份，則它不包含可用性群組中。

1. 在**物件總管] 中**hello 資料庫上按一下滑鼠右鍵，指向太**工作...**，按一下 [ **Back Up**。

1. 按一下**確定**tootake 完整備份 toohello 預設備份位置。

## <a name="create-hello-availability-group"></a>建立 hello 可用性群組
現在您已經準備就緒 tooconfigure 可用性群組使用 hello 下列步驟：

* Hello 上建立資料庫第一次的 SQL Server。
* 完整備份和交易記錄備份的 hello 資料庫
* 完整的還原 hello 和以 hello 的第二個 SQL Server 記錄檔備份 toohello **NORECOVERY**選項
* 建立 hello 可用性群組 (**AG1**) 同步認可、 自動容錯移轉，與可讀取次要複本

### <a name="create-hello-availability-group"></a>建立 hello 可用性群組：

1. 遠端桌面工作階段 toohello 上第一個 SQL Server。 在 SSMS 的 物件總管 中，於 AlwaysOn 高可用性 上按一下滑鼠右鍵，然後按一下新增可用性群組精靈。

    ![啟動新增可用性群組精靈](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. 在 hello**簡介**頁面上，按一下**下一步**。 在 hello**指定可用性群組名稱**頁面上，輸入 hello 可用性群組的名稱，例如**AG1**，請在**可用性群組名稱**。 按一下 [下一步] 。

    ![新增 AG 精靈：指定 AG 名稱](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. 在 hello**選取資料庫**頁面上，選取您的資料庫，然後按一下**下一步**。

   >[!NOTE]
   >由於您已執行至少一個完整備份 hello 預定的主要複本上，hello 資料庫會符合可用性群組的 hello 必要條件。

   ![新增 AG 精靈：選取資料庫](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. 在 hello**指定複本**頁面上，按一下**將複本加入**。

   ![新增 AG 精靈：指定複本](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. hello**連接 tooServer**的對話方塊。 型別中的 hello 第二部伺服器 hello 名稱**伺服器名稱**。 按一下 [ **連接**]。

   在 [hello**指定複本**] 頁面上，您現在應該會看到 hello 中所列的第二部伺服器**可用性複本**。 Hello 複本的設定，如下所示。

   ![新增 AG 精靈：指定複本 (完成)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. 按一下**端點**toosee hello 資料庫鏡像端點，這個可用性群組。 使用 hello 相同連接埠，使用當您設定 hello[資料庫鏡像端點的防火牆規則](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)。

    ![新增 AG 精靈：選取初始資料同步處理](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. 在 hello**選取初始資料同步處理**頁面上，選取**完整**和指定的共用的網路位置。 Hello 位置，請使用 hello[您所建立的備份共用](#backupshare)。 在 hello 範例中，**\\\\\<第一個 SQL Server\>\Backup\**。 按一下 [下一步] 。

   >[!NOTE]
   >完整同步處理會採用 hello hello 第一個執行個體的 SQL Server 資料庫的完整備份，並將它還原 toohello 第二個執行個體。 就大型資料庫而言，不建議進行完整同步處理，因為可能費時很久。 您可以減少這個時間手動建立 hello 資料庫的備份及還原與`NO RECOVERY`。 如果使用已還原 hello 資料庫`NO RECOVERY`hello 上然後再設定 hello 可用性群組的第二個 SQL Server 中，選擇**僅聯結**。 如果您想 tootake hello 備份設定 hello 可用性群組之後，請選擇**略過初始資料同步處理**。

    ![新增 AG 精靈：選取初始資料同步處理](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. 在 hello**驗證**頁面上，按一下**下一步**。 此頁面應看起來類似 toohello 下列映像：

    ![新增 AG 精靈：驗證](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >沒有 hello 接聽程式設定的警告，因為您尚未設定可用性群組接聽程式。 因為您可以在 Azure 虛擬機器上建立 hello 接聽程式來建立 hello Azure 負載平衡器之後，您可以忽略此警告。

10. 在 hello**摘要**頁面上，按一下**完成**，然後稍候 hello 精靈設定 hello 新增可用性群組。 在 [hello**進度**] 頁面上，您可以按一下**更多詳細資料**tooview hello 詳細進度。 Hello 精靈完成時，檢查 hello**結果**hello 可用性群組的頁面 tooverify 已成功建立。

     ![新增 AG 精靈：結果](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. 按一下**關閉**tooexit hello 精靈。

### <a name="check-hello-availability-group"></a>核取 hello 可用性群組

1. 在 [物件總管] 中，展開 [AlwaysOn 高可用性]，然後展開 [可用性群組]。 您現在應該會看到 hello 這個容器中的新可用性群組。 Hello 可用性群組上按一下滑鼠右鍵，然後按一下**顯示儀表板**。

   ![顯示 AG 儀表板](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   您**AlwaysOn 儀表板**看起來應該類似 toothis。

   ![AG 儀表板](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   您可以看到 hello 複本，每個複本和 hello 的同步處理狀態的 hello 容錯移轉模式。

2. 在 [容錯移轉叢集管理員] 中，按一下您的叢集。 選取 [角色]。 您所使用的 hello 可用性群組名稱是 hello 叢集上的角色。 該「可用性群組」並沒有適用於用戶端連線的 IP 位址，因為您並未設定接聽程式。 在您建立 Azure 負載平衡器之後，您將設定 hello 接聽程式。

   ![容錯移轉叢集管理員中的 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > 請勿嘗試 toofail 透過 hello 容錯移轉叢集管理員中的 hello 可用性群組。 所有容錯移轉作業都應在 SSMS 的 **AlwaysOn 儀表板** 中執行。 如需詳細資訊，請參閱[限制使用 hello 與可用性群組容錯移轉叢集管理員](https://msdn.microsoft.com/library/ff929171.aspx)。
    >

此時，您擁有一個在兩個 SQL Server 執行個體上都有複本的「可用性群組」。 您可以在執行個體之間移動 hello 可用性群組。 您無法連線 toohello 可用性群組尚未因為您沒有接聽程式。 在 Azure 虛擬機器，hello 接聽程式都需要負載平衡器。 hello 下一個步驟是在 Azure 中的 toocreate hello 負載平衡器。

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>建立 Azure Load Balancer

在 Azure 虛擬機器上，「SQL Server 可用性群組」需要負載平衡器。 hello 負載平衡器會保存 hello hello 可用性群組接聽程式的 IP 位址。 本節摘要說明如何 toocreate hello 負載平衡器 hello Azure 入口網站中。

1. 在 hello Azure 入口網站，移 toohello 資源群組，其中是您的 SQL 伺服器，而按一下**+ 加**。
2. 搜尋 [負載平衡器]。 選擇 Microsoft 所發行的 hello 負載平衡器。

   ![容錯移轉叢集管理員中的 AG](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  按一下 [建立] 。
3. 設定下列參數 hello 負載平衡器的 hello。

   | 設定 | 欄位 |
   | --- | --- |
   | **名稱** |使用文字名稱 hello 負載平衡器，例如**sqlLB**。 |
   | **類型** |內部 |
   | **虛擬網路** |使用 hello hello Azure 虛擬網路名稱。 |
   | **子網路** |正在使用 hello 名稱 hello hello 虛擬機器的子網路。  |
   | **IP 位址指派** |靜態 |
   | **IP 位址** |使用來自子網路的可用位址。 |
   | **訂用帳戶** |使用 hello 相同訂用帳戶為 hello 虛擬機器。 |
   | **位置** |使用 hello 相同 hello 虛擬機器的位置。 |

   hello Azure 入口網站的刀鋒視窗看起來應該像這樣：

   ![建立負載平衡器](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. 按一下**建立**，toocreate hello 負載平衡器。

tooconfigure hello 負載平衡器，您需要 toocreate 後端集區、 探查，以及設定 hello 負載平衡規則。 執行下列 hello Azure 入口網站中的操作。

### <a name="add-backend-pool"></a>新增後端集區

1. 在 hello Azure 入口網站，移 tooyour 可用性群組。 您可能需要 toorefresh hello 檢視 toosee hello 新建立的負載平衡器。

   ![在資源群組中尋找負載平衡器](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. 按一下 hello 負載平衡器中，按一下**後端集區**，然後按一下**+ 加**。 設定 hello 後端集區，如下所示：

   | 設定 | 說明 | 範例
   | --- | --- |---
   | **名稱** | 輸入文字名稱 | SQLLBBE
   | **與下列產生關聯** | 從清單中挑選 | 可用性集合
   | **可用性設定組** | 使用您的 SQL Server Vm 位於 hello 可用性設定組名稱 | sqlAvailabilitySet |
   | **虛擬機器** |hello 兩個 Azure SQL Server VM 名稱 | sqlserver-0、sqlserver-1

1. 輸入 hello hello 後端集區的名稱。

1. 按一下 [+ 新增虛擬機器]。

1. Hello 可用性集合時，您可以選擇 hello 可用性設定組的 SQL 伺服器位於該 hello。

1. 針對虛擬機器，包括這兩個 SQL 伺服器 hello。 請勿包含 hello 檔案共用見證伺服器。

1. 按一下**確定**toocreate hello 後端集區。

### <a name="set-hello-probe"></a>集 hello 探查

1. 按一下 hello 負載平衡器中，按一下**健全狀況探查**，然後按一下**+ 加**。

1. 設定 hello 健全狀況探查，如下所示：

   | 設定 | 說明 | 範例
   | --- | --- |---
   | **名稱** | 文字 | SQLAlwaysOnEndPointProbe |
   | **通訊協定** | 選擇 [TCP] | TCP |
   | **連接埠** | 任何未使用的連接埠 | 59999 |
   | **間隔**  | hello 一段時間之間探查嘗試以秒為單位 |5 |
   | **狀況不良臨界值** | hello 一定會被視為狀況不良的虛擬機器 toobe 進行連續探查失敗數目  | 2 |

1. 按一下**確定**tooset hello 健全狀況探查。

### <a name="set-hello-load-balancing-rules"></a>設定 hello 負載平衡規則

1. 按一下 hello 負載平衡器中，按一下**負載平衡規則**，然後按一下**+ 加**。

1. 設定 hello 負載平衡規則，如下所示。
   | 設定 | 說明 | 範例
   | --- | --- |---
   | **名稱** | 文字 | SQLAlwaysOnEndPointListener |
   | **前端 IP 位址** | 選擇一個位址 |使用建立 hello 負載平衡器時的 hello 位址。 |
   | **通訊協定** | 選擇 [TCP] |TCP |
   | **連接埠** | Hello SQL Server 執行個體使用 hello 連接埠 | 1433 |
   | **後端連接埠** | 如果已為伺服器直接回傳設定「浮動 IP」，便不會使用此欄位。 | 1433 |
   | **探查** |您指定 hello 探查的 hello 名稱 | SQLAlwaysOnEndPointProbe |
   | **工作階段持續性** | 下拉式清單 | **None** |
   | **閒置逾時** | 開啟 TCP 連線的分鐘 tookeep | 4 |
   | **浮動 IP (伺服器直接回傳)** | |已啟用 |

   > [!WARNING]
   > 伺服器直接回傳是在建立時設定。 無法予以變更。

1. 按一下**確定**tooset hello 負載平衡規則。

## <a name="configure-listener"></a>Hello 接聽程式設定

下一件事 toodo hello 是 tooconfigure hello 容錯移轉叢集上的可用性群組接聽程式。

> [!NOTE]
> 本教學課程會示範如何 toocreate 單一接聽程式-一個 ILB 的 ip 位址。 toocreate 一或多個接聽程式使用一或多個 IP 位址，請參閱[建立可用性群組接聽程式與負載平衡器 |Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>設定接聽程式連接埠

在 SQL Server Management Studio 中，設定 hello 接聽程式通訊埠。

1. 啟動 SQL Server Management Studio 並連接 toohello 主要複本。

1. 瀏覽過**AlwaysOn 高可用性** | **可用性群組** | **可用性群組接聽程式**。

1. 您現在應該會看到您在建立容錯移轉叢集管理員 中的 hello 接聽程式名稱。 以滑鼠右鍵按一下 hello 接聽程式名稱，然後按一下**屬性**。

1. 在 hello**連接埠**方塊中，使用 hello $EndpointPort 您稍早所指定 hello hello 可用性群組接聽程式的通訊埠編號 （1433年是 hello 預設值），然後按一下 **確定**。

現在，您在以 Resource Manager 模式執行的 Azure 虛擬機器中，已有一個「SQL Server 可用性群組」。

## <a name="test-connection-toolistener"></a>測試連接 toolistener

tootest hello 連線：

1. RDP tooa hello 中的 SQL Server 相同虛擬網路，但不會無法自己 hello 複本。 您可以使用 hello hello 叢集中的其他 SQL Server。

1. 使用**sqlcmd**公用程式 tootest hello 連線。 例如，下列指令碼的 hello 建立**sqlcmd**透過 hello 接聽程式使用 Windows 驗證連接 toohello 主要複本：

    ```
    sqlcmd -S <listenerName> -E
    ```

    如果 hello 接聽程式正在使用連接埠以外 hello 預設連接埠 (1433)，hello 連接字串中指定 hello 連接埠。 例如，hello 下列 sqlcmd 命令連接埠 1435 tooa 接聽程式：

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

hello SQLCMD 連線自動連線 toowhichever SQL Server 裝載 hello 主要複本執行個體。

> [!TIP]
> 請確定您指定的 hello 通訊埠的兩個 SQL 伺服器 hello 防火牆上開啟。 這兩部伺服器所需 hello 您使用的 TCP 連接埠的輸入的規則。 如需詳細資訊，請參閱[新增或編輯防火牆規則](http://technet.microsoft.com/library/cc753558.aspx)。
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>後續步驟

- [新增第二個可用性群組使用 IP 位址 tooa 負載平衡器](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP)。
