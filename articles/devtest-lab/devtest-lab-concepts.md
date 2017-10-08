---
title: "aaaDevTest 實驗室概念 |Microsoft 文件"
description: "深入了解的 DevTest Labs hello 基本概念，它可讓您輕鬆 toocreate，如何管理和監視 Azure 虛擬機器"
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
ms.openlocfilehash: d9f1d948002c4d3121e5bdd4e65eb8b54cd91f9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="devtest-labs-concepts"></a><span data-ttu-id="8f078-103">研發/測試實驗室概念</span><span class="sxs-lookup"><span data-stu-id="8f078-103">DevTest Labs concepts</span></span>
## <a name="overview"></a><span data-ttu-id="8f078-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8f078-104">Overview</span></span>
<span data-ttu-id="8f078-105">下列清單中的 hello 包含重要的 DevTest Labs 概念和定義：</span><span class="sxs-lookup"><span data-stu-id="8f078-105">hello following list contains key DevTest Labs concepts and definitions:</span></span>

## <a name="labs"></a><span data-ttu-id="8f078-106">實驗室</span><span class="sxs-lookup"><span data-stu-id="8f078-106">Labs</span></span>
<span data-ttu-id="8f078-107">實驗室環境是 hello 基礎結構包含一組資源，例如可讓您更佳的虛擬機器 (Vm)，藉由指定限制和配額管理這些資源。</span><span class="sxs-lookup"><span data-stu-id="8f078-107">A lab is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span>

## <a name="virtual-machine"></a><span data-ttu-id="8f078-108">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8f078-108">Virtual machine</span></span>
<span data-ttu-id="8f078-109">Azure VM 是由 Azure 所提供的[隨選且可調整的數種運算資源](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm)類型之一。</span><span class="sxs-lookup"><span data-stu-id="8f078-109">An Azure VM is one of several types of [on-demand, scalable computing resources](https://docs.microsoft.com/azure/app-service-web/choose-web-site-cloud-service-vm) that Azure offers.</span></span> <span data-ttu-id="8f078-110">Azure Vm 提供，而不需要 toobuy hello 虛擬化的彈性，並維護 hello 實體硬體執行，但您仍須 toomaintain hello VM 上執行特定工作，例如設定、 修補及安裝 hello 軟體在其上執行。</span><span class="sxs-lookup"><span data-stu-id="8f078-110">Azure VMs give you hello flexibility of virtualization without having toobuy and maintain hello physical hardware that runs it, although you still need toomaintain hello VM by performing certain tasks, such as configuring, patching, and installing hello software that runs on it.</span></span>

<span data-ttu-id="8f078-111">[Azure 中的 Windows 虛擬機器概觀](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview)提供您在建立 VM 之前應該考慮的事項、建立方式及管理方式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8f078-111">[Overview of Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-overview) gives you information about what you should consider before you create a VM, how you create it, and how you manage it.</span></span>

## <a name="claimable-vm"></a><span data-ttu-id="8f078-112">可宣告 VM</span><span class="sxs-lookup"><span data-stu-id="8f078-112">Claimable VM</span></span>
<span data-ttu-id="8f078-113">Azure 可宣告 VM 是可供任何具有權限的實驗室使用者使用的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8f078-113">An Azure Claimable VM is a virtual machine that is available for use by any lab user with permissions.</span></span> <span data-ttu-id="8f078-114">實驗室系統管理員可以使用特定的基底映像和成品準備 Vm，並將它們儲存 tooa 共用集區。</span><span class="sxs-lookup"><span data-stu-id="8f078-114">A lab admin can prepare VMs with specific base images and artifacts and save them tooa shared pool.</span></span> <span data-ttu-id="8f078-115">實驗室使用者在需要一個包含該特定的設定時，可以再宣告 hello 集區中的 VM 可運作。</span><span class="sxs-lookup"><span data-stu-id="8f078-115">A lab user can then claim a working VM from hello pool when they need one with that specific configuration.</span></span>

<span data-ttu-id="8f078-116">VM 若是位於 claimable 一開始未指派 tooany 特定使用者，但會顯示在 「 Claimable 虛擬機器 」 底下的每位使用者的清單。</span><span class="sxs-lookup"><span data-stu-id="8f078-116">A VM that is claimable is not initially assigned tooany particular user, but will show up in every user's list under "Claimable virtual machines".</span></span> <span data-ttu-id="8f078-117">VM 宣告的使用者之後，它是 「 我的虛擬機器 」 區域中上移 tootheir 且不再 claimable 任何其他使用者。</span><span class="sxs-lookup"><span data-stu-id="8f078-117">After a VM is claimed by a user, it is moved up tootheir "My virtual machines" area and is no longer claimable by any other user.</span></span>

## <a name="environment"></a><span data-ttu-id="8f078-118">Environment</span><span class="sxs-lookup"><span data-stu-id="8f078-118">Environment</span></span>
<span data-ttu-id="8f078-119">在 DevTest 實驗室環境是指 tooa 實驗室中的 Azure 資源集合。</span><span class="sxs-lookup"><span data-stu-id="8f078-119">In DevTest Labs, an environment refers tooa collection of Azure resources in a lab.</span></span> <span data-ttu-id="8f078-120">[此部落格文章](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/)討論如何從您的 Azure Resource Manager 範本 toocreate 多部 VM 環境。</span><span class="sxs-lookup"><span data-stu-id="8f078-120">[This blog post](https://blogs.msdn.microsoft.com/devtestlab/2016/11/16/connect-2016-news-for-azure-devtest-labs-azure-resource-manager-template-based-environments-vm-auto-shutdown-and-more/) discusses how toocreate multi-VM environments from your Azure Resource Manager templates.</span></span>

## <a name="base-images"></a><span data-ttu-id="8f078-121">基礎映像</span><span class="sxs-lookup"><span data-stu-id="8f078-121">Base images</span></span>
<span data-ttu-id="8f078-122">基底映像會使用所有的 hello 工具和設定預先安裝的 VM 映像，並設定的 tooquickly 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="8f078-122">Base images are VM images with all hello tools and settings preinstalled and configured tooquickly create a VM.</span></span> <span data-ttu-id="8f078-123">您可以佈建 VM 挑選現有的基礎，並加入成品 tooinstall 測試代理程式。</span><span class="sxs-lookup"><span data-stu-id="8f078-123">You can provision a VM by picking an existing base and adding an artifact tooinstall your test agent.</span></span> <span data-ttu-id="8f078-124">您可以再儲存 hello 佈建 VM 為基底，以便 hello 基底可以使用而不需要 tooreinstall hello 測試代理程式的每個佈建 hello VM。</span><span class="sxs-lookup"><span data-stu-id="8f078-124">You can then save hello provisioned VM as a base so that hello base can be used without having tooreinstall hello test agent for each provisioning of hello VM.</span></span>

## <a name="artifacts"></a><span data-ttu-id="8f078-125">構件</span><span class="sxs-lookup"><span data-stu-id="8f078-125">Artifacts</span></span>
<span data-ttu-id="8f078-126">使用的 toodeploy 和成品佈建 VM 之後，設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f078-126">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="8f078-127">構件可以是：</span><span class="sxs-lookup"><span data-stu-id="8f078-127">Artifacts can be:</span></span>

* <span data-ttu-id="8f078-128">您想 tooinstall 上 hello VM-例如代理程式、 Fiddler 及 Visual Studio 的工具。</span><span class="sxs-lookup"><span data-stu-id="8f078-128">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
* <span data-ttu-id="8f078-129">您想在 hello VM-toorun，諸如複製儲存機制的動作。</span><span class="sxs-lookup"><span data-stu-id="8f078-129">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
* <span data-ttu-id="8f078-130">您想 tootest 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8f078-130">Applications that you want tootest.</span></span>

<span data-ttu-id="8f078-131">成品是[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)包含指示 tooperform 部署，並將設定套用的 JSON 檔案。</span><span class="sxs-lookup"><span data-stu-id="8f078-131">Artifacts are [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) JSON files that contain instructions tooperform deployment and apply configuration.</span></span>

## <a name="artifact-repositories"></a><span data-ttu-id="8f078-132">構件儲存機制</span><span class="sxs-lookup"><span data-stu-id="8f078-132">Artifact repositories</span></span>
<span data-ttu-id="8f078-133">構件儲存機制是已簽入構件的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="8f078-133">Artifact repositories are git repositories where artifacts are checked in.</span></span> <span data-ttu-id="8f078-134">成品儲存機制可以加入 toomultiple 實驗室中重複使用及共用您的組織。</span><span class="sxs-lookup"><span data-stu-id="8f078-134">Artifact repositories can be added toomultiple labs in your organization enabling reuse and sharing.</span></span>

## <a name="formulas"></a><span data-ttu-id="8f078-135">公式</span><span class="sxs-lookup"><span data-stu-id="8f078-135">Formulas</span></span>
<span data-ttu-id="8f078-136">加法 toobase 映像中的公式，提供的快速 VM 佈建的機制。</span><span class="sxs-lookup"><span data-stu-id="8f078-136">Formulas, in addition toobase images, provide a mechanism for fast VM provisioning.</span></span> <span data-ttu-id="8f078-137">DevTest 實驗室中的公式是預設屬性值使用 toocreate 實驗室 VM 的清單。</span><span class="sxs-lookup"><span data-stu-id="8f078-137">A formula in DevTest Labs is a list of default property values used toocreate a lab VM.</span></span>
<span data-ttu-id="8f078-138">使用公式，以 hello 相同設定的屬性-例如基底映像、 VM 大小、 虛擬網路和成品-Vm 可以建立而不需要 toospecify 這些內容每次。</span><span class="sxs-lookup"><span data-stu-id="8f078-138">With formulas, VMs with hello same set of properties - such as base image, VM size, virtual network, and artifacts - can be created without needing toospecify those properties each time.</span></span> <span data-ttu-id="8f078-139">在建立 VM 時由公式，hello 預設值可以當做-或修改。</span><span class="sxs-lookup"><span data-stu-id="8f078-139">When creating a VM from a formula, hello default values can be used as-is or modified.</span></span>

## <a name="policies"></a><span data-ttu-id="8f078-140">原則</span><span class="sxs-lookup"><span data-stu-id="8f078-140">Policies</span></span>
<span data-ttu-id="8f078-141">原則可協助控制實驗室中的成本。</span><span class="sxs-lookup"><span data-stu-id="8f078-141">Policies help in controlling cost in your lab.</span></span> <span data-ttu-id="8f078-142">例如，您可以建立原則 tooautomatically 關閉 Vm，根據定義的排程。</span><span class="sxs-lookup"><span data-stu-id="8f078-142">For example, you can create a policy tooautomatically shut down VMs based on a defined schedule.</span></span>

## <a name="caps"></a><span data-ttu-id="8f078-143">最高限度</span><span class="sxs-lookup"><span data-stu-id="8f078-143">Caps</span></span>
<span data-ttu-id="8f078-144">端點是在您的實驗室機制 toominimize 浪費。</span><span class="sxs-lookup"><span data-stu-id="8f078-144">Caps is a mechanism toominimize waste in your lab.</span></span> <span data-ttu-id="8f078-145">例如，您可以設定 cap toorestrict hello 數目可以為每位使用者，或在實驗室中建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="8f078-145">For example, you can set a cap toorestrict hello number of VMs that can be created per user, or in a lab.</span></span>

## <a name="security-levels"></a><span data-ttu-id="8f078-146">安全性層級</span><span class="sxs-lookup"><span data-stu-id="8f078-146">Security levels</span></span>
<span data-ttu-id="8f078-147">安全性存取權是由 Azure 角色型存取控制 (RBAC) 所決定。</span><span class="sxs-lookup"><span data-stu-id="8f078-147">Security access is determined by Azure Role-Based Access Control (RBAC).</span></span> <span data-ttu-id="8f078-148">toounderstand 存取的方式運作，這樣做，toounderstand hello 之間差異的權限、 角色，以及範圍所定義的 RBAC。</span><span class="sxs-lookup"><span data-stu-id="8f078-148">toounderstand how access works, it helps toounderstand hello differences between a permission, a role, and a scope as defined by RBAC.</span></span>

* <span data-ttu-id="8f078-149">權限的權限會定義的存取 tooa 特定動作 （例如讀取權限 tooall 虛擬機器）。</span><span class="sxs-lookup"><span data-stu-id="8f078-149">Permission - A permission is a defined access tooa specific action (e.g. read-access tooall virtual machines).</span></span>
* <span data-ttu-id="8f078-150">角色的角色是一組權限可以指派 tooa 使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="8f078-150">Role - A role is a set of permissions that can be grouped and assigned tooa user.</span></span> <span data-ttu-id="8f078-151">例如，hello*訂用帳戶擁有者*角色有存取 tooall 訂用帳戶內的資源。</span><span class="sxs-lookup"><span data-stu-id="8f078-151">For example, hello *subscription owner* role has access tooall resources within a subscription.</span></span>
* <span data-ttu-id="8f078-152">範圍-範圍是中的 Azure 資源，例如資源群組、 單一實驗室中或 hello 整個訂閱 hello 階層的層級。</span><span class="sxs-lookup"><span data-stu-id="8f078-152">Scope - A scope is a level within hello hierarchy of an Azure resource, such as a resource group, a single lab, or hello entire subscription.</span></span>

<span data-ttu-id="8f078-153">Hello 在範圍內的 DevTest Labs，有兩種類型的角色 toodefine 使用者權限： 實驗室擁有者和實驗室使用者。</span><span class="sxs-lookup"><span data-stu-id="8f078-153">Within hello scope of DevTest Labs, there are two types of roles toodefine user permissions: lab owner and lab user.</span></span>

* <span data-ttu-id="8f078-154">實驗室的實驗室擁有者擁有者存取 tooany hello 實驗室內的資源。</span><span class="sxs-lookup"><span data-stu-id="8f078-154">Lab Owner - A lab owner has access tooany resources within hello lab.</span></span> <span data-ttu-id="8f078-155">因此，實驗室擁有者可以修改原則、 讀取和寫入任何 Vm、 變更 hello 虛擬網路，並以此類推。</span><span class="sxs-lookup"><span data-stu-id="8f078-155">Therefore, a lab owner can modify policies, read and write any VMs, change hello virtual network, and so on.</span></span>
* <span data-ttu-id="8f078-156">實驗室使用者 - 實驗室使用者可以檢視所有實驗室資源，例如 VM、原則和虛擬網路，但不能修改原則或任何由其他使用者所建立的 VM。</span><span class="sxs-lookup"><span data-stu-id="8f078-156">Lab User - A lab user can view all lab resources, such as VMs, policies, and virtual networks, but cannot modify policies or any VMs created by other users.</span></span>

<span data-ttu-id="8f078-157">toosee 如何 toocreate DevTest 實驗室中的自訂角色，請參閱 toohello 文章[toospecific 實驗室原則授與使用者權限](devtest-lab-grant-user-permissions-to-specific-lab-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="8f078-157">toosee how toocreate custom roles in DevTest Labs, refer toohello article, [Grant user permissions toospecific lab policies](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).</span></span>

<span data-ttu-id="8f078-158">由於範圍是階層形式，當使用者擁有特定範圍的權限時，就會自動獲得該範圍所包含的每個較低層級範圍的權限。</span><span class="sxs-lookup"><span data-stu-id="8f078-158">Since scopes are hierarchical, when a user has permissions at a certain scope, they are automatically granted those permissions at every lower-level scope encompassed.</span></span> <span data-ttu-id="8f078-159">比方說，如果使用者被指派 toohello 訂用帳戶擁有者的角色，則他們有存取 tooall 訂閱中的資源，包括所有虛擬機器、 所有虛擬網路，以及所有實驗室。</span><span class="sxs-lookup"><span data-stu-id="8f078-159">For instance, if a user is assigned toohello role of subscription owner, then they have access tooall resources in a subscription, which include all virtual machines, all virtual networks, and all labs.</span></span> <span data-ttu-id="8f078-160">因此，訂閱擁有者會自動繼承 hello 實驗室擁有者的角色。</span><span class="sxs-lookup"><span data-stu-id="8f078-160">Therefore, a subscription owner automatically inherits hello role of lab owner.</span></span> <span data-ttu-id="8f078-161">但是，並非反之亦然 hello 相反。</span><span class="sxs-lookup"><span data-stu-id="8f078-161">However, hello opposite is not true.</span></span> <span data-ttu-id="8f078-162">實驗室擁有者具有存取 tooa 實驗室中，也就是比 hello 訂用帳戶層級較低的領域。</span><span class="sxs-lookup"><span data-stu-id="8f078-162">A lab owner has access tooa lab, which is a lower scope than hello subscription level.</span></span> <span data-ttu-id="8f078-163">因此，實驗室擁有者不會無法 toosee 虛擬機器或虛擬網路或實驗室 hello 外的任何資源。</span><span class="sxs-lookup"><span data-stu-id="8f078-163">Therefore, a lab owner will not be able toosee virtual machines or virtual networks or any resources that are outside of hello lab.</span></span>

## <a name="azure-resource-manager-templates"></a><span data-ttu-id="8f078-164">Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="8f078-164">Azure Resource Manager templates</span></span>
<span data-ttu-id="8f078-165">所有使用 Azure 資源管理員範本，可讓您也可以設定本文所討論的概念 hello 定義 hello 基礎結構/Azure 方案的組態，並重複地部署處於一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="8f078-165">All of hello concepts discussed in this article can be configured by using Azure Resource Manager templates, which let you define hello infrastructure/configuration of your Azure solution and repeatedly deploy it in a consistent state.</span></span>

<span data-ttu-id="8f078-166">[了解 hello 結構和語法的 Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format)描述 hello 結構 hello 的範本的不同區段的 Azure 資源管理員範本和 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="8f078-166">[Understand hello structure and syntax of Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates#template-format) describes hello structure of an Azure Resource Manager template and hello properties that are available in hello different sections of a template.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="8f078-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f078-167">Next steps</span></span>
[<span data-ttu-id="8f078-168">在研測實驗室中建立實驗室</span><span class="sxs-lookup"><span data-stu-id="8f078-168">Create a lab in DevTest Labs</span></span>](devtest-lab-create-lab.md)
