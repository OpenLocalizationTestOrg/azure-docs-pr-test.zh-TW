---
title: "Azure 自動化整合模組 aaaCreate |Microsoft 文件"
description: "教學課程，將引導您透過 hello 建立、 測試和範例使用在 Azure 自動化中的整合模組。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Azure 自動化整合模組
PowerShell 是 hello Azure 自動化背後的基本技術。 因為 Azure 自動化建置在 PowerShell 中，PowerShell 模組是 Azure 自動化的金鑰 toohello 擴充性。 在本文中，我們將引導您的 Azure 自動化 PowerShell 模組使用的 hello 細節、 參考 tooas 「 整合模組 」，並建立您自己確定工作可做為整合模組內的 PowerShell 模組 toomake 的最佳作法Azure 自動化。 

## <a name="what-is-a-powershell-module"></a>什麼是 PowerShell 模組？
PowerShell 模組是一組的 PowerShell cmdlet，像是**Get-date**或**Copy-item**，從 hello PowerShell 主控台中，指令碼、 工作流程、 runbook，可以使用 PowerShell DSC 資源如同和WindowsFeature 或檔案，可從 PowerShell DSC 設定。 Hello PowerShell 功能的所有 cmdlet 和 DSC 資源，透過公開和每個 cmdlet/DSC 資源受 PowerShell 模組，其隨附於 PowerShell 本身的許多。 比方說，hello **Get-date** cmdlet 是 hello Microsoft.PowerShell.Utility PowerShell 模組的一部分和**複製項目**cmdlet 是 hello Microsoft.PowerShell.Management PowerShell 模組的一部分，hello 封裝 DSC 資源是 hello PSDesiredStateConfiguration PowerShell 模組的一部分。 以上這兩個模組隨附在 PowerShell 之中。 但許多 PowerShell 模組不寄送過程的 PowerShell，並改為與第一個或第三方產品，像是 System Center 2012 Configuration Manager，或在 PowerShell 資源庫等 hello vast PowerShell 社群所發佈。  hello 模組非常有用，因為它們可讓複雜的工作更簡單，透過封裝功能。  您可以在 MSDN 上深入了解 [PowerShell 模組](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx)。 

## <a name="what-is-an-azure-automation-integration-module"></a>什麼是 Azure 自動化整合模組？
整合模組和 PowerShell 模組的差異不大。 它只是 PowerShell 模組，選擇性地包含一個額外的檔案-指定在 runbook 中的 hello 模組的 cmdlet 搭配使用 Azure 自動化連線類型 toobe 的中繼資料檔案。 選擇性檔案，這些模組可被匯入至 Azure 自動化 toomake 適用於其 cmdlet 的 runbook 和其可用的 DSC 資源中使用 DSC 設定內使用的 PowerShell。 Hello 幕後 Azure 自動化會儲存這些模組中，並在 runbook 工作和 DSC 編譯工作執行時間，載入它們 hello Azure 自動化沙箱其中執行 runbook 而編譯 DSC 設定。  在模組中的任何 DSC 資源也會自動會置於 hello 自動化 DSC 提取伺服器，以便它們可以提取機器嘗試 tooapply DSC 設定。  

因此您可以開始立即，自動化 Azure 的管理，但是您可以匯入的任何系統、 服務或您想使用 toointegrate 工具 PowerShell 模組，我們隨附您 toouse 針對在 Azure 自動化中的 hello 立即可用的 Azure PowerShell 模組的數目。 

> [!NOTE]
> 某些模組會隨附的 hello 自動化服務中的 「 全域模組 」。 這些全域模組是可用 tooyou 建立自動化帳戶，及我們有時更新它們的自動將它們推送出 tooyour 自動化帳戶。 如果不想自動更新，您一律可以匯入 toobe hello 相同的模組，並，將會優先於該模組隨附 hello 服務中的 hello 全域模組版本。 

您匯入整合模組封裝的 hello 格式為的 hello 相同的名稱，做為 hello 模組以及副檔名為.zip 的壓縮的檔。 它包含 hello Windows PowerShell 模組和任何支援的檔案，包括資訊清單檔案 (.psd1)，如果 hello 模組有一個。

如果 hello 模組都應該包含 Azure 自動化連線類型，則也必須包含 hello 名稱的檔案`<ModuleName>-Automation.json`指定 hello 連線類型屬性。 這是放在 hello 模組資料夾的壓縮的.zip 檔案，在 json 檔案，而且包含 hello 欄位 「 連線 」，不需要的 tooconnect toohello 系統或服務 hello 模組代表。 這最終會在 Azure 自動化中建立連線類型。 使用您可以設定 hello 欄位名稱，此檔案類型，且是否 hello 欄位應該是加密和/或選用 hello 模組的 hello 連接類型。 hello 下面是 hello json 檔案格式中的範本：

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

如果您部署 Service Management Automation，並建立自動化 runbook 的整合模組封裝，這應該看起來非常熟悉 tooyou。 

## <a name="authoring-best-practices"></a>撰寫最佳做法
即使整合模組基本上是 PowerShell 模組，仍建議您撰寫 PowerShell 模組，toomake 時考慮的事項數目最 Azure 自動化中使用它。 其中有些是 Azure 自動化特定，和其中一些會很有用的只是 toomake 您模組中正常運作 PowerShell 工作流程，不論您是否使用自動化。 

1. 包含概要說明，並在 hello 模組中的每個 cmdlet 的說明 URI。 在 PowerShell 中，您可以定義特定的說明資訊 cmdlet tooallow hello 使用者 tooreceive 說明使用這些文件以 hello **Get-help** cmdlet。 例如，以下是如何為 .psm1 檔案中所撰寫的 PowerShell 模組定義概要和說明 URI。<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> 提供此資訊不只會顯示此說明使用 hello **Get-help**指令程式在 hello PowerShell 主控台中，它也會公開 （expose） 此 Azure 自動化中的說明功能。  例如，在製作 Runbook 期間插入活動時。 按一下 [檢視詳細的說明] 將另一個索引標籤中的 hello 開啟 hello 說明 URI web 瀏覽器使用 tooaccess Azure 自動化。<br>![整合模組說明](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. 如果對遠端系統，執行 hello 模組

    a. 它應該包含定義 hello 所需的資訊 tooconnect toothat 遠端系統，這表示 hello 連接類型的整合模組中繼資料檔案。  
    b. Hello 模組中的每個指令程式應該可以 tootake 連接物件 （該連接類型的執行個體） 中做為參數。  

    Hello 模組中的 Cmdlet 變得更容易 toouse Azure 自動化中的，如果您允許將 hello 欄位 hello 連接類型的物件當作參數 toohello cmdlet 傳遞。 這個方法的使用者沒有 toomap 參數 hello 連線資產 toohello cmdlet 的對應參數的每個時間它們呼叫 cmdlet。 根據上述的 hello runbook 範例，它會使用稱為 CorpTwilio tooaccess Twilio Twilio 連線資產，並傳回 hello 帳戶所有 hello 電話號碼。  請注意如何對應的 hello cmdlet hello 連接 toohello 參數 hello 欄位嗎？<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    更容易且更好的方式 tooapproach 這會直接傳遞 hello 連線物件 toohello cmdlet-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    您可以直接做為參數，而不是參數的連線欄位只允許 tooaccept 連接物件來啟用您 cmdlet 的行為就像這樣。 通常您需要的參數集，可讓使用者不使用 Azure 自動化而無須建構為 hello 連接物件的雜湊表 tooact 呼叫您的 cmdlet。 參數集**SpecifyConnectionFields**下面是使用的 toopass hello 連線欄位內容的一個。 **UseConnectionObject**可讓您傳遞 hello 直接透過的連接。 如您所見，hello 傳送 TwilioSMS 指令程式在 hello [Twilio PowerShell 模組](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8)可讓您傳遞兩種： 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Hello 模組中定義所有 cmdlet 的輸出的類型。 將輸出類型定義的指令程式可讓設計階段 IntelliSense toohelp 判斷 hello 輸出 hello cmdlet，在撰寫期間使用的屬性。 它是特別有幫助自動化 runbook 圖形化撰寫期間，設計時間知識所在模組的索引鍵 tooan 簡單使用者經驗。<br><br> ![圖形化 Runbook 輸出類型](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> 這是類似 toohello 「 類型繼續 」 功能的 cmdlet 的輸出在 PowerShell ISE 中而不需要 toorun 它。<br><br> ![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Hello 模組中的 Cmdlet 不應該接受參數的複雜物件類型。 PowerShell 工作流程與 PowerShell 的不同之處在於，它會以還原序列化的形式儲存複雜類型。 基本類型將仍維持為基本類型，但是複雜類型轉換的 tootheir 還原序列化的版本中，也就是基本上屬性包。 例如，如果您使用 hello **Get-process** cmdlet 在 runbook （或 PowerShell 工作流程就此而言），它會傳回類型 [Deserialized.System.Diagnostic.Process] 的物件，不 hello 預期的 [System.Diagnostic.Process] 類型。 這個型別都具有所有 hello 相同的屬性，如 hello 非還原序列化的型別，但不會為 hello 方法。 如果您試著 toopass 此值做為參數 tooa cmdlet，其中 hello 指令程式需要 [System.Diagnostic.Process] 值，這個參數，您會收到下列錯誤 hello 和：*無法處理 'process' 參數的引數轉換.錯誤: 「 無法轉換類型 」 Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process"hello"System.Diagnostics.Process (CcmExec) 」 值。*   這是因為沒有 hello 兩者類型不符預期 [System.Diagnostic.Process] 類型，且 hello 指定 [Deserialized.System.Diagnostic.Process] 類型。 解決此問題的 hello 方法是模組的 tooensure hello cmdlet 不接受複雜型別參數。 以下是 hello 錯誤方式 toodo 它。
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    此外，這裡有 hello 右，納入所 hello 指令程式可以在內部使用基本型別 toograb hello 複雜物件並使用它。 PowerShell hello 內容中執行 cmdlet，因為不 PowerShell 工作流程內 hello cmdlet $process 會變成 hello 正確 [System.Diagnostic.Process] 類型。  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   在 runbook 中的連線資產雜湊表，也就是複雜類型，而且這些雜湊表尚未似乎 toobe 無法 toobe 傳遞至指令程式針對其 – 連接參數，使用任何轉型例外狀況。 技術上來說，某些 PowerShell 類型是可以正確從其序列化的形式的 tootheir 還原序列化形式，toocast，因此可傳遞至指令程式接受 hello 非還原序列化的型別參數。 雜湊表便是其中之一。 很可能讓模組作者定義的型別 toobe 它們可以正確還原序列化的方式實作，但有一些缺點 tooconsider。 hello 型別需求 toohave 預設建構函式、 擁有所有的其屬性公開，並且 PSTypeConverter。 不過，對於已定義的類型該 hello 模組作者不擁有沒有不太 「 修正 」 它們，因此 hello 參數一起出現的建議 tooavoid 複雜型別。 Runbook 製作的秘訣： 如果由於某種原因您 cmdlet 需要 tootake 複雜型別參數，或使用其他人的模組需要複雜型別參數，在 PowerShell 工作流程 runbook 中的 hello 因應措施，在本機 PowerShell 工作流程PowerShell 是 toowrap hello cmdlet hello 複雜型別所產生及取用 hello hello 中的複雜類型的 hello cmdlet 相同的 InlineScript 活動。 InlineScript PowerShell 會執行它的內容，而不是 PowerShell 工作流程，hello cmdlet 產生 hello 複雜型別會產生正確類型，因為不 hello 還原序列化複雜型別。
5. 在 hello 模組中的所有 cmdlet 都進行無狀態。 PowerShell 工作流程會執行不同的工作階段呼叫 hello 工作流程中每個 cmdlet。 這表示任何相依於建立 / 修改的 hello 相同模組無法在 PowerShell 工作流程 runbook 中其他指令程式的工作階段狀態的 cmdlet。  以下是範例的功能不 toodo。
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. hello 模組應該完全包含在 Xcopy 可以封裝中。 因為 Azure 自動化模組是分散式的 toohello 自動化沙箱 runbook 需要 tooexecute 時，他們需要 toowork 獨立 hello 主機執行。 這就表示您應該會無法 tooZip 向上 hello 模組封裝、 將它移 tooany 與其他主機 hello 相同或較新的 PowerShell 版本，並讓它匯入到該主機的 PowerShell 環境時的正常運作。 為了讓該 toohappen，hello 模組相依於 hello 模組資料夾 （hello 資料夾匯入至 Azure 自動化時取得壓縮），以外的任何檔案或不在主機上的任何唯一的登錄設定，例如所設定之 hello 安裝的產品。 如果未遵循此最佳做法，將無法在 Azure 自動化中使用 hello 模組。  

## <a name="next-steps"></a>後續步驟

* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)
* toolearn 進一步了解建立 PowerShell 模組，請參閱[撰寫 Windows PowerShell 模組](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

