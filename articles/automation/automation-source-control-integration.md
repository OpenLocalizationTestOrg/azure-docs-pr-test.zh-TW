---
title: "在 Azure 自動化中的控制整合 aaaSource |Microsoft 文件"
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
ms.openlocfilehash: 6ceee1de8065fafe85a13bbd7f585e74dbc96b47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="source-control-integration-in-azure-automation"></a>Azure 自動化中的原始檔控制整合
原始檔控制整合可讓您自動化帳戶 tooa GitHub 原始檔控制儲存機制中的 tooassociate runbook。 原始檔控制可讓您 tooeasily 與您的小組共同作業、 追蹤變更，並回復 tooearlier 版本的 runbook。 例如，原始檔控制可讓您 toosync 不同分支中原始檔控制 tooyour 開發、 測試或實際執行自動化帳戶，讓它已在您開發環境 tooyour 實際執行自動化測試的簡單 toopromote 程式碼帳戶。

原始檔控制可讓您從 Azure 自動化 toosource 控制 toopush 程式碼，或提取您從原始檔控制 tooAzure 自動化的 runbook。 本文說明如何 tooset 來源控制您的 Azure 自動化環境中。 我們將會藉由設定您的 GitHub 儲存機制的 Azure 自動化 tooaccess 啟動，並逐步執行不同的作業，才可以使用原始檔控制整合。 

> [!NOTE]
> 原始檔控制支援提取和推送 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 以及 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks)。 尚未支援[圖形化 Runbook](automation-runbook-types.md#graphical-runbooks)。<br><br>
> 
> 

有兩個簡單的步驟需要的 tooconfigure 原始檔控制，為您的自動化帳戶，而且只有一如果您已經有 GitHub 帳戶。 如下：

## <a name="step-1--create-a-github-repository"></a>步驟 1：建立 GitHub 儲存機制
如果您已經有 GitHub 帳戶和您想要的儲存機制 toolink tooAzure 提供自動化功能，然後登入 tooyour 現有帳戶並開始從步驟 2 的下方。 否則，請瀏覽過[GitHub](https://github.com/)，註冊新帳戶和[建立新的儲存機制](https://help.github.com/articles/create-a-repo/)。

## <a name="step-2--set-up-source-control-in-azure-automation"></a>步驟 2 – 設定 Azure 自動化中的原始檔控制
1. 從 hello 自動化帳戶] 刀鋒視窗 hello Azure 入口網站中，按一下 [**設定原始檔控制。** 
   
    ![設定原始檔控制](media/automation-source-control-integration/automation_01_SetUpSourceControl.png)
2. hello**原始檔控制**刀鋒視窗隨即開啟，您可以在其中設定您的 GitHub 帳戶詳細資料。 以下是參數 tooconfigure hello 清單：  
   
   | **參數** | **說明** |
   |:--- |:--- |
   | 選擇原始檔 |選取 hello 來源。 目前只支援 **GitHub** 。 |
   | Authorization |按一下 hello**授權**按鈕 toogrant Azure 自動化存取 tooyour GitHub 儲存機制。 如果您已經登入 tooyour GitHub 帳戶在不同的視窗中，則 hello 會使用該帳戶的認證。 成功授權之後，hello 刀鋒視窗會顯示您的 GitHub 使用者名稱之下**授權屬性**。 |
   | 選擇儲存機制 |GitHub 儲存機制從 hello 的清單選取可用的儲存機制。 |
   | 選擇分支 |從可用的分支 hello 清單中選取分支。 只有 hello**主要**分支顯示是否您尚未建立任何分支。 |
   | Runbook 資料夾路徑 |hello runbook 的資料夾路徑指定 hello GitHub 儲存機制讓您從中想 toopush 或提取您的程式碼中的 hello 路徑。 它必須輸入 hello 格式**/資料夾名稱/子資料夾名稱**。 只有 hello runbook 資料夾中的 runbook 會同步處理的 tooyour 自動化帳戶。 Hello 的 hello runbook 的資料夾路徑的子資料夾中的 Runbook 將**不**同步。 使用 **/**  toosync 所有 hello 下 hello 儲存機制的 runbook。 |
3. 例如，如果您有名為 **PowerShellScripts** 的儲存機制，其中包含名為 **RootFolder** 的資料夾，而該資料夾內含名為 **SubFolder** 的資料夾。 您可以使用下列字串 toosync hello 每個資料夾層級：
   
   1. 從 toosync runbook**儲存機制**，runbook 的資料夾路徑*/*
   2. 從 toosync runbook **RootFolder**，runbook 的資料夾路徑*/RootFolder*
   3. 從 toosync runbook**子資料夾**，runbook 的資料夾路徑*/RootFolder/子資料夾*。
4. 設定 hello 參數之後，它們會顯示在 [hello**設定原始檔控制] 刀鋒視窗。**  
   
    ![設定刀鋒視窗](media/automation-source-control-integration/automation_02_SourceControlConfigure.png)
5. 按一下 [確定] 後，原始檔控制整合現已針對您的自動化帳戶設定，而且應以您的 GitHub 資訊進行更新。 您現在可以按一下這個組件 tooview 上所有的原始檔控制同步處理作業歷程記錄。  
   
    ![儲存機制的值](media/automation-source-control-integration/automation_03_RepoValues.png)
6. 設定原始檔控制之後，hello 下列的自動化資源將建立您的自動化帳戶中：  
   建立兩個[變數資產](automation-variables.md)。  
   
   * hello 變數**Microsoft.Azure.Automation.SourceControl.Connection**包含 hello hello 連接字串值，如下所示。  
     
     | **參數** | **值** |
     |:--- |:--- |
     | 名稱 |Microsoft.Azure.Automation.SourceControl.Connection |
     | 型別 |String |
     | 值 |{"Branch":\<您的分支名稱>,"RunbookFolderPath":\<Runbook 資料夾路徑>,"ProviderType":\<GitHub 的值為 1>,"Repository":\<您的儲存機制名稱>,"Username":\<您的 GitHub 使用者名稱>} |

    * hello 變數**Microsoft.Azure.Automation.SourceControl.OAuthToken**，包含 hello 安全的加密的值您 OAuthToken。  

    |**參數**            |**值** |
    |:---|:---|
    | 名稱  | Microsoft.Azure.Automation.SourceControl.OauthToken |
    | 型別 | Unknown(Encrypted) |
    | 值 | <*已加密的 OAuthToken*> |  

    ![變數](media/automation-source-control-integration/automation_04_Variables.png)  

    * **自動化原始檔控制**新增為授權的應用程式 tooyour GitHub 帳戶。 tooview hello 應用程式： 從您的 GitHub 首頁上，瀏覽 tooyour**設定檔** > **設定** > **應用程式**。 此應用程式可讓 Azure 自動化 toosync 您 GitHub 儲存機制 tooan 自動化帳戶。  

    ![Git 應用程式](media/automation-source-control-integration/automation_05_GitApplication.png)


## <a name="using-source-control-in-automation"></a>在自動化中使用原始檔控制
### <a name="check-in-a-runbook-from-azure-automation-toosource-control"></a>簽入的 runbook，以從 Azure 自動化 toosource 控制項
Runbook 簽入可讓您 toopush hello 變更 tooa runbook 在 Azure 自動化中到您的原始檔控制儲存機制。 以下是 runbook toocheck 中的 hello 步驟：

1. 從您的自動化帳戶，[建立新的文字 Runbook](automation-first-runbook-textual.md)，或[編輯現有的文字 Runbook](automation-edit-textual-runbook.md)。 此 Runbook 可以是 PowerShell 工作流程或 PowerShell 指令碼 Runbook。  
2. 編輯您的 runbook 之後，請加以儲存，並按一下**簽入**從 hello**編輯**刀鋒視窗。  
   
    ![簽入按鈕](media/automation-source-control-integration/automation_06_CheckinButton.png)

     > [!NOTE] 
     > 簽入來自 Azure 自動化會覆寫目前存在於原始檔控制中的 hello 程式碼。 hello Git toocheck 中的對等的命令列指示是**git 新增 + git 認可 + git 推送**  

1. 當您按一下**簽入**，您將會收到確認訊息提示，請按一下 [是] toocontinue。  
   
    ![簽入訊息](media/automation-source-control-integration/automation_07_CheckinMessage.png)
2. 簽入開始 hello 來源控制 runbook:**同步 MicrosoftAzureAutomationAccountToGitHubV1**。 此 runbook 會連線 tooGitHub，並將變更推入從 Azure 自動化 tooyour 儲存機制。 tooview hello 簽入作業歷程記錄，請回到 toohello**原始檔控制整合**索引標籤上，按一下 [tooopen hello 儲存機制同步處理] 刀鋒視窗。 此刀鋒視窗會顯示所有的原始檔控制工作。  選取您想 tooview，然後按一下 tooview hello 詳細資料的 hello 作業。  
   
    ![簽入 Runbook](media/automation-source-control-integration/automation_08_CheckinRunbook.png)
   
   > [!NOTE]
   > 原始檔控制 Runbook 是特殊的自動化 Runbook，無法檢視或編輯。 雖然它們不會出現在 Runbook 清單上，但您會看到同步處理工作顯示在您的工作清單。
   > 
   > 
3. 做為輸入的參數 toohello 簽入的 runbook，會傳送 hello hello 修改 runbook 名稱。 您可以[檢視 hello 作業詳細資料](automation-runbook-execution.md#viewing-job-status-from-the-azure-portal)展開中的 runbook**儲存機制同步處理**刀鋒視窗。  
   
    ![簽入輸入](media/automation-source-control-integration/automation_09_CheckinInput.png)
4. Hello 作業完成 tooview hello 變更之後，請重新整理您的 GitHub 儲存機制。  在您的儲存機制，以認可訊息應該會有認可：**更新*Runbook 名稱*Azure 自動化中。**  

### <a name="sync-runbooks-from-source-control-tooazure-automation"></a>同步處理從原始檔控制 tooAzure 自動化的 runbook
hello hello 儲存機制同步處理 刀鋒視窗同步處理 按鈕可讓您 toopull 所有 hello hello runbook 資料夾中您的儲存機制 tooyour 自動化帳戶的 runbook。 hello 相同的儲存機制可以是同步處理的 toomore 比一個自動化帳戶。 以下是 runbook hello 步驟 toosync:

1. 從 hello 設定原始檔控制的自動化帳戶，開啟 [hello**原始檔控制儲存機制整合/同步處理] 刀鋒視窗**按一下**同步**則會提示您確認與訊息中，按一下**是**toocontinue。  
   
    ![同步處理按鈕](media/automation-source-control-integration/automation_10_SyncButtonwithMessage.png)
2. 同步處理會啟動 hello:**同步 MicrosoftAzureAutomationAccountFromGitHubV1**。 此 runbook 會連線 tooGitHub，並會從您的儲存機制 tooAzure 自動化 hello 變更中提取。 您應該會看到新的工作上 hello**儲存機制同步處理**刀鋒視窗，這項動作。 tooview 詳細 hello 同步處理作業中，按一下 [tooopen hello 工作詳細資料] 刀鋒視窗。  
   
    ![同步處理 Runbook](media/automation-source-control-integration/automation_11_SyncRunbook.png)

    > [!NOTE] 
    > 從原始檔控制同步處理會覆寫現有的自動化帳戶中的 hello runbook hello 草稿版本**所有**runbook 目前在原始檔控制。 Git 是對等的命令列指令 toosync hello **git 提取**


## <a name="troubleshooting-source-control-problems"></a>原始檔控制問題的疑難排解
如果有任何錯誤的簽入或同步處理工作，應該暫停 hello 工作狀態，您可以在 hello 作業刀鋒視窗中檢視 hello 錯誤詳細。  hello**所有記錄檔**部分將會顯示所有 hello PowerShell 與該工作相關聯的資料流。 這將提供您與 hello 詳細資料所需 toohelp 修正簽入或同步處理的任何問題。它也會顯示您 hello 同步或簽入 runbook 時所發生的動作順序。  

![AllLogs 映像](media/automation-source-control-integration/automation_13_AllLogs.png)

## <a name="disconnecting-source-control"></a>中斷原始檔控制的連線
從您的 GitHub 帳戶 toodisconnect 開啟 hello 儲存機制同步處理] 刀鋒視窗，然後按一下 [**中斷連線**。 一旦您中斷連接原始檔控制，先前已同步處理的 runbook 仍會保留在您的自動化帳戶，但不是會啟用 hello 儲存機制同步處理 刀鋒視窗。  

  ![中斷連線按鈕](media/automation-source-control-integration/automation_12_Disconnect.png)

## <a name="next-steps"></a>後續步驟
如需原始檔控制整合的詳細資訊，請參閱下列資源的 hello:  

* [Azure 自動化：Azure 自動化中的原始檔控制整合](https://azure.microsoft.com/blog/azure-automation-source-control-13/)  
* [票選您最喜愛的原始檔控制系統](https://www.surveymonkey.com/r/?sm=2dVjdcrCPFdT0dFFI8nUdQ%3d%3d)  
* [Azure 自動化：使用 Visual Studio Team Services 整合 Runbook 原始檔控制](https://azure.microsoft.com/blog/azure-automation-integrating-runbook-source-control-using-visual-studio-online/)  

