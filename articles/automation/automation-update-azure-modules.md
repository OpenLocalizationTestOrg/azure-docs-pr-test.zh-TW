---
title: "aaaUpdate Azure 在 Azure 自動化模組 |Microsoft 文件"
description: "本文說明現在要如何更新 Azure 自動化中預設提供的通用 Azure PowerShell 模組。"
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="23bb8-103">如何在 Azure 自動化中的 tooupdate Azure PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="23bb8-103">How tooupdate Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="23bb8-104">hello 最常見的 Azure PowerShell 模組會提供預設會在每個自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="23bb8-104">hello most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="23bb8-105">hello Azure 團隊更新定期 hello Azure 模組，以便在 hello 自動化帳戶中我們提供一種您 tooupdate hello 帳戶中的 hello 模組從 hello 入口網站的新版本可用時。</span><span class="sxs-lookup"><span data-stu-id="23bb8-105">hello Azure team updates hello Azure modules regularly, so in hello Automation account we provide a way for you tooupdate hello modules in hello account when new versions are available from hello portal.</span></span>  

<span data-ttu-id="23bb8-106">模組會定期更新 hello 產品群組，因為變更可能會發生與 hello 包含 cmdlet，這可能會對您的 runbook，根據 hello 類型變更，例如重新命名的參數，或完全淘汰 cmdlet 產生負面影響。</span><span class="sxs-lookup"><span data-stu-id="23bb8-106">Because modules are updated regularly by hello product group, changes can occur with hello  included cmdlets, which may negatively impact your runbooks depending on hello type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="23bb8-107">影響您的 runbook 和 hello tooavoid 自動化程序，強烈建議您測試和驗證，然後再繼續。</span><span class="sxs-lookup"><span data-stu-id="23bb8-107">tooavoid impacting your runbooks and hello processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="23bb8-108">如果您沒有適用於此用途的專用的自動化帳戶，請考慮建立一個，以便您可以測試許多不同的案例和排列您的 runbook，加法 tooiterative 變更，例如更新 hello hello 開發期間PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="23bb8-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during hello development of your runbooks, in addition tooiterative changes such as updating hello PowerShell modules.</span></span>  <span data-ttu-id="23bb8-109">Hello 結果會進行驗證，而且您已套用所需的任何變更之後，繼續進行協調 hello 移轉的需要修改任何 runbook，並執行 hello 更新，如下所述在生產環境中。</span><span class="sxs-lookup"><span data-stu-id="23bb8-109">After hello results are validated and you have applied any changes required, proceed with coordinating hello migration of any runbooks that required modification and perform hello update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="23bb8-110">更新 Azure 模組</span><span class="sxs-lookup"><span data-stu-id="23bb8-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="23bb8-111">Hello 模組中您的自動化帳戶有刀鋒視窗是選項呼叫**更新 Azure 模組**。</span><span class="sxs-lookup"><span data-stu-id="23bb8-111">In hello Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="23bb8-112">它一律為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="23bb8-112">It is always enabled.</span></span><br><br> <span data-ttu-id="23bb8-113">![[模組] 刀鋒視窗中的 [更新 Azure 模組] 選項](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="23bb8-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="23bb8-114">按一下**更新 Azure 模組**，您將會出現詢問您是否 toocontinue 確認通知。</span><span class="sxs-lookup"><span data-stu-id="23bb8-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want toocontinue.</span></span><br><br> <span data-ttu-id="23bb8-115">![更新 Azure 模組通知](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="23bb8-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="23bb8-116">按一下**是**hello 模組更新程序會開始。</span><span class="sxs-lookup"><span data-stu-id="23bb8-116">Click **Yes** and hello module update process will begin.</span></span>  <span data-ttu-id="23bb8-117">hello 更新程序，大約需要 15 20 分鐘 tooupdate hello 下列模組：</span><span class="sxs-lookup"><span data-stu-id="23bb8-117">hello update process takes about 15-20 minutes tooupdate hello following modules:</span></span>

  * <span data-ttu-id="23bb8-118">Azure</span><span class="sxs-lookup"><span data-stu-id="23bb8-118">Azure</span></span>
  * <span data-ttu-id="23bb8-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="23bb8-119">Azure.Storage</span></span>
  * <span data-ttu-id="23bb8-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="23bb8-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="23bb8-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="23bb8-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="23bb8-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="23bb8-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="23bb8-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="23bb8-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="23bb8-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="23bb8-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="23bb8-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="23bb8-125">AzureRm.Storage</span></span>

    <span data-ttu-id="23bb8-126">如果 hello 模組已經註冊 toodate，hello 程序將會完成在幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="23bb8-126">If hello modules are already up toodate, then hello process will complete in a few seconds.</span></span>  <span data-ttu-id="23bb8-127">Hello 更新程序完成時將會通知您。</span><span class="sxs-lookup"><span data-stu-id="23bb8-127">When hello update process completes you will be notified.</span></span><br><br> ![更新 Azure 模組更新狀態](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="23bb8-129">Azure 自動化會使用 hello 最新的模組，您的自動化帳戶中，新的排程的工作執行時。</span><span class="sxs-lookup"><span data-stu-id="23bb8-129">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="23bb8-130">如果您使用 cmdlet 從您的 runbook toomanage Azure 在這些 Azure PowerShell 模組的資源，則您會想 tooperform 這個更新程序每月或您擁有的 tooassure 因此 hello 最新的模組。</span><span class="sxs-lookup"><span data-stu-id="23bb8-130">If you use cmdlets from these Azure PowerShell modules in your runbooks toomanage Azure resources, then you will want tooperform this update process every month or so tooassure that you have hello latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23bb8-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23bb8-131">Next steps</span></span>

* <span data-ttu-id="23bb8-132">toolearn 深入了解整合模組和 toocreate 自訂模組 toofurther 如何整合自動化與其他系統、 服務或方案，請參閱[整合模組](automation-integration-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="23bb8-132">toolearn more about Integration Modules and how toocreate custom modules toofurther integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="23bb8-133">請考慮使用的原始檔控制整合[GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md)或[Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally 管理和控制自動化 runbook 及設定組合的版本。</span><span class="sxs-lookup"><span data-stu-id="23bb8-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  
