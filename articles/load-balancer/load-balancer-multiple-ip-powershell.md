---
title: "在 Azure 中的多個 IP 組態上的平衡 aaaLoad |Microsoft 文件"
description: "在主要和次要 IP 組態間進行負載平衡。"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a>使用 PowerShell 在多個 IP 組態上進行負載平衡

> [!div class="op_single_selector"]
> * [入口網站](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

本文說明如何 toouse Azure 負載平衡器與多個 IP 位址上的次要網路介面 (NIC)。 在此案例中，我們有兩部執行 Windows 的 VM，每部各有一個主要和次要 NIC。 每個次要 hello Nic 有兩個 IP 組態。 每部 VM 都裝載 contoso.com 和 fabrikam.com 兩個網站。每個網站會繫結的 tooone 的 hello hello 次要 NIC 上的 IP 組態 我們使用 Azure 負載平衡器 tooexpose 兩個前端 IP 位址，一個用於每個網站，toodistribute 流量 toohello 個別的 IP 組態 hello 網站。 這種情況下使用 hello 跨前端，以及兩個後端集區 IP 位址相同的連接埠號碼。

![LB 案例影像](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>多個 IP 組態步驟 tooload 餘額

請遵循下面這篇文章所述的 tooachieve hello 案例 hello 步驟：

1. 安裝 Azure PowerShell。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關安裝 hello 最新版本的 Azure PowerShell 中，選取您的訂閱，並登入 tooyour 帳戶資訊。
2. 建立資源群組使用 hello 下列設定：

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    如需詳細資訊，請參閱[建立資源群組](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)的步驟 2。

3. [建立可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json)toocontain Vm。 此案例中，使用下列命令的 hello:

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. 請依照下列指示步驟 3 至 5[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)文章 tooprepare hello 建立與單一 NIC VM 執行步驟 6.1，並使用 hello 下列而非 6.2 步驟：

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    然後完成[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)的步驟 6.3 至 6.8。

5. 新增第二個 IP 組態 tooeach 的 hello Vm。 請依照下列中的 hello 指示[指派多個 IP 位址 toovirtual 機器](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add)發行項。 使用下列組態設定的 hello:

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    您不需要此教學課程中的 hello 目的 tooassociate hello 次要 IP 組態與公用 Ip。 編輯 hello 命令 tooremove hello 公用 IP 關聯組件。

6. 針對 VM2 再次完成本文的步驟 4 到 6。 這項操作時，是確定 tooreplace hello VM 名稱 tooVM2。 請注意，您不需要虛擬網路 toocreate hello 第二個 VM。 視您的使用案例而定，您不一定需要建立新的子網路。

7. 建立兩個公用 IP 位址，並將其儲存在 hello 適當的變數，如下所示：

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. 建立兩個前端 IP 組態：

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. 建立後端位址集區、探查和負載平衡規則︰

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. 建立好這些資源後，請建立負載平衡器︰

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. 新增 hello 第二個後端位址集區和前端 IP 組態 tooyour 新建立的負載平衡器：

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. 下列的 hello 命令取得 hello Nic，並將每個次要 NIC toohello 後端位址集區的 hello 這兩個 ipconfiguration 的負載平衡器：

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. 最後，您必須設定 DNS 資源記錄 toopoint toohello 各自的前端 IP 位址的 hello 負載平衡器。 您可以在 Azure DNS 中裝載網域。 如需搭配使用 Azure DNS 與 Load Balancer 的詳細資訊，請參閱[使用 Azure DNS 搭配其他 Azure 服務](../dns/dns-for-azure-services.md)。

## <a name="next-steps"></a>後續步驟
- 深入了解如何 toocombine 負載平衡服務在 Azure 中[在 Azure 中使用負載平衡服務](../traffic-manager/traffic-manager-load-balancing-azure.md)。
- 了解如何在 Azure toomanage 中使用不同類型的記錄檔，以及疑難排解負載平衡器中的[Azure 負載平衡器的記錄分析](../load-balancer/load-balancer-monitor-log.md)。
