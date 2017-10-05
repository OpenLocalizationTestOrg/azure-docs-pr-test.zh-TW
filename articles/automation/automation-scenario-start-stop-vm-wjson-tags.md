---
title: "使用 JSON 格式化標籤來排程 Azure VM 狀態 | Microsoft Docs"
description: "本文示範如何在標籤上使用 JSON 字串，自動排定 VM 的啟動和關閉。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6afed5d2-e939-4749-8b2c-9312b4c16fb2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: magoedte;paulomarquesc
ms.openlocfilehash: f8d9563318c3afe299cebb7c889874392f114f84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-to-create-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="abe78-103">Azure 自動化案例：使用 JSON 格式化標籤來建立 Azure VM 啟動和關閉的排程</span><span class="sxs-lookup"><span data-stu-id="abe78-103">Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="abe78-104">客戶通常會想要排程虛擬機器的啟動與關閉，以協助減少訂用帳戶成本或支援業務和技術需求。</span><span class="sxs-lookup"><span data-stu-id="abe78-104">Customers often want to schedule the startup and shutdown of virtual machines to help reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="abe78-105">下列案例可讓您在 Azure 中的資源群組層級或虛擬機器層級，使用稱為「排程」的標籤，設定自動啟動和關閉您的 VM。</span><span class="sxs-lookup"><span data-stu-id="abe78-105">The following scenario enables you to set up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="abe78-106">您可以設定從星期日至星期六具有啟動時間和關閉時間的排程。</span><span class="sxs-lookup"><span data-stu-id="abe78-106">This schedule can be configured from Sunday to Saturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="abe78-107">我們的確有一些現成可用的選項。</span><span class="sxs-lookup"><span data-stu-id="abe78-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="abe78-108">其中包含：</span><span class="sxs-lookup"><span data-stu-id="abe78-108">These include:</span></span>

* <span data-ttu-id="abe78-109">[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) ，具有自動調整設定以讓您相應縮小或相應放大。</span><span class="sxs-lookup"><span data-stu-id="abe78-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you to scale in or out.</span></span>
* <span data-ttu-id="abe78-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) 服務，具有內建的啟動及關閉作業排程功能。</span><span class="sxs-lookup"><span data-stu-id="abe78-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has the built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="abe78-111">不過，這些選項只支援特定案例，不適用於基礎結構即服務 (IaaS) VM。</span><span class="sxs-lookup"><span data-stu-id="abe78-111">However, these options only support specific scenarios and cannot be applied to infrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="abe78-112">當 [排程] 標籤套用至資源群組時，也會套用到該資源群組內的所有虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="abe78-112">When the Schedule tag is applied to a resource group, it's also applied to all virtual machines inside that resource group.</span></span> <span data-ttu-id="abe78-113">如果排程也直接套用至 VM，則最後一個排程優先，其順序如下︰</span><span class="sxs-lookup"><span data-stu-id="abe78-113">If a schedule is also directly applied to a VM, the last schedule takes precedence in the following order:</span></span>

1. <span data-ttu-id="abe78-114">套用至資源群組的排程</span><span class="sxs-lookup"><span data-stu-id="abe78-114">Schedule applied to a resource group</span></span>
2. <span data-ttu-id="abe78-115">套用至資源群組和資源群組中虛擬機器的排程</span><span class="sxs-lookup"><span data-stu-id="abe78-115">Schedule applied to a resource group and virtual machine in the resource group</span></span>
3. <span data-ttu-id="abe78-116">套用至虛擬機器的排程</span><span class="sxs-lookup"><span data-stu-id="abe78-116">Schedule applied to a virtual machine</span></span>

<span data-ttu-id="abe78-117">此案例基本上會採用具有指定格式的 JSON 字串，並將它加入為「排程」標籤的值。</span><span class="sxs-lookup"><span data-stu-id="abe78-117">This scenario essentially takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="abe78-118">然後，Runbook 會列出所有資源群組和虛擬機器，並根據稍早所列的案例識別每個 VM 的排程。</span><span class="sxs-lookup"><span data-stu-id="abe78-118">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each VM based on the scenarios listed earlier.</span></span> <span data-ttu-id="abe78-119">接下來，它會循環執行已附加排程的 VM，並評估應採取什麼動作。</span><span class="sxs-lookup"><span data-stu-id="abe78-119">Next it loops through the VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="abe78-120">例如，它會判斷哪個 VM 需要停止、關閉或忽略。</span><span class="sxs-lookup"><span data-stu-id="abe78-120">For example, it determines which VMs need to be stopped, shut down, or ignored.</span></span>

<span data-ttu-id="abe78-121">這些 Runbook 會使用 [Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)進行驗證。</span><span class="sxs-lookup"><span data-stu-id="abe78-121">These runbooks authenticate by using the [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-the-runbooks-for-the-scenario"></a><span data-ttu-id="abe78-122">下載案例的 Runbook</span><span class="sxs-lookup"><span data-stu-id="abe78-122">Download the runbooks for the scenario</span></span>
<span data-ttu-id="abe78-123">此案例包含四個 PowerShell 工作流程 Runbook，您可以從 [TechNet 資源庫](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7)或此專案的 [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) 儲存機制下載這些 Runbook。</span><span class="sxs-lookup"><span data-stu-id="abe78-123">This scenario consists of four PowerShell Workflow runbooks that you can download from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or the [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="abe78-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="abe78-124">Runbook</span></span> | <span data-ttu-id="abe78-125">說明</span><span class="sxs-lookup"><span data-stu-id="abe78-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="abe78-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="abe78-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="abe78-127">檢查每部虛擬機器的排程，並根據排程執行關閉或啟動。</span><span class="sxs-lookup"><span data-stu-id="abe78-127">Checks each virtual machine schedule and performs shutdown or startup depending on the schedule.</span></span> |
| <span data-ttu-id="abe78-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="abe78-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="abe78-129">將排程標籤加入至 VM 或資源群組。</span><span class="sxs-lookup"><span data-stu-id="abe78-129">Adds the Schedule tag to a VM or resource group.</span></span> |
| <span data-ttu-id="abe78-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="abe78-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="abe78-131">以新的排程標籤取代現有的排程標籤以進行修改。</span><span class="sxs-lookup"><span data-stu-id="abe78-131">Modifies the existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="abe78-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="abe78-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="abe78-133">從 VM 或資源群組移除排程標籤。</span><span class="sxs-lookup"><span data-stu-id="abe78-133">Removes the Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="abe78-134">安裝和設定此案例</span><span class="sxs-lookup"><span data-stu-id="abe78-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-the-runbooks"></a><span data-ttu-id="abe78-135">安裝並發佈 Runbook</span><span class="sxs-lookup"><span data-stu-id="abe78-135">Install and publish the runbooks</span></span>
<span data-ttu-id="abe78-136">下載 Runbook 之後，您可以使用[在 Azure 自動化中建立或匯入 Runbook](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation) 中的程序匯入它們。</span><span class="sxs-lookup"><span data-stu-id="abe78-136">After downloading the runbooks, you can import them by using the procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="abe78-137">在每個 Runbook 成功匯入到您的自動化帳戶之後予以發佈。</span><span class="sxs-lookup"><span data-stu-id="abe78-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-to-the-test-resourceschedule-runbook"></a><span data-ttu-id="abe78-138">將排程加入至 Test-ResourceSchedule Runbook</span><span class="sxs-lookup"><span data-stu-id="abe78-138">Add a schedule to the Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="abe78-139">請遵循以下步驟以對 Test-ResourceSchedule Runbook 啟用排程。</span><span class="sxs-lookup"><span data-stu-id="abe78-139">Follow these steps to enable the schedule for the Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="abe78-140">這個 Runbook 會確認哪些虛擬機器應該啟動、關閉或保持原狀。</span><span class="sxs-lookup"><span data-stu-id="abe78-140">This is the runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="abe78-141">從 Azure 入口網站中，開啟您的自動化帳戶，然後按一下 [Runbook]  圖格。</span><span class="sxs-lookup"><span data-stu-id="abe78-141">From the Azure portal, open your Automation account, and then click the **Runbooks** tile.</span></span>
2. <span data-ttu-id="abe78-142">在 [Test-ResourceSchedule] 刀鋒視窗中，按一下 [排程] 圖格。</span><span class="sxs-lookup"><span data-stu-id="abe78-142">On the **Test-ResourceSchedule** blade, click the **Schedules** tile.</span></span>
3. <span data-ttu-id="abe78-143">在 [排程] 刀鋒視窗上，按一下 [加入排程]。</span><span class="sxs-lookup"><span data-stu-id="abe78-143">On the **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="abe78-144">在 [排程] 刀鋒視窗中，選取 [將排程連結至您的 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="abe78-144">On the **Schedules** blade, select **Link a schedule to your runbook**.</span></span> <span data-ttu-id="abe78-145">然後選取 [建立新的排程] 。</span><span class="sxs-lookup"><span data-stu-id="abe78-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="abe78-146">在 [新增排程] 刀鋒視窗中，輸入此排程的名稱，例如：HourlyExecution。</span><span class="sxs-lookup"><span data-stu-id="abe78-146">On the **New schedule** blade, type in the name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="abe78-147">若為 [啟動] 排程，請將開始時間設為小時遞增值。</span><span class="sxs-lookup"><span data-stu-id="abe78-147">For the schedule **Start**, set the start time to an hour increment.</span></span>
7. <span data-ttu-id="abe78-148">選取 [週期]，然後針對 [重複出現間隔] 選取 [1 小時]。</span><span class="sxs-lookup"><span data-stu-id="abe78-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="abe78-149">確認 [設定到期] 已設為 [否]，然後按一下 [建立] 以儲存新排程。</span><span class="sxs-lookup"><span data-stu-id="abe78-149">Verify that **Set expiration** is set to **No**, and then click **Create** to save your new schedule.</span></span>
9. <span data-ttu-id="abe78-150">在 [排程 Runbook] 選項刀鋒視窗中，選取 [參數與回合設定]。</span><span class="sxs-lookup"><span data-stu-id="abe78-150">On the **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="abe78-151">在 Test-ResourceSchedule 的 [參數] 刀鋒視窗中，於 [SubscriptionName] 欄位 中輸入訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="abe78-151">In the Test-ResourceSchedule **Parameters** blade, enter the name of your subscription in the **SubscriptionName** field.</span></span>  <span data-ttu-id="abe78-152">這是 Runbook 所需的唯一參數。</span><span class="sxs-lookup"><span data-stu-id="abe78-152">This is the only parameter that's required for the runbook.</span></span>  <span data-ttu-id="abe78-153">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="abe78-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="abe78-154">完成時的 Runbook 排程應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="abe78-154">The runbook schedule should look like the following when it's completed:</span></span>

![已設定的 Test-ResourceSchedule Runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-the-json-string"></a><span data-ttu-id="abe78-156">格式化 JSON 字串</span><span class="sxs-lookup"><span data-stu-id="abe78-156">Format the JSON string</span></span>
<span data-ttu-id="abe78-157">此解決方案基本上會採用具有指定格式的 JSON 字串，並將它加入為「排程」標籤的值。</span><span class="sxs-lookup"><span data-stu-id="abe78-157">This solution basically takes a JSON string with a specified format and adds it as the value for a tag called Schedule.</span></span> <span data-ttu-id="abe78-158">然後，Runbook 會列出所有資源群組和虛擬機器，並識別每個虛擬機器的排程。</span><span class="sxs-lookup"><span data-stu-id="abe78-158">Then a runbook lists all resource groups and virtual machines and identifies the schedules for each virtual machine.</span></span>

<span data-ttu-id="abe78-159">Runbook 會循環執行已附加排程的虛擬機器，並檢查應採取什麼動作。</span><span class="sxs-lookup"><span data-stu-id="abe78-159">The runbook loops over the virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="abe78-160">以下是解決方案格式化方式的範例：</span><span class="sxs-lookup"><span data-stu-id="abe78-160">The following is an example of how the solutions should be formatted:</span></span>

```json
{
    "TzId": "Eastern Standard Time",
    "0": {
        "S": "11",
        "E": "17"
    },
    "1": {
        "S": "9",
        "E": "19"
    },
    "2": {
        "S": "9",
        "E": "19"
    },
}
```

<span data-ttu-id="abe78-161">以下是此結構的部分詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="abe78-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="abe78-162">此 JSON 結構的格式已經過最佳化，可解決 Azure 中單一標籤值 256 個字元的限制。</span><span class="sxs-lookup"><span data-stu-id="abe78-162">The format of this JSON structure is optimized to work around the 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="abe78-163"> 代表虛擬機器的時區。</span><span class="sxs-lookup"><span data-stu-id="abe78-163">*TzId* represents the time zone of the virtual machine.</span></span> <span data-ttu-id="abe78-164">此識別碼可以在 PowerShell 工作階段中使用 TimeZoneInfo .NET 類別來取得--**[System.TimeZoneInfo]::GetSystemTimeZones()**。</span><span class="sxs-lookup"><span data-stu-id="abe78-164">This ID can be obtained by using the TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![PowerShell 中的 GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="abe78-166">一週日期是以零到六的數字值來表示。</span><span class="sxs-lookup"><span data-stu-id="abe78-166">Weekdays are represented with a numeric value of zero to six.</span></span> <span data-ttu-id="abe78-167">值為零等於星期日。</span><span class="sxs-lookup"><span data-stu-id="abe78-167">The value zero equals Sunday.</span></span>
   * <span data-ttu-id="abe78-168">開始時間以 **S** 屬性表示，其值採用 24 小時制的格式。</span><span class="sxs-lookup"><span data-stu-id="abe78-168">The start time is represented with the **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="abe78-169">結束或關閉時間以 **E** 屬性表示，其值採用 24 小時制的格式。</span><span class="sxs-lookup"><span data-stu-id="abe78-169">The end or shutdown time is represented with the **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="abe78-170">如果 **S** 和 **E** 屬性的值各為零 (0)，則虛擬機器會在評估時留在其目前的狀態。</span><span class="sxs-lookup"><span data-stu-id="abe78-170">If the **S** and **E** attributes each have a value of zero (0), the virtual machine will be left in its present state at the time of evaluation.</span></span>
3. <span data-ttu-id="abe78-171">如果您想要跳過一週特定一天的評估，請勿加入該週當天的區段。</span><span class="sxs-lookup"><span data-stu-id="abe78-171">If you want to skip evaluation for a specific day of the week, don’t add a section for that day of the week.</span></span> <span data-ttu-id="abe78-172">在下列範例中，只會評估星期一，而會忽略一周的其他天數：</span><span class="sxs-lookup"><span data-stu-id="abe78-172">In the following example, only Monday is evaluated, and the other days of the week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="abe78-173">標記資源群組或 VM</span><span class="sxs-lookup"><span data-stu-id="abe78-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="abe78-174">若要關閉 VM，您需要標記 VM 或其所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="abe78-174">To shut down VMs, you need to tag either the VMs or the resource groups in which they're located.</span></span> <span data-ttu-id="abe78-175">沒有「排程」標籤的虛擬機器不會進行評估。</span><span class="sxs-lookup"><span data-stu-id="abe78-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="abe78-176">因此，不會加以啟動或關閉。</span><span class="sxs-lookup"><span data-stu-id="abe78-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="abe78-177">此解決方案有兩種方式可標記資源群組或 VM。</span><span class="sxs-lookup"><span data-stu-id="abe78-177">There are two ways to tag resource groups or VMs with this solution.</span></span> <span data-ttu-id="abe78-178">您可以直接從入口網站進行。</span><span class="sxs-lookup"><span data-stu-id="abe78-178">You can do it directly from the portal.</span></span> <span data-ttu-id="abe78-179">或者，您可以使用 Add-ResourceSchedule、Update-ResourceSchedule 和 Remove-ResourceSchedule Runbook。</span><span class="sxs-lookup"><span data-stu-id="abe78-179">Or you can use the Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-the-portal"></a><span data-ttu-id="abe78-180">透過入口網站進行標記</span><span class="sxs-lookup"><span data-stu-id="abe78-180">Tag through the portal</span></span>
<span data-ttu-id="abe78-181">請依照下列步驟，在入口網站中標記虛擬機器或資源群組：</span><span class="sxs-lookup"><span data-stu-id="abe78-181">Follow these steps to tag a virtual machine or resource group in the portal:</span></span>

1. <span data-ttu-id="abe78-182">壓平合併 JSON 字串，並確認沒有任何空格。</span><span class="sxs-lookup"><span data-stu-id="abe78-182">Flatten the JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="abe78-183">您的 JSON 字串應該如下所示︰</span><span class="sxs-lookup"><span data-stu-id="abe78-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="abe78-184">針對要套用此排程的 VM 或資源群組選取 [標籤]  圖示。</span><span class="sxs-lookup"><span data-stu-id="abe78-184">Select the **Tag** icon for a VM or resource group to apply this schedule.</span></span>

   ![VM 標籤選項](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="abe78-186">標籤會定義於金鑰/值組之後。</span><span class="sxs-lookup"><span data-stu-id="abe78-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="abe78-187">在 [金鑰] 欄位中輸入**排程**，然後將 JSON 字串貼到 [值] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="abe78-187">Type **Schedule** in the **Key** field, and then paste the JSON string into the **Value** field.</span></span> <span data-ttu-id="abe78-188">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="abe78-188">Click **Save**.</span></span> <span data-ttu-id="abe78-189">新標籤現在應出現在您的資源的標記清單中。</span><span class="sxs-lookup"><span data-stu-id="abe78-189">Your new tag should now appear in the list of tags for your resource.</span></span>

   ![VM 排程標籤](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="abe78-191">從 PowerShell 進行標記</span><span class="sxs-lookup"><span data-stu-id="abe78-191">Tag from PowerShell</span></span>
<span data-ttu-id="abe78-192">所有匯入的 Runbook 都在指令碼的開頭包含說明資訊，以描述如何直接從 PowerShell 執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="abe78-192">All imported runbooks contain help information at the beginning of the script that describes how to execute the runbooks directly from PowerShell.</span></span> <span data-ttu-id="abe78-193">您可以從 PowerShell 呼叫 Add-ScheduleResource 和 Update-ScheduleResource Runbook。</span><span class="sxs-lookup"><span data-stu-id="abe78-193">You can call the Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="abe78-194">若要這麼做，您可以傳遞必要的參數，以讓您能夠在入口網站外部的 VM 或資源群組上建立或更新排程標籤。</span><span class="sxs-lookup"><span data-stu-id="abe78-194">You do this by passing required parameters that enable you to create or update the Schedule tag on a VM or resource group outside of the portal.</span></span>

<span data-ttu-id="abe78-195">若要透過 PowerShell 建立、新增和刪除標籤，您必須先 [設定 Azure 的 PowerShell 環境](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="abe78-195">To create, add, and delete tags through PowerShell, you first need to [set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="abe78-196">在完成安裝後，您可以繼續進行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="abe78-196">After you complete the setup, you can proceed with the following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="abe78-197">使用 PowerShell 建立排程標籤</span><span class="sxs-lookup"><span data-stu-id="abe78-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="abe78-198">開啟 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="abe78-198">Open a PowerShell session.</span></span> <span data-ttu-id="abe78-199">然後使用下列範例，以使用您的「執行身分」帳戶進行驗證並指定訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="abe78-199">Then use the following example to authenticate with your Run As account and to specify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="abe78-200">定義排程雜湊表。</span><span class="sxs-lookup"><span data-stu-id="abe78-200">Define a schedule hash table.</span></span> <span data-ttu-id="abe78-201">以下是其建構方式的範例：</span><span class="sxs-lookup"><span data-stu-id="abe78-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="abe78-202">定義 Runbook 所需的參數。</span><span class="sxs-lookup"><span data-stu-id="abe78-202">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="abe78-203">在下列範例中，我們會以 VM 為目標。</span><span class="sxs-lookup"><span data-stu-id="abe78-203">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="abe78-204">如果您要標記資源群組，請從 $params 雜湊表移除「VMName」  參數，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="abe78-204">If you’re tagging a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="abe78-205">使用下列參數執行 Add-ResourceSchedule Runbook，以建立 [排程] 標籤︰</span><span class="sxs-lookup"><span data-stu-id="abe78-205">Run the Add-ResourceSchedule runbook with the following parameters to create the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="abe78-206">若要更新資源群組或虛擬機器的標籤，請使用下列參數執行 **Update-ResourceSchedule** Runbook︰</span><span class="sxs-lookup"><span data-stu-id="abe78-206">To update a resource group or virtual machine tag, execute the **Update-ResourceSchedule** runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="abe78-207">使用 PowerShell 移除排程標籤</span><span class="sxs-lookup"><span data-stu-id="abe78-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="abe78-208">開啟 PowerShell 工作階段並執行下列命令，以使用您的「執行身分」帳戶進行驗證並選取和指定訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="abe78-208">Open a PowerShell session and run the following to authenticate with your Run As account and to select and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="abe78-209">定義 Runbook 所需的參數。</span><span class="sxs-lookup"><span data-stu-id="abe78-209">Define the parameters that are required by the runbook.</span></span> <span data-ttu-id="abe78-210">在下列範例中，我們會以 VM 為目標。</span><span class="sxs-lookup"><span data-stu-id="abe78-210">In the following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="abe78-211">如果您要從資源群組移除標籤，請從 $params 雜湊表移除「VMName」  參數，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="abe78-211">If you’re removing a tag from a resource group, remove the *VMName* parameter from the $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="abe78-212">執行 Remove-ResourceSchedule Runbook 以移除 [排程] 標籤︰</span><span class="sxs-lookup"><span data-stu-id="abe78-212">Execute the Remove-ResourceSchedule runbook to remove the Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="abe78-213">若要更新資源群組或虛擬機器標籤，請使用下列參數執行 Remove-ResourceSchedule Runbook︰</span><span class="sxs-lookup"><span data-stu-id="abe78-213">To update a resource group or virtual machine tag, execute the Remove-ResourceSchedule runbook with the following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="abe78-214">建議您主動監視這些 Runbook (和虛擬機器狀態)，以確認您的虛擬機器相應地進行關機並啟動。</span><span class="sxs-lookup"><span data-stu-id="abe78-214">We recommend that you proactively monitor these runbooks (and the virtual machine states) to verify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="abe78-215">若要在 Azure 入口網站中檢視 Test-ResourceSchedule Runbook 作業的詳細資料，請選取 Runbook 的 [作業]  圖格。</span><span class="sxs-lookup"><span data-stu-id="abe78-215">To view the details of the Test-ResourceSchedule runbook job in the Azure portal, select the **Jobs** tile of the runbook.</span></span> <span data-ttu-id="abe78-216">除了作業和任何例外狀況 (如果發生) 的一般資訊以外，作業摘要也會顯示輸入參數和輸出串流。</span><span class="sxs-lookup"><span data-stu-id="abe78-216">The job summary displays the input parameters and the output stream, in addition to general information about the job and any exceptions if they occurred.</span></span>

<span data-ttu-id="abe78-217">[作業摘要]  包括來自輸出、警告和錯誤串流的訊息。</span><span class="sxs-lookup"><span data-stu-id="abe78-217">The **Job Summary** includes messages from the output, warning, and error streams.</span></span> <span data-ttu-id="abe78-218">選取 [輸出]  圖格以檢視 Runbook 執行的詳細結果。</span><span class="sxs-lookup"><span data-stu-id="abe78-218">Select the **Output** tile to view detailed results from the runbook execution.</span></span>

![Test-ResourceSchedule 輸出](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="abe78-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abe78-220">Next steps</span></span>
* <span data-ttu-id="abe78-221">若要開始使用 PowerShell 工作流程 Runbook，請參閱 [我的第一個 PowerShell 工作流程 Runbook](automation-first-runbook-textual.md)。</span><span class="sxs-lookup"><span data-stu-id="abe78-221">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="abe78-222">若要深入了解 Runbook 類型以及其優點和限制，請參閱 [Azure 自動化 Runbook 類型](automation-runbook-types.md)。</span><span class="sxs-lookup"><span data-stu-id="abe78-222">To learn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="abe78-223">如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)。</span><span class="sxs-lookup"><span data-stu-id="abe78-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="abe78-224">若要深入了解 Runbook 記錄和輸出，請參閱 [Azure 自動化中的 Runbook 輸出和訊息](automation-runbook-output-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="abe78-224">To learn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="abe78-225">若要深入了解 Azure 執行身分帳戶以及如何使用它來驗證 Runbook，請參閱[使用 Azure 執行身分帳戶驗證 Runbook](automation-sec-configure-azure-runas-account.md)。</span><span class="sxs-lookup"><span data-stu-id="abe78-225">To learn more about an Azure Run As account and how to authenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
