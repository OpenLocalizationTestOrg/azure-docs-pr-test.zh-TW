---
title: "定型 aaaUse Azure DevTest Labs |Microsoft 文件"
description: "深入了解如何 toouse Azure DevTest Labs 定型案例。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: 4a5f44a282d8f6a58849c730ff89237ccff39ca8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="1d9e9-103">使用 Azure DevTest Labs 進行訓練</span><span class="sxs-lookup"><span data-stu-id="1d9e9-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="1d9e9-104">Azure 的 DevTest Labs 可使用的 tooimplement 加法 toodev/測試中的許多重要案例。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-104">Azure DevTest Labs can be used tooimplement many key scenarios in addition toodev/test.</span></span> <span data-ttu-id="1d9e9-105">這些案例的其中一個是 tooset 用於定型的實驗室設定。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-105">One of those scenarios is tooset up a lab for training.</span></span> <span data-ttu-id="1d9e9-106">Azure 的 DevTest Labs 可讓您 toocreate 實驗室，您可以提供自訂範本位置每個實習生，可以使用 toocreate 相同和隔離的環境進行定型。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-106">Azure DevTest Labs allows you toocreate a lab where you can provide custom templates that each trainee can use toocreate identical and isolated environments for training.</span></span> <span data-ttu-id="1d9e9-107">您可以套用它們需要的時候，且包含足夠的資源-例如虛擬機器-hello 定型所需時，只有訓練環境，都是可用 tooeach 實習生原則 tooensure。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-107">You can apply policies tooensure that training environments are available tooeach trainee only when they need them and contain enough resources - such as virtual machines - required for hello training.</span></span> <span data-ttu-id="1d9e9-108">最後，您可以輕鬆地分享 hello 實驗室受訓，他們可以存取單鍵人員。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-108">Finally, you can easily share hello lab with trainees, which they can access in one click.</span></span>

![使用 DevTest Labs 進行訓練](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="1d9e9-110">Azure 的 DevTest Labs 符合下列需求的任何虛擬環境中的必要的 tooconduct 訓練 hello:</span><span class="sxs-lookup"><span data-stu-id="1d9e9-110">Azure DevTest Labs meets hello following requirements that are required tooconduct training in any virtual environment:</span></span> 

* <span data-ttu-id="1d9e9-111">受訓者無法看到其他受訓者所建立的 VM</span><span class="sxs-lookup"><span data-stu-id="1d9e9-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="1d9e9-112">每台訓練用機器應該相同</span><span class="sxs-lookup"><span data-stu-id="1d9e9-112">Every training machine should be identical</span></span>
* <span data-ttu-id="1d9e9-113">受訓者可以快速佈建其訓練環境</span><span class="sxs-lookup"><span data-stu-id="1d9e9-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="1d9e9-114">控制成本，方法是確保受訓人員無法取得更多的 Vm，比在不使用它們時需要 hello 定型以及關閉 Vm</span><span class="sxs-lookup"><span data-stu-id="1d9e9-114">Control cost by ensuring that trainees cannot get more VMs than they need for hello training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="1d9e9-115">輕鬆地共用每個實習生 hello 訓練實驗室</span><span class="sxs-lookup"><span data-stu-id="1d9e9-115">Easily share hello training lab with each trainee</span></span>
* <span data-ttu-id="1d9e9-116">一再重複使用 hello 訓練實驗室</span><span class="sxs-lookup"><span data-stu-id="1d9e9-116">Reuse hello training lab again and again</span></span>

<span data-ttu-id="1d9e9-117">在本文中，您了解可用的各種 Azure DevTest Labs 功能 toomeet hello 先前所述的訓練需求和詳細的步驟，您可以依照 tooset 用於定型的實驗室設定。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-117">In this article, you learn about various Azure DevTest Labs features that can be used toomeet hello previously described training requirements and detailed steps that you can follow tooset up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="1d9e9-118">使用 Azure DevTest Labs 實作訓練</span><span class="sxs-lookup"><span data-stu-id="1d9e9-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="1d9e9-119">**建立 hello 實驗室**</span><span class="sxs-lookup"><span data-stu-id="1d9e9-119">**Create hello lab**</span></span> 
   
    <span data-ttu-id="1d9e9-120">實驗室會 hello Azure DevTest Labs 中起點。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-120">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="1d9e9-121">一旦您建立實驗室環境，您可以執行的工作，例如當新增使用者 （受訓人員） toohello 實驗室中，設定原則 toocontrol 成本，定義可以快速，建立的 VM 映像等等。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-121">Once you create a lab, you can perform tasks such as add users (trainees) toohello lab, set policies toocontrol costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="1d9e9-122">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="1d9e9-122">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="1d9e9-123">Task</span><span class="sxs-lookup"><span data-stu-id="1d9e9-123">Task</span></span> | <span data-ttu-id="1d9e9-124">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1d9e9-125">在 Azure 研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="1d9e9-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="1d9e9-126">了解如何在 Azure 中的 DevTest Labs 實驗室的 toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-126">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="1d9e9-127">**使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立訓練 VM**</span><span class="sxs-lookup"><span data-stu-id="1d9e9-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="1d9e9-128">您可以在 hello Azure Marketplace 中挑選現成的映像，從各種不同的映像，並讓它們的 hello 實驗室中的 hello 受訓人員可使用。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-128">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available for hello trainees in hello lab.</span></span> <span data-ttu-id="1d9e9-129">如果 hello 現成的映像不符合您的需求，您可以建立自訂映像建立的實驗室使用 Azure marketplace，安裝所有您需要進行 hello 訓練和儲存 hello VM 做為自訂映像 hello 實驗室中的 hello 軟體現成的映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-129">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need for hello training, and saving hello VM as custom image in hello lab.</span></span> 
   
    <span data-ttu-id="1d9e9-130">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="1d9e9-130">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="1d9e9-131">Task</span><span class="sxs-lookup"><span data-stu-id="1d9e9-131">Task</span></span> | <span data-ttu-id="1d9e9-132">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1d9e9-133">設定 Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="1d9e9-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="1d9e9-134">了解如何白名單 Azure Marketplace 映像。您想要的 hello 訓練供只有 hello 映像選取項目。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-134">Learn how you can whitelist Azure Marketplace images; making available for selection only hello images you want for hello training.</span></span> |
   | [<span data-ttu-id="1d9e9-135">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="1d9e9-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="1d9e9-136">建立自訂映像預先安裝，讓受訓人員可以快速地建立使用 hello 自訂映像的 VM，您需要 hello 定型 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-136">Create a custom image by pre-installing hello software you need for hello training so that trainees can quickly create a VM using hello custom image.</span></span> |
3. <span data-ttu-id="1d9e9-137">**建立可重複用於訓練機器的範本**</span><span class="sxs-lookup"><span data-stu-id="1d9e9-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="1d9e9-138">Azure DevTest Labs 中的公式是一份預設屬性值使用 toocreate VM。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="1d9e9-139">您可以挑選的映像、 VM 大小 （結合 CPU 和 RAM） 和虛擬網路，hello 實驗室中建立公式。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="1d9e9-140">每個實習生可以看到 hello 實驗室中的 hello 公式，並使用 toocreate VM。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-140">Each trainee can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="1d9e9-141">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="1d9e9-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="1d9e9-142">Task</span><span class="sxs-lookup"><span data-stu-id="1d9e9-142">Task</span></span> | <span data-ttu-id="1d9e9-143">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1d9e9-144">管理 DevTest Labs 公式 toocreate Vm</span><span class="sxs-lookup"><span data-stu-id="1d9e9-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="1d9e9-145">了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="1d9e9-146">**控制成本**</span><span class="sxs-lookup"><span data-stu-id="1d9e9-146">**Control costs**</span></span>
   
    <span data-ttu-id="1d9e9-147">Azure 的 DevTest Labs 可讓您 tooset 原則 hello 實驗室 toospecify hello 的數目上限可由實習生 hello 實驗室中建立的 Vm 中。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-147">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a trainee in hello lab.</span></span> 
   
    <span data-ttu-id="1d9e9-148">如果您進行多日訓練和 hello 一天的特定時間想 toostop hello 的所有 Vm，然後自動重新啟動後一天的 hello 可以輕鬆地完成該作業所設定的自動關閉並自動啟動 hello 實驗室中的原則。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-148">If you are conducting multi-day training and want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="1d9e9-149">最後，完成訓練時您可以刪除所有 hello Vm 同時執行單一的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-149">Finally, when training is complete you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="1d9e9-150">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="1d9e9-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="1d9e9-151">Task</span><span class="sxs-lookup"><span data-stu-id="1d9e9-151">Task</span></span> | <span data-ttu-id="1d9e9-152">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1d9e9-153">定義實驗室原則</span><span class="sxs-lookup"><span data-stu-id="1d9e9-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="1d9e9-154">Hello 實驗室中設定原則來控制成本。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-154">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="1d9e9-155">刪除所有 hello 實驗室 Vm 的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-155">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="1d9e9-156">Hello 訓練完成時，請刪除所有在一個作業中的 hello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-156">Delete all hello labs in one operation when hello training is complete.</span></span> |
5. <span data-ttu-id="1d9e9-157">**與每個實習生共用 hello 實驗室**</span><span class="sxs-lookup"><span data-stu-id="1d9e9-157">**Share hello lab with each trainee**</span></span>
   
    <span data-ttu-id="1d9e9-158">使用您分享給受訓者的連結即可直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="1d9e9-159">您受訓人員甚至沒有 toohave Azure 帳戶，因為它們已[Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account)。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-159">Your trainees don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="1d9e9-160">受訓者無法看到其他受訓者所建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="1d9e9-161">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="1d9e9-161">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="1d9e9-162">Task</span><span class="sxs-lookup"><span data-stu-id="1d9e9-162">Task</span></span> | <span data-ttu-id="1d9e9-163">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1d9e9-164">在 Azure DevTest Labs 中加入實習生 tooa 實驗室</span><span class="sxs-lookup"><span data-stu-id="1d9e9-164">Add a trainee tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="1d9e9-165">使用 hello Azure 入口網站 tooadd 受訓人員 tooyour 訓練實驗室。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-165">Use hello Azure portal tooadd trainees tooyour training lab.</span></span> |
   | [<span data-ttu-id="1d9e9-166">新增受訓人員 toohello 實驗室使用的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-166">Add trainees toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="1d9e9-167">使用 PowerShell tooautomate 加入受訓人員 tooyour 訓練實驗室。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-167">Use PowerShell tooautomate adding trainees tooyour training lab.</span></span> |
   | [<span data-ttu-id="1d9e9-168">取得連結 toohello 實驗室</span><span class="sxs-lookup"><span data-stu-id="1d9e9-168">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="1d9e9-169">了解如何透過超連結直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="1d9e9-170">**一再重複使用 hello 實驗室**</span><span class="sxs-lookup"><span data-stu-id="1d9e9-170">**Reuse hello lab again and again**</span></span> 
   
    <span data-ttu-id="1d9e9-171">您可以自動化實驗室建立、 自訂的設定，包括建立資源管理員範本，並使用它 toocreate 相同實驗室次又一次。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="1d9e9-172">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="1d9e9-172">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="1d9e9-173">Task</span><span class="sxs-lookup"><span data-stu-id="1d9e9-173">Task</span></span> | <span data-ttu-id="1d9e9-174">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="1d9e9-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1d9e9-175">使用 Resource Manager 範本建立實驗室</span><span class="sxs-lookup"><span data-stu-id="1d9e9-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="1d9e9-176">在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="1d9e9-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

