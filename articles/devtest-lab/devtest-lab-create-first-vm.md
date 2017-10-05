---
title: "在 Azure DevTest Labs 的實驗室中建立您的第一個 VM | Microsoft Docs"
description: "了解如何在 Azure DevTest Labs 的實驗室中建立您的第一個虛擬機器"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: aa6b60b799e1e98815cf288d5612f98cd77cc00e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="179c8-103">在 Azure DevTest Labs 的實驗室中建立您的第一個 VM</span><span class="sxs-lookup"><span data-stu-id="179c8-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="179c8-104">當您首次存取 DevTest Labs 並想要建立您的第一個 VM 時，您很有可能會透過預先載入的[基底 Marketplace 映像](devtest-lab-configure-marketplace-images.md)來完成。</span><span class="sxs-lookup"><span data-stu-id="179c8-104">When you initially access DevTest Labs and want to create your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="179c8-105">您在稍後建立更多 VM 時，也可以在[自訂映像和公式](devtest-lab-add-vm.md)之間做出選擇。</span><span class="sxs-lookup"><span data-stu-id="179c8-105">Later on, you'll also be able to choose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="179c8-106">本教學課程會逐步引導您使用 Azure 入口網站，在 DevTest Labs 中將您的第一個 VM 新增至實驗室。</span><span class="sxs-lookup"><span data-stu-id="179c8-106">This tutorial walks you through using the Azure portal to add your first VM to a lab in DevTest Labs.</span></span>

## <a name="steps-to-add-your-first-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="179c8-107">在 Azure DevTest Labs 中將您的第一個 VM 新增至實驗室的步驟</span><span class="sxs-lookup"><span data-stu-id="179c8-107">Steps to add your first VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="179c8-108">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="179c8-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="179c8-109">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="179c8-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="179c8-110">從實驗室清單中，選取您想要在其中建立 VM 的實驗室。</span><span class="sxs-lookup"><span data-stu-id="179c8-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="179c8-111">在實驗室的 [概觀] 刀鋒視窗中，選取 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="179c8-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="179c8-113">在 [選擇基底] 刀鋒視窗上，選取 VM 的 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="179c8-113">On the **Choose a base** blade, select a marketplace image for the VM.</span></span>
1. <span data-ttu-id="179c8-114">在 [虛擬機器] 刀鋒視窗的 [虛擬機器名稱] 文字方塊中，輸入新虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="179c8-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="179c8-116">輸入**使用者名稱**，此名稱會被授與虛擬機器上的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="179c8-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="179c8-117">在標示為 [輸入值] 的文字欄位中輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="179c8-117">Enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="179c8-118">[虛擬機器磁碟類型] 會決定實驗室中的虛擬機器所允許的儲存磁碟類型。</span><span class="sxs-lookup"><span data-stu-id="179c8-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="179c8-119">選取 [虛擬機器大小]  ，然後選取其中一個預先定義的項目，這些項目可以指定處理器核心、RAM 大小，以及要建立的 VM 的硬碟大小。</span><span class="sxs-lookup"><span data-stu-id="179c8-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="179c8-120">選取 [構件]，然後從構件清單中，選取並設定您想要新增到基本映像中的構件。</span><span class="sxs-lookup"><span data-stu-id="179c8-120">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="179c8-121">**附註：**如果您對 DevTest Labs 或設定構件並不熟悉，請參閱[將現有的構件加入至 VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) 一節，完成該節之後再返回此處。</span><span class="sxs-lookup"><span data-stu-id="179c8-121">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="179c8-122">選取 [建立]  ，將指定的 VM 加入實驗室。</span><span class="sxs-lookup"><span data-stu-id="179c8-122">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="179c8-123">實驗室刀鋒視窗會顯示 VM 的建立狀態，其狀態會先是 [正在建立]，在啟動該 VM 之後才會變成 [正在執行]。</span><span class="sxs-lookup"><span data-stu-id="179c8-123">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="179c8-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="179c8-124">Next steps</span></span>
* <span data-ttu-id="179c8-125">一旦建立 VM 之後，您可以選取 VM 刀鋒視窗上的 [連接]  來連接至 VM。</span><span class="sxs-lookup"><span data-stu-id="179c8-125">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="179c8-126">查看[對實驗室新增 VM](devtest-lab-add-vm.md) 以取得在實驗室中新增後續 VM 的完整資訊。</span><span class="sxs-lookup"><span data-stu-id="179c8-126">Check out [Add a VM to a lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="179c8-127">瀏覽 [DevTest Labs Azure Resource Manager 快速入門範本資源庫 (英文)](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)。</span><span class="sxs-lookup"><span data-stu-id="179c8-127">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
