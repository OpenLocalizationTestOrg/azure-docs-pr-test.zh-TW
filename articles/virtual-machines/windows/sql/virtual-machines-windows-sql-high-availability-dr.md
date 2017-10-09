---
title: "aaaHigh 的可用性和災害復原 SQL Server |Microsoft 文件"
description: "討論 hello 各種類型的 HADR 策略為 Azure 虛擬機器中執行的 SQL Server。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Azure 虛擬機器中的 SQL Server 高可用性和災害復原

與 SQL Server 的 Microsoft Azure 虛擬機器 (Vm) 可協助降低高可用性和災害復原 (HADR) 資料庫方案 hello 成本。 Azure 虛擬機器中支援大部分的 SQL Server HADR 解決方案 (僅限 Azure 以及混合式解決方案兩種)。 僅 Azure 」 的方案，整個 HADR 系統 hello 都會在 Azure 中執行。 在混合式組態中，hello 方案的一部分在 Azure 中執行，並且 hello 其他部分執行內部部署組織中。 hello hello Azure 環境的彈性可讓您 toomove 部分或完全 tooAzure toosatisfy hello 預算與 HADR 需求您的 SQL Server 資料庫系統。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>了解 hello HADR 方案需要
是由 tooyou tooensure 資料庫系統擁有 hello hello 服務等級協定 (SLA) 需要的 HADR 功能。 Azure 提供高可用性機制，例如服務修復後依然存在雲端服務和虛擬機器的失敗復原偵測的 hello 事實不保證能滿足所需的 hello SLA。 這些機制保護 hello 的 hello Vm 的高可用性，但不是 hello 高可用性的 hello Vm 內執行的 SQL Server。 它時，可將 hello SQL Server 執行個體 toofail hello VM 在線上且狀況良好。 此外，即使 hello Azure 所提供的高可用性機制允許停機時間的 hello Vm 的截止 tooevents 例如從軟體或硬體失敗及作業系統升級的復原。

再者，Azure 中的異地備援儲存體 (GRS) (使用名為異地複寫功能進行實作) 對您的資料庫而言，可能不足以當作嚴重損壞修復解決方案使用。 由於地理複寫會以非同步方式傳送資料，因此新的更新可能會遺失的嚴重損壞的 hello 事件中。 Hello 涵蓋更多關於地理複寫限制[地理複寫不支援在不同磁碟上的資料和記錄檔](#geo-replication-support)> 一節。

## <a name="hadr-deployment-architectures"></a>HADR 部署架構
在 Azure 中支援的 SQL Server HADR 技術包括：

* [Always On 可用性群組](https://technet.microsoft.com/library/hh510230.aspx)
* [Always On 容錯移轉叢集執行個體](https://technet.microsoft.com/library/ms189134.aspx)
* [記錄傳送](https://technet.microsoft.com/library/ms187103.aspx)
* [SQL Server 備份及還原與 Azure Blob 儲存體服務](https://msdn.microsoft.com/library/jj919148.aspx)
* [資料庫鏡像](https://technet.microsoft.com/library/ms189852.aspx) - SQL Server 2016 中已被取代

很可能 toocombine hello 技術一起 tooimplement 具有高可用性和災害復原功能的 SQL Server 方案。 根據您所使用的 hello 技術，混合式部署可能需要以 hello Azure 虛擬網路的 VPN 通道。 hello 的以下各節會示範一些 hello 範例部署架構。

## <a name="azure-only-high-availability-solutions"></a>僅限 Azure：高可用性解決方案

您可以在含有 Always On 可用性群組 (稱為可用性群組) 的資料庫層級，具備適用於 SQL Server 的高可用性解決方案。 您也可以在含有 Always On 容錯移轉叢集執行個體 (容錯移轉叢集執行個體) 的執行個體層級，建立高可用性解決方案。 如需額外的備援，您可以藉由在容錯移轉叢集執行個體上建立可用性群組，在這兩個層級上建立備援。 

| Technology | 範例架構 |
| --- | --- |
| **可用性群組** |可用性複本執行於 Azure Vm 中 hello 相同區域提供高可用性。 您需要 tooconfigure 網域控制站 VM，因為 Windows 容錯移轉叢集需要 Active Directory 網域。<br/> ![可用性群組](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>如需詳細資訊，請參閱[在 Azure (GUI) 中設定可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)。 |
| **容錯移轉叢集執行個體** |有 3 種不同的方式可以建立需要使用共用儲存體的「容錯移轉叢集執行個體」(FCI)。<br/><br/>1.使用連接儲存體的 Azure Vm 中執行的雙節點容錯移轉叢集[Windows Server 2016 儲存空間直接存取\(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide 軟體為基礎的虛擬 SAN。<br/><br/>2.在 Azure VM 中執行的雙節點容錯移轉叢集，搭配由協力廠商叢集解決方案支援的儲存體。 如需使用 SIOS DataKeeper 的特定範例，請參閱[使用容錯移轉叢集和協力廠商軟體 SIOS DataKeeper 之檔案共用的高可用性](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/) \(英文\)。<br/><br/>3.在 Azure VM 中執行的雙節點容錯移轉叢集，搭配透過 ExpressRoute 的遠端 iSCSI 目標共用區塊儲存體。 例如，NetApp 私用儲存體 (NPS) 會公開透過 ExpressRoute Equinix tooAzure Vm 使用 iSCSI 目標。<br/><br/>協力廠商共用存放裝置和資料的複寫解決方案，您應該連絡 hello 廠商的任何問題相關的 tooaccessing 資料，在容錯移轉。<br/><br/>請注意，在 [Azure 檔案儲存體](https://azure.microsoft.com/services/storage/files/)最上層使用 FCI 尚未支援，因為這個解決方案不使用進階儲存體。 我們正在 toosupport 這很快。 |

## <a name="azure-only-disaster-recovery-solutions"></a>僅限 Azure：災害復原解決方案
您可以使用可用性群組或資料庫鏡像，為 Azure 中的 SQL Server 資料庫提供災害復原解決方案，或者使用儲存體 Blob 進行備份和還原。

| Technology | 範例架構 |
| --- | --- |
| **可用性群組** |為了進行嚴重損壞修復，可用性複本會在 Azure VM 的多個資料中心執行。 這種跨區域解決方案可防止網站完全中斷。 <br/> ![可用性群組](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>在區域中，所有複本都應位於 hello 相同的雲端服務和 hello 相同的 VNet。 因為每個區域都有個別的 VNet，這些方案需要 VNet tooVNet 連線。 如需詳細資訊，請參閱[設定 VNet 對 VNet 連線使用 hello Azure 入口網站](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)。 如需詳細指示，請參閱[在不同區域中的 Azure 虛擬機器上設定 SQL Server 可用性群組](virtual-machines-windows-portal-sql-availability-group-dr.md)。|
| **資料庫鏡像** |為了進行嚴重損壞修復，主體、鏡像和伺服器會在不同的資料中心內執行。 由於 Active Directory 網域無法跨多個資料中心，因此您必須使用伺服器憑證進行部署。<br/>![資料庫鏡像](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **備份及還原與 Azure Blob 儲存體服務** |生產資料庫直接 tooblob 存放在不同的資料中心針對災害復原備份。<br/>![備份與還原](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的備份與還原](virtual-machines-windows-sql-backup-recovery.md)。 |

## <a name="hybrid-it-disaster-recovery-solutions"></a>混合式 IT：災害復原解決方案
您可以使用可用性群組、資料庫鏡像及記錄傳送，為混合式 IT 環境中的 SQL Server 資料庫提供災害復原解決方案，以及使用 Azure Blob 儲存體進行備份和還原。

| Technology | 範例架構 |
| --- | --- |
| **可用性群組** |為了進行跨網站的嚴重損壞修復，部分可用性複本會在 Azure VM 中執行，而其他複本會在內部部署執行。 hello 生產網站可以在內部或 Azure 資料中心內。<br/>![可用性群組](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>因為所有可用性複本必須都處於 hello 相同容錯移轉叢集，hello 叢集必須跨越兩個網路 （多重子網路容錯移轉叢集）。 此設定需要 Azure 與 hello 在內部部署網路之間的 VPN 連線。<br/><br/>成功的災害復原的資料庫，您也應該安裝在 hello 災害復原站台的複本網域控制站。<br/><br/>很可能 toouse hello SSMS tooadd Azure 複本 tooan，現有的 Alwayson 可用性群組中加入複本精靈。 如需詳細資訊，請參閱教學課程： 將 Alwayson 可用性群組 tooAzure 延伸。 |
| **資料庫鏡像** |一個夥伴執行於 Azure VM，hello 其他執行於內部使用伺服器憑證的跨網站災害復原。 夥伴不需要在 toobe hello 相同的 Active Directory 網域，而且需要 VPN 連線。<br/>![資料庫鏡像](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>另一個資料庫鏡像案例牽涉到一個夥伴執行於 Azure VM 和 hello 其他正在執行的內部部署的 hello 相同 Active Directory 網域，提供跨網站災害復原。 A [hello Azure 虛擬網路和 hello 內部部署網路之間的 VPN 連線](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)需要。<br/><br/>成功的災害復原的資料庫，您也應該安裝在 hello 災害復原站台的複本網域控制站。 |
| **記錄傳送** |一部伺服器執行於 Azure VM，hello 其他內部部署執行上提供跨網站災害復原。 記錄傳送依賴 Windows 檔案共用，因此 hello hello Azure 虛擬網路之間的 VPN 連接內部網路是必要。<br/>![記錄傳送](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>成功的災害復原的資料庫，您也應該安裝在 hello 災害復原站台的複本網域控制站。 |
| **備份及還原與 Azure Blob 儲存體服務** |內部部署生產資料庫直接 tooAzure blob 儲存體進行災害復原備份。<br/>![備份與還原](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>如需詳細資訊，請參閱 [Azure 虛擬機器中 SQL Server 的備份與還原](virtual-machines-windows-sql-backup-recovery.md)。 |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Azure 中 SQL Server HADR 的重要考量
與內部部署、非虛擬化的 IT 基礎結構相較之下，Azure VM、儲存體和網路各有不同的作業特性。 成功實作 HADR SQL Server 方案，在 Azure 中，您必須了解這些差異和設計解決方案 tooaccommodate 它們。

### <a name="high-availability-nodes-in-an-availability-set"></a>可用性設定組中的高可用性節點
在 Azure 中的可用性設定組可讓您 tooplace hello 高可用性節點到不同容錯網域 (Fd) 和升級網域 (Ud)。 針對 Azure Vm toobe 置於 hello 相同可用性設定組中，您必須將其部署在 hello 相同雲端服務。 只有節點中相同的雲端服務可參與的 hello hello 相同可用性設定組。 如需詳細資訊，請參閱[管理 hello 虛擬機器可用性](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

### <a name="failover-cluster-behavior-in-azure-networking"></a>Azure 網路中的容錯移轉叢集行為
hello RFC 相容 DHCP 服務在 Azure 中的可能會導致 hello 建立特定容錯移轉叢集組態 toofail，因為重複的 IP 位址指定給 toohello 叢集網路名稱，例如 hello 相同的 IP 位址做為其中一個 hello 叢集節點。 當您實作取決於 hello Windows 容錯移轉叢集功能的可用性群組時，這會是問題。

雙節點叢集時建立並上線，請考慮 hello 案例：

1. hello 叢集上線，然後 NODE1 要求 hello 叢集網路名稱的動態指派的 IP 位址。
2. NODE1 的 IP 位址以外的任何 IP 位址就會提供 hello DHCP 服務，因為 hello DHCP 服務辨識該 hello 要求來自 NODE1 本身。
3. Windows 會偵測到重複位址指派 tooNODE1 和 toohello 容錯移轉叢集網路名稱，hello 預設叢集群組無法 toocome 線上。
4. hello 預設叢集群組移 tooNODE2 NODE1 的 IP 位址視為 hello 叢集 IP 位址，並讓 hello 預設叢集群組上線。
5. 當 NODE2 嘗試 tooestablish 連線與 node1 的連接時，導向 node1 的封包絕不會離開 NODE2，因為它會解析 NODE1 的 IP 位址 tooitself。 NODE2 無法建立與 node1 的連接，然後失去仲裁並關機 hello 叢集。
6. 在 hello 同時，NODE1 可以傳送封包 tooNODE2，但是 NODE2 無法回覆。 NODE1 失去仲裁並關機 hello 叢集。

可以避免這種情況下，藉由指派未使用靜態 IP 位址，例如像如 169.254.1.1 指派連結-本機 IP 位址、 toohello 叢集網路名稱在順序 toobring hello 叢集網路名稱上線。 toosimplify 此程序，請參閱[設定 Windows 容錯移轉叢集，在 Azure 中的可用性群組](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx)。

如需詳細資訊，請參閱[在 Azure (GUI) 中設定可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)。

### <a name="availability-group-listener-support"></a>可用性群組接聽程式支援
可用性群組接聽程式支援執行 Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 和 Windows Server 2016 的 Azure VM。 這項支援即可進行負載平衡的端點，在屬於可用性群組節點 hello Azure Vm 上啟用 hello 使用。 您必須依照特殊組態步驟進行 hello 接聽程式 toowork Azure 以及在內部部署中執行這兩個用戶端應用程式。

設定接聽程式有主要兩個選項：外部 (公用) 或內部。 hello 外部 （公用） 接聽程式會使用網際網路的負載平衡器，且相關聯的公用虛擬 IP (VIP) 存取透過 hello 網際網路。 內部的接聽程式使用內部負載平衡器，並內只支援用戶端 hello 相同虛擬網路。 對於各個負載平衡器類型，您必須啟用「伺服器直接回傳」。 

如果 hello 可用性群組跨越多個 Azure 的子網路 （如跨越 Azure 區域部署），hello 用戶端連接字串必須包含"**MultisubnetFailover = True**"。 這會導致平行連接嘗試 toohello 複本 hello 不同子網路中。 如需有關設定接聽程式的指示，請參閱

* [設定 Azure 中可用性群組的 ILB 接聽程式](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md)。
* [設定 Azure 中可用性群組的外部接聽程式](../classic/ps-sql-ext-listener.md)。

您仍然可以藉由直接連接 toohello 服務執行個體分別連接 tooeach 可用性複本。 此外，由於可用性群組是與資料庫鏡像用戶端的回溯相容，您可以連接 toohello 可用性複本如資料庫鏡像夥伴，只要 hello 複本設定類似 toodatabase 鏡像：

* 一個主要複本與一個次要複本
* hello 次要複本設定為不可讀取 (**可讀取次要複本**選項設定得**否**)

範例用戶端連接字串對應使用 ADO.NET 或 SQL Server Native Client toothis 資料庫鏡像類似的設定如下：

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

如需用戶端連線的詳細資訊，請參閱：

* [搭配 SQL Server Native Client 使用連接字串關鍵字](https://msdn.microsoft.com/library/ms130822.aspx)
* [連接的用戶端 tooa 資料庫鏡像工作階段 (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [連接 tooAvailability 混合式 IT 中的群組接聽程式](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [可用性群組接聽程式、用戶端連接及應用程式容錯移轉 (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [搭配可用性群組使用資料庫鏡像連接字串](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>混合式 IT 中的網路延遲
您應該部署 HADR 方案，可能會有一段時間，與您在內部部署網路與 Azure 之間的網路延遲的 hello 假設。 在部署複本 tooAzure 時，您應該使用非同步認可而不是同步認可 hello 同步處理模式。 當部署資料庫鏡像伺服器同時在內部部署並在 Azure 中，使用 hello 高效能模式而非 hello 的高安全性模式。

### <a name="geo-replication-support"></a>異地複寫支援
Azure 磁碟中的地理複寫不支援 hello 資料檔和記錄檔儲存在不同磁碟的相同資料庫 toobe hello。 GRS 會在每個磁碟上進行獨立與非同步變更複寫。 這項機制可確保 hello 單一磁碟上 hello 地理複寫副本，但不是會跨多個磁碟進行地理複寫副本的寫入順序。 如果您設定資料庫 toostore，其資料檔案與它在不同磁碟上的記錄檔，hello 復原磁碟損毀可能會包含比 hello 記錄檔，會預先寫入記錄 SQL Server 中的 hello 和 hello ACID hello 資料檔案的最新複本之後交易屬性。 如果您沒有 hello 儲存體帳戶的 hello 選項 toodisable 地理複寫，您應該保留所有的資料與記錄檔 hello 上所指定資料庫的相同磁碟。 如果您必須使用一個以上的磁碟，因為 toohello hello 資料庫大小，您會需要的 toodeploy hello 災害復原解決方案的其中一個上列 tooensure 資料冗餘。

## <a name="next-steps"></a>後續步驟
如果您需要 toocreate Azure 虛擬機器與 SQL Server，請參閱[佈建在 Azure 上的 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

從執行於 Azure VM 中，SQL Server tooget hello 達到最佳效能，請參閱中的 hello 指引[Azure 虛擬機器中 SQL Server 的效能最佳做法](virtual-machines-windows-sql-performance.md)。

如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。

### <a name="other-resources"></a>其他資源
* [在 Azure 中安裝新的 Active Directory 樹系](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [在 Azure VM 中建立可用性群組的容錯移轉叢集](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) \(英文\)

