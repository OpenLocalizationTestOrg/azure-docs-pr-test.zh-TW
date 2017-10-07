---
title: "高可用性的 Azure 資源管理員 Vm aaaSet |Microsoft 文件"
description: "本教學課程會示範如何 toocreate Always On 可用性群組與 Azure Resource Manager 模式中的 Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>在 Azure 虛擬機器中自動設定 Always On 可用性群組：Resource Manager

本教學課程會示範如何 toocreate SQL Server 可用性群組，它使用 Azure 資源管理員虛擬機器。 hello 教學課程使用 Azure 刀鋒 tooconfigure 範本。 您可以檢閱 hello 預設設定、 輸入必要的設定，並更新您逐步進行本教學課程中的 hello 入口網站中的 hello 刀鋒視窗。

hello 完整的教學課程會建立 SQL Server 可用性群組在 Azure 虛擬機器，包括下列項目 hello:

* 包含多個子網路 (前端和後端子網路) 的虛擬網路
* 具有 Active Directory 網域的兩個網域控制站
* 執行 SQL Server，而且已部署的 toohello 後端子網路和聯結的 toohello Active Directory 網域的兩部虛擬機器
* Hello 節點多數 仲裁模型具有三個節點的容錯移轉叢集
* 具有兩份可用性資料庫同步認可複本的可用性群組

下列圖例 hello 代表 hello 完整解決方案。

![Azure 中可用性群組的測試實驗室架構](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

此解決方案中的所有資源都屬於 tooa 單一資源群組。

開始本教學課程之前，請先確認 hello 下列：

* 您已經有 Azure 帳戶。 如果您沒有帳戶，請 [註冊一個試用帳戶](http://azure.microsoft.com/pricing/free-trial/)。
* 您已經知道如何 toouse 會 hello GUI tooprovision hello 虛擬機器映像庫中的 SQL Server 虛擬機器。 如需詳細資訊，請參閱[在 Azure 上佈建 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。
* 您已非常熟悉可用性群組的功能。 如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx)。

> [!NOTE]
> 如果您對搭配 SharePoint 使用可用性群組感興趣，另請參閱 [為 SharePoint 2013 設定 SQL Server 2012 Always On 可用性群組](http://technet.microsoft.com/library/jj715261.aspx)。
>
>

在本教學課程中，使用 hello Azure 入口網站來：

* 從 hello 入口網站選擇 hello Alwayson 範本。
* 檢閱 hello 範本設定，並更新您的環境的一些組態設定。
* 監視 Azure，因為它會建立 hello 整個環境。
* Tooa 網域控制站，然後執行 SQL Server 的 tooa 伺服器連接。

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>從 hello 組件庫佈建 hello 叢集
Azure 提供 hello 整個解決方案資源庫映像。 toolocate hello 範本：

1. Toohello Azure 入口網站使用的登入您的帳戶。
2. 在 hello Azure 入口網站，按一下  **+ 新增**tooopen hello**新增**刀鋒視窗。
3. 在 hello**新增**刀鋒視窗中，搜尋**AlwaysOn**。
   ![尋找 AlwaysOn 範本](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. 在 hello 搜尋結果中，找出**SQL Server AlwaysOn 叢集**。
   ![AlwaysOn 範本](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. 在 [選取部署模型] 中，選擇 [Resource Manager]。

### <a name="basics"></a>基本概念
按一下**基本概念**並設定下列設定的 hello:

* **系統管理員使用者名稱**是具有網域系統管理員權限的使用者帳戶，而且是 hello 這兩個 SQL Server 執行個體上 SQL Server sysadmin 固定的伺服器角色的成員。 本教學課程使用 **DomainAdmin**。
* **密碼**hello hello 網域系統管理員帳戶的密碼。 使用複雜密碼。 確認 hello 的密碼。
* **訂用帳戶**是 hello 訂用帳戶的 Azure 帳單 toorun 所有部署的 hello 可用性群組的資源。 如果您的帳戶有多個訂用帳戶，您可以指定不同的訂用帳戶。
* **資源群組**hello hello 群組 toowhich 隸屬此範本所建立的所有 Azure 資源的名稱。 本教學課程使用 **SQL-HA-RG**。 如需詳細資訊，請參閱 [Azure Resource Manager 概觀](../../../azure-resource-manager/resource-group-overview.md#resource-groups)。
* **位置**是 hello hello 教學課程中會建立 hello 資源的 Azure 區域。 選擇 Azure 區域。

hello 下列螢幕擷取畫面是完成**基本概念**刀鋒視窗中：

![基本概念](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

按一下 [確定] 。

### <a name="domain-and-network-settings"></a>網域和網路設定
此 Azure 資源庫範本會建立網域與網域控制站。 它也會建立一個網路和兩個子網路。 hello 範本無法在現有的網域或虛擬網路中建立伺服器。 hello 下一個步驟設定 hello 網域和網路設定。

在 hello**網域和網路設定**刀鋒視窗中，檢閱 hello 預設 hello 網域和網路設定的值：

* **樹系根網域名稱**該主機 hello 叢集是 hello hello Active Directory 網域的網域名稱。 Hello 教學課程中，使用**contoso.com**。
* **虛擬網路名稱**hello hello Azure 虛擬網路的網路名稱。 Hello 教學課程中，使用**autohaVNET**。
* **網域控制站的子網路名稱**該主機 hello 網域控制站是 hello 名稱 hello 虛擬網路的一部分。 請使用 **subnet-1**。 這個子網路會使用位址首碼 **10.0.0.0/24**。
* **SQL Server 的子網路名稱**hello hello 主機 hello 伺服器執行 SQL Server 和 hello 檔案共用見證的虛擬網路的部分的名稱。 請使用 **subnet-2**。 這個子網路會使用位址首碼 **10.0.1.0/26**。

toolearn 進一步了解虛擬網路在 Azure 中，請參閱[虛擬網路概觀](../../../virtual-network/virtual-networks-overview.md)。  

hello**網域和網路設定**應該看起來像 hello 下列螢幕擷取畫面：

![網域和網路設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

如有必要，您可以變更這些值。 本教學課程中，使用 hello 預先設定的值。

檢閱 hello 設定，然後按一下**確定**。

### <a name="availability-group-settings"></a>可用性群組設定
在**可用性群組設定**，檢閱 hello 預設值為 hello 可用性群組和 hello 接聽程式。

* **可用性群組名稱**hello hello 可用性群組的叢集的資源名稱。 本教學課程使用 **Contoso-ag**。
* **可用性群組接聽程式名稱**hello 叢集和 hello 內部負載平衡器使用。 連接 tooSQL 伺服器的用戶端可以使用此名稱 tooconnect toohello 適當 hello 之資料庫的複本。 本教學課程使用 **Contoso-listener**。
* **可用性群組接聽程式連接埠**指定 hello hello SQL Server 接聽程式的 TCP 通訊埠。 本教學課程中，使用 hello 預設連接埠， **1433年**。

如有必要，您可以變更這些值。 本教學課程中，使用 hello 預先設定的值。  

![可用性群組設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

按一下 [確定] 。

### <a name="virtual-machine-size-storage-settings"></a>虛擬機器大小，儲存體設定
在**VM 大小，存放裝置設定**，選擇 SQL Server 虛擬機器大小，並檢閱 hello 其他設定。

* **SQL Server 虛擬機器大小**是 hello 兩部執行 SQL Server 的虛擬機器的大小。 選擇適合工作負載的虛擬機器大小。 如果您要建置此環境 hello 教學課程中，使用**DS2**。 對於生產工作負載中，選擇可支援 hello 工作負載的虛擬機器大小。 許多生產環境工作負載需要 **DS4** 或更大。 hello 範本建置此大小的兩部虛擬機器，並在每個安裝 SQL Server。 如需相關資訊，請參閱[虛擬機器的大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

> [!NOTE]
> 安裝 azure hello 的 SQL Server Enterprise Edition。 hello 成本取決於 hello 版本和 hello 虛擬機器大小。 如需目前成本的詳細資訊，請參閱[虛擬機器定價](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql)。
>
>

* **網域控制站虛擬機器大小**網域控制站是 hello 的 hello 虛擬機器大小。 本教學課程使用 **D2**。
* **檔案共用見證的虛擬機器大小**hello 檔案共用見證的 hello 虛擬機器大小。 本教學課程使用 **A1**。
* **SQL 儲存體帳戶**hello hello 保存 hello SQL Server 資料與作業系統磁碟的儲存體帳戶名稱。 本教學課程使用 **alwaysonsql01**。
* **DC 儲存體帳戶**是 hello 名稱 hello hello 儲存體帳戶的網域控制站。 本教學課程使用 **alwaysondc01**。
* **SQL Server 資料磁碟大小**TB 是 hello TB 中的 hello SQL Server 資料磁碟大小。 指定從 1 到 4 的數字。 本教學課程使用 **1**。
* **儲存體最佳化**設定 hello hello 工作負載類型為基礎的 SQL Server 虛擬機器的特定存放裝置組態設定。 在此案例中的所有 SQL Server 虛擬機器會都使用進階儲存體與 Azure 磁碟設定 tooread 專用的主機快取。 此外，您可以選擇其中一個三個設定最佳化 hello 工作負載的 SQL Server 設定：

  * **一般工作負載**不會設定任何特定的組態設定。
  * **交易式處理**會設定追蹤旗標 1117 和 1118。
  * **資料倉儲**會設定追蹤旗標 1117 和 610。

本教學課程使用 [一般工作負載]。

![VM 大小儲存體設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

檢閱 hello 設定，然後按一下**確定**。

#### <a name="a-note-about-storage"></a>儲存體注意事項
其他最佳化 hello hello SQL Server 資料磁碟大小而定。 Azure 會針對資料磁碟的每一 TB，額外新增 1 TB 進階儲存體。 當伺服器需要 2 TB 以上時，請 hello 範本會在每個 SQL Server 虛擬機器上建立存放集區。 存放集區是一種儲存體虛擬化設定的 tooprovide 更高的容量、 備援及效能，多張光碟的所在。  hello 範本然後 hello 存放集區上建立儲存空間，並呈現單一資料磁碟 toohello 作業系統。 hello 範本會為 SQL Server，將此磁碟指定為 hello 資料磁碟。 hello 範本適用於 SQL Server 微調 hello 存放集區，使用下列設定的 hello:

* 等量磁碟區大小為 hello 交錯 hello 虛擬磁碟設定。 交易式工作負載使用 64 KB。 資料倉儲工作負載使用 256 KB。
* 備援為簡單 (無備援)。

> [!NOTE]
> Azure 高階儲存體為本地備援，並在單一區域中，會保留三份 hello 資料，因此不需要在 hello 存放集區的其他恢復功能。
>
>

* 資料行計數等於 hello hello 存放集區中的磁碟數目。

如需儲存空間和儲存體集區的詳細資訊，請參閱：

* [儲存空間概觀](http://technet.microsoft.com/library/hh831739.aspx)
* [Windows Server 備份和存放集區](http://technet.microsoft.com/library/dn390929.aspx)

如需有關 SQL Server 組態最佳做法的詳細資訊，請參閱 [Azure 虛擬機器中的 SQL Server 效能最佳做法](virtual-machines-windows-sql-performance.md)。

### <a name="sql-server-settings"></a>SQL Server 設定
在**SQL Server 設定**、 檢閱並修改 hello SQL Server 虛擬機器名稱前置詞、 SQL Server 版本、 SQL Server 服務帳戶和密碼，hello SQL 自動修補功能維護排程。

* **SQL Server 名稱前置詞**是使用的 toocreate 每個 SQL Server 虛擬機器的名稱。 本教學課程使用 **sqlserver**。 hello 範本名稱 hello SQL Server 虛擬機器*sqlserver 0*和*sqlserver 1*。
* **SQL Server 版本**hello 版本的 SQL Server。 本教學課程使用 **SQL Server 2014**。 您也可以選擇 **SQL Server 2012** 或 **SQL Server 2016**。
* **SQL Server 服務帳戶使用者名稱**hello hello SQL Server 服務的網域帳戶名稱。 本教學課程使用 **sqlservice**。
* **密碼**hello hello SQL Server 服務帳戶的密碼。  使用複雜密碼。 確認 hello 的密碼。
* **SQL 自動修補功能維護排程**識別 hello 星期幾 hello Azure 自動修補 hello SQL 伺服器。 在本教學課程中，請輸入**星期日**。
* **SQL 自動修補功能維護開始小時**時自動修補開始，hello hello Azure 區域的一天的時間。

> [!NOTE]
> hello 修補程式的每個虛擬機器視窗被階段性的一個小時。 只有一部虛擬機器已在服務中斷時間 tooprevent 修補。
>
>

![SQL Server 設定](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

檢閱 hello 設定，然後按一下**確定**。

### <a name="summary"></a>摘要
在 [hello 摘要] 頁面上，Azure 會驗證 hello 設定。 您也可以下載 hello 範本。 檢閱 hello 摘要。 按一下 [確定] 。

### <a name="buy"></a>購買
這個最終的刀鋒視窗包含 [使用條款] 和 [隱私權原則]。 檢閱此資訊。 當您準備好進行 Azure toostart toocreate hello 虛擬機器，且所有 hello hello 可用性群組所需的其他資源時，按一下**建立**。

hello Azure 入口網站建立 hello 資源群組和 hello 的所有資源。

## <a name="monitor-deployment"></a>監視部署
監視從 hello Azure 入口網站的 hello 部署進度。 代表 hello 部署的圖示會自動釘選的 toohello Azure 入口網站的儀表板。

![Azure 儀表板](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>連接 tooSQL 伺服器
在有網際網路連線的 IP 位址的虛擬機器上執行 hello 的 SQL Server 的新執行個體。 您可以遠端桌面 (RDP) 直接 tooeach SQL Server 虛擬機器。

tooRDP tooa SQL Server，請遵循下列步驟：

1. 從 hello Azure 入口網站的儀表板，確認已成功 hello 部署。
2. 按一下 [資源] 。
3. 在 hello**資源**刀鋒視窗中，按一下**sqlserver-0**，這是 hello 的其中一部執行 SQL Server 的 hello 虛擬機器的電腦名稱。
4. Hello] 刀鋒視窗的**sqlserver 0**，按一下 [**連接**。 如果您想 tooopen 或儲存 hello 遠端連線物件，則會要求您的瀏覽器。 按一下 [開啟] 。
5. **遠端桌面連線**可能會警告您該 hello 無法識別此遠端連線的發行者。 按一下 [ **連接**]。
6. Windows 安全性會提示您 tooenter hello 主要網域控制站的認證 tooconnect toohello IP 位址。 按一下 [使用其他帳戶]。 在 [使用者名稱] 中，輸入 **contoso\DomainAdmin**。 當您設定 hello 範本中的 hello 系統管理員使用者名稱時，您可以設定此帳戶。 使用您選擇設定 hello 範本時的 hello 複雜密碼。
7. **遠端桌面**可能會警告您該 hello 遠端電腦無法驗證到期 tooproblems 其安全性憑證。 它會顯示您 hello 安全性憑證名稱。 如果您遵循 hello 教學課程，hello 名稱是**sqlserver 0.contoso.com**。按一下 [是] 。

您現在已經與 RDP toohello SQL Server 虛擬機器連線。 您可以開啟 SQL Server Management Studio、 連線 toohello 預設 SQL Server 執行個體，並確認該 hello 可用性群組的設定。
