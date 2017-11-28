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
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="70539-103">使用 PowerShell 建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="70539-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="70539-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="70539-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="70539-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="70539-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="70539-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="70539-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="70539-107">範本</span><span class="sxs-lookup"><span data-stu-id="70539-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="70539-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="70539-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="70539-109">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="70539-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="70539-110">hello 下列步驟說明 toocreate 內部負載平衡器使用 PowerShell 的 Azure 資源管理員的方式。</span><span class="sxs-lookup"><span data-stu-id="70539-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="70539-111">使用 Azure 資源管理員中，hello 項目 toocreate 內部負載平衡器個別設定然後進行結合 toocreate 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="70539-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="70539-112">您需要 toocreate 並設定下列物件 toodeploy 負載平衡器的 hello:</span><span class="sxs-lookup"><span data-stu-id="70539-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="70539-113">結束 IP 組態的最上層-將設定 hello 私人 IP 位址的連入網路流量</span><span class="sxs-lookup"><span data-stu-id="70539-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="70539-114">後端位址集區-將會設定將會接收來自前端 IP 集區的 hello 負載平衡流量 hello 網路介面</span><span class="sxs-lookup"><span data-stu-id="70539-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="70539-115">負載平衡規則-來源和 hello 的本機連接埠設定負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="70539-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="70539-116">探查-設定 hello hello 虛擬機器執行個體的健全狀況狀態探查。</span><span class="sxs-lookup"><span data-stu-id="70539-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="70539-117">輸入 NAT 規則-設定 hello 連接埠規則 toodirectly 存取其中一個 hello 虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="70539-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="70539-118">您可以在 [Azure 資源管理員的負載平衡器支援](load-balancer-arm.md)中取得關於負載平衡器元件與 Azure 資源管理員的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="70539-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="70539-119">hello 下列步驟說明如何 tooconfigure 兩部虛擬機器之間的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="70539-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="70539-120">安裝 PowerShell toouse 資源管理員</span><span class="sxs-lookup"><span data-stu-id="70539-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="70539-121">請確定您擁有 hello 最新實際執行版本 hello Azure 模組的 powershell，並且正確設定 tooaccess 您 Azure 訂用帳戶的 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="70539-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="70539-122">步驟 1</span><span class="sxs-lookup"><span data-stu-id="70539-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="70539-123">步驟 2</span><span class="sxs-lookup"><span data-stu-id="70539-123">Step 2</span></span>

<span data-ttu-id="70539-124">檢查 hello 訂閱 hello 帳戶</span><span class="sxs-lookup"><span data-stu-id="70539-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="70539-125">您將會提示的 tooAuthenticate 使用您的認證。</span><span class="sxs-lookup"><span data-stu-id="70539-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="70539-126">步驟 3</span><span class="sxs-lookup"><span data-stu-id="70539-126">Step 3</span></span>

<span data-ttu-id="70539-127">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="70539-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="70539-128">建立負載平衡器的資源群組</span><span class="sxs-lookup"><span data-stu-id="70539-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="70539-129">建立新的資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="70539-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="70539-130">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="70539-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="70539-131">這當做 hello 預設位置，該資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="70539-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="70539-132">請確定所有命令的負載平衡器將會使用的 toocreate hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="70539-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="70539-133">在 hello 我們上述範例會建立資源群組，稱為 「 NRP RG 」 和 「 美國西部 」 的位置。</span><span class="sxs-lookup"><span data-stu-id="70539-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="70539-134">建立前端 IP 集區的虛擬網路和私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="70539-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="70539-135">建立 hello 虛擬網路子網路，並將指派 toovariable $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="70539-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="70539-136">建立虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="70539-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="70539-137">建立 hello 虛擬網路，並將 hello 子網路子網路是 lb toohello 虛擬網路 NRPVNet 然後指派 toovariable $vnet</span><span class="sxs-lookup"><span data-stu-id="70539-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="70539-138">建立前端 IP 集區和後端位址集區</span><span class="sxs-lookup"><span data-stu-id="70539-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="70539-139">傳入的 hello 的前端 IP 集區設定負載平衡器網路流量和後端位址集區 tooreceive hello 負載平衡流量。</span><span class="sxs-lookup"><span data-stu-id="70539-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="70539-140">步驟 1</span><span class="sxs-lookup"><span data-stu-id="70539-140">Step 1</span></span>

<span data-ttu-id="70539-141">建立用於 hello 子網路 10.0.2.0/24 會 hello 連入網路流量端點的私人 IP 位址 hello 10.0.2.5 前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="70539-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="70539-142">步驟 2</span><span class="sxs-lookup"><span data-stu-id="70539-142">Step 2</span></span>

<span data-ttu-id="70539-143">設定後端位址集區使用 tooreceive 連入流量從前端 IP 集區：</span><span class="sxs-lookup"><span data-stu-id="70539-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="70539-144">建立 LB 規則、NAT 規則、探查及負載平衡器</span><span class="sxs-lookup"><span data-stu-id="70539-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="70539-145">建立 hello 前端 IP 集區和 hello 後端位址集區之後，您需要 toocreate hello 規則所屬 toohello 負載平衡器資源：</span><span class="sxs-lookup"><span data-stu-id="70539-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="70539-146">步驟 1</span><span class="sxs-lookup"><span data-stu-id="70539-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="70539-147">上述的 hello 範例會建立下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="70539-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="70539-148">NAT 規則的所有連入流量 tooport 3441 將介紹 tooport 3389。</span><span class="sxs-lookup"><span data-stu-id="70539-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="70539-149">第二個的 NAT 規則的所有連入流量 tooport 3442 將介紹 tooport 3389。</span><span class="sxs-lookup"><span data-stu-id="70539-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="70539-150">負載平衡器規則將會載入平衡 hello 後端位址集區中公用連接埠 80 toolocal 連接埠 80 上的所有連入流量。</span><span class="sxs-lookup"><span data-stu-id="70539-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="70539-151">探查規則會檢查路徑 」 HealthProbe.aspx"hello 健全狀況狀態</span><span class="sxs-lookup"><span data-stu-id="70539-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="70539-152">步驟 2</span><span class="sxs-lookup"><span data-stu-id="70539-152">Step 2</span></span>

<span data-ttu-id="70539-153">建立 hello 負載平衡器將加在一起 （NAT 規則、 負載平衡器規則，探查設定） 的所有物件：</span><span class="sxs-lookup"><span data-stu-id="70539-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="70539-154">建立網路介面</span><span class="sxs-lookup"><span data-stu-id="70539-154">Create network interfaces</span></span>

<span data-ttu-id="70539-155">建立之後 hello 內部負載平衡器，您需要定義的網路介面接收 hello 連入負載平衡網路流量，NAT 規則和探查。</span><span class="sxs-lookup"><span data-stu-id="70539-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="70539-156">hello 網路介面在此情況下個別設定，並可以指派 tooa 虛擬機器稍後。</span><span class="sxs-lookup"><span data-stu-id="70539-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="70539-157">步驟 1</span><span class="sxs-lookup"><span data-stu-id="70539-157">Step 1</span></span>

<span data-ttu-id="70539-158">取得虛擬網路和子網路 toocreate 網路介面的 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="70539-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="70539-159">這個步驟會建立網路介面將屬於 toohello 負載平衡器後端集區，並建立第一個 NAT 規則 hello rdp 關聯此網路介面：</span><span class="sxs-lookup"><span data-stu-id="70539-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="70539-160">步驟 2</span><span class="sxs-lookup"><span data-stu-id="70539-160">Step 2</span></span>

<span data-ttu-id="70539-161">建立第二個網路介面，稱為 LB-Nic2-BE：</span><span class="sxs-lookup"><span data-stu-id="70539-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="70539-162">此步驟中建立第二個網路介面時，指派 toohello 相同負載平衡器回結束集區，並將第二個 NAT 規則 hello 建立 rdp:</span><span class="sxs-lookup"><span data-stu-id="70539-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="70539-163">hello 最終結果會顯示 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="70539-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="70539-164">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="70539-164">Expected output:</span></span>

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



### <a name="step-3"></a><span data-ttu-id="70539-165">步驟 3</span><span class="sxs-lookup"><span data-stu-id="70539-165">Step 3</span></span>

<span data-ttu-id="70539-166">使用 hello 命令新增 AzureRmVMNetworkInterface tooassign hello NIC tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="70539-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="70539-167">您可以找到 hello 逐步解說指示 toocreate 虛擬機器，並指派 tooa NIC 遵循 hello 文件：[建立使用 PowerShell 的 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="70539-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="70539-168">新增 hello 網路介面</span><span class="sxs-lookup"><span data-stu-id="70539-168">Add hello network interface</span></span>

<span data-ttu-id="70539-169">如果您已經建立的虛擬機器，您可以加入 hello 網路介面以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="70539-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="70539-170">步驟 1</span><span class="sxs-lookup"><span data-stu-id="70539-170">Step 1</span></span>

<span data-ttu-id="70539-171">（如果尚未執行此動作），則您可以載入變數 hello 負載平衡器資源。</span><span class="sxs-lookup"><span data-stu-id="70539-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="70539-172">呼叫的 $lb 而使用相同的名稱，從 hello 負載平衡器資源上面所建立的 hello hello 變數使用。</span><span class="sxs-lookup"><span data-stu-id="70539-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="70539-173">步驟 2</span><span class="sxs-lookup"><span data-stu-id="70539-173">Step 2</span></span>

<span data-ttu-id="70539-174">載入 hello 後端組態 tooa 變數。</span><span class="sxs-lookup"><span data-stu-id="70539-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="70539-175">步驟 3</span><span class="sxs-lookup"><span data-stu-id="70539-175">Step 3</span></span>

<span data-ttu-id="70539-176">載入變數中的 hello 已經建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="70539-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="70539-177">hello 使用的變數名稱是 $ nic。</span><span class="sxs-lookup"><span data-stu-id="70539-177">hello variable name used is $nic.</span></span> <span data-ttu-id="70539-178">hello 所使用的網路介面名稱是從上述的 hello 範例 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="70539-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="70539-179">步驟 4</span><span class="sxs-lookup"><span data-stu-id="70539-179">Step 4</span></span>

<span data-ttu-id="70539-180">變更 hello hello 網路介面上的後端組態。</span><span class="sxs-lookup"><span data-stu-id="70539-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="70539-181">步驟 5</span><span class="sxs-lookup"><span data-stu-id="70539-181">Step 5</span></span>

<span data-ttu-id="70539-182">儲存 hello 網路介面的物件。</span><span class="sxs-lookup"><span data-stu-id="70539-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="70539-183">網路介面加入 toohello 負載平衡器後端集區之後，它會啟動接收根據 hello 負載平衡規則，該負載平衡器資源的網路流量。</span><span class="sxs-lookup"><span data-stu-id="70539-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="70539-184">更新現有負載平衡器</span><span class="sxs-lookup"><span data-stu-id="70539-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="70539-185">步驟 1</span><span class="sxs-lookup"><span data-stu-id="70539-185">Step 1</span></span>
<span data-ttu-id="70539-186">使用從 hello 上述範例中的 hello 負載平衡器，指定負載平衡器物件 toovariable $slb 使用 Get AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="70539-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="70539-187">步驟 2</span><span class="sxs-lookup"><span data-stu-id="70539-187">Step 2</span></span>

<span data-ttu-id="70539-188">在下列範例的 hello，您將加入新的輸入 NAT 規則使用連接埠 81 在 hello 前端和連接埠 8181 hello 後的結束集區 tooan 現有負載平衡器</span><span class="sxs-lookup"><span data-stu-id="70539-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="70539-189">步驟 3</span><span class="sxs-lookup"><span data-stu-id="70539-189">Step 3</span></span>

<span data-ttu-id="70539-190">儲存使用組 AzureLoadBalancer hello 新設定</span><span class="sxs-lookup"><span data-stu-id="70539-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="70539-191">移除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="70539-191">Remove a load balancer</span></span>

<span data-ttu-id="70539-192">使用 hello 命令移除 AzureRmLoadBalancer toodelete 名為"NRP-LB 「 資源群組中稱為 「 NRP RG"先前建立的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="70539-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="70539-193">您可以使用選擇性的 hello 切換-Force tooavoid hello 提示為刪除。</span><span class="sxs-lookup"><span data-stu-id="70539-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70539-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70539-194">Next steps</span></span>

[<span data-ttu-id="70539-195">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="70539-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="70539-196">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="70539-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
