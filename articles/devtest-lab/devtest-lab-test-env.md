---
title: "VM 和 PaaS aaaUse Azure DevTest Labs 測試環境 |Microsoft 文件"
description: "了解如何 toouse Azure DevTest Labs VM 和 PaaS 測試環境的案例。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="077c2-103">為 VM 和 PaaS 測試環境使用 Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="077c2-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="077c2-104">您可以使用 Azure DevTest Labs tooimplement 許多案例中，但主要案例牽涉到使用測試人員適用的 DevTest Labs toohost 機器。</span><span class="sxs-lookup"><span data-stu-id="077c2-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="077c2-105">在此案例中，DevTest Labs 提供以下優點：</span><span class="sxs-lookup"><span data-stu-id="077c2-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="077c2-106">測試人員可以快速佈建 Windows 和 Linux 的環境，使用可重複使用的範本和成品來測試其應用程式的 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="077c2-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="077c2-107">測試人員可以佈建多個測試代理程式，相應增加其負載測試。</span><span class="sxs-lookup"><span data-stu-id="077c2-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="077c2-108">系統管理員可以確定下列事項以控制成本：</span><span class="sxs-lookup"><span data-stu-id="077c2-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="077c2-109">測試人員無法取得超過所需的 VM。</span><span class="sxs-lookup"><span data-stu-id="077c2-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="077c2-110">VM 不使用時會關閉。</span><span class="sxs-lookup"><span data-stu-id="077c2-110">VMs are shut down when not in use.</span></span>

![使用 DevTest Labs 進行訓練](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="077c2-112">在本文中，您會了解各種 Azure DevTest Labs 所使用的功能 toomeet tester 需求，然後 hello 實驗室設定的詳細的步驟 toofollow tooset。</span><span class="sxs-lookup"><span data-stu-id="077c2-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="077c2-113">實作使用 Azure DevTest Labs 的測試環境</span><span class="sxs-lookup"><span data-stu-id="077c2-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="077c2-114">**建立 hello 實驗室**</span><span class="sxs-lookup"><span data-stu-id="077c2-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="077c2-115">實驗室會 hello Azure DevTest Labs 中起點。</span><span class="sxs-lookup"><span data-stu-id="077c2-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="077c2-116">一旦您建立實驗室環境，您可以執行工作，例如新增使用者 （測試人員） toohello 實驗室、 設定原則 toocontrol 成本，定義可以快速，建立的 VM 映像等等。</span><span class="sxs-lookup"><span data-stu-id="077c2-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="077c2-117">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-118">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-118">Task</span></span> | <span data-ttu-id="077c2-119">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-120">在 Azure 研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="077c2-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="077c2-121">了解如何在 Azure 中的 DevTest Labs 實驗室的 toocreate hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="077c2-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="077c2-122">**使用現成的 Marketplace 映像和自訂映像在幾分鐘內建立 VM**</span><span class="sxs-lookup"><span data-stu-id="077c2-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="077c2-123">您可以在 hello Azure Marketplace 中挑選現成的映像，從各種不同的映像，並讓它們可在 hello 實驗室中。</span><span class="sxs-lookup"><span data-stu-id="077c2-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="077c2-124">如果 hello 現成的映像不符合您的需求，您可以建立自訂映像建立的實驗室使用現成的映像，從 Azure Marketplace，安裝所有的 hello 軟體，您需要和儲存 hello VM 做為 hello 實驗室中的自訂映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="077c2-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="077c2-125">如果您要使用自訂映像，請考慮使用映像原廠 toocreate，並將您的映像發佈。</span><span class="sxs-lookup"><span data-stu-id="077c2-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="077c2-126">映像處理站是設定即程式碼的解決方案，定期自動建置及散發已設定的映像。</span><span class="sxs-lookup"><span data-stu-id="077c2-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="077c2-127">此儲存 hello 所需時間 toomanually hello 與建立 VM 之後，請設定 hello 系統基底 OS。</span><span class="sxs-lookup"><span data-stu-id="077c2-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="077c2-128">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-129">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-129">Task</span></span> | <span data-ttu-id="077c2-130">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-131">設定 Azure Marketplace 映像</span><span class="sxs-lookup"><span data-stu-id="077c2-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="077c2-132">了解如何白名單 Azure Marketplace 映像，讓選取範圍只有 hello 映像，您可以使用您想要在 hello 測試人員。</span><span class="sxs-lookup"><span data-stu-id="077c2-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="077c2-133">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="077c2-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="077c2-134">建立自訂映像預先安裝，讓測試人員可以快速地建立使用 hello 自訂映像的 VM，您需要的 hello 軟體。</span><span class="sxs-lookup"><span data-stu-id="077c2-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="077c2-135">了解映像處理站</span><span class="sxs-lookup"><span data-stu-id="077c2-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="077c2-136">觀看影片說明如何 tooset 並使用映像處理站。</span><span class="sxs-lookup"><span data-stu-id="077c2-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="077c2-137">**建立測試電腦可重複使用的範本**</span><span class="sxs-lookup"><span data-stu-id="077c2-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="077c2-138">Azure DevTest Labs 中的公式是一份預設屬性值使用 toocreate VM。</span><span class="sxs-lookup"><span data-stu-id="077c2-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="077c2-139">您可以挑選的映像、 VM 大小 （結合 CPU 和 RAM） 和虛擬網路，hello 實驗室中建立公式。</span><span class="sxs-lookup"><span data-stu-id="077c2-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="077c2-140">每個測試人員可以看到 hello 實驗室中的 hello 公式，並使用 toocreate VM。</span><span class="sxs-lookup"><span data-stu-id="077c2-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="077c2-141">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-142">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-142">Task</span></span> | <span data-ttu-id="077c2-143">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-144">管理 DevTest Labs 公式 toocreate Vm</span><span class="sxs-lookup"><span data-stu-id="077c2-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="077c2-145">了解如何挑選映像、VM 大小 (CPU 和 RAM 的組合) 和虛擬網路以建立公式。</span><span class="sxs-lookup"><span data-stu-id="077c2-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="077c2-146">**建立多部 VM 的測試環境**</span><span class="sxs-lookup"><span data-stu-id="077c2-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="077c2-147">您可以使用 Azure Resource Manager 範本 toodefine hello 基礎結構和 Azure 方案的組態，並重複地部署多個測試 Vm 處於一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="077c2-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="077c2-148">Azure PaaS 資源可以佈建在 Resource Manager 範本環境中，並以成本追蹤顯示。</span><span class="sxs-lookup"><span data-stu-id="077c2-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="077c2-149">不過，VM 自動關機不適用 tooPaaS 資源。</span><span class="sxs-lookup"><span data-stu-id="077c2-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="077c2-150">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-151">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-151">Task</span></span> | <span data-ttu-id="077c2-152">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-153">透過 Azure Resource Manager 範本建立多個 VM 環境和 PaaS 資源</span><span class="sxs-lookup"><span data-stu-id="077c2-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="077c2-154">了解如何以一致的狀態為測試環境部署多部 VM。</span><span class="sxs-lookup"><span data-stu-id="077c2-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="077c2-155">**建立成品 tooenable 彈性 VM 自訂**</span><span class="sxs-lookup"><span data-stu-id="077c2-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="077c2-156">使用的 toodeploy 和成品佈建 VM 之後，設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="077c2-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="077c2-157">構件可以是：</span><span class="sxs-lookup"><span data-stu-id="077c2-157">Artifacts can be:</span></span>

   - <span data-ttu-id="077c2-158">您想 tooinstall 上 hello VM-例如代理程式、 Fiddler 及 Visual Studio 的工具。</span><span class="sxs-lookup"><span data-stu-id="077c2-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="077c2-159">您想在 hello VM-toorun，諸如複製儲存機制的動作。</span><span class="sxs-lookup"><span data-stu-id="077c2-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="077c2-160">您想 tootest 應用程式。</span><span class="sxs-lookup"><span data-stu-id="077c2-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="077c2-161">許多構件為現成可用。</span><span class="sxs-lookup"><span data-stu-id="077c2-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="077c2-162">但如果想要符合特定需求的更多自訂，您可以建立自己的自訂構件。</span><span class="sxs-lookup"><span data-stu-id="077c2-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="077c2-163">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-164">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-164">Task</span></span> | <span data-ttu-id="077c2-165">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-166">為您的 DevTest Labs VM 建立自訂的構件</span><span class="sxs-lookup"><span data-stu-id="077c2-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="077c2-167">在您的實驗室中建立您自己自訂的成品以利 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="077c2-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="077c2-168">在 Azure DevTest Labs 中加入 Git 儲存機制 toostore 自訂成品和使用的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="077c2-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="077c2-169">深入了解如何 toostore 您自己的私用 Git 儲存機制內的自訂成品。</span><span class="sxs-lookup"><span data-stu-id="077c2-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="077c2-170">**控制成本**</span><span class="sxs-lookup"><span data-stu-id="077c2-170">**Control costs**</span></span>
   
    <span data-ttu-id="077c2-171">Azure 的 DevTest Labs 可讓您 tooset 原則 hello 實驗室 toospecify hello 的數目上限可以在 hello 實驗室測試者建立的 Vm 中。</span><span class="sxs-lookup"><span data-stu-id="077c2-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="077c2-172">如果測試小組所擁有的工作排程一組，而且您想 toostop hello 一天的特定時間的所有 hello Vm，然後自動重新啟動它們 hello 遵循一天，您可以輕鬆地完成作業，設定自動關閉及自動啟動原則 hello 實驗室中。</span><span class="sxs-lookup"><span data-stu-id="077c2-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="077c2-173">最後，應用程式開發完成時，您可以刪除所有 hello Vm 同時執行單一的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="077c2-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="077c2-174">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-175">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-175">Task</span></span> | <span data-ttu-id="077c2-176">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-177">定義實驗室原則</span><span class="sxs-lookup"><span data-stu-id="077c2-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="077c2-178">Hello 實驗室中設定原則來控制成本。</span><span class="sxs-lookup"><span data-stu-id="077c2-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="077c2-179">刪除所有 hello 實驗室 Vm 的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="077c2-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="077c2-180">測試完成時，請刪除所有在一個作業中的 hello 實驗室。</span><span class="sxs-lookup"><span data-stu-id="077c2-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="077c2-181">**新增虛擬網路 tooa 實驗室**</span><span class="sxs-lookup"><span data-stu-id="077c2-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="077c2-182">每當建立一個實驗室時，DevTest Labs 就會建立新的虛擬網路 (VNET)。</span><span class="sxs-lookup"><span data-stu-id="077c2-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="077c2-183">如果您已設定您自己的 VNET – 例如，藉由使用 ExpressRoute 或站對站 VPN – 您可以加入此 VNET tooyour 實驗室虛擬網路設定，使其可建立 Vm 時。</span><span class="sxs-lookup"><span data-stu-id="077c2-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="077c2-184">此外，也沒有 Azure Active Directory 網域聯結成品可用 hello VM 正在建立時所加入 VM tooa 網域。</span><span class="sxs-lookup"><span data-stu-id="077c2-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="077c2-185">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-186">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-186">Task</span></span> | <span data-ttu-id="077c2-187">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-188">在 Azure DevTest Labs 中設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="077c2-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="077c2-189">了解如何 tooconfigure 虛擬網路中使用 Azure DevTest Labs hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="077c2-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="077c2-190">**與每個測試人員共用 hello 實驗室**</span><span class="sxs-lookup"><span data-stu-id="077c2-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="077c2-191">使用您分享給測試人員的連結即可直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="077c2-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="077c2-192">即使沒有 toohave Azure 帳戶，因為它們已[Microsoft 帳戶](devtest-lab-faq.md#what-is-a-microsoft-account)。</span><span class="sxs-lookup"><span data-stu-id="077c2-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="077c2-193">測試人員看不到其他測試人員建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="077c2-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="077c2-194">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-195">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-195">Task</span></span> | <span data-ttu-id="077c2-196">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-197">在 Azure DevTest Labs 中新增軟體測試人員 tooa 實驗室</span><span class="sxs-lookup"><span data-stu-id="077c2-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="077c2-198">使用 hello Azure 入口網站 tooadd 測試人員 tooyour 實驗室。</span><span class="sxs-lookup"><span data-stu-id="077c2-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="077c2-199">新增測試人員 toohello 實驗室使用的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="077c2-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="077c2-200">使用 PowerShell tooautomate 新增測試人員 tooyour 實驗室。</span><span class="sxs-lookup"><span data-stu-id="077c2-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="077c2-201">取得連結 toohello 實驗室</span><span class="sxs-lookup"><span data-stu-id="077c2-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="077c2-202">了解測試人員如何透過超連結直接存取實驗室。</span><span class="sxs-lookup"><span data-stu-id="077c2-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="077c2-203">**為更多小組自動建立實驗室**</span><span class="sxs-lookup"><span data-stu-id="077c2-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="077c2-204">您可以自動化實驗室建立、 自訂的設定，包括建立資源管理員範本，並使用它 toocreate 相同實驗室次又一次。</span><span class="sxs-lookup"><span data-stu-id="077c2-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="077c2-205">深入了 hello 下表中的 hello 連結，即可：</span><span class="sxs-lookup"><span data-stu-id="077c2-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="077c2-206">Task</span><span class="sxs-lookup"><span data-stu-id="077c2-206">Task</span></span> | <span data-ttu-id="077c2-207">您學到什麼</span><span class="sxs-lookup"><span data-stu-id="077c2-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="077c2-208">使用 Resource Manager 範本建立實驗室</span><span class="sxs-lookup"><span data-stu-id="077c2-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="077c2-209">在 Azure DevTest Labs 中使用 Resource Manager 範本建立實驗室。</span><span class="sxs-lookup"><span data-stu-id="077c2-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

