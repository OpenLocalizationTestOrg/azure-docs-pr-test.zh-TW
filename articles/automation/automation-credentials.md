---
title: "Azure 自動化中的認證資產 | Microsoft Docs"
description: "Azure 自動化中的認證資產包含可用來驗證由 Runbook 或 DSC 設定存取資源的安全性認證。 本文說明如何建立認證資產和在 Runbook 或 DSC 設定中使用它們。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: e2857515f3842a875ef7b5a9327392818931168f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="credential-assets-in-azure-automation"></a><span data-ttu-id="68878-104">Azure 自動化中的認證資產</span><span class="sxs-lookup"><span data-stu-id="68878-104">Credential assets in Azure Automation</span></span>
<span data-ttu-id="68878-105">自動化認證資產會保存 [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 物件，其中包含安全性認證，例如使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="68878-105">An Automation credential asset holds a [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential)  object which contains security credentials such as a username and password.</span></span> <span data-ttu-id="68878-106">Runbook 和 DSC 設定可以使用可接受 PSCredential 物件進行驗證的 Cmdlet，否則可能會擷取 PSCredential 物件的使用者名稱和密碼，以對需要驗證的一些應用程式或服務提供。</span><span class="sxs-lookup"><span data-stu-id="68878-106">Runbooks and DSC configurations may use cmdlets that accept a PSCredential object for authentication, or they may extract the username and password of the PSCredential object to provide to some application or service requiring authentication.</span></span> <span data-ttu-id="68878-107">認證的屬性會安全地儲存在 Azure 自動化中，並且可在 Runbook 或 DSC 設定中透過 [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) 活動存取。</span><span class="sxs-lookup"><span data-stu-id="68878-107">The properties for a credential are stored securely in Azure Automation and can be accessed in the runbook or DSC configuration with the [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) activity.</span></span>

> [!NOTE]
> <span data-ttu-id="68878-108">Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。</span><span class="sxs-lookup"><span data-stu-id="68878-108">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="68878-109">這些資產都會經過加密，並使用為每個自動化帳戶產生的唯一索引鍵儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="68878-109">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="68878-110">這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="68878-110">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="68878-111">儲存安全資產之前，會使用主要憑證解密自動化帳戶的金鑰，然後用來加密資產。</span><span class="sxs-lookup"><span data-stu-id="68878-111">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>  

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="68878-112">Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="68878-112">Windows PowerShell cmdlets</span></span>
<span data-ttu-id="68878-113">下表中的 Cmdlet 是用來透過 Windows PowerShell 建立和管理自動化認證資產。</span><span class="sxs-lookup"><span data-stu-id="68878-113">The cmdlets in the following table are used to create and manage automation credential assets with Windows PowerShell.</span></span>  <span data-ttu-id="68878-114">它們是隨著 [Azure PowerShell 模組](/powershell/azure/overview) 的一部分推出，可供在自動化 Runbook 和 DSC 設定中使用。</span><span class="sxs-lookup"><span data-stu-id="68878-114">They ship as part of the [Azure PowerShell module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span></span>

| <span data-ttu-id="68878-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="68878-115">Cmdlets</span></span> | <span data-ttu-id="68878-116">說明</span><span class="sxs-lookup"><span data-stu-id="68878-116">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="68878-117">Get-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="68878-117">Get-AzureAutomationCredential</span></span>](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="68878-118">擷取認證資產的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="68878-118">Retrieves information about a credential asset.</span></span> <span data-ttu-id="68878-119">您只能從 **Get-AutomationPSCredential** 活動擷取認證本身。</span><span class="sxs-lookup"><span data-stu-id="68878-119">You can only retrieve the credential itself from **Get-AutomationPSCredential** activity.</span></span> |
| [<span data-ttu-id="68878-120">New-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="68878-120">New-AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="68878-121">建立新的自動化認證。</span><span class="sxs-lookup"><span data-stu-id="68878-121">Creates a new Automation credential.</span></span> |
| [<span data-ttu-id="68878-122">Remove-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="68878-122">Remove- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="68878-123">移除自動化認證。</span><span class="sxs-lookup"><span data-stu-id="68878-123">Removes an Automation credential.</span></span> |
| [<span data-ttu-id="68878-124">Set-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="68878-124">Set- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="68878-125">設定現有自動化認證的屬性。</span><span class="sxs-lookup"><span data-stu-id="68878-125">Sets the properties for an existing Automation credential.</span></span> |

## <a name="runbook-activities"></a><span data-ttu-id="68878-126">Runbook 活動</span><span class="sxs-lookup"><span data-stu-id="68878-126">Runbook activities</span></span>
<span data-ttu-id="68878-127">下表中的活動用來存取中 Runbook 和 DSC 設定的認證。</span><span class="sxs-lookup"><span data-stu-id="68878-127">The activities in the following table are used to access credentials in a runbook and DSC configurations.</span></span>

| <span data-ttu-id="68878-128">活動</span><span class="sxs-lookup"><span data-stu-id="68878-128">Activities</span></span> | <span data-ttu-id="68878-129">說明</span><span class="sxs-lookup"><span data-stu-id="68878-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="68878-130">Get-AutomationPSCredential</span><span class="sxs-lookup"><span data-stu-id="68878-130">Get-AutomationPSCredential</span></span> |<span data-ttu-id="68878-131">取得要在 Runbook 或 DSC 設定中使用的認證。</span><span class="sxs-lookup"><span data-stu-id="68878-131">Gets a credential to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="68878-132">傳回 [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 物件。</span><span class="sxs-lookup"><span data-stu-id="68878-132">Returns a [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) object.</span></span> |

> [!NOTE]
> <span data-ttu-id="68878-133">您應該避免在 Get-AutomationPSCredential 的 -Name 參數中使用變數，因為這可能會使在設計階段中探索 Runbook 或 DSC 設定與認證資產之間的相依性變得複雜。</span><span class="sxs-lookup"><span data-stu-id="68878-133">You should avoid using variables in the –Name parameter of Get-AutomationPSCredential since this can complicate discovering dependencies between runbooks or DSC configurations, and credential assets at design time.</span></span>
> 
> 

## <a name="creating-a-new-credential-asset"></a><span data-ttu-id="68878-134">建立新的認證資產</span><span class="sxs-lookup"><span data-stu-id="68878-134">Creating a new credential asset</span></span>

### <a name="to-create-a-new-credential-asset-with-the-azure-portal"></a><span data-ttu-id="68878-135">使用 Azure 入口網站建立新的認證資產</span><span class="sxs-lookup"><span data-stu-id="68878-135">To create a new credential asset with the Azure portal</span></span>
1. <span data-ttu-id="68878-136">從您的自動化帳戶，按一下 [資產] 部分，以開啟 [資產] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="68878-136">From your automation account, click the **Assets** part to open the **Assets** blade.</span></span>
2. <span data-ttu-id="68878-137">按一下 [認證] 部分，以開啟 [認證] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="68878-137">Click the **Credentials** part to open the **Credentials** blade.</span></span>
3. <span data-ttu-id="68878-138">在分頁的頂端按一下 [ **加入認證** ]。</span><span class="sxs-lookup"><span data-stu-id="68878-138">Click **Add a credential** at the top of the blade.</span></span>
4. <span data-ttu-id="68878-139">完成表單，然後按一下 [ **建立** ] 以儲存新認證。</span><span class="sxs-lookup"><span data-stu-id="68878-139">Complete the form and click **Create** to save the new credential.</span></span>

### <a name="to-create-a-new-credential-asset-with-windows-powershell"></a><span data-ttu-id="68878-140">使用 Windows PowerShell 建立新的認證資產</span><span class="sxs-lookup"><span data-stu-id="68878-140">To create a new credential asset with Windows PowerShell</span></span>
<span data-ttu-id="68878-141">下列範例命令顯示如何建立新的自動化認證。</span><span class="sxs-lookup"><span data-stu-id="68878-141">The following sample commands show how to create a new automation credential.</span></span> <span data-ttu-id="68878-142">PSCredential 物件是先建立了名稱和密碼，然後用來建立認證資產。</span><span class="sxs-lookup"><span data-stu-id="68878-142">A PSCredential object is first created with the name and password and then used to create the credential asset.</span></span> <span data-ttu-id="68878-143">您也可以使用 **Get-Credential** Cmdlet 來提示您輸入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="68878-143">Alternatively, you could use the **Get-Credential** cmdlet to be prompted to type in a name and password.</span></span>

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="to-create-a-new-credential-asset-with-the-azure-classic-portal"></a><span data-ttu-id="68878-144">使用 Azure 傳統入口網站建立新的認證資產</span><span class="sxs-lookup"><span data-stu-id="68878-144">To create a new credential asset with the Azure classic portal</span></span>
1. <span data-ttu-id="68878-145">從您的自動化帳戶，在視窗的頂端按一下 [ **資產** ]。</span><span class="sxs-lookup"><span data-stu-id="68878-145">From your automation account, click **Assets** at the top of the window.</span></span>
2. <span data-ttu-id="68878-146">在視窗的底端按一下 [ **加入設定**]。</span><span class="sxs-lookup"><span data-stu-id="68878-146">At the bottom of the window, click **Add Setting**.</span></span>
3. <span data-ttu-id="68878-147">按一下 [ **加入認證**]。</span><span class="sxs-lookup"><span data-stu-id="68878-147">Click **Add Credential**.</span></span>
4. <span data-ttu-id="68878-148">在 [認證類型] 下拉式清單中，選取 [PowerShell 認證]。</span><span class="sxs-lookup"><span data-stu-id="68878-148">In the **Credential Type** dropdown, select **PowerShell Credential**.</span></span>
5. <span data-ttu-id="68878-149">完成精靈，然後按一下核取方塊以儲存新認證。</span><span class="sxs-lookup"><span data-stu-id="68878-149">Complete the wizard and click the checkbox to save the new credential.</span></span>

## <a name="using-a-powershell-credential"></a><span data-ttu-id="68878-150">使用 PowerShell 認證</span><span class="sxs-lookup"><span data-stu-id="68878-150">Using a PowerShell credential</span></span>
<span data-ttu-id="68878-151">您會使用 **Get-AutomationPSCredential** 活動在 Runbook 或 DSC 設定中擷取認證資產。</span><span class="sxs-lookup"><span data-stu-id="68878-151">You retrieve a credential asset in a runbook or DSC configuration with the **Get-AutomationPSCredential** activity.</span></span> <span data-ttu-id="68878-152">這會傳回 [PSCredential 物件](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) ，您可以對需要 PSCredential 參數的活動或 Cmdlet 搭配使用此物件。</span><span class="sxs-lookup"><span data-stu-id="68878-152">This returns a [PSCredential object](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) that you can use with an activity or cmdlet that requires a PSCredential parameter.</span></span> <span data-ttu-id="68878-153">您也可以擷取要個別使用的認證物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="68878-153">You can also retrieve the properties of the credential object to use individually.</span></span> <span data-ttu-id="68878-154">物件具備使用者名稱和安全密碼的屬性，或是您可以使用 **GetNetworkCredential** 方法來傳回將提供不安全版本的密碼的 [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) 物件。</span><span class="sxs-lookup"><span data-stu-id="68878-154">The object has a property for the username and the secure password, or you can use the **GetNetworkCredential** method to return a [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) object that will provide an unsecured version of the password.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="68878-155">文字式 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="68878-155">Textual runbook sample</span></span>
<span data-ttu-id="68878-156">下列範例命令顯示如何在 Runbook 中使用 PowerShell 認證。</span><span class="sxs-lookup"><span data-stu-id="68878-156">The following sample commands show how to use a PowerShell credential in a runbook.</span></span> <span data-ttu-id="68878-157">在此範例中，會擷取認證及指派給變數的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="68878-157">In this example, the credential is retrieved and its username and password assigned to variables.</span></span>

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a><span data-ttu-id="68878-158">圖形化 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="68878-158">Graphical runbook sample</span></span>
<span data-ttu-id="68878-159">透過在圖形化編輯器 [文件庫] 窗格的認證上按一下滑鼠右鍵，然後選取 [加入至畫布]，即可將 **Get-AutomationPSCredential** 活動加入至圖形化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="68878-159">You add a **Get-AutomationPSCredential** activity to a graphical runbook by right-clicking on the credential in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![加入認證至畫布](media/automation-credentials/credential-add-canvas.png)

<span data-ttu-id="68878-161">下圖顯示在圖形化 Runbook 中使用認證的範例。</span><span class="sxs-lookup"><span data-stu-id="68878-161">The following image shows an example of using a credential in a graphical runbook.</span></span>  <span data-ttu-id="68878-162">在此情況下，它是用來向 Azure 資源提供 Runbook 的驗證，如 [使用 Azure AD 使用者帳戶驗證 Runbook](automation-create-aduser-account.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="68878-162">In this case, it is being used to provide authentication for a runbook to Azure resources as described in [Authenticate Runbooks with Azure AD User account](automation-create-aduser-account.md).</span></span>  <span data-ttu-id="68878-163">第一個活動會擷取可存取 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="68878-163">The first activity retrieves the credential that has access to the Azure subscription.</span></span>  <span data-ttu-id="68878-164">然後 **Add-AzureAccount** 活動會使用這個認證來為隨後的任何活動提供驗證。</span><span class="sxs-lookup"><span data-stu-id="68878-164">The **Add-AzureAccount** activity then uses this credential to provide authentication for any activities that come after it.</span></span>  <span data-ttu-id="68878-165">因為 [Get-AutomationPSCredential](automation-graphical-authoring-intro.md#links-and-workflow) 需要單一物件，因此推出了 **管線連結** 。</span><span class="sxs-lookup"><span data-stu-id="68878-165">A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is here since **Get-AutomationPSCredential** is expecting a single object.</span></span>  

![加入認證至畫布](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a><span data-ttu-id="68878-167">在 DSC 中使用 PowerShell 認證</span><span class="sxs-lookup"><span data-stu-id="68878-167">Using a PowerShell credential in DSC</span></span>
<span data-ttu-id="68878-168">雖然 Azure 自動化中的 DSC 組態可以使用 **Get-AutomationPSCredential**參考認證資產，但如有需要，也可以透過參數傳入認證資產。</span><span class="sxs-lookup"><span data-stu-id="68878-168">While DSC configurations in Azure Automation can reference credential assets using **Get-AutomationPSCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="68878-169">如需詳細資訊，請參閱 [編譯 Azure Automation DSC 中的設定](automation-dsc-compile.md#credential-assets)。</span><span class="sxs-lookup"><span data-stu-id="68878-169">For more information, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md#credential-assets).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68878-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68878-170">Next Steps</span></span>
* <span data-ttu-id="68878-171">若要深入了解圖形化編寫中的連結，請參閱 [圖形化編寫中的連結](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="68878-171">To learn more about links in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="68878-172">若要了解使用自動化的不同驗證方法，請參閱 [Azure 自動化安全性](automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="68878-172">To understand the different authentication methods with Automation, see [Azure Automation Security](automation-security-overview.md)</span></span>
* <span data-ttu-id="68878-173">若要開始使用圖形化 Runbook，請參閱 [我的第一個圖形化 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="68878-173">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="68878-174">若要開始使用 PowerShell 工作流程 Runbook，請參閱 [我的第一個 PowerShell 工作流程 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="68878-174">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span> 

