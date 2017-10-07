---
title: "aaaSQL Server 可用性群組-Azure 虛擬機器-嚴重損壞修復 |Microsoft 文件"
description: "本文說明如何 tooconfigure SQL Server 可用性群組中的不同區域的複本與 Azure 虛擬機器上。"
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>在不同區域的 Azure 虛擬機器上設定 Always On 可用性群組

本文說明如何 tooconfigure SQL Server Always On 可用性群組在遠端的 Azure 位置的 Azure 虛擬機器上的複本。 使用此組態 toosupport 災害復原。

本文適用於在 Resource Manager 模式 tooAzure 虛擬機器。

hello 下列影像顯示常見的部署可用性群組的 Azure 虛擬機器上：

   ![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

在此部署中，所有虛擬機器都位於一個 Azure 區域中。 hello 可用性群組複本可能會包含在 SQL 1 和 SQL 2 上的自動容錯移轉的同步認可。 toobuild 這種架構，請參閱[可用性群組的範本或教學課程](virtual-machines-windows-portal-sql-availability-group-overview.md)。

此架構是很容易遭受 toodowntime 如果 hello Azure 地區變成無法存取。 tooovercome 這項弱點，將複本加入不同的 Azure 區域。 hello 下圖顯示 hello 新架構的外觀：

   ![可用性群組 DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

hello 上圖顯示名 SQL 3 的新虛擬機器。 SQL-3 位於不同的 Azure 區域中。 SQL 3 就會加入 toohello Windows Server 容錯移轉叢集。 SQL-3 可以裝載可用性群組複本。 最後，請注意該 hello Azure 地區 SQL 3 有新的 Azure 負載平衡器。

>[!NOTE]
> 多個虛擬機器處於 hello 相同區域時，需要 Azure 可用性設定組。 如果只有一部虛擬機器是在 hello 區域中，則不需要 hello 可用性設定組。 您只能在建立虛擬機器時將其置於可用性設定組中。 如果 hello 虛擬機器已在可用性設定組中，您可以加入稍後新增額外的複本虛擬機器。

在這種架構，通常會設定 hello 遠端區域中的 hello 複本使用非同步認可可用性模式和手動容錯移轉模式。

當可用性群組複本位於不同 Azure 區域中的 Azure 虛擬機器上時，每個區域需要：

* 虛擬網路閘道
* 虛擬網路閘道連線

hello 下列圖表顯示 hello 網路資料中心之間的通訊方式。

   ![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>此架構會針對 Azure 區域之間複寫的資料產生輸出資料費用。 請參閱[頻寬定價](http://azure.microsoft.com/pricing/details/bandwidth/)。  

## <a name="create-remote-replica"></a>建立遠端複本

toocreate 複本，以在遠端資料中心內，下列步驟 hello:

1. [在 hello 新區域中建立虛擬網路](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。

1. [設定 VNet 對 VNet 連線使用 hello Azure 入口網站](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)。

   >[!NOTE]
   >在某些情況下，您可能需要 toouse PowerShell toocreate hello VNet 對 VNet 連線。 例如，如果您使用不同的 Azure 帳戶，您無法設定 hello 連接 hello 入口網站中。 在此情況下查看，[設定 VNet 對 VNet 連線使用 hello Azure 入口網站](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)。

1. [在 hello 新區域中建立的網域控制站](../../../active-directory/active-directory-new-forest-virtual-machine.md)。

   如果 hello hello 主要站台中的網域控制站無法使用此網域控制站會提供驗證。

1. [在 hello 新的區域中建立 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。

1. [在 hello hello 新區域上的網路中建立 Azure 負載平衡器](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)。

   此負載平衡器必須：

   - 在 hello 相同網路和子網路，如 hello 新的虛擬機器。
   - 擁有 hello 可用性群組接聽程式的靜態 IP 位址。
   - 包含組成僅 hello 中的虛擬機器 hello 相同的區域，因為 hello 負載平衡器後端集區。
   - 使用 TCP 連接埠探查 toohello 特定 IP 位址。
   - 負載平衡規則特定 toohello SQL Server，hello 中的相同的區域。  

1. [新增容錯移轉叢集功能 toohello 新的 SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)。

1. [加入新 SQL Server toohello 網域 hello](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)。

1. [網域帳戶設定 hello 新 SQL Server 服務帳戶 toouse](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount)。

1. [加入新 SQL Server toohello hello Windows Server 容錯移轉叢集](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode)。

1. Hello 叢集上建立 IP 位址資源。

   您可以在 [容錯移轉叢集管理員] 中建立 hello IP 位址資源。 以滑鼠右鍵按一下 hello 可用性群組角色中，按一下**加入資源**，**更資源**，按一下**IP 位址**。

   ![建立 IP 位址](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   請依照下列方式設定此 IP 位址：

   - 使用 hello 網路 hello 遠端資料中心。
   - 從 hello 新 Azure 負載平衡器的 hello IP 位址指派。 

1. 在 hello 新的 SQL Server 在 SQL Server 組態管理員[啟用 Alwayson 可用性群組](http://msdn.microsoft.com/library/ff878259.aspx)。

1. [開啟防火牆連接埠上的 hello 新的 SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)。

   hello 連接埠號碼需要 tooopen 取決於您的環境。 開啟的連接埠鏡像端點與 Azure 的 hello 負載平衡器健全狀況探查。

1. [加入複本 toohello 可用性群組上 hello 新的 SQL Server](http://msdn.microsoft.com/library/hh213239.aspx)。

   針對遠端 Azure 區域中的複本，請設定它來進行非同步複寫搭配手動容錯移轉。  

1. 為 hello 接聽程式的用戶端存取點 （網路名稱） 叢集的相依性加入 hello IP 位址資源。

   hello 下列螢幕擷取畫面顯示已正確設定的 IP 位址叢集資源：

   ![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >hello 叢集資源群組包含兩個 IP 位址。 兩個 IP 位址是 hello 接聽程式用戶端存取點的相依性。 使用 hello**或**hello 叢集相依性設定中的運算子。

1. [在 PowerShell 中設定 hello 叢集參數](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam)。

Hello 叢集網路名稱、 IP 位址與 hello hello 新區域中的負載平衡器所設定的探查連接埠執行 hello PowerShell 指令碼。

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>設定多個子網路的連線

hello 遠端資料中心中的 hello 複本 hello 可用性群組的一部分，但是它為不同的子網路。 如果此複本會變成 hello 主要複本，可能會發生應用程式連接逾時。 此行為是 hello 與內部部署可用性群組多重子網路部署在相同的。 tooallow 連接從用戶端應用程式，請更新 hello 用戶端連線，或是設定 hello 叢集網路名稱資源的快取的名稱解析。

最好是更新 hello 用戶端連接字串 tooset `MultiSubnetFailover=Yes`。 請參閱[使用 MultiSubnetFailover 進行連接](http://msdn.microsoft.com/library/gg471494#Anchor_0)。

如果您無法修改 hello 連接字串，您可以設定快取的名稱解析。 請參閱[多子網路可用性群組中的連線逾時 (英文)](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/)。

## <a name="fail-over-tooremote-region"></a>容錯移轉 tooremote 區域

tootest 接聽程式連線能力 toohello 遠端區域中，您可以容錯移轉 hello 複本 toohello 遠端區域。 非同步 hello 複本時，容錯移轉不會受到 toopotential 資料遺失。 不會遺失資料，透過 toofail 變更 hello 可用性模式 toosynchronous，以及設定 hello 容錯移轉模式 tooautomatic。 使用下列步驟的 hello:

1. 在**物件總管 中**，連線 toohello 裝載 hello 主要複本的 SQL Server 執行個體。
1. 在 [AlwaysOn 可用性群組]、[可用性群組] 底下，於您的可用性群組上按一下滑鼠右鍵，然後按一下 [屬性]。
1. 在 hello**一般**頁面的 **可用性複本**，組 hello 中的次要複本 hello DR 網站 toouse**同步認可**可用性模式與**自動**容錯移轉模式。
1. 如果您在相同的主要複本的高可用性站台的次要複本，將此複本太**非同步認可**和**手動**。
1. 按一下 [確定]。
1. 在**物件總管 中**，以滑鼠右鍵按一下 hello 可用性群組，然後按一下**顯示儀表板**。
1. 在 hello 儀表板中，確認該 hello hello DR 網站上的複本同步處理。
1. 在**物件總管 中**，以滑鼠右鍵按一下 hello 可用性群組，然後按一下**容錯移轉...**.SQL Server Management Studio 開啟精靈 toofail 透過 SQL Server。  
1. 按一下**下一步**，並選取 hello hello DR 網站中的 SQL Server 執行個體。 再按一下 [下一步]  。
1. 連接 toohello hello DR 網站中的 SQL Server 執行個體，並按一下**下一步**。
1. 在 hello**摘要**頁面上，確認 hello 設定，然後按一下 **完成**。

測試連線之後, 移動 hello 主要複本後 tooyour 主要資料中心，且設定 hello 可用性模式後 tootheir 一般作業系統設定。 hello 下表顯示 hello 正常操作設定這份文件中所描述的 hello 架構：

| 位置 | 伺服器執行個體 | 角色 | 可用性模式 | 容錯移轉模式
| ----- | ----- | ----- | ----- | -----
| 主要資料中心 | SQL-1 | 主要 | 同步 | 自動
| 主要資料中心 | SQL-2 | 次要 | 同步 | 自動
| 次要或遠端資料中心 | SQL-3 | 次要 | 非同步 | 手動


### <a name="more-information-about-planned-and-forced-manual-failover"></a>有關計劃性和強制性容錯移轉的更多詳細資訊

如需詳細資訊，請參閱下列主題中的 hello:

- [執行可用性群組的已規劃手動容錯移轉 (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [執行可用性群組的強制手動容錯移轉 (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>其他連結

* [Always On 可用性群組](http://msdn.microsoft.com/library/hh510230.aspx)
* [Azure 虛擬機器](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Azure Load Balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Azure 可用性設定組](../manage-availability.md)
