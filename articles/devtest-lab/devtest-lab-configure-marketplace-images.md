---
title: "在 Azure DevTest Labs 中設定 Azure Marketplace 映像設定 | Microsoft Docs"
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
ms.openlocfilehash: 5f888c9d92a9164cc7d3d1aed66c29a724b365d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="73052-103">在 Azure DevTest Labs 中設定 Azure Marketplace 映像設定</span><span class="sxs-lookup"><span data-stu-id="73052-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="73052-104">DevTest Labs 支援根據 Azure Marketplace 映像來建立 VM，而這取決於您設定 Azure Marketplace 映像使用於實驗室的方式。</span><span class="sxs-lookup"><span data-stu-id="73052-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="73052-105">本文將說明在實驗室中建立 VM 時，如何指定可以使用哪些 Azure Marketplace 映像 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="73052-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="73052-106">這可確保您的小組只能存取他們所需的 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="73052-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="73052-107">選取在建立 VM 時允許使用哪些 Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="73052-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="73052-108">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="73052-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="73052-109">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="73052-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="73052-110">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="73052-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="73052-111">在實驗室的刀鋒視窗上，選取 [組態和原則]。</span><span class="sxs-lookup"><span data-stu-id="73052-111">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="73052-112">在實驗室的 [組態和原則] 刀鋒視窗的 [Virtual Machine Bases] \(虛擬機器基礎) 下，選取 [Marketplace 映像]。</span><span class="sxs-lookup"><span data-stu-id="73052-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="73052-113">指定是否要讓所有合格的 Azure Marketplace 映像可用來做為新 VM 的基底。</span><span class="sxs-lookup"><span data-stu-id="73052-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="73052-114">如果您選取 [是] ，則實驗室中允許所有符合下列準則的 Azure Marketplace 映像︰</span><span class="sxs-lookup"><span data-stu-id="73052-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="73052-115">映像會建立單一 VM， **而且**</span><span class="sxs-lookup"><span data-stu-id="73052-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="73052-116">映像會使用 Azure Resource Manager 來佈建 VM， **而且**</span><span class="sxs-lookup"><span data-stu-id="73052-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="73052-117">映像不需要購買額外的授權方案</span><span class="sxs-lookup"><span data-stu-id="73052-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="73052-118">如果您不想允許任何映像，或者想要指定可以使用哪些映像，請選取 [否] 。</span><span class="sxs-lookup"><span data-stu-id="73052-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![允許使用所有 Marketplace 映像做為 VM 基底映像的選項](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="73052-120">如果您在上一個步驟中選取 [否]，將會啟用 [允許的映像/全選] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="73052-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="73052-121">您可以將此選項與搜尋方塊一起使用，快速選取或取消選取清單中顯示的所有項目。</span><span class="sxs-lookup"><span data-stu-id="73052-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   * <span data-ttu-id="73052-122">藉由核取每個映像的對應核取方塊，個別選取您想要允許來建立 VM 的 Azure Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="73052-122">Select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="73052-123">如果您不想在實驗室中允許使用任何 Azure Marketplace 映像，請不要從清單中選取任何項目。</span><span class="sxs-lookup"><span data-stu-id="73052-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![您可以指定可使用哪些 Marketplace 映像做為 VM 的基底映像](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="73052-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73052-125">Next steps</span></span>
<span data-ttu-id="73052-126">一旦您設定在建立 VM 時允許使用 Azure Marketplace 映像的方式之後，下一個步驟就是 [將 VM 新增至您的實驗室](devtest-lab-add-vm-with-artifacts.md)。</span><span class="sxs-lookup"><span data-stu-id="73052-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

