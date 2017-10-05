---
title: "研發/測試實驗室概念 | Microsoft Docs"
description: "了解研發/測試實驗室的基本概念，以及它如何讓您輕鬆地建立、管理和監視 Azure 虛擬機器"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 105919e8-3617-4ce3-a29f-a289fa608fb2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 1caea59e71126e934e2e52a1ad7f533ffa7d4b03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="devtest-labs-concepts"></a><span data-ttu-id="83456-103">研發/測試實驗室概念</span><span class="sxs-lookup"><span data-stu-id="83456-103">DevTest Labs concepts</span></span>
## <a name="overview"></a><span data-ttu-id="83456-104">概觀</span><span class="sxs-lookup"><span data-stu-id="83456-104">Overview</span></span>
<span data-ttu-id="83456-105">下列清單包含重要的研發/測試實驗室概念和定義：</span><span class="sxs-lookup"><span data-stu-id="83456-105">The following list contains key DevTest Labs concepts and definitions:</span></span>

## <a name="labs"></a><span data-ttu-id="83456-106">實驗室</span><span class="sxs-lookup"><span data-stu-id="83456-106">Labs</span></span>
<span data-ttu-id="83456-107">實驗室是包含一組資源 (例如虛擬機器 (VM)) 的基礎結構，可讓您藉由指定限制和配額更好地管理這些資源。</span><span class="sxs-lookup"><span data-stu-id="83456-107">A lab is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="83456-108">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="83456-108">Virtual machine</span></span>
<span data-ttu-id="83456-109">Azure VM 是由 Azure 所提供的[隨選且可調整的數種運算資源](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm)類型之一。</span><span class="sxs-lookup"><span data-stu-id="83456-109">An Azure VM is one of several types of [on-demand, scalable computing resources](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) that Azure offers.</span></span> <span data-ttu-id="83456-110">Azure VM 提供您虛擬化的彈性，而無需購買並維護執行它的實體硬體，不過您仍然需要藉由執行特定工作，例如設定、修補和安裝在其中執行的軟體來維護 VM。</span><span class="sxs-lookup"><span data-stu-id="83456-110">Azure VMs give you the flexibility of virtualization without having to buy and maintain the physical hardware that runs it, although you still need to maintain the VM by performing certain tasks, such as configuring, patching, and installing the software that runs on it.</span></span>

<span data-ttu-id="83456-111">[Azure 中的 Windows 虛擬機器概觀](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview)提供您在建立 VM 之前應該考慮的事項、建立方式及管理方式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="83456-111">[Overview of Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) gives you information about what you should consider before you create a VM, how you create it, and how you manage it.</span></span>

## <a name="claimable-vm"></a><span data-ttu-id="83456-112">可宣告 VM</span><span class="sxs-lookup"><span data-stu-id="83456-112">Claimable VM</span></span>
<span data-ttu-id="83456-113">Azure 可宣告 VM 是可供任何具有權限的實驗室使用者使用的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="83456-113">An Azure Claimable VM is a virtual machine that is available for use by any lab user with permissions.</span></span> <span data-ttu-id="83456-114">實驗室系統管理員能以特定的基本映像和構件準備 VM，並將它們儲存至共用集區。</span><span class="sxs-lookup"><span data-stu-id="83456-114">A lab admin can prepare VMs with specific base images and artifacts and save them to a shared pool.</span></span> <span data-ttu-id="83456-115">實驗室使用者接著可以在需要具有特定組態的 VM 時，從集區宣告具有該組態的運作中 VM。</span><span class="sxs-lookup"><span data-stu-id="83456-115">A lab user can then claim a working VM from the pool when they need one with that specific configuration.</span></span>

<span data-ttu-id="83456-116">可宣告的 VM 最初並不會指派給任何特定的使用者，但它會出現在所有使用者的 [可宣告的虛擬機器] 清單上。</span><span class="sxs-lookup"><span data-stu-id="83456-116">A VM that is claimable is not initially assigned to any particular user, but will show up in every user's list under "Claimable virtual machines".</span></span> <span data-ttu-id="83456-117">當使用者宣告 VM 之後，該 VM 將會移至該使用者的 [我的虛擬機器] 區域，且其他使用者將無法宣告該 VM。</span><span class="sxs-lookup"><span data-stu-id="83456-117">After a VM is claimed by a user, it is moved up to their "My virtual machines" area and is no longer claimable by any other user.</span></span>

## <a name="environment"></a><span data-ttu-id="83456-118">Environment</span><span class="sxs-lookup"><span data-stu-id="83456-118">Environment</span></span>
<span data-ttu-id="83456-119">在研發/測試實驗室中，環境是指實驗室中 Azure 資源的集合。</span><span class="sxs-lookup"><span data-stu-id="83456-119">In DevTest Labs, an environment refers to a collection of Azure resources in a lab.</span></span> <span data-ttu-id="83456-120">[此部落格文章](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/)討論如何從 Azure Resource Manager 範本建立多個 VM 環境。</span><span class="sxs-lookup"><span data-stu-id="83456-120">[This blog post](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) discusses how to create multi-VM environments from your Azure Resource Manager templates.</span></span>

## <a name="base-images"></a><span data-ttu-id="83456-121">基礎映像</span><span class="sxs-lookup"><span data-stu-id="83456-121">Base images</span></span>
<span data-ttu-id="83456-122">基礎映像是 VM 映像，包含預先安裝並加以設定的所有工具與設定，可用來快速建立 VM。</span><span class="sxs-lookup"><span data-stu-id="83456-122">Base images are VM images with all the tools and settings preinstalled and configured to quickly create a VM.</span></span> <span data-ttu-id="83456-123">您可以挑選現有的基本映像並加入構件來安裝測試代理程式，藉以佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="83456-123">You can provision a VM by picking an existing base and adding an artifact to install your test agent.</span></span> <span data-ttu-id="83456-124">您接著可以儲存佈建的 VM 做為基本映像，如此一來，不必針對 VM 的每個佈建重新安裝測試代理程式，就能使用該基本映像。</span><span class="sxs-lookup"><span data-stu-id="83456-124">You can then save the provisioned VM as a base so that the base can be used without having to reinstall the test agent for each provisioning of the VM.</span></span>

## <a name="artifacts"></a><span data-ttu-id="83456-125">構件</span><span class="sxs-lookup"><span data-stu-id="83456-125">Artifacts</span></span>
<span data-ttu-id="83456-126">構件是在佈建 VM 之後用來部署和設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="83456-126">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="83456-127">構件可以是：</span><span class="sxs-lookup"><span data-stu-id="83456-127">Artifacts can be:</span></span>

* <span data-ttu-id="83456-128">您想要在 VM 上安裝的工具 - 例如，代理程式、Fiddler 及 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="83456-128">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
* <span data-ttu-id="83456-129">您想要在 VM 上執行的動作 - 例如，複製儲存機制。</span><span class="sxs-lookup"><span data-stu-id="83456-129">Actions that you want to run on the VM - such as cloning a repo.</span></span>
* <span data-ttu-id="83456-130">您想要測試的應用程式。</span><span class="sxs-lookup"><span data-stu-id="83456-130">Applications that you want to test.</span></span>

<span data-ttu-id="83456-131">構件是 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) JSON 檔案，其中包含執行部署及套用組態的指示。</span><span class="sxs-lookup"><span data-stu-id="83456-131">Artifacts are [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) JSON files that contain instructions to perform deployment and apply configuration.</span></span>

## <a name="artifact-repositories"></a><span data-ttu-id="83456-132">構件儲存機制</span><span class="sxs-lookup"><span data-stu-id="83456-132">Artifact repositories</span></span>
<span data-ttu-id="83456-133">構件儲存機制是已簽入構件的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="83456-133">Artifact repositories are git repositories where artifacts are checked in.</span></span> <span data-ttu-id="83456-134">構件儲存機制可以加入組織中的多個實驗室，以便重複使用及共用。</span><span class="sxs-lookup"><span data-stu-id="83456-134">Artifact repositories can be added to multiple labs in your organization enabling reuse and sharing.</span></span>

## <a name="formulas"></a><span data-ttu-id="83456-135">公式</span><span class="sxs-lookup"><span data-stu-id="83456-135">Formulas</span></span>
<span data-ttu-id="83456-136">除了基底映像，公式提供快速 VM 佈建的機制。</span><span class="sxs-lookup"><span data-stu-id="83456-136">Formulas, in addition to base images, provide a mechanism for fast VM provisioning.</span></span> <span data-ttu-id="83456-137">研發/測試實驗室中的公式是用來建立實驗室 VM 的預設屬性值清單。</span><span class="sxs-lookup"><span data-stu-id="83456-137">A formula in DevTest Labs is a list of default property values used to create a lab VM.</span></span>
<span data-ttu-id="83456-138">透過公式，可以建立具備相同屬性集 - 例如基底映像、VM 大小、虛擬網路以及成品 - 的 VM，而不需要每次都指定這些屬性。</span><span class="sxs-lookup"><span data-stu-id="83456-138">With formulas, VMs with the same set of properties - such as base image, VM size, virtual network, and artifacts - can be created without needing to specify those properties each time.</span></span> <span data-ttu-id="83456-139">透過公式建立 VM 時，可以依現況使用預設值，或修改預設值。</span><span class="sxs-lookup"><span data-stu-id="83456-139">When creating a VM from a formula, the default values can be used as-is or modified.</span></span>

## <a name="policies"></a><span data-ttu-id="83456-140">原則</span><span class="sxs-lookup"><span data-stu-id="83456-140">Policies</span></span>
<span data-ttu-id="83456-141">原則可協助控制實驗室中的成本。</span><span class="sxs-lookup"><span data-stu-id="83456-141">Policies help in controlling cost in your lab.</span></span> <span data-ttu-id="83456-142">例如，您可以建立一個原則，根據定義的排程自動關閉 VM。</span><span class="sxs-lookup"><span data-stu-id="83456-142">For example, you can create a policy to automatically shut down VMs based on a defined schedule.</span></span>

## <a name="caps"></a><span data-ttu-id="83456-143">最高限度</span><span class="sxs-lookup"><span data-stu-id="83456-143">Caps</span></span>
<span data-ttu-id="83456-144">最高限度是可將您實驗室中的成本浪費降至最低的機制。</span><span class="sxs-lookup"><span data-stu-id="83456-144">Caps is a mechanism to minimize waste in your lab.</span></span> <span data-ttu-id="83456-145">例如，您可以設定一個最高限度，來限制每位使用者或每個實驗室中可建立的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="83456-145">For example, you can set a cap to restrict the number of VMs that can be created per user, or in a lab.</span></span>

## <a name="security-levels"></a><span data-ttu-id="83456-146">安全性層級</span><span class="sxs-lookup"><span data-stu-id="83456-146">Security levels</span></span>
<span data-ttu-id="83456-147">安全性存取權是由 Azure 角色型存取控制 (RBAC) 所決定。</span><span class="sxs-lookup"><span data-stu-id="83456-147">Security access is determined by Azure Role-Based Access Control (RBAC).</span></span> <span data-ttu-id="83456-148">若要了解存取權的運作方式，了解 RBAC 所定義的權限、角色和範圍之間的差異將有所幫助。</span><span class="sxs-lookup"><span data-stu-id="83456-148">To understand how access works, it helps to understand the differences between a permission, a role, and a scope as defined by RBAC.</span></span>

* <span data-ttu-id="83456-149">權限 - 權限是針對特定動作所定義的存取權 (例如，針對所有虛擬機器的讀取權限)。</span><span class="sxs-lookup"><span data-stu-id="83456-149">Permission - A permission is a defined access to a specific action (e.g. read-access to all virtual machines).</span></span>
* <span data-ttu-id="83456-150">角色 - 角色是一組可以分組並指派給使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="83456-150">Role - A role is a set of permissions that can be grouped and assigned to a user.</span></span> <span data-ttu-id="83456-151">例如，「訂用帳戶擁有者」  角色擁有訂用帳戶內所有資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="83456-151">For example, the *subscription owner* role has access to all resources within a subscription.</span></span>
* <span data-ttu-id="83456-152">範圍 - 範圍是 Azure 資源階層的其中一個層級，例如，資源群組、單一實驗室或整個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="83456-152">Scope - A scope is a level within the hierarchy of an Azure resource, such as a resource group, a single lab, or the entire subscription.</span></span>

<span data-ttu-id="83456-153">在 DevTest Labs 的範圍內有兩種可用來定義使用者權限的角色類型︰實驗室擁有者和實驗室使用者。</span><span class="sxs-lookup"><span data-stu-id="83456-153">Within the scope of DevTest Labs, there are two types of roles to define user permissions: lab owner and lab user.</span></span>

* <span data-ttu-id="83456-154">實驗室擁有者 - 實驗室擁有者擁有實驗室內任何資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="83456-154">Lab Owner - A lab owner has access to any resources within the lab.</span></span> <span data-ttu-id="83456-155">因此，實驗室擁有者可以修改原則、讀取和寫入任何 VM、變更虛擬網路等等。</span><span class="sxs-lookup"><span data-stu-id="83456-155">Therefore, a lab owner can modify policies, read and write any VMs, change the virtual network, and so on.</span></span>
* <span data-ttu-id="83456-156">實驗室使用者 - 實驗室使用者可以檢視所有實驗室資源，例如 VM、原則和虛擬網路，但不能修改原則或任何由其他使用者所建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="83456-156">Lab User - A lab user can view all lab resources, such as VMs, policies, and virtual networks, but cannot modify policies or any VMs created by other users.</span></span>

<span data-ttu-id="83456-157">若要查看如何在 DevTest Labs 建立自訂角色，請參閱 [將特定實驗室原則的權限授與使用者](devtest-lab-grant-user-permissions-to-specific-lab-policies.md)一文。</span><span class="sxs-lookup"><span data-stu-id="83456-157">To see how to create custom roles in DevTest Labs, refer to the article, [Grant user permissions to specific lab policies](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).</span></span>

<span data-ttu-id="83456-158">由於範圍是階層形式，當使用者擁有特定範圍的權限時，就會自動獲得該範圍所包含的每個較低層級範圍的權限。</span><span class="sxs-lookup"><span data-stu-id="83456-158">Since scopes are hierarchical, when a user has permissions at a certain scope, they are automatically granted those permissions at every lower-level scope encompassed.</span></span> <span data-ttu-id="83456-159">例如，如果有使用者指派給訂用帳戶擁有者角色，他們就可以存取訂用帳戶中的所有資源，其中包括所有虛擬機器、所有虛擬網路和所有實驗室。</span><span class="sxs-lookup"><span data-stu-id="83456-159">For instance, if a user is assigned to the role of subscription owner, then they have access to all resources in a subscription, which include all virtual machines, all virtual networks, and all labs.</span></span> <span data-ttu-id="83456-160">因此，訂用帳戶擁有者會自動繼承實驗室擁有者角色。</span><span class="sxs-lookup"><span data-stu-id="83456-160">Therefore, a subscription owner automatically inherits the role of lab owner.</span></span> <span data-ttu-id="83456-161">不過，若情形顛倒過來就不成立。</span><span class="sxs-lookup"><span data-stu-id="83456-161">However, the opposite is not true.</span></span> <span data-ttu-id="83456-162">實驗室擁有者可存取實驗室，而實驗室是比訂用帳戶層級還低的範圍。</span><span class="sxs-lookup"><span data-stu-id="83456-162">A lab owner has access to a lab, which is a lower scope than the subscription level.</span></span> <span data-ttu-id="83456-163">因此，實驗室擁有者將無法看到實驗室以外的虛擬機器、虛擬網路或任何資源。</span><span class="sxs-lookup"><span data-stu-id="83456-163">Therefore, a lab owner will not be able to see virtual machines or virtual networks or any resources that are outside of the lab.</span></span>

## <a name="azure-resource-manager-templates"></a><span data-ttu-id="83456-164">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="83456-164">Azure Resource Manager templates</span></span>
<span data-ttu-id="83456-165">此文章中討論的所有概念都可以使用 Azure Resource Manager 範本來設定，範本可以讓您定義 Azure 解決方案的基礎結構/設定，並重複以一致的狀態來部署。</span><span class="sxs-lookup"><span data-stu-id="83456-165">All of the concepts discussed in this article can be configured by using Azure Resource Manager templates, which let you define the infrastructure/configuration of your Azure solution and repeatedly deploy it in a consistent state.</span></span>

<span data-ttu-id="83456-166">[了解 Azure Resource Manager 範本的結構和語法](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format)描述 Azure Resource Manager 範本的結構，以及範本的各區段中可用的屬性。</span><span class="sxs-lookup"><span data-stu-id="83456-166">[Understand the structure and syntax of Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) describes the structure of an Azure Resource Manager template and the properties that are available in the different sections of a template.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="83456-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="83456-167">Next steps</span></span>
[<span data-ttu-id="83456-168">在研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="83456-168">Create a lab in DevTest Labs</span></span>](devtest-lab-create-lab.md)
