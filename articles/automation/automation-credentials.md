---
title: "在 Azure 自動化中的 aaaCredential 資產 |Microsoft 文件"
description: "在 Azure 自動化認證資產包含可能是使用的 tooauthenticate tooresources hello runbook 或 DSC 設定存取的安全性認證。 本文說明 toocreate 認證資產的方式，並將其用於 runbook 或 DSC 設定。"
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
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a><span data-ttu-id="e01d8-104">Azure 自動化中的認證資產</span><span class="sxs-lookup"><span data-stu-id="e01d8-104">Credential assets in Azure Automation</span></span>
<span data-ttu-id="e01d8-105">自動化認證資產會保存 [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 物件，其中包含安全性認證，例如使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e01d8-105">An Automation credential asset holds a [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential)  object which contains security credentials such as a username and password.</span></span> <span data-ttu-id="e01d8-106">Runbook，而且當 DSC 組態可能使用指令程式可接受 PSCredential 物件，進行驗證，或它們可能會擷取 hello 使用者名稱和密碼的 hello PSCredential 物件 tooprovide toosome 應用程式或服務需要驗證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-106">Runbooks and DSC configurations may use cmdlets that accept a PSCredential object for authentication, or they may extract hello username and password of hello PSCredential object tooprovide toosome application or service requiring authentication.</span></span> <span data-ttu-id="e01d8-107">認證的 hello 屬性會安全地儲存在 Azure 自動化中，而且可以存取在 hello runbook 或以 hello 的 DSC 組態中[Get-automationpscredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx)活動。</span><span class="sxs-lookup"><span data-stu-id="e01d8-107">hello properties for a credential are stored securely in Azure Automation and can be accessed in hello runbook or DSC configuration with hello [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) activity.</span></span>

> [!NOTE]
> <span data-ttu-id="e01d8-108">Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。</span><span class="sxs-lookup"><span data-stu-id="e01d8-108">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="e01d8-109">這些資產都會經過加密並儲存在 hello 使用產生的唯一索引鍵，每個自動化帳戶的 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="e01d8-109">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="e01d8-110">這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="e01d8-110">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="e01d8-111">之前儲存安全資產，hello 自動化帳戶的 hello 金鑰會解密使用 hello 主要憑證，並接著使用 tooencrypt hello 資產。</span><span class="sxs-lookup"><span data-stu-id="e01d8-111">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>  

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="e01d8-112">Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e01d8-112">Windows PowerShell cmdlets</span></span>
<span data-ttu-id="e01d8-113">hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 的自動化認證資產。</span><span class="sxs-lookup"><span data-stu-id="e01d8-113">hello cmdlets in hello following table are used toocreate and manage automation credential assets with Windows PowerShell.</span></span>  <span data-ttu-id="e01d8-114">這些 cmdlet 隨附 hello [Azure PowerShell 模組](/powershell/azure/overview)可用於自動化 runbook 和 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="e01d8-114">They ship as part of hello [Azure PowerShell module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span></span>

| <span data-ttu-id="e01d8-115">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e01d8-115">Cmdlets</span></span> | <span data-ttu-id="e01d8-116">說明</span><span class="sxs-lookup"><span data-stu-id="e01d8-116">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="e01d8-117">Get-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="e01d8-117">Get-AzureAutomationCredential</span></span>](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="e01d8-118">擷取認證資產的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e01d8-118">Retrieves information about a credential asset.</span></span> <span data-ttu-id="e01d8-119">您只能擷取 hello 認證本身從**Get-automationpscredential**活動。</span><span class="sxs-lookup"><span data-stu-id="e01d8-119">You can only retrieve hello credential itself from **Get-AutomationPSCredential** activity.</span></span> |
| [<span data-ttu-id="e01d8-120">New-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="e01d8-120">New-AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="e01d8-121">建立新的自動化認證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-121">Creates a new Automation credential.</span></span> |
| [<span data-ttu-id="e01d8-122">Remove-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="e01d8-122">Remove- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="e01d8-123">移除自動化認證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-123">Removes an Automation credential.</span></span> |
| [<span data-ttu-id="e01d8-124">Set-AzureAutomationCredential</span><span class="sxs-lookup"><span data-stu-id="e01d8-124">Set- AzureAutomationCredential</span></span>](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |<span data-ttu-id="e01d8-125">設定 hello 現有自動化認證的屬性。</span><span class="sxs-lookup"><span data-stu-id="e01d8-125">Sets hello properties for an existing Automation credential.</span></span> |

## <a name="runbook-activities"></a><span data-ttu-id="e01d8-126">Runbook 活動</span><span class="sxs-lookup"><span data-stu-id="e01d8-126">Runbook activities</span></span>
<span data-ttu-id="e01d8-127">hello 下表中的 hello 活動是 runbook 和 DSC 設定中的使用的 tooaccess 認證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-127">hello activities in hello following table are used tooaccess credentials in a runbook and DSC configurations.</span></span>

| <span data-ttu-id="e01d8-128">活動</span><span class="sxs-lookup"><span data-stu-id="e01d8-128">Activities</span></span> | <span data-ttu-id="e01d8-129">說明</span><span class="sxs-lookup"><span data-stu-id="e01d8-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e01d8-130">Get-AutomationPSCredential</span><span class="sxs-lookup"><span data-stu-id="e01d8-130">Get-AutomationPSCredential</span></span> |<span data-ttu-id="e01d8-131">取得認證 toouse runbook 或 DSC 設定中。</span><span class="sxs-lookup"><span data-stu-id="e01d8-131">Gets a credential toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="e01d8-132">傳回 [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) 物件。</span><span class="sxs-lookup"><span data-stu-id="e01d8-132">Returns a [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) object.</span></span> |

> [!NOTE]
> <span data-ttu-id="e01d8-133">您應該避免使用中的變數 hello – Name 參數 Get-automationpscredential 因為這可以使得探索 runbook 或 DSC 設定之間的相依性，並在設計階段認證資產。</span><span class="sxs-lookup"><span data-stu-id="e01d8-133">You should avoid using variables in hello –Name parameter of Get-AutomationPSCredential since this can complicate discovering dependencies between runbooks or DSC configurations, and credential assets at design time.</span></span>
> 
> 

## <a name="creating-a-new-credential-asset"></a><span data-ttu-id="e01d8-134">建立新的認證資產</span><span class="sxs-lookup"><span data-stu-id="e01d8-134">Creating a new credential asset</span></span>

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a><span data-ttu-id="e01d8-135">toocreate hello Azure 入口網站使用新的認證資產</span><span class="sxs-lookup"><span data-stu-id="e01d8-135">toocreate a new credential asset with hello Azure portal</span></span>
1. <span data-ttu-id="e01d8-136">從您的自動化帳戶，按一下 hello**資產**一部分 tooopen hello**資產**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e01d8-136">From your automation account, click hello **Assets** part tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="e01d8-137">按一下 hello**認證**一部分 tooopen hello**認證**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e01d8-137">Click hello **Credentials** part tooopen hello **Credentials** blade.</span></span>
3. <span data-ttu-id="e01d8-138">按一下**新增認證**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="e01d8-138">Click **Add a credential** at hello top of hello blade.</span></span>
4. <span data-ttu-id="e01d8-139">完成 hello 表單，然後按一下**建立**toosave hello 新的認證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-139">Complete hello form and click **Create** toosave hello new credential.</span></span>

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a><span data-ttu-id="e01d8-140">toocreate 使用 Windows PowerShell 的新認證資產</span><span class="sxs-lookup"><span data-stu-id="e01d8-140">toocreate a new credential asset with Windows PowerShell</span></span>
<span data-ttu-id="e01d8-141">hello 下列命令範例示範如何 toocreate 新的自動化認證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-141">hello following sample commands show how toocreate a new automation credential.</span></span> <span data-ttu-id="e01d8-142">PSCredential 物件最初建立 hello 名稱和密碼，而且會用 toocreate hello 認證資產。</span><span class="sxs-lookup"><span data-stu-id="e01d8-142">A PSCredential object is first created with hello name and password and then used toocreate hello credential asset.</span></span> <span data-ttu-id="e01d8-143">或者，您可以使用 hello **Get-credential** cmdlet toobe 提示 tootype 名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e01d8-143">Alternatively, you could use hello **Get-Credential** cmdlet toobe prompted tootype in a name and password.</span></span>

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a><span data-ttu-id="e01d8-144">toocreate hello Azure 傳統入口網站使用新的認證資產</span><span class="sxs-lookup"><span data-stu-id="e01d8-144">toocreate a new credential asset with hello Azure classic portal</span></span>
1. <span data-ttu-id="e01d8-145">從您的自動化帳戶，按一下 **資產**hello hello 視窗上方。</span><span class="sxs-lookup"><span data-stu-id="e01d8-145">From your automation account, click **Assets** at hello top of hello window.</span></span>
2. <span data-ttu-id="e01d8-146">在 hello hello 視窗底部，按一下 **加入設定**。</span><span class="sxs-lookup"><span data-stu-id="e01d8-146">At hello bottom of hello window, click **Add Setting**.</span></span>
3. <span data-ttu-id="e01d8-147">按一下 [ **加入認證**]。</span><span class="sxs-lookup"><span data-stu-id="e01d8-147">Click **Add Credential**.</span></span>
4. <span data-ttu-id="e01d8-148">在 hello**認證類型**下拉式清單中，選取**PowerShell 認證**。</span><span class="sxs-lookup"><span data-stu-id="e01d8-148">In hello **Credential Type** dropdown, select **PowerShell Credential**.</span></span>
5. <span data-ttu-id="e01d8-149">完成 hello 精靈，然後按一下 [hello] 核取方塊 toosave hello 新認證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-149">Complete hello wizard and click hello checkbox toosave hello new credential.</span></span>

## <a name="using-a-powershell-credential"></a><span data-ttu-id="e01d8-150">使用 PowerShell 認證</span><span class="sxs-lookup"><span data-stu-id="e01d8-150">Using a PowerShell credential</span></span>
<span data-ttu-id="e01d8-151">擷取 runbook 或 hello DSC 組態中的認證資產**Get-automationpscredential**活動。</span><span class="sxs-lookup"><span data-stu-id="e01d8-151">You retrieve a credential asset in a runbook or DSC configuration with hello **Get-AutomationPSCredential** activity.</span></span> <span data-ttu-id="e01d8-152">這會傳回 [PSCredential 物件](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) ，您可以對需要 PSCredential 參數的活動或 Cmdlet 搭配使用此物件。</span><span class="sxs-lookup"><span data-stu-id="e01d8-152">This returns a [PSCredential object](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) that you can use with an activity or cmdlet that requires a PSCredential parameter.</span></span> <span data-ttu-id="e01d8-153">您也可以個別擷取 hello 認證物件 toouse hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="e01d8-153">You can also retrieve hello properties of hello credential object toouse individually.</span></span> <span data-ttu-id="e01d8-154">hello 物件 hello 使用者名稱和 hello 安全密碼的屬性，或是您可以使用 hello **GetNetworkCredential**方法 tooreturn [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx)會提供不安全的物件hello 密碼版本。</span><span class="sxs-lookup"><span data-stu-id="e01d8-154">hello object has a property for hello username and hello secure password, or you can use hello **GetNetworkCredential** method tooreturn a [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) object that will provide an unsecured version of hello password.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="e01d8-155">文字式 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="e01d8-155">Textual runbook sample</span></span>
<span data-ttu-id="e01d8-156">hello 下列命令範例示範 toouse PowerShell runbook 中的認證。</span><span class="sxs-lookup"><span data-stu-id="e01d8-156">hello following sample commands show how toouse a PowerShell credential in a runbook.</span></span> <span data-ttu-id="e01d8-157">在此範例中，會擷取 hello 認證，其使用者名稱和密碼指派 toovariables。</span><span class="sxs-lookup"><span data-stu-id="e01d8-157">In this example, hello credential is retrieved and its username and password assigned toovariables.</span></span>

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a><span data-ttu-id="e01d8-158">圖形化 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="e01d8-158">Graphical runbook sample</span></span>
<span data-ttu-id="e01d8-159">您將加入**Get-automationpscredential**活動 tooa 圖形化 runbook 以滑鼠右鍵按一下 hello hello 圖形化編輯器和選取的程式庫 窗格中的 hello 認證**新增 toocanvas**。</span><span class="sxs-lookup"><span data-stu-id="e01d8-159">You add a **Get-AutomationPSCredential** activity tooa graphical runbook by right-clicking on hello credential in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![新增認證 toocanvas](media/automation-credentials/credential-add-canvas.png)

<span data-ttu-id="e01d8-161">hello 下列影像顯示在圖形化 runbook 中使用認證的範例。</span><span class="sxs-lookup"><span data-stu-id="e01d8-161">hello following image shows an example of using a credential in a graphical runbook.</span></span>  <span data-ttu-id="e01d8-162">在此情況下，它正在使用的 tooprovide 驗證 runbook tooAzure 資源中所述[驗證 Azure AD 使用者帳戶的 Runbook](automation-create-aduser-account.md)。</span><span class="sxs-lookup"><span data-stu-id="e01d8-162">In this case, it is being used tooprovide authentication for a runbook tooAzure resources as described in [Authenticate Runbooks with Azure AD User account](automation-create-aduser-account.md).</span></span>  <span data-ttu-id="e01d8-163">hello 第一個活動擷取 hello 認證具有存取 toohello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e01d8-163">hello first activity retrieves hello credential that has access toohello Azure subscription.</span></span>  <span data-ttu-id="e01d8-164">hello **Add-azureaccount**活動接著會使用此認證 tooprovide 驗證針對緊跟在後的任何活動。</span><span class="sxs-lookup"><span data-stu-id="e01d8-164">hello **Add-AzureAccount** activity then uses this credential tooprovide authentication for any activities that come after it.</span></span>  <span data-ttu-id="e01d8-165">因為 [Get-AutomationPSCredential](automation-graphical-authoring-intro.md#links-and-workflow) 需要單一物件，因此推出了 **管線連結** 。</span><span class="sxs-lookup"><span data-stu-id="e01d8-165">A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is here since **Get-AutomationPSCredential** is expecting a single object.</span></span>  

![新增認證 toocanvas](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a><span data-ttu-id="e01d8-167">在 DSC 中使用 PowerShell 認證</span><span class="sxs-lookup"><span data-stu-id="e01d8-167">Using a PowerShell credential in DSC</span></span>
<span data-ttu-id="e01d8-168">雖然 Azure 自動化中的 DSC 組態可以使用 **Get-AutomationPSCredential**參考認證資產，但如有需要，也可以透過參數傳入認證資產。</span><span class="sxs-lookup"><span data-stu-id="e01d8-168">While DSC configurations in Azure Automation can reference credential assets using **Get-AutomationPSCredential**, credential assets can also be passed in via parameters, if desired.</span></span> <span data-ttu-id="e01d8-169">如需詳細資訊，請參閱 [編譯 Azure Automation DSC 中的設定](automation-dsc-compile.md#credential-assets)。</span><span class="sxs-lookup"><span data-stu-id="e01d8-169">For more information, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md#credential-assets).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e01d8-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e01d8-170">Next Steps</span></span>
* <span data-ttu-id="e01d8-171">toolearn 進一步了解連結在圖形化撰寫，請參閱[中圖形化撰寫連結](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="e01d8-171">toolearn more about links in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="e01d8-172">toounderstand hello 不同的驗證方法，使用自動化，請參閱[Azure 自動化的安全性](automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e01d8-172">toounderstand hello different authentication methods with Automation, see [Azure Automation Security](automation-security-overview.md)</span></span>
* <span data-ttu-id="e01d8-173">tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="e01d8-173">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="e01d8-174">tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="e01d8-174">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span> 

