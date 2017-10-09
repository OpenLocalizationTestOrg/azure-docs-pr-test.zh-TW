---
title: "aaaUnderstand 共用 Azure DevTest Labs 中的 IP 位址 |Microsoft 文件"
description: "了解如何 Azure DevTest Labs 會使用共用的 IP 位址 toominimize hello 公用 IP 位址需要的 tooaccess 實驗室 Vm。"
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="a79c4-103">了解 Azure DevTest Labs 中的共用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a79c4-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="a79c4-104">Azure 的 DevTest Labs 可讓實驗室 Vm 共用 hello 相同公用 IP 位址 toominimize hello 數目的公用 IP 位址需要 tooaccess 個別實驗室 Vm。</span><span class="sxs-lookup"><span data-stu-id="a79c4-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="a79c4-105">本文說明共用 IP 的運作方式和其相關的組態選項。</span><span class="sxs-lookup"><span data-stu-id="a79c4-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="a79c4-106">共用 IP 設定</span><span class="sxs-lookup"><span data-stu-id="a79c4-106">Shared IP setting</span></span>

<span data-ttu-id="a79c4-107">當您建立實驗室時，它會位於虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="a79c4-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="a79c4-108">根據預設，此子網路建立與**啟用共用公用 IP**設定得*是*。</span><span class="sxs-lookup"><span data-stu-id="a79c4-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="a79c4-109">此設定會建立一個 hello 整個子網路的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a79c4-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="a79c4-110">如需設定虛擬網路和子網路的詳細資訊，請參閱[設定 Azure DevTest Labs 中的虛擬網路](devtest-lab-configure-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="a79c4-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![新的實驗室子網路](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="a79c4-112">針對現有的實驗室，您可以藉由選取 [設定和原則 > 虛擬網路] 來啟用這個選項。</span><span class="sxs-lookup"><span data-stu-id="a79c4-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="a79c4-113">然後，從 hello 清單中選取虛擬網路，並選擇 **啟用共用的公用 IP**選子網路。</span><span class="sxs-lookup"><span data-stu-id="a79c4-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="a79c4-114">如果您不要跨實驗室 Vm tooshare 公用 IP 位址，您也可以停用任何實驗室中的這個選項。</span><span class="sxs-lookup"><span data-stu-id="a79c4-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="a79c4-115">這個實驗室預設 toousing 中所建立的共用的 IP 任何 Vm。</span><span class="sxs-lookup"><span data-stu-id="a79c4-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="a79c4-116">此設定在建立 hello VM 時，會出現在 hello**進階設定**刀鋒視窗底下**IP 位址設定**。</span><span class="sxs-lookup"><span data-stu-id="a79c4-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![新的 VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="a79c4-118">**共用：**建立為**共用**的所有 VM 歸類到一個資源群組 (RG)。</span><span class="sxs-lookup"><span data-stu-id="a79c4-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="a79c4-119">單一 IP 位址會指派該 RG 和 hello RG 中所有的 Vm 將會使用該 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a79c4-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="a79c4-120">**公用：**您建立的每個 VM 有它自己的 IP 位址，而且建立在它自己的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a79c4-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="a79c4-121">**私人：**您建立的每個 VM 使用私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a79c4-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="a79c4-122">您將不會直接從 hello 無法 tooconnect toothis VM 網際網路的遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="a79c4-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="a79c4-123">具有共用 IP 已啟用的 VM 加入 toohello 子網路，每當 DevTest Labs 自動加入 hello VM tooa 負載平衡器，並將 hello 公用 IP 位址的 TCP 連接埠號碼指派轉送 toohello hello VM 上的 RDP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="a79c4-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="a79c4-124">使用 hello 共用 IP</span><span class="sxs-lookup"><span data-stu-id="a79c4-124">Using hello shared IP</span></span>

- <span data-ttu-id="a79c4-125">**Linux 使用者：** SSH toohello VM 使用 hello IP 位址或完整的網域名稱，後面接著冒號，後面接著 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="a79c4-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="a79c4-126">例如，在 hello 圖，hello RDP 位址 tooconnect toohello VM 是`doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`。</span><span class="sxs-lookup"><span data-stu-id="a79c4-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![VM 範例](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="a79c4-128">**Windows 使用者：**選取 hello**連接**按鈕 hello Azure 入口網站 toodownload 預先設定的 RDP 檔案，並存取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a79c4-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a79c4-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a79c4-129">Next steps</span></span>

* [<span data-ttu-id="a79c4-130">在 Azure DevTest Labs 中定義實驗室原則</span><span class="sxs-lookup"><span data-stu-id="a79c4-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="a79c4-131">在 Azure DevTest Labs 中設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a79c4-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





