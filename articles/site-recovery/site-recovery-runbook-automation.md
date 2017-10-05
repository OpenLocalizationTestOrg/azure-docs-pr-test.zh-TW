---
title: "在 Azure Site Recovery 中將 Azure 自動化 Runbook 新增至復原方案 | Microsoft Docs"
description: "了解 Azure Site Recovery 如何協助您使用 Azure 自動化來擴充復原方案。 了解如何在復原至 Azure 期間完成複雜的工作。"
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
ms.openlocfilehash: 064a6782970b950543f93c24800998c1f104c8df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans"></a><span data-ttu-id="1893e-104">將 Azure 自動化 Runbook 新增至復原方案</span><span class="sxs-lookup"><span data-stu-id="1893e-104">Add Azure Automation runbooks to recovery plans</span></span>
<span data-ttu-id="1893e-105">在本文中，我們說明如何將 Azure Site Recovery 與 Azure 自動化整合在一起，以協助您擴充復原方案。</span><span class="sxs-lookup"><span data-stu-id="1893e-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation to help you extend your recovery plans.</span></span> <span data-ttu-id="1893e-106">復原方案可以協調使用 Site Recovery 保護的 VM 復原。</span><span class="sxs-lookup"><span data-stu-id="1893e-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="1893e-107">復原方案可複寫至次要雲端，也可以複寫至 Azure。</span><span class="sxs-lookup"><span data-stu-id="1893e-107">Recovery plans work both for replication to a secondary cloud, and for replication to Azure.</span></span> <span data-ttu-id="1893e-108">復原方案也有助於讓復原「保持一致精確」、「可重複執行」及「自動化」。</span><span class="sxs-lookup"><span data-stu-id="1893e-108">Recovery plans also help make the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="1893e-109">如果您將 VM 容錯移轉至 Azure，與 Azure 自動化的整合可擴充復原方案。</span><span class="sxs-lookup"><span data-stu-id="1893e-109">If you fail over your VMs to Azure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="1893e-110">您可以使用它來執行 Runbook，以提供功能強大的自動化工作。</span><span class="sxs-lookup"><span data-stu-id="1893e-110">You can use it to execute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="1893e-111">如果您是 Azure 自動化的新手，您可以[註冊](https://azure.microsoft.com/services/automation/)並[下載範例指令碼](https://azure.microsoft.com/documentation/scripts/)。</span><span class="sxs-lookup"><span data-stu-id="1893e-111">If you are new to Azure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="1893e-112">如需詳細資訊，以及了解如何使用[復原方案](https://azure.microsoft.com/blog/?p=166264)來協調復原至 Azure，請參閱 [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)。</span><span class="sxs-lookup"><span data-stu-id="1893e-112">For more information, and to learn how to orchestrate recovery to Azure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="1893e-113">在本文中，我們說明如何將 Azure 自動化 Runbook 整合至您的復原方案。</span><span class="sxs-lookup"><span data-stu-id="1893e-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="1893e-114">我們使用範例，將先前需要手動介入的基本工作自動化。</span><span class="sxs-lookup"><span data-stu-id="1893e-114">We use examples to automate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="1893e-115">我們也會說明如何將多重步驟復原轉換成單鍵復原動作。</span><span class="sxs-lookup"><span data-stu-id="1893e-115">We also describe how to convert a multi-step recovery to a single-click recovery action.</span></span>

## <a name="customize-the-recovery-plan"></a><span data-ttu-id="1893e-116">自訂復原方案</span><span class="sxs-lookup"><span data-stu-id="1893e-116">Customize the recovery plan</span></span>
1. <span data-ttu-id="1893e-117">移至 [Site Recovery] 復原方案資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1893e-117">Go to the **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="1893e-118">在此範例中，復原方案新增了兩個 VM 來進行復原。</span><span class="sxs-lookup"><span data-stu-id="1893e-118">For this example, the recovery plan has two VMs added to it, for recovery.</span></span> <span data-ttu-id="1893e-119">若要開始新增 Runbook，請按一下 [自訂] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1893e-119">To begin adding a runbook, click the **Customize** tab.</span></span>

    ![按一下 [自訂] 按鈕](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="1893e-121">以滑鼠右鍵按一下 [群組 1: 開始]，然後選取 [新增後續動作]。</span><span class="sxs-lookup"><span data-stu-id="1893e-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![以滑鼠右鍵按一下 [群組 1: 開始] 並新增後續動作](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="1893e-123">按一下 [Choose a script] (選擇指令碼)。</span><span class="sxs-lookup"><span data-stu-id="1893e-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="1893e-124">在 [更新動作] 刀鋒視窗中，將指令碼命名為 **Hello World**。</span><span class="sxs-lookup"><span data-stu-id="1893e-124">On the **Update action** blade, name the script **Hello World**.</span></span>

    ![[更新動作] 刀鋒視窗](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="1893e-126">輸入自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="1893e-127">自動化帳戶可以位於任何 Azure 區域中。</span><span class="sxs-lookup"><span data-stu-id="1893e-127">The Automation account can be in any Azure region.</span></span> <span data-ttu-id="1893e-128">自動化帳戶必須與 Azure Site Recovery 保存庫位於相同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1893e-128">The Automation account must be in the same subscription as the Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="1893e-129">在您的自動化帳戶中，選取一個 Runbook。</span><span class="sxs-lookup"><span data-stu-id="1893e-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="1893e-130">此 Runbook 是在執行復原方案時，於復原第一個群組後執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-130">This runbook is the script that runs during the execution of the recovery plan, after the recovery of the first group.</span></span>

7. <span data-ttu-id="1893e-131">若要儲存指令碼，請按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1893e-131">To save the script, click **OK**.</span></span> <span data-ttu-id="1893e-132">指令碼會新增至 [群組 1: 後續步驟]。</span><span class="sxs-lookup"><span data-stu-id="1893e-132">The script is added to **Group 1: Post-steps**.</span></span>

    ![[群組 1: 開始] 的後續動作](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="1893e-134">新增指令碼的考量</span><span class="sxs-lookup"><span data-stu-id="1893e-134">Considerations for adding a script</span></span>

* <span data-ttu-id="1893e-135">若要選擇**刪除步驟**或**更新指令碼**，請以滑鼠右鍵按一下指令碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-135">For options to **delete a step** or **update the script**, right-click the script.</span></span>
* <span data-ttu-id="1893e-136">指令碼可以在從內部部署電腦容錯移轉至 Azure 時，在 Azure 上執行；</span><span class="sxs-lookup"><span data-stu-id="1893e-136">A script can run on Azure during failover from an on-premises machine to Azure.</span></span> <span data-ttu-id="1893e-137">也可以在從 Azure 容錯回復至內部部署電腦時，於關機前在 Azure 上當做主要站台指令碼來執行。</span><span class="sxs-lookup"><span data-stu-id="1893e-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure to an on-premises machine.</span></span>
* <span data-ttu-id="1893e-138">指令碼執行時會插入復原方案內容。</span><span class="sxs-lookup"><span data-stu-id="1893e-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="1893e-139">下列範例顯示內容變數：</span><span class="sxs-lookup"><span data-stu-id="1893e-139">The following example shows a context variable:</span></span>

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

    <span data-ttu-id="1893e-140">下表列出內容中每個變數的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="1893e-140">The following table lists the name and description of each variable in the context.</span></span>

    | <span data-ttu-id="1893e-141">**變數名稱**</span><span class="sxs-lookup"><span data-stu-id="1893e-141">**Variable name**</span></span> | <span data-ttu-id="1893e-142">**說明**</span><span class="sxs-lookup"><span data-stu-id="1893e-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="1893e-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="1893e-143">RecoveryPlanName</span></span> |<span data-ttu-id="1893e-144">正在執行之方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-144">The name of the plan being run.</span></span> <span data-ttu-id="1893e-145">此變數可協助您根據復原方案名稱，而採取不同的動作。</span><span class="sxs-lookup"><span data-stu-id="1893e-145">This variable helps you take different actions based on the recovery plan name.</span></span> <span data-ttu-id="1893e-146">您也可以重複使用指令碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-146">You also can reuse the script.</span></span> |
    | <span data-ttu-id="1893e-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="1893e-147">FailoverType</span></span> |<span data-ttu-id="1893e-148">指定容錯移轉是測試、已計劃，還是未計劃。</span><span class="sxs-lookup"><span data-stu-id="1893e-148">Specifies whether the failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="1893e-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="1893e-149">FailoverDirection</span></span> |<span data-ttu-id="1893e-150">指定復原是主要或次要站台。</span><span class="sxs-lookup"><span data-stu-id="1893e-150">Specifies whether recovery is to a primary or secondary site.</span></span> |
    | <span data-ttu-id="1893e-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="1893e-151">GroupID</span></span> |<span data-ttu-id="1893e-152">識別復原方案執行時方案內的群組編號。</span><span class="sxs-lookup"><span data-stu-id="1893e-152">Identifies the group number in the recovery plan when the plan is running.</span></span> |
    | <span data-ttu-id="1893e-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="1893e-153">VmMap</span></span> |<span data-ttu-id="1893e-154">群組中所有 VM 的陣列。</span><span class="sxs-lookup"><span data-stu-id="1893e-154">An array of all VMs in the group.</span></span> |
    | <span data-ttu-id="1893e-155">VMMap 索引鍵</span><span class="sxs-lookup"><span data-stu-id="1893e-155">VMMap key</span></span> |<span data-ttu-id="1893e-156">每個 VM 的唯一索引鍵 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="1893e-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="1893e-157">與 VM 的適用 Azure Virtual Machine Manager (VMM) 識別碼相同。</span><span class="sxs-lookup"><span data-stu-id="1893e-157">It's the same as the Azure Virtual Machine Manager (VMM) ID of the VM, where applicable.</span></span> |
    | <span data-ttu-id="1893e-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1893e-158">SubscriptionId</span></span> |<span data-ttu-id="1893e-159">建立 VM 的 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-159">The Azure subscription ID in which the VM was created.</span></span> |
    | <span data-ttu-id="1893e-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="1893e-160">RoleName</span></span> |<span data-ttu-id="1893e-161">正在復原之 Azure VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-161">The name of the Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="1893e-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="1893e-162">CloudServiceName</span></span> |<span data-ttu-id="1893e-163">在其下建立 VM 的 Azure 雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-163">The Azure cloud service name under which the VM was created.</span></span> |
    | <span data-ttu-id="1893e-164">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="1893e-164">ResourceGroupName</span></span>|<span data-ttu-id="1893e-165">在其下建立 VM 的 Azure 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-165">The Azure resource group name under which the VM was created.</span></span> |
    | <span data-ttu-id="1893e-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="1893e-166">RecoveryPointId</span></span>|<span data-ttu-id="1893e-167">VM 復原時間的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="1893e-167">The timestamp for when the VM is recovered.</span></span> |

* <span data-ttu-id="1893e-168">確定自動化帳戶具有下列模組：</span><span class="sxs-lookup"><span data-stu-id="1893e-168">Ensure that the Automation account has the following modules:</span></span>
    * <span data-ttu-id="1893e-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="1893e-169">AzureRM.profile</span></span>
    * <span data-ttu-id="1893e-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="1893e-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="1893e-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="1893e-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="1893e-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="1893e-172">AzureRM.Network</span></span>
    * <span data-ttu-id="1893e-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="1893e-173">AzureRM.Compute</span></span>

<span data-ttu-id="1893e-174">所有模組都必須是相容版本。</span><span class="sxs-lookup"><span data-stu-id="1893e-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="1893e-175">確保所有模組均相容的簡單做法，就是使用所有模組的最新版本。</span><span class="sxs-lookup"><span data-stu-id="1893e-175">An easy way to ensure that all modules are compatible is to use the latest versions of all the modules.</span></span>

### <a name="access-all-vms-of-the-vmmap-in-a-loop"></a><span data-ttu-id="1893e-176">在迴圈中存取 VMMap 的所有 VM</span><span class="sxs-lookup"><span data-stu-id="1893e-176">Access all VMs of the VMMap in a loop</span></span>
<span data-ttu-id="1893e-177">使用下列程式碼循環存取 Microsoft VMMap 的所有 VM：</span><span class="sxs-lookup"><span data-stu-id="1893e-177">Use the following code to loop across all VMs of the Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is to ensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="1893e-178">當指令碼是開機群組的前置動作時，資源群組名稱和角色名稱值會是空的。</span><span class="sxs-lookup"><span data-stu-id="1893e-178">The resource group name and role name values are empty when the script is a pre-action to a boot group.</span></span> <span data-ttu-id="1893e-179">只有當該群組的 VM 成功地容錯移轉，才會填入值。</span><span class="sxs-lookup"><span data-stu-id="1893e-179">The values are populated only if the VM of that group succeeds in failover.</span></span> <span data-ttu-id="1893e-180">指令碼是開機群組的後續動作。</span><span class="sxs-lookup"><span data-stu-id="1893e-180">The script is a post-action of the boot group.</span></span>

## <a name="use-the-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="1893e-181">在多個復原方案中使用相同的自動化 Runbook</span><span class="sxs-lookup"><span data-stu-id="1893e-181">Use the same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="1893e-182">您可以透過外部變數，在多個復原方案中使用單一指令碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="1893e-183">您可以使用 [Azure 自動化變數](../automation/automation-variables.md)，儲存您在復原方案執行時可傳遞的參數。</span><span class="sxs-lookup"><span data-stu-id="1893e-183">You can use [Azure Automation variables](../automation/automation-variables.md) to store parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="1893e-184">您可以在變數前面加上復原方案名稱，為每個復原方案建立個別變數。</span><span class="sxs-lookup"><span data-stu-id="1893e-184">By adding the recovery plan name as a prefix to the variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="1893e-185">然後，使用這些變數作為參數。</span><span class="sxs-lookup"><span data-stu-id="1893e-185">Then, use the variables as parameters.</span></span> <span data-ttu-id="1893e-186">您可以變更參數而不需要變更指令碼，但仍變更指令碼的運作方式。</span><span class="sxs-lookup"><span data-stu-id="1893e-186">You can change a parameter without changing the script, but still change the way the script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="1893e-187">在 Runbook 指令碼中使用簡單的字串變數</span><span class="sxs-lookup"><span data-stu-id="1893e-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="1893e-188">在此範例中，指令碼會接受網路安全性群組 (NSG) 的輸入，並將其套用至復原方案的 VM。</span><span class="sxs-lookup"><span data-stu-id="1893e-188">In this example, a script takes the input of a Network Security Group (NSG) and applies it to the VMs of a recovery plan.</span></span>

<span data-ttu-id="1893e-189">若要讓指令碼偵測正在執行的復原方案，請使用復原方案內容：</span><span class="sxs-lookup"><span data-stu-id="1893e-189">For the script to detect which recovery plan is running, use the recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="1893e-190">若要套用現有的 NSG，您必須知道 NSG 名稱和 NSG 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-190">To apply an existing NSG, you must know the NSG name and the NSG resource group name.</span></span> <span data-ttu-id="1893e-191">使用這些變數作為復原方案指令碼的輸入。</span><span class="sxs-lookup"><span data-stu-id="1893e-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="1893e-192">若要這樣做，請在自動化帳戶資產中建立兩個變數。</span><span class="sxs-lookup"><span data-stu-id="1893e-192">To do this, create two variables in the Automation account assets.</span></span> <span data-ttu-id="1893e-193">在變數名稱前面加上您要建立參數之復原方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-193">Add the name of the recovery plan that you are creating the parameters for as a prefix to the variable name.</span></span>

1. <span data-ttu-id="1893e-194">建立變數來儲存 NSG 名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-194">Create a variable to store the NSG name.</span></span> <span data-ttu-id="1893e-195">在變數名稱前面加上復原方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-195">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![建立 NSG 名稱變數](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="1893e-197">建立變數來儲存 NSG 的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-197">Create a variable to store the NSG's resource group name.</span></span> <span data-ttu-id="1893e-198">在變數名稱前面加上復原方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-198">Add a prefix to the variable name by using the name of the recovery plan.</span></span>

    ![建立 NSG 資源群組名稱](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="1893e-200">在指令碼中，使用下列參考程式碼來取得變數值：</span><span class="sxs-lookup"><span data-stu-id="1893e-200">In the script, use the following reference code to get the variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="1893e-201">在 Runbook 中使用變數，將 NSG 套用至已容錯移轉之 VM 的網路介面：</span><span class="sxs-lookup"><span data-stu-id="1893e-201">Use the variables in the runbook to apply the NSG to the network interface of the failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply the NSG to a network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="1893e-202">針對每個復原方案，建立獨立變數讓您可以重複使用指令碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-202">For each recovery plan, create independent variables so that you can reuse the script.</span></span> <span data-ttu-id="1893e-203">在開頭加上復原方案名稱。</span><span class="sxs-lookup"><span data-stu-id="1893e-203">Add a prefix by using the recovery plan name.</span></span> <span data-ttu-id="1893e-204">如需此案例的完整端對端指令碼，請參閱 [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee) (在 Site Recovery 復原方案的測試容錯移轉期間將公用 IP 和 NSG 新增至 VM)。</span><span class="sxs-lookup"><span data-stu-id="1893e-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG to VMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-to-store-more-information"></a><span data-ttu-id="1893e-205">使用複雜變數來儲存詳細資訊</span><span class="sxs-lookup"><span data-stu-id="1893e-205">Use a complex variable to store more information</span></span>

<span data-ttu-id="1893e-206">假設您想要一個用來在特定 VM 上開啟公用 IP 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-206">Consider a scenario in which you want a single script to turn on a public IP on specific VMs.</span></span> <span data-ttu-id="1893e-207">在另一個案例中，您可能想要將不同的 NSG 套用至不同的 VM (並非所有 VM)。</span><span class="sxs-lookup"><span data-stu-id="1893e-207">In another scenario, you might want to apply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="1893e-208">您可以讓指令碼可重複使用於任何復原方案。</span><span class="sxs-lookup"><span data-stu-id="1893e-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="1893e-209">每個復原方案可以有任意數目的 VM。</span><span class="sxs-lookup"><span data-stu-id="1893e-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="1893e-210">例如，SharePoint 復原有兩個前端。</span><span class="sxs-lookup"><span data-stu-id="1893e-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="1893e-211">基本企業營運 (LOB) 應用程式只有一個前端。</span><span class="sxs-lookup"><span data-stu-id="1893e-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="1893e-212">您無法為每個復原方案建立個別變數。</span><span class="sxs-lookup"><span data-stu-id="1893e-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="1893e-213">在下列範例中，我們使用新的技術，並在 Azure 自動化帳戶資產中建立[複雜變數](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396)。</span><span class="sxs-lookup"><span data-stu-id="1893e-213">In the following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in the Azure Automation account assets.</span></span> <span data-ttu-id="1893e-214">您可以藉由指定多個值來執行這項作業。</span><span class="sxs-lookup"><span data-stu-id="1893e-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="1893e-215">您必須使用 Azure PowerShell 來完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1893e-215">You must use Azure PowerShell to complete the following steps:</span></span>

1. <span data-ttu-id="1893e-216">在 PowerShell 中，登入您的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="1893e-216">In PowerShell, sign in to your Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="1893e-217">若要儲存參數，請使用復原方案的名稱來建立複雜變數：</span><span class="sxs-lookup"><span data-stu-id="1893e-217">To store the parameters, create the complex variable by using the name of the recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="1893e-218">在此複雜變數中，**VMDetails** 是受保護 VM 的 VM 識別碼。</span><span class="sxs-lookup"><span data-stu-id="1893e-218">In this complex variable, **VMDetails** is the VM ID for the protected VM.</span></span> <span data-ttu-id="1893e-219">您若要取得 VM 識別碼，請在 Azure 入口網站中，檢視 VM 屬性。</span><span class="sxs-lookup"><span data-stu-id="1893e-219">To get the VM ID, in the Azure portal, view the VM properties.</span></span> <span data-ttu-id="1893e-220">下列螢幕擷取畫面顯儲存兩個 VM 之詳細資料的變數：</span><span class="sxs-lookup"><span data-stu-id="1893e-220">The following screenshot shows a variable that stores the details of two VMs:</span></span>

    ![使用 VM 識別碼作為 GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="1893e-222">在您的 Runbook 中使用此變數。</span><span class="sxs-lookup"><span data-stu-id="1893e-222">Use this variable in your runbook.</span></span> <span data-ttu-id="1893e-223">如果在復原方案內容中找到指定的 VM GUID，請將 NSG 套用至 VM：</span><span class="sxs-lookup"><span data-stu-id="1893e-223">If the indicated VM GUID is found in the recovery plan context, apply the NSG on the VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="1893e-224">在您的 Runbook 中，循環存取復原方案內容的 VM。</span><span class="sxs-lookup"><span data-stu-id="1893e-224">In your runbook, loop through the VMs of the recovery plan context.</span></span> <span data-ttu-id="1893e-225">檢查 VM 是否存在於 **$VMDetailsObj** 中。</span><span class="sxs-lookup"><span data-stu-id="1893e-225">Check whether the VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="1893e-226">如果存在的話，則存取變數的屬性來套用 NSG：</span><span class="sxs-lookup"><span data-stu-id="1893e-226">If it exists, access the properties of the variable to apply the NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If the VM exists in the context, this will not b Null
                $VM = $vmMap.$VMID
                # Access the properties of the variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code to apply the NSG properties to the VM
            }
        }
    ```

<span data-ttu-id="1893e-227">您可以將相同的指令碼用於不同的復原方案。</span><span class="sxs-lookup"><span data-stu-id="1893e-227">You can use the same script for different recovery plans.</span></span> <span data-ttu-id="1893e-228">藉由在不同的變數中儲存對應至復原方案的值，來輸入不同的參數。</span><span class="sxs-lookup"><span data-stu-id="1893e-228">Enter different parameters by storing the value that corresponds to a recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="1893e-229">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="1893e-229">Sample scripts</span></span>

<span data-ttu-id="1893e-230">若要將範例指令碼部署至您的自動化帳戶，請按一下 [部署至 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1893e-230">To deploy sample scripts to your Automation account, click the **Deploy to Azure** button.</span></span>

<span data-ttu-id="1893e-231">[![部署至 Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="1893e-231">[![Deploy to Azure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="1893e-232">如需其他範例，請觀看下列影片。</span><span class="sxs-lookup"><span data-stu-id="1893e-232">For another example, see the following video.</span></span> <span data-ttu-id="1893e-233">該影片示範如何將兩層式 WordPress 應用程式復原至 Azure：</span><span class="sxs-lookup"><span data-stu-id="1893e-233">It demonstrates how to recover a two-tier WordPress application to Azure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="1893e-234">其他資源</span><span class="sxs-lookup"><span data-stu-id="1893e-234">Additional resources</span></span>
* [<span data-ttu-id="1893e-235">Azure 自動化服務執行身分帳戶</span><span class="sxs-lookup"><span data-stu-id="1893e-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="1893e-236">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="1893e-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Azure 自動化概觀")
* [<span data-ttu-id="1893e-237">Azure 自動化範例指令碼</span><span class="sxs-lookup"><span data-stu-id="1893e-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Azure 自動化範例指令碼")
