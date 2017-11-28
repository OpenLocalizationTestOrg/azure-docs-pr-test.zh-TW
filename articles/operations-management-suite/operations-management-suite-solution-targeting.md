---
title: "在 OMS 中目標 aaaSolution |Microsoft 文件"
description: "方案的目標是在 Operations Management Suite (OMS)，可讓您 toolimit 管理解決方案 tooa 組特定的代理程式的功能。  本文說明如何 toocreate 領域設定並將它套用 tooa 方案。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a><span data-ttu-id="b30a2-104">使用解決方案目標 Operations Management Suite (OMS) tooscope 管理解決方案 toospecific 代理程式 （預覽）</span><span class="sxs-lookup"><span data-stu-id="b30a2-104">Use solution targeting in Operations Management Suite (OMS) tooscope management solutions toospecific agents (Preview)</span></span>
<span data-ttu-id="b30a2-105">當您加入方案 tooOMS 時，它會自動部署預設 tooall Windows 和 Linux 代理程式連接的 tooyour 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="b30a2-105">When you add a solution tooOMS, it's automatically deployed by default tooall Windows and Linux agents connected tooyour Log Analytics workspace.</span></span>  <span data-ttu-id="b30a2-106">您可能想的 toomanage 您的成本和限制 hello 量的資料收集的解決方案，藉由限制它 tooa 特定的一組代理程式。</span><span class="sxs-lookup"><span data-stu-id="b30a2-106">You may want toomanage your costs and limit hello amount of data collected for a solution by limiting it tooa particular set of agents.</span></span>  <span data-ttu-id="b30a2-107">本文說明如何 toouse**方案目標**這是一項 OMS 功能，可讓您 tooapply 範圍 tooyour 解決方案。</span><span class="sxs-lookup"><span data-stu-id="b30a2-107">This article describes how toouse **Solution Targeting** which is an OMS feature that allows you tooapply a scope tooyour solutions.</span></span>

## <a name="how-tootarget-a-solution"></a><span data-ttu-id="b30a2-108">如何 tootarget 方案</span><span class="sxs-lookup"><span data-stu-id="b30a2-108">How tootarget a solution</span></span>
<span data-ttu-id="b30a2-109">有三個步驟 tootargeting 方案 hello 下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="b30a2-109">There are three steps tootargeting a solution as described in hello following sections.</span></span>  <span data-ttu-id="b30a2-110">請注意，您將需要 hello OMS 入口網站和 hello Azure 入口網站不同的步驟。</span><span class="sxs-lookup"><span data-stu-id="b30a2-110">Note that you will need both hello OMS portal and hello Azure portal for different steps.</span></span>


### <a name="1-create-a-computer-group"></a><span data-ttu-id="b30a2-111">1.建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="b30a2-111">1. Create a computer group</span></span>
<span data-ttu-id="b30a2-112">指定您想 tooinclude 範圍中的，藉由建立 hello 電腦[電腦群組](../log-analytics/log-analytics-computer-groups.md)記錄分析中。</span><span class="sxs-lookup"><span data-stu-id="b30a2-112">You specify hello computers that you want tooinclude in a scope by creating a [computer group](../log-analytics/log-analytics-computer-groups.md) in Log Analytics.</span></span>  <span data-ttu-id="b30a2-113">hello 電腦群組可以根據 記錄搜尋，或從其他來源，例如 Active Directory 或 WSUS 群組匯入。</span><span class="sxs-lookup"><span data-stu-id="b30a2-113">hello computer group can be based on a log search or imported from other sources such as Active Directory or WSUS groups.</span></span> <span data-ttu-id="b30a2-114">做為[下述](#solutions-and-agents-that-cant-be-targeted)，只有電腦直接連線的 tooLog 分析將會包含在 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="b30a2-114">As [described below](#solutions-and-agents-that-cant-be-targeted), only computers that are directly connected tooLog Analytics will be included in hello scope.</span></span>

<span data-ttu-id="b30a2-115">一旦建立工作區中的 hello 電腦群組，然後您將會包含在可以套用的 tooone 或其他解決方案領域設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-115">Once you have hello computer group created in your workspace, then you'll include it in a scope configuration that can be applied tooone or more solutions.</span></span>
 
 
 ### <a name="2-create-a-scope-configuration"></a><span data-ttu-id="b30a2-116">2.建立範圍設定</span><span class="sxs-lookup"><span data-stu-id="b30a2-116">2. Create a scope configuration</span></span>
 <span data-ttu-id="b30a2-117">A**領域設定**包含一或多個電腦群組，而且可以是套用的 tooone 或其他解決方案。</span><span class="sxs-lookup"><span data-stu-id="b30a2-117">A **Scope Configuration** includes one or more computer groups and can be applied tooone or more solutions.</span></span> 
 
 <span data-ttu-id="b30a2-118">建立使用下列程序的 hello 的範圍設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-118">Create a scope configuration using hello following process.</span></span>  

 1. <span data-ttu-id="b30a2-119">在 hello Azure 入口網站中瀏覽過**記錄分析**並選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="b30a2-119">In hello Azure portal, navigate too**Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="b30a2-120">在 hello 工作區下的 hello 屬性**工作區中的資料來源**選取**範圍組態**。</span><span class="sxs-lookup"><span data-stu-id="b30a2-120">In hello properties for hello workspace under **Workspace Data Sources** select **Scope Configurations**.</span></span>
 3. <span data-ttu-id="b30a2-121">按一下**新增**toocreate 新的領域設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-121">Click **Add** toocreate a new scope configuration.</span></span>
 4. <span data-ttu-id="b30a2-122">輸入**名稱**hello 範圍設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-122">Type a **Name** for hello scope configuration.</span></span>
 5. <span data-ttu-id="b30a2-123">按一下 [選取電腦群組]。</span><span class="sxs-lookup"><span data-stu-id="b30a2-123">Click **Select Computer Groups**.</span></span>
 6. <span data-ttu-id="b30a2-124">選取您所建立的 hello 電腦群組和 （選擇性） 任何其他群組 tooadd toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="b30a2-124">Select hello computer group that you created and optionally any other groups tooadd toohello configuration.</span></span>  <span data-ttu-id="b30a2-125">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="b30a2-125">Click **Select**.</span></span>  
 6. <span data-ttu-id="b30a2-126">按一下**確定**toocreate hello 領域設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-126">Click **OK** toocreate hello scope configuration.</span></span> 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a><span data-ttu-id="b30a2-127">3.適用於 hello 範圍組態 tooa 方案。</span><span class="sxs-lookup"><span data-stu-id="b30a2-127">3. Apply hello scope configuration tooa solution.</span></span>
<span data-ttu-id="b30a2-128">一旦領域設定，然後您可以將它套用 tooone 或其他解決方案。</span><span class="sxs-lookup"><span data-stu-id="b30a2-128">Once you have a scope configuration, then you can apply it tooone or more solutions.</span></span>  <span data-ttu-id="b30a2-129">請注意，雖然單一範圍設定可以搭配多個解決方案使用，但每個解決方案僅可以使用一個範圍設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-129">Note that while a single scope configuration can be used with multiple solutions, each solution can only use one scope configuration.</span></span>

<span data-ttu-id="b30a2-130">適用於使用下列程序的 hello 領域設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-130">Apply a scope configuration using hello following process.</span></span>  

 1. <span data-ttu-id="b30a2-131">在 hello Azure 入口網站中瀏覽過**記錄分析**並選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="b30a2-131">In hello Azure portal, navigate too**Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="b30a2-132">在 [hello] 工作區的 hello 內容選取**解決方案**。</span><span class="sxs-lookup"><span data-stu-id="b30a2-132">In hello properties for hello workspace select **Solutions**.</span></span>
 3. <span data-ttu-id="b30a2-133">按一下您想 tooscope hello 方案。</span><span class="sxs-lookup"><span data-stu-id="b30a2-133">Click on hello solution you want tooscope.</span></span>
 4. <span data-ttu-id="b30a2-134">Hello 下 hello 方案內容中**工作區中的資料來源**選取**方案目標**。</span><span class="sxs-lookup"><span data-stu-id="b30a2-134">In hello properties for hello solution under **Workspace Data Sources** select **Solution Targeting**.</span></span>  <span data-ttu-id="b30a2-135">如果不使用 hello 選項然後[無法針對此解決方案](#solutions-and-agents-that-cant-be-targeted)。</span><span class="sxs-lookup"><span data-stu-id="b30a2-135">If hello option is not available then [this solution cannot be targeted](#solutions-and-agents-that-cant-be-targeted).</span></span>
 5. <span data-ttu-id="b30a2-136">按一下 [新增範圍設定]。</span><span class="sxs-lookup"><span data-stu-id="b30a2-136">Click **Add scope configuration**.</span></span>  <span data-ttu-id="b30a2-137">如果您已經擁有組態套用 toothis 解決方案此選項將無法使用。</span><span class="sxs-lookup"><span data-stu-id="b30a2-137">If you already have a configuration applied toothis solution then this option will be unavailable.</span></span>  <span data-ttu-id="b30a2-138">您必須移除 hello 現有組態，然後再加入另一個。</span><span class="sxs-lookup"><span data-stu-id="b30a2-138">You must remove hello existing configuration before adding another one.</span></span>
 6. <span data-ttu-id="b30a2-139">按一下您所建立的 hello 領域設定。</span><span class="sxs-lookup"><span data-stu-id="b30a2-139">Click on hello scope configuration that you created.</span></span>
 7. <span data-ttu-id="b30a2-140">監看式 hello**狀態**的它會顯示 hello 組態 tooensure **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="b30a2-140">Watch hello **Status** of hello configuration tooensure that it shows **Succeeded**.</span></span>  <span data-ttu-id="b30a2-141">如果 hello 狀態表示錯誤，然後按一下 hello 橢圓形 toohello 右邊的 hello 設定，並選取**編輯領域設定**toomake 變更。</span><span class="sxs-lookup"><span data-stu-id="b30a2-141">If hello status indicates an error, then click hello ellipse toohello right of hello configuration and select **Edit scope configuration** toomake changes.</span></span>

## <a name="solutions-and-agents-that-cant-be-targeted"></a><span data-ttu-id="b30a2-142">無法設定目標的解決方案和代理程式</span><span class="sxs-lookup"><span data-stu-id="b30a2-142">Solutions and agents that can't be targeted</span></span>
<span data-ttu-id="b30a2-143">以下是代理程式和解決方案，不能與目標方案的 hello 準則。</span><span class="sxs-lookup"><span data-stu-id="b30a2-143">Following are hello criteria for agents and solutions that can't be used with solution targeting.</span></span>

- <span data-ttu-id="b30a2-144">方案為目標時，只適用於部署 tooagents toosolutions。</span><span class="sxs-lookup"><span data-stu-id="b30a2-144">Solution targeting only applies toosolutions that deploy tooagents.</span></span>
- <span data-ttu-id="b30a2-145">目標方案僅適用於由 Microsoft 提供的 toosolutions。</span><span class="sxs-lookup"><span data-stu-id="b30a2-145">Solution targeting only applies toosolutions provided by Microsoft.</span></span>  <span data-ttu-id="b30a2-146">它不會套用 toosolutions[自己或其他協力廠商所建立](operations-management-suite-solutions-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="b30a2-146">It does not apply toosolutions [created by yourself or partners](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="b30a2-147">您可以只會篩選掉 tooLog 分析直接連接的代理程式。</span><span class="sxs-lookup"><span data-stu-id="b30a2-147">You can only filter out agents that connect directly tooLog Analytics.</span></span>  <span data-ttu-id="b30a2-148">解決方案會自動將部署 tooany 代理程式已連線的 Operations Manager 管理群組，它們包含在範圍組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="b30a2-148">Solutions will automatically deploy tooany agents that are part of a connected Operations Manager management group whether or not they're included in a scope configuration.</span></span>

### <a name="exceptions"></a><span data-ttu-id="b30a2-149">例外狀況</span><span class="sxs-lookup"><span data-stu-id="b30a2-149">Exceptions</span></span>
<span data-ttu-id="b30a2-150">方案的目標不能與 hello 下列方案，即使它們符合 hello 所述的準則。</span><span class="sxs-lookup"><span data-stu-id="b30a2-150">Solution targeting cannot be used with hello following solutions even though they fit hello stated criteria.</span></span>

- <span data-ttu-id="b30a2-151">代理程式健康狀態評估</span><span class="sxs-lookup"><span data-stu-id="b30a2-151">Agent Health Assessment</span></span>

## <a name="next-steps"></a><span data-ttu-id="b30a2-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b30a2-152">Next steps</span></span>
- <span data-ttu-id="b30a2-153">深入了解管理方案包括 hello 方案會在您環境中的可用 tooinstall[新增 Azure Log Analytics management 解決方案 tooyour 工作區](../log-analytics/log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="b30a2-153">Learn more about management solutions including hello solutions that are available tooinstall in your environment at [Add Azure Log Analytics management solutions tooyour workspace](../log-analytics/log-analytics-add-solutions.md).</span></span>
- <span data-ttu-id="b30a2-154">在 [Log Analytics 記錄檔搜尋中的電腦群組](../log-analytics/log-analytics-computer-groups.md)中深入了解建立電腦群組。</span><span class="sxs-lookup"><span data-stu-id="b30a2-154">Learn more about creating computer groups at [Computer groups in Log Analytics log searches](../log-analytics/log-analytics-computer-groups.md).</span></span>