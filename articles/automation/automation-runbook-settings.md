---
title: "aaaRunbook 設定 |Microsoft 文件"
description: "描述 Azure 自動化中 runbook 的 hello 組態設定以及如何 toochange 它們兩者都使用 hello Azure 管理入口網站和 Windows PowerShell。"
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
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a><span data-ttu-id="3291f-103">Runbook 設定</span><span class="sxs-lookup"><span data-stu-id="3291f-103">Runbook settings</span></span>
<span data-ttu-id="3291f-104">在 Azure 自動化中的每個 runbook 都有多項設定可協助它 toobe 識別和 toochange 其登入行為。</span><span class="sxs-lookup"><span data-stu-id="3291f-104">Each runbook in Azure Automation has multiple settings that help it toobe identified and toochange its logging behavior.</span></span> <span data-ttu-id="3291f-105">這些設定下面會描述如何在程序之後 toomodify 它們。</span><span class="sxs-lookup"><span data-stu-id="3291f-105">Each of these settings is described below followed by procedures on how toomodify them.</span></span>

## <a name="settings"></a><span data-ttu-id="3291f-106">設定</span><span class="sxs-lookup"><span data-stu-id="3291f-106">Settings</span></span>
### <a name="name-and-description"></a><span data-ttu-id="3291f-107">名稱和描述</span><span class="sxs-lookup"><span data-stu-id="3291f-107">Name and description</span></span>
<span data-ttu-id="3291f-108">一旦建立後，您無法變更 hello runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="3291f-108">You cannot change hello name of a runbook after it has been created.</span></span> <span data-ttu-id="3291f-109">hello 描述是選擇性的而且可以是 too512 字元組成。</span><span class="sxs-lookup"><span data-stu-id="3291f-109">hello Description is optional and can be up too512 characters.</span></span>

### <a name="tags"></a><span data-ttu-id="3291f-110">標記</span><span class="sxs-lookup"><span data-stu-id="3291f-110">Tags</span></span>
<span data-ttu-id="3291f-111">Tag 可讓您 tooassign 不同的字和片語 toohelp 識別 runbook。</span><span class="sxs-lookup"><span data-stu-id="3291f-111">Tags allow you tooassign distinct words and phrases toohelp identify a runbook.</span></span> <span data-ttu-id="3291f-112">例如，當您提交 runbook toohello [PowerShell 資源庫](https://www.powershellgallery.com/)，您可以指定特定的標籤 tooidentify 所屬的類別目錄 hello runbook 應該會列在。</span><span class="sxs-lookup"><span data-stu-id="3291f-112">For example, when you submit a runbook toohello [PowerShell Gallery](https://www.powershellgallery.com/), you specify particular tags tooidentify which categories hello runbook should be listed in.</span></span> <span data-ttu-id="3291f-113">您可以為 Runbook 指定多個標記，使用逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="3291f-113">You can specify multiple tags for a runbook by separating them with commas.</span></span>

### <a name="logging"></a><span data-ttu-id="3291f-114">記錄</span><span class="sxs-lookup"><span data-stu-id="3291f-114">Logging</span></span>
<span data-ttu-id="3291f-115">根據預設，詳細資訊和進度記錄不會寫入 toojob 歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="3291f-115">By default, Verbose and Progress records are not written toojob history.</span></span> <span data-ttu-id="3291f-116">您可以變更特定 runbook toolog hello 設定這些記錄。</span><span class="sxs-lookup"><span data-stu-id="3291f-116">You can change hello settings for a particular runbook toolog these records.</span></span> <span data-ttu-id="3291f-117">如需有關這些記錄的詳細資訊，請參閱 [Runbook 輸出和訊息](automation-runbook-output-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="3291f-117">For more information on these records, see [Runbook Output and Messages](automation-runbook-output-and-messages.md).</span></span>

## <a name="changing-runbook-settings"></a><span data-ttu-id="3291f-118">變更 Runbook 設定</span><span class="sxs-lookup"><span data-stu-id="3291f-118">Changing runbook settings</span></span>

### <a name="changing-runbook-settings-with-hello-azure-portal"></a><span data-ttu-id="3291f-119">使用 hello Azure 入口網站變更 runbook 設定</span><span class="sxs-lookup"><span data-stu-id="3291f-119">Changing runbook settings with hello Azure portal</span></span>
<span data-ttu-id="3291f-120">您可以變更 hello Azure 入口網站中 runbook 的設定從 hello**設定**hello runbook 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3291f-120">You can change settings for a runbook in hello Azure portal from hello **Settings** blade for hello runbook.</span></span>

1. <span data-ttu-id="3291f-121">在 hello Azure 入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3291f-121">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="3291f-122">選取 hello **Runbook**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3291f-122">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="3291f-123">按一下 runbook 的 hello 名稱，而且您有向的 toohello hello runbook 的設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="3291f-123">Click hello name of a runbook and you are directed toohello settings blade for hello runbook.</span></span> <span data-ttu-id="3291f-124">從這裡，您可以指定或修改標記、 hello runbook 描述、 設定記錄和追蹤設定，並存取支援工具 toohelp 解決問題。</span><span class="sxs-lookup"><span data-stu-id="3291f-124">From here you can specify or modify tags, hello runbook description, configure logging and tracing settings, and access support tools toohelp you solve problems.</span></span>     

### <a name="changing-runbook-settings-with-windows-powershell"></a><span data-ttu-id="3291f-125">使用 Windows PowerShell 變更 Runbook 設定</span><span class="sxs-lookup"><span data-stu-id="3291f-125">Changing runbook settings with Windows PowerShell</span></span>
<span data-ttu-id="3291f-126">您可以使用 hello[組 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello runbook 的設定。</span><span class="sxs-lookup"><span data-stu-id="3291f-126">You can use hello [Set-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello settings for a runbook.</span></span> <span data-ttu-id="3291f-127">如果您想 toospecify 多個標記，您可以提供陣列或單一字串以逗號分隔值 toohello Tags 參數。</span><span class="sxs-lookup"><span data-stu-id="3291f-127">If you want toospecify multiple tags, you can either provide an array or a single string with comma delimited values toohello Tags parameter.</span></span> <span data-ttu-id="3291f-128">您可以取得 hello 目前標記以 hello [Get AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3291f-128">You can get hello current tags with hello [Get-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx).</span></span>

<span data-ttu-id="3291f-129">hello，下列命令範例顯示如何 tooset hello runbook 內容。</span><span class="sxs-lookup"><span data-stu-id="3291f-129">hello following sample commands show how tooset hello properties for a runbook.</span></span> <span data-ttu-id="3291f-130">這個範例會將三個標記 toohello 現有的標記，並指定應記錄詳細記錄。</span><span class="sxs-lookup"><span data-stu-id="3291f-130">This sample adds three tags toohello existing tags and specifies that verbose records should be logged.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a><span data-ttu-id="3291f-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3291f-131">Next steps</span></span>
* <span data-ttu-id="3291f-132">如何 toocreate 並擷取輸出和錯誤訊息從 runbook，請參閱的 toolearn [Runbook 輸出和訊息](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="3291f-132">toolearn how toocreate and retrieve output and error messages from runbooks, see [Runbook Output and Messages](automation-runbook-output-and-messages.md)</span></span> 
* <span data-ttu-id="3291f-133">如何查看 tooadd 已經由開發 hello community 或其他來源或 toocreate 您自己的 runbook 的 runbook toounderstand[建立或匯入 Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="3291f-133">toounderstand how tooadd a runbook that was already developed by hello community or other source, or toocreate your own runbook see [Creating or Importing a Runbook](automation-creating-importing-runbook.md)</span></span> 

