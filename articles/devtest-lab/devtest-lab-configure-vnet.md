---
title: "設定 Azure DevTest Labs 中的虛擬網路 | Microsoft Docs"
description: "了解如何設定現有的虛擬網路和子網路，並在具備 Azure DevTest Labs 的 VM 中使用它們"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 848752085729df7d98a3a4b7be36d894c12cd033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="bb675-103">設定 Azure DevTest Labs 中的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="bb675-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="bb675-104">如 [將具有構件的 VM 加入實驗室](devtest-lab-add-vm-with-artifacts.md)文章中所述，當您在實驗室中建立 VM 時，可以指定已設定的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bb675-104">As explained in the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="bb675-105">例如，如果您需要使用以 ExpressRoute 或站台對站台 VPN 設定的虛擬網路從您的 VM 存取公司資源時，就可以這麼做。</span><span class="sxs-lookup"><span data-stu-id="bb675-105">One scenario for doing this is if you need to access your corpnet resources from your VMs using the virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="bb675-106">下列各節將說明如何將現有的虛擬網路加入至實驗室的虛擬網路設定，就能在建立 VM 時選擇它。</span><span class="sxs-lookup"><span data-stu-id="bb675-106">The following sections illustrate how to add your existing virtual network into a lab's Virtual Network settings so that it is available to choose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-the-azure-portal"></a><span data-ttu-id="bb675-107">使用 Azure 入口網站設定適用於實驗室的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="bb675-107">Configure a virtual network for a lab using the Azure portal</span></span>
<span data-ttu-id="bb675-108">下列步驟會逐步引導您將現有虛擬網路 (和子網路) 加入至實驗室，以便在同一個實驗室中建立 VM 時加以使用。</span><span class="sxs-lookup"><span data-stu-id="bb675-108">The following steps walk you through adding an existing virtual network (and subnet) to a lab so that it can be used when creating a VM in the same lab.</span></span> 

1. <span data-ttu-id="bb675-109">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="bb675-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="bb675-110">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="bb675-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="bb675-111">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="bb675-111">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="bb675-112">在實驗室的刀鋒視窗上，選取 [組態] 。</span><span class="sxs-lookup"><span data-stu-id="bb675-112">On the lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="bb675-113">在實驗室的 [組態] 刀鋒視窗上，選取 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="bb675-113">On the lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="bb675-114">在 [虛擬網路]  刀鋒視窗中，您會看到您已針對目前的實驗室設定的虛擬網路清單，以及為實驗室所建立的預設虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bb675-114">On the **Virtual networks** blade, you see a list of virtual networks configured for the current lab as well as the default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="bb675-115">選取 [+ 新增] 。</span><span class="sxs-lookup"><span data-stu-id="bb675-115">Select **+ Add**.</span></span>
   
    ![將現有的虛擬網路加入至您的實驗室](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="bb675-117">在 [虛擬網路] 刀鋒視窗中，選取 [選取虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="bb675-117">On the **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![選取現有的虛擬網路](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="bb675-119">在 [選擇虛擬網路]  刀鋒視窗中，選取所需的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bb675-119">On the **Choose virtual network** blade, select the desired virtual network.</span></span> <span data-ttu-id="bb675-120">刀鋒視窗會顯示訂用帳戶中與實驗室位於相同區域下方的所有虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bb675-120">The blade shows all the virtual networks that are under the same region in the subscription as the lab.</span></span>  
10. <span data-ttu-id="bb675-121">選取虛擬網路之後，您會回到 [虛擬網路]。按一下刀鋒視窗底部清單中的子網路。</span><span class="sxs-lookup"><span data-stu-id="bb675-121">After selecting a virtual network, you are returned to the **Virtual network** Click the subnet in the list at the bottom of the blade.</span></span>

    ![子網路清單](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="bb675-123">[實驗室子網路] 刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="bb675-123">The Lab Subnet blade is displayed.</span></span>

    ![實驗室子網路刀鋒視窗](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="bb675-125">指定 [實驗室子網路名稱]。</span><span class="sxs-lookup"><span data-stu-id="bb675-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="bb675-126">若要允許在實驗室 VM 建立期間使用子網路，請選取 [在虛擬機器建立時使用]。</span><span class="sxs-lookup"><span data-stu-id="bb675-126">To allow a subnet to be used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="bb675-127">若要啟用[共用公用 IP 位址](devtest-lab-shared-ip.md)，請選取 [啟用共用公用 IP]。</span><span class="sxs-lookup"><span data-stu-id="bb675-127">To enable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="bb675-128">若要允許子網路中使用公用 IP 位址，請選取 [允許建立公用 IP] 。</span><span class="sxs-lookup"><span data-stu-id="bb675-128">To allow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="bb675-129">在 [每位使用者的最大虛擬機器數] 欄位中，針對每個子網路指定每位使用者的最大 VM 數。</span><span class="sxs-lookup"><span data-stu-id="bb675-129">In the **Maximum virtual machines per user** field, specify the maximum VMs per user for each subnet.</span></span> <span data-ttu-id="bb675-130">如果您想要不限數目的 VM 數，請將此欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="bb675-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="bb675-131">選取 [確定]，關閉 [實驗室子網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bb675-131">Select **OK** to close the Lab Subnet blade.</span></span>
17. <span data-ttu-id="bb675-132">選取 [儲存]，關閉 [虛擬網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="bb675-132">Select **Save** to close the Virtual network blade.</span></span>
18. <span data-ttu-id="bb675-133">現在已設定虛擬網路，在建立 VM 時就能選取它。</span><span class="sxs-lookup"><span data-stu-id="bb675-133">Now that the virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="bb675-134">若要查看如何建立 VM 並指定虛擬網路，請參閱 [將具有構件的 VM 加入實驗室](devtest-lab-add-vm-with-artifacts.md)一文。</span><span class="sxs-lookup"><span data-stu-id="bb675-134">To see how to create a VM and specify a virtual network, refer to the article, [Add a VM with artifacts to a lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="bb675-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb675-135">Next steps</span></span>
<span data-ttu-id="bb675-136">一旦您在實驗室中加入所需的虛擬網路之後，下一個步驟就是 [將 VM 加入至實驗室](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="bb675-136">Once you have added the desired virtual network to your lab, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

