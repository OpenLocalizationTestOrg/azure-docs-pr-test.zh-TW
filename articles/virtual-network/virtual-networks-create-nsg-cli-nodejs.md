---
title: "建立網路安全性群組 - Azure CLI 1.0 | Microsoft Docs"
description: "了解如何使用 Azure CLI 1.0 建立和部署網路安全性群組。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ca8c182651e3c9f2f1f3a85b94361755d8e638d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="3cb13-103">使用 Azure CLI 1.0 建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="3cb13-103">Create network security groups using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="3cb13-104">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="3cb13-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="3cb13-105">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="3cb13-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="3cb13-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="3cb13-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3cb13-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="3cb13-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="3cb13-108">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="3cb13-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="3cb13-109">您也可以 [在傳統部署模型中建立 NSG](virtual-networks-create-nsg-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="3cb13-109">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="3cb13-110">以下的範例 Azure CLI 命令是假設您已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="3cb13-110">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="3cb13-111">如何建立前端子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="3cb13-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="3cb13-112">若要根據上述案例建立名為 *NSG-FrontEnd* 的 NSG，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="3cb13-112">To create an NSG named named *NSG-FrontEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="3cb13-113">如果您從未使用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3cb13-113">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="3cb13-114">執行 **azure config mode** 命令，以切換為 Azure 資源管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3cb13-114">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="3cb13-115">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="3cb13-116">執行 **azure network nsg create** 命令以建立 NSG。</span><span class="sxs-lookup"><span data-stu-id="3cb13-116">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="3cb13-117">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="3cb13-118">參數：</span><span class="sxs-lookup"><span data-stu-id="3cb13-118">Parameters:</span></span>
   
   * <span data-ttu-id="3cb13-119">**-g (or --resource-group)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="3cb13-120">將會在當中建立 NSG 之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="3cb13-120">Name of the resource group where the NSG will be created.</span></span> <span data-ttu-id="3cb13-121">在本文案例中為 *TestRG*。</span><span class="sxs-lookup"><span data-stu-id="3cb13-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="3cb13-122">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-122">**-l (or --location)**.</span></span> <span data-ttu-id="3cb13-123">將要建立新 NSG 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="3cb13-123">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="3cb13-124">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="3cb13-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="3cb13-125">**-n (或 --name)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-125">**-n (or --name)**.</span></span> <span data-ttu-id="3cb13-126">新 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="3cb13-126">Name for the new NSG.</span></span> <span data-ttu-id="3cb13-127">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="3cb13-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="3cb13-128">執行 **azure network nsg rule create** 命令來建立允許從網際網路存取連接埠 3389 (RDP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="3cb13-128">Run the **azure network nsg rule create** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="3cb13-129">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up the network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="3cb13-130">參數：</span><span class="sxs-lookup"><span data-stu-id="3cb13-130">Parameters:</span></span>
   
   * <span data-ttu-id="3cb13-131">**-a (或 --nsg-name)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="3cb13-132">將在其中建立規則之 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="3cb13-132">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="3cb13-133">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="3cb13-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="3cb13-134">**-n (或 --name)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-134">**-n (or --name)**.</span></span> <span data-ttu-id="3cb13-135">新規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="3cb13-135">Name for the new rule.</span></span> <span data-ttu-id="3cb13-136">在本文案例中為 *rdp-rule*。</span><span class="sxs-lookup"><span data-stu-id="3cb13-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="3cb13-137">**-c (或 --access)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-137">**-c (or --access)**.</span></span> <span data-ttu-id="3cb13-138">規則 (拒絕或允許) 的存取層級。</span><span class="sxs-lookup"><span data-stu-id="3cb13-138">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="3cb13-139">**-p (或 --protocol)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="3cb13-140">規則的通訊協定 (TCP、UDP 或 *)。</span><span class="sxs-lookup"><span data-stu-id="3cb13-140">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="3cb13-141">**-r (或 --direction)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-141">**-r (or --direction)**.</span></span> <span data-ttu-id="3cb13-142">連線 (輸入或輸出) 的方向。</span><span class="sxs-lookup"><span data-stu-id="3cb13-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="3cb13-143">**-y (或 --priority)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-143">**-y (or --priority)**.</span></span> <span data-ttu-id="3cb13-144">規則的優先順序。</span><span class="sxs-lookup"><span data-stu-id="3cb13-144">Priority for the rule.</span></span>
   * <span data-ttu-id="3cb13-145">**-f (或 --source-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="3cb13-146">CIDR 中的來源位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="3cb13-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="3cb13-147">**-o (或 --source-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="3cb13-148">來源連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="3cb13-148">Source port, or port range.</span></span>
   * <span data-ttu-id="3cb13-149">**-e (或 --destination-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="3cb13-150">CIDR 中的目的地位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="3cb13-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="3cb13-151">**-u (或 --destination-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="3cb13-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="3cb13-152">目的地連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="3cb13-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="3cb13-153">執行 **azure network nsg rule create** 命令來建立允許從網際網路存取連接埠 80 (HTTP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="3cb13-153">Run the **azure network nsg rule create** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="3cb13-154">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="3cb13-155">執行 **azure network vnet subnet set** 命令來連結 NSG 與前端子網路。</span><span class="sxs-lookup"><span data-stu-id="3cb13-155">Run the **azure network vnet subnet set** command to link the NSG to the front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="3cb13-156">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="3cb13-157">如何建立後端子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="3cb13-157">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="3cb13-158">若要根據上述案例建立名為 *NSG-BackEnd* 的 NSG，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="3cb13-158">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="3cb13-159">執行 **azure network nsg create** 命令以建立 NSG。</span><span class="sxs-lookup"><span data-stu-id="3cb13-159">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="3cb13-160">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="3cb13-161">執行 **azure network nsg rule create** 命令來建立允許從前端子網路存取連接埠 1433 (SQL) 的規則。</span><span class="sxs-lookup"><span data-stu-id="3cb13-161">Run the **azure network nsg rule create** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="3cb13-162">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="3cb13-163">執行 **azure network nsg rule create** 命令來建立拒絕存取網際網路的規則。</span><span class="sxs-lookup"><span data-stu-id="3cb13-163">Run the **azure network nsg rule create** command to create a rule that denies access to the Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="3cb13-164">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="3cb13-165">執行 **azure network vnet subnet set** 命令來連結 NSG 與後端子網路。</span><span class="sxs-lookup"><span data-stu-id="3cb13-165">Run the **azure network vnet subnet set** command to link the NSG to the back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="3cb13-166">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="3cb13-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up the subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

