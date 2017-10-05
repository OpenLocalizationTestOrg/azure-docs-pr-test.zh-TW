---
title: "設定負載平衡器使用 SQL 一律開啟 | Microsoft Docs"
description: "設定負載平衡器使用 SQL 一律開啟，以及如何運用 powershell 來建立 SQL 實作的負載平衡器"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 68aad6253f185d53fdd7f11c8660c7287ef12655
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="10eb0-103">設定負載平衡器使用 SQL 一律開啟</span><span class="sxs-lookup"><span data-stu-id="10eb0-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="10eb0-104">SQL Server AlwaysOn 可用性群組現在可以與 ILB 搭配執行。</span><span class="sxs-lookup"><span data-stu-id="10eb0-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="10eb0-105">可用性群組是 SQL Server 針對高可用性和災難復原的旗艦解決方案。</span><span class="sxs-lookup"><span data-stu-id="10eb0-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="10eb0-106">不論組態中的複本數目為何，可用性群組接聽程式可讓用戶端應用程式順暢地連接到主要複本。</span><span class="sxs-lookup"><span data-stu-id="10eb0-106">The Availability Group Listener allows client applications to seamlessly connect to the primary replica, irrespective of the number of the replicas in the configuration.</span></span>

<span data-ttu-id="10eb0-107">接聽程式 (DNS) 名稱會對應至負載平衡的 IP 位址，而 Azure 的負載平衡器會將連入流量只導向複本集中的主要伺服器。</span><span class="sxs-lookup"><span data-stu-id="10eb0-107">The listener (DNS) name is mapped to a load-balanced IP address and Azure's load balancer directs the incoming traffic to only the primary server in the replica set.</span></span>

<span data-ttu-id="10eb0-108">您可以使用 ILB 的 SQL Server AlwaysOn (接聽程式) 端點支援。</span><span class="sxs-lookup"><span data-stu-id="10eb0-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="10eb0-109">您現在可以控制接聽程式的存取設定，並且可以從虛擬網路 (VNet) 的特定子網路中選擇負載平衡的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="10eb0-109">You now have control over the accessibility of the listener and can choose the load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="10eb0-110">在接聽程式上使用 ILB 之後，只有下列項目可以存取 SQL Server 端點 (例如 Server=tcp:ListenerName,1433;Database=DatabaseName)：</span><span class="sxs-lookup"><span data-stu-id="10eb0-110">By using ILB on the listener, the SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="10eb0-111">相同虛擬網路中的服務與 VM</span><span class="sxs-lookup"><span data-stu-id="10eb0-111">Services and VMs in the same Virtual network</span></span>
* <span data-ttu-id="10eb0-112">來自已連線內部部署網路的服務與 VM</span><span class="sxs-lookup"><span data-stu-id="10eb0-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="10eb0-113">來自互連式 VNet 的服務與 VM</span><span class="sxs-lookup"><span data-stu-id="10eb0-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="10eb0-115">圖 1 - 使用網際網路面向負載平衡器設定的 SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="10eb0-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-to-the-service"></a><span data-ttu-id="10eb0-116">將內部負載平衡器新增至服務</span><span class="sxs-lookup"><span data-stu-id="10eb0-116">Add Internal Load Balancer to the service</span></span>

1. <span data-ttu-id="10eb0-117">在下列範例中，我們將設定一個包含名為 'Subnet-1' 之子網路的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="10eb0-117">In the following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="10eb0-118">為每個 VM 上的 ILB 新增負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="10eb0-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="10eb0-119">上述範例中，您有 2 個分別稱為 "sqlsvc1" 和 "sqlsvc2" 的 VM 正在雲端服務 "Sqlsvc" 中執行。</span><span class="sxs-lookup"><span data-stu-id="10eb0-119">In the example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in the cloud service "Sqlsvc".</span></span> <span data-ttu-id="10eb0-120">在使用 `DirectServerReturn` 參數建立 ILB 之後，您會將負載平衡的端點新增 ILB，讓 SQL 能針對可用性群組設定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="10eb0-120">After creating the ILB with `DirectServerReturn` switch, you add load balanced endpoints to the ILB to allow SQL to configure the listeners for the availability groups.</span></span>

<span data-ttu-id="10eb0-121">如需有關 SQL AlwaysOn 的詳細資訊，請參閱[針對 Azure 中的 AlwaysOn 可用性群組設定內部負載平衡器](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="10eb0-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="10eb0-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="10eb0-122">See Also</span></span>
[<span data-ttu-id="10eb0-123">開始設定網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="10eb0-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="10eb0-124">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="10eb0-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="10eb0-125">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="10eb0-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="10eb0-126">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="10eb0-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
