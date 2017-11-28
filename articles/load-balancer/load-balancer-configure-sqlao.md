---
title: "sql alwayson aaaConfigure 負載平衡器 |Microsoft 文件"
description: "使用 SQL alwayson 和 tooleverage powershell toocreate 載入 hello SQL 實作用於負載平衡器的方式來設定負載平衡器 toowork"
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
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a><span data-ttu-id="30c62-103">設定負載平衡器使用 SQL 一律開啟</span><span class="sxs-lookup"><span data-stu-id="30c62-103">Configure load balancer for SQL always on</span></span>

<span data-ttu-id="30c62-104">SQL Server AlwaysOn 可用性群組現在可以與 ILB 搭配執行。</span><span class="sxs-lookup"><span data-stu-id="30c62-104">SQL Server AlwaysOn Availability Groups can now be run with ILB.</span></span> <span data-ttu-id="30c62-105">可用性群組是 SQL Server 針對高可用性和災難復原的旗艦解決方案。</span><span class="sxs-lookup"><span data-stu-id="30c62-105">Availability Group is SQL Server's flagship solution for high availability and disaster recovery.</span></span> <span data-ttu-id="30c62-106">hello 可用性群組接聽程式可讓用戶端應用程式 tooseamlessly 連接 toohello 主要複本，無論 hello hello 組態中的 hello 複本數目。</span><span class="sxs-lookup"><span data-stu-id="30c62-106">hello Availability Group Listener allows client applications tooseamlessly connect toohello primary replica, irrespective of hello number of hello replicas in hello configuration.</span></span>

<span data-ttu-id="30c62-107">hello 接聽程式 (DNS) 名稱對應的 tooa 負載平衡 IP 位址，且 Azure 的負載平衡器會指示 hello 連入流量 tooonly hello 主要伺服器 hello 複本集中。</span><span class="sxs-lookup"><span data-stu-id="30c62-107">hello listener (DNS) name is mapped tooa load-balanced IP address and Azure's load balancer directs hello incoming traffic tooonly hello primary server in hello replica set.</span></span>

<span data-ttu-id="30c62-108">您可以使用 ILB 的 SQL Server AlwaysOn (接聽程式) 端點支援。</span><span class="sxs-lookup"><span data-stu-id="30c62-108">You can use ILB support for SQL Server AlwaysOn (listener) endpoints.</span></span> <span data-ttu-id="30c62-109">您現在控制 hello hello 接聽程式的存取範圍，也可以選擇從特定的子網路的負載平衡 IP 位址的 hello 虛擬網路 (VNet) 中。</span><span class="sxs-lookup"><span data-stu-id="30c62-109">You now have control over hello accessibility of hello listener and can choose hello load-balanced IP address from a specific subnet in your Virtual Network (VNet).</span></span>

<span data-ttu-id="30c62-110">藉由使用 hello 接聽程式的 ILB，hello SQL server 端點 (例如 Server = tcp:ListenerName，1433; Database = DatabaseName) 只能藉由存取：</span><span class="sxs-lookup"><span data-stu-id="30c62-110">By using ILB on hello listener, hello SQL server endpoint (e.g. Server=tcp:ListenerName,1433;Database=DatabaseName) is accessible only by:</span></span>

* <span data-ttu-id="30c62-111">服務和 Vm 中的 hello 相同虛擬網路</span><span class="sxs-lookup"><span data-stu-id="30c62-111">Services and VMs in hello same Virtual network</span></span>
* <span data-ttu-id="30c62-112">來自已連線內部部署網路的服務與 VM</span><span class="sxs-lookup"><span data-stu-id="30c62-112">Services and VMs from connected on-premises network</span></span>
* <span data-ttu-id="30c62-113">來自互連式 VNet 的服務與 VM</span><span class="sxs-lookup"><span data-stu-id="30c62-113">Services and VMs from interconnected VNets</span></span>

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

<span data-ttu-id="30c62-115">圖 1 - 使用網際網路面向負載平衡器設定的 SQL AlwaysOn</span><span class="sxs-lookup"><span data-stu-id="30c62-115">Figure 1 - SQL AlwaysOn configured with Internet-facing load balancer</span></span>

## <a name="add-internal-load-balancer-toohello-service"></a><span data-ttu-id="30c62-116">加入內部負載平衡器 toohello 服務</span><span class="sxs-lookup"><span data-stu-id="30c62-116">Add Internal Load Balancer toohello service</span></span>

1. <span data-ttu-id="30c62-117">在下列範例的 hello，我們會設定包含名稱為 ' 的子網路 1' 的子網路的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="30c62-117">In hello following example, we will configure a Virtual network that contains a subnet  called 'Subnet-1':</span></span>

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. <span data-ttu-id="30c62-118">為每個 VM 上的 ILB 新增負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="30c62-118">Add load balanced endpoints for ILB on each VM</span></span>

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    <span data-ttu-id="30c62-119">在 hello 上述範例中，您有 2 VM 稱為 「 sqlsvc1 」 以及 「 sqlsvc2 「 執行中 hello 雲端服務 」 Sqlsvc"。</span><span class="sxs-lookup"><span data-stu-id="30c62-119">In hello example above, you have 2 VM's called "sqlsvc1" and "sqlsvc2" running in hello cloud service "Sqlsvc".</span></span> <span data-ttu-id="30c62-120">在建立之後 hello 與 ILB`DirectServerReturn`切換時，您將加入負載平衡的端點 toohello ILB tooallow SQL tooconfigure hello 接聽程式，以 hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="30c62-120">After creating hello ILB with `DirectServerReturn` switch, you add load balanced endpoints toohello ILB tooallow SQL tooconfigure hello listeners for hello availability groups.</span></span>

<span data-ttu-id="30c62-121">如需有關 SQL AlwaysOn 的詳細資訊，請參閱[針對 Azure 中的 AlwaysOn 可用性群組設定內部負載平衡器](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)。</span><span class="sxs-lookup"><span data-stu-id="30c62-121">For more information about SQL AlwaysOn, see [Configure an internal load balancer for an AlwaysOn availability group in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="30c62-122">另請參閱</span><span class="sxs-lookup"><span data-stu-id="30c62-122">See Also</span></span>
[<span data-ttu-id="30c62-123">開始設定網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="30c62-123">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="30c62-124">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="30c62-124">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="30c62-125">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="30c62-125">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="30c62-126">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="30c62-126">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
