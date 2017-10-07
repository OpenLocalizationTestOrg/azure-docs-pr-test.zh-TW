---
title: "傳統模式中使用 aaaHow toocreate Nsg hello Azure CLI |Microsoft 文件"
description: "深入了解如何 toocreate 及使用 Azure CLI hello 的傳統模式中部署 Nsg"
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
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="42b48-103">如何 toocreate Nsg 中的 （傳統） hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="42b48-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="42b48-104">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="42b48-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="42b48-105">您也可以[hello Resource Manager 部署模型中建立 Nsg](virtual-networks-create-nsg-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="42b48-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="42b48-106">下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="42b48-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="42b48-107">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建置 hello 測試環境[建立 VNet](virtual-networks-create-vnet-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="42b48-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="42b48-108">如何 toocreate hello NSG hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="42b48-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="42b48-109">名為 NSG 名為的 toocreate **NSG 前端**根據上面的 hello 案例，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="42b48-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="42b48-110">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="42b48-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="42b48-111">執行 hello  **`azure config mode`** 命令 tooswitch tooclassic 模式，如下所示。</span><span class="sxs-lookup"><span data-stu-id="42b48-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="42b48-112">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="42b48-113">執行 hello  **`azure network nsg create`** 命令 toocreate NSG。</span><span class="sxs-lookup"><span data-stu-id="42b48-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="42b48-114">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="42b48-115">參數：</span><span class="sxs-lookup"><span data-stu-id="42b48-115">Parameters:</span></span>
   
   * <span data-ttu-id="42b48-116">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-116">**-l (or --location)**.</span></span> <span data-ttu-id="42b48-117">Hello 新的 NSG 建立所在的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="42b48-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="42b48-118">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="42b48-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="42b48-119">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-119">**-n (or --name)**.</span></span> <span data-ttu-id="42b48-120">名稱 hello 新的 NSG。</span><span class="sxs-lookup"><span data-stu-id="42b48-120">Name for hello new NSG.</span></span> <span data-ttu-id="42b48-121">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="42b48-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="42b48-122">執行 hello  **`azure network nsg rule create`** 命令 toocreate 允許從 hello 網際網路存取 tooport 3389 (RDP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="42b48-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="42b48-123">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="42b48-124">參數：</span><span class="sxs-lookup"><span data-stu-id="42b48-124">Parameters:</span></span>
   
   * <span data-ttu-id="42b48-125">**-a (或 --nsg-name)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="42b48-126">Hello NSG 中的 hello 會建立規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="42b48-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="42b48-127">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="42b48-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="42b48-128">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-128">**-n (or --name)**.</span></span> <span data-ttu-id="42b48-129">Hello 新規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="42b48-129">Name for hello new rule.</span></span> <span data-ttu-id="42b48-130">在本文案例中為 *rdp-rule*。</span><span class="sxs-lookup"><span data-stu-id="42b48-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="42b48-131">**-c (或 --action)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-131">**-c (or --action)**.</span></span> <span data-ttu-id="42b48-132">Hello 規則 （拒絕或允許） 的存取層級。</span><span class="sxs-lookup"><span data-stu-id="42b48-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="42b48-133">**-p (或 --protocol)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="42b48-134">通訊協定 (Tcp、 Udp 或 *) hello 規則。</span><span class="sxs-lookup"><span data-stu-id="42b48-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="42b48-135">**-r (或 --type)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-135">**-r (or --type)**.</span></span> <span data-ttu-id="42b48-136">連線 (輸入或輸出) 的方向。</span><span class="sxs-lookup"><span data-stu-id="42b48-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="42b48-137">**-y (或 --priority)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-137">**-y (or --priority)**.</span></span> <span data-ttu-id="42b48-138">Hello 規則的優先順序。</span><span class="sxs-lookup"><span data-stu-id="42b48-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="42b48-139">**-f (或 --source-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="42b48-140">CIDR 中的來源位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="42b48-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="42b48-141">**-o (或 --source-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="42b48-142">來源連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="42b48-142">Source port, or port range.</span></span>
   * <span data-ttu-id="42b48-143">**-e (或 --destination-address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="42b48-144">CIDR 中的目的地位址首碼或使用預設標記。</span><span class="sxs-lookup"><span data-stu-id="42b48-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="42b48-145">**-u (或 --destination-port-range)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="42b48-146">目的地連接埠，或連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="42b48-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="42b48-147">執行 hello  **`azure network nsg rule create`** 命令 toocreate 允許從 hello 網際網路存取 tooport 80 (HTTP) 的規則。</span><span class="sxs-lookup"><span data-stu-id="42b48-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="42b48-148">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="42b48-149">執行 hello  **`azure network nsg subnet add`** 命令 toolink hello NSG toohello 前端子網路。</span><span class="sxs-lookup"><span data-stu-id="42b48-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="42b48-150">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="42b48-151">Hello 回 toocreate hello NSG 如何結束子網路</span><span class="sxs-lookup"><span data-stu-id="42b48-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="42b48-152">名為 NSG 名為的 toocreate *NSG 後端*根據上面的 hello 案例，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="42b48-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="42b48-153">執行 hello  **`azure network nsg create`** 命令 toocreate NSG。</span><span class="sxs-lookup"><span data-stu-id="42b48-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="42b48-154">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
   
    <span data-ttu-id="42b48-155">參數：</span><span class="sxs-lookup"><span data-stu-id="42b48-155">Parameters:</span></span>
   
   * <span data-ttu-id="42b48-156">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-156">**-l (or --location)**.</span></span> <span data-ttu-id="42b48-157">Hello 新的 NSG 建立所在的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="42b48-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="42b48-158">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="42b48-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="42b48-159">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="42b48-159">**-n (or --name)**.</span></span> <span data-ttu-id="42b48-160">名稱 hello 新的 NSG。</span><span class="sxs-lookup"><span data-stu-id="42b48-160">Name for hello new NSG.</span></span> <span data-ttu-id="42b48-161">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="42b48-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="42b48-162">執行 hello  **`azure network nsg rule create`** 命令 toocreate 允許從 hello 前端子網路的存取 tooport 1433 (SQL) 的規則。</span><span class="sxs-lookup"><span data-stu-id="42b48-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="42b48-163">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="42b48-164">執行 hello  **`azure network nsg rule create`** 命令 toocreate 拒絕存取 toohello 網際網路的規則。</span><span class="sxs-lookup"><span data-stu-id="42b48-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="42b48-165">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="42b48-166">執行 hello  **`azure network nsg subnet add`**  toolink hello NSG toohello 回結束子網路的命令。</span><span class="sxs-lookup"><span data-stu-id="42b48-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="42b48-167">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="42b48-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

