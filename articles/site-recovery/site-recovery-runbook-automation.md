---
title: "aaaAdd Azure 自動化 runbook toorecovery 計劃在 Azure Site Recovery |Microsoft 文件"
description: "了解 Azure Site Recovery 如何協助您使用 Azure 自動化來擴充復原方案。 了解期間復原 tooAzure toocomplete 複雜工作的方式。"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="b6c0a-104">新增 Azure 自動化 runbook toorecovery 計劃</span><span class="sxs-lookup"><span data-stu-id="b6c0a-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="b6c0a-105">在本文中，我們說明如何與 Azure 自動化 toohelp 整合 Azure Site Recovery 擴充您的復原方案。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="b6c0a-106">復原方案可以協調使用 Site Recovery 保護的 VM 復原。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="b6c0a-107">復原計劃適用於複寫 tooa 次要雲端，並複寫 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="b6c0a-108">復原計劃也有助於讓 hello 復原**一致精確**， **repeatable**，和**自動化**。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="b6c0a-109">如果您容錯移轉 Vm tooAzure，與 Azure 自動化的整合會擴充您的復原方案。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="b6c0a-110">您可以使用 tooexecute runbook，提供功能強大的自動化工作。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="b6c0a-111">如果您是新 tooAzure 自動化，您可以[註冊](https://azure.microsoft.com/services/automation/)和[下載範例指令碼](https://azure.microsoft.com/documentation/scripts/)。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="b6c0a-112">如需詳細資訊，以及 toolearn 如何使用 tooorchestrate 復原 tooAzure[復原計劃](https://azure.microsoft.com/blog/?p=166264)，請參閱[Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="b6c0a-113">在本文中，我們說明如何將 Azure 自動化 Runbook 整合至您的復原方案。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="b6c0a-114">我們使用範例 tooautomate 基本工作先前需要手動介入。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="b6c0a-115">我們也會說明如何 tooconvert multi-step 復原 tooa 單鍵復原動作。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="b6c0a-116">自訂 hello 復原計劃</span><span class="sxs-lookup"><span data-stu-id="b6c0a-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="b6c0a-117">移 toohello **Site Recovery**復原計劃資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="b6c0a-118">此範例中，hello 復原計劃有兩個 Vm 加入的 tooit，進行復原。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="b6c0a-119">toobegin 加入 runbook，按一下 hello**自訂** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![按一下 hello 自訂按鈕](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="b6c0a-121">以滑鼠右鍵按一下 [群組 1: 開始]，然後選取 [新增後續動作]。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![以滑鼠右鍵按一下 [群組 1: 開始] 並新增後續動作](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="b6c0a-123">按一下 [Choose a script] \(選擇指令碼)。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="b6c0a-124">在 hello**更新動作**刀鋒視窗中，名稱 hello 指令碼**Hello World**。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![hello 更新動作刀鋒視窗](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="b6c0a-126">輸入自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="b6c0a-127">hello 自動化帳戶可以是任何 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="b6c0a-128">hello 自動化帳戶必須在 hello 與 hello Azure Site Recovery 保存庫相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="b6c0a-129">在您的自動化帳戶中，選取一個 Runbook。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="b6c0a-130">此 runbook 是 hello 復原計劃的 hello 第一個群組的 hello 復原後 hello 執行期間執行的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="b6c0a-131">toosave hello 指令碼中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="b6c0a-132">hello 指令碼會加入太**群組 1： 後續步驟**。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![[群組 1: 開始] 的後續動作](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="b6c0a-134">新增指令碼的考量</span><span class="sxs-lookup"><span data-stu-id="b6c0a-134">Considerations for adding a script</span></span>

* <span data-ttu-id="b6c0a-135">如需選項太**刪除步驟**或**更新 hello 指令碼**，以滑鼠右鍵按一下 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="b6c0a-136">從內部部署機器 tooAzure 指令碼可以在 Azure 上執行容錯移轉期間。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="b6c0a-137">它也可以執行在 Azure 上做為關機之前, 的主要站台指令碼從 Azure tooan 在內部部署機器的容錯回復期間。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="b6c0a-138">指令碼執行時會插入復原方案內容。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="b6c0a-139">下列範例中的 hello 顯示內容變數：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="b6c0a-140">hello 下表列出 hello 名稱和描述 hello 內容中的每個變數。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="b6c0a-141">**變數名稱**</span><span class="sxs-lookup"><span data-stu-id="b6c0a-141">**Variable name**</span></span> | <span data-ttu-id="b6c0a-142">**說明**</span><span class="sxs-lookup"><span data-stu-id="b6c0a-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="b6c0a-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="b6c0a-143">RecoveryPlanName</span></span> |<span data-ttu-id="b6c0a-144">hello 計劃要執行 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-144">hello name of hello plan being run.</span></span> <span data-ttu-id="b6c0a-145">此變數可協助您不同依據採取動作 hello 復原方案名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="b6c0a-146">您也可以重複使用 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="b6c0a-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="b6c0a-147">FailoverType</span></span> |<span data-ttu-id="b6c0a-148">指定測試是否 hello 容錯移轉、 規劃或非計劃。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="b6c0a-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="b6c0a-149">FailoverDirection</span></span> |<span data-ttu-id="b6c0a-150">指定是否復原為 tooa 主要或次要站台。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="b6c0a-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="b6c0a-151">GroupID</span></span> |<span data-ttu-id="b6c0a-152">Hello 計劃執行時，識別 hello 群組編號 hello 復原計劃中。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="b6c0a-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="b6c0a-153">VmMap</span></span> |<span data-ttu-id="b6c0a-154">Hello 群組中所有 Vm 的陣列。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="b6c0a-155">VMMap 索引鍵</span><span class="sxs-lookup"><span data-stu-id="b6c0a-155">VMMap key</span></span> |<span data-ttu-id="b6c0a-156">每個 VM 的唯一索引鍵 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="b6c0a-157">它的 hello 與相同 hello Azure Virtual Machine Manager (VMM) 識別碼 hello VM，在適用情況。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="b6c0a-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="b6c0a-158">SubscriptionId</span></span> |<span data-ttu-id="b6c0a-159">建立 VM 中的 hello hello Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="b6c0a-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="b6c0a-160">RoleName</span></span> |<span data-ttu-id="b6c0a-161">hello hello 要復原的 Azure VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="b6c0a-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="b6c0a-162">CloudServiceName</span></span> |<span data-ttu-id="b6c0a-163">已建立的 hello VM hello Azure 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="b6c0a-164">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="b6c0a-164">ResourceGroupName</span></span>|<span data-ttu-id="b6c0a-165">已建立的 hello VM hello Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="b6c0a-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="b6c0a-166">RecoveryPointId</span></span>|<span data-ttu-id="b6c0a-167">當復原 hello VM 的 hello 時間戳記。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="b6c0a-168">請確定該 hello 自動化帳戶能 hello 下列模組：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="b6c0a-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="b6c0a-169">AzureRM.profile</span></span>
    * <span data-ttu-id="b6c0a-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="b6c0a-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="b6c0a-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="b6c0a-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="b6c0a-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="b6c0a-172">AzureRM.Network</span></span>
    * <span data-ttu-id="b6c0a-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="b6c0a-173">AzureRM.Compute</span></span>

<span data-ttu-id="b6c0a-174">所有模組都必須是相容版本。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="b6c0a-175">所有模組都都相容輕鬆 tooensure 是所有 hello 模組 toouse hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="b6c0a-176">存取 hello VMMap 在迴圈中的所有 Vm</span><span class="sxs-lookup"><span data-stu-id="b6c0a-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="b6c0a-177">使用下列程式碼 tooloop hello Microsoft VMMap 的所有 Vm 之間的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6c0a-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="b6c0a-178">hello 指令碼時的動作前 tooa 開機群組 hello 資源群組名稱和角色名稱的值是空的。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="b6c0a-179">只有當容錯移轉中的 hello 該群組中的 VM 成功時，會填入 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="b6c0a-180">hello 指令碼是 hello 開機群組後續動作。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="b6c0a-181">使用 hello 相同多個復原方案中的 Automation runbook</span><span class="sxs-lookup"><span data-stu-id="b6c0a-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="b6c0a-182">您可以透過外部變數，在多個復原方案中使用單一指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="b6c0a-183">您可以使用[Azure 自動化變數](../automation/automation-variables.md)toostore 參數，您可以傳遞的復原計劃執行。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="b6c0a-184">藉由加入 hello 復原方案名稱作為前置詞 toohello 變數，您可以建立個別的變數，針對每個復原方案。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="b6c0a-185">然後，使用 hello 變數做為參數。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="b6c0a-186">您可以變更參數，而不需要變更 hello 指令碼，但仍變更 hello 方式 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="b6c0a-187">在 Runbook 指令碼中使用簡單的字串變數</span><span class="sxs-lookup"><span data-stu-id="b6c0a-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="b6c0a-188">在此範例中，指令碼會使用 hello 輸入的網路安全性群組 (NSG) 並將其套用 toohello Vm 的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="b6c0a-189">Hello 指令碼 toodetect 執行復原計劃，請使用 hello 復原計劃內容：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="b6c0a-190">tooapply 現有 NSG，您必須知道 hello NSG 名稱和 hello NSG 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="b6c0a-191">使用這些變數作為復原方案指令碼的輸入。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="b6c0a-192">toodo，自動化帳戶資產 hello 中建立兩個變數。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="b6c0a-193">新增 hello hello 復原方案的名稱，您要建立 hello 參數做為前置詞 toohello 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="b6c0a-194">建立變數 toostore hello NSG 名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="b6c0a-195">使用 hello hello 復原方案的名稱，以新增前置詞 toohello 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![建立 NSG 名稱變數](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="b6c0a-197">建立變數 toostore hello NSG 的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="b6c0a-198">使用 hello hello 復原方案的名稱，以新增前置詞 toohello 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![建立 NSG 資源群組名稱](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="b6c0a-200">Hello 的指令碼中使用下列參考程式碼 tooget hello 變數值的 hello:</span><span class="sxs-lookup"><span data-stu-id="b6c0a-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="b6c0a-201">使用 hello 變數 hello runbook tooapply hello NSG toohello 網路介面中的 hello 容錯 VM:</span><span class="sxs-lookup"><span data-stu-id="b6c0a-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="b6c0a-202">對於每個復原計劃，請建立獨立變數，以便您可以重複使用 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="b6c0a-203">使用 hello 復原方案名稱，以新增前置詞。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="b6c0a-204">如需此案例中完整的端對端指令碼，請參閱[站台復原的復原計劃的測試容錯移轉期間新增公用 IP 與 NSG tooVMs](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee)。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="b6c0a-205">使用複雜變數 toostore 的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="b6c0a-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="b6c0a-206">假設您想要設定特定 Vm 上的公用 IP 上單一指令碼 tooturn。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="b6c0a-207">在其他案例中，您可能想 tooapply （不在所有的 Vm) 上的不同 Vm 上不同的 Nsg。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="b6c0a-208">您可以讓指令碼可重複使用於任何復原方案。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="b6c0a-209">每個復原方案可以有任意數目的 VM。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="b6c0a-210">例如，SharePoint 復原有兩個前端。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="b6c0a-211">基本企業營運 (LOB) 應用程式只有一個前端。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="b6c0a-212">您無法為每個復原方案建立個別變數。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="b6c0a-213">在下列範例的 hello，我們使用新的技術，並建立[複雜變數](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396)在 hello Azure 自動化帳戶的資產。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="b6c0a-214">您可以藉由指定多個值來執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="b6c0a-215">您必須使用 Azure PowerShell toocomplete hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="b6c0a-216">在 PowerShell 中，登入 tooyour Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="b6c0a-217">toostore hello 參數，會使用 hello hello 復原方案的名稱，以建立 hello 複雜變數：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="b6c0a-218">在此複雜變數， **VMDetails**為 hello VM 識別碼 hello 受保護 VM。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="b6c0a-219">tooget hello VM 識別碼 hello Azure 入口網站中的檢視 hello VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="b6c0a-220">hello 下列螢幕擷取畫面顯示變數以存放的兩個 Vm 的 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Hello GUID 作為 hello VM 識別碼](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="b6c0a-222">在您的 Runbook 中使用此變數。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-222">Use this variable in your runbook.</span></span> <span data-ttu-id="b6c0a-223">如果 hello 指示 hello 復原計劃內容中找到 VM GUID，套用 hello NSG hello VM 上：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="b6c0a-224">在您的 runbook，迴圈 hello Vm 的 hello 復原計劃內容。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="b6c0a-225">檢查 hello VM 是否存在於**$VMDetailsObj**。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="b6c0a-226">如果存在的話，存取 hello 變數 tooapply hello NSG hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="b6c0a-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="b6c0a-227">您可以使用相同指令碼的 hello 不同的復原計劃。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="b6c0a-228">儲存對應 tooa 復原計劃在不同的變數中的 hello 值，請輸入不同的參數。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="b6c0a-229">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b6c0a-229">Sample scripts</span></span>

<span data-ttu-id="b6c0a-230">toodeploy 範例指令碼 tooyour 自動化帳戶中，按一下 hello**部署 tooAzure**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="b6c0a-231">[![部署 tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="b6c0a-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="b6c0a-232">如需其他範例，請參閱下列視訊的 hello。</span><span class="sxs-lookup"><span data-stu-id="b6c0a-232">For another example, see hello following video.</span></span> <span data-ttu-id="b6c0a-233">它會示範如何 toorecover 兩層式 WordPress 應用程式 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="b6c0a-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="b6c0a-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="b6c0a-234">Additional resources</span></span>
* [<span data-ttu-id="b6c0a-235">Azure 自動化服務執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="b6c0a-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="b6c0a-236">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="b6c0a-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 自動化概觀")
* [<span data-ttu-id="b6c0a-237">Azure 自動化範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b6c0a-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 自動化範例指令碼")
