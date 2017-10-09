---
title: "aaaConfigure 位於 Azure 的 DevTest Labs 虛擬網路 |Microsoft 文件"
description: "深入了解如何 tooconfigure 現有的虛擬網路和子網路，並將其用於具有 Azure DevTest Labs 的 VM"
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
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a><span data-ttu-id="26f12-103">設定 Azure DevTest Labs 中的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="26f12-103">Configure a virtual network in Azure DevTest Labs</span></span>
<span data-ttu-id="26f12-104">Hello 文章所述[加入成品 tooa 實驗室與 VM](devtest-lab-add-vm-with-artifacts.md)，當您建立 VM 在實驗室中，您可以指定設定的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26f12-104">As explained in hello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md), when you create a VM in a lab, you can specify a configured virtual network.</span></span> <span data-ttu-id="26f12-105">執行此動作的其中一個案例是您的公司網路資源，您使用的 Vm 所傳來如果您需要 tooaccess hello 與 ExpressRoute 或站對站 VPN 已經設定的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26f12-105">One scenario for doing this is if you need tooaccess your corpnet resources from your VMs using hello virtual network that was configured with ExpressRoute or site-to-site VPN.</span></span> <span data-ttu-id="26f12-106">hello 下列各節將說明如何 tooadd 實驗室的虛擬網路設定，讓建立 Vm 時，它會變成可用 toochoose 到您現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26f12-106">hello following sections illustrate how tooadd your existing virtual network into a lab's Virtual Network settings so that it is available toochoose when creating VMs.</span></span>

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a><span data-ttu-id="26f12-107">設定實驗室，使用 hello Azure 入口網站的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="26f12-107">Configure a virtual network for a lab using hello Azure portal</span></span>
<span data-ttu-id="26f12-108">hello 下列步驟引導您完成新增現有的虛擬網路 （和子網路） tooa 實驗室使 hello 中建立 VM 時才能使用相同的實驗室。</span><span class="sxs-lookup"><span data-stu-id="26f12-108">hello following steps walk you through adding an existing virtual network (and subnet) tooa lab so that it can be used when creating a VM in hello same lab.</span></span> 

1. <span data-ttu-id="26f12-109">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="26f12-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="26f12-110">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="26f12-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="26f12-111">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="26f12-111">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="26f12-112">在 hello 實驗室刀鋒視窗中，選取 **組態**。</span><span class="sxs-lookup"><span data-stu-id="26f12-112">On hello lab's blade, select **Configuration**.</span></span>
5. <span data-ttu-id="26f12-113">在 hello 實驗室**組態**刀鋒視窗中，選取**虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="26f12-113">On hello lab's **Configuration** blade, select **Virtual networks**.</span></span>
6. <span data-ttu-id="26f12-114">在 hello**虛擬網路**刀鋒視窗中，您會看到一份 hello 目前實驗室以及 hello 預設建立虛擬網路是您的實驗室中設定虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26f12-114">On hello **Virtual networks** blade, you see a list of virtual networks configured for hello current lab as well as hello default virtual network that is created for your lab.</span></span> 
7. <span data-ttu-id="26f12-115">選取 [+ 新增] 。</span><span class="sxs-lookup"><span data-stu-id="26f12-115">Select **+ Add**.</span></span>
   
    ![加入現有的虛擬網路 tooyour 實驗室](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. <span data-ttu-id="26f12-117">在 hello**虛擬網路**刀鋒視窗中，選取**[選取虛擬網路]**。</span><span class="sxs-lookup"><span data-stu-id="26f12-117">On hello **Virtual network** blade, select **[Select virtual network]**.</span></span>
   
    ![選取現有的虛擬網路](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. <span data-ttu-id="26f12-119">在 hello**選擇虛擬網路**刀鋒視窗中，選取 hello 所需的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26f12-119">On hello **Choose virtual network** blade, select hello desired virtual network.</span></span> <span data-ttu-id="26f12-120">hello 刀鋒視窗中顯示所有 hello 虛擬網路會在 hello 相同 hello 實驗室 hello 訂用帳戶中的區域。</span><span class="sxs-lookup"><span data-stu-id="26f12-120">hello blade shows all hello virtual networks that are under hello same region in hello subscription as hello lab.</span></span>  
10. <span data-ttu-id="26f12-121">選取虛擬網路之後, 您會返回 toohello**虛擬網路**按一下 hello hello 在 hello hello 刀鋒視窗底部的清單中的子網路。</span><span class="sxs-lookup"><span data-stu-id="26f12-121">After selecting a virtual network, you are returned toohello **Virtual network** Click hello subnet in hello list at hello bottom of hello blade.</span></span>

    ![子網路清單](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    <span data-ttu-id="26f12-123">hello 實驗室子網路 刀鋒視窗會顯示。</span><span class="sxs-lookup"><span data-stu-id="26f12-123">hello Lab Subnet blade is displayed.</span></span>

    ![實驗室子網路刀鋒視窗](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. <span data-ttu-id="26f12-125">指定 [實驗室子網路名稱]。</span><span class="sxs-lookup"><span data-stu-id="26f12-125">Specify a **Lab subnet name**.</span></span>
12. <span data-ttu-id="26f12-126">在實驗室中建立 VM，使用子網路 toobe tooallow 選取**中建立虛擬機器使用**。</span><span class="sxs-lookup"><span data-stu-id="26f12-126">tooallow a subnet toobe used in lab VM creation, select **Use in virtual machine creation**.</span></span>
13. <span data-ttu-id="26f12-127">tooenable[共用公用 IP 位址](devtest-lab-shared-ip.md)，選取**啟用共用公用 IP**。</span><span class="sxs-lookup"><span data-stu-id="26f12-127">tooenable a [shared public IP address](devtest-lab-shared-ip.md), select **Enable shared public IP**.</span></span>
14. <span data-ttu-id="26f12-128">tooallow 公用 IP 位址的子網路中，選取**允許公用 IP 建立**。</span><span class="sxs-lookup"><span data-stu-id="26f12-128">tooallow public IP addresses in a subnet, select **Allow public IP creation**.</span></span>
15. <span data-ttu-id="26f12-129">在 hello**每位使用者最多虛擬機器**欄位中，指定 hello 每位使用者每個子網路的最大 Vm。</span><span class="sxs-lookup"><span data-stu-id="26f12-129">In hello **Maximum virtual machines per user** field, specify hello maximum VMs per user for each subnet.</span></span> <span data-ttu-id="26f12-130">如果您想要不限數目的 VM 數，請將此欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="26f12-130">If you want an unrestricted number of VMs, leave this field blank.</span></span>
16. <span data-ttu-id="26f12-131">選取**確定**tooclose hello 實驗室子網路 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="26f12-131">Select **OK** tooclose hello Lab Subnet blade.</span></span>
17. <span data-ttu-id="26f12-132">選取**儲存**tooclose hello 虛擬網路 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="26f12-132">Select **Save** tooclose hello Virtual network blade.</span></span>
18. <span data-ttu-id="26f12-133">既然 hello 虛擬網路設定，也可以選取建立 VM 時。</span><span class="sxs-lookup"><span data-stu-id="26f12-133">Now that hello virtual network is configured, it can be selected when creating a VM.</span></span> 
    <span data-ttu-id="26f12-134">toosee 如何 toocreate VM 並指定虛擬網路，請參閱 toohello 文章[加入成品 tooa 實驗室與 VM](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="26f12-134">toosee how toocreate a VM and specify a virtual network, refer toohello article, [Add a VM with artifacts tooa lab](devtest-lab-add-vm-with-artifacts.md).</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="26f12-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26f12-135">Next steps</span></span>
<span data-ttu-id="26f12-136">新增 hello 預期虛擬網路 tooyour 實驗室之後下, 一個步驟的 hello 太[加入 VM tooyour 實驗室](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="26f12-136">Once you have added hello desired virtual network tooyour lab, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

