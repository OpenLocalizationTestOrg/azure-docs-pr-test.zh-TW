---
title: "aaaCreate 網路安全性群組-Azure CLI 1.0 |Microsoft 文件"
description: "深入了解如何 toocreate 及部署使用 hello Azure CLI 1.0 的網路安全性群組。"
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
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="6ca6e-103">建立網路安全性群組，使用 Azure CLI 1.0 hello</span><span class="sxs-lookup"><span data-stu-id="6ca6e-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6ca6e-104">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="6ca6e-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="6ca6e-105">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="6ca6e-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="6ca6e-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6ca6e-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -我們的下一代 CLI hello 資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="6ca6e-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="6ca6e-108">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="6ca6e-109">您也可以[hello 傳統部署模型中建立 Nsg](virtual-networks-create-nsg-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="6ca6e-110">下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="6ca6e-111">如何 toocreate hello NSG hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="6ca6e-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="6ca6e-112">名為 NSG 名為的 toocreate *NSG 前端*根據上面的 hello 案例，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="6ca6e-113">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="6ca6e-114">執行 hello **azure 組態模式**命令 tooswitch tooResource 管理員模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="6ca6e-115">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="6ca6e-116">執行 hello **azure 網路 nsg 建立**命令 toocreate NSG。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="6ca6e-117">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="6ca6e-118">參數：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-118">Parameters:</span></span>
   
   * <span data-ttu-id="6ca6e-119">**-g (or --resource-group)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="6ca6e-120">將會建立 hello NSG hello 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="6ca6e-121">在本文案例中為 *TestRG*。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="6ca6e-122">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-122">**-l (or --location)**.</span></span> <span data-ttu-id="6ca6e-123">Hello 新的 NSG 建立所在的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="6ca6e-124">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="6ca6e-125">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-125">**-n (or --name)**.</span></span> <span data-ttu-id="6ca6e-126">名稱 hello 新的 NSG。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-126">Name for hello new NSG.</span></span> <span data-ttu-id="6ca6e-127">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="6ca6e-128">執行 hello **azure 網路 nsg 規則建立**命令 toocreate 允許從 hello 網際網路存取 tooport 3389 (RDP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="6ca6e-129">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="6ca6e-130">參數：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-130">Parameters:</span></span>
   
   * <span data-ttu-id="6ca6e-131">**-a (或 --nsg-name)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="6ca6e-132">Hello NSG 中的 hello 會建立規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="6ca6e-133">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="6ca6e-134">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-134">**-n (or --name)**.</span></span> <span data-ttu-id="6ca6e-135">Hello 新規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-135">Name for hello new rule.</span></span> <span data-ttu-id="6ca6e-136">在本文案例中為 *rdp-rule*。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="6ca6e-137">**-c (或 --access)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-137">**-c (or --access)**.</span></span> <span data-ttu-id="6ca6e-138">Hello 規則 （拒絕或允許） 的存取層級。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="6ca6e-139">**-p (或 --protocol)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="6ca6e-140">通訊協定 (Tcp、 Udp 或 *) hello 規則。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="6ca6e-141">**-r (或 --direction)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-141">**-r (or --direction)**.</span></span> <span data-ttu-id="6ca6e-142">連線 (輸入或輸出) 的方向。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="6ca6e-143">**-y (或 --priority)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-143">**-y (or --priority)**.</span></span> <span data-ttu-id="6ca6e-144">Hello 規則的優先順序。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="6ca6e-145">**-f (或 --source-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="6ca6e-146">CIDR 中的來源位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="6ca6e-147">**-o (或 --source-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="6ca6e-148">來源連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-148">Source port, or port range.</span></span>
   * <span data-ttu-id="6ca6e-149">**-e (或 --destination-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="6ca6e-150">CIDR 中的目的地位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="6ca6e-151">**-u (或 --destination-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="6ca6e-152">目的地連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="6ca6e-153">執行 hello **azure 網路 nsg 規則建立**命令 toocreate 允許從 hello 網際網路存取 tooport 80 (HTTP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="6ca6e-154">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="6ca6e-155">執行 hello **azure 網路 vnet 子網路集**命令 toolink hello NSG toohello 前端子網路。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="6ca6e-156">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="6ca6e-157">Hello 回 toocreate hello NSG 如何結束子網路</span><span class="sxs-lookup"><span data-stu-id="6ca6e-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="6ca6e-158">名為 NSG 名為的 toocreate *NSG 後端*根據上面的 hello 案例，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="6ca6e-159">執行 hello **azure 網路 nsg 建立**命令 toocreate NSG。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="6ca6e-160">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
2. <span data-ttu-id="6ca6e-161">執行 hello **azure 網路 nsg 規則建立**命令 toocreate 允許從 hello 前端子網路的存取 tooport 1433 (SQL) 的規則。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="6ca6e-162">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="6ca6e-163">執行 hello **azure 網路 nsg 規則建立**命令 toocreate 的規則，拒絕存取 toohello 網際網路從。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="6ca6e-164">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="6ca6e-165">執行 hello **azure 網路 vnet 子網路集**toolink hello NSG toohello 回結束子網路的命令。</span><span class="sxs-lookup"><span data-stu-id="6ca6e-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="6ca6e-166">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ca6e-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
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

