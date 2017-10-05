---
title: "Runbook 設定 |Microsoft Docs"
description: "描述 Azure 自動化中 Runbook 的組態設定，以及如何使用 Azure 管理入口網站和 Windows PowerShell 來加以變更。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 20ecbc270e61d234e026e6ba2634c7aad63b3355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="e1c0a-103">Runbook 設定</span><span class="sxs-lookup"><span data-stu-id="e1c0a-103">Runbook settings</span></span>
<span data-ttu-id="e1c0a-104">Azure 自動化中的每個 Runbook 具備多個有助於識別其本身及變更其記錄行為的設定。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-104">Each runbook in Azure Automation has multiple settings that help it to be identified and to change its logging behavior.</span></span> <span data-ttu-id="e1c0a-105">以下會說明這些設定，後面則是如何加以修改的程序。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-105">Each of these settings is described below followed by procedures on how to modify them.</span></span>

## <a name="settings"></a><span data-ttu-id="e1c0a-106">Settings</span><span class="sxs-lookup"><span data-stu-id="e1c0a-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="e1c0a-107">名稱和描述</span><span class="sxs-lookup"><span data-stu-id="e1c0a-107">Name and description</span></span>
<span data-ttu-id="e1c0a-108">建立 Runbook 之後，您即無法變更其名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-108">You cannot change the name of a runbook after it has been created.</span></span> <span data-ttu-id="e1c0a-109">描述是選擇性的，而且最多可以是 512 個字元。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-109">The Description is optional and can be up to 512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="e1c0a-110">標記</span><span class="sxs-lookup"><span data-stu-id="e1c0a-110">Tags</span></span>
<span data-ttu-id="e1c0a-111">標記可讓您指派不同的單字和片語，有助於識別 Runbook。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-111">Tags allow you to assign distinct words and phrases to help identify a runbook.</span></span> <span data-ttu-id="e1c0a-112">例如，將 Runbook 提交到 [PowerShell 資源庫](https://www.powershellgallery.com/)時，您會指定特定的標記來識別應該列出此 Runbook 的分類。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-112">For example, when you submit a runbook to the [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags to identify which categories the runbook should be listed in.</span></span> <span data-ttu-id="e1c0a-113">您可以為 Runbook 指定多個標記，使用逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="e1c0a-114">記錄</span><span class="sxs-lookup"><span data-stu-id="e1c0a-114">Logging</span></span>
<span data-ttu-id="e1c0a-115">依預設，詳細資訊和進度記錄不會寫入工作歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-115">By default, Verbose and Progress records are not written to job history.</span></span> <span data-ttu-id="e1c0a-116">您可以變更特定 Runbook 的設定來記錄這些記錄。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-116">You can change the settings for a particular runbook to log these records.</span></span> <span data-ttu-id="e1c0a-117">如需有關這些記錄的詳細資訊，請參閱 [Runbook 輸出和訊息](automation-runbook-output-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="e1c0a-118">變更 Runbook 設定</span><span class="sxs-lookup"><span data-stu-id="e1c0a-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-the-azure-portal"></a><span data-ttu-id="e1c0a-119">使用 Azure 入口網站變更 Runbook 設定</span><span class="sxs-lookup"><span data-stu-id="e1c0a-119">Changing runbook settings with the Azure portal</span></span>
<span data-ttu-id="e1c0a-120">您可以在 Azure 入口網站中 Runbook 的 [設定] 刀鋒視窗上變更 Runbook 的設定。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-120">You can change settings for a runbook in the Azure portal from the **Settings** blade for the runbook.</span></span>

1. <span data-ttu-id="e1c0a-121">在 Azure 入口網站中，選取 [ **自動化** ]，然後按一下自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-121">In the Azure portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="e1c0a-122">選取 [ **Runbook** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-122">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="e1c0a-123">按一下 Runbook 的名稱，然後系統會將您導向至該 Runbook 的 [設定] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-123">Click the name of a runbook and you are directed to the settings blade for the runbook.</span></span> <span data-ttu-id="e1c0a-124">您可以在此處指定或修改標記、Runbook 描述、設定記錄和追蹤設定，以及存取支援工具來協助您解決問題。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-124">From here you can specify or modify tags, the runbook description, configure logging and tracing settings, and access support tools to help you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="e1c0a-125">使用 Windows PowerShell 變更 Runbook 設定</span><span class="sxs-lookup"><span data-stu-id="e1c0a-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="e1c0a-126">您可以使用 [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) Cmdlet 來變更 Runbook 的設定。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-126">You can use the [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet to change the settings for a runbook.</span></span> <span data-ttu-id="e1c0a-127">如果您想要指定多個標記，可以對標記參數提供陣列或單一字串 (使用逗號分隔值)。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-127">If you want to specify multiple tags, you can either provide an array or a single string with comma delimited values to the Tags parameter.</span></span> <span data-ttu-id="e1c0a-128">您可以使用 [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx) 來取得目前的標記。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-128">You can get the current tags with the [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="e1c0a-129">下列命令範例示範如何設定 Runbook 的屬性。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-129">The following sample commands show how to set the properties for a runbook.</span></span> <span data-ttu-id="e1c0a-130">此範例會將三個標記加入至現有的標記，並指定應該記錄詳細記錄。</span><span class="sxs-lookup"><span data-stu-id="e1c0a-130">This sample adds three tags to the existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="e1c0a-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e1c0a-131">Next steps</span></span>
* <span data-ttu-id="e1c0a-132">若要了解如何建立及擷取 Runbook 的輸出與錯誤訊息，請參閱 [Runbook 輸出與訊息](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="e1c0a-132">To learn how to create and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="e1c0a-133">若要了解如何新增社群或其他來源已經開發的 Runbook，或建立您自己的 Runbook，請參閱[建立或匯入 Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="e1c0a-133">To understand how to add a runbook that was already developed by the community or other source, or to create your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

