---
title: "使用 Azure DevTest Labs 進行訓練 | Microsoft Docs"
description: "了解如何針對訓練案例使用 Azure DevTest Labs。"
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
ms.openlocfilehash: a85999b7963e9a07d3f91ec47f298f91439c0808
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="ce7c5-103">使用 Azure DevTest Labs 進行訓練</span><span class="sxs-lookup"><span data-stu-id="ce7c5-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="ce7c5-104">除了進行開發/測試，Azure DevTest Labs 還可用來實作許多重要案例。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-104">Azure DevTest Labs can be used to implement many key scenarios in addition to dev/test.</span></span> <span data-ttu-id="ce7c5-105">這些案例的其中之一便是設置訓練實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-105">One of those scenarios is to set up a lab for training.</span></span> <span data-ttu-id="ce7c5-106">Azure DevTest Labs 可讓您建立實驗室，在其中提供自訂範本供每位受訓者建立相同且隔離的訓練環境。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-106">Azure DevTest Labs allows you to create a lab where you can provide custom templates that each trainee can use to create identical and isolated environments for training.</span></span> <span data-ttu-id="ce7c5-107">您可以新增原則，以確保訓練環境只會在受訓者需要時才提供給他們使用，且包含足夠的訓練所需資源，例如虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-107">You can apply policies to ensure that training environments are available to each trainee only when they need them and contain enough resources - such as virtual machines - required for the training.</span></span> <span data-ttu-id="ce7c5-108">最後，您可以輕易地與受訓者共用實驗室，讓他們只要按一下就能存取。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-108">Finally, you can easily share the lab with trainees, which they can access in one click.</span></span>

![使用 DevTest Labs 進行訓練](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="ce7c5-110">Azure DevTest Labs 符合下列在任何虛擬環境進行訓練所必須具備的需求︰</span><span class="sxs-lookup"><span data-stu-id="ce7c5-110">Azure DevTest Labs meets the following requirements that are required to conduct training in any virtual environment:</span></span> 

* <span data-ttu-id="ce7c5-111">受訓者無法看到其他受訓者所建立的 VM</span><span class="sxs-lookup"><span data-stu-id="ce7c5-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="ce7c5-112">每台訓練用機器應該相同</span><span class="sxs-lookup"><span data-stu-id="ce7c5-112">Every training machine should be identical</span></span>
* <span data-ttu-id="ce7c5-113">受訓者可以快速佈建其訓練環境</span><span class="sxs-lookup"><span data-stu-id="ce7c5-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="ce7c5-114">確保受訓者無法取得超過訓練所需數量的 VM 以控制成本，並在受訓者不使用 VM 時將其關閉</span><span class="sxs-lookup"><span data-stu-id="ce7c5-114">Control cost by ensuring that trainees cannot get more VMs than they need for the training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="ce7c5-115">輕易地與每位受訓者共用訓練實驗室</span><span class="sxs-lookup"><span data-stu-id="ce7c5-115">Easily share the training lab with each trainee</span></span>
* <span data-ttu-id="ce7c5-116">一再重複使用訓練實驗室</span><span class="sxs-lookup"><span data-stu-id="ce7c5-116">Reuse the training lab again and again</span></span>

<span data-ttu-id="ce7c5-117">在本文中，您會了解可用來符合先前所述訓練需求的各種 Azure DevTest Labs 功能，以及可供遵循的訓練實驗室詳細設定步驟。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-117">In this article, you learn about various Azure DevTest Labs features that can be used to meet the previously described training requirements and detailed steps that you can follow to set up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="ce7c5-118">使用 Azure DevTest Labs 實作訓練</span><span class="sxs-lookup"><span data-stu-id="ce7c5-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="ce7c5-119">**建立實驗室**</span><span class="sxs-lookup"><span data-stu-id="ce7c5-119">**Create the lab**</span></span> 
   
    <span data-ttu-id="ce7c5-120">實驗室是 Azure DevTest Labs 的起點。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-120">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="ce7c5-121">建立實驗室之後就可以執行各種工作，例如新增使用者 (受訓者) 至實驗室、設定原則來控制成本，以及定義可以快速建立的 VM 映像等。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-121">Once you create a lab, you can perform tasks such as add users (trainees) to the lab, set policies to control costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="ce7c5-122">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="ce7c5-122">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ce7c5-123">工作</span><span class="sxs-lookup"><span data-stu-id="ce7c5-123">Task</span></span> | <span data-ttu-id="ce7c5-124">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="ce7c5-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ce7c5-125">在 Azure 研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="ce7c5-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="ce7c5-126">了解如何在 Azure 入口網站的 Azure DevTest Labs 中建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-126">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="ce7c5-127">**使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立訓練 VM**</span><span class="sxs-lookup"><span data-stu-id="ce7c5-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="ce7c5-128">您可以從 Azure Marketplace 的各種映像中挑選現成的映像，並在實驗室中提供給受訓者使用。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-128">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available for the trainees in the lab.</span></span> <span data-ttu-id="ce7c5-129">如果現成映像不符合您的需求，您可以透過使用 Azure Marketplace 中的現成映像建立實驗室 VM、安裝訓練所需的所有軟體，並將該 VM 儲存為實驗室中的自訂映像，以建立自訂映像。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-129">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need for the training, and saving the VM as custom image in the lab.</span></span> 
   
    <span data-ttu-id="ce7c5-130">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="ce7c5-130">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ce7c5-131">工作</span><span class="sxs-lookup"><span data-stu-id="ce7c5-131">Task</span></span> | <span data-ttu-id="ce7c5-132">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="ce7c5-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ce7c5-133">設定 Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="ce7c5-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="ce7c5-134">了解如何將 Azure Marketplace 映像加入白名單；只讓想要用於進行訓練的映像可供選取。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-134">Learn how you can whitelist Azure Marketplace images; making available for selection only the images you want for the training.</span></span> |
   | [<span data-ttu-id="ce7c5-135">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="ce7c5-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="ce7c5-136">預先安裝訓練所需軟體以建立自訂映像，讓受訓者可以使用自訂映像快速建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-136">Create a custom image by pre-installing the software you need for the training so that trainees can quickly create a VM using the custom image.</span></span> |
3. <span data-ttu-id="ce7c5-137">**建立可重複用於訓練機器的範本**</span><span class="sxs-lookup"><span data-stu-id="ce7c5-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="ce7c5-138">Azure DevTest Labs 中的公式是用來建立 VM 的預設屬性值清單。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="ce7c5-139">您可以在實驗室中挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="ce7c5-140">每位受訓者都能查看實驗室中的公式，並使用它來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-140">Each trainee can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="ce7c5-141">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="ce7c5-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ce7c5-142">工作</span><span class="sxs-lookup"><span data-stu-id="ce7c5-142">Task</span></span> | <span data-ttu-id="ce7c5-143">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="ce7c5-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ce7c5-144">管理研發/測試實驗室公式來建立 VM</span><span class="sxs-lookup"><span data-stu-id="ce7c5-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="ce7c5-145">了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="ce7c5-146">**控制成本**</span><span class="sxs-lookup"><span data-stu-id="ce7c5-146">**Control costs**</span></span>
   
    <span data-ttu-id="ce7c5-147">Azure DevTest Labs 可讓您在實驗室中設定原則，以指定受訓者可在實驗室中建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-147">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a trainee in the lab.</span></span> 
   
    <span data-ttu-id="ce7c5-148">如果您在進行為期數天的訓練，並且想要在一天當中的特定時間停止所有 VM，然後在隔天自動重新啟動，您可以藉由設定實驗室中的自動關閉和自動啟動原則來輕鬆達到該目的。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-148">If you are conducting multi-day training and want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="ce7c5-149">最後，當訓練完成時，您可以執行單一 PowerShell 指令碼一次刪除所有 VM。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-149">Finally, when training is complete you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="ce7c5-150">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="ce7c5-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ce7c5-151">工作</span><span class="sxs-lookup"><span data-stu-id="ce7c5-151">Task</span></span> | <span data-ttu-id="ce7c5-152">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="ce7c5-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ce7c5-153">定義實驗室原則</span><span class="sxs-lookup"><span data-stu-id="ce7c5-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="ce7c5-154">在實驗室中設定原則來控制成本。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-154">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="ce7c5-155">使用 PowerShell 指令碼刪除所有實驗室 VM</span><span class="sxs-lookup"><span data-stu-id="ce7c5-155">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="ce7c5-156">當訓練完成時，在一次作業中刪除所有實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-156">Delete all the labs in one operation when the training is complete.</span></span> |
5. <span data-ttu-id="ce7c5-157">**與每位受訓者共用實驗室**</span><span class="sxs-lookup"><span data-stu-id="ce7c5-157">**Share the lab with each trainee**</span></span>
   
    <span data-ttu-id="ce7c5-158">使用您分享給受訓者的連結即可直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="ce7c5-159">受訓者甚至不必有 Azure 帳戶，只要他們擁有 [Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account)。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-159">Your trainees don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="ce7c5-160">受訓者無法看到其他受訓者所建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="ce7c5-161">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="ce7c5-161">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ce7c5-162">工作</span><span class="sxs-lookup"><span data-stu-id="ce7c5-162">Task</span></span> | <span data-ttu-id="ce7c5-163">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="ce7c5-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ce7c5-164">在 Azure DevTest Labs 中新增受訓者到實驗室</span><span class="sxs-lookup"><span data-stu-id="ce7c5-164">Add a trainee to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="ce7c5-165">使用 Azure 入口網站將受訓者新增到訓練實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-165">Use the Azure portal to add trainees to your training lab.</span></span> |
   | [<span data-ttu-id="ce7c5-166">使用 PowerShell 指令碼新增受訓者到實驗室</span><span class="sxs-lookup"><span data-stu-id="ce7c5-166">Add trainees to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="ce7c5-167">使用 PowerShell 自動將受訓者新增到訓練實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-167">Use PowerShell to automate adding trainees to your training lab.</span></span> |
   | [<span data-ttu-id="ce7c5-168">取得實驗室連結</span><span class="sxs-lookup"><span data-stu-id="ce7c5-168">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="ce7c5-169">了解如何透過超連結直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="ce7c5-170">**一再重複使用實驗室**</span><span class="sxs-lookup"><span data-stu-id="ce7c5-170">**Reuse the lab again and again**</span></span> 
   
    <span data-ttu-id="ce7c5-171">您可以建立 Resource Manager 範本並一再使用它來建立相同的實驗室，以自動建立實驗室，包括自訂設定。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="ce7c5-172">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="ce7c5-172">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ce7c5-173">工作</span><span class="sxs-lookup"><span data-stu-id="ce7c5-173">Task</span></span> | <span data-ttu-id="ce7c5-174">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="ce7c5-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ce7c5-175">使用 Resource Manager 範本建立實驗室</span><span class="sxs-lookup"><span data-stu-id="ce7c5-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="ce7c5-176">在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="ce7c5-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

