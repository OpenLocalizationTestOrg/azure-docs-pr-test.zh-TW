---
title: "在 Azure DevTest Labs 中管理實驗室原則 | Microsoft Docs"
description: "了解如何定義實驗室原則，例如 VM 大小、每位使用者的 VM 數目上限，以及自動關機。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="27e57-103">在 Azure DevTest Labs 中管理實驗室的所有原則</span><span class="sxs-lookup"><span data-stu-id="27e57-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="27e57-104">Azure DevTest Labs 讓您管理每個實驗室的原則 (設定)，以控制實驗室的成本並儘可能避免浪費。</span><span class="sxs-lookup"><span data-stu-id="27e57-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="27e57-105">本文逐步地詳細說明如何設定每個原則。</span><span class="sxs-lookup"><span data-stu-id="27e57-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="27e57-106">設定允許的虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="27e57-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="27e57-107">設定允許的 VM 大小的原則有助於將實驗室的成本浪費降至最低，方式是讓您指定實驗室中允許的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="27e57-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="27e57-108">如果啟用此原則，就只能使用此清單中的 VM 大小來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="27e57-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="27e57-109">在實驗室的 [組態和原則] 刀鋒視窗上，選取 [允許的虛擬機器大小]。</span><span class="sxs-lookup"><span data-stu-id="27e57-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![允許的虛擬機器大小](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="27e57-111">選取 [開啟] 來啟用此原則，以及選取 [關閉] 來停用它。</span><span class="sxs-lookup"><span data-stu-id="27e57-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="27e57-112">如果啟用這個原則，請選取一或多個可在實驗室中建立的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="27e57-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="27e57-113">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="27e57-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="27e57-114">設定每位使用者的虛擬機器數目</span><span class="sxs-lookup"><span data-stu-id="27e57-114">Set virtual machines per user</span></span>
<span data-ttu-id="27e57-115">[每位使用者的虛擬機器數目]  原則可讓您指定個別使用者可以建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="27e57-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="27e57-116">當達到使用者限制時，如果使用者嘗試建立或宣告 VM，就會顯示錯誤訊息，指出無法建立/宣告 VM。</span><span class="sxs-lookup"><span data-stu-id="27e57-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="27e57-117">在實驗室的 [組態和原則] 功能表上，選取 [每位使用者的虛擬機器數目]。</span><span class="sxs-lookup"><span data-stu-id="27e57-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![每位使用者的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="27e57-119">選取 [是]，以限制每個使用者的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="27e57-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="27e57-120">如果不想限制每個使用者的 VM 數目，請選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="27e57-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="27e57-121">如果您選取 [是]，請輸入數值，指出使用者可建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="27e57-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="27e57-122">選取 [是]，以限制可使用 SSD (固態硬碟) 的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="27e57-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="27e57-123">如果不想限制可使用 SSD 的 VM 數目，請選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="27e57-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="27e57-124">如果您選取 [是]，請輸入一個值，指出可使用 SSD 建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="27e57-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="27e57-125">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="27e57-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="27e57-126">設定每個實驗室的虛擬機器數目</span><span class="sxs-lookup"><span data-stu-id="27e57-126">Set virtual machines per lab</span></span>
<span data-ttu-id="27e57-127">[每個實驗室的虛擬機器數目]  原則可讓您指定可為目前實驗室建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="27e57-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="27e57-128">當達到實驗室限制時，如果使用者嘗試建立 VM，就會顯示錯誤訊息，指出無法建立 VM。</span><span class="sxs-lookup"><span data-stu-id="27e57-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="27e57-129">在實驗室的 [組態和原則] 功能表上，選取 [每個實驗室的虛擬機器數目]。</span><span class="sxs-lookup"><span data-stu-id="27e57-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![每個實驗室的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="27e57-131">選取 [是]，以限制每個實驗室的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="27e57-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="27e57-132">如果不想限制每個實驗室的 VM 數目，請選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="27e57-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="27e57-133">如果您選取 [是]，請輸入數值，指出使用者可建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="27e57-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="27e57-134">選取 [是]，以限制可使用 SSD (固態硬碟) 的 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="27e57-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="27e57-135">如果不想限制可使用 SSD 的 VM 數目，請選取 [否]。</span><span class="sxs-lookup"><span data-stu-id="27e57-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="27e57-136">如果您選取 [是]，請輸入一個值，指出可使用 SSD 建立的 VM 數目上限。</span><span class="sxs-lookup"><span data-stu-id="27e57-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="27e57-137">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="27e57-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="27e57-138">設定自動關機</span><span class="sxs-lookup"><span data-stu-id="27e57-138">Set auto-shutdown</span></span>
<span data-ttu-id="27e57-139">自動關機原則有助於將實驗室的成本浪費降至最低，方式是讓您指定這個實驗室中 VM 的關機時間。</span><span class="sxs-lookup"><span data-stu-id="27e57-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="27e57-140">在實驗室的 [組態和原則] 刀鋒視窗上，選取 [自動關機]。</span><span class="sxs-lookup"><span data-stu-id="27e57-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![自動關機](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="27e57-142">選取 [開啟] 來啟用此原則，以及選取 [關閉] 來停用它。</span><span class="sxs-lookup"><span data-stu-id="27e57-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="27e57-143">如果您啟用這個原則，請指定時間 (和時區) 以關閉目前實驗室中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="27e57-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="27e57-144">對於在指定的自動關機時間之前 15 分鐘傳送通知的選項中，指定 [是] 或 [否]。</span><span class="sxs-lookup"><span data-stu-id="27e57-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="27e57-145">如果您指定 [是]，請輸入要接收通知的 webhook URL 端點。</span><span class="sxs-lookup"><span data-stu-id="27e57-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="27e57-146">如需 webhook 的詳細資訊，請參閱[建立 webhook 或 API Azure 函式](../azure-functions/functions-create-a-web-hook-or-api-function.md)。</span><span class="sxs-lookup"><span data-stu-id="27e57-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="27e57-147">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="27e57-147">Select **Save**.</span></span>

    <span data-ttu-id="27e57-148">根據預設，這個原則一經啟用，就會套用到目前實驗室的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="27e57-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="27e57-149">若要移除特定 VM 的這項設定，請開啟 VM 的刀鋒視窗並變更其 [自動關機]  設定。</span><span class="sxs-lookup"><span data-stu-id="27e57-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="27e57-150">設定自動啟動</span><span class="sxs-lookup"><span data-stu-id="27e57-150">Set auto-start</span></span>
<span data-ttu-id="27e57-151">自動啟動原則可讓您指定目前實驗室 VM 應該啟動的時間。</span><span class="sxs-lookup"><span data-stu-id="27e57-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="27e57-152">在實驗室的 [組態和原則] 刀鋒視窗上，選取 [自動啟動]。</span><span class="sxs-lookup"><span data-stu-id="27e57-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![自動啟動](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="27e57-154">選取 [開啟] 來啟用此原則，以及選取 [關閉] 來停用它。</span><span class="sxs-lookup"><span data-stu-id="27e57-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="27e57-155">如果您啟用這個原則，請指定排定的啟動時間、時區和該時間適用於星期幾。</span><span class="sxs-lookup"><span data-stu-id="27e57-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="27e57-156">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="27e57-156">Select **Save**.</span></span>

    <span data-ttu-id="27e57-157">這個原則一經啟用，就不會自動套用到目前實驗室中的任何 VM。</span><span class="sxs-lookup"><span data-stu-id="27e57-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="27e57-158">若要將這項設定套用至特定的 VM，請開啟 VM 的刀鋒視窗並變更其 [自動啟動]  設定。</span><span class="sxs-lookup"><span data-stu-id="27e57-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="27e57-159">設定到期日期</span><span class="sxs-lookup"><span data-stu-id="27e57-159">Set expiration date</span></span>
<span data-ttu-id="27e57-160">當您[建立 VM](devtest-lab-add-vm.md)時，可以設定到期日期。</span><span class="sxs-lookup"><span data-stu-id="27e57-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="27e57-161">在進階設定中，選擇行事曆圖示，以指定 VM 將會自動刪除的日期。</span><span class="sxs-lookup"><span data-stu-id="27e57-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="27e57-162">根據預設，VM 永遠不會到期。</span><span class="sxs-lookup"><span data-stu-id="27e57-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="27e57-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="27e57-163">Next steps</span></span>
<span data-ttu-id="27e57-164">實驗室一旦定義並套用了各種 VM 原則設定，接下來就要嘗試一些作業：</span><span class="sxs-lookup"><span data-stu-id="27e57-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="27e57-165">[了解共用 IP 位址](devtest-lab-shared-ip.md) - 說明 DevTest Labs 中如何使用共用 IP 位址，將需要連線至您的實驗室 VM 的公用 IP 位址數目減到最少。</span><span class="sxs-lookup"><span data-stu-id="27e57-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="27e57-166">[設定成本管理](devtest-lab-configure-cost-management.md) - 示範如何使用 [每月估計成本趨勢] 圖表，</span><span class="sxs-lookup"><span data-stu-id="27e57-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="27e57-167">來檢視本月到目前為止的估計成本，以及預計的月底成本。</span><span class="sxs-lookup"><span data-stu-id="27e57-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="27e57-168">[建立自訂映像](devtest-lab-create-template.md) - 當您建立 VM 時，您要指定一個基本映像，它可以是自訂映像或 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="27e57-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="27e57-169">本文會示範如何從 VHD 檔案建立自訂的映像。</span><span class="sxs-lookup"><span data-stu-id="27e57-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="27e57-170">[設定 Marketplace 映像](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs 支援根據 Azure Marketplace 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="27e57-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="27e57-171">本文會示範在實驗室中建立 VM 時，如何指定可以使用哪些 Azure Marketplace 映像 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="27e57-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="27e57-172">[在實驗室中建立 VM](devtest-lab-add-vm-with-artifacts.md) - 示範如何從基本映像 (自訂或 Marketplace) 建立 VM，以及如何使用 VM 中的構件。</span><span class="sxs-lookup"><span data-stu-id="27e57-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

