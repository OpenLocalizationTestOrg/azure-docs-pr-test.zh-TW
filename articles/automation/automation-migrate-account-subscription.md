---
title: "移轉自動化帳戶和資源 | Microsoft Docs"
description: "本文章說明如何將 Azure 自動化中的自動化帳戶和相關聯的資源，從某一個訂用帳戶移到另一個訂用帳戶。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="87731-103">移轉自動化帳戶和資源</span><span class="sxs-lookup"><span data-stu-id="87731-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="87731-104">對於您在 Azure 入口網站中建立並且想要在資源群組或訂用帳戶之間移轉的自動化帳戶及其相關資源 (例如資產、Runbook、模組等)，您可以使用 Azure 入口網站中可用的[移動資源](../azure-resource-manager/resource-group-move-resources.md)功能，輕鬆完成這項作業。</span><span class="sxs-lookup"><span data-stu-id="87731-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in the Azure portal and want to migrate from one resource group to another or from one subscription to another, you can accomplish this easily with the [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in the Azure portal.</span></span> <span data-ttu-id="87731-105">不過，在繼續此動作之前，您應該先檢閱下列[檢查清單再移動資源](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources)，此外，還需檢閱以下自動化專用的清單。</span><span class="sxs-lookup"><span data-stu-id="87731-105">However, before proceeding with this action, you should first review the following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, the list below specific to Automation.</span></span>   

1. <span data-ttu-id="87731-106">目的地訂用帳戶/資源群組必須位於與來源相同的區域。</span><span class="sxs-lookup"><span data-stu-id="87731-106">The destination subscription/resource group must be in same region as the source.</span></span>  <span data-ttu-id="87731-107">這表示，無法跨區域移動自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="87731-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="87731-108">移動資源 (如 Runbook、作業等) 時，會在作業期間鎖定來源群組和目標群組。</span><span class="sxs-lookup"><span data-stu-id="87731-108">When moving resources (e.g. runbooks, jobs, etc.), both the source group and the target group are locked for the duration of the operation.</span></span> <span data-ttu-id="87731-109">群組上的寫入和刪除作業將會封鎖，直到移動完成。</span><span class="sxs-lookup"><span data-stu-id="87731-109">Write and delete operations are blocked on the groups until the move completes.</span></span>  
3. <span data-ttu-id="87731-110">在移轉完成之後，需要更新任何參考現有訂用帳戶中資源或訂用帳戶識別碼的 Runbook 或變數。</span><span class="sxs-lookup"><span data-stu-id="87731-110">Any runbooks or variables which reference a resource or subscription ID from the existing subscription will need to be updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="87731-111">這項功能不支援移動傳統自動化資源。</span><span class="sxs-lookup"><span data-stu-id="87731-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a><span data-ttu-id="87731-112">使用入口網站移動自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="87731-112">To move the Automation Account using the portal</span></span>
1. <span data-ttu-id="87731-113">從您的自動化帳戶，按一下刀鋒視窗頂端的 [移動]。</span><span class="sxs-lookup"><span data-stu-id="87731-113">From your Automation account, click **Move** at the top of the blade.</span></span><br> <span data-ttu-id="87731-114">![移動選項](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="87731-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="87731-115">在 [移動資源] 刀鋒視窗上，請注意它會顯示與您的自動化帳戶和資源群組相關的資源。</span><span class="sxs-lookup"><span data-stu-id="87731-115">On the **Move resources** blade, note that it presents resources related to both your Automation account and your resource group(s).</span></span>  <span data-ttu-id="87731-116">從下拉式清單中選取 [訂用帳戶] 和 [資源群組] ，或選取 [建立新的資源群組] 選項並且在提供的欄位中輸入新的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="87731-116">Select the **subscription** and **resource group** from the drop-down lists, or select the option **create a new resource group** and enter a new resource group name in the field provided.</span></span>  
3. <span data-ttu-id="87731-117">檢閱並選取核取方塊，以確認您「了解工具和指令碼需要更新，才能在移動資源後使用新的資源識別碼」，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="87731-117">Review and select the checkbox to acknowledge you *understand tools and scripts will need to be updated to use new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="87731-118">![移動資源刀鋒視窗](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="87731-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="87731-119">此動作需要幾分鐘時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="87731-119">This action will take several minutes to complete.</span></span>  <span data-ttu-id="87731-120">在 [通知] 中，您會看到所進行的每個動作 (驗證、移轉) 的狀態，然後最後是完成的時間。</span><span class="sxs-lookup"><span data-stu-id="87731-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="to-move-the-automation-account-using-powershell"></a><span data-ttu-id="87731-121">使用 PowerShell 移動自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="87731-121">To move the Automation Account using PowerShell</span></span>
<span data-ttu-id="87731-122">若要將現有的自動化資源移至另一個資源群組或訂用帳戶，請使用 **Get-AzureRmResource** Cmdlet 來取得特定的自動化帳戶，然後使用 **Move-AzureRmResource** Cmdlet 來執行移動。</span><span class="sxs-lookup"><span data-stu-id="87731-122">To move existing Automation resources to another resource group or subscription, use the  **Get-AzureRmResource** cmdlet to get the specific Automation account and then **Move-AzureRmResource** cmdlet to perform the move.</span></span>

<span data-ttu-id="87731-123">第一個範例示範如何將自動化帳戶移到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="87731-123">The first example shows how to move an Automation account to a new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="87731-124">執行上述程式碼範例之後，系統會提示您確認您要執行此動作。</span><span class="sxs-lookup"><span data-stu-id="87731-124">After you execute the above code example, you will be prompted to verify you want to perform this action.</span></span>  <span data-ttu-id="87731-125">一旦按一下 [是]  並允許繼續執行指令碼，您就不會在執行移轉時收到任何通知。</span><span class="sxs-lookup"><span data-stu-id="87731-125">Once you click **Yes** and allow the script to proceed, you will not receive any notifications while it's performing the migration.</span></span>  

<span data-ttu-id="87731-126">若要移動到新的訂用帳戶，請為 *DestinationSubscriptionId* 參數設定某個值。</span><span class="sxs-lookup"><span data-stu-id="87731-126">To move to a new subscription, include a value for the *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="87731-127">如同上述範例，系統會提示您確認移動。</span><span class="sxs-lookup"><span data-stu-id="87731-127">As with the previous example, you will be prompted to confirm the move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="87731-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87731-128">Next steps</span></span>
* <span data-ttu-id="87731-129">如需將資源移到新的資源群組或訂用帳戶的詳細資訊，請參閱[將資源移到新的資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="87731-129">For more information about moving resources to new resource group or subscription, see [Move  resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="87731-130">如需 Azure 自動化中角色型存取控制的詳細資訊，請參閱 [Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="87731-130">For more information about Role-based Access Control in Azure Automation, refer to [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="87731-131">若要了解用於管理訂用帳戶的 PowerShell Cmdlet，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="87731-131">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="87731-132">若要了解用於管理訂用帳戶的入口網站功能，請參閱 [使用 Azure 入口網站來管理資源](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="87731-132">To learn about portal features for managing your subscription, see [Using the Azure Portal to manage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
