---
title: "常見的 Azure 自動化發出的 aaaTroubleshooting |Microsoft 文件"
description: "本文提供資訊 toohelp 疑難排解和修正常見 Azure 自動化的錯誤。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: "自動化錯誤, 疑難排解, 問題"
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>針對 Azure 自動化中的常見問題進行疑難排解 
本文章提供疑難排解常見的錯誤，您可能會遇到 Azure 自動化中，並建議可能的解決方案 tooresolve 說明它們。

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>使用 Azure 自動化 Runbook 時的驗證錯誤
### <a name="scenario-sign-in-tooazure-account-failed"></a>登入帳戶失敗的 tooAzure 的案例：
**錯誤：** hello Add-azureaccount 或登入 AzureRmAccount cmdlet 使用時，收到 hello 錯誤 「 Unknown_user_type:: 無法辨識使用者類型 」。

**Hello 錯誤的原因：**如果 hello 認證資產名稱不正確，或如果 hello 使用者名稱和您使用 toosetup hello 自動化認證資產的密碼不正確，就會發生這個錯誤。

**疑難排解秘訣：**中順序 toodetermine 錯誤，採取下列步驟的 hello:  

1. 請確定您不需要任何特殊字元，包括 hello  **@** 字元中使用 tooconnect tooAzure hello 自動化認證資產名稱。  
2. 請檢查您可以使用 hello 使用者名稱和密碼儲存在本機 PowerShell ISE 編輯器中的 hello Azure 自動化認證。 您可以執行下列 cmdlet 在 hello PowerShell ISE 中的 hello:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. 如果您的驗證在本機失敗，這表示您尚未正確設定 Azure Active Directory 認證。 請參閱太[驗證使用 Azure Active Directory tooAzure](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/)部落格文章 tooget hello Azure Active Directory 帳戶已正確地設定。  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>案例： 無法 toofind hello Azure 訂用帳戶
**錯誤：**收到 hello 錯誤 「 hello 訂用帳戶命名為``<subscription name>``找不到"hello Select-azuresubscription 或選取 AzureRmSubscription cmdlet 使用時。

**Hello 錯誤的原因：**如果 hello 訂用帳戶名稱無效，或 hello Azure Active Directory 使用者正嘗試 tooget hello 訂用帳戶詳細資料，未設定為 hello 訂用帳戶的系統管理員，就會發生此錯誤。

**疑難排解秘訣：**順序 toodetermine 如果您已正確地驗證 tooAzure 並且有存取 toohello 訂用帳戶正在 tooselect，採取下列步驟的 hello:  

1. 請確定您執行 hello **Add-azureaccount**之前執行 hello **Select-azuresubscription** cmdlet。  
2. 如果您仍發現此錯誤訊息，修改您的程式碼加入 hello **Get-azuresubscription** cmdlet hello **Add-azureaccount**指令程式，然後執行 hello 程式碼。  現在請確認是否 Get-azuresubscription hello 輸出包含您的訂用帳戶詳細資料。  

   * 如果您沒有看到 hello 輸出中的任何訂用帳戶詳細資料，這表示 hello 訂用帳戶不尚未初始化。  
   * 如果您看見 hello 輸出中的 hello 訂用帳戶詳細資料，來確認您使用 hello 正確的訂用帳戶名稱或識別碼以 hello **Select-azuresubscription** cmdlet。   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>案例： 驗證 tooAzure 失敗，因為已啟用多因素驗證
**錯誤：**收到 hello 錯誤 「 Add-azureaccount: AADSTS50079： 增強式驗證註冊 （證明最多） 無須"tooAzure 使用您的 Azure 使用者名稱和密碼進行驗證時。

**Hello 錯誤的原因：**您的 Azure 帳戶上有多重要素驗證，如果您不能使用 Azure Active Directory 使用者 tooauthenticate tooAzure。  相反地，您需要 toouse 憑證或服務主體 tooauthenticate tooAzure。

**疑難排解秘訣：** toouse hello Azure 服務管理 cmdlet 的憑證，請參閱太[建立並加入憑證 toomanage Azure 服務。](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse Azure 資源管理員 cmdlet 的服務主體，請參閱太[建立服務主體使用 Azure 入口網站](../azure-resource-manager/resource-group-create-service-principal-portal.md)和[驗證 Azure 資源管理員與服務主體。](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>使用 Runbook 時的常見錯誤
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>案例： hello runbook 作業開始嘗試三次，但每次失敗 toostart
**錯誤：**在 runbook 失敗，發生 hello 錯誤 「"hello 工作嘗試三次但失敗。 」

**Hello 錯誤的原因：**這個錯誤可能因下列原因 hello:  

1. 記憶體限制。  我們有記載的配置 tooa 沙箱記憶體限制[自動化服務限制](../azure-subscription-service-limits.md#automation-limits)讓作業可能會失敗它正在使用的記憶體超過 400 MB。 

2. 模組不相容。  如果模組相依性不正確，可能會發生這個錯誤；而且不正確時，您的 Runbook 通常會傳回「找不到命令」或「無法繫結參數」訊息。 

**疑難排解秘訣：**任何 hello 下列解決方案就會修正 hello 問題：  

* Hello 記憶體限制內的建議的方法 toowork toosplit hello 工作負載，多個 runbook 之間，不會處理最多的資料在記憶體中，不 toowrite 不必要輸出從您的 runbook，或考慮多少的檢查點寫入至您的 PowerShell工作流程 runbook。  

* 您需要 tooupdate 您的 Azure 模組的 hello 步驟[如何在 Azure 自動化中的 tooupdate Azure PowerShell 模組](automation-update-azure-modules.md)。  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>案例：Runbook 因還原序列化物件而失敗
**錯誤：**在 runbook 失敗，發生 hello 錯誤 「 無法繫結參數``<ParameterName>``。 無法將轉換 hello``<ParameterType>``型別的值 Deserialized ``<ParameterType>`` tootype ``<ParameterType>``"。

**Hello 錯誤的原因：**如果您的 runbook 是 PowerShell 工作流程，它會儲存複雜物件已還原序列化格式中順序 toopersist runbook 狀態如果 hello 工作流程暫止。  

**疑難排解秘訣：**  
任何 hello 下列三個方案會修正此問題：

1. 如果您使用複雜的物件，從一個 cmdlet tooanother，包裝在 InlineScript 中這些 cmdlet。  
2. 將 hello 名稱或值，您必須傳遞從 hello 複雜物件，而不是傳遞 hello 整個物件。  
3. 使用 PowerShell Runbook，而不是 PowerShell 工作流程 Runbook。  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>案例： Runbook 工作失敗，因為 hello 配置超過配額
**錯誤：** runbook 工作失敗，發生 hello 錯誤 「 hello hello 每月作業執行時間總計配額已達到此訂用帳戶 」。

**Hello 錯誤的原因：**時會發生此錯誤 hello 工作執行超過您的帳戶的 hello 500 分鐘可用配額。 這個配額會套用 tooall 工作執行工作，例如測試工作、 從 hello 入口網站中啟動工作、 執行工作所使用 webhook 與排程工作 tooexecute，使用任一 hello Azure 入口網站，或資料中心中的型別。 有關自動化定價的詳細資訊請參閱的 toolearn[自動化定價](https://azure.microsoft.com/pricing/details/automation/)。

**疑難排解秘訣：**如果您想 toouse 超過 500 分鐘的處理每個月您將需要 toochange hello 免費層 toohello 基本層從訂用帳戶。 您可以採取下列步驟 hello 升級 toohello 基本層：  

1. 登入 tooyour Azure 訂用帳戶  
2. 選取您想 tooupgrade hello 自動化帳戶  
3. 按一下 [設定] > [定價層和使用方式] > [定價層]  
4. 在 hello**選擇定價層**刀鋒視窗中，選取**基本**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>案例：執行 Runbook 時，無法辨識 Cmdlet
**錯誤：** runbook 工作失敗，發生 hello 錯誤 「``<cmdlet name>``: hello 詞彙``<cmdlet name>``無法辨識為 cmdlet、 函式、 指令碼檔案或可執行程式 hello 名稱。 」

**Hello 錯誤的原因：** hello PowerShell 引擎找不到您使用您在 runbook 中的 hello cmdlet 時，會造成這個錯誤。  這可能是因為包含 hello cmdlet hello 模組遺漏 hello 帳戶，就會發生名稱衝突的 runbook 名稱，或 hello cmdlet 也存在於另一個模組，自動化無法 hello 名稱解析。

**疑難排解秘訣：**任何 hello 下列解決方案就會修正 hello 問題：  

* 請檢查您所輸入的 hello cmdlet 名稱正確。  
* 請確定您的自動化帳戶中的 hello cmdlet 存在，而且沒有衝突。 tooverify 如果 hello cmdlet，在編輯模式，並搜尋您想要 toofind hello 文件庫中的，或執行 hello cmdlet 中開啟 runbook **Get-command ``<CommandName>``** 。  一旦您已驗證該 hello 指令程式可用 toohello 帳戶並沒有與其他 cmdlet 或 runbook 的名稱衝突將它加入 toohello 畫布，並確認您使用的有效的參數，在您的 runbook 中設定。  
* 如果您沒有名稱衝突，而且 hello 指令程式可以使用兩個不同的模組中，您可以解決此問題使用 hello hello cmdlet 的完整的名稱。 例如，您可以使用 **ModuleName\CmdletName**。  
* 如果您正在執行 hello runbook 在內部部署混合式背景工作群組中，則請確定該 hello hello 裝載 hello 混合式背景工作的電腦上安裝模組/cmdlet。

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>案例： 長時間執行的 runbook 以一致的方式會因 hello 例外狀況:"hello 作業無法繼續執行，因為它已重複收回 hello 從相同的檢查點 」。
**Hello 錯誤的原因：**這是因為 toohello 自動暫停 runbook，如果它超過 3 小時內執行的 Azure 自動化中的程序監視的 「 公平共用 」 的設計行為。 不過，hello 傳回錯誤訊息不會提供 「 哪些下一步 選項。 有許多原因能造成 Runbook 暫停， 暫止發生大部分到期 tooerrors。 例如，runbook、 網路失敗，或在上的損毀的遺漏例外狀況 hello 執行 hello runbook 的 Runbook Worker，將所有導致 hello runbook toobe 暫止並從其最後一個檢查點繼續時啟動。

**疑難排解秘訣：** hello 記載方案 tooavoid toouse 工作流程中的檢查點會出現此情況。  多個參照太 toolearn[學習 PowerShell 工作流程](automation-powershell-workflow.md#checkpoints)。  如需對於「公平共用」及檢查點更詳細的說明，請參閱這篇部落格文章：[在 Runbook 中使用檢查點](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/)。

## <a name="common-errors-when-importing-modules"></a>匯入模組時的常見錯誤
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>案例： 程式模組 tooimport 或 cmdlet 無法匯入後執行
**錯誤：**模組失敗 tooimport 或匯入成功，但沒有 cmdlet 會解壓縮。

**Hello 錯誤的原因：**模組可能未成功匯入的 tooAzure 自動化是一些常見原因如下：  

* hello 結構與 hello 結構不符，自動化需要它 toobe 中的。  
* hello 模組會相依於另一個模組，但尚未部署的 tooyour 自動化帳戶。  
* hello 模組遺漏其 hello 資料夾中的相依性。  
* hello**新增 AzureRmAutomationModule**指令程式正在使用的 tooupload hello 模組，並沒有提供 hello 完整的儲存體路徑，或未載入 hello 模組使用可公開存取的 URL。  

**疑難排解秘訣：**  
任何 hello 下列解決方案就會修正 hello 問題：  

* 請確定該 hello 模組會遵循下列格式的 hello:  
  ModuleName.Zip **->** ModuleName 或版本號碼 **->** (ModuleName.psm1、ModuleName.psd1)
* 開啟 hello.psd1 檔案，並查看 hello 模組是否有任何相依性。  若是如此上, 傳這些模組 toohello 自動化帳戶。  
* 請確定任何參考的.dll 檔都存在 hello 模組資料夾中。  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>使用 Desired State Configuration (DSC) 時的常見錯誤
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>案例：節點處於失敗狀態，並發生「找不到」錯誤
**錯誤：** hello 節點已包含的報表**失敗**狀態和包含 hello 錯誤 「 hello 嘗試 tooget hello 動作，從伺服器 https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction 失敗，因為是有效的組態``<guid>``找不到。 」

**Hello 錯誤的原因：**時發生此錯誤通常 hello 節點被指派 tooa 組態名稱 (例如，ABC)，而不是節點組態名稱 (例如，ABC。網頁伺服器）。  

**疑難排解秘訣：**  

* 請確定您正在指派 hello 節點具有 「 節點組態名稱 」 和不 hello 「 組態名稱 」。  
* 您可以指派使用 Azure 入口網站，或使用 PowerShell cmdlet 的節點組態 tooa 節點。

  * 在排序 tooassign 使用 Azure 入口網站的節點組態 tooa 節點中，開啟 hello **DSC 節點**刀鋒視窗中，然後選取節點，然後按一下 [**指派節點設定**] 按鈕。  
  * 在排序 tooassign 組態 tooa 節點使用 PowerShell cmdlet，請使用**組 AzureRmAutomationDscNode** cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>案例：編譯組態時沒有產生任何節點組態 (MOF 檔案)
**錯誤：** DSC 編譯工作暫停，hello 錯誤: 「 編譯成功完成，但所產生的任何節點組態.mofs 」。

**Hello 錯誤的原因：**當 hello 運算式後面 hello**節點**hello DSC 組態中的關鍵字的評估太 $null，則將不會產生任何節點設定。    

**疑難排解秘訣：**  
任何 hello 下列解決方案就會修正 hello 問題：  

* 請確定該 hello 運算式下一步 toohello**節點**hello 組態定義中的關鍵字不太評估 $null。  
* 如果您要將 ConfigurationData 編譯 hello 組態時，請確定您傳遞 hello 預期的值從需要該 hello 組態[ConfigurationData](automation-dsc-compile.md#configurationdata)。

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>案例： hello DSC 節點之報表會變成困在 「 進行中 」 狀態
**錯誤：** DSC 代理程式輸出「找不到體指定屬性值的執行個體」。

**Hello 錯誤的原因：**您已升級 WMF 版本，並且已損毀的 WMI。  

**疑難排解秘訣：**遵循 hello hello 指示[已知問題和限制的 DSC](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) toofix hello 問題。

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>案例： 無法 toouse DSC 設定中的認證
**錯誤：** DSC 編譯工作暫止 hello 錯誤: 「 System.InvalidOperationException 錯誤處理屬性 「 認證 」 類型的``<some resource name>``： 轉換及儲存加密的密碼時，才允許純文字PSDscAllowPlainTextPassword 設定 tootrue"。

**Hello 錯誤的原因：**您已經在組態中使用認證，但是沒有提供適當**ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue 每個節點組態設定。  

**疑難排解秘訣：**  

* 請確定 toopass 中適當的 hello **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue 每個節點組態 hello 組態中所述。 如需詳細資訊，請參閱太[資產在 Azure Automation DSC](automation-dsc-compile.md#assets)。

## <a name="next-steps"></a>後續步驟
如果您已依照 hello 疑難排解上述步驟，找不到 hello 回應時，您可以檢閱下列的 hello 其他支援選項。

* 取得 Azure 專家協助。 送出問題 toohello [MSDN Azure 或堆疊溢位的論壇。](https://azure.microsoft.com/support/forums/)。
* 提出 Azure 支援事件。 移 toohello [Azure 支援的站台](https://azure.microsoft.com/support/options/)按一下**取得支援**下**技術和帳單支援**。
* 如果您在尋找 Azure 自動化 Runbook 解決方案或整合模組，請在 [指令碼中心](https://azure.microsoft.com/documentation/scripts/) 提出指令碼要求。
* 請在 [User Voice](https://feedback.azure.com/forums/34192--general-feedback)上張貼 Azure 自動化的意見反應或功能要求。
