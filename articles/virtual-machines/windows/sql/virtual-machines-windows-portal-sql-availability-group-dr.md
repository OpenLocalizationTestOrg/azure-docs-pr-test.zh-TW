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
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="a44ef-103">在不同區域的 Azure 虛擬機器上設定 Always On 可用性群組</span><span class="sxs-lookup"><span data-stu-id="a44ef-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="a44ef-104">本文說明如何 tooconfigure SQL Server Always On 可用性群組在遠端的 Azure 位置的 Azure 虛擬機器上的複本。</span><span class="sxs-lookup"><span data-stu-id="a44ef-104">This article explains how tooconfigure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="a44ef-105">使用此組態 toosupport 災害復原。</span><span class="sxs-lookup"><span data-stu-id="a44ef-105">Use this configuration toosupport disaster recovery.</span></span>

<span data-ttu-id="a44ef-106">本文適用於在 Resource Manager 模式 tooAzure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a44ef-106">This article applies tooAzure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="a44ef-107">hello 下列影像顯示常見的部署可用性群組的 Azure 虛擬機器上：</span><span class="sxs-lookup"><span data-stu-id="a44ef-107">hello following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="a44ef-109">在此部署中，所有虛擬機器都位於一個 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="a44ef-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="a44ef-110">hello 可用性群組複本可能會包含在 SQL 1 和 SQL 2 上的自動容錯移轉的同步認可。</span><span class="sxs-lookup"><span data-stu-id="a44ef-110">hello availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="a44ef-111">toobuild 這種架構，請參閱[可用性群組的範本或教學課程](virtual-machines-windows-portal-sql-availability-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-111">toobuild this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="a44ef-112">此架構是很容易遭受 toodowntime 如果 hello Azure 地區變成無法存取。</span><span class="sxs-lookup"><span data-stu-id="a44ef-112">This architecture is vulnerable toodowntime if hello Azure region becomes inaccessible.</span></span> <span data-ttu-id="a44ef-113">tooovercome 這項弱點，將複本加入不同的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="a44ef-113">tooovercome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="a44ef-114">hello 下圖顯示 hello 新架構的外觀：</span><span class="sxs-lookup"><span data-stu-id="a44ef-114">hello following diagram shows how hello new architecture would look:</span></span>

   ![可用性群組 DR](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="a44ef-116">hello 上圖顯示名 SQL 3 的新虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a44ef-116">hello preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="a44ef-117">SQL-3 位於不同的 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="a44ef-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="a44ef-118">SQL 3 就會加入 toohello Windows Server 容錯移轉叢集。</span><span class="sxs-lookup"><span data-stu-id="a44ef-118">SQL-3 is added toohello Windows Server Failover Cluster.</span></span> <span data-ttu-id="a44ef-119">SQL-3 可以裝載可用性群組複本。</span><span class="sxs-lookup"><span data-stu-id="a44ef-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="a44ef-120">最後，請注意該 hello Azure 地區 SQL 3 有新的 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a44ef-120">Finally, notice that hello Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="a44ef-121">多個虛擬機器處於 hello 相同區域時，需要 Azure 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="a44ef-121">An Azure availability set is required when more than one virtual machine is in hello same region.</span></span> <span data-ttu-id="a44ef-122">如果只有一部虛擬機器是在 hello 區域中，則不需要 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="a44ef-122">If only one virtual machine is in hello region, then hello availability set is not required.</span></span> <span data-ttu-id="a44ef-123">您只能在建立虛擬機器時將其置於可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="a44ef-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="a44ef-124">如果 hello 虛擬機器已在可用性設定組中，您可以加入稍後新增額外的複本虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a44ef-124">If hello virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="a44ef-125">在這種架構，通常會設定 hello 遠端區域中的 hello 複本使用非同步認可可用性模式和手動容錯移轉模式。</span><span class="sxs-lookup"><span data-stu-id="a44ef-125">In this architecture, hello replica in hello remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="a44ef-126">當可用性群組複本位於不同 Azure 區域中的 Azure 虛擬機器上時，每個區域需要：</span><span class="sxs-lookup"><span data-stu-id="a44ef-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="a44ef-127">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="a44ef-127">A virtual network gateway</span></span>
* <span data-ttu-id="a44ef-128">虛擬網路閘道連線</span><span class="sxs-lookup"><span data-stu-id="a44ef-128">A virtual network gateway connection</span></span>

<span data-ttu-id="a44ef-129">hello 下列圖表顯示 hello 網路資料中心之間的通訊方式。</span><span class="sxs-lookup"><span data-stu-id="a44ef-129">hello following diagram shows how hello networks communicate between data centers.</span></span>

   ![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="a44ef-131">此架構會針對 Azure 區域之間複寫的資料產生輸出資料費用。</span><span class="sxs-lookup"><span data-stu-id="a44ef-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="a44ef-132">請參閱[頻寬定價](http://azure.microsoft.com/pricing/details/bandwidth/)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="a44ef-133">建立遠端複本</span><span class="sxs-lookup"><span data-stu-id="a44ef-133">Create remote replica</span></span>

<span data-ttu-id="a44ef-134">toocreate 複本，以在遠端資料中心內，下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="a44ef-134">toocreate a replica in a remote data center, do hello following steps:</span></span>

1. <span data-ttu-id="a44ef-135">[在 hello 新區域中建立虛擬網路](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-135">[Create a virtual network in hello new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="a44ef-136">[設定 VNet 對 VNet 連線使用 hello Azure 入口網站](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-136">[Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="a44ef-137">在某些情況下，您可能需要 toouse PowerShell toocreate hello VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="a44ef-137">In some cases, you may have toouse PowerShell toocreate hello VNet-to-VNet connection.</span></span> <span data-ttu-id="a44ef-138">例如，如果您使用不同的 Azure 帳戶，您無法設定 hello 連接 hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a44ef-138">For example, if you use different Azure accounts you cannot configure hello connection in hello portal.</span></span> <span data-ttu-id="a44ef-139">在此情況下查看，[設定 VNet 對 VNet 連線使用 hello Azure 入口網站](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-139">In this case see, [Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="a44ef-140">[在 hello 新區域中建立的網域控制站](../../../active-directory/active-directory-new-forest-virtual-machine.md)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-140">[Create a domain controller in hello new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="a44ef-141">如果 hello hello 主要站台中的網域控制站無法使用此網域控制站會提供驗證。</span><span class="sxs-lookup"><span data-stu-id="a44ef-141">This domain controller provides authentication if hello domain controller in hello primary site is not available.</span></span>

1. <span data-ttu-id="a44ef-142">[在 hello 新的區域中建立 SQL Server 虛擬機器](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-142">[Create a SQL Server virtual machine in hello new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="a44ef-143">[在 hello hello 新區域上的網路中建立 Azure 負載平衡器](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-143">[Create an Azure load balancer in hello network on hello new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="a44ef-144">此負載平衡器必須：</span><span class="sxs-lookup"><span data-stu-id="a44ef-144">This load balancer must:</span></span>

   - <span data-ttu-id="a44ef-145">在 hello 相同網路和子網路，如 hello 新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a44ef-145">Be in hello same network and subnet as hello new virtual machine.</span></span>
   - <span data-ttu-id="a44ef-146">擁有 hello 可用性群組接聽程式的靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a44ef-146">Have a static IP address for hello availability group listener.</span></span>
   - <span data-ttu-id="a44ef-147">包含組成僅 hello 中的虛擬機器 hello 相同的區域，因為 hello 負載平衡器後端集區。</span><span class="sxs-lookup"><span data-stu-id="a44ef-147">Include a backend pool consisting of only hello virtual machines in hello same region as hello load balancer.</span></span>
   - <span data-ttu-id="a44ef-148">使用 TCP 連接埠探查 toohello 特定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a44ef-148">Use a TCP port probe specific toohello IP address.</span></span>
   - <span data-ttu-id="a44ef-149">負載平衡規則特定 toohello SQL Server，hello 中的相同的區域。</span><span class="sxs-lookup"><span data-stu-id="a44ef-149">Have a load balancing rule specific toohello SQL Server in hello same region.</span></span>  

1. <span data-ttu-id="a44ef-150">[新增容錯移轉叢集功能 toohello 新的 SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-150">[Add Failover Clustering feature toohello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="a44ef-151">[加入新 SQL Server toohello 網域 hello](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-151">[Join hello new SQL Server toohello domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="a44ef-152">[網域帳戶設定 hello 新 SQL Server 服務帳戶 toouse](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-152">[Set hello new SQL Server service account toouse a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="a44ef-153">[加入新 SQL Server toohello hello Windows Server 容錯移轉叢集](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-153">[Add hello new SQL Server toohello Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="a44ef-154">Hello 叢集上建立 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="a44ef-154">Create an IP address resource on hello cluster.</span></span>

   <span data-ttu-id="a44ef-155">您可以在 [容錯移轉叢集管理員] 中建立 hello IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="a44ef-155">You can create hello IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="a44ef-156">以滑鼠右鍵按一下 hello 可用性群組角色中，按一下**加入資源**，**更資源**，按一下**IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="a44ef-156">Right-click hello availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![建立 IP 位址](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="a44ef-158">請依照下列方式設定此 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="a44ef-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="a44ef-159">使用 hello 網路 hello 遠端資料中心。</span><span class="sxs-lookup"><span data-stu-id="a44ef-159">Use hello network from hello remote data center.</span></span>
   - <span data-ttu-id="a44ef-160">從 hello 新 Azure 負載平衡器的 hello IP 位址指派。</span><span class="sxs-lookup"><span data-stu-id="a44ef-160">Assign hello IP address from hello new Azure load balancer.</span></span> 

1. <span data-ttu-id="a44ef-161">在 hello 新的 SQL Server 在 SQL Server 組態管理員[啟用 Alwayson 可用性群組](http://msdn.microsoft.com/library/ff878259.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-161">On hello new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="a44ef-162">[開啟防火牆連接埠上的 hello 新的 SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-162">[Open firewall ports on hello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="a44ef-163">hello 連接埠號碼需要 tooopen 取決於您的環境。</span><span class="sxs-lookup"><span data-stu-id="a44ef-163">hello port numbers you need tooopen depend on your environment.</span></span> <span data-ttu-id="a44ef-164">開啟的連接埠鏡像端點與 Azure 的 hello 負載平衡器健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="a44ef-164">Open ports for hello mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="a44ef-165">[加入複本 toohello 可用性群組上 hello 新的 SQL Server](http://msdn.microsoft.com/library/hh213239.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-165">[Add a replica toohello availability group on hello new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="a44ef-166">針對遠端 Azure 區域中的複本，請設定它來進行非同步複寫搭配手動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="a44ef-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="a44ef-167">為 hello 接聽程式的用戶端存取點 （網路名稱） 叢集的相依性加入 hello IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="a44ef-167">Add hello IP address resource as a dependency for hello listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="a44ef-168">hello 下列螢幕擷取畫面顯示已正確設定的 IP 位址叢集資源：</span><span class="sxs-lookup"><span data-stu-id="a44ef-168">hello following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![可用性群組](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="a44ef-170">hello 叢集資源群組包含兩個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a44ef-170">hello cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="a44ef-171">兩個 IP 位址是 hello 接聽程式用戶端存取點的相依性。</span><span class="sxs-lookup"><span data-stu-id="a44ef-171">Both IP addresses are dependencies for hello listener client access point.</span></span> <span data-ttu-id="a44ef-172">使用 hello**或**hello 叢集相依性設定中的運算子。</span><span class="sxs-lookup"><span data-stu-id="a44ef-172">Use hello **OR** operator in hello cluster dependency configuration.</span></span>

1. <span data-ttu-id="a44ef-173">[在 PowerShell 中設定 hello 叢集參數](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-173">[Set hello cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="a44ef-174">Hello 叢集網路名稱、 IP 位址與 hello hello 新區域中的負載平衡器所設定的探查連接埠執行 hello PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="a44ef-174">Run hello PowerShell script with hello cluster network name, IP address, and probe port that you configured on hello load balancer in hello new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="a44ef-175">設定多個子網路的連線</span><span class="sxs-lookup"><span data-stu-id="a44ef-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="a44ef-176">hello 遠端資料中心中的 hello 複本 hello 可用性群組的一部分，但是它為不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="a44ef-176">hello replica in hello remote data center is part of hello availability group but it is in a different subnet.</span></span> <span data-ttu-id="a44ef-177">如果此複本會變成 hello 主要複本，可能會發生應用程式連接逾時。</span><span class="sxs-lookup"><span data-stu-id="a44ef-177">If this replica becomes hello primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="a44ef-178">此行為是 hello 與內部部署可用性群組多重子網路部署在相同的。</span><span class="sxs-lookup"><span data-stu-id="a44ef-178">This behavior is hello same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="a44ef-179">tooallow 連接從用戶端應用程式，請更新 hello 用戶端連線，或是設定 hello 叢集網路名稱資源的快取的名稱解析。</span><span class="sxs-lookup"><span data-stu-id="a44ef-179">tooallow connections from client applications, either update hello client connection or configure name resolution caching on hello cluster network name resource.</span></span>

<span data-ttu-id="a44ef-180">最好是更新 hello 用戶端連接字串 tooset `MultiSubnetFailover=Yes`。</span><span class="sxs-lookup"><span data-stu-id="a44ef-180">Preferably, update hello client connection strings tooset `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="a44ef-181">請參閱[使用 MultiSubnetFailover 進行連接](http://msdn.microsoft.com/library/gg471494#Anchor_0)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="a44ef-182">如果您無法修改 hello 連接字串，您可以設定快取的名稱解析。</span><span class="sxs-lookup"><span data-stu-id="a44ef-182">If you cannot modify hello connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="a44ef-183">請參閱[多子網路可用性群組中的連線逾時 (英文)](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/)。</span><span class="sxs-lookup"><span data-stu-id="a44ef-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-tooremote-region"></a><span data-ttu-id="a44ef-184">容錯移轉 tooremote 區域</span><span class="sxs-lookup"><span data-stu-id="a44ef-184">Fail over tooremote region</span></span>

<span data-ttu-id="a44ef-185">tootest 接聽程式連線能力 toohello 遠端區域中，您可以容錯移轉 hello 複本 toohello 遠端區域。</span><span class="sxs-lookup"><span data-stu-id="a44ef-185">tootest listener connectivity toohello remote region, you can fail over hello replica toohello remote region.</span></span> <span data-ttu-id="a44ef-186">非同步 hello 複本時，容錯移轉不會受到 toopotential 資料遺失。</span><span class="sxs-lookup"><span data-stu-id="a44ef-186">While hello replica is asynchronous, failover is vulnerable toopotential data loss.</span></span> <span data-ttu-id="a44ef-187">不會遺失資料，透過 toofail 變更 hello 可用性模式 toosynchronous，以及設定 hello 容錯移轉模式 tooautomatic。</span><span class="sxs-lookup"><span data-stu-id="a44ef-187">toofail over without data loss, change hello availability mode toosynchronous and set hello failover mode tooautomatic.</span></span> <span data-ttu-id="a44ef-188">使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a44ef-188">Use hello following steps:</span></span>

1. <span data-ttu-id="a44ef-189">在**物件總管 中**，連線 toohello 裝載 hello 主要複本的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a44ef-189">In **Object Explorer**, connect toohello instance of SQL Server that hosts hello primary replica.</span></span>
1. <span data-ttu-id="a44ef-190">在 [AlwaysOn 可用性群組]、[可用性群組] 底下，於您的可用性群組上按一下滑鼠右鍵，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="a44ef-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="a44ef-191">在 hello**一般**頁面的 **可用性複本**，組 hello 中的次要複本 hello DR 網站 toouse**同步認可**可用性模式與**自動**容錯移轉模式。</span><span class="sxs-lookup"><span data-stu-id="a44ef-191">On hello **General** page, under **Availability Replicas**, set hello secondary replica in hello DR site toouse **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="a44ef-192">如果您在相同的主要複本的高可用性站台的次要複本，將此複本太**非同步認可**和**手動**。</span><span class="sxs-lookup"><span data-stu-id="a44ef-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica too**Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="a44ef-193">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a44ef-193">Click OK.</span></span>
1. <span data-ttu-id="a44ef-194">在**物件總管 中**，以滑鼠右鍵按一下 hello 可用性群組，然後按一下**顯示儀表板**。</span><span class="sxs-lookup"><span data-stu-id="a44ef-194">In **Object Explorer**, right-click hello availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="a44ef-195">在 hello 儀表板中，確認該 hello hello DR 網站上的複本同步處理。</span><span class="sxs-lookup"><span data-stu-id="a44ef-195">On hello dashboard, verify that hello replica on hello DR site is synchronized.</span></span>
1. <span data-ttu-id="a44ef-196">在**物件總管 中**，以滑鼠右鍵按一下 hello 可用性群組，然後按一下**容錯移轉...**.SQL Server Management Studio 開啟精靈 toofail 透過 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="a44ef-196">In **Object Explorer**, right-click hello availability group, and click **Failover...**. SQL Server Management Studios opens a wizard toofail over SQL Server.</span></span>  
1. <span data-ttu-id="a44ef-197">按一下**下一步**，並選取 hello hello DR 網站中的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a44ef-197">Click **Next**, and select hello SQL Server instance in hello DR site.</span></span> <span data-ttu-id="a44ef-198">再按一下 [下一步]  。</span><span class="sxs-lookup"><span data-stu-id="a44ef-198">Click **Next** again.</span></span>
1. <span data-ttu-id="a44ef-199">連接 toohello hello DR 網站中的 SQL Server 執行個體，並按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="a44ef-199">Connect toohello SQL Server instance in hello DR site and click **Next**.</span></span>
1. <span data-ttu-id="a44ef-200">在 hello**摘要**頁面上，確認 hello 設定，然後按一下 **完成**。</span><span class="sxs-lookup"><span data-stu-id="a44ef-200">On hello **Summary** page, verify hello settings and click **Finish**.</span></span>

<span data-ttu-id="a44ef-201">測試連線之後, 移動 hello 主要複本後 tooyour 主要資料中心，且設定 hello 可用性模式後 tootheir 一般作業系統設定。</span><span class="sxs-lookup"><span data-stu-id="a44ef-201">After testing connectivity, move hello primary replica back tooyour primary data center and set hello availability mode back tootheir normal operating settings.</span></span> <span data-ttu-id="a44ef-202">hello 下表顯示 hello 正常操作設定這份文件中所描述的 hello 架構：</span><span class="sxs-lookup"><span data-stu-id="a44ef-202">hello following table shows hello normal operational settings for hello architecture described in this document:</span></span>

| <span data-ttu-id="a44ef-203">位置</span><span class="sxs-lookup"><span data-stu-id="a44ef-203">Location</span></span> | <span data-ttu-id="a44ef-204">伺服器執行個體</span><span class="sxs-lookup"><span data-stu-id="a44ef-204">Server Instance</span></span> | <span data-ttu-id="a44ef-205">角色</span><span class="sxs-lookup"><span data-stu-id="a44ef-205">Role</span></span> | <span data-ttu-id="a44ef-206">可用性模式</span><span class="sxs-lookup"><span data-stu-id="a44ef-206">Availability Mode</span></span> | <span data-ttu-id="a44ef-207">容錯移轉模式</span><span class="sxs-lookup"><span data-stu-id="a44ef-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="a44ef-208">主要資料中心</span><span class="sxs-lookup"><span data-stu-id="a44ef-208">Primary data center</span></span> | <span data-ttu-id="a44ef-209">SQL-1</span><span class="sxs-lookup"><span data-stu-id="a44ef-209">SQL-1</span></span> | <span data-ttu-id="a44ef-210">主要</span><span class="sxs-lookup"><span data-stu-id="a44ef-210">Primary</span></span> | <span data-ttu-id="a44ef-211">同步</span><span class="sxs-lookup"><span data-stu-id="a44ef-211">Synchronous</span></span> | <span data-ttu-id="a44ef-212">自動</span><span class="sxs-lookup"><span data-stu-id="a44ef-212">Automatic</span></span>
| <span data-ttu-id="a44ef-213">主要資料中心</span><span class="sxs-lookup"><span data-stu-id="a44ef-213">Primary data center</span></span> | <span data-ttu-id="a44ef-214">SQL-2</span><span class="sxs-lookup"><span data-stu-id="a44ef-214">SQL-2</span></span> | <span data-ttu-id="a44ef-215">次要</span><span class="sxs-lookup"><span data-stu-id="a44ef-215">Secondary</span></span> | <span data-ttu-id="a44ef-216">同步</span><span class="sxs-lookup"><span data-stu-id="a44ef-216">Synchronous</span></span> | <span data-ttu-id="a44ef-217">自動</span><span class="sxs-lookup"><span data-stu-id="a44ef-217">Automatic</span></span>
| <span data-ttu-id="a44ef-218">次要或遠端資料中心</span><span class="sxs-lookup"><span data-stu-id="a44ef-218">Secondary or remote data center</span></span> | <span data-ttu-id="a44ef-219">SQL-3</span><span class="sxs-lookup"><span data-stu-id="a44ef-219">SQL-3</span></span> | <span data-ttu-id="a44ef-220">次要</span><span class="sxs-lookup"><span data-stu-id="a44ef-220">Secondary</span></span> | <span data-ttu-id="a44ef-221">非同步</span><span class="sxs-lookup"><span data-stu-id="a44ef-221">Asynchronous</span></span> | <span data-ttu-id="a44ef-222">手動</span><span class="sxs-lookup"><span data-stu-id="a44ef-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="a44ef-223">有關計劃性和強制性容錯移轉的更多詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a44ef-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="a44ef-224">如需詳細資訊，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="a44ef-224">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="a44ef-225">執行可用性群組的已規劃手動容錯移轉 (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="a44ef-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="a44ef-226">執行可用性群組的強制手動容錯移轉 (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="a44ef-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="a44ef-227">其他連結</span><span class="sxs-lookup"><span data-stu-id="a44ef-227">Additional Links</span></span>

* [<span data-ttu-id="a44ef-228">Always On 可用性群組</span><span class="sxs-lookup"><span data-stu-id="a44ef-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="a44ef-229">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a44ef-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="a44ef-230">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="a44ef-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="a44ef-231">Azure 可用性設定組</span><span class="sxs-lookup"><span data-stu-id="a44ef-231">Azure Availability Sets</span></span>](../manage-availability.md)
