---
title: "aaaUse JSON 格式的標記 tooschedule Azure VM 狀態 |Microsoft 文件"
description: "本文示範如何 toouse JSON 字串上標記 tooautomate hello 排程 VM 啟動及關機。"
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
ms.openlocfilehash: f6bbf1dea1c193e5d1010f12f3b1ed63562f9daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario-using-json-formatted-tags-toocreate-a-schedule-for-azure-vm-startup-and-shutdown"></a><span data-ttu-id="9124b-103">Azure 自動化案例： 使用 JSON 格式標記 toocreate Azure VM 的啟動和關閉的排程</span><span class="sxs-lookup"><span data-stu-id="9124b-103">Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown</span></span>
<span data-ttu-id="9124b-104">客戶通常希望 tooschedule hello 啟動和關機的虛擬機器 toohelp 減少訂用成本或支援商務和技術需求。</span><span class="sxs-lookup"><span data-stu-id="9124b-104">Customers often want tooschedule hello startup and shutdown of virtual machines toohelp reduce subscription costs or support business and technical requirements.</span></span>

<span data-ttu-id="9124b-105">hello 下列案例可讓您自動的啟動和關機的 Vm tooset 使用稱為排程在資源群組層級或在 Azure 中的虛擬機器層級的標記。</span><span class="sxs-lookup"><span data-stu-id="9124b-105">hello following scenario enables you tooset up automated startup and shutdown of your VMs by using a tag called Schedule at a resource group level or virtual machine level in Azure.</span></span> <span data-ttu-id="9124b-106">此排程可以設定從星期日 tooSaturday 的啟動時間和關機時間。</span><span class="sxs-lookup"><span data-stu-id="9124b-106">This schedule can be configured from Sunday tooSaturday with a startup time and shutdown time.</span></span>

<span data-ttu-id="9124b-107">我們的確有一些現成可用的選項。</span><span class="sxs-lookup"><span data-stu-id="9124b-107">We do have some out-of-the-box options.</span></span> <span data-ttu-id="9124b-108">其中包含：</span><span class="sxs-lookup"><span data-stu-id="9124b-108">These include:</span></span>

* <span data-ttu-id="9124b-109">[虛擬機器擴展集](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)tooscale in 或 out 可讓您的自動調整設定。</span><span class="sxs-lookup"><span data-stu-id="9124b-109">[Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) with autoscale settings that enable you tooscale in or out.</span></span>
* <span data-ttu-id="9124b-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md)服務，其具有 hello 排程啟動及關閉作業的內建的功能。</span><span class="sxs-lookup"><span data-stu-id="9124b-110">[DevTest Labs](../devtest-lab/devtest-lab-overview.md) service, which has hello built-in capability of scheduling startup and shutdown operations.</span></span>

<span data-ttu-id="9124b-111">不過，這些選項只支援特定案例並不能套用的 tooinfrastructure 做為服務 (IaaS) Vm。</span><span class="sxs-lookup"><span data-stu-id="9124b-111">However, these options only support specific scenarios and cannot be applied tooinfrastructure-as-a-service (IaaS) VMs.</span></span>

<span data-ttu-id="9124b-112">套用的 tooa 資源群組 hello 排程標記時，也會套用的 tooall 該資源群組內的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9124b-112">When hello Schedule tag is applied tooa resource group, it's also applied tooall virtual machines inside that resource group.</span></span> <span data-ttu-id="9124b-113">如果排程也是直接套用的 tooa VM，hello 最後一個排程會優先使用在 hello 順序：</span><span class="sxs-lookup"><span data-stu-id="9124b-113">If a schedule is also directly applied tooa VM, hello last schedule takes precedence in hello following order:</span></span>

1. <span data-ttu-id="9124b-114">排程套用的 tooa 資源群組</span><span class="sxs-lookup"><span data-stu-id="9124b-114">Schedule applied tooa resource group</span></span>
2. <span data-ttu-id="9124b-115">排程套用的 tooa 資源群組和 hello 資源群組中的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9124b-115">Schedule applied tooa resource group and virtual machine in hello resource group</span></span>
3. <span data-ttu-id="9124b-116">排程套用 tooa 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9124b-116">Schedule applied tooa virtual machine</span></span>

<span data-ttu-id="9124b-117">此案例基本上會採用指定格式的 JSON 字串，並將它加入做為 hello 值稱為 「 排程的標記。</span><span class="sxs-lookup"><span data-stu-id="9124b-117">This scenario essentially takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="9124b-118">Runbook 會列出所有資源群組和虛擬機器，然後識別 hello 排程為每個稍早所列的 hello 案例為基礎的 VM。</span><span class="sxs-lookup"><span data-stu-id="9124b-118">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each VM based on hello scenarios listed earlier.</span></span> <span data-ttu-id="9124b-119">接下來它會迴圈 hello 有附加的排程的 Vm，並評估，應該採取什麼動作。</span><span class="sxs-lookup"><span data-stu-id="9124b-119">Next it loops through hello VMs that have schedules attached and evaluates what action should be taken.</span></span> <span data-ttu-id="9124b-120">例如，它會判斷 Vm 需要 toobe 停止、 關閉或忽略。</span><span class="sxs-lookup"><span data-stu-id="9124b-120">For example, it determines which VMs need toobe stopped, shut down, or ignored.</span></span>

<span data-ttu-id="9124b-121">這些 runbook 使用 hello 驗證[Azure 執行身分帳戶](automation-sec-configure-azure-runas-account.md)。</span><span class="sxs-lookup"><span data-stu-id="9124b-121">These runbooks authenticate by using hello [Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>

## <a name="download-hello-runbooks-for-hello-scenario"></a><span data-ttu-id="9124b-122">下載 hello runbook hello 案例</span><span class="sxs-lookup"><span data-stu-id="9124b-122">Download hello runbooks for hello scenario</span></span>
<span data-ttu-id="9124b-123">此案例包含四個 PowerShell 工作流程 runbook，您可以下載從 hello [TechNet 資源庫](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7)或 hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup)這個專案的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9124b-123">This scenario consists of four PowerShell Workflow runbooks that you can download from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Automation-Runbooks-84f0efc7) or hello [GitHub](https://github.com/paulomarquesdacosta/azure-automation-scheduled-shutdown-and-startup) repository for this project.</span></span>

| <span data-ttu-id="9124b-124">Runbook</span><span class="sxs-lookup"><span data-stu-id="9124b-124">Runbook</span></span> | <span data-ttu-id="9124b-125">說明</span><span class="sxs-lookup"><span data-stu-id="9124b-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9124b-126">Test-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="9124b-126">Test-ResourceSchedule</span></span> |<span data-ttu-id="9124b-127">檢查每個虛擬機器排程並執行關機或根據 hello 排程啟動。</span><span class="sxs-lookup"><span data-stu-id="9124b-127">Checks each virtual machine schedule and performs shutdown or startup depending on hello schedule.</span></span> |
| <span data-ttu-id="9124b-128">Add-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="9124b-128">Add-ResourceSchedule</span></span> |<span data-ttu-id="9124b-129">新增 hello 排程標記 tooa VM 或資源群組。</span><span class="sxs-lookup"><span data-stu-id="9124b-129">Adds hello Schedule tag tooa VM or resource group.</span></span> |
| <span data-ttu-id="9124b-130">Update-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="9124b-130">Update-ResourceSchedule</span></span> |<span data-ttu-id="9124b-131">修改現有排程標記 hello 取代新建一個。</span><span class="sxs-lookup"><span data-stu-id="9124b-131">Modifies hello existing Schedule tag by replacing it with a new one.</span></span> |
| <span data-ttu-id="9124b-132">Remove-ResourceSchedule</span><span class="sxs-lookup"><span data-stu-id="9124b-132">Remove-ResourceSchedule</span></span> |<span data-ttu-id="9124b-133">從 VM 或資源群組中移除 hello 排程標記。</span><span class="sxs-lookup"><span data-stu-id="9124b-133">Removes hello Schedule tag from a VM or resource group.</span></span> |

## <a name="install-and-configure-this-scenario"></a><span data-ttu-id="9124b-134">安裝和設定此案例</span><span class="sxs-lookup"><span data-stu-id="9124b-134">Install and configure this scenario</span></span>
### <a name="install-and-publish-hello-runbooks"></a><span data-ttu-id="9124b-135">安裝和發佈 runbook hello</span><span class="sxs-lookup"><span data-stu-id="9124b-135">Install and publish hello runbooks</span></span>
<span data-ttu-id="9124b-136">下載之後 hello runbook，您可以使用匯入它們中的 hello 程序[建立或匯入 Azure 自動化中的 runbook](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation)。</span><span class="sxs-lookup"><span data-stu-id="9124b-136">After downloading hello runbooks, you can import them by using hello procedure in [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md#importing-a-runbook-from-a-file-into-azure-automation).</span></span>  <span data-ttu-id="9124b-137">在每個 Runbook 成功匯入到您的自動化帳戶之後予以發佈。</span><span class="sxs-lookup"><span data-stu-id="9124b-137">Publish each runbook after it has been successfully imported into your Automation account.</span></span>

### <a name="add-a-schedule-toohello-test-resourceschedule-runbook"></a><span data-ttu-id="9124b-138">新增排程 toohello 測試 ResourceSchedule runbook</span><span class="sxs-lookup"><span data-stu-id="9124b-138">Add a schedule toohello Test-ResourceSchedule runbook</span></span>
<span data-ttu-id="9124b-139">請遵循這些步驟 tooenable hello 排程的 hello 測試 ResourceSchedule runbook。</span><span class="sxs-lookup"><span data-stu-id="9124b-139">Follow these steps tooenable hello schedule for hello Test-ResourceSchedule runbook.</span></span> <span data-ttu-id="9124b-140">這是 hello runbook，用來驗證虛擬機器應該要啟動、 關閉，或者保持原樣。</span><span class="sxs-lookup"><span data-stu-id="9124b-140">This is hello runbook that verifies which virtual machines should be started, shut down, or left as is.</span></span>

1. <span data-ttu-id="9124b-141">從 hello Azure 入口網站，開啟您的自動化帳戶，然後按一下hello **Runbook**磚。</span><span class="sxs-lookup"><span data-stu-id="9124b-141">From hello Azure portal, open your Automation account, and then click hello **Runbooks** tile.</span></span>
2. <span data-ttu-id="9124b-142">在 hello**測試 ResourceSchedule**刀鋒視窗中，按一下 hello**排程**磚。</span><span class="sxs-lookup"><span data-stu-id="9124b-142">On hello **Test-ResourceSchedule** blade, click hello **Schedules** tile.</span></span>
3. <span data-ttu-id="9124b-143">在 hello**排程**刀鋒視窗中，按一下 **加入排程**。</span><span class="sxs-lookup"><span data-stu-id="9124b-143">On hello **Schedules** blade, click **Add a schedule**.</span></span>
4. <span data-ttu-id="9124b-144">在 hello**排程**刀鋒視窗中，選取**排程 tooyour runbook 連結**。</span><span class="sxs-lookup"><span data-stu-id="9124b-144">On hello **Schedules** blade, select **Link a schedule tooyour runbook**.</span></span> <span data-ttu-id="9124b-145">然後選取 [建立新的排程] 。</span><span class="sxs-lookup"><span data-stu-id="9124b-145">Then select **Create a new schedule**.</span></span>
5. <span data-ttu-id="9124b-146">在 hello**新排程**刀鋒視窗中，輸入 hello 名稱的這個排程，例如： *HourlyExecution*。</span><span class="sxs-lookup"><span data-stu-id="9124b-146">On hello **New schedule** blade, type in hello name of this schedule, for example: *HourlyExecution*.</span></span>
6. <span data-ttu-id="9124b-147">Hello 排程**啟動**，設定 hello 開始時間 tooan 小時增量。</span><span class="sxs-lookup"><span data-stu-id="9124b-147">For hello schedule **Start**, set hello start time tooan hour increment.</span></span>
7. <span data-ttu-id="9124b-148">選取 [週期]，然後針對 [重複出現間隔] 選取 [1 小時]。</span><span class="sxs-lookup"><span data-stu-id="9124b-148">Select **Recurrence**, and then for **Recur every interval**, select **1 hour**.</span></span>
8. <span data-ttu-id="9124b-149">確認**組是否逾期**設定得**否**，然後按一下**建立**toosave 新的排程。</span><span class="sxs-lookup"><span data-stu-id="9124b-149">Verify that **Set expiration** is set too**No**, and then click **Create** toosave your new schedule.</span></span>
9. <span data-ttu-id="9124b-150">在 hello**排程 Runbook**選項刀鋒視窗中，選取**參數與回合的設定**。</span><span class="sxs-lookup"><span data-stu-id="9124b-150">On hello **Schedule Runbook** options blade, select **Parameters and run settings**.</span></span> <span data-ttu-id="9124b-151">在 hello 測試 ResourceSchedule**參數**刀鋒視窗中，輸入您的訂閱 hello 名稱 hello**訂用帳戶名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="9124b-151">In hello Test-ResourceSchedule **Parameters** blade, enter hello name of your subscription in hello **SubscriptionName** field.</span></span>  <span data-ttu-id="9124b-152">這是 hello hello runbook 所需的唯一參數。</span><span class="sxs-lookup"><span data-stu-id="9124b-152">This is hello only parameter that's required for hello runbook.</span></span>  <span data-ttu-id="9124b-153">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9124b-153">When you're finished, click **OK**.</span></span>

<span data-ttu-id="9124b-154">hello runbook 排程看起來應該類似下列 hello 完成之後：</span><span class="sxs-lookup"><span data-stu-id="9124b-154">hello runbook schedule should look like hello following when it's completed:</span></span>

![已設定的 Test-ResourceSchedule Runbook](./media/automation-scenario-start-stop-vm-wjson-tags/automation-schedule-config.png)<br>

## <a name="format-hello-json-string"></a><span data-ttu-id="9124b-156">格式 hello JSON 字串</span><span class="sxs-lookup"><span data-stu-id="9124b-156">Format hello JSON string</span></span>
<span data-ttu-id="9124b-157">此解決方案會採用 JSON 的指定格式的字串，並將它加入做為標記的 hello 值基本上呼叫排程。</span><span class="sxs-lookup"><span data-stu-id="9124b-157">This solution basically takes a JSON string with a specified format and adds it as hello value for a tag called Schedule.</span></span> <span data-ttu-id="9124b-158">然後 runbook 列出所有資源群組和虛擬機器，並識別每個虛擬機器的 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="9124b-158">Then a runbook lists all resource groups and virtual machines and identifies hello schedules for each virtual machine.</span></span>

<span data-ttu-id="9124b-159">hello runbook 有附加的排程的 hello 虛擬機器上執行迴圈，並檢查應該採取什麼動作。</span><span class="sxs-lookup"><span data-stu-id="9124b-159">hello runbook loops over hello virtual machines that have schedules attached and checks what actions should be taken.</span></span> <span data-ttu-id="9124b-160">hello 以下是如何格式化 hello 解決方案的範例：</span><span class="sxs-lookup"><span data-stu-id="9124b-160">hello following is an example of how hello solutions should be formatted:</span></span>

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

<span data-ttu-id="9124b-161">以下是此結構的部分詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="9124b-161">Here is some detailed information about this structure:</span></span>

1. <span data-ttu-id="9124b-162">此 JSON 結構的 hello 格式為最佳化的 toowork 採用單一標記值，在 Azure 中的 hello 256 個字元限制。</span><span class="sxs-lookup"><span data-stu-id="9124b-162">hello format of this JSON structure is optimized toowork around hello 256-character limitation of a single tag value in Azure.</span></span>
2. <span data-ttu-id="9124b-163">*TzId*代表 hello hello 虛擬機器的時區時間。</span><span class="sxs-lookup"><span data-stu-id="9124b-163">*TzId* represents hello time zone of hello virtual machine.</span></span> <span data-ttu-id="9124b-164">這個識別碼可透過 PowerShell 工作階段--使用 hello TimeZoneInfo.NET 類別**[System.TimeZoneInfo]:: GetSystemTimeZones()**。</span><span class="sxs-lookup"><span data-stu-id="9124b-164">This ID can be obtained by using hello TimeZoneInfo .NET class in a PowerShell session--**[System.TimeZoneInfo]::GetSystemTimeZones()**.</span></span>

   ![PowerShell 中的 GetSystemTimeZones](./media/automation-scenario-start-stop-vm-wjson-tags/automation-get-timzone-powershell.png)

   * <span data-ttu-id="9124b-166">工作日會使用零 toosix 的數值表示。</span><span class="sxs-lookup"><span data-stu-id="9124b-166">Weekdays are represented with a numeric value of zero toosix.</span></span> <span data-ttu-id="9124b-167">hello 零的值等於星期日。</span><span class="sxs-lookup"><span data-stu-id="9124b-167">hello value zero equals Sunday.</span></span>
   * <span data-ttu-id="9124b-168">hello 開始時間以表示 hello **S**屬性和其值為 24 小時制格式。</span><span class="sxs-lookup"><span data-stu-id="9124b-168">hello start time is represented with hello **S** attribute, and its value is in a 24-hour format.</span></span>
   * <span data-ttu-id="9124b-169">hello 結束或關機時間表示以 hello **E**屬性和其值為 24 小時制格式。</span><span class="sxs-lookup"><span data-stu-id="9124b-169">hello end or shutdown time is represented with hello **E** attribute, and its value is in a 24-hour format.</span></span>

     <span data-ttu-id="9124b-170">如果 hello **S**和**E**每一個屬性的值為零 (0)、 在 hello 時間評估其目前的狀態將保持 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9124b-170">If hello **S** and **E** attributes each have a value of zero (0), hello virtual machine will be left in its present state at hello time of evaluation.</span></span>
3. <span data-ttu-id="9124b-171">如果您想 tooskip 評估 hello 當週的特定日期時，不針對該日 hello 週中的新增區段。</span><span class="sxs-lookup"><span data-stu-id="9124b-171">If you want tooskip evaluation for a specific day of hello week, don’t add a section for that day of hello week.</span></span> <span data-ttu-id="9124b-172">在 hello 遵循範例中，只有星期一會評估並 hello 其他 hello 星期幾都會被忽略：</span><span class="sxs-lookup"><span data-stu-id="9124b-172">In hello following example, only Monday is evaluated, and hello other days of hello week are ignored:</span></span>

    ```json
    {
        "TzId": "Eastern Standard Time",
        "1": {
            "S": "11",
            "E": "17"
        }
    }
    ```

## <a name="tag-resource-groups-or-vms"></a><span data-ttu-id="9124b-173">標記資源群組或 VM</span><span class="sxs-lookup"><span data-stu-id="9124b-173">Tag resource groups or VMs</span></span>
<span data-ttu-id="9124b-174">tooshut 關閉 Vm，您需要 tootag hello Vm 或其所處的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="9124b-174">tooshut down VMs, you need tootag either hello VMs or hello resource groups in which they're located.</span></span> <span data-ttu-id="9124b-175">沒有「排程」標籤的虛擬機器不會進行評估。</span><span class="sxs-lookup"><span data-stu-id="9124b-175">Virtual machines that don't have a Schedule tag are not evaluated.</span></span> <span data-ttu-id="9124b-176">因此，不會加以啟動或關閉。</span><span class="sxs-lookup"><span data-stu-id="9124b-176">Therefore, they aren't started or shut down.</span></span>

<span data-ttu-id="9124b-177">有兩種方式 tootag 資源群組或 Vm 具有此解決方案。</span><span class="sxs-lookup"><span data-stu-id="9124b-177">There are two ways tootag resource groups or VMs with this solution.</span></span> <span data-ttu-id="9124b-178">您可以直接從 hello 入口網站進行。</span><span class="sxs-lookup"><span data-stu-id="9124b-178">You can do it directly from hello portal.</span></span> <span data-ttu-id="9124b-179">或者，您可以使用新增 ResourceSchedule hello、 更新 ResourceSchedule 及移除 ResourceSchedule runbook。</span><span class="sxs-lookup"><span data-stu-id="9124b-179">Or you can use hello Add-ResourceSchedule, Update-ResourceSchedule, and Remove-ResourceSchedule runbooks.</span></span>

### <a name="tag-through-hello-portal"></a><span data-ttu-id="9124b-180">標記透過 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="9124b-180">Tag through hello portal</span></span>
<span data-ttu-id="9124b-181">請遵循這些步驟 tootag 虛擬機器或 hello 入口網站中的資源群組：</span><span class="sxs-lookup"><span data-stu-id="9124b-181">Follow these steps tootag a virtual machine or resource group in hello portal:</span></span>

1. <span data-ttu-id="9124b-182">壓平合併 hello JSON 字串，並確認沒有任何空格。</span><span class="sxs-lookup"><span data-stu-id="9124b-182">Flatten hello JSON string and verify that there aren't any spaces.</span></span>  <span data-ttu-id="9124b-183">您的 JSON 字串應該如下所示︰</span><span class="sxs-lookup"><span data-stu-id="9124b-183">Your JSON string should look like this:</span></span>

    ```json
    {"TzId":"Eastern Standard Time","0":{"S":"11","E":"17"},"1":{"S":"9","E":"19"},"2": {"S":"9","E":"19"},"3":{"S":"9","E":"19"},"4":{"S":"9","E":"19"},"5":{"S":"9","E":"19"},"6":{"S":"11","E":"17"}}
    ```

2. <span data-ttu-id="9124b-184">選取 hello**標記**圖示的 VM 或資源群組 tooapply 此排程。</span><span class="sxs-lookup"><span data-stu-id="9124b-184">Select hello **Tag** icon for a VM or resource group tooapply this schedule.</span></span>

   ![VM 標籤選項](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-tag-option.png)

3. <span data-ttu-id="9124b-186">標籤會定義於金鑰/值組之後。</span><span class="sxs-lookup"><span data-stu-id="9124b-186">Tags are defined following a key/value pair.</span></span> <span data-ttu-id="9124b-187">型別**排程**在 hello**金鑰**欄位，並將 hello JSON 字串 hello 貼入**值**欄位。</span><span class="sxs-lookup"><span data-stu-id="9124b-187">Type **Schedule** in hello **Key** field, and then paste hello JSON string into hello **Value** field.</span></span> <span data-ttu-id="9124b-188">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9124b-188">Click **Save**.</span></span> <span data-ttu-id="9124b-189">您的新標籤現在應該會出現在 hello 清單中的資源標記。</span><span class="sxs-lookup"><span data-stu-id="9124b-189">Your new tag should now appear in hello list of tags for your resource.</span></span>

   ![VM 排程標籤](./media/automation-scenario-start-stop-vm-wjson-tags/automation-vm-schedule-tag.png)

### <a name="tag-from-powershell"></a><span data-ttu-id="9124b-191">從 PowerShell 進行標記</span><span class="sxs-lookup"><span data-stu-id="9124b-191">Tag from PowerShell</span></span>
<span data-ttu-id="9124b-192">所有匯入的 runbook 會包含在 hello 開頭的 hello 指令碼可說明如何 tooexecute hello 直接從 PowerShell runbook 的說明資訊。</span><span class="sxs-lookup"><span data-stu-id="9124b-192">All imported runbooks contain help information at hello beginning of hello script that describes how tooexecute hello runbooks directly from PowerShell.</span></span> <span data-ttu-id="9124b-193">您可以從 PowerShell 呼叫 hello 新增 ScheduleResource 和更新 ScheduleResource runbook。</span><span class="sxs-lookup"><span data-stu-id="9124b-193">You can call hello Add-ScheduleResource and Update-ScheduleResource runbooks from PowerShell.</span></span> <span data-ttu-id="9124b-194">您藉由傳遞必要的參數可讓您 toocreate 或更新 hello 排程標記 hello 入口網站以外的 VM 或資源群組上。</span><span class="sxs-lookup"><span data-stu-id="9124b-194">You do this by passing required parameters that enable you toocreate or update hello Schedule tag on a VM or resource group outside of hello portal.</span></span>

<span data-ttu-id="9124b-195">toocreate，新增和刪除透過 PowerShell 的標記，則需要太[設定 azure PowerShell 環境](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9124b-195">toocreate, add, and delete tags through PowerShell, you first need too[set up your PowerShell environment for Azure](/powershell/azure/overview).</span></span> <span data-ttu-id="9124b-196">Hello 安裝程式完成之後，您可以繼續以 hello 下列步驟。</span><span class="sxs-lookup"><span data-stu-id="9124b-196">After you complete hello setup, you can proceed with hello following steps.</span></span>

### <a name="create-a-schedule-tag-with-powershell"></a><span data-ttu-id="9124b-197">使用 PowerShell 建立排程標籤</span><span class="sxs-lookup"><span data-stu-id="9124b-197">Create a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="9124b-198">開啟 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9124b-198">Open a PowerShell session.</span></span> <span data-ttu-id="9124b-199">接著，使用下列執行身分帳戶與訂用帳戶 toospecify 範例 tooauthenticate hello:</span><span class="sxs-lookup"><span data-stu-id="9124b-199">Then use hello following example tooauthenticate with your Run As account and toospecify a subscription:</span></span>

    ```powershell
    $Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="9124b-200">定義排程雜湊表。</span><span class="sxs-lookup"><span data-stu-id="9124b-200">Define a schedule hash table.</span></span> <span data-ttu-id="9124b-201">以下是其建構方式的範例：</span><span class="sxs-lookup"><span data-stu-id="9124b-201">Here is an example of how it should be constructed:</span></span>

    ```powershell
    $schedule= @{ "TzId"="Eastern Standard Time"; "0"= @{"S"="11";"E"="17"};"1"= @{"S"="9";"E"="19"};"2"= @{"S"="9";"E"="19"};"3"= @{"S"="9";"E"="19"};"4"= @{"S"="9";"E"="19"};"5"= @{"S"="9";"E"="19"};"6"= @{"S"="11";"E"="17"}}
    ```

3. <span data-ttu-id="9124b-202">定義所需的 hello runbook hello 參數。</span><span class="sxs-lookup"><span data-stu-id="9124b-202">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="9124b-203">在下列範例的 hello，我們的目標 VM:</span><span class="sxs-lookup"><span data-stu-id="9124b-203">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "VmName"="VM01";"Schedule"=$schedule}
    ```

    <span data-ttu-id="9124b-204">如果您要標記的資源群組，移除 hello *VMName*參數從 hello $params 雜湊資料表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9124b-204">If you’re tagging a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"; "Schedule"=$schedule}
    ```

4. <span data-ttu-id="9124b-205">執行 hello 新增 ResourceSchedule runbook 以下列參數 toocreate hello 排程標記 hello:</span><span class="sxs-lookup"><span data-stu-id="9124b-205">Run hello Add-ResourceSchedule runbook with hello following parameters toocreate hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Add-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

5. <span data-ttu-id="9124b-206">資源群組或虛擬機器標記，tooupdate 執行 hello**更新 ResourceSchedule** runbook 以 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="9124b-206">tooupdate a resource group or virtual machine tag, execute hello **Update-ResourceSchedule** runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Update-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

### <a name="remove-a-schedule-tag-with-powershell"></a><span data-ttu-id="9124b-207">使用 PowerShell 移除排程標籤</span><span class="sxs-lookup"><span data-stu-id="9124b-207">Remove a schedule tag with PowerShell</span></span>
1. <span data-ttu-id="9124b-208">開啟 PowerShell 工作階段和執行下列執行身分帳戶與 tooselect tooauthenticate hello 和指定的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="9124b-208">Open a PowerShell session and run hello following tooauthenticate with your Run As account and tooselect and specify a subscription:</span></span>

    ```powershell
    Conn = Get-AutomationConnection -Name AzureRunAsConnection
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

2. <span data-ttu-id="9124b-209">定義所需的 hello runbook hello 參數。</span><span class="sxs-lookup"><span data-stu-id="9124b-209">Define hello parameters that are required by hello runbook.</span></span> <span data-ttu-id="9124b-210">在下列範例的 hello，我們的目標 VM:</span><span class="sxs-lookup"><span data-stu-id="9124b-210">In hello following example, we are targeting a VM:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01";"VmName"="VM01"}
    ```

    <span data-ttu-id="9124b-211">如果您正在從資源群組中移除標記，移除 hello *VMName*參數從 hello $params 雜湊資料表，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9124b-211">If you’re removing a tag from a resource group, remove hello *VMName* parameter from hello $params hash table as follows:</span></span>

    ```powershell
    $params = @{"SubscriptionName"="MySubscription";"ResourceGroupName"="ResourceGroup01"}
    ```

3. <span data-ttu-id="9124b-212">執行 hello 移除 ResourceSchedule runbook tooremove hello 排程標記：</span><span class="sxs-lookup"><span data-stu-id="9124b-212">Execute hello Remove-ResourceSchedule runbook tooremove hello Schedule tag:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

4. <span data-ttu-id="9124b-213">tooupdate 資源群組或虛擬機器標記，執行 hello 移除 ResourceSchedule runbook 以 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="9124b-213">tooupdate a resource group or virtual machine tag, execute hello Remove-ResourceSchedule runbook with hello following parameters:</span></span>

    ```powershell
    Start-AzureRmAutomationRunbook -Name "Remove-ResourceSchedule" -Parameters $params `
    -AutomationAccountName "AutomationAccount" -ResourceGroupName "ResourceGroup01"
    ```

> [!NOTE]
> <span data-ttu-id="9124b-214">我們建議您主動監視正在您的虛擬機器的 tooverify 關閉這些 runbook （和 hello 虛擬機器狀態），並據以啟動。</span><span class="sxs-lookup"><span data-stu-id="9124b-214">We recommend that you proactively monitor these runbooks (and hello virtual machine states) tooverify that your virtual machines are being shut down and started accordingly.</span></span>
>

<span data-ttu-id="9124b-215">hello Azure 入口網站中，選取 hello tooview hello 詳細資料的 hello 測試 ResourceSchedule runbook 作業**作業**hello runbook 的磚。</span><span class="sxs-lookup"><span data-stu-id="9124b-215">tooview hello details of hello Test-ResourceSchedule runbook job in hello Azure portal, select hello **Jobs** tile of hello runbook.</span></span> <span data-ttu-id="9124b-216">hello 工作摘要顯示 hello 輸入的參數及 hello 輸出資料流，此外 toogeneral hello 工作的資訊和任何例外狀況發生。</span><span class="sxs-lookup"><span data-stu-id="9124b-216">hello job summary displays hello input parameters and hello output stream, in addition toogeneral information about hello job and any exceptions if they occurred.</span></span>

<span data-ttu-id="9124b-217">hello**工作摘要**包括從 hello 輸出、 警告和錯誤資料流的訊息。</span><span class="sxs-lookup"><span data-stu-id="9124b-217">hello **Job Summary** includes messages from hello output, warning, and error streams.</span></span> <span data-ttu-id="9124b-218">選取 hello**輸出**磚 tooview 詳細 hello runbook 執行結果。</span><span class="sxs-lookup"><span data-stu-id="9124b-218">Select hello **Output** tile tooview detailed results from hello runbook execution.</span></span>

![Test-ResourceSchedule 輸出](./media/automation-scenario-start-stop-vm-wjson-tags/automation-job-output.png)

## <a name="next-steps"></a><span data-ttu-id="9124b-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9124b-220">Next steps</span></span>
* <span data-ttu-id="9124b-221">tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)。</span><span class="sxs-lookup"><span data-stu-id="9124b-221">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md).</span></span>
* <span data-ttu-id="9124b-222">toolearn 深入了解 runbook 類型，其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)。</span><span class="sxs-lookup"><span data-stu-id="9124b-222">toolearn more about runbook types, and their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md).</span></span>
* <span data-ttu-id="9124b-223">如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)。</span><span class="sxs-lookup"><span data-stu-id="9124b-223">For more information about PowerShell script support features, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/).</span></span>
* <span data-ttu-id="9124b-224">toolearn 深入了解 runbook 記錄和輸出，請參閱[Runbook 輸出和在 Azure 自動化中的訊息](automation-runbook-output-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="9124b-224">toolearn more about runbook logging and output, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md).</span></span>
* <span data-ttu-id="9124b-225">深入了解 Azure 執行身分帳戶，以及如何 tooauthenticate runbook 使用，請參閱 toolearn[驗證與 Azure 執行身分帳戶的 runbook](automation-sec-configure-azure-runas-account.md)。</span><span class="sxs-lookup"><span data-stu-id="9124b-225">toolearn more about an Azure Run As account and how tooauthenticate your runbooks by using it, see [Authenticate runbooks with Azure Run As account](automation-sec-configure-azure-runas-account.md).</span></span>
