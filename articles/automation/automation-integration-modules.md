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
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="02ca2-103">Azure 自動化整合模組</span><span class="sxs-lookup"><span data-stu-id="02ca2-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="02ca2-104">PowerShell 是 hello Azure 自動化背後的基本技術。</span><span class="sxs-lookup"><span data-stu-id="02ca2-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="02ca2-105">因為 Azure 自動化建置在 PowerShell 中，PowerShell 模組是 Azure 自動化的金鑰 toohello 擴充性。</span><span class="sxs-lookup"><span data-stu-id="02ca2-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="02ca2-106">在本文中，我們將引導您的 Azure 自動化 PowerShell 模組使用的 hello 細節、 參考 tooas 「 整合模組 」，並建立您自己確定工作可做為整合模組內的 PowerShell 模組 toomake 的最佳作法Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="02ca2-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="02ca2-107">什麼是 PowerShell 模組？</span><span class="sxs-lookup"><span data-stu-id="02ca2-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="02ca2-108">PowerShell 模組是一組的 PowerShell cmdlet，像是**Get-date**或**Copy-item**，從 hello PowerShell 主控台中，指令碼、 工作流程、 runbook，可以使用 PowerShell DSC 資源如同和WindowsFeature 或檔案，可從 PowerShell DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="02ca2-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="02ca2-109">Hello PowerShell 功能的所有 cmdlet 和 DSC 資源，透過公開和每個 cmdlet/DSC 資源受 PowerShell 模組，其隨附於 PowerShell 本身的許多。</span><span class="sxs-lookup"><span data-stu-id="02ca2-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="02ca2-110">比方說，hello **Get-date** cmdlet 是 hello Microsoft.PowerShell.Utility PowerShell 模組的一部分和**複製項目**cmdlet 是 hello Microsoft.PowerShell.Management PowerShell 模組的一部分，hello 封裝 DSC 資源是 hello PSDesiredStateConfiguration PowerShell 模組的一部分。</span><span class="sxs-lookup"><span data-stu-id="02ca2-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="02ca2-111">以上這兩個模組隨附在 PowerShell 之中。</span><span class="sxs-lookup"><span data-stu-id="02ca2-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="02ca2-112">但許多 PowerShell 模組不寄送過程的 PowerShell，並改為與第一個或第三方產品，像是 System Center 2012 Configuration Manager，或在 PowerShell 資源庫等 hello vast PowerShell 社群所發佈。</span><span class="sxs-lookup"><span data-stu-id="02ca2-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="02ca2-113">hello 模組非常有用，因為它們可讓複雜的工作更簡單，透過封裝功能。</span><span class="sxs-lookup"><span data-stu-id="02ca2-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="02ca2-114">您可以在 MSDN 上深入了解 [PowerShell 模組](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="02ca2-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="02ca2-115">什麼是 Azure 自動化整合模組？</span><span class="sxs-lookup"><span data-stu-id="02ca2-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="02ca2-116">整合模組和 PowerShell 模組的差異不大。</span><span class="sxs-lookup"><span data-stu-id="02ca2-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="02ca2-117">它只是 PowerShell 模組，選擇性地包含一個額外的檔案-指定在 runbook 中的 hello 模組的 cmdlet 搭配使用 Azure 自動化連線類型 toobe 的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="02ca2-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="02ca2-118">選擇性檔案，這些模組可被匯入至 Azure 自動化 toomake 適用於其 cmdlet 的 runbook 和其可用的 DSC 資源中使用 DSC 設定內使用的 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="02ca2-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="02ca2-119">Hello 幕後 Azure 自動化會儲存這些模組中，並在 runbook 工作和 DSC 編譯工作執行時間，載入它們 hello Azure 自動化沙箱其中執行 runbook 而編譯 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="02ca2-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="02ca2-120">在模組中的任何 DSC 資源也會自動會置於 hello 自動化 DSC 提取伺服器，以便它們可以提取機器嘗試 tooapply DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="02ca2-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="02ca2-121">因此您可以開始立即，自動化 Azure 的管理，但是您可以匯入的任何系統、 服務或您想使用 toointegrate 工具 PowerShell 模組，我們隨附您 toouse 針對在 Azure 自動化中的 hello 立即可用的 Azure PowerShell 模組的數目。</span><span class="sxs-lookup"><span data-stu-id="02ca2-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="02ca2-122">某些模組會隨附的 hello 自動化服務中的 「 全域模組 」。</span><span class="sxs-lookup"><span data-stu-id="02ca2-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="02ca2-123">這些全域模組是可用 tooyou 建立自動化帳戶，及我們有時更新它們的自動將它們推送出 tooyour 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="02ca2-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="02ca2-124">如果不想自動更新，您一律可以匯入 toobe hello 相同的模組，並，將會優先於該模組隨附 hello 服務中的 hello 全域模組版本。</span><span class="sxs-lookup"><span data-stu-id="02ca2-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="02ca2-125">您匯入整合模組封裝的 hello 格式為的 hello 相同的名稱，做為 hello 模組以及副檔名為.zip 的壓縮的檔。</span><span class="sxs-lookup"><span data-stu-id="02ca2-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="02ca2-126">它包含 hello Windows PowerShell 模組和任何支援的檔案，包括資訊清單檔案 (.psd1)，如果 hello 模組有一個。</span><span class="sxs-lookup"><span data-stu-id="02ca2-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="02ca2-127">如果 hello 模組都應該包含 Azure 自動化連線類型，則也必須包含 hello 名稱的檔案`<ModuleName>-Automation.json`指定 hello 連線類型屬性。</span><span class="sxs-lookup"><span data-stu-id="02ca2-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="02ca2-128">這是放在 hello 模組資料夾的壓縮的.zip 檔案，在 json 檔案，而且包含 hello 欄位 「 連線 」，不需要的 tooconnect toohello 系統或服務 hello 模組代表。</span><span class="sxs-lookup"><span data-stu-id="02ca2-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="02ca2-129">這最終會在 Azure 自動化中建立連線類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="02ca2-130">使用您可以設定 hello 欄位名稱，此檔案類型，且是否 hello 欄位應該是加密和/或選用 hello 模組的 hello 連接類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="02ca2-131">hello 下面是 hello json 檔案格式中的範本：</span><span class="sxs-lookup"><span data-stu-id="02ca2-131">hello following is a template in hello json file format:</span></span>

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

<span data-ttu-id="02ca2-132">如果您部署 Service Management Automation，並建立自動化 runbook 的整合模組封裝，這應該看起來非常熟悉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="02ca2-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="02ca2-133">撰寫最佳做法</span><span class="sxs-lookup"><span data-stu-id="02ca2-133">Authoring Best Practices</span></span>
<span data-ttu-id="02ca2-134">即使整合模組基本上是 PowerShell 模組，仍建議您撰寫 PowerShell 模組，toomake 時考慮的事項數目最 Azure 自動化中使用它。</span><span class="sxs-lookup"><span data-stu-id="02ca2-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="02ca2-135">其中有些是 Azure 自動化特定，和其中一些會很有用的只是 toomake 您模組中正常運作 PowerShell 工作流程，不論您是否使用自動化。</span><span class="sxs-lookup"><span data-stu-id="02ca2-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="02ca2-136">包含概要說明，並在 hello 模組中的每個 cmdlet 的說明 URI。</span><span class="sxs-lookup"><span data-stu-id="02ca2-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="02ca2-137">在 PowerShell 中，您可以定義特定的說明資訊 cmdlet tooallow hello 使用者 tooreceive 說明使用這些文件以 hello **Get-help** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="02ca2-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="02ca2-138">例如，以下是如何為 .psm1 檔案中所撰寫的 PowerShell 模組定義概要和說明 URI。</span><span class="sxs-lookup"><span data-stu-id="02ca2-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="02ca2-139">提供此資訊不只會顯示此說明使用 hello **Get-help**指令程式在 hello PowerShell 主控台中，它也會公開 （expose） 此 Azure 自動化中的說明功能。</span><span class="sxs-lookup"><span data-stu-id="02ca2-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="02ca2-140">例如，在製作 Runbook 期間插入活動時。</span><span class="sxs-lookup"><span data-stu-id="02ca2-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="02ca2-141">按一下 [檢視詳細的說明] 將另一個索引標籤中的 hello 開啟 hello 說明 URI web 瀏覽器使用 tooaccess Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="02ca2-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="02ca2-142">![整合模組說明](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="02ca2-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="02ca2-143">如果對遠端系統，執行 hello 模組</span><span class="sxs-lookup"><span data-stu-id="02ca2-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="02ca2-144">a.</span><span class="sxs-lookup"><span data-stu-id="02ca2-144">a.</span></span> <span data-ttu-id="02ca2-145">它應該包含定義 hello 所需的資訊 tooconnect toothat 遠端系統，這表示 hello 連接類型的整合模組中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="02ca2-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="02ca2-146">b.</span><span class="sxs-lookup"><span data-stu-id="02ca2-146">b.</span></span> <span data-ttu-id="02ca2-147">Hello 模組中的每個指令程式應該可以 tootake 連接物件 （該連接類型的執行個體） 中做為參數。</span><span class="sxs-lookup"><span data-stu-id="02ca2-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="02ca2-148">Hello 模組中的 Cmdlet 變得更容易 toouse Azure 自動化中的，如果您允許將 hello 欄位 hello 連接類型的物件當作參數 toohello cmdlet 傳遞。</span><span class="sxs-lookup"><span data-stu-id="02ca2-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="02ca2-149">這個方法的使用者沒有 toomap 參數 hello 連線資產 toohello cmdlet 的對應參數的每個時間它們呼叫 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="02ca2-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="02ca2-150">根據上述的 hello runbook 範例，它會使用稱為 CorpTwilio tooaccess Twilio Twilio 連線資產，並傳回 hello 帳戶所有 hello 電話號碼。</span><span class="sxs-lookup"><span data-stu-id="02ca2-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="02ca2-151">請注意如何對應的 hello cmdlet hello 連接 toohello 參數 hello 欄位嗎？</span><span class="sxs-lookup"><span data-stu-id="02ca2-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="02ca2-152">更容易且更好的方式 tooapproach 這會直接傳遞 hello 連線物件 toohello cmdlet-</span><span class="sxs-lookup"><span data-stu-id="02ca2-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="02ca2-153">您可以直接做為參數，而不是參數的連線欄位只允許 tooaccept 連接物件來啟用您 cmdlet 的行為就像這樣。</span><span class="sxs-lookup"><span data-stu-id="02ca2-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="02ca2-154">通常您需要的參數集，可讓使用者不使用 Azure 自動化而無須建構為 hello 連接物件的雜湊表 tooact 呼叫您的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="02ca2-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="02ca2-155">參數集**SpecifyConnectionFields**下面是使用的 toopass hello 連線欄位內容的一個。</span><span class="sxs-lookup"><span data-stu-id="02ca2-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="02ca2-156">**UseConnectionObject**可讓您傳遞 hello 直接透過的連接。</span><span class="sxs-lookup"><span data-stu-id="02ca2-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="02ca2-157">如您所見，hello 傳送 TwilioSMS 指令程式在 hello [Twilio PowerShell 模組](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8)可讓您傳遞兩種：</span><span class="sxs-lookup"><span data-stu-id="02ca2-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="02ca2-158">Hello 模組中定義所有 cmdlet 的輸出的類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="02ca2-159">將輸出類型定義的指令程式可讓設計階段 IntelliSense toohelp 判斷 hello 輸出 hello cmdlet，在撰寫期間使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="02ca2-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="02ca2-160">它是特別有幫助自動化 runbook 圖形化撰寫期間，設計時間知識所在模組的索引鍵 tooan 簡單使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="02ca2-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="02ca2-161">![圖形化 Runbook 輸出類型](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="02ca2-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="02ca2-162">這是類似 toohello 「 類型繼續 」 功能的 cmdlet 的輸出在 PowerShell ISE 中而不需要 toorun 它。</span><span class="sxs-lookup"><span data-stu-id="02ca2-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="02ca2-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="02ca2-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="02ca2-164">Hello 模組中的 Cmdlet 不應該接受參數的複雜物件類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="02ca2-165">PowerShell 工作流程與 PowerShell 的不同之處在於，它會以還原序列化的形式儲存複雜類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="02ca2-166">基本類型將仍維持為基本類型，但是複雜類型轉換的 tootheir 還原序列化的版本中，也就是基本上屬性包。</span><span class="sxs-lookup"><span data-stu-id="02ca2-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="02ca2-167">例如，如果您使用 hello **Get-process** cmdlet 在 runbook （或 PowerShell 工作流程就此而言），它會傳回類型 [Deserialized.System.Diagnostic.Process] 的物件，不 hello 預期的 [System.Diagnostic.Process] 類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="02ca2-168">這個型別都具有所有 hello 相同的屬性，如 hello 非還原序列化的型別，但不會為 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="02ca2-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="02ca2-169">如果您試著 toopass 此值做為參數 tooa cmdlet，其中 hello 指令程式需要 [System.Diagnostic.Process] 值，這個參數，您會收到下列錯誤 hello 和：*無法處理 'process' 參數的引數轉換.錯誤: 「 無法轉換類型 」 Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process"hello"System.Diagnostics.Process (CcmExec) 」 值。*</span><span class="sxs-lookup"><span data-stu-id="02ca2-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="02ca2-170">這是因為沒有 hello 兩者類型不符預期 [System.Diagnostic.Process] 類型，且 hello 指定 [Deserialized.System.Diagnostic.Process] 類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="02ca2-171">解決此問題的 hello 方法是模組的 tooensure hello cmdlet 不接受複雜型別參數。</span><span class="sxs-lookup"><span data-stu-id="02ca2-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="02ca2-172">以下是 hello 錯誤方式 toodo 它。</span><span class="sxs-lookup"><span data-stu-id="02ca2-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="02ca2-173">此外，這裡有 hello 右，納入所 hello 指令程式可以在內部使用基本型別 toograb hello 複雜物件並使用它。</span><span class="sxs-lookup"><span data-stu-id="02ca2-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="02ca2-174">PowerShell hello 內容中執行 cmdlet，因為不 PowerShell 工作流程內 hello cmdlet $process 會變成 hello 正確 [System.Diagnostic.Process] 類型。</span><span class="sxs-lookup"><span data-stu-id="02ca2-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="02ca2-175">在 runbook 中的連線資產雜湊表，也就是複雜類型，而且這些雜湊表尚未似乎 toobe 無法 toobe 傳遞至指令程式針對其 – 連接參數，使用任何轉型例外狀況。</span><span class="sxs-lookup"><span data-stu-id="02ca2-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="02ca2-176">技術上來說，某些 PowerShell 類型是可以正確從其序列化的形式的 tootheir 還原序列化形式，toocast，因此可傳遞至指令程式接受 hello 非還原序列化的型別參數。</span><span class="sxs-lookup"><span data-stu-id="02ca2-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="02ca2-177">雜湊表便是其中之一。</span><span class="sxs-lookup"><span data-stu-id="02ca2-177">Hashtable is one of these.</span></span> <span data-ttu-id="02ca2-178">很可能讓模組作者定義的型別 toobe 它們可以正確還原序列化的方式實作，但有一些缺點 tooconsider。</span><span class="sxs-lookup"><span data-stu-id="02ca2-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="02ca2-179">hello 型別需求 toohave 預設建構函式、 擁有所有的其屬性公開，並且 PSTypeConverter。</span><span class="sxs-lookup"><span data-stu-id="02ca2-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="02ca2-180">不過，對於已定義的類型該 hello 模組作者不擁有沒有不太 「 修正 」 它們，因此 hello 參數一起出現的建議 tooavoid 複雜型別。</span><span class="sxs-lookup"><span data-stu-id="02ca2-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="02ca2-181">Runbook 製作的秘訣： 如果由於某種原因您 cmdlet 需要 tootake 複雜型別參數，或使用其他人的模組需要複雜型別參數，在 PowerShell 工作流程 runbook 中的 hello 因應措施，在本機 PowerShell 工作流程PowerShell 是 toowrap hello cmdlet hello 複雜型別所產生及取用 hello hello 中的複雜類型的 hello cmdlet 相同的 InlineScript 活動。</span><span class="sxs-lookup"><span data-stu-id="02ca2-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="02ca2-182">InlineScript PowerShell 會執行它的內容，而不是 PowerShell 工作流程，hello cmdlet 產生 hello 複雜型別會產生正確類型，因為不 hello 還原序列化複雜型別。</span><span class="sxs-lookup"><span data-stu-id="02ca2-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="02ca2-183">在 hello 模組中的所有 cmdlet 都進行無狀態。</span><span class="sxs-lookup"><span data-stu-id="02ca2-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="02ca2-184">PowerShell 工作流程會執行不同的工作階段呼叫 hello 工作流程中每個 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="02ca2-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="02ca2-185">這表示任何相依於建立 / 修改的 hello 相同模組無法在 PowerShell 工作流程 runbook 中其他指令程式的工作階段狀態的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="02ca2-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="02ca2-186">以下是範例的功能不 toodo。</span><span class="sxs-lookup"><span data-stu-id="02ca2-186">Here is an example of what not toodo.</span></span>
   
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
6. <span data-ttu-id="02ca2-187">hello 模組應該完全包含在 Xcopy 可以封裝中。</span><span class="sxs-lookup"><span data-stu-id="02ca2-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="02ca2-188">因為 Azure 自動化模組是分散式的 toohello 自動化沙箱 runbook 需要 tooexecute 時，他們需要 toowork 獨立 hello 主機執行。</span><span class="sxs-lookup"><span data-stu-id="02ca2-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="02ca2-189">這就表示您應該會無法 tooZip 向上 hello 模組封裝、 將它移 tooany 與其他主機 hello 相同或較新的 PowerShell 版本，並讓它匯入到該主機的 PowerShell 環境時的正常運作。</span><span class="sxs-lookup"><span data-stu-id="02ca2-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="02ca2-190">為了讓該 toohappen，hello 模組相依於 hello 模組資料夾 （hello 資料夾匯入至 Azure 自動化時取得壓縮），以外的任何檔案或不在主機上的任何唯一的登錄設定，例如所設定之 hello 安裝的產品。</span><span class="sxs-lookup"><span data-stu-id="02ca2-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="02ca2-191">如果未遵循此最佳做法，將無法在 Azure 自動化中使用 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="02ca2-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="02ca2-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02ca2-192">Next steps</span></span>

* <span data-ttu-id="02ca2-193">tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="02ca2-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="02ca2-194">toolearn 進一步了解建立 PowerShell 模組，請參閱[撰寫 Windows PowerShell 模組](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="02ca2-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

