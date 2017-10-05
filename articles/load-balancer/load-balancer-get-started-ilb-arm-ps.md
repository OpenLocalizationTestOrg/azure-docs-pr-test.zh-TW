---
title: "建立 Azure 內部負載平衡器 - PowerShell | Microsoft Docs"
description: "了解如何使用資源管理員中的 PowerShell 建立內部負載平衡器"
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
ms.openlocfilehash: 7bd31ab8f52ec5e81f6966000554be46eaa59396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="6b496-103">使用 PowerShell 建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="6b496-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b496-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6b496-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="6b496-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b496-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="6b496-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6b496-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="6b496-107">範本</span><span class="sxs-lookup"><span data-stu-id="6b496-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="6b496-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6b496-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6b496-109">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是[傳統部署模型](load-balancer-get-started-ilb-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="6b496-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="6b496-110">下列步驟說明如何搭配 PowerShell 使用 Azure Resource Manager，來建立內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="6b496-110">The following steps explain how to create an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="6b496-111">使用 Azure Resource Manager 時，會個別設定建立內部負載平衡器所需的項目，然後結合在一起以建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="6b496-111">With Azure Resource Manager, the items to create a Internal load balancer are configured individually and then combined to create a load balancer.</span></span>

<span data-ttu-id="6b496-112">您需要建立和設定下列物件以部署負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="6b496-112">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="6b496-113">前端 IP 組態 - 會設定傳入網路流量的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6b496-113">Front end IP configuration - will configure the private IP address for incoming network traffic</span></span>
* <span data-ttu-id="6b496-114">後端位址集區 - 會設定可接收來自前端 IP 集區之負載平衡流量的網路介面</span><span class="sxs-lookup"><span data-stu-id="6b496-114">Backend address pool - will configure the network interfaces which will receive the load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="6b496-115">負載平衡規則 - 負載平衡器的來源與本機連接埠組態。</span><span class="sxs-lookup"><span data-stu-id="6b496-115">Load balancing rules - source and local port configuration for the load balancer.</span></span>
* <span data-ttu-id="6b496-116">探查 - 設定虛擬機器執行個體的健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="6b496-116">Probes - configures the health status probe for the Virtual Machine instances.</span></span>
* <span data-ttu-id="6b496-117">傳入 NAT 規則 - 設定直接存取其中一個虛擬機器執行個體的連接埠規則。</span><span class="sxs-lookup"><span data-stu-id="6b496-117">Inbound NAT rules - configures the port rules to directly access one of the Virtual Machine instances.</span></span>

<span data-ttu-id="6b496-118">您可以在 [Azure 資源管理員的負載平衡器支援](load-balancer-arm.md)中取得關於負載平衡器元件與 Azure 資源管理員的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6b496-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="6b496-119">下列步驟說明如何在兩部虛擬機器之間設定負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="6b496-119">The following steps explain how to configure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-to-use-resource-manager"></a><span data-ttu-id="6b496-120">設定 PowerShell 以使用資源管理員</span><span class="sxs-lookup"><span data-stu-id="6b496-120">Setup PowerShell to use Resource Manager</span></span>

<span data-ttu-id="6b496-121">請確定您的 PowerShell 的 Azure 模組具有最新的實際執行版本，以及正確設定 PowerShell 以存取您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b496-121">Make sure you have the latest production version of the Azure module for PowerShell, and have PowerShell setup correctly to access your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-122">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6b496-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="6b496-123">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6b496-123">Step 2</span></span>

<span data-ttu-id="6b496-124">檢查帳戶的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6b496-124">Check the subscriptions for the account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="6b496-125">系統會提示使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="6b496-125">You will be prompted to Authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="6b496-126">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6b496-126">Step 3</span></span>

<span data-ttu-id="6b496-127">選擇其中一個要使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6b496-127">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="6b496-128">建立負載平衡器的資源群組</span><span class="sxs-lookup"><span data-stu-id="6b496-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="6b496-129">建立新的資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="6b496-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="6b496-130">Azure 資源管理員需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="6b496-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6b496-131">這用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="6b496-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="6b496-132">請確定所有建立負載平衡器的命令都是使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="6b496-132">Make sure all commands to create a load balancer will use the same resource group.</span></span>

<span data-ttu-id="6b496-133">在上述範例中，我們已建立名為 "NRP-RG" 的資源群組，且位置為「美國西部」。</span><span class="sxs-lookup"><span data-stu-id="6b496-133">In the example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="6b496-134">建立前端 IP 集區的虛擬網路和私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6b496-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="6b496-135">建立虛擬網路的子網路，並指派給變數 $backendSubnet</span><span class="sxs-lookup"><span data-stu-id="6b496-135">Creates a subnet for the virtual network and assigns to variable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="6b496-136">建立虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="6b496-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="6b496-137">建立虛擬網路，並將子網路 lb-subnet-be 加入至虛擬網路 NRPVNet，並指派給變數 $vnet</span><span class="sxs-lookup"><span data-stu-id="6b496-137">Creates the virtual network and adds the subnet lb-subnet-be to the virtual network NRPVNet and assigns to variable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="6b496-138">建立前端 IP 集區和後端位址集區</span><span class="sxs-lookup"><span data-stu-id="6b496-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="6b496-139">設定傳入負載平衡器網路流量的前端 IP 集區以及後端位址集區，以接收負載平衡流量。</span><span class="sxs-lookup"><span data-stu-id="6b496-139">Setting up a front end IP pool for the incoming load balancer network traffic and backend address pool to receive the load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-140">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6b496-140">Step 1</span></span>

<span data-ttu-id="6b496-141">使用私人 IP 位址 10.0.2.5 為子網路 10.0.2.0/24 建立前端 IP 集區，做為傳入網路流量端點。</span><span class="sxs-lookup"><span data-stu-id="6b496-141">Create a front end IP pool using the private IP address 10.0.2.5 for the subnet 10.0.2.0/24 which will be the incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="6b496-142">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6b496-142">Step 2</span></span>

<span data-ttu-id="6b496-143">設定用來從前端 IP 集區接收傳入流量的後端位址集區：</span><span class="sxs-lookup"><span data-stu-id="6b496-143">Set up a back end address pool used to receive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="6b496-144">建立 LB 規則、NAT 規則、探查及負載平衡器</span><span class="sxs-lookup"><span data-stu-id="6b496-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="6b496-145">建立前端 IP 集區和後端位址集區之後，您必須建立將屬於負載平衡器資源的規則：</span><span class="sxs-lookup"><span data-stu-id="6b496-145">After creating the front end IP pool and the backend address pool, you will need to create the rules which will belong to the load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-146">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6b496-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="6b496-147">上述範例會建立下列項目：</span><span class="sxs-lookup"><span data-stu-id="6b496-147">The example above is creating the following items:</span></span>

* <span data-ttu-id="6b496-148">NAT 規則，連接埠 3441 的所有傳入流量都會移至連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="6b496-148">NAT rule which all incoming traffic to port 3441 will go to port 3389.</span></span>
* <span data-ttu-id="6b496-149">第二個 NAT 規則，連接埠 3442 的所有傳入流量都會移至連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="6b496-149">a second NAT rule which all incoming traffic to port 3442 will go to port 3389.</span></span>
* <span data-ttu-id="6b496-150">負載平衡器規則，將公用連接埠 80 上的所有傳入流量，負載平衡至後端位址集區中的本機連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="6b496-150">a load balancer rule which will load balance all incoming traffic on public port 80 to local port 80 in the back end address pool.</span></span>
* <span data-ttu-id="6b496-151">探查規則，檢查路徑 "HealthProbe.aspx" 的健全狀態。</span><span class="sxs-lookup"><span data-stu-id="6b496-151">a probe rule which will check the health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="6b496-152">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6b496-152">Step 2</span></span>

<span data-ttu-id="6b496-153">建立負載平衡器，並將所有物件 (NAT 規則、負載平衡器規則、探查組態) 加在一起：</span><span class="sxs-lookup"><span data-stu-id="6b496-153">Create the load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="6b496-154">建立網路介面</span><span class="sxs-lookup"><span data-stu-id="6b496-154">Create network interfaces</span></span>

<span data-ttu-id="6b496-155">建立內部負載平衡器之後，您需要定義要由哪些網路介面接收傳入的負載平衡網路流量，以及定義 NAT 規則和探查。</span><span class="sxs-lookup"><span data-stu-id="6b496-155">After creating the internal load balancer, you need define which network interfaces will be receiving the incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="6b496-156">在此情況下需個別設定網路介面，並在稍後指派給虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6b496-156">The network interface in this case is configured individually and can be assigned to a virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-157">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6b496-157">Step 1</span></span>

<span data-ttu-id="6b496-158">取得資源的虛擬網路和子網路以建立網路介面：</span><span class="sxs-lookup"><span data-stu-id="6b496-158">Get the resource virtual network and subnet to create network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="6b496-159">此步驟會建立屬於負載平衡器後端集區的網路介面，並針對此網路介面的 RDP 與第一個 NAT 規則建立關聯：</span><span class="sxs-lookup"><span data-stu-id="6b496-159">This step creates a network interface which will belong to the load balancer back end pool and associate the first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="6b496-160">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6b496-160">Step 2</span></span>

<span data-ttu-id="6b496-161">建立第二個網路介面，稱為 LB-Nic2-BE：</span><span class="sxs-lookup"><span data-stu-id="6b496-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="6b496-162">此步驟會建立第二個網路介面，並指派給同一個負載平衡器後端集區，然後與針對 RDP 所建立的第二個 NAT 規則建立關聯：</span><span class="sxs-lookup"><span data-stu-id="6b496-162">This step creates a second network interface, assigning to the same load balancer back end pool and associating the second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="6b496-163">最終結果會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="6b496-163">The end result will show the following:</span></span>

    $backendnic1

<span data-ttu-id="6b496-164">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6b496-164">Expected output:</span></span>

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



### <a name="step-3"></a><span data-ttu-id="6b496-165">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6b496-165">Step 3</span></span>

<span data-ttu-id="6b496-166">使用 AzureRmVMNetworkInterface 命令將 NIC 指派給虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6b496-166">Use the command Add-AzureRmVMNetworkInterface to assign the NIC to a virtual Machine.</span></span>

<span data-ttu-id="6b496-167">您可以在下列文件中找到建立虛擬機器並指派給 NIC 的逐步指示︰[使用 PowerShell 建立 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6b496-167">You can find the step by step instructions to create a virtual machine and assign to a NIC following the documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface"></a><span data-ttu-id="6b496-168">加入網路介面</span><span class="sxs-lookup"><span data-stu-id="6b496-168">Add the network interface</span></span>

<span data-ttu-id="6b496-169">如果您已建立虛擬機器，您可以透過下列步驟新增網路介面：</span><span class="sxs-lookup"><span data-stu-id="6b496-169">If you already have a virtual machine created, you can add the network interface with the following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-170">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6b496-170">Step 1</span></span>

<span data-ttu-id="6b496-171">將負載平衡器資源載入到變數之中 (如果您還沒這麼做)。</span><span class="sxs-lookup"><span data-stu-id="6b496-171">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="6b496-172">所使用的變數稱為 $lb，並使用來自以上建立之負載平衡器資源的相同名稱。</span><span class="sxs-lookup"><span data-stu-id="6b496-172">The variable used is called $lb and use the same names from the load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="6b496-173">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6b496-173">Step 2</span></span>

<span data-ttu-id="6b496-174">將後端組態載入到變數之中。</span><span class="sxs-lookup"><span data-stu-id="6b496-174">Load the backend configuration to a variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="6b496-175">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6b496-175">Step 3</span></span>

<span data-ttu-id="6b496-176">將已建立的網路介面載入到變數之中。</span><span class="sxs-lookup"><span data-stu-id="6b496-176">Load the already created network interface into a variable.</span></span> <span data-ttu-id="6b496-177">所使用的變數名稱是 $nic。</span><span class="sxs-lookup"><span data-stu-id="6b496-177">the variable name used is $nic.</span></span> <span data-ttu-id="6b496-178">所使用的網路介面名稱是來自上述範例的相同名稱。</span><span class="sxs-lookup"><span data-stu-id="6b496-178">The network interface name used is the same from the example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="6b496-179">步驟 4</span><span class="sxs-lookup"><span data-stu-id="6b496-179">Step 4</span></span>

<span data-ttu-id="6b496-180">變更網路介面上的後端組態。</span><span class="sxs-lookup"><span data-stu-id="6b496-180">Change the backend configuration on the network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="6b496-181">步驟 5</span><span class="sxs-lookup"><span data-stu-id="6b496-181">Step 5</span></span>

<span data-ttu-id="6b496-182">儲存網路介面物件。</span><span class="sxs-lookup"><span data-stu-id="6b496-182">Save the network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="6b496-183">網路介面在新增至負載平衡器的後端集區後，便會開始根據該負載平衡器資源的負載平衡規則接收網路流量。</span><span class="sxs-lookup"><span data-stu-id="6b496-183">After a network interface is added to the load balancer backend pool, it starts receiving network traffic based on the load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="6b496-184">更新現有負載平衡器</span><span class="sxs-lookup"><span data-stu-id="6b496-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="6b496-185">步驟 1</span><span class="sxs-lookup"><span data-stu-id="6b496-185">Step 1</span></span>
<span data-ttu-id="6b496-186">使用上述範例中的負載平衡器，透過 Get-AzureRmLoadBalancer 將負載平衡器物件指派給變數 $slb</span><span class="sxs-lookup"><span data-stu-id="6b496-186">Using the load balancer from the example above, assign load balancer object to variable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="6b496-187">步驟 2</span><span class="sxs-lookup"><span data-stu-id="6b496-187">Step 2</span></span>

<span data-ttu-id="6b496-188">在下列範例中，您會使用前端的連接埠 81 和後端集區的連接埠 8181，將新的輸入 NAT 規則加入現有的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="6b496-188">In the following example, you will add a new Inbound NAT rule using port 81 in the front end and port 8181 for the back end pool to an existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="6b496-189">步驟 3</span><span class="sxs-lookup"><span data-stu-id="6b496-189">Step 3</span></span>

<span data-ttu-id="6b496-190">使用 Set-AzureLoadBalancer 儲存新組態</span><span class="sxs-lookup"><span data-stu-id="6b496-190">Save the new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="6b496-191">移除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="6b496-191">Remove a load balancer</span></span>

<span data-ttu-id="6b496-192">使用命令 Remove-AzureRmLoadBalancer 刪除資源群組 "NRP-RG" 中先前建立的負載平衡器 "NRP-LB"</span><span class="sxs-lookup"><span data-stu-id="6b496-192">Use the command Remove-AzureRmLoadBalancer to delete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="6b496-193">您可以使用選擇性參數 -Force 以避免出現刪除提示。</span><span class="sxs-lookup"><span data-stu-id="6b496-193">You can use the optional switch -Force to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b496-194">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b496-194">Next steps</span></span>

[<span data-ttu-id="6b496-195">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="6b496-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="6b496-196">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="6b496-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
