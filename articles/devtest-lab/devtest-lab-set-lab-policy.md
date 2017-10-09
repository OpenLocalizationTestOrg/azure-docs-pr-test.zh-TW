---
title: "在 Azure DevTest Labs aaaManage 實驗室原則 |Microsoft 文件"
description: "深入了解如何 toodefine 實驗室原則，例如 VM 大小，請每位使用者的最大 Vm 和關機自動化。"
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
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="eb680-103">在 Azure DevTest Labs 中管理實驗室的所有原則</span><span class="sxs-lookup"><span data-stu-id="eb680-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="eb680-104">Azure DevTest Labs 讓您管理每個實驗室的原則 (設定)，以控制實驗室的成本並儘可能避免浪費。</span><span class="sxs-lookup"><span data-stu-id="eb680-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="eb680-105">本文將逐步的詳細說明如何 tooset 每個原則。</span><span class="sxs-lookup"><span data-stu-id="eb680-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="eb680-106">設定允許的虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="eb680-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="eb680-107">hello 設定 hello 原則允許 VM 大小可協助讓您 toospecify hello 實驗室中允許的 VM 大小會浪費 toominimize 實驗室。</span><span class="sxs-lookup"><span data-stu-id="eb680-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="eb680-108">如果啟用這個原則，則只有從此清單中的 VM 大小可以是使用的 toocreate Vm。</span><span class="sxs-lookup"><span data-stu-id="eb680-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="eb680-109">在 hello 實驗室**組態和原則**刀鋒視窗中，選取**允許虛擬機器大小**。</span><span class="sxs-lookup"><span data-stu-id="eb680-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![允許的虛擬機器大小](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="eb680-111">選取**上**tooenable 此原則，和**關閉**toodisable 它。</span><span class="sxs-lookup"><span data-stu-id="eb680-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="eb680-112">如果啟用這個原則，請選取一或多個可在實驗室中建立的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="eb680-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="eb680-113">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="eb680-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="eb680-114">設定每位使用者的虛擬機器數目</span><span class="sxs-lookup"><span data-stu-id="eb680-114">Set virtual machines per user</span></span>
<span data-ttu-id="eb680-115">hello 原則**每位使用者的虛擬機器**可讓您 toospecify hello 的 Vm 數目上限，您可以建立個別的使用者。</span><span class="sxs-lookup"><span data-stu-id="eb680-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="eb680-116">如果使用者嘗試 toocreate 或宣告 VM 在達到 hello 使用者限制時，錯誤訊息會指出該 VM 無法建立/宣告的 hello。</span><span class="sxs-lookup"><span data-stu-id="eb680-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="eb680-117">在 hello 實驗室**組態和原則**功能表上，選取**每位使用者的虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="eb680-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![每位使用者的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="eb680-119">選取**是**toolimit hello Vm 數目每位使用者。</span><span class="sxs-lookup"><span data-stu-id="eb680-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="eb680-120">如果您不想 toolimit hello Vm 數目每位使用者，選取**否**。</span><span class="sxs-lookup"><span data-stu-id="eb680-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="eb680-121">如果您選取**是**，輸入數字值，指出 hello 可建立或由使用者宣告的 Vm 數目上限。</span><span class="sxs-lookup"><span data-stu-id="eb680-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="eb680-122">選取**是**toolimit hello 數目可以使用 SSD （固態磁碟） 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="eb680-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="eb680-123">如果您不想 toolimit hello 數目可以使用 SSD 的 Vm，選取**否**。</span><span class="sxs-lookup"><span data-stu-id="eb680-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="eb680-124">如果您選取**是**，輸入值，指出 hello 可使用 SSD 來建立的 Vm 數目上限。</span><span class="sxs-lookup"><span data-stu-id="eb680-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="eb680-125">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="eb680-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="eb680-126">設定每個實驗室的虛擬機器數目</span><span class="sxs-lookup"><span data-stu-id="eb680-126">Set virtual machines per lab</span></span>
<span data-ttu-id="eb680-127">hello 原則**每個實驗室的虛擬機器**可讓您 toospecify hello 的 Vm 數目上限可建立 hello 目前實驗室。</span><span class="sxs-lookup"><span data-stu-id="eb680-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="eb680-128">如果使用者嘗試 toocreate VM，在達到 hello 實驗室限制時，錯誤訊息指出無法建立 VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="eb680-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="eb680-129">在 hello 實驗室**組態和原則**功能表上，選取**每個實驗室的虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="eb680-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![每個實驗室的虛擬機器數目](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="eb680-131">選取**是**toolimit hello Vm 數目每個實驗室。</span><span class="sxs-lookup"><span data-stu-id="eb680-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="eb680-132">如果您不想 toolimit hello Vm 數目每個實驗室，請選取**否**。</span><span class="sxs-lookup"><span data-stu-id="eb680-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="eb680-133">如果您選取**是**，輸入數字值，指出 hello 可建立或由使用者宣告的 Vm 數目上限。</span><span class="sxs-lookup"><span data-stu-id="eb680-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="eb680-134">選取**是**toolimit hello 數目可以使用 SSD （固態磁碟） 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="eb680-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="eb680-135">如果您不想 toolimit hello 數目可以使用 SSD 的 Vm，選取**否**。</span><span class="sxs-lookup"><span data-stu-id="eb680-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="eb680-136">如果您選取**是**，輸入值，指出 hello 可使用 SSD 來建立的 Vm 數目上限。</span><span class="sxs-lookup"><span data-stu-id="eb680-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="eb680-137">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="eb680-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="eb680-138">設定自動關機</span><span class="sxs-lookup"><span data-stu-id="eb680-138">Set auto-shutdown</span></span>
<span data-ttu-id="eb680-139">hello 自動關閉原則可幫助 toominimize 實驗室可以讓您在本實驗室 Vm 關機的 toospecify hello 時間會浪費。</span><span class="sxs-lookup"><span data-stu-id="eb680-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="eb680-140">在 hello 實驗室**組態和原則**刀鋒視窗中，選取**自動關機**。</span><span class="sxs-lookup"><span data-stu-id="eb680-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![自動關機](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="eb680-142">選取**上**tooenable 此原則，和**關閉**toodisable 它。</span><span class="sxs-lookup"><span data-stu-id="eb680-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="eb680-143">如果您啟用這個原則，指定下所有 Vm 的 hello 時間 （和時區） tooshut hello 目前實驗室中。</span><span class="sxs-lookup"><span data-stu-id="eb680-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="eb680-144">指定**是**或**否**hello 選項 toosend 通知 15 分鐘先前 toohello 指定自動關機時間。</span><span class="sxs-lookup"><span data-stu-id="eb680-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="eb680-145">如果您指定**是**，輸入 webhook URL 端點 tooreceive hello 通知。</span><span class="sxs-lookup"><span data-stu-id="eb680-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="eb680-146">如需 webhook 的詳細資訊，請參閱[建立 webhook 或 API Azure 函式](../azure-functions/functions-create-a-web-hook-or-api-function.md)。</span><span class="sxs-lookup"><span data-stu-id="eb680-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="eb680-147">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="eb680-147">Select **Save**.</span></span>

    <span data-ttu-id="eb680-148">根據預設，一旦啟用此原則適用於 tooall hello 目前實驗室中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="eb680-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="eb680-149">這項設定特定 VM 中，開啟 tooremove hello VM 刀鋒視窗，然後變更其**自動關機**設定</span><span class="sxs-lookup"><span data-stu-id="eb680-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="eb680-150">設定自動啟動</span><span class="sxs-lookup"><span data-stu-id="eb680-150">Set auto-start</span></span>
<span data-ttu-id="eb680-151">hello 自動啟動原則可讓您 toospecify 時應該啟動 hello 目前實驗室中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="eb680-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="eb680-152">在 hello 實驗室**組態和原則**刀鋒視窗中，選取**自動啟動**。</span><span class="sxs-lookup"><span data-stu-id="eb680-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![自動啟動](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="eb680-154">選取**上**tooenable 此原則，和**關閉**toodisable 它。</span><span class="sxs-lookup"><span data-stu-id="eb680-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="eb680-155">如果您啟用這個原則，指定 hello 排定的開始時間、 時區、 和 hello 星期幾 hello 時間適用的 hello。</span><span class="sxs-lookup"><span data-stu-id="eb680-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="eb680-156">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="eb680-156">Select **Save**.</span></span>

    <span data-ttu-id="eb680-157">啟用之後，此原則不會自動套用的 tooany Vm hello 目前實驗室中。</span><span class="sxs-lookup"><span data-stu-id="eb680-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="eb680-158">tooapply 這個設定 tooa 特定 VM、 開啟 hello VM 刀鋒視窗，然後變更其**自動啟動**設定</span><span class="sxs-lookup"><span data-stu-id="eb680-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="eb680-159">設定到期日期</span><span class="sxs-lookup"><span data-stu-id="eb680-159">Set expiration date</span></span>
<span data-ttu-id="eb680-160">您可以設定到期日的日期時您[建立 hello VM](devtest-lab-add-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="eb680-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="eb680-161">在**進階設定**，選擇 hello 行事曆圖示 toospecify 日期所在 hello VM 將會自動刪除。</span><span class="sxs-lookup"><span data-stu-id="eb680-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="eb680-162">根據預設，永遠不會過期 hello VM。</span><span class="sxs-lookup"><span data-stu-id="eb680-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="eb680-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb680-163">Next steps</span></span>
<span data-ttu-id="eb680-164">一旦您定義並套用 hello 各種 VM 原則設定您的實驗室，以下是一些事情 tootry 下一步：</span><span class="sxs-lookup"><span data-stu-id="eb680-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="eb680-165">[了解共用的 IP 位址](devtest-lab-shared-ip.md)-說明如何共用的 IP 位址為使用中的公用 IP 位址需要的 tooconnect tooyour 實驗室 Vm 的 DevTest Labs toominimize hello 數目。</span><span class="sxs-lookup"><span data-stu-id="eb680-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="eb680-166">[設定成本管理](devtest-lab-configure-cost-management.md)-說明如何 toouse hello**每月估計成本趨勢**圖表</span><span class="sxs-lookup"><span data-stu-id="eb680-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="eb680-167">tooview hello 目前月份的估計的成本至今和投射 hello 月底的成本。</span><span class="sxs-lookup"><span data-stu-id="eb680-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="eb680-168">[建立自訂映像](devtest-lab-create-template.md) - 當您建立 VM 時，您要指定一個基本映像，它可以是自訂映像或 Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="eb680-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="eb680-169">本文說明如何 toocreate 自訂映像從 VHD 檔案。</span><span class="sxs-lookup"><span data-stu-id="eb680-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="eb680-170">[設定 Marketplace 映像](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs 支援根據 Azure Marketplace 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="eb680-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="eb680-171">本文將說明如何 toospecify 它，如果有的話，可以是 Azure Marketplace 映像在實驗室中建立 Vm 時使用。</span><span class="sxs-lookup"><span data-stu-id="eb680-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="eb680-172">[在實驗室中建立的 VM](devtest-lab-add-vm-with-artifacts.md) -說明如何 toocreate 將 VM 的基本映像從 (可能是自訂或 Marketplace)，以及如何 toowork 連同成品放在 VM 中。</span><span class="sxs-lookup"><span data-stu-id="eb680-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

