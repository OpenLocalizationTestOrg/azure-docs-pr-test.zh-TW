---
title: "aaaReplicate 多層式 SharePoint 應用程式使用 Azure Site Recovery |Microsoft 文件"
description: "本文說明如何 tooreplicate 多層式 SharePoint 應用程式使用 Azure Site Recovery 功能。"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>使用 Azure Site Recovery 複寫多層式 SharePoint 應用程式以便進行災害復原

本文詳細說明如何使用 SharePoint 應用程式的 tooprotect [Azure Site Recovery](site-recovery-overview.md)。


## <a name="overview"></a>概觀

Microsoft SharePoint 是功能強大的應用程式，可協助群組或部門組織、共同作業及共用資訊。 SharePoint 可提供內部網路入口網站、文件和檔案管理、共同作業、社交網路、外部網路、網站、企業搜尋與商業智慧。 它也具有系統整合、程序整合和工作流程自動化功能。 通常，組織將其視為第 1 層應用程式機密 toodowntime 和資料遺失。

現今，Microsoft SharePoint 並未提供任何現成的災害復原功能。 不論 hello 型別和小數位數的災害，復原會涉及 hello 的待命資料庫的資料中心，您可以 hello 伺服器陣列復原到使用。 待命資料庫的資料中心案例所需的位置本機備援系統和備份無法從復原在 hello 主要資料中心的 hello 中斷。

理想的災害復原解決方案應該 hello 複雜的應用程式架構，例如 SharePoint 周圍允許復原方案的模型。 它也應該擁有 hello 能力 tooadd 自訂步驟 toohandle 應用程式之間的對應各層，因此具有較低 RTO hello 災害事件中提供單鍵容錯移轉。

本文詳細說明如何使用 SharePoint 應用程式的 tooprotect [Azure Site Recovery](site-recovery-overview.md)。 本文將討論複寫三層 SharePoint 應用程式 tooAzure、 告訴您如何進行災害復原訓練，及如何容錯移轉 hello 應用程式 tooAzure 最佳的作法。

您可以觀賞復原多層應用程式 tooAzure 相關的影片下方的 hello。

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>必要條件

開始之前，請確定您了解 hello 下列：

1. [複寫虛擬機器 tooAzure](site-recovery-vmware-to-azure.md)
2. 如何太[設計與復原網路](site-recovery-network-design.md)
3. [執行測試容錯移轉 tooAzure](site-recovery-test-failover-to-azure.md)
4. [執行容錯移轉 tooAzure](site-recovery-failover.md)
5. 如何太[複寫的網域控制站](site-recovery-active-directory.md)
6. 如何太[複寫 SQL Server](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>SharePoint 架構

可以使用階層的拓撲和伺服器角色 tooimplement 符合特定目標的伺服器陣列設計的一或多個伺服器上部署 SharePoint。 支援大量並行使用者和大量內容項目的典型大型、高需求 SharePoint 伺服器陣列，會使用服務群組作為其延展性策略的一部分。 這種方法牽涉到將這些服務群組在一起，且再向外擴充 hello 伺服器做為群組的專用伺服器上執行服務。 hello 下列拓撲描述在 hello 服務和伺服器群組的三層 SharePoint 伺服器陣列。 請參閱 tooSharePoint 文件和產品線架構的不同 SharePoint 拓撲的詳細指引。 您可以在[這份文件](https://technet.microsoft.com/en-us/library/cc303422.aspx)中找到有關 SharePoint 2013 部署的詳細資訊。



![部署模式 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Site Recovery 支援

為了建立這篇文章，使用了 VMware 虛擬機器搭配 Windows Server 2012 R2 Enterprise。 還使用 SharePoint 2013 Enterprise 版本和 SQL Server 2014 Enterprise 版本。 站台復原複寫與應用程式無關，因為 hello 建議這裡提供預期的 toohold 上也有下列情況。

### <a name="source-and-target"></a>來源與目標

**案例** | **tooa 次要站台** | **tooAzure**
--- | --- | ---
**Hyper-V** | 是 | 是
**VMware** | 是 | 是
**實體伺服器** | 是 | 是

### <a name="sharepoint-versions"></a>SharePoint 版本
支援下列 SharePoint server 版本的 hello。

* SharePoint Server 2013 Standard
* SharePoint Server 2013 Enterprise
* SharePoint Server 2016 Standard
* SharePoint Server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>請注意的事項 tookeep

如果您使用的共用磁碟叢集做為任何層應用程式中，則您不會是能 toouse 站台復原複寫 tooreplicate 這些虛擬機器。 您可以使用原生 hello 應用程式所提供的複寫，然後使用[復原計劃](site-recovery-create-recovery-plans.md)toofailover 所有層。

## <a name="replicating-virtual-machines"></a>複寫虛擬機器

請遵循[本指南](site-recovery-vmware-to-azure.md)toostart 複寫 hello 虛擬機器 tooAzure。

* Hello 複寫完成之後，請確定您移 tooeach 每一層的虛擬機器，然後選取相同的可用性設定組 ' 複寫項目 > 設定 > 內容 > 計算與網路 '。 例如，如果您的 web 層有 3 個 Vm，確定所有 hello 3 的 vm 都設定 toobe 一部分在 Azure 中設定的同一個可用性。

    ![Set-Availability-Set](./media/site-recovery-sharepoint/select-av-set.png)

* 如需保護 Active Directory 和 DNS 的指引，請參閱太[保護 Active Directory 和 DNS](site-recovery-active-directory.md)文件。

* 如需保護 SQL server 上執行的資料庫層的指引，請參閱太[保護 SQL Server](site-recovery-active-directory.md)文件。

## <a name="networking-configuration"></a>網路設定

### <a name="network-properties"></a>網路屬性

* Hello 應用程式與 Web 層的 Vm，以便讓 hello Vm 取得附加的 toohello 正確 DR 網路容錯移轉之後，Azure 入口網站中設定網路設定。

    ![選取網路](./media/site-recovery-sharepoint/select-network.png)


* 如果您使用靜態 ip 位址，然後指定您想 hello hello 中的虛擬機器 tootake hello IP**目標 IP**欄位

    ![設定靜態 IP](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>DNS 和流量路由

為網際網路對向站台，[建立 Traffic Manager 設定檔 'Priority' 型別的](../traffic-manager/traffic-manager-create-profile.md)hello Azure 訂用帳戶中。 然後在 hello 下列方式設定您的 DNS 和 Traffic Manager 設定檔。


| **其中** | **來源** | **目標**|
| --- | --- | --- |
| 公用 DNS | SharePoint 網站的 公用 DNS <br/><br/> 例如︰sharepoint.contoso.com | 流量管理員 <br/><br/> contososharepoint.trafficmanager.net |
| 內部部署 DNS | sharepointonprem.contoso.com | Hello 在內部部署伺服器陣列上的公用 IP |


在 hello Traffic Manager 設定檔，[主要和復原的端點建立 hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md)。 使用 hello 外部端點的內部端點與 Azure 端點的公用 IP。 請確定 hello 優先權會設定較高的 tooon 內部端點。

主機測試頁上為了讓 Traffic Manager tooautomatically hello SharePoint web 層中的特定連接埠 (例如 800) 會偵測容錯移轉後的可用性。 如果您無法在任何 SharePoint 網站上啟用匿名驗證，這是個解決辦法。

[設定 hello Traffic Manager 設定檔](../traffic-manager/traffic-manager-configure-priority-routing-method.md)以 hello 以下設定。

* 路由方法 -「優先順序」
* DNS 時間 toolive (TTL)-' 30 秒'
* 端點監視器設定 - 如果您可以啟用匿名驗證，即可提供特定的網站端點。 或者，您可以在特定連接埠 (例如 800) 上使用測試頁。

## <a name="creating-a-recovery-plan"></a>建立復原計劃

復原計劃可讓您排序 hello 容錯移轉維護應用程式一致性是多層式應用程式，因此，在各層。 建立多層式 web 應用程式的復原計劃時，請遵循下面的步驟 hello。 [深入了解如何建立復原計劃](site-recovery-runbook-automation.md#customize-the-recovery-plan)。

### <a name="adding-virtual-machines-toofailover-groups"></a>新增虛擬機器 toofailover 群組

1. 建立復原方案所加入的 hello 應用程式和 Web 層 Vm。
2. 按一下 自訂' toogroup hello Vm。 根據預設，所有 VM 都是「群組 1」的一部分。

    ![自訂 RP](./media/site-recovery-sharepoint/rp-groups.png)

3. 建立另一個群組 (群組 2)，並將 hello Web 層 Vm 移到 hello 新群組。 您的應用程式層 VM 應該是「群組 1」的一部分，而 Web 層 VM 應該是「群組 2」的一部分。 這是 hello 應用程式層 Vm 開機第一次後面接著 Web 層 Vm 的 tooensure。


### <a name="adding-scripts-toohello-recovery-plan"></a>加入指令碼 toohello 復原計劃

您可以將最常用的 hello Azure 站台復原指令碼部署到您的自動化帳戶按一下下面的 hello '部署 tooAzure' 按鈕。 當您使用任何已發行的指令碼時，請確定您遵循 hello 指令碼中的 hello 指導方針。

[![部署 tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. 新增動作前指令碼 too'Group 1' toofailover SQL 可用性群組。 使用發行 hello 範例指令碼中的 hello ' ASR-SQL-FailoverAG' 指令碼。 請確定您遵循 hello 指令碼中的 hello 指導方針，變更所需的 hello hello 指令碼中適當地。

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. 新增網頁階層 (群組 2) 的虛擬機器容錯移轉負載平衡器上 hello 後動作指令碼 tooattach。 使用發行 hello 範例指令碼中的 hello ' ASR AddSingleLoadBalancer' 指令碼。 請確定您遵循 hello 指令碼中的 hello 指導方針，變更所需的 hello hello 指令碼中適當地。

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. 在 Azure 中新增的手動步驟 tooupdate hello DNS 記錄 toopoint toohello 新伺服器陣列。

    * 若為網際網路面向網站，容錯移轉後不需要更新 DNS。 請遵循 hello hello '網路指引' 區段 tooconfigure Traffic Manager 中所述的步驟。 如果 hello Traffic Manager 設定檔已設定 hello 上一節中所述，，新增指令碼 tooopen 虛擬連接埠 (在 hello 範例 800) hello Azure VM 上。

    * 內部對向的網站，加入手動步驟 tooupdate hello DNS 記錄 toopoint toohello 新 Web 層的 VM 的負載平衡器 IP。

4. 從備份中新增的手動步驟 toorestore 搜尋應用程式或啟動新的搜尋服務。

5. 如需從備份還原搜尋服務應用程式，請遵循下列步驟。

    * 這個方法會假設 hello 搜尋服務應用程式的備份執行之前 hello 重大事件，而且該 hello 備份可以使用在 hello DR 網站。
    * 這可以輕易地達成排程 hello 備份 （例如每天一次），並在 hello DR 網站使用複製程序 tooplace hello 備份。 複製程序可能包含指令碼程式，例如 AzCopy (Azure 複製) 或設定 DFSR (分散式檔案服務複寫)。
    * 現在該 hello SharePoint 伺服器陣列執行時，瀏覽 hello 管理中心] 中，[備份及還原]，然後選取 [還原。 hello 還原質詢 hello 所指定的備份位置 （您可能需要 tooupdate hello 值）。 選取您想要 toorestore hello 搜尋服務應用程式備份。
    * 已還原搜尋。 請記住，hello 還原預期 toofind hello 相同拓撲 （相同的伺服器數目），和相同硬碟磁碟機代號指派 toothose 伺服器。 如需詳細資訊，請參閱[在 SharePoint 2013 中還原搜尋服務應用程式](https://technet.microsoft.com/library/ee748654.aspx)文件。


6. 如需從新的搜尋服務應用程式著手，請遵循下列步驟。

    * 這個方法會假設 hello 「 搜尋系統管理 」 資料庫的備份可以使用在 hello DR 網站。
    * Hello 其他搜尋服務應用程式資料庫不會複寫，因為它們會需要 toobe 重新建立。 toodo，瀏覽 tooCentral 管理，然後刪除 hello 搜尋服務應用程式。 在任何伺服器上的主機 hello 搜尋索引會刪除 hello 索引檔案。
    * 重新建立 hello 搜尋服務應用程式與這個重新建立 hello 資料庫。 建議 toohave 備妥的指令碼重新建立此服務應用程式因為它不可能 tooperform 透過 hello GUI 的所有動作。 例如，設定 hello 索引的磁碟機位置和設定 hello 搜尋拓樸都僅能使用 SharePoint PowerShell 指令程式。 使用 hello 還原 SPEnterpriseSearchServiceApplication 的 Windows PowerShell cmdlet 並指定 hello 記錄傳送和複寫 Search_Service__DB 搜尋管理資料庫。 此 cmdlet 提供 hello 搜尋設定、 結構描述、 managed 的屬性、 規則和來源並建立一組預設的 hello 其他元件。
    * 一旦搜尋服務應用程式的 hello 加以重新建立，您必須啟動完整搜耙的每個內容來源 toorestore hello 搜尋服務。 您會遺失一些從 hello 在內部部署伺服器陣列，例如搜尋建議的分析資訊。

7. 一旦 hello 的所有步驟都完成都之後，儲存 hello 復原計劃並 hello 最終的復原計劃看起來像下列。

    ![已儲存的 RP](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>執行測試容錯移轉
請遵循[本指南](site-recovery-test-failover-to-azure.md)toodo 測試容錯移轉。

1.  移 tooAzure 入口網站，然後選取您的復原服務保存庫。
2.  按一下 hello 復原計劃建立 SharePoint 應用程式。
3.  按一下 [測試容錯移轉]。
4.  選取的復原點和 Azure 虛擬網路 toostart hello 測試容錯移轉程序。
5.  一旦 hello 次要環境已啟動，您可以執行您的驗證。
6.  Hello 驗證完成後，您可以按一下 清除測試容錯移轉' hello 復原計劃，並會清除 hello 測試容錯移轉環境。

如需 ad 執行測試容錯移轉的指引和 DNS，請參閱太[測試容錯移轉考量 AD 和 DNS](site-recovery-active-directory.md#test-failover-considerations)文件。

如需執行測試容錯移轉的 SQL Alwayson 可用性群組的指引，請參閱太[執行測試容錯移轉 SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover)文件。

## <a name="doing-a-failover"></a>執行容錯移轉
請依照[本指引](site-recovery-failover.md)來進行容錯移轉。

1.  移 tooAzure 入口網站，然後選取您的復原服務保存庫。
2.  按一下 hello 復原計劃建立 SharePoint 應用程式。
3.  按一下 [容錯移轉]。
4.  選取的復原點 toostart hello 容錯移轉程序。

## <a name="next-steps"></a>後續步驟
您可以深入了解如何使用 Site Recovery [複寫其他應用程式](site-recovery-workload.md)。
