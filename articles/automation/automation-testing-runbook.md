---
title: "在 Azure 自動化中測試 Runbook | Microsoft Docs"
description: "在 Azure 自動化中發佈 Runbook 之前，您可以先加以測試，以確保 Runbook 能夠如預期般運作。  本文說明如何測試 Runbook 及檢視其輸出。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 5186eb8f1732d533cbceb397b4d8b5224ad773cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a><span data-ttu-id="114d3-104">在 Azure 自動化中測試 Runbook</span><span class="sxs-lookup"><span data-stu-id="114d3-104">Testing a runbook in Azure Automation</span></span>
<span data-ttu-id="114d3-105">當您測試 Runbook 時， [草稿版本](automation-creating-importing-runbook.md#publishing-a-runbook) 會執行，而且它執行的任何動作都會完成。</span><span class="sxs-lookup"><span data-stu-id="114d3-105">When you test a runbook, the [Draft version](automation-creating-importing-runbook.md#publishing-a-runbook) is executed and any actions that it performs are completed.</span></span> <span data-ttu-id="114d3-106">不會建立任何工作歷程記錄，但 [測試輸出] 窗格中會顯示[輸出](automation-runbook-output-and-messages.md#output-stream)與[警告和錯誤](automation-runbook-output-and-messages.md#message-streams)串流。</span><span class="sxs-lookup"><span data-stu-id="114d3-106">No job history is created, but the [Output](automation-runbook-output-and-messages.md#output-stream) and [Warning and Error](automation-runbook-output-and-messages.md#message-streams) streams are displayed in the Test output Pane.</span></span> <span data-ttu-id="114d3-107">只有將 [$VerbosePreference 變數](automation-runbook-output-and-messages.md#preference-variables)設為 Continue，傳送給[詳細資訊串流](automation-runbook-output-and-messages.md#message-streams)的訊息才會顯示在 [輸出] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="114d3-107">Messages to the [Verbose Stream](automation-runbook-output-and-messages.md#message-streams) are displayed in the Output Pane only if the [$VerbosePreference variable](automation-runbook-output-and-messages.md#preference-variables) is set to Continue.</span></span>

<span data-ttu-id="114d3-108">即使執行的是草稿版本，Runbook 仍會正常執行工作流程，並會針對環境中的資源執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="114d3-108">Even though the draft version is being run, the runbook still executes the workflow normally and performs any actions against resources in the environment.</span></span> <span data-ttu-id="114d3-109">因此，您只能在非生產資源中測試 Runbook。</span><span class="sxs-lookup"><span data-stu-id="114d3-109">For this reason, you should only test runbooks at non-production resources.</span></span>

<span data-ttu-id="114d3-110">測試每個 [Runbook 類型](automation-runbook-types.md) 的程序都相同，而且無論是在文字式編輯器或 Azure 入口網站的圖形化編輯器中進行測試，都沒有任何差別。</span><span class="sxs-lookup"><span data-stu-id="114d3-110">The procedure to test each [type of runbook](automation-runbook-types.md) is the same, and there is no difference in testing between the textual editor and the graphical editor in the Azure portal.</span></span>  

## <a name="to-test-a-runbook-in-the-azure-portal"></a><span data-ttu-id="114d3-111">在 Azure 入口網站中測試 Runbook</span><span class="sxs-lookup"><span data-stu-id="114d3-111">To test a runbook in the Azure portal</span></span>
<span data-ttu-id="114d3-112">您可以在 Azure 入口網站中使用任何 [Runbook 類型](automation-runbook-types.md) 。</span><span class="sxs-lookup"><span data-stu-id="114d3-112">You can work with any [runbook type](automation-runbook-types.md) in the Azure portal.</span></span>

1. <span data-ttu-id="114d3-113">您可以在[文字編輯器](automation-edit-textual-runbook.md)或[圖形化編輯器](automation-graphical-authoring-intro.md)中開啟 Runbook 的草稿版本。</span><span class="sxs-lookup"><span data-stu-id="114d3-113">Open the Draft version of the runbook in either the [textual editor](automation-edit-textual-runbook.md) or [graphical editor](automation-graphical-authoring-intro.md).</span></span>
2. <span data-ttu-id="114d3-114">按一下  [測試] 按鈕以開啟 [測試] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="114d3-114">Click the **Test** button to open the Test blade.</span></span>
3. <span data-ttu-id="114d3-115">如果 Runbook 含有參數，這些參數會列在左窗格中，您可以在此提供值，以供測試使用。</span><span class="sxs-lookup"><span data-stu-id="114d3-115">If the runbook has parameters, they will be listed in the left pane where you can provide values to be used for the test.</span></span>
4. <span data-ttu-id="114d3-116">如果您想要在[混合式 Runbook 背景工作](automation-hybrid-runbook-worker.md)上執行測試，則需將 [執行設定] 變更為 [混合式背景工作]，然後選取目標群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="114d3-116">If you want to run the test on a [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md), then change **Run Settings** to **Hybrid Worker** and select the name of the target group.</span></span>  <span data-ttu-id="114d3-117">否則，請保留預設值 **Azure**，以便在雲端中執行測試。</span><span class="sxs-lookup"><span data-stu-id="114d3-117">Otherwise, keep the default **Azure** to run the test in the cloud.</span></span>
5. <span data-ttu-id="114d3-118">按一下 [啟動]  按鈕以啟動測試。</span><span class="sxs-lookup"><span data-stu-id="114d3-118">Click the **Start** button to start the test.</span></span>
6. <span data-ttu-id="114d3-119">如果 Runbook 是 [PowerShell 工作流程](automation-runbook-types.md#powershell-workflow-runbooks)或[圖形化](automation-runbook-types.md#graphical-runbooks) Runbook，則在測試過程中，您可以使用 [輸出] 窗格下方的按鈕來停止或暫停 Runbook。</span><span class="sxs-lookup"><span data-stu-id="114d3-119">If the runbook is [PowerShell Workflow](automation-runbook-types.md#powershell-workflow-runbooks) or [Graphical](automation-runbook-types.md#graphical-runbooks), then you can stop or suspend it while it is being tested with the buttons underneath the Output Pane.</span></span> <span data-ttu-id="114d3-120">暫停 Runbook 時，它會先完成目前的活動後才暫停。</span><span class="sxs-lookup"><span data-stu-id="114d3-120">When you suspend the runbook, it completes the current activity before being suspended.</span></span> <span data-ttu-id="114d3-121">Runbook 一旦暫停，您可以選擇停止或重新啟動。</span><span class="sxs-lookup"><span data-stu-id="114d3-121">Once the runbook is suspended, you can stop it or restart it.</span></span>
7. <span data-ttu-id="114d3-122">您可以在 [輸出] 窗格中檢查 Runbook 的輸出。</span><span class="sxs-lookup"><span data-stu-id="114d3-122">Inspect the output from the runbook in the output pane.</span></span>

## <a name="next-steps"></a><span data-ttu-id="114d3-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="114d3-123">Next Steps</span></span>
* <span data-ttu-id="114d3-124">若要了解如何建立或匯入 Runbook，請參閱 [建立或匯入 Azure 自動化中的 Runbook](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="114d3-124">To learn how to create or import a runbook, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>
* <span data-ttu-id="114d3-125">若要深入了解圖形化編寫，請參閱 [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)</span><span class="sxs-lookup"><span data-stu-id="114d3-125">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md)</span></span>
* <span data-ttu-id="114d3-126">若要開始使用 PowerShell 工作流程 Runbook，請參閱 [我的第一個 PowerShell 工作流程 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="114d3-126">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="114d3-127">若要深入了解設定 Runbok 以傳回狀態訊息和錯誤，包括建議的作法，請參閱 [Azure 自動化中的 Runbook 輸出和訊息](automation-runbook-output-and-messages.md)</span><span class="sxs-lookup"><span data-stu-id="114d3-127">To learn more about configuring runboks to return status messages and errors, including recommended practices, see [Runbook output and messages in Azure Automation](automation-runbook-output-and-messages.md)</span></span>

