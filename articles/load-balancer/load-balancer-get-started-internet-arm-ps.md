---
title: "aaaCreate Azure 網際網路對向負載平衡器-PowerShell |Microsoft 文件"
description: "了解如何 toocreate 網際網路對向的負載平衡器資源管理員 中使用 PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started"></a>使用 PowerShell 在 Resource Manager 中建立網際網路面向的負載平衡器

> [!div class="op_single_selector"]
> * [入口網站](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

本文涵蓋 hello Resource Manager 部署模型。 您也可以[深入了解如何 toocreate 網際網路對向的負載平衡器使用 hello 傳統部署模型](load-balancer-get-started-internet-classic-cli.md)。

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a>使用 Azure PowerShell 部署 hello 方案

hello 下列程序說明如何 toocreate 網際網路對向的負載平衡器使用 PowerShell 的 Azure 資源管理員。 使用 Azure 資源管理員中，每個資源建立個別的設定，然後放在一起 toocreate 負載平衡器。

您必須建立並設定下列物件 toodeploy 負載平衡器的 hello:

* 前端 IP 組態：包含傳入網路流量的公用 IP (PIP) 位址。
* 後端位址集區： 包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。
* 負載平衡規則： 包含規則，可將 hello 負載平衡器 tooa 連接埠 hello 後端位址集區中的公用連接埠。
* 輸入 NAT 規則： 包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用連接埠對應規則。
* 探查： 包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。

如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。

## <a name="set-up-powershell-toouse-resource-manager"></a>設定 PowerShell toouse 資源管理員

請確定您的 PowerShell hello 最新實際執行版本的 hello Azure Resource Manager 模組：

1. 登入 tooAzure。

    ```powershell
    Login-AzureRmAccount
    ```

    出現提示時，請輸入您的認證。

2. 請檢查 hello hello 帳戶的訂用帳戶。

    ```powershell
    Get-AzureRmSubscription
    ```

3. 選擇 Azure 訂用帳戶 toouse。

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. 建立資源群組。 (如果您使用現有的資源群組，請略過此步驟。)

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>建立虛擬網路和 hello 前端 IP 集區的公用 IP 位址

1. 建立子網路和虛擬網路。

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. 建立 Azure 公用 IP 位址資源，名為**PublicIP**，hello DNS 名稱的前端 IP 集區所使用的 toobe **loadbalancernrp.westus.cloudapp.azure.com**。 hello 下列命令會使用 hello靜態配置類型。

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > hello 負載平衡器使用 FQDN 做為前置詞的 hello 公用 IP 的 hello 網域標籤。 這點不同於 hello 傳統部署模型，會使用 hello 雲端服務，如 hello 負載平衡器 FQDN。
   > 此範例中的 hello FQDN 是**loadbalancernrp.westus.cloudapp.azure.com**。

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a>建立前端 IP 集區與後端位址集區

1. 建立名為前端的 IP 集區**LB 前端**使用 hello **PublicIp**資源。

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. 建立名為 **LB-backend**的後端位址集區。

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a>建立 NAT 規則、負載平衡器規則、探查及負載平衡器

這個範例會建立下列項目 hello:

* 所有的連入流量的連接埠 3441 tooport 3389 NAT 規則 tootranslate
* 所有的連入流量的連接埠 3442 tooport 3389 NAT 規則 tootranslate
* 探查規則 toocheck hello 健全狀況狀態上名為的頁面**HealthProbe.aspx**
* 負載平衡器規則 toobalance 位址 hello 後端集區中的 hello 連接埠 80 tooport 80 上的所有傳入流量
* 使用所有上述物件的負載平衡器

使用這些步驟：

1. 建立 hello NAT 規則。

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. 建立健全狀況探查。 有兩種方式 tooconfigure 探查：

    HTTP 探查

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    TCP 探查

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. 建立負載平衡器規則。

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. 使用先前建立的 hello 物件建立 hello 負載平衡器。

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a>建立 NIC

建立網路介面 （或修改現有的），然後將其關聯 tooNAT 規則、 負載平衡器規則和探查：

1. 收到 hello Nic 其中需要建立 toobe hello 虛擬網路和虛擬網路子網路。

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. 建立名為的 NIC **lb nic1 是**，並將它與第一個 NAT 規則 hello 和 hello 第一個 （且唯一的） 後端位址集區關聯。

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. 建立名為的 NIC **lb nic2 是**，並將它與第二個 NAT 規則 hello 和 hello 第一個 （且唯一的） 後端位址集區關聯。

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. 請檢查 hello Nic。

        $backendnic1

    預期的輸出：

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. 使用 hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello Nic toodifferent Vm。

## <a name="create-a-virtual-machine"></a>建立虛擬機器

如需建立虛擬機器和指定 NIC 的指引，請參閱[使用 PowerShell 建立 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)。

## <a name="add-hello-network-interface-toohello-load-balancer"></a>新增 hello 網路介面 toohello 負載平衡器

1. 從 Azure 擷取 hello 負載平衡器。

    （如果尚未執行此動作），則您可以載入變數 hello 負載平衡器資源。 hello 變數稱為**$lb**。使用您稍早建立的 hello 負載平衡器資源名稱相同的 hello。

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. 載入 hello 後端組態 tooa 變數。

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. 載入變數中的 hello 已經建立網路介面。 hello 變數名稱是**$nic**。 hello 網路介面名稱是 hello 同一個 hello 從先前的範例。

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. 變更 hello hello 網路介面上的後端組態。

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. 儲存 hello 網路介面的物件。

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    網路介面加入 toohello 負載平衡器後端集區之後，它會啟動接收 hello 該負載平衡器資源的負載平衡規則為基礎的網路流量。

## <a name="update-an-existing-load-balancer"></a>更新現有負載平衡器

1. 使用 hello 的負載平衡器從 hello 先前範例中，指派負載平衡器物件 toohello 變數**$slb**使用`Get-AzureLoadBalancer`。

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. 下列範例的 hello，在中，您可以將連入的 NAT 規則-使用連接埠 81 hello 前端集區中，連接埠 8181 hello 後端集區-tooan 現有負載平衡器。

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. 使用儲存 hello 新組態`Set-AzureLoadBalancer`。

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a>移除負載平衡器

使用 hello 命令`Remove-AzureLoadBalancer`toodelete 名為先前建立的負載平衡器**NRP LB**資源群組中呼叫**NRP RG**。

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> 您可以使用選擇性參數的 hello **-Force** tooavoid hello 提示為刪除。

## <a name="next-steps"></a>後續步驟

[開始設定內部負載平衡器](load-balancer-get-started-ilb-arm-ps.md)

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
