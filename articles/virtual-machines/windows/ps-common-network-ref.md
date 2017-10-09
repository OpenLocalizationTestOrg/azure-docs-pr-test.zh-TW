---
title: "aaaCommon PowerShell 命令的 Azure 虛擬網路 |Microsoft 文件"
description: "常見的 PowerShell 命令的 tooget 啟動 建立 Vm 的虛擬網路和其相關聯的資源。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 56e1a73c-8299-4996-bd03-f74585caa1dc
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b46b78f1b7c5a0c5ba917fb48f568d871e5e8789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-azure-virtual-networks"></a>Azure 虛擬網路的常用 PowerShell 命令

如果您想 toocreate 虛擬機器，您需要 toocreate[虛擬網路](../../virtual-network/virtual-networks-overview.md)或不知道哪些 hello VM 可以加入現有的虛擬網路。 一般而言，當您建立 VM 時，您也需要 tooconsider 建立 hello 本文中所述的資源。

請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關安裝 hello 最新版本的 Azure PowerShell 中，選取您的訂閱，並登入 tooyour 帳戶資訊。

如果一個以上的 hello 命令執行本文中，可能適用於您的部分變數：

- $location-hello hello 網路資源的位置。 您可以使用[Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind[地理區域](https://azure.microsoft.com/regions/)適合您。
- $myResourceGroup-hello hello 網路資源位於何處的 hello 資源群組名稱。

## <a name="create-network-resources"></a>建立網路資源

| Task | 命令 |
| ---- | ------- |
| 建立子網路組態 |$subnet1 = [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -AddressPrefix XX.X.X.X/XX<BR>$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet2" -AddressPrefix XX.X.X.X/XX<BR><BR>一般網路可能有[網際網路面向負載平衡器](../../load-balancer/load-balancer-internet-overview.md)的子網路和[內部負載平衡器](../../load-balancer/load-balancer-internal-overview.md)的不同子網路。 |
| 建立虛擬網路 |$vnet = [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup -Location $location -AddressPrefix XX.X.X.X/XX -Subnet $subnet1, $subnet2 |
| 唯一網域名稱的測試 |[Test-AzureRmDnsAvailability](https://docs.microsoft.com/powershell/module/azurerm.network/test-azurermdnsavailability) -DomainNameLabel "myDNS" -Location $location<BR><BR>您可以指定的 DNS 網域名稱[公用 IP 資源](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)，它會建立 domainname.location.cloudapp.azure.com toohello 公用 IP 位址的對應中 hello Azure 受管理 DNS 伺服器。 hello 名稱只能包含字母、 數字和連字號。 hello 第一個和最後一個字元必須是字母或數字和 hello 網域名稱內必須是唯一的 Azure 位置。 如果傳回 **True** ，表示您提出的名稱是全域唯一的。 |
| 建立公用 IP 位址 |$pip = [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermpublicipaddress) -Name "myPublicIp" -ResourceGroupName $myResourceGroup -DomainNameLabel "myDNS" -Location $location -AllocationMethod Dynamic<BR><BR>hello 公用 IP 位址會使用先前測試且可由 hello 前端組態 hello 負載平衡器的 hello 網域名稱。 |
| 建立前端 IP 組態 |$frontendIP = [New-AzureRmLoadBalancerFrontendIpConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) -Name "myFrontendIP" -PublicIpAddress $pip<BR><BR>hello 前端組態包括 hello 公用 IP 位址，您先前建立的連入網路流量。 |
| 建立後端位址集區 |$beAddressPool = [New-AzureRmLoadBalancerBackendAddressPoolConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) -Name "myBackendAddressPool"<BR><BR>提供內部的 hello hello 後端位址的負載平衡器可透過網路介面存取。 |
| 建立探查 |$healthProbe = [New-AzureRmLoadBalancerProbeConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) -Name "myProbe" -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2<BR><BR>包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。 |
| 建立負載平衡規則 |$lbRule = [New-AzureRmLoadBalancerRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80<BR><BR>包含可指派公用連接埠 hello 負載平衡器上的 tooa hello 後端位址集區中的連接埠規則。 |
| 建立輸入 NAT 規則 |$inboundNATRule = [New-AzureRmLoadBalancerInboundNatRuleConfig](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) -Name "myInboundRule1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389<BR><BR>包含對應 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用連接埠規則。 |
| 建立負載平衡器 |$loadBalancer = [New-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermloadbalancer) -ResourceGroupName $myResourceGroup -Name "myLoadBalancer" -Location $location -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule -LoadBalancingRule $lbRule -BackendAddressPool $beAddressPool -Probe $healthProbe |
| 建立網路介面 |$nic1= [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/new-azurermnetworkinterface) -ResourceGroupName $myResourceGroup -Name "myNIC" -Location $location -PrivateIpAddress XX.X.X.X -Subnet $subnet2 -LoadBalancerBackendAddressPool $loadBalancer.BackendAddressPools[0] -LoadBalancerInboundNatRule $loadBalancer.InboundNatRules[0]<BR><BR>建立使用 hello 公用 IP 位址和您先前建立的虛擬網路子網路的網路介面。 |

## <a name="get-information-about-network-resources"></a>取得關於網路資源的資訊

| Task | 命令 |
| ---- | ------- |
| 列出虛擬網路 |[Get-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetwork) -ResourceGroupName $myResourceGroup<BR><BR>列出 hello 資源群組中的 hello 虛擬網路。 |
| 取得虛擬網路的相關資訊 |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup |
| 列出虛擬網路中的子網路 |Get-AzureRmVirtualNetwork -Name "myVNet" -ResourceGroupName $myResourceGroup &#124; Select Subnets |
| 取得子網路的相關資訊 |[Get-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>取得 hello 指定虛擬網路中的 hello 子網路的相關資訊。 hello $vnet 值代表 hello Get AzureRmVirtualNetwork 所傳回的物件。 |
| 列出 IP 位址 |[Get-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermpublicipaddress) -ResourceGroupName $myResourceGroup<BR><BR>列出 hello 公用 IP 位址在 hello 資源群組中。 |
| 列出負載平衡器 |[Get-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermloadbalancer) -ResourceGroupName $myResourceGroup<BR><BR>列出所有 hello 資源群組中的 hello 負載平衡器。 |
| 列出網路介面 |[Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterface) -ResourceGroupName $myResourceGroup<BR><BR>列出所有 hello 資源群組中的 hello 網路介面。 |
| 取得網路介面的相關資訊 |Get-AzureRmNetworkInterface -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>取得特定網路介面的相關資訊。 |
| 取得 hello IP 設定的網路介面 |[Get-AzureRmNetworkInterfaceIPConfig](https://docs.microsoft.com/powershell/module/azurerm.network/get-azurermnetworkinterfaceipconfig) -Name "myNICIP" -NetworkInterface $nic<BR><BR>取得 hello hello 指定的網路介面的 IP 組態的相關資訊。 hello $nic 值代表 hello Get AzureRmNetworkInterface 所傳回的物件。 |

## <a name="manage-network-resources"></a>管理網路資源

| Task | 命令 |
| ---- | ------- |
| 新增子網路 tooa 虛擬網路 |[Add-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) -AddressPrefix XX.X.X.X/XX -Name "mySubnet1" -VirtualNetwork $vnet<BR><BR>新增子網路 tooan 現有虛擬網路。 hello $vnet 值代表 hello Get AzureRmVirtualNetwork 所傳回的物件。 |
| 刪除虛擬網路 |[Remove-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermvirtualnetwork) -Name "myVNet" -ResourceGroupName $myResourceGroup<BR><BR>移除 hello 資源群組中的 hello 指定的虛擬網路。 |
| 刪除網路介面 |[Remove-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermnetworkinterface) -Name "myNIC" -ResourceGroupName $myResourceGroup<BR><BR>移除 hello 資源群組中的 hello 指定的網路介面。 |
| 刪除負載平衡器 |[Remove-AzureRmLoadBalancer](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermloadbalancer) -Name "myLoadBalancer" -ResourceGroupName $myResourceGroup<BR><BR>移除 hello 指定從 hello 資源群組的負載平衡器。 |
| 刪除公用 IP 位址 |[Remove-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/module/azurerm.network/remove-azurermpublicipaddress)-Name "myIPAddress" -ResourceGroupName $myResourceGroup<BR><BR>移除 hello 指定 hello 資源群組中的公用 IP 位址。 |

## <a name="next-steps"></a>後續步驟
* 使用您剛 hello 網路介面時，建立您[建立 VM](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 深入了解如何 [建立具有多個網路介面的 VM](../../virtual-network/virtual-networks-multiple-nics.md)。

