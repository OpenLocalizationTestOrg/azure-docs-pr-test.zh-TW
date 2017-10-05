---
title: "Operations Management Suite (OMS) 中的解決方案 | Microsoft Docs"
description: "解決方案會藉由提供客戶可新增至他們 OMS 工作區的套件管理案例，以擴充 Operations Management Suite (OMS) 的功能。  本文提供如何自訂客戶和合作夥伴所建立之解決方案的詳細資訊。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2443dd73fdf441721bd6f6f340da515d9f5a22a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a><span data-ttu-id="3eb69-104">在 Operations Management Suite (OMS) 中使用管理解決方案 (預覽)</span><span class="sxs-lookup"><span data-stu-id="3eb69-104">Working with management solutions in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="3eb69-105">這是 OMS 中管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="3eb69-105">This is preliminary documentation for management solutions in OMS which are currently in preview.</span></span>    
> 
> 

<span data-ttu-id="3eb69-106">管理解決方案藉由提供客戶可新增至其環境的套裝管理案例，擴充 Operations Management Suite (OMS) 的功能。</span><span class="sxs-lookup"><span data-stu-id="3eb69-106">Management solutions extend the functionality of Operations Management Suite (OMS) by providing packaged management scenarios that customers can add to their environment.</span></span>  <span data-ttu-id="3eb69-107">除了 [Microsoft 所提供的解決方案](../log-analytics/log-analytics-add-solutions.md)，合作夥伴和客戶可以建立要用於其自己的環境中或可透過社群供您客戶使用的管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-107">In addition to [solutions provided by Microsoft](../log-analytics/log-analytics-add-solutions.md), partners and customers can create management solutions to be used in their own environment or made available to customers through the community.</span></span>

## <a name="finding-and-installing-management-solutions"></a><span data-ttu-id="3eb69-108">尋找及安裝管理解決方案</span><span class="sxs-lookup"><span data-stu-id="3eb69-108">Finding and installing management solutions</span></span>
<span data-ttu-id="3eb69-109">有多種方法可尋找及安裝下列各節中所述的管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-109">There are multiple methods for locating and installing management solutions as described in the following sections.</span></span>

### <a name="azure-marketplace"></a><span data-ttu-id="3eb69-110">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="3eb69-110">Azure Marketplace</span></span>
<span data-ttu-id="3eb69-111">可以從 Azure 入口網站中的 Azure Marketplace 安裝 Microsoft 和信任的夥伴所提供的管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-111">Management solutions provided by Microsoft and trusted partners may be installed from the Azure Marketplace in the Azure portal.</span></span>

1. <span data-ttu-id="3eb69-112">登入 Azure 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3eb69-112">Log in to the Azure portal.</span></span>
2. <span data-ttu-id="3eb69-113">在左側窗格中，選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="3eb69-113">In the left pane, select **More services**.</span></span>
3. <span data-ttu-id="3eb69-114">向下捲動至 [解決方案]，或在 [篩選] 對話方塊中輸入 solutions。</span><span class="sxs-lookup"><span data-stu-id="3eb69-114">Either scroll down to **Solutions** or type *solutions* into the **Filter** dialog.</span></span>
4. <span data-ttu-id="3eb69-115">按一下 [+新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb69-115">Click the **+ Add** button.</span></span>
5. <span data-ttu-id="3eb69-116">藉由瀏覽、按一下 [篩選] 按鈕，或在 [搜尋所有項目] 方塊中輸入資料，以搜尋您感興趣的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-116">Search for solutions that you're interested in either by browsing, clicking the **Filter** button, or typing in the **Search Everthing** box.</span></span>
6. <span data-ttu-id="3eb69-117">按一下 Marketplace 項目，以檢視其詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3eb69-117">Click a marketplace item to view its detailed information.</span></span>
7. <span data-ttu-id="3eb69-118">按一下 [建立] 以開啟 [新增方案] 窗格。</span><span class="sxs-lookup"><span data-stu-id="3eb69-118">Click **Create** to open the **Add Solution** pane.</span></span>
8. <span data-ttu-id="3eb69-119">除了解決方案中任何參數的值以外，系統還會提示您輸入所需的資訊，例如 [OMS 工作區和自動化帳戶](#oms-workspace-and-automation-account)。</span><span class="sxs-lookup"><span data-stu-id="3eb69-119">You will be prompted to required information such as the [OMS workspace and Automation account](#oms-workspace-and-automation-account) in addition to values for any parameters in the solution.</span></span>
9. <span data-ttu-id="3eb69-120">按一下 [建立] 以安裝解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-120">Click **Create** to install the solution.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="3eb69-121">OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="3eb69-121">OMS Portal</span></span>
<span data-ttu-id="3eb69-122">可以從 OMS 入口網站中的「方案庫」安裝 Microsoft 所提供的管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-122">Management solutions provided by Microsoft may be installed from the Solutions Gallery in the OMS portal.</span></span>

1. <span data-ttu-id="3eb69-123">登入 OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3eb69-123">Log in to the OMS portal.</span></span>
2. <span data-ttu-id="3eb69-124">按一下 [方案庫] 圖格。</span><span class="sxs-lookup"><span data-stu-id="3eb69-124">Click the **Solutions Gallery** tile.</span></span>
3. <span data-ttu-id="3eb69-125">在 [OMS 方案庫] 頁面中，您可以了解每個可用的方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-125">On the OMS Solutions Gallery page, learn about each available solution.</span></span> <span data-ttu-id="3eb69-126">按一下要加入 OMS 之方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="3eb69-126">Click the name of the solution that you want to add to OMS.</span></span>
4. <span data-ttu-id="3eb69-127">在所選解決方案的頁面中，該解決方案的詳細資料會顯示於此。</span><span class="sxs-lookup"><span data-stu-id="3eb69-127">On the page for the solution that you chose, detailed information about the solution is displayed.</span></span> <span data-ttu-id="3eb69-128">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="3eb69-128">Click **Add**.</span></span>
5. <span data-ttu-id="3eb69-129">加入方案之後，新建立的圖格會出現在 OMS 的 [概觀] 頁面中；待 OMS 服務處理資料後，您便可以開始使用該方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-129">A new tile for the solution that you added appears on the Overview page in OMS and you can start using it after the OMS service processes your data.</span></span>

### <a name="azure-quickstart-templates"></a><span data-ttu-id="3eb69-130">Azure 快速入門範本</span><span class="sxs-lookup"><span data-stu-id="3eb69-130">Azure Quickstart Templates</span></span>
<span data-ttu-id="3eb69-131">社群成員可以將管理解決方案提交至 Azure 快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="3eb69-131">Members of the community can submit management solutions to Azure Quickstart Templates.</span></span>  <span data-ttu-id="3eb69-132">您可以下載這些範本以供稍後安裝，或檢查這些範本以了解如何[建立自己的解決方案](#creating-a-solution)。</span><span class="sxs-lookup"><span data-stu-id="3eb69-132">You can either download these templates for later installation or inspect them to learn how to [create your own solutions](#creating-a-solution).</span></span>

1. <span data-ttu-id="3eb69-133">請依照 [OMS 工作區和自動化帳戶](#oms-workspace-and-automation-account)中所述的程序來連結工作區和帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb69-133">Follow the process described in [OMS workspace and Automation account](#oms-workspace-and-automation-account) to link a workspace and account.</span></span>
2. <span data-ttu-id="3eb69-134">移至 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="3eb69-134">Go to [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>  
3. <span data-ttu-id="3eb69-135">搜尋您感興趣的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-135">Search for a solution that you're interested in.</span></span>
4. <span data-ttu-id="3eb69-136">選取結果中的解決方案，以檢視其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3eb69-136">Select the solution from the results to view its details.</span></span>
5. <span data-ttu-id="3eb69-137">按一下 [部署至 Azure] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb69-137">Click the **Deploy to Azure** button.</span></span>
6. <span data-ttu-id="3eb69-138">除了解決方案中任何參數的值以外，系統還會提示您提供資源群組和位置等資訊。</span><span class="sxs-lookup"><span data-stu-id="3eb69-138">You will be prompted to provide information such as the resource group and location in addition to values for any parameters in the solution.</span></span>
7. <span data-ttu-id="3eb69-139">按一下 [購買] 以安裝解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-139">Click **Purchase** to install the solution.</span></span>

### <a name="deploy-azure-resource-manager-template"></a><span data-ttu-id="3eb69-140">部署 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3eb69-140">Deploy Azure Resource Manager template</span></span>
<span data-ttu-id="3eb69-141">您從社群取得的解決方案或您[自己建立](#creating-a-solution)的解決方案會當作 Resource Manager 範本實作，因此您可以使用任何[部署範本](../azure-resource-manager/resource-group-template-deploy-portal.md)的標準方法。</span><span class="sxs-lookup"><span data-stu-id="3eb69-141">Solutions that you get from the community or that you [create yourself](#creating-a-solution) are implemented as a Resource Manager template, and you can use any of the standard methods for [deploying a template](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>  <span data-ttu-id="3eb69-142">請注意，在安裝解決方案前，您必須建立並連結 [OMS 工作區和自動化帳戶](#oms-workspace-and-automation-account)。</span><span class="sxs-lookup"><span data-stu-id="3eb69-142">Note that before installing the solution, you must create and link the [OMS workspace and Automation account](#oms-workspace-and-automation-account).</span></span>

## <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="3eb69-143">OMS 工作區和自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="3eb69-143">OMS workspace and Automation account</span></span>
<span data-ttu-id="3eb69-144">大部分的管理解決方案都需要 [OMS 工作區](../log-analytics/log-analytics-manage-access.md)才會包含檢視，以及需要[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)才會包含 Runbook 和相關的資源。</span><span class="sxs-lookup"><span data-stu-id="3eb69-144">Most management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span> <span data-ttu-id="3eb69-145">工作區和帳戶必須符合下列需求。</span><span class="sxs-lookup"><span data-stu-id="3eb69-145">The workspace and account must meet the following requirements.</span></span>

* <span data-ttu-id="3eb69-146">一個解決方案只能使用一個 OMS 工作區和一個自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb69-146">A solution can only use one OMS workspace and one Automation account.</span></span>  
* <span data-ttu-id="3eb69-147">解決方案所用的 OMS 工作區和自動化帳戶必須連結到另一個。</span><span class="sxs-lookup"><span data-stu-id="3eb69-147">The OMS workspace and Automation account used by a solution must be linked to one another.</span></span> <span data-ttu-id="3eb69-148">OMS 工作區只能連結到一個自動化帳戶，而自動化帳戶只能連結至一個 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="3eb69-148">An OMS workspace may only be linked to one Automation account, and an Automation account may only be linked to one OMS workspace.</span></span>
* <span data-ttu-id="3eb69-149">若要連結，OMS 工作區和自動化帳戶必須位於相同的資源群組與區域中。</span><span class="sxs-lookup"><span data-stu-id="3eb69-149">To be linked, the OMS workspace and Automation account must be in the same resource group and region.</span></span>  <span data-ttu-id="3eb69-150">例外狀況是美國東部區域中的 OMS 工作區和美國東部 2 中的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb69-150">The exception is an OMS workspace in East US region and and Automation account in East US 2.</span></span>

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="3eb69-151">建立 OMS 工作區與自動化帳戶之間的連結</span><span class="sxs-lookup"><span data-stu-id="3eb69-151">Creating a link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="3eb69-152">指定 OMS 工作區和自動化帳戶的方式，取決於解決方案的安裝方法。</span><span class="sxs-lookup"><span data-stu-id="3eb69-152">How you specify the OMS workspace and Automation account depends on the installation method for your solution.</span></span>

* <span data-ttu-id="3eb69-153">當您透過 OMS 入口網站安裝 Microsoft 解決方案時，它會安裝在目前的 OMS 工作區中，而不需要自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb69-153">When you install a Microsoft solution through the OMS portal, it is installed in the current OMS workspace and no Automation account is required.</span></span>
* <span data-ttu-id="3eb69-154">當您透過 Azure Marketplace 安裝解決方案時，系統會提示您輸入 OMS 工作區和自動化帳戶，並為您建立它們之間的連結。</span><span class="sxs-lookup"><span data-stu-id="3eb69-154">When you install a solution through the Azure Marketplace, you are prompted for an OMS workspace and Automation account, and the link between them is created for you.</span></span>  
* <span data-ttu-id="3eb69-155">對於 Azure Marketplace 外部的解決方案，您必須在安裝解決方案之前，先連結 OMS 工作區和自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb69-155">For solutions outside of the Azure Marketplace, you must link the OMS workspace and Automation account before installing the solution.</span></span>  <span data-ttu-id="3eb69-156">選取 Azure Marketplace 中的任何解決方案並選取 OMS 工作區和自動化帳戶，即可執行此作業。</span><span class="sxs-lookup"><span data-stu-id="3eb69-156">You can do this by selecting any solution in the Azure Marketplace and selecting the OMS workspace and Automation account.</span></span>  <span data-ttu-id="3eb69-157">您不必實際安裝解決方案，因為在選取 OMS 工作區和自動化帳戶時，就會馬上建立連結。</span><span class="sxs-lookup"><span data-stu-id="3eb69-157">You don't have to actually install the solution because the link will be created as soon as the OMS workspace and Automation account are selected.</span></span>  <span data-ttu-id="3eb69-158">一旦建立連結，您即可將該 OMS 工作區和自動化帳戶使用於任何解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-158">Once the link is created, then you can use that OMS workspace and Automation account for any solution.</span></span> 

### <a name="verifying-the-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="3eb69-159">驗證 OMS 工作區與自動化帳戶之間的連結</span><span class="sxs-lookup"><span data-stu-id="3eb69-159">Verifying the link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="3eb69-160">您可以使用下列程序，驗證 OMS 工作區與自動化帳戶之間的連結。</span><span class="sxs-lookup"><span data-stu-id="3eb69-160">You can verify the link between an OMS workspace and an Automation account using the following procedure.</span></span>

1. <span data-ttu-id="3eb69-161">在 Azure 入口網站中選取自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3eb69-161">Select the Automation account in the Azure portal.</span></span>
2. <span data-ttu-id="3eb69-162">向下捲動到 [設定] 窗格底部。</span><span class="sxs-lookup"><span data-stu-id="3eb69-162">Scroll to the bottom of the **Settings** pane.</span></span>
3. <span data-ttu-id="3eb69-163">如果 [設定] 窗格中有名為 [OMS 資源] 的區段，則此帳戶會附加至 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="3eb69-163">If there is a section called **OMS Resources** in the **Settings** pane, then this account is attached to an OMS workspace.</span></span>
4. <span data-ttu-id="3eb69-164">選取 [工作區]，以檢視連結至此自動化帳戶之 OMS 工作區的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3eb69-164">Select **Workspace** to view the details of the OMS workspace linked to this Automation account.</span></span>

## <a name="listing-management-solutions"></a><span data-ttu-id="3eb69-165">列出管理解決方案</span><span class="sxs-lookup"><span data-stu-id="3eb69-165">Listing management solutions</span></span>
<span data-ttu-id="3eb69-166">使用下列程序，檢視連結至您的 Azure 訂用帳戶的工作區中的管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-166">Use the following procedure to to view the management solutions in the workspaces linked to your Azure subscription.</span></span>

1. <span data-ttu-id="3eb69-167">登入 Azure 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3eb69-167">Log in to the Azure portal.</span></span>
2. <span data-ttu-id="3eb69-168">在左側窗格中，選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="3eb69-168">In the left pane, select **More services**.</span></span>
3. <span data-ttu-id="3eb69-169">向下捲動至 [解決方案]，或在 [篩選] 對話方塊中輸入 solutions。</span><span class="sxs-lookup"><span data-stu-id="3eb69-169">Either scroll down to **Solutions** or type *solutions* into the **Filter** dialog.</span></span>
4. <span data-ttu-id="3eb69-170">將會列出安裝在您所有工作區中的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-170">Solutions installed in all your workspaces will be listed.</span></span>

<span data-ttu-id="3eb69-171">請注意，您只可以檢視使用 OMS 入口網站在目前工作區中安裝的 Microsoft 解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-171">Note that you can view only the Microsoft solutions installed in the current workspace using the OMS portal.</span></span>

## <a name="removing-a-management-solution"></a><span data-ttu-id="3eb69-172">移除管理解決方案</span><span class="sxs-lookup"><span data-stu-id="3eb69-172">Removing a management solution</span></span>
<span data-ttu-id="3eb69-173">移除管理解決方案時，也會移除解決方案中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="3eb69-173">When a management solution is removed, all resources in the solution are also removed.</span></span>  

1. <span data-ttu-id="3eb69-174">使用[列出解決方案](#listing-solutions)中的程序，在 Azure 入口網站中尋找解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-174">Locate the solution in the Azure portal using the procedure in [Listing solutions](#listing-solutions).</span></span>
2. <span data-ttu-id="3eb69-175">選取您想要移除的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3eb69-175">Select the solution you want to remove.</span></span>
3. <span data-ttu-id="3eb69-176">按一下 [刪除]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3eb69-176">Click the **Delete** button.</span></span>

## <a name="creating-a-management-solution"></a><span data-ttu-id="3eb69-177">建立管理解決方案</span><span class="sxs-lookup"><span data-stu-id="3eb69-177">Creating a management solution</span></span>
<span data-ttu-id="3eb69-178">[在 Operations Management Suite (OMS) 中建立解決方案](operations-management-suite-solutions-creating.md)提供有關建立管理解決方案的完整指引。</span><span class="sxs-lookup"><span data-stu-id="3eb69-178">Complete guidance on creating management solutions are available at [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3eb69-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3eb69-179">Next steps</span></span>
* <span data-ttu-id="3eb69-180">搜尋 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates)不同 Resource Manager 範本的範例。</span><span class="sxs-lookup"><span data-stu-id="3eb69-180">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
* <span data-ttu-id="3eb69-181">建立自己的[管理解決方案](operations-management-suite-solutions-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="3eb69-181">Create your own [management solutions](operations-management-suite-solutions-creating.md).</span></span>

