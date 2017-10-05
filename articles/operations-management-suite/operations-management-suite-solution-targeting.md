---
title: "OMS 中的設定解決方案目標 | Microsoft Docs"
description: "「設定解決方案目標」是 Operations Management Suite (OMS) 中的功能，可讓您限制管理解決方案以針對一組特定的代理程式。  本文說明如何建立範圍設定，並將它套用至解決方案。"
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
ms.openlocfilehash: cb73a2d7ae57a5a11869259dbe913ae83ffb2b01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-to-scope-management-solutions-to-specific-agents-preview"></a><span data-ttu-id="57d6a-104">使用 Operations Management Suite (OMS) 中的「設定解決方案目標」將管理解決方案的範圍設定為特定的代理程式 (預覽)</span><span class="sxs-lookup"><span data-stu-id="57d6a-104">Use solution targeting in Operations Management Suite (OMS) to scope management solutions to specific agents (Preview)</span></span>
<span data-ttu-id="57d6a-105">當您將解決方案加入 OMS 時，它預設會自動部署到與您 Log Analytics 工作區連線的所有 Windows 與 Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="57d6a-105">When you add a solution to OMS, it's automatically deployed by default to all Windows and Linux agents connected to your Log Analytics workspace.</span></span>  <span data-ttu-id="57d6a-106">您可能會想要管理您的成本，並透過將解決方案限制在一組特定的代理程式，來限制針對該解決方案所收集的資料量。</span><span class="sxs-lookup"><span data-stu-id="57d6a-106">You may want to manage your costs and limit the amount of data collected for a solution by limiting it to a particular set of agents.</span></span>  <span data-ttu-id="57d6a-107">本文說明如何使用 OMS 功能「設定解決方案目標」，此功能可讓您將範圍套用至解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-107">This article describes how to use **Solution Targeting** which is an OMS feature that allows you to apply a scope to your solutions.</span></span>

## <a name="how-to-target-a-solution"></a><span data-ttu-id="57d6a-108">如何為解決方案設定目標</span><span class="sxs-lookup"><span data-stu-id="57d6a-108">How to target a solution</span></span>
<span data-ttu-id="57d6a-109">為解決方案設定目標有三個步驟，如下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="57d6a-109">There are three steps to targeting a solution as described in the following sections.</span></span>  <span data-ttu-id="57d6a-110">請注意，針對不同的步驟，您將需要 OMS 入口網站和 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="57d6a-110">Note that you will need both the OMS portal and the Azure portal for different steps.</span></span>


### <a name="1-create-a-computer-group"></a><span data-ttu-id="57d6a-111">1.建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="57d6a-111">1. Create a computer group</span></span>
<span data-ttu-id="57d6a-112">您可以透過在 Log Analytics 中建立[電腦群組](../log-analytics/log-analytics-computer-groups.md)，來指定您想要包含在範圍內的電腦。</span><span class="sxs-lookup"><span data-stu-id="57d6a-112">You specify the computers that you want to include in a scope by creating a [computer group](../log-analytics/log-analytics-computer-groups.md) in Log Analytics.</span></span>  <span data-ttu-id="57d6a-113">電腦群組可以是根據記錄搜尋，或者從其他來源匯入 (例如 Active Directory 或 WSUS 群組)。</span><span class="sxs-lookup"><span data-stu-id="57d6a-113">The computer group can be based on a log search or imported from other sources such as Active Directory or WSUS groups.</span></span> <span data-ttu-id="57d6a-114">[如同下面所述](#solutions-and-agents-that-cant-be-targeted)，只有直接連線至 Log Analytics 的電腦才會包含在範圍內。</span><span class="sxs-lookup"><span data-stu-id="57d6a-114">As [described below](#solutions-and-agents-that-cant-be-targeted), only computers that are directly connected to Log Analytics will be included in the scope.</span></span>

<span data-ttu-id="57d6a-115">一旦您在工作區中建立電腦群組，便可將它包含在可套用至一或多個解決方案的範圍設定中。</span><span class="sxs-lookup"><span data-stu-id="57d6a-115">Once you have the computer group created in your workspace, then you'll include it in a scope configuration that can be applied to one or more solutions.</span></span>
 
 
 ### <a name="2-create-a-scope-configuration"></a><span data-ttu-id="57d6a-116">2.建立範圍設定</span><span class="sxs-lookup"><span data-stu-id="57d6a-116">2. Create a scope configuration</span></span>
 <span data-ttu-id="57d6a-117">「範圍設定」包含一或多個電腦群組，可以套用至一或多個解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-117">A **Scope Configuration** includes one or more computer groups and can be applied to one or more solutions.</span></span> 
 
 <span data-ttu-id="57d6a-118">使用下列程序建立範圍設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-118">Create a scope configuration using the following process.</span></span>  

 1. <span data-ttu-id="57d6a-119">在 Azure 入口網站中，瀏覽至 [Log Analytics] 並選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="57d6a-119">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="57d6a-120">在工作區內容中的 [工作區資料來源] 底下，選取 [範圍設定]。</span><span class="sxs-lookup"><span data-stu-id="57d6a-120">In the properties for the workspace under **Workspace Data Sources** select **Scope Configurations**.</span></span>
 3. <span data-ttu-id="57d6a-121">按一下 [新增] 以建立新的範圍設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-121">Click **Add** to create a new scope configuration.</span></span>
 4. <span data-ttu-id="57d6a-122">輸入範圍設定的 [名稱]。</span><span class="sxs-lookup"><span data-stu-id="57d6a-122">Type a **Name** for the scope configuration.</span></span>
 5. <span data-ttu-id="57d6a-123">按一下 [選取電腦群組]。</span><span class="sxs-lookup"><span data-stu-id="57d6a-123">Click **Select Computer Groups**.</span></span>
 6. <span data-ttu-id="57d6a-124">選取您所建立的電腦群組 (並選擇性地選取其他群組) 以新增至設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-124">Select the computer group that you created and optionally any other groups to add to the configuration.</span></span>  <span data-ttu-id="57d6a-125">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="57d6a-125">Click **Select**.</span></span>  
 6. <span data-ttu-id="57d6a-126">按一下 [確定] 以建立範圍設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-126">Click **OK** to create the scope configuration.</span></span> 


 ### <a name="3-apply-the-scope-configuration-to-a-solution"></a><span data-ttu-id="57d6a-127">3.將範圍設定套用至解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-127">3. Apply the scope configuration to a solution.</span></span>
<span data-ttu-id="57d6a-128">一旦您有範圍設定，便可以將它套用至一或多個解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-128">Once you have a scope configuration, then you can apply it to one or more solutions.</span></span>  <span data-ttu-id="57d6a-129">請注意，雖然單一範圍設定可以搭配多個解決方案使用，但每個解決方案僅可以使用一個範圍設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-129">Note that while a single scope configuration can be used with multiple solutions, each solution can only use one scope configuration.</span></span>

<span data-ttu-id="57d6a-130">使用下列程序套用範圍設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-130">Apply a scope configuration using the following process.</span></span>  

 1. <span data-ttu-id="57d6a-131">在 Azure 入口網站中，瀏覽至 [Log Analytics] 並選取您的工作區。</span><span class="sxs-lookup"><span data-stu-id="57d6a-131">In the Azure portal, navigate to **Log Analytics** and select your workspace.</span></span>
 2. <span data-ttu-id="57d6a-132">在工作區內容中，選取 [解決方案]。</span><span class="sxs-lookup"><span data-stu-id="57d6a-132">In the properties for the workspace select **Solutions**.</span></span>
 3. <span data-ttu-id="57d6a-133">按一下您想要設定範圍的解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-133">Click on the solution you want to scope.</span></span>
 4. <span data-ttu-id="57d6a-134">在解決方案內容中的 [工作區資料來源] 底下，選取 [設定解決方案目標]。</span><span class="sxs-lookup"><span data-stu-id="57d6a-134">In the properties for the solution under **Workspace Data Sources** select **Solution Targeting**.</span></span>  <span data-ttu-id="57d6a-135">如果該選項無法使用，便代表[此解決方案無法設定目標](#solutions-and-agents-that-cant-be-targeted)。</span><span class="sxs-lookup"><span data-stu-id="57d6a-135">If the option is not available then [this solution cannot be targeted](#solutions-and-agents-that-cant-be-targeted).</span></span>
 5. <span data-ttu-id="57d6a-136">按一下 [新增範圍設定]。</span><span class="sxs-lookup"><span data-stu-id="57d6a-136">Click **Add scope configuration**.</span></span>  <span data-ttu-id="57d6a-137">如果您已經將設定套用到此解決方案，則此選項將無法使用。</span><span class="sxs-lookup"><span data-stu-id="57d6a-137">If you already have a configuration applied to this solution then this option will be unavailable.</span></span>  <span data-ttu-id="57d6a-138">您必須移除現有設定，才能新增其他設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-138">You must remove the existing configuration before adding another one.</span></span>
 6. <span data-ttu-id="57d6a-139">按一下您所建立的範圍設定。</span><span class="sxs-lookup"><span data-stu-id="57d6a-139">Click on the scope configuration that you created.</span></span>
 7. <span data-ttu-id="57d6a-140">查看設定的 [狀態]，以確定它顯示 [成功]。</span><span class="sxs-lookup"><span data-stu-id="57d6a-140">Watch the **Status** of the configuration to ensure that it shows **Succeeded**.</span></span>  <span data-ttu-id="57d6a-141">如果狀態顯示發生錯誤，請按一下設定右側的省略符號，並選取 [編輯範圍設定] 以進行變更。</span><span class="sxs-lookup"><span data-stu-id="57d6a-141">If the status indicates an error, then click the ellipse to the right of the configuration and select **Edit scope configuration** to make changes.</span></span>

## <a name="solutions-and-agents-that-cant-be-targeted"></a><span data-ttu-id="57d6a-142">無法設定目標的解決方案和代理程式</span><span class="sxs-lookup"><span data-stu-id="57d6a-142">Solutions and agents that can't be targeted</span></span>
<span data-ttu-id="57d6a-143">下列是無法搭配「設定解決方案目標」使用的代理程式和解決方案準則。</span><span class="sxs-lookup"><span data-stu-id="57d6a-143">Following are the criteria for agents and solutions that can't be used with solution targeting.</span></span>

- <span data-ttu-id="57d6a-144">「設定解決方案目標」僅適用於會部署至代理程式的解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-144">Solution targeting only applies to solutions that deploy to agents.</span></span>
- <span data-ttu-id="57d6a-145">「設定解決方案目標」僅適用於 Microsoft 提供的解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-145">Solution targeting only applies to solutions provided by Microsoft.</span></span>  <span data-ttu-id="57d6a-146">不適用於[由您或合作夥伴所建立的](operations-management-suite-solutions-creating.md)解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-146">It does not apply to solutions [created by yourself or partners](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="57d6a-147">您只能篩選掉直接連線至 Log Analytics 的代理程式。</span><span class="sxs-lookup"><span data-stu-id="57d6a-147">You can only filter out agents that connect directly to Log Analytics.</span></span>  <span data-ttu-id="57d6a-148">解決方案會自動部署到屬於已連線 Operations Manager 管理群組之一部分的所有代理程式，不論它們是否包含在範圍設定內。</span><span class="sxs-lookup"><span data-stu-id="57d6a-148">Solutions will automatically deploy to any agents that are part of a connected Operations Manager management group whether or not they're included in a scope configuration.</span></span>

### <a name="exceptions"></a><span data-ttu-id="57d6a-149">例外狀況</span><span class="sxs-lookup"><span data-stu-id="57d6a-149">Exceptions</span></span>
<span data-ttu-id="57d6a-150">「設定解決方案目標」無法搭配下列解決方案使用，即使它們符合上述準則。</span><span class="sxs-lookup"><span data-stu-id="57d6a-150">Solution targeting cannot be used with the following solutions even though they fit the stated criteria.</span></span>

- <span data-ttu-id="57d6a-151">代理程式健康狀態評估</span><span class="sxs-lookup"><span data-stu-id="57d6a-151">Agent Health Assessment</span></span>

## <a name="next-steps"></a><span data-ttu-id="57d6a-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57d6a-152">Next steps</span></span>
- <span data-ttu-id="57d6a-153">在[將 Azure Log Analytics 管理解決方案新增至您的工作區](../log-analytics/log-analytics-add-solutions.md)中深入了解管理解決方案，包含可在您的環境中安裝的可用解決方案。</span><span class="sxs-lookup"><span data-stu-id="57d6a-153">Learn more about management solutions including the solutions that are available to install in your environment at [Add Azure Log Analytics management solutions to your workspace](../log-analytics/log-analytics-add-solutions.md).</span></span>
- <span data-ttu-id="57d6a-154">在 [Log Analytics 記錄檔搜尋中的電腦群組](../log-analytics/log-analytics-computer-groups.md)中深入了解建立電腦群組。</span><span class="sxs-lookup"><span data-stu-id="57d6a-154">Learn more about creating computer groups at [Computer groups in Log Analytics log searches](../log-analytics/log-analytics-computer-groups.md).</span></span>