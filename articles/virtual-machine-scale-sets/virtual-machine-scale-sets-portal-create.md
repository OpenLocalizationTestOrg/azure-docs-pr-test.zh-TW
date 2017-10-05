---
title: "使用 Azure 入口網站建立虛擬機器擴展集 | Microsoft Docs"
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
ms.openlocfilehash: 7157a429829974b45dad29ac53fb5fb46c71f821
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-the-azure-portal"></a><span data-ttu-id="4ca31-104">如何使用 Azure 入口網站建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="4ca31-104">How to create a Virtual Machine Scale Set with the Azure portal</span></span>
<span data-ttu-id="4ca31-105">本教學課程示範使用 Azure 入口網站建虛擬機器擴展集有多麼容易，只需數分鐘。</span><span class="sxs-lookup"><span data-stu-id="4ca31-105">This tutorial shows you how easy it is to create a Virtual Machine Scale Set in just a few minutes, by using the Azure portal.</span></span> <span data-ttu-id="4ca31-106">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="4ca31-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-the-vm-image-from-the-marketplace"></a><span data-ttu-id="4ca31-107">從 Marketplace 選擇 VM 映像</span><span class="sxs-lookup"><span data-stu-id="4ca31-107">Choose the VM image from the marketplace</span></span>
<span data-ttu-id="4ca31-108">您可以輕易地從入口網站使用 CentOS、CoreOS、Debian、Open Suse、Red Hat Enterprise Linux、SUSE Linux Enterprise Server、Ubuntu Server 或 Windows Server 映像部署擴展集。</span><span class="sxs-lookup"><span data-stu-id="4ca31-108">From the portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="4ca31-109">首先，在網頁瀏覽器中導覽至 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="4ca31-109">First, navigate to the [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="4ca31-110">按一下 [`New`]，搜尋 `scale set`，然後選取 [`Virtual machine scale set`] 項目：</span><span class="sxs-lookup"><span data-stu-id="4ca31-110">Click `New`, search for `scale set`, and then select the `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-the-scale-set"></a><span data-ttu-id="4ca31-112">建立擴展集</span><span class="sxs-lookup"><span data-stu-id="4ca31-112">Create the scale set</span></span>
<span data-ttu-id="4ca31-113">現在您可以使用預設設定並快速建立擴展集。</span><span class="sxs-lookup"><span data-stu-id="4ca31-113">Now you can use the default settings and quickly create the scale set.</span></span>

* <span data-ttu-id="4ca31-114">在 [ `Basics` ] 刀鋒視窗上，為擴展集輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="4ca31-114">On the `Basics` blade, enter a name for the scale set.</span></span> <span data-ttu-id="4ca31-115">此名稱會成為擴展集前方負載平衡器 FQDN 的基底，因此請確保該名稱在整個 Azure 中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4ca31-115">This name becomes the base of the FQDN of the load balancer in front of the scale set, so make sure the name is unique across all Azure.</span></span>
* <span data-ttu-id="4ca31-116">選取所需的 OS 類型，輸入所需的使用者名稱，然後選取偏好的驗證類型。</span><span class="sxs-lookup"><span data-stu-id="4ca31-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="4ca31-117">如果您選擇密碼，它的長度必須至少為 12 個字元，且符合下列四個複雜性需求的其中三項：1 個小寫字元、1 個大寫字元、1 個數字和 1 個特殊字元。</span><span class="sxs-lookup"><span data-stu-id="4ca31-117">If you choose a password, it must be at least 12 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="4ca31-118">進一步了解 [使用者名稱和密碼需求](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="4ca31-119">如果您選擇 `SSH public key`，請務必只貼上公開金鑰，而不要貼上您的私密金鑰：</span><span class="sxs-lookup"><span data-stu-id="4ca31-119">If you choose `SSH public key`, be sure to only paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="4ca31-121">選擇是要將擴展集限制在單一放置群組，還是讓它跨多個放置群組。</span><span class="sxs-lookup"><span data-stu-id="4ca31-121">Choose whether you would like to limit the scale set to a single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="4ca31-122">允許擴展集跨放置群組即可允許擴展集的容量超過 100 個 (上限為 1,000 個) VM，但有一些限制。</span><span class="sxs-lookup"><span data-stu-id="4ca31-122">Allowing the scale set to span placement groups allows for scale sets over 100 VMs in capacity (up to 1,000) with certain limitations.</span></span> <span data-ttu-id="4ca31-123">如需詳細資訊，請參閱[這份文件](./virtual-machine-scale-sets-placement-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="4ca31-124">輸入所需的資源群組名稱及位置，然後按一下 [`OK`]。</span><span class="sxs-lookup"><span data-stu-id="4ca31-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="4ca31-125">在 [ `Virtual machine scale set service settings` ] 刀鋒視窗上，輸入所需的網域名稱標籤 (擴展集前方負載平衡器 FQDN 的基底)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-125">On the `Virtual machine scale set service settings` blade: enter your desired domain name label (the base of the FQDN for the load balancer in front of the scale set).</span></span> <span data-ttu-id="4ca31-126">此標籤在整個 Azure 中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="4ca31-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="4ca31-127">選擇所需的作業系統磁碟映像、執行個體計數，以及機器大小。</span><span class="sxs-lookup"><span data-stu-id="4ca31-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="4ca31-128">選擇您想要的磁碟類型：受管理或未受管理。</span><span class="sxs-lookup"><span data-stu-id="4ca31-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="4ca31-129">如需詳細資訊，請參閱[這份文件](./virtual-machine-scale-sets-managed-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="4ca31-130">如果您選擇讓擴展集跨多個放置群組，將無法使用此選項，因為必須使用受管理磁碟，擴展集才能跨放置群組。</span><span class="sxs-lookup"><span data-stu-id="4ca31-130">If you chose to have the scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets to span placement groups.</span></span>
* <span data-ttu-id="4ca31-131">啟用或停用自動調整，並於啟用的情況下進行設定：</span><span class="sxs-lookup"><span data-stu-id="4ca31-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="4ca31-133">在 [`Summary`] 刀鋒視窗上，按一下 [`OK`] 以開始部署擴展集。</span><span class="sxs-lookup"><span data-stu-id="4ca31-133">On the `Summary` blade, when validation is done, click `OK` to start the scale set deployment.</span></span>


## <a name="connect-to-a-vm-in-the-scale-set"></a><span data-ttu-id="4ca31-134">連線到擴展集中的 VM</span><span class="sxs-lookup"><span data-stu-id="4ca31-134">Connect to a VM in the scale set</span></span>
<span data-ttu-id="4ca31-135">如果您選擇將擴展集限制在單一放置群組，則在部署擴展集時會設定好可讓您輕鬆連接到擴展集的 NAT 規則 (否則，若要連接到擴展集中的虛擬機器，您可能需要在與該擴展集相同的虛擬網路中建立跳轉盒 (Jumpbox))。</span><span class="sxs-lookup"><span data-stu-id="4ca31-135">If you chose to limit your scale set to a single placement group, then the scale set is deployed with NAT rules configured to let you connect to the scale set easily (if not, to connect to the virtual machines in the scale set, you likely need to create a jumpbox in the same virtual network as the scale set).</span></span> <span data-ttu-id="4ca31-136">若要查看它們，請瀏覽至該擴展集之負載平衡器的 [`Inbound NAT Rules`] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="4ca31-136">To see them, navigate to the `Inbound NAT Rules` tab of the load balancer for the scale set:</span></span>

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="4ca31-138">您可以使用下列 NAT 規則來連線到擴展集中的每個 VM。</span><span class="sxs-lookup"><span data-stu-id="4ca31-138">You can connect to each VM in the scale set using these NAT rules.</span></span> <span data-ttu-id="4ca31-139">例如，針對 Windows 擴展集而言，假設連入連接埠 50000 上具有一個 NAT 規則，您便可以透過 `<load-balancer-ip-address>:50000`上的 RDP 連線到該機器。</span><span class="sxs-lookup"><span data-stu-id="4ca31-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect to that machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="4ca31-140">針對 Linux 擴展集，您必須使用命令 `ssh -p 50000 <username>@<load-balancer-ip-address>`來進行連線。</span><span class="sxs-lookup"><span data-stu-id="4ca31-140">For a Linux scale set, you would connect using the command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ca31-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ca31-141">Next steps</span></span>
<span data-ttu-id="4ca31-142">如需如何從 CLI 部署擴展集的相關文件，請參閱 [此文件](virtual-machine-scale-sets-cli-quick-create.md)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-142">For documentation on how to deploy scale sets from the CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="4ca31-143">如需如何從 PowerShell 部署擴展集的相關文件，請參閱[此文件](virtual-machine-scale-sets-windows-create.md)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-143">For documentation on how to deploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="4ca31-144">如需如何從 Visual Studio 部署擴展集的相關文件，請參閱 [此文件](virtual-machine-scale-sets-vs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-144">For documentation on how to deploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="4ca31-145">如需一般文件，請參閱 [擴展集的文件概觀頁面](virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-145">For general documentation, check out the [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="4ca31-146">如需一般資訊，請參閱 [擴展集的主要登陸頁面](https://azure.microsoft.com/services/virtual-machine-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="4ca31-146">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

