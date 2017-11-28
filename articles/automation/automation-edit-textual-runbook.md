---
title: "Azure 自動化中的 aaaEditing 文字 runbook"
description: "本文提供不同的程序使用 PowerShell 和 PowerShell 工作流程在 Azure 自動化中 runbook 使用 hello 文字編輯器。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a><span data-ttu-id="e4bd2-103">在 Azure 自動化中編輯文字式 Runbook</span><span class="sxs-lookup"><span data-stu-id="e4bd2-103">Editing textual runbooks in Azure Automation</span></span>
<span data-ttu-id="e4bd2-104">hello Azure 自動化中的文字編輯器可使用的 tooedit [PowerShell runbook](automation-runbook-types.md#powershell-runbooks)和[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-104">hello textual editor in Azure Automation can be used tooedit [PowerShell runbooks](automation-runbook-types.md#powershell-runbooks) and [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks).</span></span> <span data-ttu-id="e4bd2-105">這會有 hello 的 intellisense 和色彩編碼與額外的特殊功能 tooassist 您在存取資源的一般 toorunbooks 等其他程式碼編輯器的一般功能。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-105">This has hello typical features of other code editors such as intellisense and color coding  with additional special features tooassist you in accessing resources common toorunbooks.</span></span>  <span data-ttu-id="e4bd2-106">本文提供執行與此編輯器不同的功能的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-106">This article provides detailed steps for performing different functions with this editor.</span></span>

<span data-ttu-id="e4bd2-107">hello 文字編輯器包含至 runbook 的活動、 資產和子系 runbook 的功能 tooinsert 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-107">hello textual editor includes a feature tooinsert code for activities, assets, and child runbooks into a runbook.</span></span> <span data-ttu-id="e4bd2-108">而不是輸入 hello 程式碼本身，您可以從可用資源的清單中選取，然後利用 hello 適當的程式碼插入 hello 的 runbook。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-108">Rather than typing in hello code yourself, you can select from a list of available resources and have hello appropriate code inserted into hello runbook.</span></span>

<span data-ttu-id="e4bd2-109">Azure 自動化中的每個 Runbook 有兩個版本，「草稿」和「已發佈」。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-109">Each runbook in Azure Automation has two versions, Draft and Published.</span></span> <span data-ttu-id="e4bd2-110">編輯 hello hello runbook 草稿版本，並執行它，按一下此處。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-110">You edit hello Draft version of hello runbook and then publish it so it can be executed.</span></span> <span data-ttu-id="e4bd2-111">無法編輯 hello 已發佈版本。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-111">hello Published version cannot be edited.</span></span> <span data-ttu-id="e4bd2-112">如需詳細資訊，請參閱 [發佈 Runbook](automation-creating-importing-runbook.md#publishing-a-runbook) 。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-112">See [Publishing a runbook](automation-creating-importing-runbook.md#publishing-a-runbook) for more information.</span></span>

<span data-ttu-id="e4bd2-113">與 toowork[圖形化 Runbook](automation-runbook-types.md#graphical-runbooks)，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-113">toowork with [Graphical Runbooks](automation-runbook-types.md#graphical-runbooks), see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="e4bd2-114">tooedit runbook 以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e4bd2-114">tooedit a runbook with hello Azure portal</span></span>
<span data-ttu-id="e4bd2-115">使用下列程序 tooopen runbook 進行編輯 hello 文字編輯器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-115">Use hello following procedure tooopen a runbook for editing in hello textual editor.</span></span>

1. <span data-ttu-id="e4bd2-116">在 hello Azure 入口網站，選取您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-116">In hello Azure portal, select your automation account.</span></span>
2. <span data-ttu-id="e4bd2-117">按一下 hello **Runbook**磚 tooopen hello runbook 的清單。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-117">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="e4bd2-118">按一下 hello 名稱 hello runbook 的方法，您可以想 tooedit，，然後按一下hello**編輯** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-118">Click hello name of hello runbook you want tooedit and then click hello **Edit** button.</span></span>
4. <span data-ttu-id="e4bd2-119">執行所需編輯 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-119">Perform hello required editing.</span></span>
5. <span data-ttu-id="e4bd2-120">當您完成編輯時，按一下 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-120">Click **Save** when your edits are complete.</span></span>
6. <span data-ttu-id="e4bd2-121">按一下**發行**如果您想發行的 hello runbook toobe 的 hello 最新草稿版本。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-121">Click **Publish** if you want hello latest draft version of hello runbook toobe published.</span></span>

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a><span data-ttu-id="e4bd2-122">tooinsert cmdlet 至 runbook</span><span class="sxs-lookup"><span data-stu-id="e4bd2-122">tooinsert a cmdlet into a runbook</span></span>
1. <span data-ttu-id="e4bd2-123">Hello 游標 hello 畫布的 hello 文字編輯器，在您在要 tooplace hello 指令程式的位置。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-123">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello cmdlet.</span></span>
2. <span data-ttu-id="e4bd2-124">展開 hello **Cmdlet** hello 控制項程式庫中的節點。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-124">Expand hello **Cmdlets** node in hello Library control.</span></span>
3. <span data-ttu-id="e4bd2-125">展開包含您想要 toouse hello cmdlet hello 模組。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-125">Expand hello module containing hello cmdlet you want toouse.</span></span>
4. <span data-ttu-id="e4bd2-126">以滑鼠右鍵按一下 hello cmdlet tooinsert，然後選取**新增 toocanvas**。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-126">Right click hello cmdlet tooinsert and select **Add toocanvas**.</span></span>  <span data-ttu-id="e4bd2-127">如果 hello cmdlet 有一個以上的參數集，將會加入 hello 預設集。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-127">If hello cmdlet has more than one parameter set, then hello default set will be added.</span></span>  <span data-ttu-id="e4bd2-128">您也可以展開 hello cmdlet tooselect 不同的參數設定。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-128">You can also expand hello cmdlet tooselect a different parameter set.</span></span>
5. <span data-ttu-id="e4bd2-129">hello hello 指令程式的程式碼會插入與它的參數的完整清單。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-129">hello code for hello cmdlet is inserted with its entire list of parameters.</span></span>
6. <span data-ttu-id="e4bd2-130">提供適當的值取代以大括號 <> 的任何必要參數的 hello 資料型別。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-130">Provide an appropriate value in place of hello data type surrounded by braces <> for any required parameters.</span></span>  <span data-ttu-id="e4bd2-131">移除您不需要的任何參數。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-131">Remove any parameters you don't need.</span></span>

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a><span data-ttu-id="e4bd2-132">tooinsert 至 runbook 的子 runbook 的程式碼</span><span class="sxs-lookup"><span data-stu-id="e4bd2-132">tooinsert code for a child runbook into a runbook</span></span>
1. <span data-ttu-id="e4bd2-133">Hello 畫布的 hello 文字編輯器，在 hello 游標位置所在的程式碼 tooplace hello hello[子系 runbook](automation-child-runbooks.md)。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-133">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello code for hello [child runbook](automation-child-runbooks.md).</span></span>
2. <span data-ttu-id="e4bd2-134">展開 hello **Runbook** hello 控制項程式庫中的節點。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-134">Expand hello **Runbooks** node in hello Library control.</span></span>
3. <span data-ttu-id="e4bd2-135">以滑鼠右鍵按一下 hello runbook tooinsert，然後選取**新增 toocanvas**。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-135">Right click hello runbook tooinsert and select **Add toocanvas**.</span></span>
4. <span data-ttu-id="e4bd2-136">hello hello 子 runbook 的程式碼會插入其中任何含有任何 runbook 參數的預留位置。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-136">hello code for hello child runbook is inserted with any placeholders for any runbook parameters.</span></span>
5. <span data-ttu-id="e4bd2-137">Hello 預留位置取代為適當的每個參數的值。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-137">Replace hello placeholders with appropriate values for each parameter.</span></span>

### <a name="tooinsert-an-asset-into-a-runbook"></a><span data-ttu-id="e4bd2-138">tooinsert 資產至 runbook</span><span class="sxs-lookup"><span data-stu-id="e4bd2-138">tooinsert an asset into a runbook</span></span>
1. <span data-ttu-id="e4bd2-139">Hello 資料指標在 hello 畫布的 hello 文字編輯器，在您要 tooplace hello 程式碼 hello 子 runbook 的位置。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-139">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello code for hello child runbook.</span></span>
2. <span data-ttu-id="e4bd2-140">展開 hello**資產**hello 控制項程式庫中的節點。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-140">Expand hello **Assets** node in hello Library control.</span></span>
3. <span data-ttu-id="e4bd2-141">展開您想要的資產的 hello 類型 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-141">Expand hello node for hello type of asset you want.</span></span>
4. <span data-ttu-id="e4bd2-142">以滑鼠右鍵按一下 hello 資產 tooinsert，然後選取**新增 toocanvas**。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-142">Right click hello asset tooinsert and select **Add toocanvas**.</span></span>  <span data-ttu-id="e4bd2-143">如[變數資產](automation-variables.md)，選取 **新增 「 取得變數 」 toocanvas**或**新增 「 設定變數 」 toocanvas**根據您想 tooget 還是設定 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-143">For [variable assets](automation-variables.md), select either **Add "Get Variable" toocanvas** or **Add "Set Variable" toocanvas** depending on whether you want tooget or set hello variable.</span></span>
5. <span data-ttu-id="e4bd2-144">hello hello 資產的程式碼會插入至 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-144">hello code for hello asset is inserted into hello runbook.</span></span>

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a><span data-ttu-id="e4bd2-145">tooedit runbook 以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e4bd2-145">tooedit a runbook with hello Azure portal</span></span>
<span data-ttu-id="e4bd2-146">使用下列程序 tooopen runbook 進行編輯 hello 文字編輯器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-146">Use hello following procedure tooopen a runbook for editing in hello textual editor.</span></span>

1. <span data-ttu-id="e4bd2-147">在 hello Azure 入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-147">In hello Azure portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="e4bd2-148">選取 hello **Runbook**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-148">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="e4bd2-149">按一下 hello 名稱 hello runbook 的方法，您可以想 tooedit，，然後選取 [hello**作者**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-149">Click hello name of hello runbook you want tooedit and then select hello **Author** tab.</span></span>
4. <span data-ttu-id="e4bd2-150">按一下 hello**編輯**在 hello 囉 」 畫面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-150">Click hello **Edit** button at hello bottom of hello screen.</span></span>
5. <span data-ttu-id="e4bd2-151">執行所需編輯 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-151">Perform hello required editing.</span></span>
6. <span data-ttu-id="e4bd2-152">當您完成編輯時，按一下 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-152">Click **Save** when your edits are complete.</span></span>
7. <span data-ttu-id="e4bd2-153">按一下**發行**如果您想發行的 hello runbook toobe 的 hello 最新草稿版本。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-153">Click **Publish** if you want hello latest draft version of hello runbook toobe published.</span></span>

### <a name="tooinsert-an-activity-into-a-runbook"></a><span data-ttu-id="e4bd2-154">tooinsert 至 Runbook 活動</span><span class="sxs-lookup"><span data-stu-id="e4bd2-154">tooinsert an activity into a Runbook</span></span>
1. <span data-ttu-id="e4bd2-155">Hello 資料指標在 hello 畫布的 hello 文字編輯器，在您要 tooplace hello 活動的位置。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-155">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello activity.</span></span>
2. <span data-ttu-id="e4bd2-156">在 hello 囉 」 畫面底部，按一下 **插入**然後**活動**。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-156">At hello bottom of hello screen, click **Insert** and then **Activity**.</span></span>
3. <span data-ttu-id="e4bd2-157">在 hello**整合模組**資料行中，選取 hello 模組包含 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-157">In hello **Integration Module** column, select hello module that contains hello activity.</span></span>
4. <span data-ttu-id="e4bd2-158">在 [hello**活動**] 窗格中，選取一個活動。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-158">In hello **Activity** pane, select an activity.</span></span>
5. <span data-ttu-id="e4bd2-159">在 hello**描述**資料行中，注意 hello hello 活動描述。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-159">In hello **Description** column, note hello description of hello activity.</span></span> <span data-ttu-id="e4bd2-160">或者，您可以按一下 檢視詳細的說明 toolaunch hello hello 瀏覽器中的活動。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-160">Optionally, you can click View detailed help toolaunch help for hello activity in hello browser.</span></span>
6. <span data-ttu-id="e4bd2-161">按一下向右箭號 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-161">Click hello right arrow.</span></span>  <span data-ttu-id="e4bd2-162">如果 hello 活動有參數，它們會列出供您的資訊。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-162">If hello activity has parameters, they will be listed for your information.</span></span>
7. <span data-ttu-id="e4bd2-163">按一下 hello 核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-163">Click hello check button.</span></span>  <span data-ttu-id="e4bd2-164">程式碼 toorun hello 活動會將插入 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-164">Code toorun hello activity will be inserted into hello runbook.</span></span>
8. <span data-ttu-id="e4bd2-165">如果 hello 活動需要參數，提供適當的值取代以大括號 <> hello 資料型別。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-165">If hello activity requires parameters, provide an appropriate value in place of hello data type surrounded by braces <>.</span></span>

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a><span data-ttu-id="e4bd2-166">tooinsert 至 runbook 的子 runbook 的程式碼</span><span class="sxs-lookup"><span data-stu-id="e4bd2-166">tooinsert code for a child runbook into a runbook</span></span>
1. <span data-ttu-id="e4bd2-167">Hello 畫布的 hello 文字編輯器，在游標的位置 hello 想 tooplace hello[子系 runbook](automation-child-runbooks.md)。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-167">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello [child runbook](automation-child-runbooks.md).</span></span>
2. <span data-ttu-id="e4bd2-168">在 hello 囉 」 畫面底部，按一下 **插入**然後**Runbook**。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-168">At hello bottom of hello screen, click **Insert** and then **Runbook**.</span></span>
3. <span data-ttu-id="e4bd2-169">選取 hello runbook tooinsert 從 hello 中心資料行，然後按一下向右箭號 hello。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-169">Select hello runbook tooinsert from hello center column and click hello right arrow.</span></span>
4. <span data-ttu-id="e4bd2-170">如果 hello runbook 有參數，它們會列出供您的資訊。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-170">If hello runbook has parameters, they will be listed for your information.</span></span>
5. <span data-ttu-id="e4bd2-171">按一下 hello 核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-171">Click hello check button.</span></span>  <span data-ttu-id="e4bd2-172">程式碼 toorun hello 選取 runbook 會將插入 hello 目前的 runbook。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-172">Code toorun hello selected runbook will be inserted into hello current runbook.</span></span>
6. <span data-ttu-id="e4bd2-173">如果 hello runbook 需要參數，提供適當的值取代以大括號 <> hello 資料型別。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-173">If hello runbook requires parameters, provide an appropriate value in place of hello data type surrounded by braces <>.</span></span>

### <a name="tooinsert-an-asset-into-a-runbook"></a><span data-ttu-id="e4bd2-174">tooinsert 資產至 runbook</span><span class="sxs-lookup"><span data-stu-id="e4bd2-174">tooinsert an asset into a runbook</span></span>
1. <span data-ttu-id="e4bd2-175">Hello 游標 hello 畫布的 hello 文字編輯器，在您想 tooplace hello 活動 tooretrieve hello 資產所在的位置。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-175">In hello Canvas of hello textual editor, position hello cursor where you want tooplace hello activity tooretrieve hello asset.</span></span>
2. <span data-ttu-id="e4bd2-176">在 hello 囉 」 畫面底部，按一下 **插入**然後**設定**。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-176">At hello bottom of hello screen, click **Insert** and then **Setting**.</span></span>
3. <span data-ttu-id="e4bd2-177">在 hello**設定動作**資料行中，選取 hello 您想要的動作。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-177">In hello **Setting Action** column, select hello action that you want.</span></span>
4. <span data-ttu-id="e4bd2-178">選取從 hello hello 中心資料行中的可用資產。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-178">Select from hello available assets in hello center column.</span></span>
5. <span data-ttu-id="e4bd2-179">按一下 hello 核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-179">Click hello check button.</span></span>  <span data-ttu-id="e4bd2-180">程式碼 tooget 或組 hello 資產會將插入 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-180">Code tooget or set hello asset will be inserted into hello runbook.</span></span>

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a><span data-ttu-id="e4bd2-181">tooedit 使用 Windows PowerShell 的 Azure 自動化 runbook</span><span class="sxs-lookup"><span data-stu-id="e4bd2-181">tooedit an Azure Automation runbook using Windows PowerShell</span></span>
<span data-ttu-id="e4bd2-182">tooedit runbook 讓您使用 Windows PowerShell，使用您選擇的 hello 編輯器並儲存 tooa.ps1 檔案。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-182">tooedit a runbook with Windows PowerShell, you use hello editor of your choice and save it tooa .ps1 file.</span></span> <span data-ttu-id="e4bd2-183">您可以使用 hello [Get-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) hello runbook cmdlet tooretrieve hello 內容，然後[Set-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello 現有草稿 runbook 以 hello 修改其中一個。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-183">You can use hello [Get-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) cmdlet tooretrieve hello contents of hello runbook and then [Set-AzureAutomationRunbookDefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello existing draft runbook with hello modified one.</span></span>

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a><span data-ttu-id="e4bd2-184">tooRetrieve hello Runbook Using Windows PowerShell 的內容</span><span class="sxs-lookup"><span data-stu-id="e4bd2-184">tooRetrieve hello Contents of a Runbook Using Windows PowerShell</span></span>
<span data-ttu-id="e4bd2-185">hello，下列命令範例顯示如何 tooretrieve hello runbook 指令碼，並將它儲存 tooa 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-185">hello following sample commands show how tooretrieve hello script for a runbook and save it tooa script file.</span></span> <span data-ttu-id="e4bd2-186">在此範例中，會擷取 hello 草稿版本。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-186">In this example, hello Draft version is retrieved.</span></span> <span data-ttu-id="e4bd2-187">它也是可能 tooretrieve hello 已發佈版本 hello runbook 但無法變更此版本。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-187">It is also possible tooretrieve hello Published version of hello runbook although this version cannot be changed.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a><span data-ttu-id="e4bd2-188">tooChange hello Runbook Using Windows PowerShell 的內容</span><span class="sxs-lookup"><span data-stu-id="e4bd2-188">tooChange hello Contents of a Runbook Using Windows PowerShell</span></span>
<span data-ttu-id="e4bd2-189">hello 下列命令範例示範如何 tooreplace hello hello 的指令碼檔案的內容與現有的 runbook 內容。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-189">hello following sample commands show how tooreplace hello existing contents of a runbook with hello contents of a script file.</span></span> <span data-ttu-id="e4bd2-190">請注意，這是 hello 相同範例中的程序[tooimport 從使用 Windows PowerShell 指令碼檔案 runbook](automation-creating-importing-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="e4bd2-190">Note that this is hello same sample procedure as in [tooimport a runbook from a script file with Windows PowerShell](automation-creating-importing-runbook.md).</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a><span data-ttu-id="e4bd2-191">相關文章</span><span class="sxs-lookup"><span data-stu-id="e4bd2-191">Related articles</span></span>
* [<span data-ttu-id="e4bd2-192">在 Azure 自動化中建立或匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="e4bd2-192">Creating or importing a runbook in Azure Automation</span></span>](automation-creating-importing-runbook.md)
* [<span data-ttu-id="e4bd2-193">了解 PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="e4bd2-193">Learning PowerShell workflow</span></span>](automation-powershell-workflow.md)
* [<span data-ttu-id="e4bd2-194">Azure 自動化中的圖形化編寫</span><span class="sxs-lookup"><span data-stu-id="e4bd2-194">Graphical authoring in Azure Automation</span></span>](automation-graphical-authoring-intro.md)
* [<span data-ttu-id="e4bd2-195">憑證</span><span class="sxs-lookup"><span data-stu-id="e4bd2-195">Certificates</span></span>](automation-certificates.md)
* [<span data-ttu-id="e4bd2-196">連線</span><span class="sxs-lookup"><span data-stu-id="e4bd2-196">Connections</span></span>](automation-connections.md)
* [<span data-ttu-id="e4bd2-197">認證</span><span class="sxs-lookup"><span data-stu-id="e4bd2-197">Credentials</span></span>](automation-credentials.md)
* [<span data-ttu-id="e4bd2-198">排程</span><span class="sxs-lookup"><span data-stu-id="e4bd2-198">Schedules</span></span>](automation-schedules.md)
* [<span data-ttu-id="e4bd2-199">變數</span><span class="sxs-lookup"><span data-stu-id="e4bd2-199">Variables</span></span>](automation-variables.md)
