---
title: "整合 Azure 自動化與 Visual Stuido Team Services 原始檔控制 | Microsoft Docs"
description: "案例將逐步引導您設定 Azure 自動化帳戶與 Visual Stuido Team Services 原始檔控制的整合。"
services: automation
documentationcenter: 
author: eamono
manager: 
editor: 
keywords: "azure powershell, VSTS, 原始檔控制, 自動化"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.openlocfilehash: 01f9c01c9e04e02dbb548b68cf99684ba6ddd57e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="293ef-104">Azure 自動化案例 - 自動化原始檔控制與 Visual Studio Team Services 的整合</span><span class="sxs-lookup"><span data-stu-id="293ef-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="293ef-105">在此案例中，您有 Visual Studio Team Services 專案可用來管理原始檔控制下的 Azure 自動化 Runbook 或 DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="293ef-105">In this scenario, you have a Visual Studio Team Services project that you are using to manage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="293ef-106">本文說明如何整合 VSTS 與 Azure 自動化環境，以便每次簽入時都能持續整合。</span><span class="sxs-lookup"><span data-stu-id="293ef-106">This article describes how to integrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-the-scenario"></a><span data-ttu-id="293ef-107">取得案例</span><span class="sxs-lookup"><span data-stu-id="293ef-107">Getting the scenario</span></span>

<span data-ttu-id="293ef-108">此案例包含兩個 PowerShell Runbook，可直接從 Azure 入口網站的 [Powerbook 資源庫](automation-runbook-gallery.md)匯入，也可以從 [PowerShell 資源庫](https://www.powershellgallery.com)下載。</span><span class="sxs-lookup"><span data-stu-id="293ef-108">This scenario consists of two PowerShell runbooks that you can import directly from the [Runbook Gallery](automation-runbook-gallery.md) in the Azure portal or download from the [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="293ef-109">Runbook</span><span class="sxs-lookup"><span data-stu-id="293ef-109">Runbooks</span></span>

<span data-ttu-id="293ef-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="293ef-110">Runbook</span></span> | <span data-ttu-id="293ef-111">說明</span><span class="sxs-lookup"><span data-stu-id="293ef-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="293ef-112">Sync-VSTS</span><span class="sxs-lookup"><span data-stu-id="293ef-112">Sync-VSTS</span></span> | <span data-ttu-id="293ef-113">完成簽入時，從 VSTS 原始檔控制匯入 Runbook 或組態。</span><span class="sxs-lookup"><span data-stu-id="293ef-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="293ef-114">如果以手動執行，它會將所有 Runbook 或組態匯入並發佈到自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="293ef-114">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>| 
<span data-ttu-id="293ef-115">Sync-VSTSGit</span><span class="sxs-lookup"><span data-stu-id="293ef-115">Sync-VSTSGit</span></span> | <span data-ttu-id="293ef-116">完成簽入時，從 Git 原始檔控制下的 VSTS 匯入 Runbook 或組態。</span><span class="sxs-lookup"><span data-stu-id="293ef-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="293ef-117">如果以手動執行，它會將所有 Runbook 或組態匯入並發佈到自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="293ef-117">If run manually, it will import and publish all runbooks or configurations into the Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="293ef-118">變數</span><span class="sxs-lookup"><span data-stu-id="293ef-118">Variables</span></span>

<span data-ttu-id="293ef-119">變數</span><span class="sxs-lookup"><span data-stu-id="293ef-119">Variable</span></span> | <span data-ttu-id="293ef-120">說明</span><span class="sxs-lookup"><span data-stu-id="293ef-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="293ef-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="293ef-121">VSToken</span></span> | <span data-ttu-id="293ef-122">您將建立的安全變數資產，其中包含 VSTS 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="293ef-122">Secure variable asset you will create that contains the VSTS personal access token.</span></span> <span data-ttu-id="293ef-123">您可以了解如何在 [VSTS 驗證頁面 (VSTS authentication page)](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) 建立 VSTS 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="293ef-123">You can learn how to create a VSTS personal access token on the [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="293ef-124">安裝和設定此案例</span><span class="sxs-lookup"><span data-stu-id="293ef-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="293ef-125">在 VSTS 中建立[個人存取權杖 (personal access token)](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)，用來將 Runbook 或組態同步處理到您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="293ef-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use to sync the runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="293ef-126">在自動化帳戶中建立[安全變數](automation-variables.md)以儲存個人存取權杖，讓 Runbook 可向 VSTS 驗證並將 Runbook 或組態同步處理到自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="293ef-126">Create a [secure variable](automation-variables.md) in your automation account to hold the personal access token so that the runbook can authenticate to VSTS and sync the runbooks or configurations into the Automation account.</span></span> <span data-ttu-id="293ef-127">您可以將此命名為 VSToken。</span><span class="sxs-lookup"><span data-stu-id="293ef-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="293ef-128">匯入的 Runbook 會將您的 Runbook 或組態同步處理到自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="293ef-128">Import the runbook that will sync your runbooks or configurations into the automation account.</span></span> <span data-ttu-id="293ef-129">如果您使用 VSTS 原始檔控制，可以使用來自 PowerShellGallery.com 的 [VSTS 範例 Runbook (VSTS sample runbook)](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript)，如果搭配 Git 使用 VSTS，則可以使用 [VSTS with Git 範例 Runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript)，然後再部署至自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="293ef-129">You can use the [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or the [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from the PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy to your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="293ef-130">您現在可以[發佈](automation-creating-importing-runbook.md#publishing-a-runbook)此 Runbook，以便建立 Webhook.</span><span class="sxs-lookup"><span data-stu-id="293ef-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="293ef-131">建立此 Sync-VSTS Runbook 的 [Webhook](automation-webhooks.md)，並填入參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="293ef-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in the parameters as shown below.</span></span> <span data-ttu-id="293ef-132">請務必複製 Webhook URL，因為您需要將它當做 VSTS 中的服務勾點。</span><span class="sxs-lookup"><span data-stu-id="293ef-132">Make sure you copy the webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="293ef-133">VSAccessTokenVariableName 是您稍早建立的安全變數名稱 (VSToken)，可保存個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="293ef-133">The VSAccessTokenVariableName is the name (VSToken) of the secure variable that you created earlier to hold the personal access token.</span></span> 

<span data-ttu-id="293ef-134">與 VSTS (Sync-VSTS.ps1) 整合將需要下列參數。</span><span class="sxs-lookup"><span data-stu-id="293ef-134">Integrating with VSTS (Sync-VSTS.ps1) will take the following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="293ef-135">Sync-VSTS Parameters</span><span class="sxs-lookup"><span data-stu-id="293ef-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="293ef-136">參數</span><span class="sxs-lookup"><span data-stu-id="293ef-136">Parameter</span></span> | <span data-ttu-id="293ef-137">說明</span><span class="sxs-lookup"><span data-stu-id="293ef-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="293ef-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="293ef-138">WebhookData</span></span> | <span data-ttu-id="293ef-139">這將包含從 VSTS 服務勾點傳送的簽入資訊。</span><span class="sxs-lookup"><span data-stu-id="293ef-139">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="293ef-140">您應該將此參數保留為空白。</span><span class="sxs-lookup"><span data-stu-id="293ef-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="293ef-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="293ef-141">ResourceGroup</span></span> | <span data-ttu-id="293ef-142">這是自動化帳戶所在資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-142">This is the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="293ef-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="293ef-143">AutomationAccountName</span></span> | <span data-ttu-id="293ef-144">與 VSTS 同步處理的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-144">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="293ef-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="293ef-145">VSFolder</span></span> | <span data-ttu-id="293ef-146">VSTS 中有 Runbook 與組態存在的資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-146">The name of the folder in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="293ef-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="293ef-147">VSAccount</span></span> | <span data-ttu-id="293ef-148">Visual Studio Team Services 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-148">The name of the Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="293ef-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="293ef-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="293ef-150">保留 VSTS 個人存取權杖的安全變數 (VSToken) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-150">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="293ef-151">如果您搭配 GIT 使用 VSTS (Sync-VSTSGit.ps1)，將需要下列參數。</span><span class="sxs-lookup"><span data-stu-id="293ef-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take the following parameters.</span></span>

<span data-ttu-id="293ef-152">參數</span><span class="sxs-lookup"><span data-stu-id="293ef-152">Parameter</span></span> | <span data-ttu-id="293ef-153">說明</span><span class="sxs-lookup"><span data-stu-id="293ef-153">Description</span></span>|
--------|------------|
<span data-ttu-id="293ef-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="293ef-154">WebhookData</span></span> | <span data-ttu-id="293ef-155">這將包含從 VSTS 服務勾點傳送的簽入資訊。</span><span class="sxs-lookup"><span data-stu-id="293ef-155">This will contain the checkin information sent from the VSTS service hook.</span></span> <span data-ttu-id="293ef-156">您應該將此參數保留為空白。</span><span class="sxs-lookup"><span data-stu-id="293ef-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="293ef-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="293ef-157">ResourceGroup</span></span> | <span data-ttu-id="293ef-158">這是自動化帳戶所在資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-158">This the name of the resource group that the automation account is in.</span></span>|
<span data-ttu-id="293ef-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="293ef-159">AutomationAccountName</span></span> | <span data-ttu-id="293ef-160">與 VSTS 同步處理的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-160">The name of the automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="293ef-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="293ef-161">VSAccount</span></span> | <span data-ttu-id="293ef-162">Visual Studio Team Services 帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-162">The name of the Visual Studio Team Services account.</span></span>|
<span data-ttu-id="293ef-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="293ef-163">VSProject</span></span> | <span data-ttu-id="293ef-164">VSTS 中有 Runbook 與組態存在的專案名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-164">The name of the project in VSTS where the runbooks and configurations exist.</span></span>|
<span data-ttu-id="293ef-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="293ef-165">GitRepo</span></span> | <span data-ttu-id="293ef-166">Git 儲存機制的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-166">The name of the Git repository.</span></span>|
<span data-ttu-id="293ef-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="293ef-167">GitBranch</span></span> | <span data-ttu-id="293ef-168">VSTS Git 儲存機制中分支的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-168">The name of the branch in VSTS Git repository.</span></span>|
<span data-ttu-id="293ef-169">資料夾</span><span class="sxs-lookup"><span data-stu-id="293ef-169">Folder</span></span> | <span data-ttu-id="293ef-170">VSTS Git 分支中資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-170">The name of the folder in VSTS Git branch.</span></span>|
<span data-ttu-id="293ef-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="293ef-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="293ef-172">保留 VSTS 個人存取權杖的安全變數 (VSToken) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="293ef-172">The name of the secure variable (VSToken) that holds the VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="293ef-173">針對會在程式碼簽入時觸發此 Webhook 的資料夾，在 VSTS 中建立服務掛勾以供簽入使用。</span><span class="sxs-lookup"><span data-stu-id="293ef-173">Create a service hook in VSTS for check-ins to the folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="293ef-174">選取 Webhook 作為建立新的訂用帳戶時要與之整合的服務。</span><span class="sxs-lookup"><span data-stu-id="293ef-174">Select Web Hooks as the service to integrate with when you create a new subscription.</span></span> <span data-ttu-id="293ef-175">您可以在 [VSTS 服務掛勾說明文件](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started)深入了解服務掛勾。</span><span class="sxs-lookup"><span data-stu-id="293ef-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="293ef-176">您現在應能執行 Runbook 和組態的所有簽入至 VSTS，並讓這些自動同步處理至您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="293ef-176">You should now be able to do all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="293ef-177">如果您以手動執行而非由 VSTS 觸發此 Runbook，您可以將 webhookdata 參數保留為空白，它會從指定的 VSTS 資料夾執行完整同步處理。</span><span class="sxs-lookup"><span data-stu-id="293ef-177">If you run this runbook manually without being triggered by VSTS, you can leave the webhookdata parameter empty and it will do a full sync from the VSTS folder specified.</span></span>

<span data-ttu-id="293ef-178">如果您想要將案例解除安裝，請從 VSTS 移除其服務掛勾，刪除 Runbook 和 VSToken 變數。</span><span class="sxs-lookup"><span data-stu-id="293ef-178">If you wish to uninstall the scenario, remove the service hook from VSTS, delete the runbook, and the VSToken variable.</span></span>
