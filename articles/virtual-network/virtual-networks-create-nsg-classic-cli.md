---
title: "如何在傳統模式中使用 Azure CLI 建立 NSG | Microsoft Docs"
description: "了解如何在傳統模式中使用 Azure CLI 建立及部署 NSG"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 115a1937a4c88ba2b986a40c84b1b759ed5e03b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-nsgs-classic-in-the-azure-cli"></a><span data-ttu-id="43905-103">如何在 Azure CLI 中建立 NSG (傳統)</span><span class="sxs-lookup"><span data-stu-id="43905-103">How to create NSGs (classic) in the Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="43905-104">本文涵蓋之內容包括傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="43905-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="43905-105">您也可以 [在資源管理員部署模型中建立 NSG](virtual-networks-create-nsg-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="43905-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="43905-106">以下的範例 Azure CLI 命令是假設您已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="43905-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="43905-107">如果您想要執行如本文件中所顯示的命令，請先建置 [建立 VNet](virtual-networks-create-vnet-classic-cli.md)以建置測試環境。</span><span class="sxs-lookup"><span data-stu-id="43905-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="43905-108">如何建立前端子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="43905-108">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="43905-109">若要根據上述案例建立名為 **NSG-FrontEnd** 的 NSG，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="43905-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="43905-110">如果您從未用過 Azure CLI，請參閱 [安裝和設定 Azure CLI](../cli-install-nodejs.md) ，並依照指示進行，直到選取您的 Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="43905-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="43905-111">執行 **`azure config mode`** 命令，以切換為傳統模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="43905-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="43905-112">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="43905-113">執行 **`azure network nsg create`** 命令，以建立 NSG。</span><span class="sxs-lookup"><span data-stu-id="43905-113">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="43905-114">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="43905-115">參數：</span><span class="sxs-lookup"><span data-stu-id="43905-115">Parameters:</span></span>
   
   * <span data-ttu-id="43905-116">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="43905-116">**-l (or --location)**.</span></span> <span data-ttu-id="43905-117">將要建立新 NSG 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="43905-117">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="43905-118">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="43905-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="43905-119">**-n (或 --name)**。</span><span class="sxs-lookup"><span data-stu-id="43905-119">**-n (or --name)**.</span></span> <span data-ttu-id="43905-120">新 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="43905-120">Name for the new NSG.</span></span> <span data-ttu-id="43905-121">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="43905-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="43905-122">執行 **`azure network nsg rule create`** 命令來建立允許從網際網路存取連接埠 3389 (RDP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="43905-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="43905-123">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="43905-124">參數：</span><span class="sxs-lookup"><span data-stu-id="43905-124">Parameters:</span></span>
   
   * <span data-ttu-id="43905-125">**-a (或 --nsg-name)**。</span><span class="sxs-lookup"><span data-stu-id="43905-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="43905-126">將在其中建立規則之 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="43905-126">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="43905-127">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="43905-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="43905-128">**-n (或 --name)**。</span><span class="sxs-lookup"><span data-stu-id="43905-128">**-n (or --name)**.</span></span> <span data-ttu-id="43905-129">新規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="43905-129">Name for the new rule.</span></span> <span data-ttu-id="43905-130">在本文案例中為 *rdp-rule*。</span><span class="sxs-lookup"><span data-stu-id="43905-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="43905-131">**-c (或 --action)**。</span><span class="sxs-lookup"><span data-stu-id="43905-131">**-c (or --action)**.</span></span> <span data-ttu-id="43905-132">規則 (拒絕或允許) 的存取層級。</span><span class="sxs-lookup"><span data-stu-id="43905-132">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="43905-133">**-p (或 --protocol)**。</span><span class="sxs-lookup"><span data-stu-id="43905-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="43905-134">規則的通訊協定 (TCP、UDP 或 *)。</span><span class="sxs-lookup"><span data-stu-id="43905-134">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="43905-135">**-r (或 --type)**。</span><span class="sxs-lookup"><span data-stu-id="43905-135">**-r (or --type)**.</span></span> <span data-ttu-id="43905-136">連線 (輸入或輸出) 的方向。</span><span class="sxs-lookup"><span data-stu-id="43905-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="43905-137">**-y (或 --priority)**。</span><span class="sxs-lookup"><span data-stu-id="43905-137">**-y (or --priority)**.</span></span> <span data-ttu-id="43905-138">規則的優先順序。</span><span class="sxs-lookup"><span data-stu-id="43905-138">Priority for the rule.</span></span>
   * <span data-ttu-id="43905-139">**-f (或 --source-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="43905-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="43905-140">CIDR 中的來源位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="43905-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="43905-141">**-o (或 --source-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="43905-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="43905-142">來源連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="43905-142">Source port, or port range.</span></span>
   * <span data-ttu-id="43905-143">**-e (或 --destination-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="43905-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="43905-144">CIDR 中的目的地位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="43905-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="43905-145">**-u (或 --destination-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="43905-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="43905-146">目的地連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="43905-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="43905-147">執行 **`azure network nsg rule create`** 命令來建立允許從網際網路存取連接埠 80 (HTTP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="43905-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="43905-148">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="43905-149">執行 **`azure network nsg subnet add`** 命令來連結 NSG 與前端子網路。</span><span class="sxs-lookup"><span data-stu-id="43905-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="43905-150">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="43905-151">如何建立後端子網路的 NSG</span><span class="sxs-lookup"><span data-stu-id="43905-151">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="43905-152">若要根據上述案例建立名為 *NSG-BackEnd* 的 NSG，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="43905-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="43905-153">執行 **`azure network nsg create`** 命令，以建立 NSG。</span><span class="sxs-lookup"><span data-stu-id="43905-153">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="43905-154">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="43905-155">參數：</span><span class="sxs-lookup"><span data-stu-id="43905-155">Parameters:</span></span>
   
   * <span data-ttu-id="43905-156">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="43905-156">**-l (or --location)**.</span></span> <span data-ttu-id="43905-157">將要建立新 NSG 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="43905-157">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="43905-158">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="43905-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="43905-159">**-n (或 --name)**。</span><span class="sxs-lookup"><span data-stu-id="43905-159">**-n (or --name)**.</span></span> <span data-ttu-id="43905-160">新 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="43905-160">Name for the new NSG.</span></span> <span data-ttu-id="43905-161">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="43905-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="43905-162">執行 **`azure network nsg rule create`** 命令來建立允許從前端子網路存取連接埠 1433 (SQL) 的規則。</span><span class="sxs-lookup"><span data-stu-id="43905-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="43905-163">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="43905-164">執行 **`azure network nsg rule create`** 命令來建立拒絕存取網際網路的規則。</span><span class="sxs-lookup"><span data-stu-id="43905-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="43905-165">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="43905-166">執行 **`azure network nsg subnet add`** 命令來連結 NSG 與後端子網路。</span><span class="sxs-lookup"><span data-stu-id="43905-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="43905-167">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="43905-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-BackEndX"
        info:    Looking up the subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

