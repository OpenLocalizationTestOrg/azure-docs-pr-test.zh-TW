---
title: "IPv6-PowerShell 的 Azure 網際網路對向 aaaCreate 負載平衡器 |Microsoft 文件"
description: "了解如何 toocreate 面對網際網路的負載平衡器使用 IPv6 使用資源管理員的 PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a>開始使用 PowerShell 在 Resource Manager 中建立配置有 IPv6 的網際網路面向負載平衡器

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [範本](load-balancer-ipv6-internet-template.md)

Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。 hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。 Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。

## <a name="example-deployment-scenario"></a>範例部署案例

hello 下列圖表說明 hello 負載平衡解決方案部署在本文中。

![負載平衡器案例](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

在此案例中，您將建立下列 Azure 資源的 hello:

* 配置有 IPv4 和 IPv6 公用 IP 位址的網際網路面向負載平衡器
* 兩個負載平衡規則 toomap hello 公用 Vip toohello 私用端點
* 可用性設定組的 toothat 包含 hello 兩個 Vm
* 兩部虛擬機器 (VM)
* 虛擬網路介面，用於每個已指派 IPv4 和 IPv6 位址的 VM

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a>使用 Azure PowerShell hello hello 方案部署

下列步驟的 hello 顯示 toocreate 網際網路向負載平衡器使用 PowerShell 的 Azure 資源管理員的方式。 使用 Azure 資源管理員中，建立每個資源，並個別設定，然後放在一起 toocreate 資源。

toodeploy 負載平衡器，建立並設定 hello 下列物件：

* 前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。
* 後端位址集區-包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。
* 負載平衡規則-包含對應 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠的規則。
* 輸入 NAT 規則-包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用通訊埠對應規則。
* 探查-包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。

如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。

## <a name="set-up-powershell-toouse-resource-manager"></a>設定 PowerShell toouse 資源管理員

請確定您的 PowerShell hello Azure 資源管理員模組的 hello 最新實際執行版本。

1. 登入 Azure

    ```powershell
    Login-AzureRmAccount
    ```

    出現提示時，請輸入您的認證。

2. 檢查 hello 訂閱 hello 帳戶

    ```powershell
    Get-AzureRmSubscription
    ```

3. 選擇 Azure 訂用帳戶 toouse。

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. 建立資源群組 (如果是使用現有的資源群組，請略過此步驟)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>建立虛擬網路和 hello 前端 IP 集區的公用 IP 位址

1. 建立具有子網路的虛擬網路。

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. 建立 Azure 公用 IP 位址 (PIP) hello 前端 IP 位址集區的資源。

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > hello 負載平衡器會使用做為前置詞的 hello 公用 IP 的 hello 網域標籤，其 fqdn。 在此範例中，是 hello Fqdn *lbnrpipv4.westus.cloudapp.azure.com*和*lbnrpipv6.westus.cloudapp.azure.com*。

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a>建立前端 IP 組態和後端位址集區

1. 建立使用您所建立的 hello 公用 IP 位址的前端位址設定。

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. 建立後端位址集區。

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a>建立 LB 規則、NAT 規則、探查及負載平衡器

這個範例會建立下列項目 hello:

* NAT 規則 tootranslate 連接埠 443 tooport 4443 上的所有傳入流量
* 負載平衡器規則 toobalance hello 連接埠 80 tooport 80 上的所有連入流量 hello 後端集區中的位址。
* 負載平衡器規則 tooallow RDP 連線 toohello 上連接埠 3389 的 Vm。
* 探查規則 toocheck hello 健全狀況狀態上名為的頁面*HealthProbe.aspx*或連接埠 8080 上的服務
* 會使用上述所有物件的負載平衡器

1. 建立 hello NAT 規則。

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. 建立健全狀況探查。 有兩種方式 tooconfigure 探查：

    HTTP 探查

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    或 TCP 探查

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    此範例中，我們會 toouse hello TCP 探查。

3. 建立負載平衡器規則。

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. 建立 hello 負載平衡器使用 hello 先前建立的物件。

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a>建立 hello 後端 Vm Nic

1. 取得 hello 虛擬網路與虛擬網路子網路，hello Nic 需要 toobe 建立的位置。

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. 建立 hello Vm 的 IP 組態和 Nic。

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a>建立虛擬機器，並指派新建立的 Nic 的 hello

如需有關建立 VM 的詳細資訊，請參閱 [使用 Resource Manager 和 Azure PowerShell 建立及預先設定 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. 建立可用性設定組和儲存體帳戶

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. 建立每個 VM，並指派 hello 先前建立 Nic

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
