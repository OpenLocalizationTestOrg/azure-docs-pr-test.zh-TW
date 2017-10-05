---
title: "從 VHD 檔案建立 Azure DevTest Labs 自訂映像 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="4ce08-103">從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="4ce08-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="4ce08-104">逐步指示</span><span class="sxs-lookup"><span data-stu-id="4ce08-104">Step-by-step instructions</span></span>

<span data-ttu-id="4ce08-105">下列步驟將逐步引導您使用 Azure 入口網站從 VHD 檔案建立自訂映像：</span><span class="sxs-lookup"><span data-stu-id="4ce08-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="4ce08-106">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="4ce08-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="4ce08-107">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="4ce08-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="4ce08-108">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="4ce08-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="4ce08-109">在實驗室的刀鋒視窗上，選取 [組態] 。</span><span class="sxs-lookup"><span data-stu-id="4ce08-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="4ce08-110">在實驗室的 [組態] 刀鋒視窗上，選取 [自訂映像 (VHD)]。</span><span class="sxs-lookup"><span data-stu-id="4ce08-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="4ce08-111">在 [自訂映像] 刀鋒視窗上，選取 [+加入]。</span><span class="sxs-lookup"><span data-stu-id="4ce08-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![加入自訂映像](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="4ce08-113">輸入自訂映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ce08-113">Enter the name of the custom image.</span></span> <span data-ttu-id="4ce08-114">這個名稱會在建立 VM 時顯示於基本映像清單中。</span><span class="sxs-lookup"><span data-stu-id="4ce08-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4ce08-115">輸入自訂映像的描述。</span><span class="sxs-lookup"><span data-stu-id="4ce08-115">Enter the description of the custom image.</span></span> <span data-ttu-id="4ce08-116">這個描述會在建立 VM 時顯示於基本映像清單中。</span><span class="sxs-lookup"><span data-stu-id="4ce08-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="4ce08-117">選取 [VHD]。</span><span class="sxs-lookup"><span data-stu-id="4ce08-117">Select **VHD**.</span></span>

1. <span data-ttu-id="4ce08-118">從 [VHD] 刀鋒視窗，選取想要的 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="4ce08-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="4ce08-119">選取 [確定] 以關閉 [VHD] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4ce08-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="4ce08-120">選取 [作業系統組態]。</span><span class="sxs-lookup"><span data-stu-id="4ce08-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="4ce08-121">在 [作業系統組態] 索引標籤上，選取 [Windows] 或 [Linux]。</span><span class="sxs-lookup"><span data-stu-id="4ce08-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="4ce08-122">如果選取 [Windows]  ，請透過核取方塊來指定 *Sysprep* 是否已在電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="4ce08-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="4ce08-123">選取 [確定] 以關閉 [作業系統組態] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4ce08-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="4ce08-124">選取 [確定]  ，以建立自訂映像。</span><span class="sxs-lookup"><span data-stu-id="4ce08-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4ce08-125">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="4ce08-125">Related blog posts</span></span>

- [<span data-ttu-id="4ce08-126">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="4ce08-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="4ce08-127">在 Azure DevTest Labs 之間複製自訂映像</span><span class="sxs-lookup"><span data-stu-id="4ce08-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="4ce08-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ce08-128">Next steps</span></span>

- [<span data-ttu-id="4ce08-129">將 VM 新增到實驗室</span><span class="sxs-lookup"><span data-stu-id="4ce08-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
