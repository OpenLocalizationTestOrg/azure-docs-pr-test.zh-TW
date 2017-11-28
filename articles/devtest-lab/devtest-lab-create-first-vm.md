---
title: "aaaCreate 您在 Azure DevTest 實驗室的實驗室中的第一個 VM |Microsoft 文件"
description: "深入了解如何 toocreate Azure DevTest 實驗室中的實驗室中的第一個虛擬機器"
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
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="0a4dd-103">在 Azure DevTest Labs 的實驗室中建立您的第一個 VM</span><span class="sxs-lookup"><span data-stu-id="0a4dd-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="0a4dd-104">當您一開始存取 DevTest Labs，並想 toocreate 第一個 VM 時，您將可能會使用進行預先載入[基底 marketplace 映像](devtest-lab-configure-marketplace-images.md)。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="0a4dd-105">在稍後，您也可以從能夠 toochoose[自訂映像和公式](devtest-lab-add-vm.md)時建立多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="0a4dd-106">本教學課程中引導您使用 Azure 入口網站 tooadd hello DevTest Labs 中的第一個 VM tooa 實驗室。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="0a4dd-107">步驟 tooadd Azure DevTest Labs 中的第一個 VM tooa 實驗室</span><span class="sxs-lookup"><span data-stu-id="0a4dd-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="0a4dd-108">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="0a4dd-109">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="0a4dd-110">從 hello 清單的實驗室中，選取您想在其中 toocreate hello VM hello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="0a4dd-111">在 hello 實驗室**概觀**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![加入 VM 按鈕](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="0a4dd-113">在 hello**選擇基底**刀鋒視窗中，選取 marketplace 映像的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="0a4dd-114">在 hello**虛擬機器**刀鋒視窗中，輸入 hello 新的虛擬機器的名稱在 hello**虛擬機器名稱**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![實驗室 VM 刀鋒視窗](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="0a4dd-116">輸入**使用者名**，授與 hello 虛擬機器上的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="0a4dd-117">標示的 hello 文字欄位中輸入密碼**輸入值**。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="0a4dd-118">hello**虛擬機器磁碟類型**會決定哪些儲存磁碟類型可供 hello hello 實驗室中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="0a4dd-119">選取**虛擬機器大小**和選取 hello 的其中一個預先定義的指定 hello 處理器核心、 RAM 大小，以及 hello VM toocreate hello 硬碟大小的項目。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="0a4dd-120">選取**成品**和-從成品-hello 清單選取，然後設定您想 tooadd toohello 基底映像的 hello 成品。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="0a4dd-121">**注意：**若您是新 tooDevTest 實驗室或設定成品，請參閱 toohello[加入現有的成品 tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm)區段，然後再在完成時，返回此處。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="0a4dd-122">選取**建立**tooadd hello 指定 VM toohello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="0a4dd-123">hello 實驗室刀鋒視窗會顯示 hello 狀態的 hello VM 建立-第一次為**建立**，然後為**執行**之後 hello VM 已啟動。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a4dd-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a4dd-124">Next steps</span></span>
* <span data-ttu-id="0a4dd-125">一次 hello 在建立 VM，您可以連接 toohello VM 選取**連接**hello VM 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="0a4dd-126">簽出[加入 VM tooa 實驗室](devtest-lab-add-vm.md)如需將後續的 Vm 加入您的實驗室中的更完整資訊。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="0a4dd-127">瀏覽 hello [DevTest Labs Azure 資源管理員的快速入門範本庫](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)。</span><span class="sxs-lookup"><span data-stu-id="0a4dd-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
