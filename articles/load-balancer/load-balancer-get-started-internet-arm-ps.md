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
# <span data-ttu-id="5e4c0-103"><a name="get-started"></a>使用 PowerShell 在 Resource Manager 中建立網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e4c0-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="5e4c0-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="5e4c0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e4c0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="5e4c0-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e4c0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="5e4c0-107">範本</span><span class="sxs-lookup"><span data-stu-id="5e4c0-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5e4c0-108">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="5e4c0-109">您也可以[深入了解如何 toocreate 網際網路對向的負載平衡器使用 hello 傳統部署模型](load-balancer-get-started-internet-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="5e4c0-110">使用 Azure PowerShell 部署 hello 方案</span><span class="sxs-lookup"><span data-stu-id="5e4c0-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="5e4c0-111">hello 下列程序說明如何 toocreate 網際網路對向的負載平衡器使用 PowerShell 的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="5e4c0-112">使用 Azure 資源管理員中，每個資源建立個別的設定，然後放在一起 toocreate 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="5e4c0-113">您必須建立並設定下列物件 toodeploy 負載平衡器的 hello:</span><span class="sxs-lookup"><span data-stu-id="5e4c0-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="5e4c0-114">前端 IP 組態：包含傳入網路流量的公用 IP (PIP) 位址。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="5e4c0-115">後端位址集區： 包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="5e4c0-116">負載平衡規則： 包含規則，可將 hello 負載平衡器 tooa 連接埠 hello 後端位址集區中的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="5e4c0-117">輸入 NAT 規則： 包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用連接埠對應規則。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="5e4c0-118">探查： 包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="5e4c0-119">如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="5e4c0-120">設定 PowerShell toouse 資源管理員</span><span class="sxs-lookup"><span data-stu-id="5e4c0-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="5e4c0-121">請確定您的 PowerShell hello 最新實際執行版本的 hello Azure Resource Manager 模組：</span><span class="sxs-lookup"><span data-stu-id="5e4c0-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="5e4c0-122">登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="5e4c0-123">出現提示時，請輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="5e4c0-124">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="5e4c0-125">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="5e4c0-126">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-126">Create a resource group.</span></span> <span data-ttu-id="5e4c0-127">(如果您使用現有的資源群組，請略過此步驟。)</span><span class="sxs-lookup"><span data-stu-id="5e4c0-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="5e4c0-128">建立虛擬網路和 hello 前端 IP 集區的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5e4c0-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="5e4c0-129">建立子網路和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="5e4c0-130">建立 Azure 公用 IP 位址資源，名為**PublicIP**，hello DNS 名稱的前端 IP 集區所使用的 toobe **loadbalancernrp.westus.cloudapp.azure.com**。 hello 下列命令會使用 hello靜態配置類型。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="5e4c0-131">hello 負載平衡器使用 FQDN 做為前置詞的 hello 公用 IP 的 hello 網域標籤。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="5e4c0-132">這點不同於 hello 傳統部署模型，會使用 hello 雲端服務，如 hello 負載平衡器 FQDN。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="5e4c0-133">此範例中的 hello FQDN 是**loadbalancernrp.westus.cloudapp.azure.com**。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="5e4c0-134">建立前端 IP 集區與後端位址集區</span><span class="sxs-lookup"><span data-stu-id="5e4c0-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="5e4c0-135">建立名為前端的 IP 集區**LB 前端**使用 hello **PublicIp**資源。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="5e4c0-136">建立名為 **LB-backend**的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="5e4c0-137">建立 NAT 規則、負載平衡器規則、探查及負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="5e4c0-138">這個範例會建立下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5e4c0-138">This example creates hello following items:</span></span>

* <span data-ttu-id="5e4c0-139">所有的連入流量的連接埠 3441 tooport 3389 NAT 規則 tootranslate</span><span class="sxs-lookup"><span data-stu-id="5e4c0-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="5e4c0-140">所有的連入流量的連接埠 3442 tooport 3389 NAT 規則 tootranslate</span><span class="sxs-lookup"><span data-stu-id="5e4c0-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="5e4c0-141">探查規則 toocheck hello 健全狀況狀態上名為的頁面**HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="5e4c0-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="5e4c0-142">負載平衡器規則 toobalance 位址 hello 後端集區中的 hello 連接埠 80 tooport 80 上的所有傳入流量</span><span class="sxs-lookup"><span data-stu-id="5e4c0-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="5e4c0-143">使用所有上述物件的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="5e4c0-144">使用這些步驟：</span><span class="sxs-lookup"><span data-stu-id="5e4c0-144">Use these steps:</span></span>

1. <span data-ttu-id="5e4c0-145">建立 hello NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="5e4c0-146">建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-146">Create a health probe.</span></span> <span data-ttu-id="5e4c0-147">有兩種方式 tooconfigure 探查：</span><span class="sxs-lookup"><span data-stu-id="5e4c0-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="5e4c0-148">HTTP 探查</span><span class="sxs-lookup"><span data-stu-id="5e4c0-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="5e4c0-149">TCP 探查</span><span class="sxs-lookup"><span data-stu-id="5e4c0-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="5e4c0-150">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="5e4c0-151">使用先前建立的 hello 物件建立 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="5e4c0-152">建立 NIC</span><span class="sxs-lookup"><span data-stu-id="5e4c0-152">Create NICs</span></span>

<span data-ttu-id="5e4c0-153">建立網路介面 （或修改現有的），然後將其關聯 tooNAT 規則、 負載平衡器規則和探查：</span><span class="sxs-lookup"><span data-stu-id="5e4c0-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="5e4c0-154">收到 hello Nic 其中需要建立 toobe hello 虛擬網路和虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="5e4c0-155">建立名為的 NIC **lb nic1 是**，並將它與第一個 NAT 規則 hello 和 hello 第一個 （且唯一的） 後端位址集區關聯。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="5e4c0-156">建立名為的 NIC **lb nic2 是**，並將它與第二個 NAT 規則 hello 和 hello 第一個 （且唯一的） 後端位址集區關聯。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="5e4c0-157">請檢查 hello Nic。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="5e4c0-158">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="5e4c0-158">Expected output:</span></span>

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

5. <span data-ttu-id="5e4c0-159">使用 hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello Nic toodifferent Vm。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="5e4c0-160">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-160">Create a virtual machine</span></span>

<span data-ttu-id="5e4c0-161">如需建立虛擬機器和指定 NIC 的指引，請參閱[使用 PowerShell 建立 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="5e4c0-162">新增 hello 網路介面 toohello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="5e4c0-163">從 Azure 擷取 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="5e4c0-164">（如果尚未執行此動作），則您可以載入變數 hello 負載平衡器資源。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="5e4c0-165">hello 變數稱為**$lb**。使用您稍早建立的 hello 負載平衡器資源名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="5e4c0-166">載入 hello 後端組態 tooa 變數。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="5e4c0-167">載入變數中的 hello 已經建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="5e4c0-168">hello 變數名稱是**$nic**。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="5e4c0-169">hello 網路介面名稱是 hello 同一個 hello 從先前的範例。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="5e4c0-170">變更 hello hello 網路介面上的後端組態。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="5e4c0-171">儲存 hello 網路介面的物件。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="5e4c0-172">網路介面加入 toohello 負載平衡器後端集區之後，它會啟動接收 hello 該負載平衡器資源的負載平衡規則為基礎的網路流量。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="5e4c0-173">更新現有負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="5e4c0-174">使用 hello 的負載平衡器從 hello 先前範例中，指派負載平衡器物件 toohello 變數**$slb**使用`Get-AzureLoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="5e4c0-175">下列範例的 hello，在中，您可以將連入的 NAT 規則-使用連接埠 81 hello 前端集區中，連接埠 8181 hello 後端集區-tooan 現有負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="5e4c0-176">使用儲存 hello 新組態`Set-AzureLoadBalancer`。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="5e4c0-177">移除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-177">Remove a load balancer</span></span>

<span data-ttu-id="5e4c0-178">使用 hello 命令`Remove-AzureLoadBalancer`toodelete 名為先前建立的負載平衡器**NRP LB**資源群組中呼叫**NRP RG**。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="5e4c0-179">您可以使用選擇性參數的 hello **-Force** tooavoid hello 提示為刪除。</span><span class="sxs-lookup"><span data-stu-id="5e4c0-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e4c0-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e4c0-180">Next steps</span></span>

[<span data-ttu-id="5e4c0-181">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5e4c0-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="5e4c0-182">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="5e4c0-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="5e4c0-183">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="5e4c0-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
