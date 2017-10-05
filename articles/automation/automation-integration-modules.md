---
title: "<span data-ttu-id=\"99f71-101\">建立 Azure 自動化整合模組 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"99f71-101\">Create an Azure Automation Integration Module | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"99f71-102\">引導您在 Azure 自動化中建立、測試和舉例使用整合模組的逐步解說教學課程。</span><span class=\"sxs-lookup\"><span data-stu-id=\"99f71-102\">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>"
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
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="99f71-103">Azure 自動化整合模組</span><span class="sxs-lookup"><span data-stu-id="99f71-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="99f71-104">PowerShell 是 Azure 自動化背後的基本技術。</span><span class="sxs-lookup"><span data-stu-id="99f71-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="99f71-105">由於 Azure 自動化的基礎是 PowerShell，PowerShell 模組會是 Azure 自動化的擴充性關鍵。</span><span class="sxs-lookup"><span data-stu-id="99f71-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="99f71-106">本文會引導您了解 Azure 自動化在使用 PowerShell 模組 (稱為「整合模組」) 方面的細節以及用來建立自有 PowerShell 模組的最佳做法，以確保 PowerShell 模組可做為 Azure 自動化內的整合模組。</span><span class="sxs-lookup"><span data-stu-id="99f71-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="99f71-107">什麼是 PowerShell 模組？</span><span class="sxs-lookup"><span data-stu-id="99f71-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="99f71-108">PowerShell 模組是一組 PowerShell Cmdlet (例如 **Get-Date** 或 **Copy-Item**，可透過 PowerShell 主控台、指令碼、工作流程、Runbook 來使用) 和 PowerShell DSC 資源 (例如 WindowsFeature 或檔案，可透過 PowerShell DSC 組態來使用)。</span><span class="sxs-lookup"><span data-stu-id="99f71-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="99f71-109">所有 PowerShell 功能都是透過 Cmdlet 和 DSC 資源來公開，而每個 Cmdlet/DSC 資源都會受到 PowerShell 模組所支援，其中有許多模組會隨附在 PowerShell 本身之中。</span><span class="sxs-lookup"><span data-stu-id="99f71-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="99f71-110">例如，**Get-Date** Cmdlet 是 Microsoft.PowerShell.Utility PowerShell 模組的一部分、**Copy-Item** Cmdlet 是 Microsoft.PowerShell.Management PowerShell 模組的一部分，而「套件 DSC」資源是 PSDesiredStateConfiguration PowerShell 模組的一部分。</span><span class="sxs-lookup"><span data-stu-id="99f71-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="99f71-111">以上這兩個模組隨附在 PowerShell 之中。</span><span class="sxs-lookup"><span data-stu-id="99f71-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="99f71-112">但有許多 PowerShell 模組並未隨附為 PowerShell 的一部分，而是會隨第一方或第三方產品 (例如 System Center 2012 Configuration Manager) 或是透過廣大的 PowerShell 社群 (PowerShell 資源庫之類的地方) 來散發。</span><span class="sxs-lookup"><span data-stu-id="99f71-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="99f71-113">模組非常實用，因為它們能透過封裝起來的功能讓複雜的工作變得簡單。</span><span class="sxs-lookup"><span data-stu-id="99f71-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="99f71-114">您可以在 MSDN 上深入了解 [PowerShell 模組](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx)。</span><span class="sxs-lookup"><span data-stu-id="99f71-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="99f71-115">什麼是 Azure 自動化整合模組？</span><span class="sxs-lookup"><span data-stu-id="99f71-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="99f71-116">整合模組和 PowerShell 模組的差異不大。</span><span class="sxs-lookup"><span data-stu-id="99f71-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="99f71-117">它就是選擇性地多包含一個檔案的 PowerShell 模組，該檔案是一個中繼資料檔案，會指定要與模組在 Runbook 中的 Cmdlet 搭配使用的 Azure 自動化連線類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="99f71-118">不論是否包含選擇性檔案，這些 PowerShell 模組都可以匯入到 Azure 自動化，以使其 Cmdlet 可供在 Runbook 內使用，以及使其 DSC 資源可供在 DSC 組態內使用。</span><span class="sxs-lookup"><span data-stu-id="99f71-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="99f71-119">Azure 自動化會在幕後儲存這些模組，並在執行 Runbook 作業和 DSC 編譯作業時將其載入 Azure 自動化沙箱，以在其中執行 Runbook 和編譯 DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="99f71-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="99f71-120">模組中的任何 DSC 資源也會自動放在 Automation DSC 提取伺服器上，以供嘗試套用 DSC 組態的機器提取。</span><span class="sxs-lookup"><span data-stu-id="99f71-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="99f71-121">我們在 Azure 自動化中隨附了許多現成可用的 Azure PowerShell 模組供您使用，因此您可以立即開始將 Azure 管理自動化，但您也可以針對任何您想要整合的系統、服務或工具匯入 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="99f71-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="99f71-122">某些模組會以自動化服務中的「全域模組 」隨附。</span><span class="sxs-lookup"><span data-stu-id="99f71-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="99f71-123">這些全域模組可在您建立自動化帳戶時使用，而我們有時會更新這些模組，自動將其推送到您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="99f71-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="99f71-124">如果您不想要進行自動更新，您一律可以自行匯入相同的模組，而這將會優先於隨附在服務中該模組的全域模組版本。</span><span class="sxs-lookup"><span data-stu-id="99f71-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="99f71-125">您匯入整合模組封裝時所用的格式為，和模組同名的且副檔名為 .zip 的壓縮檔。</span><span class="sxs-lookup"><span data-stu-id="99f71-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="99f71-126">封裝中含有 Windows PowerShell 模組和任何支援檔案，包括資訊清單檔 (.psd1) (如果模組有此檔的話)。</span><span class="sxs-lookup"><span data-stu-id="99f71-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="99f71-127">如果模組應該包含 Azure 自動化連線類型，則它也必須包含名稱為 `<ModuleName>-Automation.json` 的檔案，以指定連線類型屬性。</span><span class="sxs-lookup"><span data-stu-id="99f71-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="99f71-128">這是放在 .zip 壓縮檔的模組資料夾內的 json 檔案，並包含要連線到模組所代表的系統或服務所必須具有之「連線」的欄位。</span><span class="sxs-lookup"><span data-stu-id="99f71-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="99f71-129">這最終會在 Azure 自動化中建立連線類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="99f71-130">使用此檔案，您就可以為模組的連線類型設定欄位名稱、類型以及欄位是否應該加密和/或選用的。</span><span class="sxs-lookup"><span data-stu-id="99f71-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="99f71-131">以下是使用 json 檔案格式的範本︰</span><span class="sxs-lookup"><span data-stu-id="99f71-131">The following is a template in the json file format:</span></span>

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

<span data-ttu-id="99f71-132">如果您已部署 Service Management Automation 並為自動化 Runbook 建立整合模組封裝，您應該會相當熟悉此範本。</span><span class="sxs-lookup"><span data-stu-id="99f71-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="99f71-133">撰寫最佳做法</span><span class="sxs-lookup"><span data-stu-id="99f71-133">Authoring Best Practices</span></span>
<span data-ttu-id="99f71-134">即使整合模組本來是 PowerShell 模組，當您在撰寫 PowerShell 模組時，我們仍建議您考慮一些事項，以便讓它在 Azure 自動化中發揮最大效用。</span><span class="sxs-lookup"><span data-stu-id="99f71-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="99f71-135">其中有些考慮事項是 Azure 自動化特有的，有些則只適用於讓模組能在 PowerShell 工作流程中良好運作，而不論您是否使用自動化。</span><span class="sxs-lookup"><span data-stu-id="99f71-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="99f71-136">在模組中加入每個 Cmdlet 的概要、描述和說明 URI。</span><span class="sxs-lookup"><span data-stu-id="99f71-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="99f71-137">在 PowerShell 中，您可以為 Cmdlet 定義特定說明資訊，以讓使用者透過 **Get-Help** Cmdlet 獲得其使用說明。</span><span class="sxs-lookup"><span data-stu-id="99f71-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="99f71-138">例如，以下是如何為 .psm1 檔案中所撰寫的 PowerShell 模組定義概要和說明 URI。</span><span class="sxs-lookup"><span data-stu-id="99f71-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="99f71-139">提供此資訊不只能在 PowerShell 主控台中透過 **Get-Help** Cmdlet 來顯示此說明，也會在 Azure 自動化內公開這個說明功能。</span><span class="sxs-lookup"><span data-stu-id="99f71-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="99f71-140">例如，在製作 Runbook 期間插入活動時。</span><span class="sxs-lookup"><span data-stu-id="99f71-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="99f71-141">按一下 [檢視詳細說明]，就會在用來存取 Azure 自動化之 Web 瀏覽器的另一個索引標籤中，開啟說明 URI。</span><span class="sxs-lookup"><span data-stu-id="99f71-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="99f71-142">![整合模組說明](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="99f71-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="99f71-143">如果針對遠端系統來執行模組，</span><span class="sxs-lookup"><span data-stu-id="99f71-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="99f71-144">a.</span><span class="sxs-lookup"><span data-stu-id="99f71-144">a.</span></span> <span data-ttu-id="99f71-145">它應該包含整合模組中繼資料檔案，以定義用來連線到該遠端系統所需的資訊，也就是連線類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="99f71-146">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="99f71-146">b.</span></span> <span data-ttu-id="99f71-147">模組中的每個 Cmdlet 應該要能夠採用連線物件 (該連線類型的執行個體) 來做為參數。</span><span class="sxs-lookup"><span data-stu-id="99f71-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="99f71-148">如果您允許將具有連線類型之欄位的物件，當做參數來傳遞至 Cmdlet，則模組中的 Cmdlet 會變得更容易使用 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="99f71-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="99f71-149">如此一來，使用者就不必在每次呼叫 Cmdlet 時，將連線資產的參數對應至 Cmdlet 的相對應參數。</span><span class="sxs-lookup"><span data-stu-id="99f71-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="99f71-150">根據上述的 Runbook 範例，它使用稱為 CorpTwilio 的 Twilio 連線資產來存取 Twilio，並傳回帳戶中的所有電話號碼。</span><span class="sxs-lookup"><span data-stu-id="99f71-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="99f71-151">請注意它如何將連線的欄位對應至 Cmdlet 的參數？</span><span class="sxs-lookup"><span data-stu-id="99f71-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="99f71-152">更容易且更好的處理方法是直接將連線物件傳遞給 Cmdlet -</span><span class="sxs-lookup"><span data-stu-id="99f71-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="99f71-153">您可以透過讓 Cmdlet 接受直接將連線物件當做參數，而非只是參數的連線欄位，來讓 Cmdlet 具有這樣的行為。</span><span class="sxs-lookup"><span data-stu-id="99f71-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="99f71-154">通常您會想讓每個 Cmdlet 均設定參數，以便未使用 Azure 自動化的使用者可以直接呼叫 Cmdlet，而不必建構雜湊表來做為連線物件。</span><span class="sxs-lookup"><span data-stu-id="99f71-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="99f71-155">下面的參數集 **SpecifyConnectionFields** 可用來逐一傳遞連線欄位屬性。</span><span class="sxs-lookup"><span data-stu-id="99f71-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="99f71-156">**UseConnectionObject** 則可讓您直接傳遞連線。</span><span class="sxs-lookup"><span data-stu-id="99f71-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="99f71-157">如您所見， [Twilio PowerShell 模組](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) 中的 Send-TwilioSMS Cmdlet 允許以任一方式傳遞︰</span><span class="sxs-lookup"><span data-stu-id="99f71-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="99f71-158">為模組中的所有 Cmdlet 定義輸出類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="99f71-159">為 Cmdlet 定義輸出類型，可讓設計階段 IntelliSense 協助您判斷 Cmdlet 的輸出屬性，以供在撰寫期間使用。</span><span class="sxs-lookup"><span data-stu-id="99f71-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="99f71-160">在圖形化撰寫自動化 Runbook 期間，它會特別有幫助，因為設計階段的知識是讓模組的使用者獲得容易使用體驗的關鍵。</span><span class="sxs-lookup"><span data-stu-id="99f71-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="99f71-161">![圖形化 Runbook 輸出類型](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="99f71-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="99f71-162">這類似於 Cmdlet 在 PowerShell ISE 中的輸出的「自動提示」功能，但不需要加以執行。</span><span class="sxs-lookup"><span data-stu-id="99f71-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="99f71-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="99f71-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="99f71-164">模組中的 Cmdlet 不應該採用複雜物件類型來做為參數。</span><span class="sxs-lookup"><span data-stu-id="99f71-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="99f71-165">PowerShell 工作流程與 PowerShell 的不同之處在於，它會以還原序列化的形式儲存複雜類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="99f71-166">基本類型會保持基本，但複雜類型則會轉換為已還原序列化的版本，基本上來說也就是屬性包。</span><span class="sxs-lookup"><span data-stu-id="99f71-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="99f71-167">例如，如果您在 Runbook 使用 **Get-Process** Cmdlet (或任何類似用途的 PowerShell 工作流程)，它會傳回類型為 [Deserialized.System.Diagnostic.Process] 的物件，而非預期的 [System.Diagnostic.Process] 類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="99f71-168">這個類型擁有和非還原序列化類型相同的屬性，但沒有任何方法。</span><span class="sxs-lookup"><span data-stu-id="99f71-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="99f71-169">而且如果您嘗試將此值做為參數傳遞至 Cmdlet，而此 Cmdlet 預期此參數要有 [System.Diagnostic.Process] 值，則您會收到下列錯誤︰「無法處理參數 'process' 的引數轉換。*錯誤：「無法將類型為 "Deserialized.System.Diagnostics.Process" 的 "System.Diagnostics.Process (CcmExec)" 值，轉換為 "System.Diagnostics.Process" 類型。」*</span><span class="sxs-lookup"><span data-stu-id="99f71-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="99f71-170">這是因為預期的 [System.Diagnostic.Process] 類型和給定的 [Deserialized.System.Diagnostic.Process] 類型不相符。</span><span class="sxs-lookup"><span data-stu-id="99f71-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="99f71-171">此問題的解決方式是確保模組的 Cmdlet 不會採用複雜類型來做為參數。</span><span class="sxs-lookup"><span data-stu-id="99f71-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="99f71-172">以下是錯誤的處理方式。</span><span class="sxs-lookup"><span data-stu-id="99f71-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="99f71-173">以下則是正確的方式，採用可由 Cmdlet 在內部使用的原始物件，來捕捉複雜物件並加以使用。</span><span class="sxs-lookup"><span data-stu-id="99f71-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="99f71-174">既然 Cmdlet 會在 PowerShell 環境中執行，而非 PowerShell 工作流程中，因此在 Cmdlet 內，$process 會變成正確的 [System.Diagnostic.Process] 類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="99f71-175">Runbook 中的連線資產是雜湊表，其為複雜類型，然而這些雜湊表似乎可以傳遞給 Cmdlet 供 –Connection 參數完美使用，而不會發生轉換例外狀況。</span><span class="sxs-lookup"><span data-stu-id="99f71-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="99f71-176">技術上來說，某些 PowerShell 類型能夠從其序列化形式正確轉換成還原序列化形式，因此可以傳遞給 Cmdlet 以供接受非還原序列化類型的參數使用。</span><span class="sxs-lookup"><span data-stu-id="99f71-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="99f71-177">雜湊表便是其中之一。</span><span class="sxs-lookup"><span data-stu-id="99f71-177">Hashtable is one of these.</span></span> <span data-ttu-id="99f71-178">模組作者所定義的類型也有可能以可正確還原序列化的方式來實作，但必須考量一些取捨。</span><span class="sxs-lookup"><span data-stu-id="99f71-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="99f71-179">此類型需要有預設建構函式、其所有公用的屬性和 PSTypeConverter。</span><span class="sxs-lookup"><span data-stu-id="99f71-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="99f71-180">不過，對於模組作者未擁有的已定義類型，則沒有辦法加以「修正」，因此才會建議所有參數全都避免使用複雜類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="99f71-181">Runbook 製作提示︰如果 Cmdlet 因為某些原因需要採用複雜類型的參數，或要使用他人需要複雜類型參數的模組，則在 PowerShell 工作流程 Runbook 中和本機 PowerShell 內的 PowerShell 工作流程中，因應措施是將會產生複雜類型的 Cmdlet 和在相同 InlineScript 活動中使用複雜類型的 Cmdlet 包裝起來。</span><span class="sxs-lookup"><span data-stu-id="99f71-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="99f71-182">由於 InlineScript 會以 PowerShell 形式而非 PowerShell 工作流程形式來執行其內容，產生複雜類型 Cmdlet 會產生該正確類型，而不會產生還原序列化的複雜類型。</span><span class="sxs-lookup"><span data-stu-id="99f71-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="99f71-183">讓模組中的所有 Cmdlet 變成無狀態。</span><span class="sxs-lookup"><span data-stu-id="99f71-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="99f71-184">PowerShell 工作流程會在不同工作階段執行工作流程中所呼叫的每個 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="99f71-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="99f71-185">這表示任何相依於同一模組中其他 Cmdlet 所建立/修改的工作階段狀態的 Cmdlet，將不會在 PowerShell 工作流程 Runbook 中運作。</span><span class="sxs-lookup"><span data-stu-id="99f71-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="99f71-186">以下是不該做之事情的範例：</span><span class="sxs-lookup"><span data-stu-id="99f71-186">Here is an example of what not to do.</span></span>
   
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
6. <span data-ttu-id="99f71-187">模組應該完全包含在可 Xcopy 的封裝中。</span><span class="sxs-lookup"><span data-stu-id="99f71-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="99f71-188">當 Runbook 需要執行時，Azure 自動化模組會散發到自動化沙箱中，因此它們需要獨立於其執行所在的主機之外單獨運作。</span><span class="sxs-lookup"><span data-stu-id="99f71-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="99f71-189">其所代表的意義是，您應該能夠壓縮模組封裝，將它移至擁有相同或較新 PowerShell 版本的任何其他主機，並讓它在匯入到該主機的 PowerShell 環境時正常運作。</span><span class="sxs-lookup"><span data-stu-id="99f71-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="99f71-190">為了達成此一情況，模組不應該相依於模組資料夾 (匯入至 Azure 自動化時遭到壓縮的資料夾) 以外的任何檔案，或相依於主機上的任何唯一的登錄設定，例如產品安裝時所設定的登錄設定。</span><span class="sxs-lookup"><span data-stu-id="99f71-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="99f71-191">若未遵循此最佳做法，模組在 Azure 自動化中將無法使用。</span><span class="sxs-lookup"><span data-stu-id="99f71-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="99f71-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99f71-192">Next steps</span></span>

* <span data-ttu-id="99f71-193">若要開始使用 PowerShell 工作流程 Runbook，請參閱 [我的第一個 PowerShell 工作流程 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="99f71-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="99f71-194">若要深入了解如何建立 PowerShell 模組，請參閱 [撰寫 Windows PowerShell 模組](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="99f71-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

