---
title: "了解 Azure DevTest Labs 中的共用 IP 位址 | Microsoft Docs"
description: "了解 Azure DevTest Labs 如何使用共用 IP 位址，將需要存取您的實驗室 VM 的公用 IP 位址減到最少。"
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
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="438c6-103">了解 Azure DevTest Labs 中的共用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="438c6-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="438c6-104">Azure DevTest Labs 讓實驗室 VM 共用相同公用 IP 位址，將需要存取您的個人實驗室 VM 的公用 IP 位址數目減到最少。</span><span class="sxs-lookup"><span data-stu-id="438c6-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="438c6-105">本文說明共用 IP 的運作方式和其相關的組態選項。</span><span class="sxs-lookup"><span data-stu-id="438c6-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="438c6-106">共用 IP 設定</span><span class="sxs-lookup"><span data-stu-id="438c6-106">Shared IP setting</span></span>

<span data-ttu-id="438c6-107">當您建立實驗室時，它會位於虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="438c6-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="438c6-108">根據預設，建立這個子網路時會將 [啟用共用公用 IP]設為 [是]。</span><span class="sxs-lookup"><span data-stu-id="438c6-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="438c6-109">此設定會為整個子網路建立一個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="438c6-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="438c6-110">如需設定虛擬網路和子網路的詳細資訊，請參閱[設定 Azure DevTest Labs 中的虛擬網路](devtest-lab-configure-vnet.md)。</span><span class="sxs-lookup"><span data-stu-id="438c6-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![新的實驗室子網路](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="438c6-112">針對現有的實驗室，您可以藉由選取 [設定和原則 > 虛擬網路] 來啟用這個選項。</span><span class="sxs-lookup"><span data-stu-id="438c6-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="438c6-113">然後，從清單中選取虛擬網路，並且針對選取的子網路選擇 [啟用共用公用 IP]。</span><span class="sxs-lookup"><span data-stu-id="438c6-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="438c6-114">如果您不想要在實驗室 VM 之間共用公用 IP 位址，您也可以在任何實驗室中停用這個選項。</span><span class="sxs-lookup"><span data-stu-id="438c6-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="438c6-115">此實驗室中建立任何 VM 會預設為使用共用 IP。</span><span class="sxs-lookup"><span data-stu-id="438c6-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="438c6-116">建立 VM 時，此設定會出現在 [進階設定] 刀鋒視窗的 [IP 位址組態] 之下。</span><span class="sxs-lookup"><span data-stu-id="438c6-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![新的 VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="438c6-118">**共用：**建立為**共用**的所有 VM 歸類到一個資源群組 (RG)。</span><span class="sxs-lookup"><span data-stu-id="438c6-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="438c6-119">針對該 RG 指派單一 IP 位址，RG 中的所有 VM 將會使用該 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="438c6-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="438c6-120">**公用：**您建立的每個 VM 有它自己的 IP 位址，而且建立在它自己的資源群組。</span><span class="sxs-lookup"><span data-stu-id="438c6-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="438c6-121">**私人：**您建立的每個 VM 使用私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="438c6-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="438c6-122">您無法使用遠端桌面直接從網際網路連線到此 VM。</span><span class="sxs-lookup"><span data-stu-id="438c6-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="438c6-123">每當已啟用共用 IP 的 VM 新增至子網路時，DevTest Labs 就會自動將 VM 新增至負載平衡器，並且在公用 IP 位址上指派 TCP 通訊埠號碼，以轉送至 VM 上的 RDP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="438c6-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="438c6-124">使用共用 IP</span><span class="sxs-lookup"><span data-stu-id="438c6-124">Using the shared IP</span></span>

- <span data-ttu-id="438c6-125">**Linux 使用者**：您可以使用 IP 位址或完整網域名稱，後面緊接冒號，再接著連接埠，以 SSH 至 VM。</span><span class="sxs-lookup"><span data-stu-id="438c6-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="438c6-126">例如，在下圖中，連線至 VM 的 RDP 位址是 `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`。</span><span class="sxs-lookup"><span data-stu-id="438c6-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![VM 範例](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="438c6-128">**Windows 使用者**：選取 Azure 入口網站中的 [連線] 按鈕，下載預先設定的 RDP 檔案，並且存取 VM。</span><span class="sxs-lookup"><span data-stu-id="438c6-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="438c6-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="438c6-129">Next steps</span></span>

* [<span data-ttu-id="438c6-130">在 Azure DevTest Labs 中定義實驗室原則</span><span class="sxs-lookup"><span data-stu-id="438c6-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="438c6-131">在 Azure DevTest Labs 中設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="438c6-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





