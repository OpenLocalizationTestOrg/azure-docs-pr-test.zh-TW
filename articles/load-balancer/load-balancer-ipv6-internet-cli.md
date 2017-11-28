---
title: "IPv6-Azure CLI aaaCreate 網際網路對向負載平衡器 |Microsoft 文件"
description: "了解如何 toocreate 網際網路對向負載平衡器 IPv6 的 Azure 資源管理員使用中的 hello Azure CLI"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="d1b82-104">建立網際網路對向 IPv6 Azure 資源管理員中使用 Azure CLI hello 的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1b82-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1b82-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1b82-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="d1b82-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d1b82-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="d1b82-107">範本</span><span class="sxs-lookup"><span data-stu-id="d1b82-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="d1b82-108">Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="d1b82-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="d1b82-109">hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="d1b82-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="d1b82-110">Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。</span><span class="sxs-lookup"><span data-stu-id="d1b82-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="d1b82-111">範例部署案例</span><span class="sxs-lookup"><span data-stu-id="d1b82-111">Example deployment scenario</span></span>

<span data-ttu-id="d1b82-112">hello 下列圖表說明 hello 負載平衡解決方案使用本文中所述的 hello 範例範本部署。</span><span class="sxs-lookup"><span data-stu-id="d1b82-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![負載平衡器案例](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="d1b82-114">在此案例中，您將建立下列 Azure 資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="d1b82-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="d1b82-115">兩部虛擬機器 (VM)</span><span class="sxs-lookup"><span data-stu-id="d1b82-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="d1b82-116">虛擬網路介面，用於每個已指派 IPv4 和 IPv6 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="d1b82-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="d1b82-117">配置有 IPv4 和 IPv6 公用 IP 位址的網際網路面向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1b82-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="d1b82-118">可用性設定組的 toothat 包含 hello 兩個 Vm</span><span class="sxs-lookup"><span data-stu-id="d1b82-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="d1b82-119">兩個負載平衡規則 toomap hello 公用 Vip toohello 私用端點</span><span class="sxs-lookup"><span data-stu-id="d1b82-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="d1b82-120">使用 Azure CLI hello hello 方案部署</span><span class="sxs-lookup"><span data-stu-id="d1b82-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="d1b82-121">下列步驟的 hello 顯示 toocreate 網際網路向負載平衡器使用 CLI 的 Azure 資源管理員的方式。</span><span class="sxs-lookup"><span data-stu-id="d1b82-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="d1b82-122">使用 Azure 資源管理員中，每個資源建立個別的設定，然後放在一起 toocreate 資源。</span><span class="sxs-lookup"><span data-stu-id="d1b82-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="d1b82-123">toodeploy 負載平衡器，建立並設定 hello 下列物件：</span><span class="sxs-lookup"><span data-stu-id="d1b82-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="d1b82-124">前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d1b82-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="d1b82-125">後端位址集區-包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。</span><span class="sxs-lookup"><span data-stu-id="d1b82-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="d1b82-126">負載平衡規則-包含對應 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="d1b82-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="d1b82-127">輸入 NAT 規則-包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用通訊埠對應規則。</span><span class="sxs-lookup"><span data-stu-id="d1b82-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="d1b82-128">探查-包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。</span><span class="sxs-lookup"><span data-stu-id="d1b82-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="d1b82-129">如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="d1b82-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="d1b82-130">設定您的 CLI 環境 toouse Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="d1b82-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="d1b82-131">針對此範例中，目前我們正在執行 PowerShell 命令視窗中的 hello CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="d1b82-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="d1b82-132">我們不使用 hello Azure PowerShell cmdlet，但我們會使用 PowerShell 的指令碼功能 tooimprove 可讀性並重複使用。</span><span class="sxs-lookup"><span data-stu-id="d1b82-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="d1b82-133">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="d1b82-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d1b82-134">執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式。</span><span class="sxs-lookup"><span data-stu-id="d1b82-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d1b82-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d1b82-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="d1b82-136">登入 tooAzure，並取得訂閱的清單。</span><span class="sxs-lookup"><span data-stu-id="d1b82-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="d1b82-137">出現提示時，請輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="d1b82-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="d1b82-138">Toouse 挑選您想要的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1b82-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="d1b82-139">請記下一個步驟的 hello hello 訂用帳戶 Id。</span><span class="sxs-lookup"><span data-stu-id="d1b82-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="d1b82-140">設定用於 hello CLI 命令的 PowerShell 變數。</span><span class="sxs-lookup"><span data-stu-id="d1b82-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="d1b82-141">建立資源群組、負載平衡器、虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="d1b82-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="d1b82-142">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d1b82-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="d1b82-143">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1b82-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="d1b82-144">建立虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="d1b82-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="d1b82-145">在此 VNet 中建立兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="d1b82-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="d1b82-146">建立 hello 前端集區的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d1b82-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="d1b82-147">Hello PowerShell 變數設定</span><span class="sxs-lookup"><span data-stu-id="d1b82-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="d1b82-148">建立公用 IP 位址 hello 前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="d1b82-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d1b82-149">hello 負載平衡器會使用 hello 公用 IP 的 hello 網域標籤做為其 FQDN。</span><span class="sxs-lookup"><span data-stu-id="d1b82-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="d1b82-150">此的傳統部署，會使用 hello 雲端服務名稱，如 hello 負載平衡器 FQDN 已變更。</span><span class="sxs-lookup"><span data-stu-id="d1b82-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="d1b82-151">此範例中的 hello FQDN 是*contoso09152016.southcentralus.cloudapp.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="d1b82-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="d1b82-152">建立前端和後端集區</span><span class="sxs-lookup"><span data-stu-id="d1b82-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="d1b82-153">這個範例會建立 hello 前端的 IP 集區收到 hello 負載平衡器上的 hello 連入網路流量和 hello 前端集區讓傳送嗨負載平衡網路流量的 hello 後端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="d1b82-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="d1b82-154">Hello PowerShell 變數設定</span><span class="sxs-lookup"><span data-stu-id="d1b82-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="d1b82-155">建立 hello hello 上一個步驟和 hello 負載平衡器中建立的公用 IP 建立關聯的前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="d1b82-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="d1b82-156">建立 hello 探查、 NAT 規則和 LB 規則</span><span class="sxs-lookup"><span data-stu-id="d1b82-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="d1b82-157">這個範例會建立下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d1b82-157">This example creates hello following items:</span></span>

* <span data-ttu-id="d1b82-158">探查規則 toocheck 連線 tooTCP 連接埠 80</span><span class="sxs-lookup"><span data-stu-id="d1b82-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="d1b82-159">NAT 規則 tootranslate 所有連入流量連接埠 3389 tooport 3389 rdp<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d1b82-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="d1b82-160">NAT 規則 tootranslate 所有連入流量連接埠 3391 tooport 3389 rdp<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d1b82-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="d1b82-161">負載平衡器規則 toobalance hello 連接埠 80 tooport 80 上的所有連入流量 hello 後端集區中的位址。</span><span class="sxs-lookup"><span data-stu-id="d1b82-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="d1b82-162"><sup>1</sup> NAT 規則是相關聯的 tooa hello 負載平衡器後方的特定虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="d1b82-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="d1b82-163">toohello 特定虛擬機器和與 hello NAT 規則相關聯的連接埠，則傳送嗨網路流量到達連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="d1b82-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="d1b82-164">您必須為 NAT 規則指定通訊協定 (UDP 或 TCP)。</span><span class="sxs-lookup"><span data-stu-id="d1b82-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="d1b82-165">這兩種通訊協定不能指定 toohello 相同連接埠。</span><span class="sxs-lookup"><span data-stu-id="d1b82-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="d1b82-166">Hello PowerShell 變數設定</span><span class="sxs-lookup"><span data-stu-id="d1b82-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="d1b82-167">建立 hello 探查</span><span class="sxs-lookup"><span data-stu-id="d1b82-167">Create hello probe</span></span>

    <span data-ttu-id="d1b82-168">hello 下列範例會建立一個 TCP 探查，檢查連線 tooback 端 TCP 通訊埠 80 每 15 秒。</span><span class="sxs-lookup"><span data-stu-id="d1b82-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="d1b82-169">它會將標記 hello 後端資源無法使用在兩個連續的失敗之後。</span><span class="sxs-lookup"><span data-stu-id="d1b82-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="d1b82-170">建立允許 RDP 連線 toohello 後端資源的輸入的 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="d1b82-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="d1b82-171">建立負載平衡器的前端收到 hello 要求根據 toodifferent 後端連接埠傳送流量的規則</span><span class="sxs-lookup"><span data-stu-id="d1b82-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="d1b82-172">檢查您的設定</span><span class="sxs-lookup"><span data-stu-id="d1b82-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="d1b82-173">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d1b82-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="d1b82-174">建立 NIC</span><span class="sxs-lookup"><span data-stu-id="d1b82-174">Create NICs</span></span>

<span data-ttu-id="d1b82-175">建立 Nic，並將其關聯 tooNAT 規則、 負載平衡器規則和探查。</span><span class="sxs-lookup"><span data-stu-id="d1b82-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="d1b82-176">Hello PowerShell 變數設定</span><span class="sxs-lookup"><span data-stu-id="d1b82-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="d1b82-177">建立的每個後端 NIC，並新增 IPv6 設定。</span><span class="sxs-lookup"><span data-stu-id="d1b82-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="d1b82-178">建立 hello 後端 VM 資源，並附加每個 NIC</span><span class="sxs-lookup"><span data-stu-id="d1b82-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="d1b82-179">toocreate Vm，您必須儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1b82-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="d1b82-180">對於負載平衡，hello Vm 需要 toobe 成員的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d1b82-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="d1b82-181">如需建立 VM 的詳細資訊，請參閱 [使用 PowerShell 建立 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d1b82-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="d1b82-182">Hello PowerShell 變數設定</span><span class="sxs-lookup"><span data-stu-id="d1b82-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="d1b82-183">此範例會使用 hello 使用者名稱和密碼以純文字的 hello vm。</span><span class="sxs-lookup"><span data-stu-id="d1b82-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="d1b82-184">清除使用認證 hello 時，務必謹慎。</span><span class="sxs-lookup"><span data-stu-id="d1b82-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="d1b82-185">處理認證在 PowerShell 中的更安全的方法，請參閱 hello [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d1b82-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="d1b82-186">建立 hello 儲存體帳戶和可用性設定組</span><span class="sxs-lookup"><span data-stu-id="d1b82-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="d1b82-187">當您建立 hello Vm 時，您可能會使用現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1b82-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="d1b82-188">hello，下列命令會建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d1b82-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="d1b82-189">接下來，建立 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="d1b82-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="d1b82-190">建立具有相關聯的 hello Nic hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d1b82-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="d1b82-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1b82-191">Next steps</span></span>

[<span data-ttu-id="d1b82-192">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d1b82-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="d1b82-193">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="d1b82-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d1b82-194">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="d1b82-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
