---
title: "虛擬機器擴展集使用 aaaCreate hello Azure 入口網站 |Microsoft 文件"
description: "使用 Azure 入口網站部署擴展集。"
keywords: "虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a><span data-ttu-id="4a1ff-104">虛擬機器擴展集與 toocreate hello Azure 入口網站的方式</span><span class="sxs-lookup"><span data-stu-id="4a1ff-104">How toocreate a Virtual Machine Scale Set with hello Azure portal</span></span>
<span data-ttu-id="4a1ff-105">本教學課程會示範是多麼的輕鬆 toocreate 虛擬機器擴展集在短短幾分鐘的時間，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-105">This tutorial shows you how easy it is toocreate a Virtual Machine Scale Set in just a few minutes, by using hello Azure portal.</span></span> <span data-ttu-id="4a1ff-106">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-hello-vm-image-from-hello-marketplace"></a><span data-ttu-id="4a1ff-107">選擇 hello 商場 hello VM 映像</span><span class="sxs-lookup"><span data-stu-id="4a1ff-107">Choose hello VM image from hello marketplace</span></span>
<span data-ttu-id="4a1ff-108">從 hello 入口網站，您可以輕鬆地部署在擴展集與 CentOS、 CoreOS、 Debian、 開啟 Suse、 Red Hat Enterprise Linux、 SUSE Linux Enterprise Server、 Ubuntu Server 或 Windows Server 映像。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-108">From hello portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="4a1ff-109">首先，瀏覽 toohello [Azure 入口網站](https://portal.azure.com)網頁瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-109">First, navigate toohello [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="4a1ff-110">按一下`New`，搜尋`scale set`，然後選取 hello`Virtual machine scale set`項目：</span><span class="sxs-lookup"><span data-stu-id="4a1ff-110">Click `New`, search for `scale set`, and then select hello `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a><span data-ttu-id="4a1ff-112">建立 hello 規模集</span><span class="sxs-lookup"><span data-stu-id="4a1ff-112">Create hello scale set</span></span>
<span data-ttu-id="4a1ff-113">現在您可以使用 hello 預設設定，以及快速建立 hello 規模集。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-113">Now you can use hello default settings and quickly create hello scale set.</span></span>

* <span data-ttu-id="4a1ff-114">在 hello`Basics`刀鋒視窗中，輸入 hello 規模集的名稱。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-114">On hello `Basics` blade, enter a name for hello scale set.</span></span> <span data-ttu-id="4a1ff-115">這個名稱會成為 hello 基底的 hello hello hello 規模集前面的負載平衡器的 FQDN，因此請確定所有 Azure 跨 hello 名稱是唯一。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-115">This name becomes hello base of hello FQDN of hello load balancer in front of hello scale set, so make sure hello name is unique across all Azure.</span></span>
* <span data-ttu-id="4a1ff-116">選取所需的 OS 類型，輸入所需的使用者名稱，然後選取偏好的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="4a1ff-117">如果您選擇的密碼，必須至少為 12 個字元，且符合個 hello 四個下列複雜性需求的三種： 一個小寫字元、 一個大寫字元、 一個數字和一個特殊字元。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-117">If you choose a password, it must be at least 12 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="4a1ff-118">進一步了解 [使用者名稱和密碼需求](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="4a1ff-119">如果您選擇`SSH public key`，是確定 tooonly 貼上的公用金鑰，不是您的私用索引鍵：</span><span class="sxs-lookup"><span data-stu-id="4a1ff-119">If you choose `SSH public key`, be sure tooonly paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="4a1ff-121">選擇您想 like toolimit hello 規模調整集合 tooa 單一位置 群組，或是否就應該跨越多個位置群組。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-121">Choose whether you would like toolimit hello scale set tooa single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="4a1ff-122">允許 hello 規模調整集合 toospan 放置群組允許進行小數位數 （向上 too1 000) 的容量設定超過 100 個 Vm 有一些限制。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-122">Allowing hello scale set toospan placement groups allows for scale sets over 100 VMs in capacity (up too1,000) with certain limitations.</span></span> <span data-ttu-id="4a1ff-123">如需詳細資訊，請參閱[這份文件](./virtual-machine-scale-sets-placement-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="4a1ff-124">輸入所需的資源群組名稱及位置，然後按一下`OK`。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="4a1ff-125">在 hello`Virtual machine scale set service settings`刀鋒視窗： 輸入您想要的網域名稱標籤 (hello FQDN hello hello 規模集前面的負載平衡器中的 hello base)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-125">On hello `Virtual machine scale set service settings` blade: enter your desired domain name label (hello base of hello FQDN for hello load balancer in front of hello scale set).</span></span> <span data-ttu-id="4a1ff-126">此標籤在整個 Azure 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="4a1ff-127">選擇所需的作業系統磁碟映像、執行個體計數，以及機器大小。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="4a1ff-128">選擇您想要的磁碟類型：受管理或未受管理。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="4a1ff-129">如需詳細資訊，請參閱[這份文件](./virtual-machine-scale-sets-managed-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="4a1ff-130">如果您選擇 toohave hello 規模集橫跨多個位置群組，無法使用此選項，因為受管理的磁碟，才能執行規模集 toospan 放置群組。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-130">If you chose toohave hello scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets toospan placement groups.</span></span>
* <span data-ttu-id="4a1ff-131">啟用或停用自動調整，並於啟用的情況下進行設定：</span><span class="sxs-lookup"><span data-stu-id="4a1ff-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="4a1ff-133">在 hello`Summary`刀鋒視窗中，當驗證完成時，按一下`OK`toostart hello 小數位數設定的部署。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-133">On hello `Summary` blade, when validation is done, click `OK` toostart hello scale set deployment.</span></span>


## <a name="connect-tooa-vm-in-hello-scale-set"></a><span data-ttu-id="4a1ff-134">連接 hello 規模集中的 tooa VM</span><span class="sxs-lookup"><span data-stu-id="4a1ff-134">Connect tooa VM in hello scale set</span></span>
<span data-ttu-id="4a1ff-135">如果您選擇 toolimit 您規模調整集合 tooa 單一位置] 群組，然後 hello 規模調整集合部署了 NAT 規則設定的 toolet 連接 toohello 輕易設定的小數位數 (如果沒有，hello 規模 tooconnect toohello 虛擬機器設定，您可能需要在 toocreate在 [hello jumpbox hello 規模集的相同虛擬網路)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-135">If you chose toolimit your scale set tooa single placement group, then hello scale set is deployed with NAT rules configured toolet you connect toohello scale set easily (if not, tooconnect toohello virtual machines in hello scale set, you likely need toocreate a jumpbox in hello same virtual network as hello scale set).</span></span> <span data-ttu-id="4a1ff-136">toosee，瀏覽 toohello `Inbound NAT Rules` hello hello 擴展集的負載平衡器 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="4a1ff-136">toosee them, navigate toohello `Inbound NAT Rules` tab of hello load balancer for hello scale set:</span></span>

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="4a1ff-138">您可以連接的 tooeach hello 規模的 VM 設定使用這些 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-138">You can connect tooeach VM in hello scale set using these NAT rules.</span></span> <span data-ttu-id="4a1ff-139">比方說，Windows 擴展集，如果內送連接埠 50000，NAT 規則您無法連線透過 RDP toothat 機器上`<load-balancer-ip-address>:50000`。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect toothat machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="4a1ff-140">Linux 擴展集，您會使用連接 hello 命令`ssh -p 50000 <username>@<load-balancer-ip-address>`。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-140">For a Linux scale set, you would connect using hello command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a1ff-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4a1ff-141">Next steps</span></span>
<span data-ttu-id="4a1ff-142">如需如何 toodeploy 小數位數設定從 hello CLI 文件，請參閱[這份文件](virtual-machine-scale-sets-cli-quick-create.md)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-142">For documentation on how toodeploy scale sets from hello CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="4a1ff-143">如需從 PowerShell toodeploy 小數位數的設定方式的文件，請參閱[這份文件](virtual-machine-scale-sets-windows-create.md)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-143">For documentation on how toodeploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="4a1ff-144">如需如何 toodeploy 小數位數設定從 Visual Studio 的文件，請參閱[這份文件](virtual-machine-scale-sets-vs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-144">For documentation on how toodeploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="4a1ff-145">如需一般文件，查看 hello[規模集的文件概觀頁面](virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-145">For general documentation, check out hello [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="4a1ff-146">如需一般資訊，請參閱 hello[規模集的主要登陸頁面](https://azure.microsoft.com/services/virtual-machine-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="4a1ff-146">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

