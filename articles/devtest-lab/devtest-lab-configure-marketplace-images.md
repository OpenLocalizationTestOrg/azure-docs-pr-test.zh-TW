---
title: "在 Azure DevTest Labs aaaConfigure Azure Marketplace 映像設定 |Microsoft 文件"
description: "設定在 Azure DevTest Labs 中建立 VM 時可以使用哪些 Azure Marketplace 映像"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="810d3-103">在 Azure DevTest Labs 中設定 Azure Marketplace 映像設定</span><span class="sxs-lookup"><span data-stu-id="810d3-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="810d3-104">DevTest Labs 支援建立 Vm，視您如何設定您的實驗室中使用 Azure Marketplace 映像 toobe Azure Marketplace 映像為基礎。</span><span class="sxs-lookup"><span data-stu-id="810d3-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="810d3-105">本文章將示範如何 toospecify 它，如果有的話，可以是 Azure Marketplace 映像在實驗室中建立 Vm 時使用。</span><span class="sxs-lookup"><span data-stu-id="810d3-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="810d3-106">這可確保您的小組只具有所需的存取 toohello Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="810d3-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="810d3-107">選取在建立 VM 時允許使用哪些 Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="810d3-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="810d3-108">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="810d3-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="810d3-109">選取**更服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="810d3-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="810d3-110">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="810d3-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="810d3-111">在 hello 實驗室刀鋒視窗中，選取 **組態和原則**。</span><span class="sxs-lookup"><span data-stu-id="810d3-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="810d3-112">在實驗室的 [組態和原則] 刀鋒視窗的 [Virtual Machine Bases] \(虛擬機器基礎) 下，選取 [Marketplace 映像]。</span><span class="sxs-lookup"><span data-stu-id="810d3-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="810d3-113">指定您是否要在所有 hello 限定的 Azure Marketplace 映像 toobe 可供使用，做為基底的新 VM。</span><span class="sxs-lookup"><span data-stu-id="810d3-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="810d3-114">如果您選取**是**，然後所有 hello Azure Marketplace 映像的符合所有下列準則 hello 都允許 hello 實驗室中：</span><span class="sxs-lookup"><span data-stu-id="810d3-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="810d3-115">hello 映像建立之單一 VM，**和**</span><span class="sxs-lookup"><span data-stu-id="810d3-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="810d3-116">hello 映像會使用 Azure Resource Manager tooprovision Vm，**和**</span><span class="sxs-lookup"><span data-stu-id="810d3-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="810d3-117">hello 映像並不需要購買額外授權計劃</span><span class="sxs-lookup"><span data-stu-id="810d3-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="810d3-118">如果您想允許，沒有映像 toobe 或您想要的映像可用，請選取的 toospecify**否**。</span><span class="sxs-lookup"><span data-stu-id="810d3-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![選項 tooallow 所有 Marketplace 映像 toobe 都做為基底映像的 Vm](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="810d3-120">如果您選取**否**toohello 前一個步驟，hello**允許映像/選取所有**核取方塊會啟用。</span><span class="sxs-lookup"><span data-stu-id="810d3-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="810d3-121">您可以使用此選項，連同 hello 搜尋 tooquickly 中，選取或取消選取所有顯示在 [hello] 清單中的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="810d3-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="810d3-122">選取您想要 tooallow VM 建立個別選取每個映像的對應核取方塊的 hello Azure Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="810d3-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="810d3-123">執行任何動作從清單中選取 hello 如果您不想 tooallow hello 實驗室中使用任何 Azure Marketplace 映像 toobe。</span><span class="sxs-lookup"><span data-stu-id="810d3-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![您可以指定可使用哪些 Marketplace 映像做為 VM 的基底映像](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="810d3-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="810d3-125">Next steps</span></span>
<span data-ttu-id="810d3-126">一旦您已建立 VM 時，如何允許 Azure Marketplace 映像，hello 下一個步驟太[加入 VM tooyour 實驗室](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="810d3-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

