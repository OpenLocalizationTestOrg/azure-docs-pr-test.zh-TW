---
title: "建立配置有 IPv6 的網際網路對向負載平衡器 - Azure CLI | Microsoft Docs"
description: "了解如何使用 Azure CLI 在 Azure Resource Manager 中建立配置有 IPv6 的網際網路面向負載平衡器"
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="e43b9-104">使用 Azure CLI 在 Azure Resource Manager 中建立配置有 IPv6 的網際網路面向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e43b9-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e43b9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e43b9-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="e43b9-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e43b9-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="e43b9-107">範本</span><span class="sxs-lookup"><span data-stu-id="e43b9-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="e43b9-108">Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e43b9-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="e43b9-109">此負載平衡器可藉由在負載平衡器集合中，將連入流量分散於雲端服務或虛擬機器中狀況良好的服務執行個體之間，來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="e43b9-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="e43b9-110">Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。</span><span class="sxs-lookup"><span data-stu-id="e43b9-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="e43b9-111">範例部署案例</span><span class="sxs-lookup"><span data-stu-id="e43b9-111">Example deployment scenario</span></span>

<span data-ttu-id="e43b9-112">下圖說明使用本文所述範例範本部署的負載平衡解決方案。</span><span class="sxs-lookup"><span data-stu-id="e43b9-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![負載平衡器案例](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="e43b9-114">在此案例中，您將建立下列 Azure 資源：</span><span class="sxs-lookup"><span data-stu-id="e43b9-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="e43b9-115">兩部虛擬機器 (VM)</span><span class="sxs-lookup"><span data-stu-id="e43b9-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="e43b9-116">虛擬網路介面，用於每個已指派 IPv4 和 IPv6 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="e43b9-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="e43b9-117">配置有 IPv4 和 IPv6 公用 IP 位址的網際網路面向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e43b9-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="e43b9-118">包含兩個 VM 的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="e43b9-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="e43b9-119">兩個負載平衡規則，用以對應公用 VIP 至私人端點</span><span class="sxs-lookup"><span data-stu-id="e43b9-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="e43b9-120">使用 Azure CLI 來部署方案</span><span class="sxs-lookup"><span data-stu-id="e43b9-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="e43b9-121">下列步驟說明如何搭配 CLI 使用 Azure Resource Manager，來建立網際網路對向負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e43b9-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="e43b9-122">使用 Azure Resource Manager 時，會個別建立並設定每項資源，然後放在一起來建立一項資源。</span><span class="sxs-lookup"><span data-stu-id="e43b9-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="e43b9-123">若要部署負載平衡器，請建立並設定下列物件：</span><span class="sxs-lookup"><span data-stu-id="e43b9-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="e43b9-124">前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e43b9-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="e43b9-125">後端位址集區 - 包含虛擬機器的網路介面 (NIC)，可從負載平衡器接收網路流量。</span><span class="sxs-lookup"><span data-stu-id="e43b9-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="e43b9-126">負載平衡規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="e43b9-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="e43b9-127">輸入 NAT 規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中特定虛擬機器之連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="e43b9-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="e43b9-128">探查 - 包含用來檢查後端位址集區中虛擬機器執行個體可用性的健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="e43b9-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="e43b9-129">如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="e43b9-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="e43b9-130">設定 CLI 環境為使用 Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e43b9-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="e43b9-131">在此範例中，我們會在 PowerShell 命令視窗中執行 CLI 工具。</span><span class="sxs-lookup"><span data-stu-id="e43b9-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="e43b9-132">我們沒有使用 Azure PowerShell Cmdlet，但使用 PowerShell 的指令碼處理功能來改善可讀性與重複使用。</span><span class="sxs-lookup"><span data-stu-id="e43b9-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="e43b9-133">如果您從未使用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶為止。</span><span class="sxs-lookup"><span data-stu-id="e43b9-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="e43b9-134">執行 **azure config mode** 命令切換為 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="e43b9-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="e43b9-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="e43b9-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="e43b9-136">登入 Azure，並取得您的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="e43b9-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="e43b9-137">出現提示時，請輸入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="e43b9-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="e43b9-138">選出您想要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e43b9-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="e43b9-139">記下訂用帳戶識別碼在下一步驟使用。</span><span class="sxs-lookup"><span data-stu-id="e43b9-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="e43b9-140">設定 PowerShell 變數以搭配使用 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="e43b9-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="e43b9-141">建立資源群組、負載平衡器、虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="e43b9-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="e43b9-142">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="e43b9-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="e43b9-143">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e43b9-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="e43b9-144">建立虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="e43b9-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="e43b9-145">在此 VNet 中建立兩個子網路。</span><span class="sxs-lookup"><span data-stu-id="e43b9-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="e43b9-146">建立前端集區的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e43b9-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="e43b9-147">設定 PowerShell 變數</span><span class="sxs-lookup"><span data-stu-id="e43b9-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="e43b9-148">建立前端集區的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e43b9-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e43b9-149">負載平衡器會使用公用 IP 的網域標籤作為其 FQDN。</span><span class="sxs-lookup"><span data-stu-id="e43b9-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="e43b9-150">這是一項來自傳統部署的變更，該部署使用雲端服務名稱作為負載平衡器 FQDN。</span><span class="sxs-lookup"><span data-stu-id="e43b9-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="e43b9-151">在此範例中，FQDN 是 *contoso09152016.southcentralus.cloudapp.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="e43b9-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="e43b9-152">建立前端和後端集區</span><span class="sxs-lookup"><span data-stu-id="e43b9-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="e43b9-153">此範例會建立前端 IP 集區來接收負載平衡器上的傳入網路流量，以及建立後端 IP 集區，供前端集區傳送已負載平衡的網路流量。</span><span class="sxs-lookup"><span data-stu-id="e43b9-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="e43b9-154">設定 PowerShell 變數</span><span class="sxs-lookup"><span data-stu-id="e43b9-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="e43b9-155">建立將在上個步驟中建立的公用 IP 與負載平衡器關聯的前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="e43b9-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="e43b9-156">建立探查、NAT 規則和 LB 規則</span><span class="sxs-lookup"><span data-stu-id="e43b9-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="e43b9-157">此範例會建立下列項目：</span><span class="sxs-lookup"><span data-stu-id="e43b9-157">This example creates the following items:</span></span>

* <span data-ttu-id="e43b9-158">探查規則，用以檢查連到 TCP 連接埠 80 的連線</span><span class="sxs-lookup"><span data-stu-id="e43b9-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="e43b9-159">NAT 規則，用以將連接埠 3389 上的所有傳入流量轉譯為 RDP 的連接埠 3389<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e43b9-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="e43b9-160">NAT 規則，用以將連接埠 3391 上的所有傳入流量轉譯為 RDP 的連接埠 3389<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e43b9-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="e43b9-161">一個可將連接埠 80 上所有傳入流量負載平衡至後端集區中位址上連接埠 80 的負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="e43b9-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="e43b9-162"><sup>1</sup> NAT 規則會關聯到負載平衡器後方的特定虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="e43b9-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="e43b9-163">系統會將抵達連接埠 3389 的網路流量傳送給特定虛擬機器和與 NAT 規則關聯的連接埠 3389。</span><span class="sxs-lookup"><span data-stu-id="e43b9-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="e43b9-164">您必須為 NAT 規則指定通訊協定 (UDP 或 TCP)。</span><span class="sxs-lookup"><span data-stu-id="e43b9-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="e43b9-165">無法將兩種通訊協定指派到相同的連接埠。</span><span class="sxs-lookup"><span data-stu-id="e43b9-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="e43b9-166">設定 PowerShell 變數</span><span class="sxs-lookup"><span data-stu-id="e43b9-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="e43b9-167">建立探查</span><span class="sxs-lookup"><span data-stu-id="e43b9-167">Create the probe</span></span>

    <span data-ttu-id="e43b9-168">下列範例會建立 TCP 探查，它每隔 15 秒會檢查與後端 TCP 連接埠 80 的連線。</span><span class="sxs-lookup"><span data-stu-id="e43b9-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="e43b9-169">連續兩次失敗後，它會標記無法使用的後端資源。</span><span class="sxs-lookup"><span data-stu-id="e43b9-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="e43b9-170">建立輸入 NAT 規則，允許 RDP 連線到後端資源</span><span class="sxs-lookup"><span data-stu-id="e43b9-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="e43b9-171">建立負載平衡器規則，依據接收要求的前端將流量傳送到不同後端連接埠</span><span class="sxs-lookup"><span data-stu-id="e43b9-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="e43b9-172">檢查您的設定</span><span class="sxs-lookup"><span data-stu-id="e43b9-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="e43b9-173">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="e43b9-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="e43b9-174">建立 NIC</span><span class="sxs-lookup"><span data-stu-id="e43b9-174">Create NICs</span></span>

<span data-ttu-id="e43b9-175">建立 NIC，並將它們關聯至 NAT 規則、負載平衡器規則和探查。</span><span class="sxs-lookup"><span data-stu-id="e43b9-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="e43b9-176">設定 PowerShell 變數</span><span class="sxs-lookup"><span data-stu-id="e43b9-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="e43b9-177">建立的每個後端 NIC，並新增 IPv6 設定。</span><span class="sxs-lookup"><span data-stu-id="e43b9-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="e43b9-178">建立後端 VM 資源並連接每個 NIC</span><span class="sxs-lookup"><span data-stu-id="e43b9-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="e43b9-179">若要建立 VM，您必須有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e43b9-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="e43b9-180">為了負載平衡，VM 必須是可用性設定組的成員。</span><span class="sxs-lookup"><span data-stu-id="e43b9-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="e43b9-181">如需建立 VM 的詳細資訊，請參閱 [使用 PowerShell 建立 Azure VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e43b9-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="e43b9-182">設定 PowerShell 變數</span><span class="sxs-lookup"><span data-stu-id="e43b9-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="e43b9-183">此範例使用純文字的 VM 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e43b9-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="e43b9-184">使用純文字的認證時，請務必謹慎。</span><span class="sxs-lookup"><span data-stu-id="e43b9-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="e43b9-185">如需在 PowerShell 中更安全處理認證的做法，請參閱 [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e43b9-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="e43b9-186">建立儲存體帳戶杏可用性設定組</span><span class="sxs-lookup"><span data-stu-id="e43b9-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="e43b9-187">建立 VM時，可以使用現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e43b9-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="e43b9-188">下列命令會建立新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e43b9-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="e43b9-189">接下，建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="e43b9-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="e43b9-190">建立與 NIC 關聯的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e43b9-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="e43b9-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e43b9-191">Next steps</span></span>

[<span data-ttu-id="e43b9-192">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e43b9-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="e43b9-193">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="e43b9-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="e43b9-194">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="e43b9-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
