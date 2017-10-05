---
title: "建立內部負載平衡器 - Azure CLI | Microsoft Docs"
description: "了解如何使用 Resource Manager 的 Azure CLI 建立內部負載平衡器"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="d1f68-103">使用 Azure CLI 建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1f68-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1f68-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d1f68-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="d1f68-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1f68-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="d1f68-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d1f68-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="d1f68-107">範本</span><span class="sxs-lookup"><span data-stu-id="d1f68-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="d1f68-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d1f68-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="d1f68-109">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是[傳統部署模型](load-balancer-get-started-ilb-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="d1f68-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="d1f68-110">使用 Azure CLI 來部署解釋方案</span><span class="sxs-lookup"><span data-stu-id="d1f68-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="d1f68-111">下列步驟說明如何搭配 CLI 使用 Azure Resource Manager，來建立網際網路對向負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="d1f68-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="d1f68-112">使用 Azure Resource Manager 時，會個別建立並設定每項資源，然後放在一起來建立一項資源。</span><span class="sxs-lookup"><span data-stu-id="d1f68-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="d1f68-113">您需要建立和設定下列物件以部署負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="d1f68-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="d1f68-114">**前端 IP 組態**- 包含傳入網路流量的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d1f68-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="d1f68-115">**後端位址集區**：包含網路介面 (NIC)，可使虛擬機器從負載平衡器接收網路流量</span><span class="sxs-lookup"><span data-stu-id="d1f68-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="d1f68-116">**負載平衡規則**：包含將負載平衡器上的公用連接埠對應至後端位址集區中連接埠的規則</span><span class="sxs-lookup"><span data-stu-id="d1f68-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="d1f68-117">**輸入 NAT 規則**：包含將負載平衡器上的公用連接埠對應至後端位址集區中特定虛擬機器之連接埠的規則</span><span class="sxs-lookup"><span data-stu-id="d1f68-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="d1f68-118">**探查**- 包含用來檢查後端位址集區中虛擬機器執行個體可用性的健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="d1f68-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="d1f68-119">如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="d1f68-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="d1f68-120">設定 CLI 以使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1f68-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="d1f68-121">若您未安裝 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="d1f68-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="d1f68-122">請依照指示操作到選取 Azure 帳戶和訂用帳戶之處。</span><span class="sxs-lookup"><span data-stu-id="d1f68-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d1f68-123">執行 **azure config mode** 命令，以切換為 Resource Manager 模式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1f68-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d1f68-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d1f68-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="d1f68-125">逐步建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1f68-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="d1f68-126">登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="d1f68-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="d1f68-127">出現提示時，輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="d1f68-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="d1f68-128">將命令工具變更為 Azure Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="d1f68-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="d1f68-129">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d1f68-129">Create a resource group</span></span>

<span data-ttu-id="d1f68-130">Azure Resource Manager 中的所有資源都會與資源群組關聯。</span><span class="sxs-lookup"><span data-stu-id="d1f68-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="d1f68-131">若尚未建立資源群組，請先建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="d1f68-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="d1f68-132">建立內部負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="d1f68-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="d1f68-133">建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1f68-133">Create an internal load balancer</span></span>

    <span data-ttu-id="d1f68-134">在下列案例中，有一個名為 nrprg 的資源群組建立於美國東部區域。</span><span class="sxs-lookup"><span data-stu-id="d1f68-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="d1f68-135">內部負載平衡器的所有資源 (例如虛擬網路和虛擬網路子網路) 必須位於同一個資源群組及區域。</span><span class="sxs-lookup"><span data-stu-id="d1f68-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.</span></span>

2. <span data-ttu-id="d1f68-136">建立內部負載平衡器的前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d1f68-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="d1f68-137">使用的 IP 位址必須位於虛擬網路的子網路範圍內。</span><span class="sxs-lookup"><span data-stu-id="d1f68-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="d1f68-138">建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="d1f68-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="d1f68-139">定義前端 IP 位址和後端位址集區之後，您可以建立負載平衡器規則、輸入 NAT 規則，以及自訂的健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="d1f68-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="d1f68-140">建立內部負載平衡器的負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="d1f68-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="d1f68-141">在您依前述步驟操作之後，命令會建立負載平衡器規則，用來接聽前端集區中的連接埠 1433，以及用來將負載平衡的網路流量傳送到後端位址集區 (也是使用連接埠 1433)。</span><span class="sxs-lookup"><span data-stu-id="d1f68-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="d1f68-142">建立輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="d1f68-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="d1f68-143">輸入 NAT 規則可用來在負載平衡器中建立通往特定虛擬機器執行個體的端點。</span><span class="sxs-lookup"><span data-stu-id="d1f68-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="d1f68-144">前述步驟會建立遠端桌面的兩個 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="d1f68-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="d1f68-145">為負載平衡器建立健康情況探查。</span><span class="sxs-lookup"><span data-stu-id="d1f68-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="d1f68-146">健全狀況探查會檢查所有虛擬機器執行個體，確認它們可以傳送網路流量。</span><span class="sxs-lookup"><span data-stu-id="d1f68-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="d1f68-147">探查檢查失敗的虛擬機器執行個體會從負載平衡器上移除，直到其恢復正常運作且探查判斷其健全狀況良好為止。</span><span class="sxs-lookup"><span data-stu-id="d1f68-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="d1f68-148">Microsoft Azure 平台會對各種管理案例使用靜態、可公開路由傳送的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="d1f68-148">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="d1f68-149">IP 位址是 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="d1f68-149">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="d1f68-150">此 IP 位址不應該遭到任何防火牆封鎖，因為可能會造成非預期的行為。</span><span class="sxs-lookup"><span data-stu-id="d1f68-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="d1f68-151">採用 Azure 內部負載平衡，來自負載平衡器的監視探查會使用此 IP 位址，藉此判斷虛擬機器在負載平衡集的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="d1f68-151">With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="d1f68-152">如果網路安全性群組已用來限制傳輸至內部負載平衡集中 Azure 虛擬機器的流量，或已套用至虛擬網路子網路，請確定您已新增網路安全性規則，允許來自 168.63.129.16 的流量。</span><span class="sxs-lookup"><span data-stu-id="d1f68-152">If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="d1f68-153">建立 NIC</span><span class="sxs-lookup"><span data-stu-id="d1f68-153">Create NICs</span></span>

<span data-ttu-id="d1f68-154">您需要建立 NIC (或修改現有的) 並將它們關聯至 NAT 規則、負載平衡器規則和探查。</span><span class="sxs-lookup"><span data-stu-id="d1f68-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="d1f68-155">建立名為 lb-nic1-be 的 NIC，並將其關聯到 rdp1 NAT 規則及 beilb 後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="d1f68-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="d1f68-156">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d1f68-156">Expected output:</span></span>

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

2. <span data-ttu-id="d1f68-157">建立名為 lb-nic2-be 的 NIC，並將其關聯到 rdp2 NAT 規則及 beilb 後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="d1f68-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="d1f68-158">建立名為 DB1 的虛擬機器，並將其關聯到名為 lb-nic1-be 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="d1f68-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="d1f68-159">系統會先建立名為 *web1nrp* 的儲存體帳戶，再執行下方命令：</span><span class="sxs-lookup"><span data-stu-id="d1f68-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="d1f68-160">負載平衡器中的 VM 必須在相同的可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="d1f68-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="d1f68-161">使用 `azure availset create` 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d1f68-161">Use `azure availset create` to create an availability set.</span></span>

4. <span data-ttu-id="d1f68-162">建立名為 DB2 的虛擬機器 (VM)，並將其關聯到名為 lb-nic2-be 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="d1f68-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="d1f68-163">系統會先建立名為 *web1nrp* 的儲存體帳戶，再執行下方命令。</span><span class="sxs-lookup"><span data-stu-id="d1f68-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="d1f68-164">刪除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1f68-164">Delete a load balancer</span></span>

<span data-ttu-id="d1f68-165">若要移除負載平衡器，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1f68-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="d1f68-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1f68-166">Next steps</span></span>

[<span data-ttu-id="d1f68-167">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="d1f68-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d1f68-168">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="d1f68-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

