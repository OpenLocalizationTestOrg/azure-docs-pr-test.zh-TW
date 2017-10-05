---
title: "使用適用於開發人員的 Azure DevTest Labs | Microsoft Docs"
description: "了解如何使用適用於開發人員案例的 Azure DevTest Labs。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="feb44-103">使用適用於開發人員的 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="feb44-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="feb44-104">Azure DevTest Labs 可以用來實作許多重要案例，但是其中一個主要案例是使用 DevTest Labs 來託管開發人員的開發電腦。</span><span class="sxs-lookup"><span data-stu-id="feb44-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="feb44-105">在此案例中，DevTest Labs 提供以下優點：</span><span class="sxs-lookup"><span data-stu-id="feb44-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="feb44-106">開發人員可以快速視需要佈建開發電腦。</span><span class="sxs-lookup"><span data-stu-id="feb44-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="feb44-107">開發人員可以隨時輕鬆自訂他們的開發電腦。</span><span class="sxs-lookup"><span data-stu-id="feb44-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="feb44-108">系統管理員可以確定下列事項以控制成本：</span><span class="sxs-lookup"><span data-stu-id="feb44-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="feb44-109">開發人員無法取得超過開發所需的 VM。</span><span class="sxs-lookup"><span data-stu-id="feb44-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="feb44-110">VM 不使用時會關閉。</span><span class="sxs-lookup"><span data-stu-id="feb44-110">VMs are shut down when not in use.</span></span> 

![使用 DevTest Labs 進行訓練](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="feb44-112">在本文中，您會了解可用來符合開發人員需求的各種 Azure DevTest Labs 功能，以及可供遵循的實驗室詳細設定步驟。</span><span class="sxs-lookup"><span data-stu-id="feb44-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="feb44-113">實作使用 Azure DevTest Labs 的開發人員環境</span><span class="sxs-lookup"><span data-stu-id="feb44-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="feb44-114">**建立實驗室**</span><span class="sxs-lookup"><span data-stu-id="feb44-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="feb44-115">實驗室是 Azure DevTest Labs 的起點。</span><span class="sxs-lookup"><span data-stu-id="feb44-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="feb44-116">建立實驗室之後就可以執行各種工作，例如將使用者 (開發人員) 新增至實驗室、設定原則來控制成本，以及定義可以快速建立的 VM 映像等等。</span><span class="sxs-lookup"><span data-stu-id="feb44-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="feb44-117">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-118">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-118">Task</span></span> | <span data-ttu-id="feb44-119">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-120">在 Azure 研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="feb44-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="feb44-121">了解如何在 Azure 入口網站的 Azure DevTest Labs 中建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="feb44-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="feb44-122">**使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立 VM**</span><span class="sxs-lookup"><span data-stu-id="feb44-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="feb44-123">您可以從 Azure Marketplace 的各種映像中挑選現成的映像，供實驗室使用。</span><span class="sxs-lookup"><span data-stu-id="feb44-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="feb44-124">如果現成映像不符合您的需求，您可以透過使用 Azure Marketplace 中的現成映像建立實驗室 VM、安裝所需的所有軟體，並將該 VM 儲存為實驗室中的自訂映像，以建立自訂映像。</span><span class="sxs-lookup"><span data-stu-id="feb44-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="feb44-125">如果您要使用自訂映像，請考慮使用映像處理站建立和散發您的映像。</span><span class="sxs-lookup"><span data-stu-id="feb44-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="feb44-126">映像處理站是設定即程式碼的解決方案，定期自動建置及散發已設定的映像。</span><span class="sxs-lookup"><span data-stu-id="feb44-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="feb44-127">這可以在使用基礎作業系統建立 VM 之後，節省手動設定系統所需的時間。</span><span class="sxs-lookup"><span data-stu-id="feb44-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="feb44-128">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-129">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-129">Task</span></span> | <span data-ttu-id="feb44-130">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-131">設定 Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="feb44-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="feb44-132">了解如何將 Azure Marketplace 映像加入白名單；只讓您想要提供給開發人員使用的映像可供選取。</span><span class="sxs-lookup"><span data-stu-id="feb44-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="feb44-133">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="feb44-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="feb44-134">預先安裝所需軟體以建立自訂映像，讓開發人員可以使用自訂映像快速建立 VM。</span><span class="sxs-lookup"><span data-stu-id="feb44-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="feb44-135">了解映像處理站</span><span class="sxs-lookup"><span data-stu-id="feb44-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="feb44-136">觀看如何設定及使用映像處理站的說明影片。</span><span class="sxs-lookup"><span data-stu-id="feb44-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="feb44-137">**建立可供開發人員電腦重複使用的範本**</span><span class="sxs-lookup"><span data-stu-id="feb44-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="feb44-138">Azure DevTest Labs 中的公式是用來建立 VM 的預設屬性值清單。</span><span class="sxs-lookup"><span data-stu-id="feb44-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="feb44-139">您可以在實驗室中挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。</span><span class="sxs-lookup"><span data-stu-id="feb44-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="feb44-140">每位開發人員都能查看實驗室中的公式，並使用它來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="feb44-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="feb44-141">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-142">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-142">Task</span></span> | <span data-ttu-id="feb44-143">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-144">管理研發/測試實驗室公式來建立 VM</span><span class="sxs-lookup"><span data-stu-id="feb44-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="feb44-145">了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。</span><span class="sxs-lookup"><span data-stu-id="feb44-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="feb44-146">**建立構件以彈性自訂 VM**</span><span class="sxs-lookup"><span data-stu-id="feb44-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="feb44-147">構件是在佈建 VM 之後用來部署和設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="feb44-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="feb44-148">構件可以是：</span><span class="sxs-lookup"><span data-stu-id="feb44-148">Artifacts can be:</span></span>

   - <span data-ttu-id="feb44-149">您想要在 VM 上安裝的工具 - 例如，代理程式、Fiddler 及 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="feb44-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="feb44-150">您想要在 VM 上執行的動作 - 例如，複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="feb44-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="feb44-151">您想要測試的應用程式。</span><span class="sxs-lookup"><span data-stu-id="feb44-151">Applications that you want to test.</span></span>

   <span data-ttu-id="feb44-152">許多構件為現成可用。</span><span class="sxs-lookup"><span data-stu-id="feb44-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="feb44-153">如果想要符合特定需求的更多自訂，您可以建立自己的自訂構件。</span><span class="sxs-lookup"><span data-stu-id="feb44-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="feb44-154">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-155">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-155">Task</span></span> | <span data-ttu-id="feb44-156">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-157">為您的 DevTest Labs VM 建立自訂的構件</span><span class="sxs-lookup"><span data-stu-id="feb44-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="feb44-158">在實驗室中為虛擬機器建立自己的自訂構件。</span><span class="sxs-lookup"><span data-stu-id="feb44-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="feb44-159">在 Azure DevTest Labs 中新增可以存放自訂構件和 Azure Resource Manager 範本來使用的 Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="feb44-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="feb44-160">了解如何在您自己的私用 Git 儲存機制中儲存您的自訂構件。</span><span class="sxs-lookup"><span data-stu-id="feb44-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="feb44-161">**控制成本**</span><span class="sxs-lookup"><span data-stu-id="feb44-161">**Control costs**</span></span>
   
    <span data-ttu-id="feb44-162">Azure DevTest Labs 可讓您在實驗室中設定原則，以指定開發人員可在實驗室中建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="feb44-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="feb44-163">如果您的開發人員小組有既定的工作時程，而您想要在一天中的某個特定時間停止所有的 VM，然後在隔天自動重新啟動，只要設定實驗室自動關閉和自動啟動原則即可輕鬆達到目的。</span><span class="sxs-lookup"><span data-stu-id="feb44-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="feb44-164">最後，當應用程式開發完成時，您可以執行單一 PowerShell 指令碼一次刪除所有 VM。</span><span class="sxs-lookup"><span data-stu-id="feb44-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="feb44-165">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-166">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-166">Task</span></span> | <span data-ttu-id="feb44-167">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-168">定義實驗室原則</span><span class="sxs-lookup"><span data-stu-id="feb44-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="feb44-169">在實驗室中設定原則來控制成本。</span><span class="sxs-lookup"><span data-stu-id="feb44-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="feb44-170">使用 PowerShell 指令碼刪除所有實驗室 VM</span><span class="sxs-lookup"><span data-stu-id="feb44-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="feb44-171">當開發完成時，在一次作業中刪除所有實驗室。</span><span class="sxs-lookup"><span data-stu-id="feb44-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="feb44-172">**將虛擬網路新增至 VM**</span><span class="sxs-lookup"><span data-stu-id="feb44-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="feb44-173">每當建立一個實驗室時，DevTest Labs 就會建立新的虛擬網路 (VNET)。</span><span class="sxs-lookup"><span data-stu-id="feb44-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="feb44-174">如果您已設定自己的 VNET – 例如，使用 ExpressRoute 或站對站 VPN – 您可以將此 VNET 新增至實驗室的虛擬網路設定，以便在建立 VM 時使用。</span><span class="sxs-lookup"><span data-stu-id="feb44-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="feb44-175">此外，還有 Azure Active Directory 網域聯結構件可用，它會在建立 VM 時將 VM 加入網域。</span><span class="sxs-lookup"><span data-stu-id="feb44-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="feb44-176">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-177">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-177">Task</span></span> | <span data-ttu-id="feb44-178">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-179">在 Azure DevTest Labs 中設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="feb44-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="feb44-180">了解如何使用 Azure 入口網站在 Azure DevTest Labs 中設定虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="feb44-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="feb44-181">**與每位開發人員共用實驗室**</span><span class="sxs-lookup"><span data-stu-id="feb44-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="feb44-182">使用您與開發人員共用的連結即可直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="feb44-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="feb44-183">他們甚至不必有 Azure 帳戶，只要有 [Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account) 即可。</span><span class="sxs-lookup"><span data-stu-id="feb44-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="feb44-184">開發人員看不到其他開發人員建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="feb44-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="feb44-185">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-186">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-186">Task</span></span> | <span data-ttu-id="feb44-187">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-188">在 Azure DevTest Labs 中將開發人員新增至實驗室</span><span class="sxs-lookup"><span data-stu-id="feb44-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="feb44-189">使用 Azure 入口網站將開發人員新增至實驗室。</span><span class="sxs-lookup"><span data-stu-id="feb44-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="feb44-190">使用 PowerShell 指令碼將開發人員新增至實驗室</span><span class="sxs-lookup"><span data-stu-id="feb44-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="feb44-191">使用 PowerShell 自動將開發人員新增到實驗室。</span><span class="sxs-lookup"><span data-stu-id="feb44-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="feb44-192">取得實驗室連結</span><span class="sxs-lookup"><span data-stu-id="feb44-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="feb44-193">了解開發人員如何透過超連結直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="feb44-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="feb44-194">**為更多小組自動建立實驗室**</span><span class="sxs-lookup"><span data-stu-id="feb44-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="feb44-195">您可以建立 Resource Manager 範本並一再使用它來建立相同的實驗室，以自動建立實驗室，包括自訂設定。</span><span class="sxs-lookup"><span data-stu-id="feb44-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="feb44-196">按一下下表中的連結以便深入了解︰</span><span class="sxs-lookup"><span data-stu-id="feb44-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="feb44-197">工作</span><span class="sxs-lookup"><span data-stu-id="feb44-197">Task</span></span> | <span data-ttu-id="feb44-198">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="feb44-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="feb44-199">使用 Resource Manager 範本建立實驗室</span><span class="sxs-lookup"><span data-stu-id="feb44-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="feb44-200">在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="feb44-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

