---
title: "在 Azure DevTest Labs 中管理基本實驗室原則 | Microsoft Docs"
description: "了解如何在 DevTest Labs 中設定實驗室的一些基本原則 (設定)"
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
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bc210-103">在 Azure DevTest Labs 中管理實驗室的基本原則</span><span class="sxs-lookup"><span data-stu-id="bc210-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="bc210-104">Azure DevTest Labs 可讓您管理每個實驗室的原則 (設定)，以控制實驗室的成本並儘可能避免浪費。</span><span class="sxs-lookup"><span data-stu-id="bc210-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="bc210-105">在本文中，您將從學習如何設定兩個最重要的原則來開始使用原則：限制單一使用者可建立或宣告的虛擬機器 (VM) 數目，以及設定自動關機。</span><span class="sxs-lookup"><span data-stu-id="bc210-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="bc210-106">若要了解如何設定每個實驗室原則，請參閱[在 Azure DevTest Labs 中定義實驗室原則](devtest-lab-set-lab-policy.md)一文。</span><span class="sxs-lookup"><span data-stu-id="bc210-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="bc210-107">在 Azure DevTest Labs 中存取實驗室的原則</span><span class="sxs-lookup"><span data-stu-id="bc210-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="bc210-108">下列步驟將引導您完成在 Azure DevTest Labs 中設定實驗室原則的步驟︰</span><span class="sxs-lookup"><span data-stu-id="bc210-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="bc210-109">若要檢視 (及變更) 實驗室的原則，請依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="bc210-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="bc210-110">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="bc210-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="bc210-111">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="bc210-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="bc210-112">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="bc210-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="bc210-113">選取 [組態和原則]。</span><span class="sxs-lookup"><span data-stu-id="bc210-113">Select **Configuration and policies**.</span></span>

    ![[原則設定] 刀鋒視窗](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="bc210-115">[組態和原則] 刀鋒視窗包含一個功能表，內含您可以指定的設定。</span><span class="sxs-lookup"><span data-stu-id="bc210-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="bc210-116">本文章只涵蓋 [每位使用者的虛擬機器數目] 和 [自動關機] 的設定。</span><span class="sxs-lookup"><span data-stu-id="bc210-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="bc210-117">若要深入了解其餘設定，請參閱[在 Azure DevTest Labs 中管理實驗室的所有原則](./devtest-lab-set-lab-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="bc210-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="bc210-118">設定每位使用者的虛擬機器數目</span><span class="sxs-lookup"><span data-stu-id="bc210-118">Set virtual machines per user</span></span>
<span data-ttu-id="bc210-119">[每位使用者的虛擬機器數目]  原則可讓您指定個別使用者可以建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc210-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="bc210-120">當達到使用者限制時，如果使用者嘗試建立或宣告 VM，就會顯示錯誤訊息，指出無法建立/宣告 VM。</span><span class="sxs-lookup"><span data-stu-id="bc210-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="bc210-121">在實驗室的 [組態和原則] 功能表上，選取 [每位使用者的虛擬機器數目]。</span><span class="sxs-lookup"><span data-stu-id="bc210-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![每位使用者的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="bc210-123">選取 [是]，以限制每個使用者的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="bc210-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="bc210-124">如果不想限制每個使用者的 VM 數目，請選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="bc210-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="bc210-125">如果您選取 [是]，請輸入數值，指出使用者可建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc210-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="bc210-126">選取 [是]，以限制可使用 SSD (固態硬碟) 的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="bc210-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="bc210-127">如果不想限制可使用 SSD 的 VM 數目，請選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="bc210-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="bc210-128">如果您選取 [是]，請輸入一個值，指出可使用 SSD 建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="bc210-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="bc210-129">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="bc210-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="bc210-130">設定自動關機</span><span class="sxs-lookup"><span data-stu-id="bc210-130">Set auto-shutdown</span></span>
<span data-ttu-id="bc210-131">自動關機原則有助於將實驗室的成本浪費降至最低，方式是讓您指定這個實驗室中 VM 的關機時間。</span><span class="sxs-lookup"><span data-stu-id="bc210-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="bc210-132">在實驗室的 [組態和原則] 刀鋒視窗上，選取 [自動關機]。</span><span class="sxs-lookup"><span data-stu-id="bc210-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![自動關機](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="bc210-134">選取 [開啟] 來啟用此原則，以及選取 [關閉] 來停用它。</span><span class="sxs-lookup"><span data-stu-id="bc210-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="bc210-135">如果您啟用這個原則，請指定時間 (和時區) 以關閉目前實驗室中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="bc210-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="bc210-136">對於在指定的自動關機時間之前 15 分鐘傳送通知的選項中，指定 [是] 或 [否]。</span><span class="sxs-lookup"><span data-stu-id="bc210-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="bc210-137">如果您指定 [是]，請輸入要接收通知的 webhook URL 端點。</span><span class="sxs-lookup"><span data-stu-id="bc210-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="bc210-138">如需 webhook 的詳細資訊，請參閱[建立 webhook 或 API Azure 函式](../azure-functions/functions-create-a-web-hook-or-api-function.md)。</span><span class="sxs-lookup"><span data-stu-id="bc210-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="bc210-139">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="bc210-139">Select **Save**.</span></span>

    <span data-ttu-id="bc210-140">根據預設，這個原則一經啟用，就會套用到目前實驗室的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="bc210-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="bc210-141">若要移除特定 VM 的這項設定，請開啟 VM 的刀鋒視窗並變更其 [自動關機]  設定。</span><span class="sxs-lookup"><span data-stu-id="bc210-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="bc210-142">設定自動啟動</span><span class="sxs-lookup"><span data-stu-id="bc210-142">Set auto-start</span></span>
<span data-ttu-id="bc210-143">自動啟動原則可讓您指定目前實驗室 VM 應該啟動的時間。</span><span class="sxs-lookup"><span data-stu-id="bc210-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="bc210-144">在實驗室的 [組態和原則] 刀鋒視窗上，選取 [自動啟動]。</span><span class="sxs-lookup"><span data-stu-id="bc210-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![自動啟動](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="bc210-146">選取 [開啟] 來啟用此原則，以及選取 [關閉] 來停用它。</span><span class="sxs-lookup"><span data-stu-id="bc210-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="bc210-147">如果您啟用這個原則，請指定排定的啟動時間、時區和該時間適用於星期幾。</span><span class="sxs-lookup"><span data-stu-id="bc210-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="bc210-148">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="bc210-148">Select **Save**.</span></span>

    <span data-ttu-id="bc210-149">這個原則一經啟用，就不會自動套用到目前實驗室中的任何 VM。</span><span class="sxs-lookup"><span data-stu-id="bc210-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="bc210-150">若要將這項設定套用至特定的 VM，請開啟 VM 的刀鋒視窗並變更其 [自動啟動]  設定。</span><span class="sxs-lookup"><span data-stu-id="bc210-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bc210-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc210-151">Next steps</span></span>

- <span data-ttu-id="bc210-152">[在 Azure DevTest Labs 中定義實驗室原則](devtest-lab-set-lab-policy.md) - 了解如何修改其他實驗室原則</span><span class="sxs-lookup"><span data-stu-id="bc210-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
