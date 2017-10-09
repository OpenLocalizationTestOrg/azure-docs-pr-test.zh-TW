---
title: "與 Visual stuido 來 Team Services 原始檔控制的 Azure 自動化 aaaIntegrate |Microsoft 文件"
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
ms.openlocfilehash: 8f6faa596a5ad1f8b72e820ca320b3e103d83579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---automation-source-control-integration-with-visual-studio-team-services"></a><span data-ttu-id="3fab6-104">Azure 自動化案例 - 自動化原始檔控制與 Visual Studio Team Services 的整合</span><span class="sxs-lookup"><span data-stu-id="3fab6-104">Azure Automation scenario - Automation source control integration with Visual Studio Team Services</span></span>

<span data-ttu-id="3fab6-105">在此案例中，您有 Visual Studio Team Services 專案，您會使用 toomanage Azure 自動化 runbook 或原始檔控制下的 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="3fab6-105">In this scenario, you have a Visual Studio Team Services project that you are using toomanage Azure Automation runbooks or DSC configurations under source control.</span></span>
<span data-ttu-id="3fab6-106">本文說明如何與 Azure 自動化環境讓該持續整合就進行每次簽入 toointegrate VSTS。</span><span class="sxs-lookup"><span data-stu-id="3fab6-106">This article describes how toointegrate VSTS with your Azure Automation environment so that continuous integration happens for each check-in.</span></span>

## <a name="getting-hello-scenario"></a><span data-ttu-id="3fab6-107">取得 hello 案例</span><span class="sxs-lookup"><span data-stu-id="3fab6-107">Getting hello scenario</span></span>

<span data-ttu-id="3fab6-108">此案例包含兩個您可以直接從 hello 匯入的 PowerShell runbook [Runbook 庫](automation-runbook-gallery.md)在 hello Azure 入口網站，或從 hello 下載[PowerShell 資源庫](https://www.powershellgallery.com)。</span><span class="sxs-lookup"><span data-stu-id="3fab6-108">This scenario consists of two PowerShell runbooks that you can import directly from hello [Runbook Gallery](automation-runbook-gallery.md) in hello Azure portal or download from hello [PowerShell Gallery](https://www.powershellgallery.com).</span></span>

### <a name="runbooks"></a><span data-ttu-id="3fab6-109">Runbook</span><span class="sxs-lookup"><span data-stu-id="3fab6-109">Runbooks</span></span>

<span data-ttu-id="3fab6-110">Runbook</span><span class="sxs-lookup"><span data-stu-id="3fab6-110">Runbook</span></span> | <span data-ttu-id="3fab6-111">說明</span><span class="sxs-lookup"><span data-stu-id="3fab6-111">Description</span></span>| 
--------|------------|
<span data-ttu-id="3fab6-112">Sync-VSTS</span><span class="sxs-lookup"><span data-stu-id="3fab6-112">Sync-VSTS</span></span> | <span data-ttu-id="3fab6-113">完成簽入時，從 VSTS 原始檔控制匯入 Runbook 或組態。</span><span class="sxs-lookup"><span data-stu-id="3fab6-113">Import runbooks or configurations from VSTS source control when a check-in is done.</span></span> <span data-ttu-id="3fab6-114">如果以手動方式執行，它將會匯入及發行所有 runbook 或設定成 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-114">If run manually, it will import and publish all runbooks or configurations into hello Automation account.</span></span>| 
<span data-ttu-id="3fab6-115">Sync-VSTSGit</span><span class="sxs-lookup"><span data-stu-id="3fab6-115">Sync-VSTSGit</span></span> | <span data-ttu-id="3fab6-116">完成簽入時，從 Git 原始檔控制下的 VSTS 匯入 Runbook 或組態。</span><span class="sxs-lookup"><span data-stu-id="3fab6-116">Import runbooks or configurations from VSTS under Git source control when a check-in is done.</span></span> <span data-ttu-id="3fab6-117">如果以手動方式執行，它將會匯入及發行所有 runbook 或設定成 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-117">If run manually, it will import and publish all runbooks or configurations into hello Automation account.</span></span>|

### <a name="variables"></a><span data-ttu-id="3fab6-118">變數</span><span class="sxs-lookup"><span data-stu-id="3fab6-118">Variables</span></span>

<span data-ttu-id="3fab6-119">變數</span><span class="sxs-lookup"><span data-stu-id="3fab6-119">Variable</span></span> | <span data-ttu-id="3fab6-120">說明</span><span class="sxs-lookup"><span data-stu-id="3fab6-120">Description</span></span>|
-----------|------------|
<span data-ttu-id="3fab6-121">VSToken</span><span class="sxs-lookup"><span data-stu-id="3fab6-121">VSToken</span></span> | <span data-ttu-id="3fab6-122">保護變數將會建立包含的資產 hello VSTS 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="3fab6-122">Secure variable asset you will create that contains hello VSTS personal access token.</span></span> <span data-ttu-id="3fab6-123">您可以了解如何 toocreate VSTS 個人存取權杖上 hello [VSTS 驗證頁面](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)。</span><span class="sxs-lookup"><span data-stu-id="3fab6-123">You can learn how toocreate a VSTS personal access token on hello [VSTS authentication page](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview).</span></span> 
## <a name="installing-and-configuring-this-scenario"></a><span data-ttu-id="3fab6-124">安裝和設定此案例</span><span class="sxs-lookup"><span data-stu-id="3fab6-124">Installing and configuring this scenario</span></span>

<span data-ttu-id="3fab6-125">建立[個人存取權杖](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview)VSTS 您將為您的自動化帳戶使用 toosync hello runbook 或組態中。</span><span class="sxs-lookup"><span data-stu-id="3fab6-125">Create a [personal access token](https://www.visualstudio.com/en-us/docs/integrate/get-started/auth/overview) in VSTS that you will use toosync hello runbooks or configurations into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPersonalToken.png) 

<span data-ttu-id="3fab6-126">建立[secure 變數](automation-variables.md)在您的自動化帳戶 toohold hello 個人存取權杖，讓 hello runbook 可以驗證 tooVSTS 和同步處理 hello runbook 或設定成 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-126">Create a [secure variable](automation-variables.md) in your automation account toohold hello personal access token so that hello runbook can authenticate tooVSTS and sync hello runbooks or configurations into hello Automation account.</span></span> <span data-ttu-id="3fab6-127">您可以將此命名為 VSToken。</span><span class="sxs-lookup"><span data-stu-id="3fab6-127">You can name this VSToken.</span></span> 

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSTokenVariable.png)

<span data-ttu-id="3fab6-128">匯入 hello runbook 會同步您的 runbook 或設定成 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-128">Import hello runbook that will sync your runbooks or configurations into hello automation account.</span></span> <span data-ttu-id="3fab6-129">您可以使用 hello [VSTS 範例 runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript)或 hello [VSTS 與 Git 範例 runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) 從 hello PowerShellGallery.com 視您使用 VSTS原始檔控制或 Git 與 VSTS 和部署 tooyour 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-129">You can use hello [VSTS sample runbook](https://www.powershellgallery.com/packages/Sync-VSTS/1.0/DisplayScript) or hello [VSTS with Git sample runbook] (https://www.powershellgallery.com/packages/Sync-VSTSGit/1.0/DisplayScript) from hello PowerShellGallery.com depending on if you use VSTS source control or VSTS with Git and deploy tooyour automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPowerShellGallery.png)

<span data-ttu-id="3fab6-130">您現在可以[發佈](automation-creating-importing-runbook.md#publishing-a-runbook)此 Runbook，以便建立 Webhook.</span><span class="sxs-lookup"><span data-stu-id="3fab6-130">You can now [publish](automation-creating-importing-runbook.md#publishing-a-runbook) this runbook so you can create a webhook.</span></span> 
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSPublishRunbook.png)

<span data-ttu-id="3fab6-131">建立[webhook](automation-webhooks.md)此同步 VSTS runbook 和填滿 hello 參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3fab6-131">Create a [webhook](automation-webhooks.md) for this Sync-VSTS runbook and fill in hello parameters as shown below.</span></span> <span data-ttu-id="3fab6-132">請確定您複製 hello webhook url 將需於 VSTS 中的服務勾點。</span><span class="sxs-lookup"><span data-stu-id="3fab6-132">Make sure you copy hello webhook url as you will need it for a service hook in VSTS.</span></span> <span data-ttu-id="3fab6-133">hello VSAccessTokenVariableName 為您建立舊版 toohold hello 個人存取權杖的 hello 安全變數 hello 名稱 (VSToken)。</span><span class="sxs-lookup"><span data-stu-id="3fab6-133">hello VSAccessTokenVariableName is hello name (VSToken) of hello secure variable that you created earlier toohold hello personal access token.</span></span> 

<span data-ttu-id="3fab6-134">整合與 VSTS (同步-VSTS.ps1) 需要下列參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="3fab6-134">Integrating with VSTS (Sync-VSTS.ps1) will take hello following parameters.</span></span>
### <a name="sync-vsts-parameters"></a><span data-ttu-id="3fab6-135">Sync-VSTS Parameters</span><span class="sxs-lookup"><span data-stu-id="3fab6-135">Sync-VSTS Parameters</span></span>

<span data-ttu-id="3fab6-136">參數</span><span class="sxs-lookup"><span data-stu-id="3fab6-136">Parameter</span></span> | <span data-ttu-id="3fab6-137">說明</span><span class="sxs-lookup"><span data-stu-id="3fab6-137">Description</span></span>| 
--------|------------|
<span data-ttu-id="3fab6-138">WebhookData</span><span class="sxs-lookup"><span data-stu-id="3fab6-138">WebhookData</span></span> | <span data-ttu-id="3fab6-139">這會包含從 hello VSTS 服務勾點傳送 hello 簽入資訊。</span><span class="sxs-lookup"><span data-stu-id="3fab6-139">This will contain hello checkin information sent from hello VSTS service hook.</span></span> <span data-ttu-id="3fab6-140">您應該將此參數保留為空白。</span><span class="sxs-lookup"><span data-stu-id="3fab6-140">You should leave this parameter blank.</span></span>| 
<span data-ttu-id="3fab6-141">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3fab6-141">ResourceGroup</span></span> | <span data-ttu-id="3fab6-142">這是 hello hello 資源群組中的 hello 自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-142">This is hello name of hello resource group that hello automation account is in.</span></span>|
<span data-ttu-id="3fab6-143">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="3fab6-143">AutomationAccountName</span></span> | <span data-ttu-id="3fab6-144">hello hello 與 VSTS 將同步的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-144">hello name of hello automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="3fab6-145">VSFolder</span><span class="sxs-lookup"><span data-stu-id="3fab6-145">VSFolder</span></span> | <span data-ttu-id="3fab6-146">VSTS 存在 hello runbook 和組態中的 hello 資料夾的名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-146">The name of hello folder in VSTS where hello runbooks and configurations exist.</span></span>|
<span data-ttu-id="3fab6-147">VSAccount</span><span class="sxs-lookup"><span data-stu-id="3fab6-147">VSAccount</span></span> | <span data-ttu-id="3fab6-148">hello hello Visual Studio Team Services 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-148">hello name of hello Visual Studio Team Services account.</span></span>| 
<span data-ttu-id="3fab6-149">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="3fab6-149">VSAccessTokenVariableName</span></span> | <span data-ttu-id="3fab6-150">hello hello 安全的變數名稱 (VSToken) 保留 hello VSTS 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="3fab6-150">hello name of hello secure variable (VSToken) that holds hello VSTS personal access token.</span></span>| 


![](media/automation-scenario-source-control-integration-with-VSTS/VSTSWebhook.png)

<span data-ttu-id="3fab6-151">如果您使用 VSTS 含 GIT (同步-VSTSGit.ps1) 需要下列參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="3fab6-151">If you are using VSTS with GIT (Sync-VSTSGit.ps1) it will take hello following parameters.</span></span>

<span data-ttu-id="3fab6-152">參數</span><span class="sxs-lookup"><span data-stu-id="3fab6-152">Parameter</span></span> | <span data-ttu-id="3fab6-153">說明</span><span class="sxs-lookup"><span data-stu-id="3fab6-153">Description</span></span>|
--------|------------|
<span data-ttu-id="3fab6-154">WebhookData</span><span class="sxs-lookup"><span data-stu-id="3fab6-154">WebhookData</span></span> | <span data-ttu-id="3fab6-155">這會包含從 hello VSTS 服務勾點傳送 hello 簽入資訊。</span><span class="sxs-lookup"><span data-stu-id="3fab6-155">This will contain hello checkin information sent from hello VSTS service hook.</span></span> <span data-ttu-id="3fab6-156">您應該將此參數保留為空白。</span><span class="sxs-lookup"><span data-stu-id="3fab6-156">You should leave this parameter blank.</span></span>| <span data-ttu-id="3fab6-157">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3fab6-157">ResourceGroup</span></span> | <span data-ttu-id="3fab6-158">這個 hello hello 資源群組的名稱中的 hello 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-158">This hello name of hello resource group that hello automation account is in.</span></span>|
<span data-ttu-id="3fab6-159">AutomationAccountName</span><span class="sxs-lookup"><span data-stu-id="3fab6-159">AutomationAccountName</span></span> | <span data-ttu-id="3fab6-160">hello hello 與 VSTS 將同步的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-160">hello name of hello automation account that will sync with VSTS.</span></span>|
<span data-ttu-id="3fab6-161">VSAccount</span><span class="sxs-lookup"><span data-stu-id="3fab6-161">VSAccount</span></span> | <span data-ttu-id="3fab6-162">hello hello Visual Studio Team Services 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-162">hello name of hello Visual Studio Team Services account.</span></span>|
<span data-ttu-id="3fab6-163">VSProject</span><span class="sxs-lookup"><span data-stu-id="3fab6-163">VSProject</span></span> | <span data-ttu-id="3fab6-164">hello VSTS 存在 hello runbook 和組態中的 hello 專案名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-164">hello name of hello project in VSTS where hello runbooks and configurations exist.</span></span>|
<span data-ttu-id="3fab6-165">GitRepo</span><span class="sxs-lookup"><span data-stu-id="3fab6-165">GitRepo</span></span> | <span data-ttu-id="3fab6-166">hello hello Git 儲存機制名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-166">hello name of hello Git repository.</span></span>|
<span data-ttu-id="3fab6-167">GitBranch</span><span class="sxs-lookup"><span data-stu-id="3fab6-167">GitBranch</span></span> | <span data-ttu-id="3fab6-168">hello VSTS Git 儲存機制中的 hello 分支名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-168">hello name of hello branch in VSTS Git repository.</span></span>|
<span data-ttu-id="3fab6-169">資料夾</span><span class="sxs-lookup"><span data-stu-id="3fab6-169">Folder</span></span> | <span data-ttu-id="3fab6-170">hello VSTS Git 分支中的 hello 資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="3fab6-170">hello name of hello folder in VSTS Git branch.</span></span>|
<span data-ttu-id="3fab6-171">VSAccessTokenVariableName</span><span class="sxs-lookup"><span data-stu-id="3fab6-171">VSAccessTokenVariableName</span></span> | <span data-ttu-id="3fab6-172">hello hello 安全的變數名稱 (VSToken) 保留 hello VSTS 個人存取權杖。</span><span class="sxs-lookup"><span data-stu-id="3fab6-172">hello name of hello secure variable (VSToken) that holds hello VSTS personal access token.</span></span>|

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSGitWebhook.png)

<span data-ttu-id="3fab6-173">建立於 VSTS 中的服務勾點，此 webhook 在程式碼簽入觸發程序的簽入 toohello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3fab6-173">Create a service hook in VSTS for check-ins toohello folder that triggers this webhook on code check-in.</span></span> <span data-ttu-id="3fab6-174">選取 Web Hook 做為 hello 服務 toointegrate 與當您建立新的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-174">Select Web Hooks as hello service toointegrate with when you create a new subscription.</span></span> <span data-ttu-id="3fab6-175">您可以在 [VSTS 服務掛勾說明文件](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started)深入了解服務掛勾。</span><span class="sxs-lookup"><span data-stu-id="3fab6-175">You can learn more about service hooks on [VSTS Service Hooks documentation](https://www.visualstudio.com/en-us/docs/marketplace/integrate/service-hooks/get-started).</span></span>
![](media/automation-scenario-source-control-integration-with-VSTS/VSTSServiceHook.png)

<span data-ttu-id="3fab6-176">您應該要能 toodo 所有簽入您的 runbook 和 vsts 組態的並在這些自動現在會同步處理已為您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fab6-176">You should now be able toodo all check-ins of your runbooks and configurations into VSTS and have these automatically sync’d into your automation account.</span></span>

![](media/automation-scenario-source-control-integration-with-VSTS/VSTSSyncRunbookOutput.png)

<span data-ttu-id="3fab6-177">如果您手動執行此 runbook，而不由 VSTS 被觸發，則可以是空白 hello webhookdata 參數，它會執行完整同步處理從指定的 hello VSTS 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3fab6-177">If you run this runbook manually without being triggered by VSTS, you can leave hello webhookdata parameter empty and it will do a full sync from hello VSTS folder specified.</span></span>

<span data-ttu-id="3fab6-178">如果您想 toouninstall hello 案例中，從 VSTS 移除 hello 服務勾點，刪除 hello runbook 和 hello VSToken 變數。</span><span class="sxs-lookup"><span data-stu-id="3fab6-178">If you wish toouninstall hello scenario, remove hello service hook from VSTS, delete hello runbook, and hello VSToken variable.</span></span>
