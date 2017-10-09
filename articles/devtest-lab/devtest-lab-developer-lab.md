---
title: "適用於開發人員的 Azure DevTest Labs aaaUse |Microsoft 文件"
description: "深入了解如何開發人員案例 toouse Azure DevTest Labs。"
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
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="343ee-103">使用適用於開發人員的 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="343ee-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="343ee-104">Azure 的 DevTest Labs 可使用的 tooimplement 許多案例中，但其中一個 hello 主要案例牽涉到使用適用於開發人員的 DevTest Labs toohost 開發電腦。</span><span class="sxs-lookup"><span data-stu-id="343ee-104">Azure DevTest Labs can be used tooimplement many key scenarios, but one of hello primary scenarios involves using DevTest Labs toohost development machines for developers.</span></span> <span data-ttu-id="343ee-105">在此案例中，DevTest Labs 提供以下優點：</span><span class="sxs-lookup"><span data-stu-id="343ee-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="343ee-106">開發人員可以快速視需要佈建開發電腦。</span><span class="sxs-lookup"><span data-stu-id="343ee-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="343ee-107">開發人員可以隨時輕鬆自訂他們的開發電腦。</span><span class="sxs-lookup"><span data-stu-id="343ee-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="343ee-108">系統管理員可以確定下列事項以控制成本：</span><span class="sxs-lookup"><span data-stu-id="343ee-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="343ee-109">開發人員無法取得超過開發所需的 VM。</span><span class="sxs-lookup"><span data-stu-id="343ee-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="343ee-110">VM 不使用時會關閉。</span><span class="sxs-lookup"><span data-stu-id="343ee-110">VMs are shut down when not in use.</span></span> 

![使用 DevTest Labs 進行訓練](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="343ee-112">在本文中，您會了解各種 Azure DevTest Labs 功能可使用的 toomeet 開發人員需求和 hello 詳細的步驟，您可以依照 tooset 實驗室設定。</span><span class="sxs-lookup"><span data-stu-id="343ee-112">In this article, you learn about various Azure DevTest Labs features that can be used toomeet developer requirements and hello detailed steps that you can follow tooset up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="343ee-113">實作使用 Azure DevTest Labs 的開發人員環境</span><span class="sxs-lookup"><span data-stu-id="343ee-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="343ee-114">**建立 hello 實驗室**</span><span class="sxs-lookup"><span data-stu-id="343ee-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="343ee-115">實驗室會 hello Azure DevTest Labs 中起點。</span><span class="sxs-lookup"><span data-stu-id="343ee-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="343ee-116">一旦您建立實驗室環境，您可以執行工作，例如新增使用者 （開發人員） toohello 實驗室、 設定原則 toocontrol 成本，定義可以快速，建立的 VM 映像等等。</span><span class="sxs-lookup"><span data-stu-id="343ee-116">Once you create a lab, you can perform tasks such as adding users (developers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="343ee-117">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-118">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-118">Task</span></span> | <span data-ttu-id="343ee-119">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-120">在 Azure 研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="343ee-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="343ee-121">了解如何在 Azure 中的 DevTest Labs 實驗室的 toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="343ee-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="343ee-122">**使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立 VM**</span><span class="sxs-lookup"><span data-stu-id="343ee-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="343ee-123">您可以在 hello Azure Marketplace 中挑選現成的映像，從各種不同的映像，並讓它們可在 hello 實驗室中。</span><span class="sxs-lookup"><span data-stu-id="343ee-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="343ee-124">如果 hello 現成的映像不符合您的需求，您可以建立自訂映像建立的實驗室使用現成的映像，從 Azure Marketplace，安裝所有的 hello 軟體，您需要和儲存 hello VM 做為 hello 實驗室中的自訂映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="343ee-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="343ee-125">如果您要使用自訂映像，請考慮使用映像原廠 toocreate，並將您的映像發佈。</span><span class="sxs-lookup"><span data-stu-id="343ee-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="343ee-126">映像處理站是設定即程式碼的解決方案，定期自動建置及散發已設定的映像。</span><span class="sxs-lookup"><span data-stu-id="343ee-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="343ee-127">此儲存 hello 所需時間 toomanually hello 與建立 VM 之後，請設定 hello 系統基底 OS。</span><span class="sxs-lookup"><span data-stu-id="343ee-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="343ee-128">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-129">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-129">Task</span></span> | <span data-ttu-id="343ee-130">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-131">設定 Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="343ee-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="343ee-132">了解如何白名單 Azure Marketplace 映像，讓選取範圍只有 hello 映像，您可以使用您想要在 hello 開發人員。</span><span class="sxs-lookup"><span data-stu-id="343ee-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello developers.</span></span>|
   | [<span data-ttu-id="343ee-133">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="343ee-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="343ee-134">建立自訂映像預先安裝，讓開發人員可以快速地建立使用 hello 自訂映像的 VM，您需要的 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="343ee-134">Create a custom image by pre-installing hello software you need so that developers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="343ee-135">了解映像處理站</span><span class="sxs-lookup"><span data-stu-id="343ee-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="343ee-136">觀看影片說明如何 tooset 並使用映像處理站。</span><span class="sxs-lookup"><span data-stu-id="343ee-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="343ee-137">**建立可供開發人員電腦重複使用的範本**</span><span class="sxs-lookup"><span data-stu-id="343ee-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="343ee-138">Azure DevTest Labs 中的公式是一份預設屬性值使用 toocreate VM。</span><span class="sxs-lookup"><span data-stu-id="343ee-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="343ee-139">您可以挑選的映像、 VM 大小 （結合 CPU 和 RAM） 和虛擬網路，hello 實驗室中建立公式。</span><span class="sxs-lookup"><span data-stu-id="343ee-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="343ee-140">每位開發人員可以看到 hello 實驗室中的 hello 公式，並使用 toocreate VM。</span><span class="sxs-lookup"><span data-stu-id="343ee-140">Each developer can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="343ee-141">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-142">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-142">Task</span></span> | <span data-ttu-id="343ee-143">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-144">管理 DevTest Labs 公式 toocreate Vm</span><span class="sxs-lookup"><span data-stu-id="343ee-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="343ee-145">了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。</span><span class="sxs-lookup"><span data-stu-id="343ee-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="343ee-146">**建立成品 tooenable 彈性 VM 自訂**</span><span class="sxs-lookup"><span data-stu-id="343ee-146">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="343ee-147">使用的 toodeploy 和成品佈建 VM 之後，設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="343ee-147">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="343ee-148">構件可以是：</span><span class="sxs-lookup"><span data-stu-id="343ee-148">Artifacts can be:</span></span>

   - <span data-ttu-id="343ee-149">您想 tooinstall 上 hello VM-例如代理程式、 Fiddler 及 Visual Studio 的工具。</span><span class="sxs-lookup"><span data-stu-id="343ee-149">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="343ee-150">您想在 hello VM-toorun，諸如複製儲存機制的動作。</span><span class="sxs-lookup"><span data-stu-id="343ee-150">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="343ee-151">您想 tootest 應用程式。</span><span class="sxs-lookup"><span data-stu-id="343ee-151">Applications that you want tootest.</span></span>

   <span data-ttu-id="343ee-152">許多構件為現成可用。</span><span class="sxs-lookup"><span data-stu-id="343ee-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="343ee-153">如果想要符合特定需求的更多自訂，您可以建立自己的自訂構件。</span><span class="sxs-lookup"><span data-stu-id="343ee-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="343ee-154">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-154">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-155">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-155">Task</span></span> | <span data-ttu-id="343ee-156">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-157">為您的 DevTest Labs VM 建立自訂的構件</span><span class="sxs-lookup"><span data-stu-id="343ee-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="343ee-158">在您的實驗室中建立您自己自訂的成品以利 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="343ee-158">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="343ee-159">在 Azure DevTest Labs 中加入 Git 儲存機制 toostore 自訂成品和使用的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="343ee-159">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="343ee-160">深入了解如何 toostore 您自己的私用 Git 儲存機制內的自訂成品。</span><span class="sxs-lookup"><span data-stu-id="343ee-160">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="343ee-161">**控制成本**</span><span class="sxs-lookup"><span data-stu-id="343ee-161">**Control costs**</span></span>
   
    <span data-ttu-id="343ee-162">Azure 的 DevTest Labs 可讓您 tooset 原則 hello 實驗室 toospecify hello 的數目上限可以在 hello 實驗室中的開發人員所建立的 Vm 中。</span><span class="sxs-lookup"><span data-stu-id="343ee-162">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a developer in hello lab.</span></span> 
   
    <span data-ttu-id="343ee-163">如果開發人員小組所擁有的工作排程一組，而且您想 toostop hello 一天的特定時間的所有 hello Vm，然後自動重新啟動它們 hello 遵循一天，您可以輕鬆地完成作業，設定自動關閉及自動啟動原則 hello 實驗室中。</span><span class="sxs-lookup"><span data-stu-id="343ee-163">If your developer team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="343ee-164">最後，應用程式開發完成時，您可以刪除所有 hello Vm 同時執行單一的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="343ee-164">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="343ee-165">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-165">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-166">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-166">Task</span></span> | <span data-ttu-id="343ee-167">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-168">定義實驗室原則</span><span class="sxs-lookup"><span data-stu-id="343ee-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="343ee-169">Hello 實驗室中設定原則來控制成本。</span><span class="sxs-lookup"><span data-stu-id="343ee-169">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="343ee-170">刪除所有 hello 實驗室 Vm 的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="343ee-170">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="343ee-171">開發完成時，請刪除所有在一個作業中的 hello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="343ee-171">Delete all hello labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="343ee-172">**新增虛擬網路 tooa VM**</span><span class="sxs-lookup"><span data-stu-id="343ee-172">**Add a virtual network tooa VM**</span></span> 
   
    <span data-ttu-id="343ee-173">每當建立一個實驗室時，DevTest Labs 就會建立新的虛擬網路 (VNET)。</span><span class="sxs-lookup"><span data-stu-id="343ee-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="343ee-174">如果您已設定您自己的 VNET – 例如，藉由使用 ExpressRoute 或站對站 VPN – 您可以加入此 VNET tooyour 實驗室虛擬網路設定，使其可建立 Vm 時。</span><span class="sxs-lookup"><span data-stu-id="343ee-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="343ee-175">此外，也沒有 Azure Active Directory 網域聯結成品可用，會將 VM tooa 網域聯結時正在建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="343ee-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="343ee-176">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-176">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-177">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-177">Task</span></span> | <span data-ttu-id="343ee-178">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-179">在 Azure DevTest Labs 中設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="343ee-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="343ee-180">了解如何 tooconfigure 虛擬網路中使用 Azure DevTest Labs hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="343ee-180">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="343ee-181">**與每個開發人員共用 hello 實驗室**</span><span class="sxs-lookup"><span data-stu-id="343ee-181">**Share hello lab with each developer**</span></span>
   
    <span data-ttu-id="343ee-182">使用您與開發人員共用的連結即可直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="343ee-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="343ee-183">即使沒有 toohave Azure 帳戶，因為它們已[Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account)。</span><span class="sxs-lookup"><span data-stu-id="343ee-183">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="343ee-184">開發人員看不到其他開發人員建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="343ee-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="343ee-185">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-186">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-186">Task</span></span> | <span data-ttu-id="343ee-187">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-188">在 Azure DevTest Labs 中新增的開發人員 tooa 實驗室</span><span class="sxs-lookup"><span data-stu-id="343ee-188">Add a developer tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="343ee-189">使用 hello Azure 入口網站 tooadd 開發人員 tooyour 實驗室。</span><span class="sxs-lookup"><span data-stu-id="343ee-189">Use hello Azure portal tooadd developers tooyour lab.</span></span>|
   | [<span data-ttu-id="343ee-190">加入使用 PowerShell 指令碼的開發人員 toohello 實驗室</span><span class="sxs-lookup"><span data-stu-id="343ee-190">Add developers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="343ee-191">使用 PowerShell tooautomate 加入開發人員 tooyour 實驗室。</span><span class="sxs-lookup"><span data-stu-id="343ee-191">Use PowerShell tooautomate adding developers tooyour lab.</span></span> |
   | [<span data-ttu-id="343ee-192">取得連結 toohello 實驗室</span><span class="sxs-lookup"><span data-stu-id="343ee-192">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="343ee-193">了解開發人員如何透過超連結直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="343ee-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="343ee-194">**為更多小組自動建立實驗室**</span><span class="sxs-lookup"><span data-stu-id="343ee-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="343ee-195">您可以自動化實驗室建立、 自訂的設定，包括建立資源管理員範本，並使用它 toocreate 相同實驗室次又一次。</span><span class="sxs-lookup"><span data-stu-id="343ee-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="343ee-196">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="343ee-196">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="343ee-197">Task</span><span class="sxs-lookup"><span data-stu-id="343ee-197">Task</span></span> | <span data-ttu-id="343ee-198">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="343ee-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="343ee-199">使用 Resource Manager 範本建立實驗室</span><span class="sxs-lookup"><span data-stu-id="343ee-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="343ee-200">在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="343ee-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

