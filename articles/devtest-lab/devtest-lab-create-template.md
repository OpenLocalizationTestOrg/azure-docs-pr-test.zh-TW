---
title: "aaaCreate Azure DevTest Labs 自訂映像的 VHD 檔案從 |Microsoft 文件"
description: "了解如何在 Azure DevTest Labs 從 VHD 檔案使用的自訂映像 toocreate hello Azure 入口網站"
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
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="87e2d-103">從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="87e2d-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="87e2d-104">逐步指示</span><span class="sxs-lookup"><span data-stu-id="87e2d-104">Step-by-step instructions</span></span>

<span data-ttu-id="87e2d-105">hello 下列步驟引導您完成建立自訂映像從 VHD 檔案使用 hello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="87e2d-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="87e2d-106">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="87e2d-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="87e2d-107">選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="87e2d-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="87e2d-108">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="87e2d-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="87e2d-109">在 hello 實驗室刀鋒視窗中，選取 **組態**。</span><span class="sxs-lookup"><span data-stu-id="87e2d-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="87e2d-110">在 hello 實驗室**組態**刀鋒視窗中，選取**自訂映像 (Vhd)**。</span><span class="sxs-lookup"><span data-stu-id="87e2d-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="87e2d-111">在 hello**自訂映像**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="87e2d-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![加入自訂映像](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="87e2d-113">輸入 hello hello 自訂映像名稱。</span><span class="sxs-lookup"><span data-stu-id="87e2d-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="87e2d-114">建立 VM 時，此名稱會顯示 hello 的基底映像的清單中。</span><span class="sxs-lookup"><span data-stu-id="87e2d-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="87e2d-115">輸入 hello hello 自訂映像的描述。</span><span class="sxs-lookup"><span data-stu-id="87e2d-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="87e2d-116">建立 VM 時，此描述會顯示 hello 的基底映像的清單中。</span><span class="sxs-lookup"><span data-stu-id="87e2d-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="87e2d-117">選取 [VHD]。</span><span class="sxs-lookup"><span data-stu-id="87e2d-117">Select **VHD**.</span></span>

1. <span data-ttu-id="87e2d-118">從 hello **VHD**刀鋒視窗中，選取所需的 hello VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="87e2d-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="87e2d-119">選取**確定**tooclose hello **VHD**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87e2d-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="87e2d-120">選取 [作業系統組態]。</span><span class="sxs-lookup"><span data-stu-id="87e2d-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="87e2d-121">在 hello**作業系統組態**索引標籤上，選取  **Windows**或**Linux**。</span><span class="sxs-lookup"><span data-stu-id="87e2d-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="87e2d-122">如果**Windows**是透過 hello 核取方塊選取，指定是否*Sysprep*已經 hello 機器上執行。</span><span class="sxs-lookup"><span data-stu-id="87e2d-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="87e2d-123">選取**確定**tooclose hello**作業系統組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="87e2d-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="87e2d-124">選取**確定**toocreate hello 自訂映像。</span><span class="sxs-lookup"><span data-stu-id="87e2d-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="87e2d-125">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="87e2d-125">Related blog posts</span></span>

- [<span data-ttu-id="87e2d-126">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="87e2d-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="87e2d-127">在 Azure DevTest Labs 之間複製自訂映像</span><span class="sxs-lookup"><span data-stu-id="87e2d-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="87e2d-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87e2d-128">Next steps</span></span>

- [<span data-ttu-id="87e2d-129">新增 VM tooyour 實驗室</span><span class="sxs-lookup"><span data-stu-id="87e2d-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
