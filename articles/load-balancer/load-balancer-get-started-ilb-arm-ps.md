---
title: "aaaCreate Azure 內部負載平衡器-PowerShell |Microsoft 文件"
description: "了解 toocreate 內部負載平衡器使用 PowerShell 在資源管理員的方式"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a>使用 PowerShell 建立內部負載平衡器

> [!div class="op_single_selector"]
> * [Azure 入口網站](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [範本](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。  本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

hello 下列步驟說明 toocreate 內部負載平衡器使用 PowerShell 的 Azure 資源管理員的方式。 使用 Azure 資源管理員中，hello 項目 toocreate 內部負載平衡器個別設定然後進行結合 toocreate 負載平衡器。

您需要 toocreate 並設定下列物件 toodeploy 負載平衡器的 hello:

* 結束 IP 組態的最上層-將設定 hello 私人 IP 位址的連入網路流量
* 後端位址集區-將會設定將會接收來自前端 IP 集區的 hello 負載平衡流量 hello 網路介面
* 負載平衡規則-來源和 hello 的本機連接埠設定負載平衡器。
* 探查-設定 hello hello 虛擬機器執行個體的健全狀況狀態探查。
* 輸入 NAT 規則-設定 hello 連接埠規則 toodirectly 存取其中一個 hello 虛擬機器執行個體。

您可以在 [Azure 資源管理員的負載平衡器支援](load-balancer-arm.md)中取得關於負載平衡器元件與 Azure 資源管理員的詳細資訊。

hello 下列步驟說明如何 tooconfigure 兩部虛擬機器之間的負載平衡器。

## <a name="setup-powershell-toouse-resource-manager"></a>安裝 PowerShell toouse 資源管理員

請確定您擁有 hello 最新實際執行版本 hello Azure 模組的 powershell，並且正確設定 tooaccess 您 Azure 訂用帳戶的 PowerShell。

### <a name="step-1"></a>步驟 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>步驟 2

檢查 hello 訂閱 hello 帳戶

```powershell
Get-AzureRmSubscription
```

您將會提示的 tooAuthenticate 使用您的認證。

### <a name="step-3"></a>步驟 3

選擇 Azure 訂用帳戶 toouse。

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a>建立負載平衡器的資源群組

建立新的資源群組 (若使用現有的資源群組，請略過此步驟)。

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

Azure Resource Manager 需要所有的資源群組指定一個位置。 這當做 hello 預設位置，該資源群組中的資源。 請確定所有命令的負載平衡器將會使用的 toocreate hello 相同資源群組。

在 hello 我們上述範例會建立資源群組，稱為 「 NRP RG 」 和 「 美國西部 」 的位置。

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a>建立前端 IP 集區的虛擬網路和私人 IP 位址

建立 hello 虛擬網路子網路，並將指派 toovariable $backendSubnet

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

建立虛擬網路：

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

建立 hello 虛擬網路，並將 hello 子網路子網路是 lb toohello 虛擬網路 NRPVNet 然後指派 toovariable $vnet

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a>建立前端 IP 集區和後端位址集區

傳入的 hello 的前端 IP 集區設定負載平衡器網路流量和後端位址集區 tooreceive hello 負載平衡流量。

### <a name="step-1"></a>步驟 1

建立用於 hello 子網路 10.0.2.0/24 會 hello 連入網路流量端點的私人 IP 位址 hello 10.0.2.5 前端 IP 集區。

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a>步驟 2

設定後端位址集區使用 tooreceive 連入流量從前端 IP 集區：

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a>建立 LB 規則、NAT 規則、探查及負載平衡器

建立 hello 前端 IP 集區和 hello 後端位址集區之後，您需要 toocreate hello 規則所屬 toohello 負載平衡器資源：

### <a name="step-1"></a>步驟 1

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

上述的 hello 範例會建立下列項目 hello:

* NAT 規則的所有連入流量 tooport 3441 將介紹 tooport 3389。
* 第二個的 NAT 規則的所有連入流量 tooport 3442 將介紹 tooport 3389。
* 負載平衡器規則將會載入平衡 hello 後端位址集區中公用連接埠 80 toolocal 連接埠 80 上的所有連入流量。
* 探查規則會檢查路徑 」 HealthProbe.aspx"hello 健全狀況狀態

### <a name="step-2"></a>步驟 2

建立 hello 負載平衡器將加在一起 （NAT 規則、 負載平衡器規則，探查設定） 的所有物件：

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a>建立網路介面

建立之後 hello 內部負載平衡器，您需要定義的網路介面接收 hello 連入負載平衡網路流量，NAT 規則和探查。 hello 網路介面在此情況下個別設定，並可以指派 tooa 虛擬機器稍後。

### <a name="step-1"></a>步驟 1

取得虛擬網路和子網路 toocreate 網路介面的 hello 資源：

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

這個步驟會建立網路介面將屬於 toohello 負載平衡器後端集區，並建立第一個 NAT 規則 hello rdp 關聯此網路介面：

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a>步驟 2

建立第二個網路介面，稱為 LB-Nic2-BE：

此步驟中建立第二個網路介面時，指派 toohello 相同負載平衡器回結束集區，並將第二個 NAT 規則 hello 建立 rdp:

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

hello 最終結果會顯示 hello 下列：

    $backendnic1

預期的輸出：

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a>步驟 3

使用 hello 命令新增 AzureRmVMNetworkInterface tooassign hello NIC tooa 虛擬機器。

您可以找到 hello 逐步解說指示 toocreate 虛擬機器，並指派 tooa NIC 遵循 hello 文件：[建立使用 PowerShell 的 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)。

## <a name="add-hello-network-interface"></a>新增 hello 網路介面

如果您已經建立的虛擬機器，您可以加入 hello 網路介面以 hello 下列步驟：

### <a name="step-1"></a>步驟 1

（如果尚未執行此動作），則您可以載入變數 hello 負載平衡器資源。 呼叫的 $lb 而使用相同的名稱，從 hello 負載平衡器資源上面所建立的 hello hello 變數使用。

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a>步驟 2

載入 hello 後端組態 tooa 變數。

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a>步驟 3

載入變數中的 hello 已經建立網路介面。 hello 使用的變數名稱是 $ nic。 hello 所使用的網路介面名稱是從上述的 hello 範例 hello 相同。

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a>步驟 4

變更 hello hello 網路介面上的後端組態。

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a>步驟 5

儲存 hello 網路介面的物件。

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

網路介面加入 toohello 負載平衡器後端集區之後，它會啟動接收根據 hello 負載平衡規則，該負載平衡器資源的網路流量。

## <a name="update-an-existing-load-balancer"></a>更新現有負載平衡器

### <a name="step-1"></a>步驟 1
使用從 hello 上述範例中的 hello 負載平衡器，指定負載平衡器物件 toovariable $slb 使用 Get AzureRmLoadBalancer

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a>步驟 2

在下列範例的 hello，您將加入新的輸入 NAT 規則使用連接埠 81 在 hello 前端和連接埠 8181 hello 後的結束集區 tooan 現有負載平衡器

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a>步驟 3

儲存使用組 AzureLoadBalancer hello 新設定

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a>移除負載平衡器

使用 hello 命令移除 AzureRmLoadBalancer toodelete 名為"NRP-LB 「 資源群組中稱為 「 NRP RG"先前建立的負載平衡器

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> 您可以使用選擇性的 hello 切換-Force tooavoid hello 提示為刪除。

## <a name="next-steps"></a>後續步驟

[設定負載平衡器分配模式](load-balancer-distribution-mode.md)

[設定負載平衡器的閒置 TCP 逾時設定](load-balancer-tcp-idle-timeout.md)
