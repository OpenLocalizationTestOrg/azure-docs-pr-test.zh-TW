---
title: "aaaCreate 內部負載平衡器-Azure CLI |Microsoft 文件"
description: "了解如何使用內部負載平衡器 toocreate hello Azure CLI 資源管理員 中"
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
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="3c64f-103">使用 Azure CLI hello 建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="3c64f-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c64f-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3c64f-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="3c64f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c64f-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="3c64f-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c64f-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="3c64f-107">範本</span><span class="sxs-lookup"><span data-stu-id="3c64f-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="3c64f-108">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3c64f-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="3c64f-109">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](load-balancer-get-started-ilb-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="3c64f-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="3c64f-110">使用 Azure CLI hello 部署 hello 方案</span><span class="sxs-lookup"><span data-stu-id="3c64f-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="3c64f-111">hello 下列步驟顯示如何 toocreate 網際網路對向的負載平衡器使用 CLI 的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="3c64f-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="3c64f-112">使用 Azure 資源管理員中，每個資源建立個別的設定，然後放在一起 toocreate 資源。</span><span class="sxs-lookup"><span data-stu-id="3c64f-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="3c64f-113">您需要 toocreate 並設定下列物件 toodeploy 負載平衡器的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c64f-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="3c64f-114">**前端 IP 組態**- 包含傳入網路流量的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="3c64f-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="3c64f-115">**後端位址集區**： 包含啟用 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)</span><span class="sxs-lookup"><span data-stu-id="3c64f-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="3c64f-116">**負載平衡規則**： 包含規則，可將 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠</span><span class="sxs-lookup"><span data-stu-id="3c64f-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="3c64f-117">**輸入 NAT 規則**： 包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用連接埠對應規則</span><span class="sxs-lookup"><span data-stu-id="3c64f-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="3c64f-118">**探查**： 包含會使用的 toocheck hello 可用性 hello 後端位址集區中的虛擬機器執行個體的健全狀態探查</span><span class="sxs-lookup"><span data-stu-id="3c64f-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="3c64f-119">如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="3c64f-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="3c64f-120">設定 CLI toouse 資源管理員</span><span class="sxs-lookup"><span data-stu-id="3c64f-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="3c64f-121">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="3c64f-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="3c64f-122">請遵循 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示。</span><span class="sxs-lookup"><span data-stu-id="3c64f-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="3c64f-123">執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式下，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3c64f-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="3c64f-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3c64f-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="3c64f-125">逐步建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="3c64f-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="3c64f-126">登入 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="3c64f-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="3c64f-127">出現提示時，輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="3c64f-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="3c64f-128">變更 hello 命令工具 tooAzure Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="3c64f-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="3c64f-129">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="3c64f-129">Create a resource group</span></span>

<span data-ttu-id="3c64f-130">Azure Resource Manager 中的所有資源都會與資源群組關聯。</span><span class="sxs-lookup"><span data-stu-id="3c64f-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="3c64f-131">若尚未建立資源群組，請先建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="3c64f-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="3c64f-132">建立內部負載平衡器集</span><span class="sxs-lookup"><span data-stu-id="3c64f-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="3c64f-133">建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="3c64f-133">Create an internal load balancer</span></span>

    <span data-ttu-id="3c64f-134">在下列案例中的 hello，美東地區建立名為 nrprg 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3c64f-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="3c64f-135">內部負載平衡器，例如虛擬網路和虛擬網路子網路的所有資源都必須在 hello 相同的資源群組，並在 hello 相同區域。</span><span class="sxs-lookup"><span data-stu-id="3c64f-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="3c64f-136">建立 hello 內部負載平衡器前端的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3c64f-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="3c64f-137">您使用的 hello IP 位址必須是虛擬網路的 hello 子網路範圍內。</span><span class="sxs-lookup"><span data-stu-id="3c64f-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="3c64f-138">建立 hello 後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="3c64f-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="3c64f-139">定義前端 IP 位址和後端位址集區之後，您可以建立負載平衡器規則、輸入 NAT 規則，以及自訂的健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="3c64f-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="3c64f-140">建立 hello 內部負載平衡器負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="3c64f-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="3c64f-141">當您遵循 hello 先前的步驟時，hello 命令會建立接聽 tooport 1433 的負載平衡器規則 hello 前端，而傳送負載平衡網路流量 toohello 後端位址集區，也使用通訊埠 1433年。</span><span class="sxs-lookup"><span data-stu-id="3c64f-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="3c64f-142">建立輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="3c64f-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="3c64f-143">輸入的 NAT 規則會移 tooa 特定虛擬機器執行個體的使用的 toocreate 端點在負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3c64f-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="3c64f-144">hello 先前的步驟建立兩個遠端桌面的 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="3c64f-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="3c64f-145">建立 hello 負載平衡器的健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="3c64f-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="3c64f-146">健全狀況探查會檢查所有虛擬機器執行個體 toomake 確定他們可以傳送網路流量。</span><span class="sxs-lookup"><span data-stu-id="3c64f-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="3c64f-147">hello 失敗的探查檢查虛擬機器執行個體移除 hello 負載平衡器，直到它變成上線並探查核取判斷為狀況良好。</span><span class="sxs-lookup"><span data-stu-id="3c64f-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="3c64f-148">hello Microsoft Azure 平台會使用各種不同的系統管理情況靜態、 可公開路由傳送的 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="3c64f-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="3c64f-149">hello IP 位址是 168.63.129.16。</span><span class="sxs-lookup"><span data-stu-id="3c64f-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="3c64f-150">此 IP 位址不應該遭到任何防火牆封鎖，因為可能會造成非預期的行為。</span><span class="sxs-lookup"><span data-stu-id="3c64f-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="3c64f-151">尊重 tooAzure 內部負載平衡，此 IP 位址可供監視探查 hello 負載平衡器 toodetermine hello 健全狀況狀態從一組負載平衡中虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3c64f-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="3c64f-152">如果網路安全性小組使用的 toorestrict 內部負載平衡集內的流量 tooAzure 虛擬機器或套用的 tooa 虛擬網路子網路，請確定網路安全性規則從 168.63.129.16 加入 tooallow 流量。</span><span class="sxs-lookup"><span data-stu-id="3c64f-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="3c64f-153">建立 NIC</span><span class="sxs-lookup"><span data-stu-id="3c64f-153">Create NICs</span></span>

<span data-ttu-id="3c64f-154">您需要 toocreate Nic （或修改現有的） 並將其關聯 tooNAT 規則、 負載平衡器規則和探查。</span><span class="sxs-lookup"><span data-stu-id="3c64f-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="3c64f-155">建立名為 NIC *lb nic1 是*，然後將它產生關聯以 hello *rdp1* NAT 規則，並於 hello *beilb*後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="3c64f-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="3c64f-156">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3c64f-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
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

2. <span data-ttu-id="3c64f-157">建立名為 NIC *lb nic2 是*，然後將它產生關聯以 hello *rdp2* NAT 規則，並於 hello *beilb*後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="3c64f-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="3c64f-158">建立虛擬機器名為*DB1*，然後將它產生關聯以 hello NIC 名為*lb nic1 是*。</span><span class="sxs-lookup"><span data-stu-id="3c64f-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="3c64f-159">儲存體帳戶呼叫*web1nrp*建立 hello 下列命令執行之前：</span><span class="sxs-lookup"><span data-stu-id="3c64f-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="3c64f-160">中的負載平衡器需要 toobe 中 Vm hello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="3c64f-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="3c64f-161">使用`azure availset create`toocreate 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="3c64f-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="3c64f-162">建立名為的虛擬機器 (VM) *DB2*，然後將它產生關聯以 hello NIC 名為*lb nic2 是*。</span><span class="sxs-lookup"><span data-stu-id="3c64f-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="3c64f-163">儲存體帳戶呼叫*web1nrp*之前執行下列命令的 hello 建立。</span><span class="sxs-lookup"><span data-stu-id="3c64f-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="3c64f-164">刪除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="3c64f-164">Delete a load balancer</span></span>

<span data-ttu-id="3c64f-165">tooremove 負載平衡器，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3c64f-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="3c64f-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c64f-166">Next steps</span></span>

[<span data-ttu-id="3c64f-167">使用來源 IP 同質性設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="3c64f-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="3c64f-168">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="3c64f-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

