---
title: "aaaOpen 連接埠 tooa VM 使用 hello Azure 入口網站 |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Windows VM / hello Azure 入口網站中使用 hello 資源管理員部署模型"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="521db-103">如何 tooopen 連接埠 tooa hello Azure 入口網站的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="521db-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="521db-104">快速命令</span><span class="sxs-lookup"><span data-stu-id="521db-104">Quick commands</span></span>
<span data-ttu-id="521db-105">您也可以 [使用 Azure PowerShell 來執行這些步驟](nsg-quickstart-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="521db-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="521db-106">首先，建立您的「網路安全性群組」。</span><span class="sxs-lookup"><span data-stu-id="521db-106">First, create your Network Security Group.</span></span> <span data-ttu-id="521db-107">在 hello 入口網站中選取資源群組中，選擇 **新增**，然後搜尋並選取**網路安全性群組**:</span><span class="sxs-lookup"><span data-stu-id="521db-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![新增網路安全性群組](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="521db-109">輸入您「網路安全性群組」的名稱，選取或建立資源群組，然後選取位置。</span><span class="sxs-lookup"><span data-stu-id="521db-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="521db-110">完成後，請選取 [建立]：</span><span class="sxs-lookup"><span data-stu-id="521db-110">Select **Create** when finished:</span></span>

![建立網路安全性群組](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="521db-112">選取您的新「網路安全性群組」。</span><span class="sxs-lookup"><span data-stu-id="521db-112">Select your new Network Security Group.</span></span> <span data-ttu-id="521db-113">選取 '輸入安全性規則'，然後選取 hello**新增**按鈕 toocreate 規則：</span><span class="sxs-lookup"><span data-stu-id="521db-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![新增輸入規則](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="521db-115">選擇一般**服務**從 hello 下拉式選單，例如*HTTP*。</span><span class="sxs-lookup"><span data-stu-id="521db-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="521db-116">您也可以選取*自訂*tooprovide 特定通訊埠 toouse。</span><span class="sxs-lookup"><span data-stu-id="521db-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="521db-117">如有需要，變更 hello 優先順序或名稱。</span><span class="sxs-lookup"><span data-stu-id="521db-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="521db-118">hello 優先權會影響 hello 規則會套用的順序-hello 低 hello 數值，hello 早 hello 套用規則。</span><span class="sxs-lookup"><span data-stu-id="521db-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="521db-119">您也可以選取**進階**頂端 hello 這個畫面 tooenter 特定來源 IP 區塊或連接埠範圍，例如。</span><span class="sxs-lookup"><span data-stu-id="521db-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="521db-120">當您準備好時，選取**確定**toocreate hello 規則：</span><span class="sxs-lookup"><span data-stu-id="521db-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![建立輸入規則](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="521db-122">最後一個步驟是的 tooassociate 群組與子網路或特定的網路介面的網路安全性。</span><span class="sxs-lookup"><span data-stu-id="521db-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="521db-123">讓我們 hello 網路安全性群組關聯的子網路。</span><span class="sxs-lookup"><span data-stu-id="521db-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="521db-124">選取 [子網路]，然後選擇 [關聯]：</span><span class="sxs-lookup"><span data-stu-id="521db-124">Select **Subnets**, then choose **Associate**:</span></span>

![將網路安全性群組與子網路建立關聯](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="521db-126">選取您的虛擬網路，然後選取 hello 適當的子網路：</span><span class="sxs-lookup"><span data-stu-id="521db-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![將網路安全性群組與虛擬網路功能建立關聯](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="521db-128">您現在已建立「網路安全性群組」、已建立允許連接埠 80 上流量的輸入規則，並且已將它與子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="521db-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="521db-129">任何連接 toothat 子網路的 Vm 會連線到通訊埠 80 上。</span><span class="sxs-lookup"><span data-stu-id="521db-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="521db-130">網路安全性群組的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="521db-130">More information on Network Security Groups</span></span>
<span data-ttu-id="521db-131">這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。</span><span class="sxs-lookup"><span data-stu-id="521db-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="521db-132">網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。</span><span class="sxs-lookup"><span data-stu-id="521db-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="521db-133">您可以深入了解 [建立網路安全性群組和 ACL 規則](../../virtual-network/virtual-networks-create-nsg-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="521db-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="521db-134">針對高可用性 Web 應用程式，您應該將 VM 放在 Azure Load Balancer 後方。</span><span class="sxs-lookup"><span data-stu-id="521db-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="521db-135">hello 負載平衡器會將流量 tooVMs，以提供的流量篩選的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="521db-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="521db-136">如需詳細資訊，請參閱[如何 tooload 平衡 Linux 虛擬機器中 Azure toocreate 高可用性的應用程式](tutorial-load-balancer.md)。</span><span class="sxs-lookup"><span data-stu-id="521db-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="521db-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="521db-137">Next steps</span></span>
<span data-ttu-id="521db-138">在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="521db-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="521db-139">您可以找到有關 hello 下列文件中建立更詳細的環境：</span><span class="sxs-lookup"><span data-stu-id="521db-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="521db-140">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="521db-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="521db-141">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="521db-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)