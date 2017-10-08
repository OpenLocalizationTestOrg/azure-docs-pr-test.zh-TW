---
title: "aaaCreate Azure DevTest Labs 自訂映像從 VM |Microsoft 文件"
description: "了解如何從佈建的 VM 使用 Azure DevTest Labs 中的自訂映像 toocreate hello Azure 入口網站"
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
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="9fd65-103">從 VM 建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="9fd65-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="9fd65-104">逐步指示</span><span class="sxs-lookup"><span data-stu-id="9fd65-104">Step-by-step instructions</span></span>

<span data-ttu-id="9fd65-105">您可以從佈建 VM，建立自訂映像，並在之後使用該自訂映像 toocreate 相同的 Vm。</span><span class="sxs-lookup"><span data-stu-id="9fd65-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="9fd65-106">hello 下列步驟說明如何 toocreate 自訂映像從 VM:</span><span class="sxs-lookup"><span data-stu-id="9fd65-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="9fd65-107">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="9fd65-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="9fd65-108">選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="9fd65-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="9fd65-109">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="9fd65-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="9fd65-110">在 hello 實驗室刀鋒視窗中，選取 **我的虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="9fd65-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="9fd65-111">在 hello**我的虛擬機器**刀鋒視窗中，選取 hello VM 要從中 toocreate hello 自訂映像。</span><span class="sxs-lookup"><span data-stu-id="9fd65-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="9fd65-112">在 hello VM 刀鋒視窗中，選取 **建立自訂映像 (VHD)**。</span><span class="sxs-lookup"><span data-stu-id="9fd65-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![建立自訂映像的功能表項目](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="9fd65-114">在 hello**建立映像**刀鋒視窗中，輸入名稱和自訂映像的描述。</span><span class="sxs-lookup"><span data-stu-id="9fd65-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="9fd65-115">當您建立 VM 時，這項資訊會顯示 hello 從基底清單中。</span><span class="sxs-lookup"><span data-stu-id="9fd65-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![建立自訂映像刀鋒視窗](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="9fd65-117">選擇是否要在 hello VM 上執行 sysprep。</span><span class="sxs-lookup"><span data-stu-id="9fd65-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="9fd65-118">如果不執行 hello sysprep hello VM 上，指定是否要從這個自訂映像建立 VM 時執行 sysprep。</span><span class="sxs-lookup"><span data-stu-id="9fd65-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="9fd65-119">選取**確定**時完成的 toocreate hello 自訂映像。</span><span class="sxs-lookup"><span data-stu-id="9fd65-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="9fd65-120">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="9fd65-120">Related blog posts</span></span>

- [<span data-ttu-id="9fd65-121">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="9fd65-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="9fd65-122">在 Azure DevTest Labs 之間複製自訂映像</span><span class="sxs-lookup"><span data-stu-id="9fd65-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="9fd65-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9fd65-123">Next steps</span></span>

- [<span data-ttu-id="9fd65-124">新增 VM tooyour 實驗室</span><span class="sxs-lookup"><span data-stu-id="9fd65-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
