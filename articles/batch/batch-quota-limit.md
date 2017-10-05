---
title: "Azure Batch 的服務配額和限制 | Microsoft Docs"
description: "了解預設的 Azure Batch 配額、限制和條件約束，以及如何要求增加配額"
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
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="21949-103">Batch 服務配額和限制</span><span class="sxs-lookup"><span data-stu-id="21949-103">Batch service quotas and limits</span></span>

<span data-ttu-id="21949-104">如同使用其他 Azure 服務，對於與 Batch 服務相關聯的特定資源有一些限制。</span><span class="sxs-lookup"><span data-stu-id="21949-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="21949-105">這其中有許多限制是 Azure 在訂用帳戶或帳戶層級上所套用的預設配額。</span><span class="sxs-lookup"><span data-stu-id="21949-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="21949-106">本文將討論這些預設值，以及如何申請加大配額。</span><span class="sxs-lookup"><span data-stu-id="21949-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="21949-107">當您設計和相應增加您的 Batch 工作負載時，請記住這些配額。</span><span class="sxs-lookup"><span data-stu-id="21949-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="21949-108">例如，如果您的集區未觸達您所指定的計算節點目標數目，您可能已達到 Batch 帳戶的核心配額限制，或是您訂用帳戶的地區 VM 核心配額。</span><span class="sxs-lookup"><span data-stu-id="21949-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="21949-109">您可以在單一 Batch 帳戶中執行多個 Batch 工作負載，或在相同訂用帳戶 (但不同 Azure 區域) 的 Batch 帳戶之間散佈工作負載。</span><span class="sxs-lookup"><span data-stu-id="21949-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="21949-110">如果您計劃在 Batch 中執行生產工作負載，您可能需要增加一或多個高於預設值的配額。</span><span class="sxs-lookup"><span data-stu-id="21949-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="21949-111">若要加大配額，您可以開啟線上 [客戶支援要求](#increase-a-quota) ，不另外加收費用。</span><span class="sxs-lookup"><span data-stu-id="21949-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="21949-112">配額是一種信用限制，不是容量保證。</span><span class="sxs-lookup"><span data-stu-id="21949-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="21949-113">如果您有大規模的容量需求，請連絡 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="21949-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="21949-114">資源配額</span><span class="sxs-lookup"><span data-stu-id="21949-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="21949-115">使用者訂用帳戶模式中的配額</span><span class="sxs-lookup"><span data-stu-id="21949-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="21949-116">針對集區配置模式設定為**使用者訂用帳戶**的 Batch 帳戶，當集區建立時，Batch VM 和其他資源 (例如儲存體帳戶) 會直接建立在訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="21949-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="21949-117">Azure Batch 核心配額不適用於在此模式中建立的帳戶。</span><span class="sxs-lookup"><span data-stu-id="21949-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="21949-118">相反地，會套用您在地區計算核心和其他資源之訂用帳戶中的配額。</span><span class="sxs-lookup"><span data-stu-id="21949-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="21949-119">深入了解 [Azure 訂用帳戶和服務限制、配額與限制](../azure-subscription-service-limits.md)中的配額。</span><span class="sxs-lookup"><span data-stu-id="21949-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="21949-120">在規劃以使用者訂用帳戶模式所建立的帳戶之資源使用狀況時，請注意每 40 個 Linux VM 或 20 個 Windows VM 就需要下列 Batch 資源 (除了計算核心)：</span><span class="sxs-lookup"><span data-stu-id="21949-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="21949-121">資源</span><span class="sxs-lookup"><span data-stu-id="21949-121">Resource</span></span> | <span data-ttu-id="21949-122">配額</span><span class="sxs-lookup"><span data-stu-id="21949-122">Quota</span></span> | <span data-ttu-id="21949-123">提供者</span><span class="sxs-lookup"><span data-stu-id="21949-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="21949-124">一個儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="21949-124">One storage account</span></span> | <span data-ttu-id="21949-125">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="21949-125">Storage Accounts</span></span> | <span data-ttu-id="21949-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="21949-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="21949-127">一個公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="21949-127">One public IP address</span></span> | <span data-ttu-id="21949-128">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="21949-128">Public IP Addresses</span></span> | <span data-ttu-id="21949-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="21949-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="21949-130">一個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="21949-130">One virtual network</span></span> | <span data-ttu-id="21949-131">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="21949-131">Virtual Networks</span></span> | <span data-ttu-id="21949-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="21949-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="21949-133">一個網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="21949-133">One network security group</span></span> | <span data-ttu-id="21949-134">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="21949-134">Network Security Groups</span></span> | <span data-ttu-id="21949-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="21949-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="21949-136">一個虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="21949-136">One virtual machine scale set</span></span> | <span data-ttu-id="21949-137">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="21949-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="21949-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="21949-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="21949-139">一個負載平衡器</span><span class="sxs-lookup"><span data-stu-id="21949-139">One load balancer</span></span> | <span data-ttu-id="21949-140">負載平衡器</span><span class="sxs-lookup"><span data-stu-id="21949-140">Load Balancers</span></span> | <span data-ttu-id="21949-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="21949-141">Microsoft.Network</span></span> | 

<span data-ttu-id="21949-142">區域層級或每個 VM 系列的核心配額應根據您的 Batch 集區或集區所需的 VM 大小來設定︰</span><span class="sxs-lookup"><span data-stu-id="21949-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="21949-143">配額</span><span class="sxs-lookup"><span data-stu-id="21949-143">Quota</span></span> | <span data-ttu-id="21949-144">提供者</span><span class="sxs-lookup"><span data-stu-id="21949-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="21949-145">地區核心總數</span><span class="sxs-lookup"><span data-stu-id="21949-145">Total Regional Cores</span></span> | <span data-ttu-id="21949-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="21949-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="21949-147">…</span><span class="sxs-lookup"><span data-stu-id="21949-147">…</span></span> <span data-ttu-id="21949-148">系列的核心</span><span class="sxs-lookup"><span data-stu-id="21949-148">Family Cores</span></span> | <span data-ttu-id="21949-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="21949-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="21949-150">其他限制</span><span class="sxs-lookup"><span data-stu-id="21949-150">Other limits</span></span>
| <span data-ttu-id="21949-151">**Resource**</span><span class="sxs-lookup"><span data-stu-id="21949-151">**Resource**</span></span> | <span data-ttu-id="21949-152">**上限**</span><span class="sxs-lookup"><span data-stu-id="21949-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="21949-153">[並行工作](batch-parallel-node-tasks.md) </span><span class="sxs-lookup"><span data-stu-id="21949-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="21949-154">4 x 節點的核心數目</span><span class="sxs-lookup"><span data-stu-id="21949-154">4 x number of node cores</span></span> |
| <span data-ttu-id="21949-155">[應用程式](batch-application-packages.md) </span><span class="sxs-lookup"><span data-stu-id="21949-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="21949-156">20</span><span class="sxs-lookup"><span data-stu-id="21949-156">20</span></span> |
| <span data-ttu-id="21949-157">每個應用程式的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="21949-157">Application packages per application</span></span> |<span data-ttu-id="21949-158">40</span><span class="sxs-lookup"><span data-stu-id="21949-158">40</span></span> |
| <span data-ttu-id="21949-159">應用程式封裝大小 (每一個)</span><span class="sxs-lookup"><span data-stu-id="21949-159">Application package size (each)</span></span> |<span data-ttu-id="21949-160">大約 195 GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="21949-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="21949-161">最大啟動工作大小</span><span class="sxs-lookup"><span data-stu-id="21949-161">Maximum start task size</span></span> | <span data-ttu-id="21949-162">32768 個字元<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="21949-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="21949-163"><sup>1</sup> 對於區塊 Blob 大小上限的 Azure 儲存體限制</span><span class="sxs-lookup"><span data-stu-id="21949-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="21949-164">
<sup>2</sup> 包含資源檔案和環境變數</span><span class="sxs-lookup"><span data-stu-id="21949-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="21949-165">檢視 Batch 配額</span><span class="sxs-lookup"><span data-stu-id="21949-165">View Batch quotas</span></span>
<span data-ttu-id="21949-166">在 [Azure 入口網站][portal]中檢視您的 Batch 帳戶配額。</span><span class="sxs-lookup"><span data-stu-id="21949-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="21949-167">在入口網站中選取 [Batch 帳戶]  ，然後選取您感興趣的 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="21949-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="21949-168">在 Batch 帳戶的功能表刀鋒視窗上選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="21949-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="21949-169">[屬性] 刀鋒視窗會顯示目前套用至 Batch 帳戶的「配額」 </span><span class="sxs-lookup"><span data-stu-id="21949-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Batch 帳戶配額][account_quotas]

<span data-ttu-id="21949-171">針對在使用者訂用帳戶模式中建立的 Batch 帳戶，可在 Azure 入口網站中檢視相關的訂用帳戶配額。</span><span class="sxs-lookup"><span data-stu-id="21949-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="21949-172">選取 [訂用帳戶]，然後選取您要用於 Batch 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="21949-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="21949-173">在 [訂用帳戶] 刀鋒視窗中，選取 [使用量 + 配額]。</span><span class="sxs-lookup"><span data-stu-id="21949-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="21949-174">增加配額</span><span class="sxs-lookup"><span data-stu-id="21949-174">Increase a quota</span></span>
<span data-ttu-id="21949-175">使用 [Azure 入口網站][portal]，遵循下列步驟來要求增加您 Batch 帳戶或訂用帳戶的配額。</span><span class="sxs-lookup"><span data-stu-id="21949-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="21949-176">增加配額的類型取決於您 Batch 帳戶的集區配置模式。</span><span class="sxs-lookup"><span data-stu-id="21949-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="21949-177">增加 Batch 的核心配額</span><span class="sxs-lookup"><span data-stu-id="21949-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="21949-178">如果您是在 **Batch 服務**模式中建立 Batch 帳戶，請遵循下列步驟來要求增加 Batch 的核心配額︰</span><span class="sxs-lookup"><span data-stu-id="21949-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="21949-179">選取入口網站儀表板上的 [說明 + 支援] 圖格或入口網站右上角的問號 (**？**)。</span><span class="sxs-lookup"><span data-stu-id="21949-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="21949-180">選取 [新增支援要求] > [基本]。</span><span class="sxs-lookup"><span data-stu-id="21949-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="21949-181">在 [基本]  刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="21949-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="21949-182">a.</span><span class="sxs-lookup"><span data-stu-id="21949-182">a.</span></span> <span data-ttu-id="21949-183">**問題類型** > **配額**</span><span class="sxs-lookup"><span data-stu-id="21949-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="21949-184">b.</span><span class="sxs-lookup"><span data-stu-id="21949-184">b.</span></span> <span data-ttu-id="21949-185">選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="21949-185">Select your subscription.</span></span>
   
    <span data-ttu-id="21949-186">c.</span><span class="sxs-lookup"><span data-stu-id="21949-186">c.</span></span> <span data-ttu-id="21949-187">**配額類型** > **批次**</span><span class="sxs-lookup"><span data-stu-id="21949-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="21949-188">d.</span><span class="sxs-lookup"><span data-stu-id="21949-188">d.</span></span> <span data-ttu-id="21949-189">**支援方案** > **配額支援 - 已包含**</span><span class="sxs-lookup"><span data-stu-id="21949-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="21949-190">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="21949-190">Click **Next**.</span></span>
4. <span data-ttu-id="21949-191">在 [問題]  刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="21949-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="21949-192">a.</span><span class="sxs-lookup"><span data-stu-id="21949-192">a.</span></span> <span data-ttu-id="21949-193">根據[商業影響][support_sev]選取 [嚴重性]。</span><span class="sxs-lookup"><span data-stu-id="21949-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="21949-194">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="21949-194">b.</span></span> <span data-ttu-id="21949-195">在 [詳細資料] 中，指定每個您想要變更的配額、Batch 帳戶名稱和新限制。</span><span class="sxs-lookup"><span data-stu-id="21949-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="21949-196">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="21949-196">Click **Next**.</span></span>
5. <span data-ttu-id="21949-197">在 [連絡資訊]  刀鋒視窗上：</span><span class="sxs-lookup"><span data-stu-id="21949-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="21949-198">a.</span><span class="sxs-lookup"><span data-stu-id="21949-198">a.</span></span> <span data-ttu-id="21949-199">選取 [偏好的連絡方式]。</span><span class="sxs-lookup"><span data-stu-id="21949-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="21949-200">b.</span><span class="sxs-lookup"><span data-stu-id="21949-200">b.</span></span> <span data-ttu-id="21949-201">確認並輸入必要的連絡人詳細資料。</span><span class="sxs-lookup"><span data-stu-id="21949-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="21949-202">按一下 [建立]  提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="21949-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="21949-203">一旦您上傳支援要求，Azure 支援會與您連絡。</span><span class="sxs-lookup"><span data-stu-id="21949-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="21949-204">請注意，完成要求最多需要花費 2 個工作天。</span><span class="sxs-lookup"><span data-stu-id="21949-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="21949-205">增加訂用帳戶核心配額</span><span class="sxs-lookup"><span data-stu-id="21949-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="21949-206">如果您是在**使用者訂用帳戶**模式中建立 Batch 帳戶，而且您需要其他地區或 VM 系列核心，請要求增加您訂用帳戶中的配額。</span><span class="sxs-lookup"><span data-stu-id="21949-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="21949-207">如需步驟，請參閱 [Resource Manager 核心配額增加要求](../azure-supportability/resource-manager-core-quotas-request.md)。</span><span class="sxs-lookup"><span data-stu-id="21949-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="21949-208">相關主題</span><span class="sxs-lookup"><span data-stu-id="21949-208">Related topics</span></span>
* [<span data-ttu-id="21949-209">使用 Azure 入口網站建立 Azure Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="21949-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="21949-210">Azure Batch 功能概觀</span><span class="sxs-lookup"><span data-stu-id="21949-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="21949-211">Azure 訂用帳戶和服務限制、配額與限制</span><span class="sxs-lookup"><span data-stu-id="21949-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
