---
title: "aaaSolutions Operations Management Suite (OMS) |Microsoft 文件"
description: "解決方案會擴充 hello 功能 Operations Management Suite (OMS) 藉由提供封裝的管理案例，客戶可以加入 tootheir OMS 工作區。  本文提供如何自訂客戶和合作夥伴所建立之解決方案的詳細資訊。"
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
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a><span data-ttu-id="9b660-104">在 Operations Management Suite (OMS) 中使用管理解決方案 (預覽)</span><span class="sxs-lookup"><span data-stu-id="9b660-104">Working with management solutions in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="9b660-105">這是 OMS 中管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="9b660-105">This is preliminary documentation for management solutions in OMS which are currently in preview.</span></span>    
> 
> 

<span data-ttu-id="9b660-106">管理解決方案會擴充 hello 功能 Operations Management Suite (OMS) 藉由提供封裝的管理案例，客戶可以加入 tootheir 環境。</span><span class="sxs-lookup"><span data-stu-id="9b660-106">Management solutions extend hello functionality of Operations Management Suite (OMS) by providing packaged management scenarios that customers can add tootheir environment.</span></span>  <span data-ttu-id="9b660-107">此外太[由 Microsoft 提供的解決方案](../log-analytics/log-analytics-add-solutions.md)、 合作夥伴和客戶可以建立自己的環境中使用，或可透過 hello 社群可用 toocustomers 管理解決方案 toobe。</span><span class="sxs-lookup"><span data-stu-id="9b660-107">In addition too[solutions provided by Microsoft](../log-analytics/log-analytics-add-solutions.md), partners and customers can create management solutions toobe used in their own environment or made available toocustomers through hello community.</span></span>

## <a name="finding-and-installing-management-solutions"></a><span data-ttu-id="9b660-108">尋找及安裝管理解決方案</span><span class="sxs-lookup"><span data-stu-id="9b660-108">Finding and installing management solutions</span></span>
<span data-ttu-id="9b660-109">有多個方法來尋找及安裝管理解決方案的更多資訊，hello 下列各節中所述。</span><span class="sxs-lookup"><span data-stu-id="9b660-109">There are multiple methods for locating and installing management solutions as described in hello following sections.</span></span>

### <a name="azure-marketplace"></a><span data-ttu-id="9b660-110">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="9b660-110">Azure Marketplace</span></span>
<span data-ttu-id="9b660-111">由 Microsoft 提供的管理解決方案，而且受信任的協力廠商可能會安裝從 hello Azure 入口網站中的 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="9b660-111">Management solutions provided by Microsoft and trusted partners may be installed from hello Azure Marketplace in hello Azure portal.</span></span>

1. <span data-ttu-id="9b660-112">登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9b660-112">Log in toohello Azure portal.</span></span>
2. <span data-ttu-id="9b660-113">Hello 左窗格中，選取**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="9b660-113">In hello left pane, select **More services**.</span></span>
3. <span data-ttu-id="9b660-114">請向下捲動太**解決方案**或型別*解決方案*到 hello**篩選**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9b660-114">Either scroll down too**Solutions** or type *solutions* into hello **Filter** dialog.</span></span>
4. <span data-ttu-id="9b660-115">按一下 hello **+ 加** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b660-115">Click hello **+ Add** button.</span></span>
5. <span data-ttu-id="9b660-116">搜尋您感興趣藉由瀏覽的解決方案按一下 hello**篩選** 按鈕，或輸入 hello**搜尋積木**方塊。</span><span class="sxs-lookup"><span data-stu-id="9b660-116">Search for solutions that you're interested in either by browsing, clicking hello **Filter** button, or typing in hello **Search Everthing** box.</span></span>
6. <span data-ttu-id="9b660-117">按一下 marketplace 項目 tooview 其詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="9b660-117">Click a marketplace item tooview its detailed information.</span></span>
7. <span data-ttu-id="9b660-118">按一下**建立**tooopen hello**將方案加入**窗格。</span><span class="sxs-lookup"><span data-stu-id="9b660-118">Click **Create** tooopen hello **Add Solution** pane.</span></span>
8. <span data-ttu-id="9b660-119">您將會提示的 toorequired 資訊，例如 hello [OMS 工作區以及自動化帳戶](#oms-workspace-and-automation-account)中的任何參數的 toovalues 此外 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-119">You will be prompted toorequired information such as hello [OMS workspace and Automation account](#oms-workspace-and-automation-account) in addition toovalues for any parameters in hello solution.</span></span>
9. <span data-ttu-id="9b660-120">按一下**建立**tooinstall hello 方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-120">Click **Create** tooinstall hello solution.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="9b660-121">OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="9b660-121">OMS Portal</span></span>
<span data-ttu-id="9b660-122">由 Microsoft 提供的管理解決方案可能安裝從 hello OMS 入口網站中的 hello 解決方案資源庫。</span><span class="sxs-lookup"><span data-stu-id="9b660-122">Management solutions provided by Microsoft may be installed from hello Solutions Gallery in hello OMS portal.</span></span>

1. <span data-ttu-id="9b660-123">登入 toohello OMS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9b660-123">Log in toohello OMS portal.</span></span>
2. <span data-ttu-id="9b660-124">按一下 hello**解決方案資源庫**磚。</span><span class="sxs-lookup"><span data-stu-id="9b660-124">Click hello **Solutions Gallery** tile.</span></span>
3. <span data-ttu-id="9b660-125">在 [hello OMS 解決方案資源庫] 頁面上，了解每個可用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-125">On hello OMS Solutions Gallery page, learn about each available solution.</span></span> <span data-ttu-id="9b660-126">按一下您想 tooadd tooOMS hello 方案 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9b660-126">Click hello name of hello solution that you want tooadd tooOMS.</span></span>
4. <span data-ttu-id="9b660-127">在您選擇的 hello 解決方案 hello 頁面上，會顯示 hello 方案的詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="9b660-127">On hello page for hello solution that you chose, detailed information about hello solution is displayed.</span></span> <span data-ttu-id="9b660-128">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="9b660-128">Click **Add**.</span></span>
5. <span data-ttu-id="9b660-129">新建立的磚加入 將顯示在 hello 在 OMS 中的 概觀 頁面上，您便可以開始使用 hello OMS 服務處理資料後的 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-129">A new tile for hello solution that you added appears on hello Overview page in OMS and you can start using it after hello OMS service processes your data.</span></span>

### <a name="azure-quickstart-templates"></a><span data-ttu-id="9b660-130">Azure 快速入門範本</span><span class="sxs-lookup"><span data-stu-id="9b660-130">Azure Quickstart Templates</span></span>
<span data-ttu-id="9b660-131">Hello 社群的成員可以提交管理解決方案 tooAzure 快速入門範本。</span><span class="sxs-lookup"><span data-stu-id="9b660-131">Members of hello community can submit management solutions tooAzure Quickstart Templates.</span></span>  <span data-ttu-id="9b660-132">您可以下載這些更新版本安裝的範本，或檢查這些 toolearn 如何太[建立您自己的解決方案](#creating-a-solution)。</span><span class="sxs-lookup"><span data-stu-id="9b660-132">You can either download these templates for later installation or inspect them toolearn how too[create your own solutions](#creating-a-solution).</span></span>

1. <span data-ttu-id="9b660-133">請依照下列所述的 hello 程序[OMS 工作區以及自動化帳戶](#oms-workspace-and-automation-account)toolink 工作區和帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-133">Follow hello process described in [OMS workspace and Automation account](#oms-workspace-and-automation-account) toolink a workspace and account.</span></span>
2. <span data-ttu-id="9b660-134">跳過[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="9b660-134">Go too[Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>  
3. <span data-ttu-id="9b660-135">搜尋您感興趣的解決方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-135">Search for a solution that you're interested in.</span></span>
4. <span data-ttu-id="9b660-136">選取 hello 解決方案從 hello 結果 tooview 其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9b660-136">Select hello solution from hello results tooview its details.</span></span>
5. <span data-ttu-id="9b660-137">按一下 hello**部署 tooAzure**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b660-137">Click hello **Deploy tooAzure** button.</span></span>
6. <span data-ttu-id="9b660-138">系統會提示的 tooprovide 資訊，例如 hello 資源群組和新增 toovalues hello 方案中的任何參數中的位置。</span><span class="sxs-lookup"><span data-stu-id="9b660-138">You will be prompted tooprovide information such as hello resource group and location in addition toovalues for any parameters in hello solution.</span></span>
7. <span data-ttu-id="9b660-139">按一下**購買**tooinstall hello 方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-139">Click **Purchase** tooinstall hello solution.</span></span>

### <a name="deploy-azure-resource-manager-template"></a><span data-ttu-id="9b660-140">部署 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="9b660-140">Deploy Azure Resource Manager template</span></span>
<span data-ttu-id="9b660-141">您收到 hello 社群或您的方案[自行建立](#creating-a-solution)會實作為資源管理員範本，而且您可以使用任何 hello 標準方法[部署範本](../azure-resource-manager/resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="9b660-141">Solutions that you get from hello community or that you [create yourself](#creating-a-solution) are implemented as a Resource Manager template, and you can use any of hello standard methods for [deploying a template](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>  <span data-ttu-id="9b660-142">請注意，在安裝之前 hello 方案，您必須建立並連結 hello [OMS 工作區以及自動化帳戶](#oms-workspace-and-automation-account)。</span><span class="sxs-lookup"><span data-stu-id="9b660-142">Note that before installing hello solution, you must create and link hello [OMS workspace and Automation account](#oms-workspace-and-automation-account).</span></span>

## <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="9b660-143">OMS 工作區和自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="9b660-143">OMS workspace and Automation account</span></span>
<span data-ttu-id="9b660-144">大部分的管理解決方案需要[OMS 工作區](../log-analytics/log-analytics-manage-access.md)toocontain 檢視和[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)toocontain runbook 和相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="9b660-144">Most management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span> <span data-ttu-id="9b660-145">hello 工作區中，帳戶必須符合下列需求的 hello。</span><span class="sxs-lookup"><span data-stu-id="9b660-145">hello workspace and account must meet hello following requirements.</span></span>

* <span data-ttu-id="9b660-146">一個解決方案只能使用一個 OMS 工作區和一個自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-146">A solution can only use one OMS workspace and one Automation account.</span></span>  
* <span data-ttu-id="9b660-147">hello OMS 工作區和自動化解決方案所用的帳戶必須是連結的 tooone 另一個。</span><span class="sxs-lookup"><span data-stu-id="9b660-147">hello OMS workspace and Automation account used by a solution must be linked tooone another.</span></span> <span data-ttu-id="9b660-148">OMS 工作區只能連結的 tooone 自動化帳戶，並且自動化帳戶可能只是連結的 tooone OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="9b660-148">An OMS workspace may only be linked tooone Automation account, and an Automation account may only be linked tooone OMS workspace.</span></span>
* <span data-ttu-id="9b660-149">toobe 連結，hello OMS 工作區以及自動化帳戶必須在 hello 相同資源群組和區域。</span><span class="sxs-lookup"><span data-stu-id="9b660-149">toobe linked, hello OMS workspace and Automation account must be in hello same resource group and region.</span></span>  <span data-ttu-id="9b660-150">hello 例外狀況是在美國東部地區的 OMS 工作區，並在美國東部 2 中的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-150">hello exception is an OMS workspace in East US region and and Automation account in East US 2.</span></span>

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="9b660-151">建立 OMS 工作區與自動化帳戶之間的連結</span><span class="sxs-lookup"><span data-stu-id="9b660-151">Creating a link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="9b660-152">如何指定 hello OMS 工作區，並且自動化帳戶取決於您的方案的 hello 安裝方法。</span><span class="sxs-lookup"><span data-stu-id="9b660-152">How you specify hello OMS workspace and Automation account depends on hello installation method for your solution.</span></span>

* <span data-ttu-id="9b660-153">當您安裝 Microsoft 解決方案透過 hello OMS 入口網站時，它會安裝在 hello 目前 OMS 工作區，而且沒有任何自動化帳戶需要。</span><span class="sxs-lookup"><span data-stu-id="9b660-153">When you install a Microsoft solution through hello OMS portal, it is installed in hello current OMS workspace and no Automation account is required.</span></span>
* <span data-ttu-id="9b660-154">當您安裝透過 hello Azure Marketplace 的解決方案時，系統會提示您的 OMS 工作區，以及自動化帳戶和 hello 兩者之間的連結會為您建立。</span><span class="sxs-lookup"><span data-stu-id="9b660-154">When you install a solution through hello Azure Marketplace, you are prompted for an OMS workspace and Automation account, and hello link between them is created for you.</span></span>  
* <span data-ttu-id="9b660-155">有外部 hello Azure Marketplace 的解決方案，您必須安裝 hello 解決方案之前連結 hello OMS 工作區以及自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-155">For solutions outside of hello Azure Marketplace, you must link hello OMS workspace and Automation account before installing hello solution.</span></span>  <span data-ttu-id="9b660-156">您可以在 hello Azure Marketplace 中選取任何解決方案，並選取 hello OMS 工作區及自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-156">You can do this by selecting any solution in hello Azure Marketplace and selecting hello OMS workspace and Automation account.</span></span>  <span data-ttu-id="9b660-157">您不需要 tooactually 安裝 hello 方案，因為將會建立 hello 連結，為已選取 hello OMS 工作區] 和 [自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-157">You don't have tooactually install hello solution because hello link will be created as soon as hello OMS workspace and Automation account are selected.</span></span>  <span data-ttu-id="9b660-158">一旦建立 hello 連結，然後您可以使用該 OMS 工作區和自動化帳戶的任何方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-158">Once hello link is created, then you can use that OMS workspace and Automation account for any solution.</span></span> 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a><span data-ttu-id="9b660-159">正在驗證 hello OMS 工作區與自動化帳戶之間的連結</span><span class="sxs-lookup"><span data-stu-id="9b660-159">Verifying hello link between an OMS workspace and Automation account</span></span>
<span data-ttu-id="9b660-160">您可以確認 hello OMS 工作區與使用下列程序的 hello 自動化帳戶之間的連結。</span><span class="sxs-lookup"><span data-stu-id="9b660-160">You can verify hello link between an OMS workspace and an Automation account using hello following procedure.</span></span>

1. <span data-ttu-id="9b660-161">選取在 hello Azure 入口網站中的 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-161">Select hello Automation account in hello Azure portal.</span></span>
2. <span data-ttu-id="9b660-162">捲軸 toohello 底部 hello**設定**窗格。</span><span class="sxs-lookup"><span data-stu-id="9b660-162">Scroll toohello bottom of hello **Settings** pane.</span></span>
3. <span data-ttu-id="9b660-163">如果沒有呼叫的區段**OMS 資源**在 hello**設定** 窗格中，則此帳戶是附加的 tooan OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="9b660-163">If there is a section called **OMS Resources** in hello **Settings** pane, then this account is attached tooan OMS workspace.</span></span>
4. <span data-ttu-id="9b660-164">選取**工作區**tooview hello hello OMS 工作區詳細資料連結 toothis 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="9b660-164">Select **Workspace** tooview hello details of hello OMS workspace linked toothis Automation account.</span></span>

## <a name="listing-management-solutions"></a><span data-ttu-id="9b660-165">列出管理解決方案</span><span class="sxs-lookup"><span data-stu-id="9b660-165">Listing management solutions</span></span>
<span data-ttu-id="9b660-166">使用下列程序 tootooview hello hello 工作區連結 tooyour Azure 訂用帳戶中的管理解決方案的 hello。</span><span class="sxs-lookup"><span data-stu-id="9b660-166">Use hello following procedure tootooview hello management solutions in hello workspaces linked tooyour Azure subscription.</span></span>

1. <span data-ttu-id="9b660-167">登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9b660-167">Log in toohello Azure portal.</span></span>
2. <span data-ttu-id="9b660-168">Hello 左窗格中，選取**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="9b660-168">In hello left pane, select **More services**.</span></span>
3. <span data-ttu-id="9b660-169">請向下捲動太**解決方案**或型別*解決方案*到 hello**篩選**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9b660-169">Either scroll down too**Solutions** or type *solutions* into hello **Filter** dialog.</span></span>
4. <span data-ttu-id="9b660-170">將會列出安裝在您所有工作區中的解決方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-170">Solutions installed in all your workspaces will be listed.</span></span>

<span data-ttu-id="9b660-171">請注意，您可以檢視 hello 目前工作區中使用 hello OMS 入口網站安裝的唯一 hello Microsoft 解決方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-171">Note that you can view only hello Microsoft solutions installed in hello current workspace using hello OMS portal.</span></span>

## <a name="removing-a-management-solution"></a><span data-ttu-id="9b660-172">移除管理解決方案</span><span class="sxs-lookup"><span data-stu-id="9b660-172">Removing a management solution</span></span>
<span data-ttu-id="9b660-173">移除管理解決方案時，也會移除 hello 方案中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="9b660-173">When a management solution is removed, all resources in hello solution are also removed.</span></span>  

1. <span data-ttu-id="9b660-174">在 hello Azure 中尋找 hello 方案入口網站的使用中的 hello 程序[列出解決方案](#listing-solutions)。</span><span class="sxs-lookup"><span data-stu-id="9b660-174">Locate hello solution in hello Azure portal using hello procedure in [Listing solutions](#listing-solutions).</span></span>
2. <span data-ttu-id="9b660-175">選取您想要 tooremove hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="9b660-175">Select hello solution you want tooremove.</span></span>
3. <span data-ttu-id="9b660-176">按一下 hello**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b660-176">Click hello **Delete** button.</span></span>

## <a name="creating-a-management-solution"></a><span data-ttu-id="9b660-177">建立管理解決方案</span><span class="sxs-lookup"><span data-stu-id="9b660-177">Creating a management solution</span></span>
<span data-ttu-id="9b660-178">[在 Operations Management Suite (OMS) 中建立解決方案](operations-management-suite-solutions-creating.md)提供有關建立管理解決方案的完整指引。</span><span class="sxs-lookup"><span data-stu-id="9b660-178">Complete guidance on creating management solutions are available at [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9b660-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b660-179">Next steps</span></span>
* <span data-ttu-id="9b660-180">搜尋 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates)不同 Resource Manager 範本的範例。</span><span class="sxs-lookup"><span data-stu-id="9b660-180">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
* <span data-ttu-id="9b660-181">建立自己的[管理解決方案](operations-management-suite-solutions-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="9b660-181">Create your own [management solutions](operations-management-suite-solutions-creating.md).</span></span>

