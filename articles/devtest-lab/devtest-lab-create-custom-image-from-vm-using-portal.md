---
title: "從 VM 建立 Azure DevTest Labs 自訂映像 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站在 Azure DevTest Labs 中從已佈建的 VM 建立自訂映像"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="22329-103">從 VM 建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="22329-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="22329-104">逐步指示</span><span class="sxs-lookup"><span data-stu-id="22329-104">Step-by-step instructions</span></span>

<span data-ttu-id="22329-105">您可以從已佈建的 VM 建立自訂映像，之後再使用該自訂映像來建立完全相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="22329-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="22329-106">下列步驟說明如何從 VM 建立自訂映像︰</span><span class="sxs-lookup"><span data-stu-id="22329-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="22329-107">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="22329-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="22329-108">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="22329-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="22329-109">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="22329-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="22329-110">在實驗室的刀鋒視窗中，選取 [我的虛擬機器] 。</span><span class="sxs-lookup"><span data-stu-id="22329-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="22329-111">在 [我的虛擬機器]  刀鋒視窗中，選取要從中建立自訂映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="22329-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="22329-112">在 VM 的刀鋒視窗中，選取 [建立自訂映像 (VHD)] 。</span><span class="sxs-lookup"><span data-stu-id="22329-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![建立自訂映像的功能表項目](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="22329-114">在 [建立映像]  刀鋒視窗上，輸入自訂映像的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="22329-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="22329-115">此資訊會在建立 VM 時顯示於基底清單中。</span><span class="sxs-lookup"><span data-stu-id="22329-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![建立自訂映像刀鋒視窗](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="22329-117">選取 sysprep 是否在 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="22329-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="22329-118">如果 sysprep 未在 VM 上執行，請指定您是否要在從這個自訂映像建立 VM 時讓 sysprep 執行。</span><span class="sxs-lookup"><span data-stu-id="22329-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="22329-119">完成時選取 [確定]  ，以建立自訂映像。</span><span class="sxs-lookup"><span data-stu-id="22329-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="22329-120">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="22329-120">Related blog posts</span></span>

- [<span data-ttu-id="22329-121">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="22329-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="22329-122">在 Azure DevTest Labs 之間複製自訂映像</span><span class="sxs-lookup"><span data-stu-id="22329-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="22329-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22329-123">Next steps</span></span>

- [<span data-ttu-id="22329-124">將 VM 新增到實驗室</span><span class="sxs-lookup"><span data-stu-id="22329-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
