---
title: "Azure 自動化中的原始檔控制整合 | Microsoft Docs"
description: "本文說明在 Azure 自動化中與 GitHub 的原始檔控制整合。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 224d7375-9887-44dd-b137-06ffe396a4b4
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 763bf5805e3a3cb95ad63c7a354dd3d4cd531b2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="source-control-integration-in-azure-automation"></a><span data-ttu-id="0c953-103">Azure 自動化中的原始檔控制整合</span><span class="sxs-lookup"><span data-stu-id="0c953-103">Source control integration in Azure Automation</span></span>
<span data-ttu-id="0c953-104">原始檔控制整合可讓您將自動化帳戶中的 Runbook 關聯至 GitHub 原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0c953-104">Source control integration allows you to associate runbooks in your Automation account to a GitHub source control repository.</span></span> <span data-ttu-id="0c953-105">原始檔控制可讓您輕鬆地與小組共同作業、追蹤變更，以及回復至舊版的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="0c953-105">Source control allows you to easily collaborate with your team, track changes, and roll back to earlier versions of your runbooks.</span></span> <span data-ttu-id="0c953-106">例如，原始檔控制可讓您將原始檔控制中的不同分支同步處理至您的開發、測試或生產自動化帳戶，以輕鬆地將已在開發環境中測試過的程式碼提升至生產自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c953-106">For example, source control allows you to sync different branches in source control to your development, test or production Automation accounts, making it easy to promote code that has been tested in your development environment to your production Automation account.</span></span>

<span data-ttu-id="0c953-107">原始檔控制可讓您從 Azure 自動化推送程式碼至原始檔控制，或將 Runbook 從原始檔控制提取至 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="0c953-107">Source control allows you to push code from Azure Automation to source control or pull your runbooks from source control to Azure Automation.</span></span> <span data-ttu-id="0c953-108">本文說明如何在 Azure 自動化環境中設定原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="0c953-108">This article describes how to set up source control in your Azure Automation environment.</span></span> <span data-ttu-id="0c953-109">我們將先設定 Azure 自動化存取 GitHub 儲存機制，並逐步解說可使用原始檔控制整合完成的不同作業。</span><span class="sxs-lookup"><span data-stu-id="0c953-109">We will start by configuring Azure Automation to access your GitHub repository and walk through different operations that can be done using source control integration.</span></span> 

> [!NOTE]
> <span data-ttu-id="0c953-110">原始檔控制支援提取和推送 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 以及 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="0c953-110">Source control supports pulling and pushing [PowerShell Workflow runbooks](automation-runbook-types.md#powershell-workflow-runbooks) as well as [PowerShell runbooks](automation-runbook-types.md#powershell-runbooks).</span></span> <span data-ttu-id="0c953-111">尚未支援[圖形化 Runbook](automation-runbook-types.md#graphical-runbooks)。</span><span class="sxs-lookup"><span data-stu-id="0c953-111">[Graphical runbooks](automation-runbook-types.md#graphical-runbooks) are not yet supported.</span></span><br><br>
> 
> 

<span data-ttu-id="0c953-112">為您的自動化帳戶設定原始檔控制時，必須執行兩個簡單的步驟，而如果您已經有 GitHub 帳戶，則只需要執行一個步驟。</span><span class="sxs-lookup"><span data-stu-id="0c953-112">There are two simple steps required to configure source control for your Automation account, and only one if you already have a GitHub account.</span></span> <span data-ttu-id="0c953-113">如下：</span><span class="sxs-lookup"><span data-stu-id="0c953-113">They are:</span></span>

## <a name="step-1--create-a-github-repository"></a><span data-ttu-id="0c953-114">步驟 1：建立 GitHub 儲存機制</span><span class="sxs-lookup"><span data-stu-id="0c953-114">Step 1 – Create a GitHub repository</span></span>
<span data-ttu-id="0c953-115">如果您已經有想要連結到 Azure 自動化的 GitHub 帳戶和儲存機制，則登入您現有的帳戶並從下面的步驟 2 開始執行。</span><span class="sxs-lookup"><span data-stu-id="0c953-115">If you already have a GitHub account and a repository that you want to link to Azure Automation, then login to your existing account and start from step 2 below.</span></span> <span data-ttu-id="0c953-116">否則，瀏覽至 [GitHub](https://github.com/)，註冊新的帳戶以及[建立新的儲存機制](https://help.github.com/articles/create-a-repo/)。</span><span class="sxs-lookup"><span data-stu-id="0c953-116">Otherwise, navigate to [GitHub](https://github.com/), sign up for a new account and [create a new repository](https://help.github.com/articles/create-a-repo/).</span></span>

## <a name="step-2--set-up-source-control-in-azure-automation"></a><span data-ttu-id="0c953-117">步驟 2 – 設定 Azure 自動化中的原始檔控制</span><span class="sxs-lookup"><span data-stu-id="0c953-117">Step 2 – Set up source control in Azure Automation</span></span>
1. <span data-ttu-id="0c953-118">從 Azure 入口網站中的 自動化帳戶 刀鋒視窗，按一下  **設定原始檔控制**</span><span class="sxs-lookup"><span data-stu-id="0c953-118">From the Automation Account blade in the Azure portal, click **Set Up Source Control.**</span></span> 
   
    ![設定原始檔控制](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. <span data-ttu-id="0c953-120">[原始檔控制]  刀鋒視窗隨即開啟，您可以在其中設定您的 GitHub 帳戶詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0c953-120">The **Source Control** blade opens, where you can configure your GitHub account details.</span></span> <span data-ttu-id="0c953-121">以下是要設定的參數清單：</span><span class="sxs-lookup"><span data-stu-id="0c953-121">Below is the list of parameters to configure:</span></span>  
   
   | <span data-ttu-id="0c953-122">**參數**</span><span class="sxs-lookup"><span data-stu-id="0c953-122">**Parameter**</span></span> | <span data-ttu-id="0c953-123">**說明**</span><span class="sxs-lookup"><span data-stu-id="0c953-123">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0c953-124">選擇原始檔</span><span class="sxs-lookup"><span data-stu-id="0c953-124">Choose Source</span></span> |<span data-ttu-id="0c953-125">選取原始檔。</span><span class="sxs-lookup"><span data-stu-id="0c953-125">Select the source.</span></span> <span data-ttu-id="0c953-126">目前只支援 **GitHub** 。</span><span class="sxs-lookup"><span data-stu-id="0c953-126">Currently, only **GitHub** is supported.</span></span> |
   | <span data-ttu-id="0c953-127">Authorization</span><span class="sxs-lookup"><span data-stu-id="0c953-127">Authorization</span></span> |<span data-ttu-id="0c953-128">按一下 [授權]  按鈕，授與 GitHub 儲存機制的 Azure 自動化存取權。</span><span class="sxs-lookup"><span data-stu-id="0c953-128">Click the **Authorize** button to grant Azure Automation access to your GitHub repository.</span></span> <span data-ttu-id="0c953-129">如果您已在不同的視窗中登入您的 GitHub 帳戶，則會使用該帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="0c953-129">If you are already logged in to your GitHub account in a different window, then the credentials of that account are used.</span></span> <span data-ttu-id="0c953-130">成功授權之後，刀鋒視窗會在 [授權屬性] 之下顯示您的 GitHub 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0c953-130">Once authorization is successful, the blade will show your GitHub username under **Authorization Property**.</span></span> |
   | <span data-ttu-id="0c953-131">選擇儲存機制</span><span class="sxs-lookup"><span data-stu-id="0c953-131">Choose repository</span></span> |<span data-ttu-id="0c953-132">從可用的儲存機制清單中選取 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0c953-132">Select a GitHub repository from the list of available repositories.</span></span> |
   | <span data-ttu-id="0c953-133">選擇分支</span><span class="sxs-lookup"><span data-stu-id="0c953-133">Choose branch</span></span> |<span data-ttu-id="0c953-134">從可用的分支清單中選取分支。</span><span class="sxs-lookup"><span data-stu-id="0c953-134">Select a branch from the list of available branches.</span></span> <span data-ttu-id="0c953-135">如果您尚未建立任何分支，只會顯示 **master** 分支。</span><span class="sxs-lookup"><span data-stu-id="0c953-135">Only the **master** branch is shown if you haven’t created any branches.</span></span> |
   | <span data-ttu-id="0c953-136">Runbook 資料夾路徑</span><span class="sxs-lookup"><span data-stu-id="0c953-136">Runbook folder path</span></span> |<span data-ttu-id="0c953-137">Runbook 資料夾路徑可指定 GitHub 儲存機制中的路徑，以便您從中推送或提取程式碼。</span><span class="sxs-lookup"><span data-stu-id="0c953-137">The runbook folder path specifies the path in the GitHub repository from which you want to push or pull your code.</span></span> <span data-ttu-id="0c953-138">它必須以 **/foldername/subfoldername**格式輸入。</span><span class="sxs-lookup"><span data-stu-id="0c953-138">It must be entered in the format **/foldername/subfoldername**.</span></span> <span data-ttu-id="0c953-139">只有 Runbook 資料夾路徑中的 Runbook 會同步處理至您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c953-139">Only runbooks in the runbook folder path will be synced to your Automation account.</span></span> <span data-ttu-id="0c953-140">Runbook 資料夾路徑之子資料夾中的 Runbook **不會** 進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="0c953-140">Runbooks in the subfolders of the runbook folder path will **NOT** be synced.</span></span> <span data-ttu-id="0c953-141">使用 **/** 來同步處理儲存機制下的所有 Runbook。</span><span class="sxs-lookup"><span data-stu-id="0c953-141">Use **/** to sync all the runbooks under the repository.</span></span> |
3. <span data-ttu-id="0c953-142">例如，如果您有名為 **PowerShellScripts** 的儲存機制，其中包含名為 **RootFolder** 的資料夾，而該資料夾內含名為 **SubFolder** 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="0c953-142">For example, if you have a repository named **PowerShellScripts** that contains a folder named **RootFolder**, which contains a folder named **SubFolder**.</span></span> <span data-ttu-id="0c953-143">您可以使用下列字串來同步處理每個資料夾層級：</span><span class="sxs-lookup"><span data-stu-id="0c953-143">You can use the following strings to sync each folder level:</span></span>
   
   1. <span data-ttu-id="0c953-144">若要從 **儲存機制**同步處理 Runbook，則 Runbook 資料夾路徑為 */*</span><span class="sxs-lookup"><span data-stu-id="0c953-144">To sync runbooks from **repository**, runbook folder path is */*</span></span>
   2. <span data-ttu-id="0c953-145">若要從 **RootFolder**同步處理 Runbook，則 Runbook 資料夾路徑為 */RootFolder*</span><span class="sxs-lookup"><span data-stu-id="0c953-145">To sync runbooks from **RootFolder**, runbook folder path is */RootFolder*</span></span>
   3. <span data-ttu-id="0c953-146">若要從 **SubFolder**同步處理 Runbook，則 Runbook 資料夾路徑為 */RootFolder/SubFolder*。</span><span class="sxs-lookup"><span data-stu-id="0c953-146">To sync runbooks from **SubFolder**, runbook folder path is */RootFolder/SubFolder*.</span></span>
4. <span data-ttu-id="0c953-147">設定參數之後，它們會顯示在 [設定原始檔控制] </span><span class="sxs-lookup"><span data-stu-id="0c953-147">After you configure the parameters, they are displayed on the **Set Up Source Control blade.**</span></span>  
   
    ![設定刀鋒視窗](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. <span data-ttu-id="0c953-149">按一下 [確定] 後，原始檔控制整合現已針對您的自動化帳戶設定，而且應以您的 GitHub 資訊進行更新。</span><span class="sxs-lookup"><span data-stu-id="0c953-149">Once you click OK, source control integration is now configured for your Automation account and should be updated with your GitHub information.</span></span> <span data-ttu-id="0c953-150">您現在可以按一下此部分來檢視所有原始檔控制同步處理工作歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0c953-150">You can now click on this part to view all of your source control sync job history.</span></span>  
   
    ![儲存機制的值](media/automation-source-control-integration/automation_03_RepoValues.png)
6. <span data-ttu-id="0c953-152">設定原始檔控制之後，將會在您的自動化帳戶中建立下列自動化資源：</span><span class="sxs-lookup"><span data-stu-id="0c953-152">After you set up source control, the following Automation resources will be created in your Automation account:</span></span>  
   <span data-ttu-id="0c953-153">建立兩個[變數資產](automation-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="0c953-153">Two [variable assets](automation-variables.md) are created.</span></span>  
   
   * <span data-ttu-id="0c953-154">**Microsoft.Azure.Automation.SourceControl.Connection** 變數包含連接字串的值，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0c953-154">The variable **Microsoft.Azure.Automation.SourceControl.Connection** contains the values of the connection string, as shown below.</span></span>  
     
     | <span data-ttu-id="0c953-155">**參數**</span><span class="sxs-lookup"><span data-stu-id="0c953-155">**Parameter**</span></span> | <span data-ttu-id="0c953-156">**值**</span><span class="sxs-lookup"><span data-stu-id="0c953-156">**Value**</span></span> |
     |:--- |:--- |
     | <span data-ttu-id="0c953-157">名稱</span><span class="sxs-lookup"><span data-stu-id="0c953-157">Name</span></span> |<span data-ttu-id="0c953-158">Microsoft.Azure.Automation.SourceControl.Connection</span><span class="sxs-lookup"><span data-stu-id="0c953-158">Microsoft.Azure.Automation.SourceControl.Connection</span></span> |
     | <span data-ttu-id="0c953-159">型別</span><span class="sxs-lookup"><span data-stu-id="0c953-159">Type</span></span> |<span data-ttu-id="0c953-160">String</span><span class="sxs-lookup"><span data-stu-id="0c953-160">String</span></span> |
     | <span data-ttu-id="0c953-161">值</span><span class="sxs-lookup"><span data-stu-id="0c953-161">Value</span></span> |<span data-ttu-id="0c953-162">{"Branch":\<您的分支名稱>,"RunbookFolderPath":\<Runbook 資料夾路徑>,"ProviderType":\<GitHub 的值為 1>,"Repository":\<您的儲存機制名稱>,"Username":\<您的 GitHub 使用者名稱>}</span><span class="sxs-lookup"><span data-stu-id="0c953-162">{"Branch":\<*Your branch name*>,"RunbookFolderPath":\<*Runbook folder path*>,"ProviderType":\<*has a value 1 for GitHub*>,"Repository":\<*Name of your repository*>,"Username":\<*Your GitHub user name*>}</span></span> |

    * <span data-ttu-id="0c953-163">**Microsoft.Azure.Automation.SourceControl.OauthToken**變數包含 OAuthToken 的安全加密值。</span><span class="sxs-lookup"><span data-stu-id="0c953-163">The variable **Microsoft.Azure.Automation.SourceControl.OAuthToken**, contains the secure encrypted value of your OAuthToken.</span></span>  

    |<span data-ttu-id="0c953-164">**參數**</span><span class="sxs-lookup"><span data-stu-id="0c953-164">**Parameter**</span></span>            |<span data-ttu-id="0c953-165">**值**</span><span class="sxs-lookup"><span data-stu-id="0c953-165">**Value**</span></span> |
    |:---|:---|
    | <span data-ttu-id="0c953-166">名稱</span><span class="sxs-lookup"><span data-stu-id="0c953-166">Name</span></span>  | <span data-ttu-id="0c953-167">Microsoft.Azure.Automation.SourceControl.OauthToken</span><span class="sxs-lookup"><span data-stu-id="0c953-167">Microsoft.Azure.Automation.SourceControl.OAuthToken</span></span> |
    | <span data-ttu-id="0c953-168">型別</span><span class="sxs-lookup"><span data-stu-id="0c953-168">Type</span></span> | <span data-ttu-id="0c953-169">Unknown(Encrypted)</span><span class="sxs-lookup"><span data-stu-id="0c953-169">Unknown(Encrypted)</span></span> |
    | <span data-ttu-id="0c953-170">值</span><span class="sxs-lookup"><span data-stu-id="0c953-170">Value</span></span> | <span data-ttu-id="0c953-171"><*已加密的 OAuthToken*></span><span class="sxs-lookup"><span data-stu-id="0c953-171"><*Encrypted OAuthToken*></span></span> |  

    ![變數](media/automation-source-control-integration/automation_04_Variables.png)  

    * <span data-ttu-id="0c953-173">**自動化原始檔控制** 已做為已授權的應用程式加入至您的 GitHub 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c953-173">**Automation Source Control** is added as an authorized application to your GitHub account.</span></span> <span data-ttu-id="0c953-174">若要檢視應用程式：從 GitHub 首頁，瀏覽至您的 [設定檔] > [設定] > [應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0c953-174">To view the application: From your GitHub home page, navigate to your **profile** > **Settings** > **Applications**.</span></span> <span data-ttu-id="0c953-175">此應用程式可讓 Azure 自動化將 GitHub 儲存機制同步至自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c953-175">This application allows Azure Automation to sync your GitHub repository to an Automation account.</span></span>  

    ![Git 應用程式](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a><span data-ttu-id="0c953-177">在自動化中使用原始檔控制</span><span class="sxs-lookup"><span data-stu-id="0c953-177">Using Source Control in Automation</span></span>
### <a name="check-in-a-runbook-from-azure-automation-to-source-control"></a><span data-ttu-id="0c953-178">從 Azure 自動化將 Runbook 簽入至原始檔控制</span><span class="sxs-lookup"><span data-stu-id="0c953-178">Check-in a runbook from Azure Automation to source control</span></span>
<span data-ttu-id="0c953-179">Runbook 簽入可讓您將對 Azure 自動化中的 Runbook 所做的變更推送至原始檔控制儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0c953-179">Runbook check-in allows you to push the changes you have made to a runbook in Azure Automation into your source control repository.</span></span> <span data-ttu-id="0c953-180">以下是簽入 Runbook 的步驟：</span><span class="sxs-lookup"><span data-stu-id="0c953-180">Below are the steps to check-in a runbook:</span></span>

1. <span data-ttu-id="0c953-181">從您的自動化帳戶，[建立新的文字 Runbook](automation-first-runbook-textual.md)，或[編輯現有的文字 Runbook](automation-edit-textual-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="0c953-181">From your Automation Account, [create a new textual runbook](automation-first-runbook-textual.md), or [edit an existing, textual runbook](automation-edit-textual-runbook.md).</span></span> <span data-ttu-id="0c953-182">此 Runbook 可以是 PowerShell 工作流程或 PowerShell 指令碼 Runbook。</span><span class="sxs-lookup"><span data-stu-id="0c953-182">This runbook can be either a PowerShell Workflow or a PowerShell script runbook.</span></span>  
2. <span data-ttu-id="0c953-183">編輯 Runbook 之後，加以儲存並按一下 [編輯] 刀鋒視窗中的 [簽入]。</span><span class="sxs-lookup"><span data-stu-id="0c953-183">After you edit your runbook, save it and click **check-in** from the **Edit** blade.</span></span>  
   
    ![簽入按鈕](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > <span data-ttu-id="0c953-185">從 Azure 自動化簽入會覆寫原始檔控制中目前存在的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0c953-185">Check-in from Azure Automation will overwrite the code that currently exists in your source control.</span></span> <span data-ttu-id="0c953-186">要簽入的 Git 對等命令列指示為 **git add + git commit + git push**</span><span class="sxs-lookup"><span data-stu-id="0c953-186">The Git equivalent command line instruction to check-in is **git add + git commit + git push**</span></span>  

1. <span data-ttu-id="0c953-187">當您按一下 [簽入] 時，將會出現一個確認訊息，按一下 [是] 繼續進行。</span><span class="sxs-lookup"><span data-stu-id="0c953-187">When you click **check-in**, you will be prompted with a confirmation message, click yes to continue.</span></span>  
   
    ![簽入訊息](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. <span data-ttu-id="0c953-189">簽入會啟動原始檔控制 Runbook： **Sync-MicrosoftAzureAutomationAccountToGitHubV1**。</span><span class="sxs-lookup"><span data-stu-id="0c953-189">Check-in starts the source control runbook: **Sync-MicrosoftAzureAutomationAccountToGitHubV1**.</span></span> <span data-ttu-id="0c953-190">此 Runbook 會連接到 GitHub 並將 Azure 自動化中的變更推送至您的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0c953-190">This runbook connects to GitHub and pushes changes from Azure Automation to your repository.</span></span> <span data-ttu-id="0c953-191">若要檢視簽入工作歷程記錄，請回到 [原始檔控制整合]  索引標籤，按一下以開啟 [儲存機制同步處理] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0c953-191">To view the check-in job history, go back to the **Source Control Integration** tab and click to open the Repository Synchronization blade.</span></span> <span data-ttu-id="0c953-192">此刀鋒視窗會顯示所有的原始檔控制工作。</span><span class="sxs-lookup"><span data-stu-id="0c953-192">This blade shows all of your source control jobs.</span></span>  <span data-ttu-id="0c953-193">選取您要檢視的工作並按一下以檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0c953-193">Select the job you want to view and click to view the details.</span></span>  
   
    ![簽入 Runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > <span data-ttu-id="0c953-195">原始檔控制 Runbook 是特殊的自動化 Runbook，無法檢視或編輯。</span><span class="sxs-lookup"><span data-stu-id="0c953-195">Source control runbooks are special Automation runbooks that you cannot view or edit.</span></span> <span data-ttu-id="0c953-196">雖然它們不會出現在 Runbook 清單上，但您會看到同步處理工作顯示在您的工作清單。</span><span class="sxs-lookup"><span data-stu-id="0c953-196">While they will not show up on your runbook list, you will see sync jobs showing up on your jobs list.</span></span>
   > 
   > 
3. <span data-ttu-id="0c953-197">修改過的 Runbook 名稱會當作輸入參數傳送至簽入 Runbook。</span><span class="sxs-lookup"><span data-stu-id="0c953-197">The name of the modified runbook is sent as an input parameter to the check-in runbook.</span></span> <span data-ttu-id="0c953-198">在 [儲存機制同步處理] 刀鋒視窗中展開 Runbook，即可[檢視作業詳細資料](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="0c953-198">You can [view the job details](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal) by expanding runbook in **Repository Synchronization** blade.</span></span>  
   
    ![簽入輸入](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. <span data-ttu-id="0c953-200">在工作完成時重新整理您的 GitHub 儲存機制，即可檢視變更。</span><span class="sxs-lookup"><span data-stu-id="0c953-200">Refresh your GitHub repository once the job completes to view the changes.</span></span>  <span data-ttu-id="0c953-201">在您的儲存機制，以認可訊息應該會有認可：**更新*Runbook 名稱*Azure 自動化中。**</span><span class="sxs-lookup"><span data-stu-id="0c953-201">There should be a commit in your repository with a commit message: **Updated *Runbook Name* in Azure Automation.**</span></span>  

### <a name="sync-runbooks-from-source-control-to-azure-automation"></a><span data-ttu-id="0c953-202">將原始檔控制中的 Runbook 同步處理至 Azure 自動化</span><span class="sxs-lookup"><span data-stu-id="0c953-202">Sync runbooks from source control to Azure Automation</span></span>
<span data-ttu-id="0c953-203">[儲存機制同步處理] 刀鋒視窗上的 [同步處理] 按鈕可讓您將儲存機制的 Runbook 資料夾路徑中的所有 Runbook 提取至您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c953-203">The sync button on the Repository Synchronization blade allows you to pull all the runbooks in the runbook folder path of your repository to your Automation account.</span></span> <span data-ttu-id="0c953-204">相同的儲存機制可以同步處理至多個自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="0c953-204">The same repository can be synced to more than one Automation account.</span></span> <span data-ttu-id="0c953-205">以下是同步處理 Runbook 的步驟：</span><span class="sxs-lookup"><span data-stu-id="0c953-205">Below are the steps to sync a runbook:</span></span>

1. <span data-ttu-id="0c953-206">從您設定原始檔控制的自動化帳戶，開啟 [原始檔控制整合/儲存機制同步處理] 刀鋒視窗並按一下 [同步處理]，然後在顯示一則確認訊息時，請按一下 [是] 繼續進行。</span><span class="sxs-lookup"><span data-stu-id="0c953-206">From the Automation account where you set up source control, open the **Source Control Integration/Repository Synchronization blade** and click **Sync** then you will be prompted with a confirmation message, click **Yes** to continue.</span></span>  
   
    ![同步處理按鈕](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. <span data-ttu-id="0c953-208">同步處理會啟動 Runbook： **Sync-MicrosoftAzureAutomationAccountFromGitHubV1**。</span><span class="sxs-lookup"><span data-stu-id="0c953-208">Sync starts the runbook: **Sync-MicrosoftAzureAutomationAccountFromGitHubV1**.</span></span> <span data-ttu-id="0c953-209">此 Runbook 會連接到 GitHub 並將儲存機制中的變更提取至 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="0c953-209">This runbook connects to GitHub and pulls the changes from your repository to Azure Automation.</span></span> <span data-ttu-id="0c953-210">您應該會在此動作的 [儲存機制同步處理]  刀鋒視窗看到新工作。</span><span class="sxs-lookup"><span data-stu-id="0c953-210">You should see a new job on the **Repository Synchronization** blade for this action.</span></span> <span data-ttu-id="0c953-211">若要檢視同步處理工作的詳細資料，按一下以開啟工作詳細資料刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0c953-211">To view details about the sync job, click to open the job details blade.</span></span>  
   
    ![同步處理 Runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > <span data-ttu-id="0c953-213">從原始檔控制進行的同步處理會針對目前在原始檔控制中的 **所有** Runbook，覆寫目前存在於您的自動化帳戶中的 Runbook 草稿版本。</span><span class="sxs-lookup"><span data-stu-id="0c953-213">A sync from source control overwrites the draft version of the runbooks that currently exist in your Automation account for **ALL** runbooks that are currently in source control.</span></span> <span data-ttu-id="0c953-214">要同步處理的 Git 對等命令列指示為 **git pull**</span><span class="sxs-lookup"><span data-stu-id="0c953-214">The Git equivalent command line instruction to sync is **git pull**</span></span>


## <a name="troubleshooting-source-control-problems"></a><span data-ttu-id="0c953-215">原始檔控制問題的疑難排解</span><span class="sxs-lookup"><span data-stu-id="0c953-215">Troubleshooting source control problems</span></span>
<span data-ttu-id="0c953-216">簽入或同步處理工作如有任何錯誤，工作狀態應為 [暫止]，而您可以在工作刀鋒視窗中檢視更多錯誤詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0c953-216">If there are any errors with a check-in or sync job, the job status should be suspended and you can view more details about the error in the job blade.</span></span>  <span data-ttu-id="0c953-217">[所有記錄檔]  部分會顯示與該工作相關聯的所有 PowerShell 串流。</span><span class="sxs-lookup"><span data-stu-id="0c953-217">The **All Logs** part will show you all the PowerShell streams associated with that job.</span></span> <span data-ttu-id="0c953-218">這會提供協助您修正任何簽入或同步處理問題所需的細節。</span><span class="sxs-lookup"><span data-stu-id="0c953-218">This will provide you with the details needed to help you fix any problems with your check-in or sync.</span></span> <span data-ttu-id="0c953-219">它也會顯示同步處理或簽入 Runbook 時發生的動作順序。</span><span class="sxs-lookup"><span data-stu-id="0c953-219">It will also show you the sequence of actions that occurred while syncing or checking-in a runbook.</span></span>  

![AllLogs 映像](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a><span data-ttu-id="0c953-221">中斷原始檔控制的連線</span><span class="sxs-lookup"><span data-stu-id="0c953-221">Disconnecting source control</span></span>
<span data-ttu-id="0c953-222">若要中斷與 GitHub 帳戶的連線，請開啟 [儲存機制同步處理] 刀鋒視窗，然後按一下 [中斷連線] 。</span><span class="sxs-lookup"><span data-stu-id="0c953-222">To disconnect from your GitHub account, open the Repository Synchronization blade and click **Disconnect**.</span></span> <span data-ttu-id="0c953-223">一旦中斷與原始檔控制的連線，先前同步處理的 Runbook 仍會保留在您的自動化帳戶中，但不會啟用 [儲存機制同步處理] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0c953-223">Once you disconnect source control, runbooks that were synced earlier will still remain in your Automation account but the Repository Synchronization blade will not be enabled.</span></span>  

  ![中斷連線按鈕](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a><span data-ttu-id="0c953-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0c953-225">Next steps</span></span>
<span data-ttu-id="0c953-226">如需原始檔控制整合的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="0c953-226">For more information about source control integration, see the following resources:</span></span>  

* [<span data-ttu-id="0c953-227">Azure 自動化：Azure 自動化中的原始檔控制整合</span><span class="sxs-lookup"><span data-stu-id="0c953-227">Azure Automation: Source Control Integration in Azure Automation</span></span>](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [<span data-ttu-id="0c953-228">票選您最喜愛的原始檔控制系統</span><span class="sxs-lookup"><span data-stu-id="0c953-228">Vote for your favorite source control system</span></span>](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [<span data-ttu-id="0c953-229">Azure 自動化：使用 Visual Studio Team Services 整合 Runbook 原始檔控制</span><span class="sxs-lookup"><span data-stu-id="0c953-229">Azure Automation: Integrating Runbook Source Control using Visual Studio Team Services</span></span>](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

