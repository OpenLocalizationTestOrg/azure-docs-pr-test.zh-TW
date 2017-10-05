---
title: "建立網際網路對向負載平衡器 - Azure CLI | Microsoft Docs"
description: "了解如何使用 Azure CLI 在資源管理員中建立網際網路面向的負載平衡器"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3b1780033cbc8aa3e108a213a4d2bfd0332fd7d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-load-balancer-using-the-azure-cli"></a><span data-ttu-id="d9da6-103">使用 Azure CLI 建立網際網路負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d9da6-103">Creating an internet load balancer using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9da6-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="d9da6-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="d9da6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9da6-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="d9da6-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d9da6-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="d9da6-107">範本</span><span class="sxs-lookup"><span data-stu-id="d9da6-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d9da6-108">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="d9da6-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="d9da6-109">您也可以 [了解如何使用傳統部署建立網際網路面向的負載平衡器](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d9da6-109">You can also [Learn how to create an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="d9da6-110">使用 Azure CLI 來部署方案</span><span class="sxs-lookup"><span data-stu-id="d9da6-110">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="d9da6-111">下列步驟說明如何搭配 CLI 使用 Azure Resource Manager，來建立網際網路對向負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="d9da6-111">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="d9da6-112">使用 Azure Resource Manager 時，會個別建立並設定每項資源，然後放在一起來建立一項資源。</span><span class="sxs-lookup"><span data-stu-id="d9da6-112">With Azure Resource Manager each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="d9da6-113">您必須建立並設定下列物件，才能部署負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="d9da6-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="d9da6-114">前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d9da6-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="d9da6-115">後端位址集區 - 包含虛擬機器的網路介面 (NIC)，可從負載平衡器接收網路流量。</span><span class="sxs-lookup"><span data-stu-id="d9da6-115">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="d9da6-116">負載平衡規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="d9da6-116">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="d9da6-117">輸入 NAT 規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中特定虛擬機器之連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="d9da6-117">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="d9da6-118">探查 - 包含用來檢查後端位址集區中虛擬機器執行個體可用性的健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="d9da6-118">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="d9da6-119">如需詳細資訊，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="d9da6-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="d9da6-120">設定 CLI 以使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d9da6-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="d9da6-121">如果您從未用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d9da6-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d9da6-122">執行 **azure config mode** 命令，以切換為 Azure 資源管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d9da6-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="d9da6-123">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d9da6-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="d9da6-124">建立前端 IP 集區的虛擬網路和公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d9da6-124">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="d9da6-125">使用名為 NRPRG 的資源群組，在美國東部位置建立名為 NRPVnet 的虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="d9da6-125">Create a virtual network (VNet) named *NRPVnet* in the East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="d9da6-126">建立名為 NRPVnetSubnet 的子網路，其中包含 NRPVnet 中 10.0.0.0/24 的 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="d9da6-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="d9da6-127">建立名為 NRPPublicIP 的公用 IP 位址，以供 DNS 名稱為 loadbalancernrp.eastus.cloudapp.azure.com 的前端 IP 集區使用。</span><span class="sxs-lookup"><span data-stu-id="d9da6-127">Create a public IP address named *NRPPublicIP* to be used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span> <span data-ttu-id="d9da6-128">下列命令使用靜態配置類型和 4 分鐘的閒置逾時。</span><span class="sxs-lookup"><span data-stu-id="d9da6-128">The command below uses the static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="d9da6-129">負載平衡器將使用公用 IP 的網域標籤作為其 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d9da6-129">The load balancer will use the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="d9da6-130">這是一項來自傳統部署的變更，該部署使用雲端服務作為負載平衡器完整網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="d9da6-130">This a change from classic deployment, which uses the cloud service as the load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="d9da6-131">在此範例中，FQDN 是 *loadbalancernrp.eastus.cloudapp.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="d9da6-131">In this example, the FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="d9da6-132">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d9da6-132">Create a load balancer</span></span>

<span data-ttu-id="d9da6-133">下列命令會在「美國東部」Azure 位置中的 NRPRG 資源群組內，建立名為 NRPlb 的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="d9da6-133">The following command creates a load balancer named *NRPlb* in the *NRPRG* resource group in the *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="d9da6-134">建立前端 IP 集區與後端位址集區</span><span class="sxs-lookup"><span data-stu-id="d9da6-134">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="d9da6-135">此範例示範如何建立前端 IP 集區來接收負載平衡器上的傳入網路流量，以及建立後端 IP 集區，供前端集區傳送已負載平衡的網路流量。</span><span class="sxs-lookup"><span data-stu-id="d9da6-135">This example demonstrates how to create the front-end IP pool that receives the incoming network traffic on the load balancer and the backend IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="d9da6-136">建立將在上個步驟中建立的公用 IP 與負載平衡器關聯的前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="d9da6-136">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="d9da6-137">設定用來從前端 IP 集區接收傳入流量的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="d9da6-137">Set up a back-end address pool used to receive incoming traffic from the front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="d9da6-138">建立 LB 規則、NAT 規則及探查</span><span class="sxs-lookup"><span data-stu-id="d9da6-138">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="d9da6-139">此範例會建立下列項目：</span><span class="sxs-lookup"><span data-stu-id="d9da6-139">This example creates the following items.</span></span>

* <span data-ttu-id="d9da6-140">一個可將連接埠 21 上的所有傳入流量轉譯至連接埠 22<sup>1</sup> 的 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="d9da6-140">a NAT rule to translate all incoming traffic on port 21 to port 22<sup>1</sup></span></span>
* <span data-ttu-id="d9da6-141">一個可將連接埠 23 上的所有傳入流量轉譯至連接埠 22 的 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="d9da6-141">a NAT rule to translate all incoming traffic on port 23 to port 22</span></span>
* <span data-ttu-id="d9da6-142">一個可將連接埠 80 上所有傳入流量負載平衡至後端集區中位址上連接埠 80 的負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="d9da6-142">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="d9da6-143">一個可在名為 *HealthProbe.aspx*的頁面上檢查健全狀態的探查規則。</span><span class="sxs-lookup"><span data-stu-id="d9da6-143">a probe rule to check the health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="d9da6-144"><sup>1</sup> NAT 規則會關聯到負載平衡器後方的特定虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="d9da6-144"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="d9da6-145">系統會將抵達連接埠 21 的網路流量會傳送給與此 NAT 規則關聯之連接埠 22 上的特定虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d9da6-145">The network traffic arriving on port 21 is sent to a specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="d9da6-146">您必須為 NAT 規則指定通訊協定 (UDP 或 TCP)。</span><span class="sxs-lookup"><span data-stu-id="d9da6-146">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="d9da6-147">無法將兩種通訊協定指派到相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="d9da6-147">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="d9da6-148">建立 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="d9da6-148">Create the NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="d9da6-149">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="d9da6-149">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="d9da6-150">建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="d9da6-150">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="d9da6-151">檢查您的設定。</span><span class="sxs-lookup"><span data-stu-id="d9da6-151">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="d9da6-152">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d9da6-152">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up the load balancer "nrplb"
        + Looking up the public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="d9da6-153">建立 NIC</span><span class="sxs-lookup"><span data-stu-id="d9da6-153">Create NICs</span></span>

<span data-ttu-id="d9da6-154">您需要建立 NIC (或修改現有的) 並將它們關聯至 NAT 規則、負載平衡器規則和探查。</span><span class="sxs-lookup"><span data-stu-id="d9da6-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="d9da6-155">建立名為 lb-nic1-be 的 NIC，並將它與 rdp1 NAT 規則及 NRPbackendpool 後端位址集區建立關聯。</span><span class="sxs-lookup"><span data-stu-id="d9da6-155">Create a NIC named *lb-nic1-be*, and associate it with the *rdp1* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="d9da6-156">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d9da6-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="d9da6-157">建立名為 lb-nic2-be 的 NIC，並將它與 rdp2 NAT 規則及 NRPbackendpool 後端位址集區建立關聯。</span><span class="sxs-lookup"><span data-stu-id="d9da6-157">Create a NIC named *lb-nic2-be*, and associate it with the *rdp2* NAT rule, and the *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="d9da6-158">建立名為 web1 的虛擬機器 (VM)，並將它與名為 lb-nic1-be 的 NIC 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="d9da6-158">Create a virtual machine (VM) named *web1*, and associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="d9da6-159">系統先建立了名為 *web1nrp* 的儲存體帳戶，再執行下方命令。</span><span class="sxs-lookup"><span data-stu-id="d9da6-159">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d9da6-160">負載平衡器中的 VM 必須在相同的可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="d9da6-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="d9da6-161">使用 `azure availset create` 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d9da6-161">Use `azure availset create` to create an availability set.</span></span>

    <span data-ttu-id="d9da6-162">輸出應該類似如下範例：</span><span class="sxs-lookup"><span data-stu-id="d9da6-162">The output should be similar to the following:</span></span>

        info:    Executing command vm create
        + Looking up the VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using the VM Size "Standard_A1"
        info:    The [OS, Data] Disk or image configuration requires storage account
        + Looking up the storage account web1nrp
        + Looking up the availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up the NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in the NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="d9da6-163">預期會顯示**此 NIC 未設有 publicIP** 訊息，因為針對負載平衡器建立的 NIC 會使用負載平衡器公用 IP 位址連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="d9da6-163">The informational message **This is a NIC without publicIP configured** is expected since the NIC created for the load balancer connecting to Internet using the load balancer public IP address.</span></span>

    <span data-ttu-id="d9da6-164">由於 lb-nic1-be NIC 會與 rdp1 NAT 規則相關聯，因此您可以使用 RDP 透過負載平衡器上的連接埠 3441 連線至 web1。</span><span class="sxs-lookup"><span data-stu-id="d9da6-164">Since the *lb-nic1-be* NIC is associated with the *rdp1* NAT rule, you can connect to *web1* using RDP through port 3441 on the load balancer.</span></span>

4. <span data-ttu-id="d9da6-165">建立名為 web2 的虛擬機器 (VM)，並將它與名為 lb-nic2-be 的 NIC 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="d9da6-165">Create a virtual machine (VM) named *web2*, and associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="d9da6-166">系統先建立了名為 *web1nrp* 的儲存體帳戶，再執行下方命令。</span><span class="sxs-lookup"><span data-stu-id="d9da6-166">A storage account called *web1nrp* was created before running the command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="d9da6-167">更新現有負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d9da6-167">Update an existing load balancer</span></span>
<span data-ttu-id="d9da6-168">您可以新增參考現有負載平衡器的規則。</span><span class="sxs-lookup"><span data-stu-id="d9da6-168">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="d9da6-169">在下一個範例中，會將新負載平衡器規則新增到現有的負載平衡器 **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="d9da6-169">In the next example, a new load balancer rule is added to an existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="d9da6-170">刪除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d9da6-170">Delete a load balancer</span></span>
<span data-ttu-id="d9da6-171">請使用下列命令來移除負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="d9da6-171">Use the following command to remove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="d9da6-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9da6-172">Next steps</span></span>
[<span data-ttu-id="d9da6-173">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d9da6-173">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="d9da6-174">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="d9da6-174">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d9da6-175">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="d9da6-175">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
