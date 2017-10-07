---
title: "aaaService 的 Azure Batch 配額與限制 |Microsoft 文件"
description: "深入了解預設 Azure Batch 配額、 限制和條件約束，及如何 toorequest 配額，以提升"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="32520-103">Batch 服務配額和限制</span><span class="sxs-lookup"><span data-stu-id="32520-103">Batch service quotas and limits</span></span>

<span data-ttu-id="32520-104">做為與其他 Azure 服務，會有限制某些 hello 批次服務相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="32520-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="32520-105">許多這些限制會套用由 Azure hello 訂用帳戶或帳戶層級的預設配額。</span><span class="sxs-lookup"><span data-stu-id="32520-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="32520-106">本文將討論這些預設值，以及如何申請加大配額。</span><span class="sxs-lookup"><span data-stu-id="32520-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="32520-107">當您設計和相應增加您的 Batch 工作負載時，請記住這些配額。</span><span class="sxs-lookup"><span data-stu-id="32520-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="32520-108">比方說，如果您的集區未達到您所指定的運算節點的 hello 目標數目，您可能已達到 hello 核心配額限制您的 Batch 帳戶或區域的 VM 核心配額訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="32520-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="32520-109">您可以在單一批次帳戶，執行多個批次工作負載或散發您的工作負載中 hello 的批次帳戶中相同的訂用帳戶，但位於不同的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="32520-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="32520-110">如果您計劃 toorun 生產工作負載，批次中的，您可能需要 tooincrease 一或多個上述 hello 預設 hello 配額。</span><span class="sxs-lookup"><span data-stu-id="32520-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="32520-111">如果您想 tooraise 配額時，您可以開啟線上[客戶支援要求](#increase-a-quota)不收費。</span><span class="sxs-lookup"><span data-stu-id="32520-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="32520-112">配額是一種信用限制，不是容量保證。</span><span class="sxs-lookup"><span data-stu-id="32520-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="32520-113">如果您有大規模的容量需求，請連絡 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="32520-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="32520-114">資源配額</span><span class="sxs-lookup"><span data-stu-id="32520-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="32520-115">使用者訂用帳戶模式中的配額</span><span class="sxs-lookup"><span data-stu-id="32520-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="32520-116">批次帳戶集區配置模式下設定得**使用者訂用帳戶**、 批次 Vm 和其他資源，例如儲存體帳戶、 建立集區時，直接在您的訂用帳戶中建立。</span><span class="sxs-lookup"><span data-stu-id="32520-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="32520-117">hello Azure 批次核心配額不適用 tooan 帳戶在此模式中建立。</span><span class="sxs-lookup"><span data-stu-id="32520-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="32520-118">相反地，會套用您地區計算核心和其他資源的訂用帳戶中的 hello 配額。</span><span class="sxs-lookup"><span data-stu-id="32520-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="32520-119">深入了解 [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)中的配額。</span><span class="sxs-lookup"><span data-stu-id="32520-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="32520-120">在規劃資源使用狀況，在使用者訂用帳戶模式中建立的帳戶時，注意 hello 下列批次 （在加法 toocompute 核心） 的資源所需每 40 Linux Vm 或 20 Windows Vm:</span><span class="sxs-lookup"><span data-stu-id="32520-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="32520-121">資源</span><span class="sxs-lookup"><span data-stu-id="32520-121">Resource</span></span> | <span data-ttu-id="32520-122">配額</span><span class="sxs-lookup"><span data-stu-id="32520-122">Quota</span></span> | <span data-ttu-id="32520-123">提供者</span><span class="sxs-lookup"><span data-stu-id="32520-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="32520-124">一個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="32520-124">One storage account</span></span> | <span data-ttu-id="32520-125">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="32520-125">Storage Accounts</span></span> | <span data-ttu-id="32520-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="32520-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="32520-127">一個公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="32520-127">One public IP address</span></span> | <span data-ttu-id="32520-128">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="32520-128">Public IP Addresses</span></span> | <span data-ttu-id="32520-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="32520-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="32520-130">一個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="32520-130">One virtual network</span></span> | <span data-ttu-id="32520-131">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="32520-131">Virtual Networks</span></span> | <span data-ttu-id="32520-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="32520-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="32520-133">一個網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="32520-133">One network security group</span></span> | <span data-ttu-id="32520-134">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="32520-134">Network Security Groups</span></span> | <span data-ttu-id="32520-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="32520-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="32520-136">一個虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="32520-136">One virtual machine scale set</span></span> | <span data-ttu-id="32520-137">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="32520-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="32520-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="32520-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="32520-139">一個負載平衡器</span><span class="sxs-lookup"><span data-stu-id="32520-139">One load balancer</span></span> | <span data-ttu-id="32520-140">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="32520-140">Load Balancers</span></span> | <span data-ttu-id="32520-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="32520-141">Microsoft.Network</span></span> | 

<span data-ttu-id="32520-142">在地區層級或每個 VM 系列 hello 核心配額應該集相應 toohello VM 大小所需的程式批次集區或集區：</span><span class="sxs-lookup"><span data-stu-id="32520-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="32520-143">Quota</span><span class="sxs-lookup"><span data-stu-id="32520-143">Quota</span></span> | <span data-ttu-id="32520-144">提供者</span><span class="sxs-lookup"><span data-stu-id="32520-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="32520-145">地區核心總數</span><span class="sxs-lookup"><span data-stu-id="32520-145">Total Regional Cores</span></span> | <span data-ttu-id="32520-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="32520-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="32520-147">…</span><span class="sxs-lookup"><span data-stu-id="32520-147">…</span></span> <span data-ttu-id="32520-148">系列的核心</span><span class="sxs-lookup"><span data-stu-id="32520-148">Family Cores</span></span> | <span data-ttu-id="32520-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="32520-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="32520-150">其他限制</span><span class="sxs-lookup"><span data-stu-id="32520-150">Other limits</span></span>
| <span data-ttu-id="32520-151">**Resource**</span><span class="sxs-lookup"><span data-stu-id="32520-151">**Resource**</span></span> | <span data-ttu-id="32520-152">**上限**</span><span class="sxs-lookup"><span data-stu-id="32520-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="32520-153">[並行工作](batch-parallel-node-tasks.md) </span><span class="sxs-lookup"><span data-stu-id="32520-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="32520-154">4 x 節點的核心數目</span><span class="sxs-lookup"><span data-stu-id="32520-154">4 x number of node cores</span></span> |
| <span data-ttu-id="32520-155">[應用程式](batch-application-packages.md) </span><span class="sxs-lookup"><span data-stu-id="32520-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="32520-156">20</span><span class="sxs-lookup"><span data-stu-id="32520-156">20</span></span> |
| <span data-ttu-id="32520-157">每個應用程式的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="32520-157">Application packages per application</span></span> |<span data-ttu-id="32520-158">40</span><span class="sxs-lookup"><span data-stu-id="32520-158">40</span></span> |
| <span data-ttu-id="32520-159">應用程式封裝大小 (每一個)</span><span class="sxs-lookup"><span data-stu-id="32520-159">Application package size (each)</span></span> |<span data-ttu-id="32520-160">大約 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="32520-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="32520-161">最大啟動工作大小</span><span class="sxs-lookup"><span data-stu-id="32520-161">Maximum start task size</span></span> | <span data-ttu-id="32520-162">32768 個字元<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="32520-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="32520-163"><sup>1</sup> 對於區塊 Blob 大小上限的 Azure 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="32520-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="32520-164">
<sup>2</sup> 包含資源檔案和環境變數</span><span class="sxs-lookup"><span data-stu-id="32520-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="32520-165">檢視 Batch 配額</span><span class="sxs-lookup"><span data-stu-id="32520-165">View Batch quotas</span></span>
<span data-ttu-id="32520-166">檢視您的批次帳戶配額在 hello [Azure 入口網站][portal]。</span><span class="sxs-lookup"><span data-stu-id="32520-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="32520-167">選取**批次帳戶**hello 入口網站，然後選取您感興趣的 hello Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="32520-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="32520-168">選取**屬性**hello 批次帳戶的 [功能表] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="32520-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="32520-169">hello 屬性刀鋒視窗會顯示 hello**配額**目前套用 toohello 批次帳戶</span><span class="sxs-lookup"><span data-stu-id="32520-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Batch 帳戶配額][account_quotas]

<span data-ttu-id="32520-171">對於批次建立的帳戶使用者訂用帳戶模式中，檢視 hello 與相關 hello Azure 入口網站中的訂用帳戶配額。</span><span class="sxs-lookup"><span data-stu-id="32520-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="32520-172">選取**訂閱**，選取您要用於 hello 批次帳戶的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="32520-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="32520-173">在 hello**訂用帳戶**刀鋒視窗中，選取**使用量 + 配額**。</span><span class="sxs-lookup"><span data-stu-id="32520-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="32520-174">增加配額</span><span class="sxs-lookup"><span data-stu-id="32520-174">Increase a quota</span></span>
<span data-ttu-id="32520-175">請遵循這些步驟 toorequest，配額增加您的 Batch 帳戶或訂用帳戶使用 hello [Azure 入口網站][portal]。</span><span class="sxs-lookup"><span data-stu-id="32520-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="32520-176">hello 的類型增加配額取決於您的 Batch 帳戶 hello 集區配置模式。</span><span class="sxs-lookup"><span data-stu-id="32520-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="32520-177">增加 Batch 的核心配額</span><span class="sxs-lookup"><span data-stu-id="32520-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="32520-178">如果您的 Batch 帳戶中建立**批次服務**模式中，請遵循這些步驟 toorequest 批次核心配額增加：</span><span class="sxs-lookup"><span data-stu-id="32520-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="32520-179">選取 hello**說明 + 支援**入口網站儀表板、 磚或 hello 問號 (**？**) 中的 hello 入口網站的 hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="32520-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="32520-180">選取 [新增支援要求] > [基本]。</span><span class="sxs-lookup"><span data-stu-id="32520-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="32520-181">在 hello**基本概念**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="32520-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="32520-182">a.</span><span class="sxs-lookup"><span data-stu-id="32520-182">a.</span></span> <span data-ttu-id="32520-183">**問題類型** > **配額**</span><span class="sxs-lookup"><span data-stu-id="32520-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="32520-184">b.</span><span class="sxs-lookup"><span data-stu-id="32520-184">b.</span></span> <span data-ttu-id="32520-185">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="32520-185">Select your subscription.</span></span>
   
    <span data-ttu-id="32520-186">c.</span><span class="sxs-lookup"><span data-stu-id="32520-186">c.</span></span> <span data-ttu-id="32520-187">**配額類型** > **批次**</span><span class="sxs-lookup"><span data-stu-id="32520-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="32520-188">d.</span><span class="sxs-lookup"><span data-stu-id="32520-188">d.</span></span> <span data-ttu-id="32520-189">**支援方案** > **配額支援 - 已包含**</span><span class="sxs-lookup"><span data-stu-id="32520-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="32520-190">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="32520-190">Click **Next**.</span></span>
4. <span data-ttu-id="32520-191">在 hello**問題**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="32520-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="32520-192">a.</span><span class="sxs-lookup"><span data-stu-id="32520-192">a.</span></span> <span data-ttu-id="32520-193">選取**嚴重性**根據 tooyour[業務衝擊][support_sev]。</span><span class="sxs-lookup"><span data-stu-id="32520-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="32520-194">b.</span><span class="sxs-lookup"><span data-stu-id="32520-194">b.</span></span> <span data-ttu-id="32520-195">在**詳細資料**，指定您想要 toochange、 hello 批次帳戶名稱和 hello 新限制每個配額。</span><span class="sxs-lookup"><span data-stu-id="32520-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="32520-196">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="32520-196">Click **Next**.</span></span>
5. <span data-ttu-id="32520-197">在 hello**連絡資訊**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="32520-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="32520-198">a.</span><span class="sxs-lookup"><span data-stu-id="32520-198">a.</span></span> <span data-ttu-id="32520-199">選取 [偏好的連絡方式]。</span><span class="sxs-lookup"><span data-stu-id="32520-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="32520-200">b.</span><span class="sxs-lookup"><span data-stu-id="32520-200">b.</span></span> <span data-ttu-id="32520-201">請確認，然後輸入所需的 hello 連絡人詳細資料。</span><span class="sxs-lookup"><span data-stu-id="32520-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="32520-202">按一下**建立**toosubmit hello 支援要求。</span><span class="sxs-lookup"><span data-stu-id="32520-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="32520-203">一旦您上傳支援要求，Azure 支援會與您連絡。</span><span class="sxs-lookup"><span data-stu-id="32520-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="32520-204">請注意，完成 hello 要求可以佔用 too2 工作日。</span><span class="sxs-lookup"><span data-stu-id="32520-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="32520-205">增加訂用帳戶核心配額</span><span class="sxs-lookup"><span data-stu-id="32520-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="32520-206">如果您是在**使用者訂用帳戶**模式中建立 Batch 帳戶，而且您需要其他地區或 VM 系列核心，請要求增加您訂用帳戶中的配額。</span><span class="sxs-lookup"><span data-stu-id="32520-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="32520-207">如需步驟，請參閱 [Resource Manager 核心配額增加要求](../azure-supportability/resource-manager-core-quotas-request.md)。</span><span class="sxs-lookup"><span data-stu-id="32520-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="32520-208">相關主題</span><span class="sxs-lookup"><span data-stu-id="32520-208">Related topics</span></span>
* [<span data-ttu-id="32520-209">建立使用 hello Azure 入口網站的 Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="32520-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="32520-210">Azure Batch 功能概觀</span><span class="sxs-lookup"><span data-stu-id="32520-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="32520-211">Azure 訂用帳戶和服務限制、配額與限制</span><span class="sxs-lookup"><span data-stu-id="32520-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
