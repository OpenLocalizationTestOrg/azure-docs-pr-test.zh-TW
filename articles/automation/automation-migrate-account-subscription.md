---
title: "aaaMigrate 自動化帳戶和資源 |Microsoft 文件"
description: "本文說明如何 toomove 自動化帳戶在 Azure 自動化和相關聯的資源從一個訂用帳戶 tooanother。"
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
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a><span data-ttu-id="df6cb-103">移轉自動化帳戶和資源</span><span class="sxs-lookup"><span data-stu-id="df6cb-103">Migrate Automation Account and resources</span></span>
<span data-ttu-id="df6cb-104">自動化帳戶和其相關聯的資源 （例如資產、 runbook、 模組、 等等） 已在 hello Azure 入口網站中建立，而且想要從一個資源 toomigrate 群組 tooanother 或從一個訂用帳戶 tooanother，您可以完成這項作業輕鬆地與hello[資源移](../azure-resource-manager/resource-group-move-resources.md)hello Azure 入口網站中可用功能。</span><span class="sxs-lookup"><span data-stu-id="df6cb-104">For Automation accounts and its associated resources (i.e. assets, runbooks, modules, etc.) that you have created in hello Azure portal and want toomigrate from one resource group tooanother or from one subscription tooanother, you can accomplish this easily with hello [move resources](../azure-resource-manager/resource-group-move-resources.md) feature available in hello Azure portal.</span></span> <span data-ttu-id="df6cb-105">不過，此動作之前，您應該先檢閱下列 hello[之前移動資源的檢查清單](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources)，此外，hello 特定 tooAutomation 下方的清單。</span><span class="sxs-lookup"><span data-stu-id="df6cb-105">However, before proceeding with this action, you should first review hello following [checklist before moving resources](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) and additionally, hello list below specific tooAutomation.</span></span>   

1. <span data-ttu-id="df6cb-106">hello 目的地訂用帳戶/資源群組必須與 hello 來源相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="df6cb-106">hello destination subscription/resource group must be in same region as hello source.</span></span>  <span data-ttu-id="df6cb-107">這表示，無法跨區域移動自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="df6cb-107">Meaning, Automation accounts cannot be moved across regions.</span></span>
2. <span data-ttu-id="df6cb-108">當您移動資源 （例如 runbook、 作業、 等等），hello 來源群組及 hello 目標群組被鎖住 hello hello 作業持續期間。</span><span class="sxs-lookup"><span data-stu-id="df6cb-108">When moving resources (e.g. runbooks, jobs, etc.), both hello source group and hello target group are locked for hello duration of hello operation.</span></span> <span data-ttu-id="df6cb-109">寫入和刪除作業 hello 移動作業完成之前被封鎖於 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="df6cb-109">Write and delete operations are blocked on hello groups until hello move completes.</span></span>  
3. <span data-ttu-id="df6cb-110">任何 runbook 或變數參考 hello 現有訂用帳戶的資源或訂用帳戶 ID 必須 toobe 移轉完成之後更新。</span><span class="sxs-lookup"><span data-stu-id="df6cb-110">Any runbooks or variables which reference a resource or subscription ID from hello existing subscription will need toobe updated after migration is completed.</span></span>   

> [!NOTE]
> <span data-ttu-id="df6cb-111">這項功能不支援移動傳統自動化資源。</span><span class="sxs-lookup"><span data-stu-id="df6cb-111">This feature does not support moving Classic automation resources.</span></span>
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a><span data-ttu-id="df6cb-112">toomove hello 使用 hello 入口網站的自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="df6cb-112">toomove hello Automation Account using hello portal</span></span>
1. <span data-ttu-id="df6cb-113">從您的自動化帳戶，按一下 **移動**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="df6cb-113">From your Automation account, click **Move** at hello top of hello blade.</span></span><br> <span data-ttu-id="df6cb-114">![移動選項](media/automation-migrate-account-subscription/automation-menu-move.png)</span><span class="sxs-lookup"><span data-stu-id="df6cb-114">![Move option](media/automation-migrate-account-subscription/automation-menu-move.png)</span></span><br>
2. <span data-ttu-id="df6cb-115">在 hello**資源移**刀鋒視窗時，請注意，它會呈現資源相關的 tooboth 自動化帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="df6cb-115">On hello **Move resources** blade, note that it presents resources related tooboth your Automation account and your resource group(s).</span></span>  <span data-ttu-id="df6cb-116">選取 hello**訂用帳戶**和**資源群組**hello 下拉式清單或選取 hello 選項從**建立新的資源群組**並輸入新的資源群組名稱中提供的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="df6cb-116">Select hello **subscription** and **resource group** from hello drop-down lists, or select hello option **create a new resource group** and enter a new resource group name in hello field provided.</span></span>  
3. <span data-ttu-id="df6cb-117">檢閱和選取 hello 核取方塊 tooacknowledge 您*了解工具和指令碼將會需要更新 toobe toouse 新的資源 Id 後已經移動資源*，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="df6cb-117">Review and select hello checkbox tooacknowledge you *understand tools and scripts will need toobe updated toouse new resource IDs after resources have been moved* and then click **OK**.</span></span><br> <span data-ttu-id="df6cb-118">![移動資源刀鋒視窗](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span><span class="sxs-lookup"><span data-stu-id="df6cb-118">![Move Resources Blade](media/automation-migrate-account-subscription/automation-move-resources-blade.png)</span></span><br>   

<span data-ttu-id="df6cb-119">這個動作將會需要幾分鐘的時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="df6cb-119">This action will take several minutes toocomplete.</span></span>  <span data-ttu-id="df6cb-120">在 [通知] 中，您會看到所進行的每個動作 (驗證、移轉) 的狀態，然後最後是完成的時間。</span><span class="sxs-lookup"><span data-stu-id="df6cb-120">In **Notifications**, you will be presented with a status of each action that takes place - validation, migration, and then finally when it is completed.</span></span>     

## <a name="toomove-hello-automation-account-using-powershell"></a><span data-ttu-id="df6cb-121">toomove hello 使用 PowerShell 的自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="df6cb-121">toomove hello Automation Account using PowerShell</span></span>
<span data-ttu-id="df6cb-122">toomove 現有自動化資源 tooanother 資源群組或訂用帳戶，使用 hello **Get AzureRmResource** cmdlet tooget hello 特定自動化帳戶，然後**Move-azurermresource**cmdlet tooperform hello 移動。</span><span class="sxs-lookup"><span data-stu-id="df6cb-122">toomove existing Automation resources tooanother resource group or subscription, use hello  **Get-AzureRmResource** cmdlet tooget hello specific Automation account and then **Move-AzureRmResource** cmdlet tooperform hello move.</span></span>

<span data-ttu-id="df6cb-123">hello 第一個範例顯示如何 toomove 自動化帳戶 tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="df6cb-123">hello first example shows how toomove an Automation account tooa new resource group.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

<span data-ttu-id="df6cb-124">執行上述程式碼範例的 hello 之後，您會想 tooperform 此動作的提示的 tooverify。</span><span class="sxs-lookup"><span data-stu-id="df6cb-124">After you execute hello above code example, you will be prompted tooverify you want tooperform this action.</span></span>  <span data-ttu-id="df6cb-125">一旦您按一下**是**並允許 hello tooproceed 指令碼，您不會執行 hello 移轉時收到任何通知。</span><span class="sxs-lookup"><span data-stu-id="df6cb-125">Once you click **Yes** and allow hello script tooproceed, you will not receive any notifications while it's performing hello migration.</span></span>  

<span data-ttu-id="df6cb-126">toomove tooa 新訂用帳戶，包含的值 hello *DestinationSubscriptionId*參數。</span><span class="sxs-lookup"><span data-stu-id="df6cb-126">toomove tooa new subscription, include a value for hello *DestinationSubscriptionId* parameter.</span></span>

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

<span data-ttu-id="df6cb-127">如同 hello 上述範例中，您將會提示的 tooconfirm hello 移動。</span><span class="sxs-lookup"><span data-stu-id="df6cb-127">As with hello previous example, you will be prompted tooconfirm hello move.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="df6cb-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df6cb-128">Next steps</span></span>
* <span data-ttu-id="df6cb-129">如需移動資源 toonew 資源群組或訂用帳戶的詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](../azure-resource-manager/resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="df6cb-129">For more information about moving resources toonew resource group or subscription, see [Move  resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md)</span></span>
* <span data-ttu-id="df6cb-130">如需有關在 Azure 自動化中的 角色型存取控制的詳細資訊，請參閱太[Azure 自動化中的角色型存取控制](automation-role-based-access-control.md)。</span><span class="sxs-lookup"><span data-stu-id="df6cb-130">For more information about Role-based Access Control in Azure Automation, refer too[Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="df6cb-131">toolearn 相關 PowerShell cmdlet 來管理您的訂閱，請參閱[使用 Azure PowerShell 與資源管理員](../azure-resource-manager/powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="df6cb-131">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)</span></span>
* <span data-ttu-id="df6cb-132">toolearn 有關入口網站功能來管理您的訂閱，請參閱[使用 hello Azure 入口網站 toomanage 資源](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="df6cb-132">toolearn about portal features for managing your subscription, see [Using hello Azure Portal toomanage resources](../azure-resource-manager/resource-group-portal.md).</span></span>
