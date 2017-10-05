---
title: "更新 Azure 自動化中的 Azure 模組 | Microsoft Docs"
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
ms.openlocfilehash: ed8c97b642d406a05817ec6c67f31a1b4bce93b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-update-azure-powershell-modules-in-azure-automation"></a><span data-ttu-id="51721-103">如何更新 Azure 自動化中的 Azure PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="51721-103">How to update Azure PowerShell modules in Azure Automation</span></span>

<span data-ttu-id="51721-104">每個自動化帳戶依預設都會提供最通用的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="51721-104">The most common Azure PowerShell modules are provided by default in each Automation account.</span></span>  <span data-ttu-id="51721-105">Azure 小組會定期更新 Azure 模組，因此在自動化帳戶中，我們會提供方法供您在入口網站有新的版本可供使用時，更新帳戶中的模組。</span><span class="sxs-lookup"><span data-stu-id="51721-105">The Azure team updates the Azure modules regularly, so in the Automation account we provide a way for you to update the modules in the account when new versions are available from the portal.</span></span>  

<span data-ttu-id="51721-106">因為會根據產品群組定期更新模組，所以內含 Cmdlet 可能會變更，這樣可能會根據變更類型 (例如重新命名參數，或完全淘汰 Cmdlet) 對 Runbook 造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="51721-106">Because modules are updated regularly by the product group, changes can occur with the  included cmdlets, which may negatively impact your runbooks depending on the type of change, such as renaming a parameter or deprecating a cmdlet entirely.</span></span> <span data-ttu-id="51721-107">若要避免影響 Runbook 以及它們所自動化的處理序，強烈建議您先進行測試和驗證，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="51721-107">To avoid impacting your runbooks and the processes they automate, it is strongly recommended that you test and validate before proceeding.</span></span>  <span data-ttu-id="51721-108">如果您沒有適用於此用途的專用自動化帳戶，請考慮建立自動化帳戶，讓您除了更新 PowerShell 模組這類反覆變更之外，還可以在開發 Runbook 期間測試許多不同的案例和排列。</span><span class="sxs-lookup"><span data-stu-id="51721-108">If you do not have a dedicated Automation account intended for this purpose, consider creating one so that you can test many different scenarios and permutations during the development of your runbooks, in addition to iterative changes such as updating the PowerShell modules.</span></span>  <span data-ttu-id="51721-109">驗證結果且套用任何所需變更之後，請繼續協調任何需要修改之 Runbook 的移轉，並如下所述在生產環境中執行更新。</span><span class="sxs-lookup"><span data-stu-id="51721-109">After the results are validated and you have applied any changes required, proceed with coordinating the migration of any runbooks that required modification and perform the update as described below in production.</span></span>     

## <a name="updating-azure-modules"></a><span data-ttu-id="51721-110">更新 Azure 模組</span><span class="sxs-lookup"><span data-stu-id="51721-110">Updating Azure Modules</span></span>

1. <span data-ttu-id="51721-111">自動化帳戶的 [模組] 刀鋒視窗中有一個稱為**更新 Azure 模組**的選項。</span><span class="sxs-lookup"><span data-stu-id="51721-111">In the Modules blade of your Automation account there is an option called **Update Azure Modules**.</span></span>  <span data-ttu-id="51721-112">它一律為啟用狀態。</span><span class="sxs-lookup"><span data-stu-id="51721-112">It is always enabled.</span></span><br><br> <span data-ttu-id="51721-113">![[模組] 刀鋒視窗中的 [更新 Azure 模組] 選項](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span><span class="sxs-lookup"><span data-stu-id="51721-113">![Update Azure Modules option in Modules blade](media/automation-update-azure-modules/automation-update-azure-modules-option.png)</span></span>

2. <span data-ttu-id="51721-114">按一下 [更新 Azure 模組]，您便會看到確認通知，詢問您是否要繼續。</span><span class="sxs-lookup"><span data-stu-id="51721-114">Click **Update Azure Modules** and you will be presented with a confirmation notification that asks you if you want to continue.</span></span><br><br> <span data-ttu-id="51721-115">![更新 Azure 模組通知](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span><span class="sxs-lookup"><span data-stu-id="51721-115">![Update Azure Modules notification](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)</span></span>

3. <span data-ttu-id="51721-116">按一下 [是]便會開始模組更新程序。</span><span class="sxs-lookup"><span data-stu-id="51721-116">Click **Yes** and the module update process will begin.</span></span>  <span data-ttu-id="51721-117">更新程序大約需要 15-20 分鐘來更新下列模組︰</span><span class="sxs-lookup"><span data-stu-id="51721-117">The update process takes about 15-20 minutes to update the following modules:</span></span>

  * <span data-ttu-id="51721-118">Azure</span><span class="sxs-lookup"><span data-stu-id="51721-118">Azure</span></span>
  * <span data-ttu-id="51721-119">Azure.Storage</span><span class="sxs-lookup"><span data-stu-id="51721-119">Azure.Storage</span></span>
  * <span data-ttu-id="51721-120">AzureRm.Automation</span><span class="sxs-lookup"><span data-stu-id="51721-120">AzureRm.Automation</span></span>
  * <span data-ttu-id="51721-121">AzureRm.Compute</span><span class="sxs-lookup"><span data-stu-id="51721-121">AzureRm.Compute</span></span>
  * <span data-ttu-id="51721-122">AzureRm.Profile</span><span class="sxs-lookup"><span data-stu-id="51721-122">AzureRm.Profile</span></span>
  * <span data-ttu-id="51721-123">AzureRm.Resources</span><span class="sxs-lookup"><span data-stu-id="51721-123">AzureRm.Resources</span></span>
  * <span data-ttu-id="51721-124">AzureRm.Sql</span><span class="sxs-lookup"><span data-stu-id="51721-124">AzureRm.Sql</span></span>
  * <span data-ttu-id="51721-125">AzureRm.Storage</span><span class="sxs-lookup"><span data-stu-id="51721-125">AzureRm.Storage</span></span>

    <span data-ttu-id="51721-126">如果模組已是最新狀態，此程序在幾秒鐘內便會完成。</span><span class="sxs-lookup"><span data-stu-id="51721-126">If the modules are already up to date, then the process will complete in a few seconds.</span></span>  <span data-ttu-id="51721-127">更新程序完成時，您會收到通知。</span><span class="sxs-lookup"><span data-stu-id="51721-127">When the update process completes you will be notified.</span></span><br><br> ![更新 Azure 模組更新狀態](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> <span data-ttu-id="51721-129">執行新的排程工作時，Azure 自動化會使用自動化帳戶中的最新模組。</span><span class="sxs-lookup"><span data-stu-id="51721-129">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>    

<span data-ttu-id="51721-130">如果您在 Runbook 中使用來自這些 Azure PowerShell 模組的 Cmdlet 來管理 Azure 資源，則您會想要每隔大約一個月執行一次此更新程序，以確保您擁有最新模組。</span><span class="sxs-lookup"><span data-stu-id="51721-130">If you use cmdlets from these Azure PowerShell modules in your runbooks to manage Azure resources, then you will want to perform this update process every month or so to assure that you have the latest modules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51721-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51721-131">Next steps</span></span>

* <span data-ttu-id="51721-132">若要深入了解整合模組，以及如何建立自訂模組以進一步整合自動化與其他系統、服務或解決方案，請參閱[整合模組](automation-integration-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="51721-132">To learn more about Integration Modules and how to create custom modules to further integrate Automation with other systems, services, or solutions, see [Integration Modules](automation-integration-modules.md).</span></span>

* <span data-ttu-id="51721-133">請考慮使用 [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) 或 [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) 的原始檔控制整合，以集中管理和控制自動化 Runbook 和設定組合的發行。</span><span class="sxs-lookup"><span data-stu-id="51721-133">Consider source control integration using [GitHub Enterprise](automation-scenario-source-control-integration-with-github-ent.md) or [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) to centrally manage and control releases of your Automation runbook and configuration portfolio.</span></span>  