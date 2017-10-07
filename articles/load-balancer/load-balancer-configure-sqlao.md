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
# <a name="configure-load-balancer-for-sql-always-on"></a>設定負載平衡器使用 SQL 一律開啟

SQL Server AlwaysOn 可用性群組現在可以與 ILB 搭配執行。 可用性群組是 SQL Server 針對高可用性和災難復原的旗艦解決方案。 hello 可用性群組接聽程式可讓用戶端應用程式 tooseamlessly 連接 toohello 主要複本，無論 hello hello 組態中的 hello 複本數目。

hello 接聽程式 (DNS) 名稱對應的 tooa 負載平衡 IP 位址，且 Azure 的負載平衡器會指示 hello 連入流量 tooonly hello 主要伺服器 hello 複本集中。

您可以使用 ILB 的 SQL Server AlwaysOn (接聽程式) 端點支援。 您現在控制 hello hello 接聽程式的存取範圍，也可以選擇從特定的子網路的負載平衡 IP 位址的 hello 虛擬網路 (VNet) 中。

藉由使用 hello 接聽程式的 ILB，hello SQL server 端點 (例如 Server = tcp:ListenerName，1433; Database = DatabaseName) 只能藉由存取：

* 服務和 Vm 中的 hello 相同虛擬網路
* 來自已連線內部部署網路的服務與 VM
* 來自互連式 VNet 的服務與 VM

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

圖 1 - 使用網際網路面向負載平衡器設定的 SQL AlwaysOn

## <a name="add-internal-load-balancer-toohello-service"></a>加入內部負載平衡器 toohello 服務

1. 在下列範例的 hello，我們會設定包含名稱為 ' 的子網路 1' 的子網路的虛擬網路：

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. 為每個 VM 上的 ILB 新增負載平衡端點

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    在 hello 上述範例中，您有 2 VM 稱為 「 sqlsvc1 」 以及 「 sqlsvc2 「 執行中 hello 雲端服務 」 Sqlsvc"。 在建立之後 hello 與 ILB`DirectServerReturn`切換時，您將加入負載平衡的端點 toohello ILB tooallow SQL tooconfigure hello 接聽程式，以 hello 可用性群組。

如需有關 SQL AlwaysOn 的詳細資訊，請參閱[針對 Azure 中的 AlwaysOn 可用性群組設定內部負載平衡器](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)。

## <a name="see-also"></a>另請參閱
[開始設定網際網路面向的負載平衡器](load-balancer-get-started-internet-arm-ps.md)

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
