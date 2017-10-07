---
title: "在 Azure DevTest Labs aaaManage 基本實驗室環境原則 |Microsoft 文件"
description: "深入了解如何 tooset 某些 hello 基本原則 （設定），在 DevTest Labs 實驗室"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="d05d1-103">在 Azure DevTest Labs 中管理實驗室的基本原則</span><span class="sxs-lookup"><span data-stu-id="d05d1-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="d05d1-104">Azure 的 DevTest Labs 可讓您 toocontrol 成本，並減少浪費在實驗室每個實驗室管理原則 （設定）。</span><span class="sxs-lookup"><span data-stu-id="d05d1-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="d05d1-105">本文中，在您開始使用原則學習 tooset 如何當兩個 hello 最關鍵原則-限制 hello 數目的虛擬機器 (VM) 可建立或宣告單一使用者，並設定自動關機。</span><span class="sxs-lookup"><span data-stu-id="d05d1-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="d05d1-106">tooview 如何 tooset 每個實驗室原則，請參閱 hello 文件，[定義中 Azure DevTest Labs 實驗室原則](devtest-lab-set-lab-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="d05d1-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="d05d1-107">在 Azure DevTest Labs 中存取實驗室的原則</span><span class="sxs-lookup"><span data-stu-id="d05d1-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="d05d1-108">hello 下列步驟會引導您設定原則的實驗室中 Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="d05d1-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="d05d1-109">tooview （與變更） hello 原則的實驗室，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d05d1-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="d05d1-110">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="d05d1-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="d05d1-111">選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="d05d1-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="d05d1-112">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="d05d1-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="d05d1-113">選取 [組態和原則]。</span><span class="sxs-lookup"><span data-stu-id="d05d1-113">Select **Configuration and policies**.</span></span>

    ![[原則設定] 刀鋒視窗](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="d05d1-115">hello**組態和原則**刀鋒視窗中包含的設定，您可以指定一個功能表。</span><span class="sxs-lookup"><span data-stu-id="d05d1-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="d05d1-116">本文章涵蓋只 hello 設定**每位使用者的虛擬機器**和**自動關機**。</span><span class="sxs-lookup"><span data-stu-id="d05d1-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="d05d1-117">toolearn 有關 hello 剩餘的設定，請參閱[管理所有原則的實驗室中 Azure DevTest Labs](./devtest-lab-set-lab-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="d05d1-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="d05d1-118">設定每位使用者的虛擬機器數目</span><span class="sxs-lookup"><span data-stu-id="d05d1-118">Set virtual machines per user</span></span>
<span data-ttu-id="d05d1-119">hello 原則**每位使用者的虛擬機器**可讓您 toospecify hello 的 Vm 數目上限，您可以建立個別的使用者。</span><span class="sxs-lookup"><span data-stu-id="d05d1-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="d05d1-120">如果使用者嘗試 toocreate 或宣告 VM 在達到 hello 使用者限制時，錯誤訊息會指出該 VM 無法建立/宣告的 hello。</span><span class="sxs-lookup"><span data-stu-id="d05d1-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="d05d1-121">在 hello 實驗室**組態和原則**功能表上，選取**每位使用者的虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="d05d1-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![每位使用者的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="d05d1-123">選取**是**toolimit hello Vm 數目每位使用者。</span><span class="sxs-lookup"><span data-stu-id="d05d1-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="d05d1-124">如果您不想 toolimit hello Vm 數目每位使用者，選取**否**。</span><span class="sxs-lookup"><span data-stu-id="d05d1-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="d05d1-125">如果您選取**是**，輸入數字值，指出 hello 可建立或由使用者宣告的 Vm 數目上限。</span><span class="sxs-lookup"><span data-stu-id="d05d1-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="d05d1-126">選取**是**toolimit hello 數目可以使用 SSD （固態磁碟） 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="d05d1-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="d05d1-127">如果您不想 toolimit hello 數目可以使用 SSD 的 Vm，選取**否**。</span><span class="sxs-lookup"><span data-stu-id="d05d1-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="d05d1-128">如果您選取**是**，輸入值，指出 hello 可使用 SSD 來建立的 Vm 數目上限。</span><span class="sxs-lookup"><span data-stu-id="d05d1-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="d05d1-129">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d05d1-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="d05d1-130">設定自動關機</span><span class="sxs-lookup"><span data-stu-id="d05d1-130">Set auto-shutdown</span></span>
<span data-ttu-id="d05d1-131">hello 自動關閉原則可幫助 toominimize 實驗室可以讓您在本實驗室 Vm 關機的 toospecify hello 時間會浪費。</span><span class="sxs-lookup"><span data-stu-id="d05d1-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="d05d1-132">在 hello 實驗室**組態和原則**刀鋒視窗中，選取**自動關機**。</span><span class="sxs-lookup"><span data-stu-id="d05d1-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![自動關機](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="d05d1-134">選取**上**tooenable 此原則，和**關閉**toodisable 它。</span><span class="sxs-lookup"><span data-stu-id="d05d1-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="d05d1-135">如果您啟用這個原則，指定下所有 Vm 的 hello 時間 （和時區） tooshut hello 目前實驗室中。</span><span class="sxs-lookup"><span data-stu-id="d05d1-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="d05d1-136">指定**是**或**否**hello 選項 toosend 通知 15 分鐘先前 toohello 指定自動關機時間。</span><span class="sxs-lookup"><span data-stu-id="d05d1-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="d05d1-137">如果您指定**是**，輸入 webhook URL 端點 tooreceive hello 通知。</span><span class="sxs-lookup"><span data-stu-id="d05d1-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="d05d1-138">如需 webhook 的詳細資訊，請參閱[建立 webhook 或 API Azure 函式](../azure-functions/functions-create-a-web-hook-or-api-function.md)。</span><span class="sxs-lookup"><span data-stu-id="d05d1-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="d05d1-139">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d05d1-139">Select **Save**.</span></span>

    <span data-ttu-id="d05d1-140">根據預設，一旦啟用此原則適用於 tooall hello 目前實驗室中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="d05d1-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="d05d1-141">這項設定特定 VM 中，開啟 tooremove hello VM 刀鋒視窗，然後變更其**自動關機**設定</span><span class="sxs-lookup"><span data-stu-id="d05d1-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="d05d1-142">設定自動啟動</span><span class="sxs-lookup"><span data-stu-id="d05d1-142">Set auto-start</span></span>
<span data-ttu-id="d05d1-143">hello 自動啟動原則可讓您 toospecify 時應該啟動 hello 目前實驗室中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="d05d1-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="d05d1-144">在 hello 實驗室**組態和原則**刀鋒視窗中，選取**自動啟動**。</span><span class="sxs-lookup"><span data-stu-id="d05d1-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![自動啟動](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="d05d1-146">選取**上**tooenable 此原則，和**關閉**toodisable 它。</span><span class="sxs-lookup"><span data-stu-id="d05d1-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="d05d1-147">如果您啟用這個原則，指定 hello 排定的開始時間、 時區、 和 hello 星期幾 hello 時間適用的 hello。</span><span class="sxs-lookup"><span data-stu-id="d05d1-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="d05d1-148">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="d05d1-148">Select **Save**.</span></span>

    <span data-ttu-id="d05d1-149">啟用之後，此原則不會自動套用的 tooany Vm hello 目前實驗室中。</span><span class="sxs-lookup"><span data-stu-id="d05d1-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="d05d1-150">tooapply 這個設定 tooa 特定 VM、 開啟 hello VM 刀鋒視窗，然後變更其**自動啟動**設定</span><span class="sxs-lookup"><span data-stu-id="d05d1-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d05d1-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d05d1-151">Next steps</span></span>

- <span data-ttu-id="d05d1-152">[在 Azure DevTest Labs 中定義實驗室原則](devtest-lab-set-lab-policy.md)-了解如何 toomodify 其他實驗室原則</span><span class="sxs-lookup"><span data-stu-id="d05d1-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
