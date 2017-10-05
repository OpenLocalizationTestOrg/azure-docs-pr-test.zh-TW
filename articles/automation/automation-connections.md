---
title: "Azure 自動化中的連接資產 |Microsoft Docs"
description: "Azure 自動化中的連接資產包含從 Runbook 或 DSC 設定連接到外部服務或應用程式所需的資訊。 這篇文章說明連接的詳細資料，以及如何以文字和圖形化編寫形式加以使用。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: 3cf85651332c85ddf7ef26c21619b5e3a0b89b79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connection-assets-in-azure-automation"></a><span data-ttu-id="c889c-104">Azure 自動化中的連接資產</span><span class="sxs-lookup"><span data-stu-id="c889c-104">Connection assets in Azure Automation</span></span>

<span data-ttu-id="c889c-105">自動化連接資產包含從 Runbook 或 DSC 設定連接到外部服務或應用程式所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="c889c-105">An Automation connection asset contains the information required to connect to an external service or application from a runbook or DSC configuration.</span></span> <span data-ttu-id="c889c-106">除了連接資訊，例如 URL 或連接埠等，這可能包括驗證所需的資訊，例如使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c889c-106">This may include information required for authentication such as a username and password in addition to connection information such as a URL or a port.</span></span> <span data-ttu-id="c889c-107">連接的值會將連接到特定應用程式的所有屬性放在一個資產中，而不是建立多個變數。</span><span class="sxs-lookup"><span data-stu-id="c889c-107">The value of a connection is keeping all of the properties for connecting to a particular application in one asset as opposed to creating multiple variables.</span></span> <span data-ttu-id="c889c-108">使用者可以在一個地方編輯連接的值，而您可以將連接的名稱在單一參數中傳遞至 Runbook 或 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="c889c-108">The user can edit the values for a connection in one place, and you can pass the name of a connection to a runbook or DSC configuration in a single parameter.</span></span> <span data-ttu-id="c889c-109">可以在 Runbook 或 DSC 設定中使用 **Get-AutomationConnection** 活動存取連接的屬性。</span><span class="sxs-lookup"><span data-stu-id="c889c-109">The properties for a connection can be accessed in the runbook or DSC configuration with the **Get-AutomationConnection** activity.</span></span>

<span data-ttu-id="c889c-110">建立連接時，您必須指定 *連接類型*。</span><span class="sxs-lookup"><span data-stu-id="c889c-110">When you create a connection, you must specify a *connection type*.</span></span> <span data-ttu-id="c889c-111">連接類型是定義一組屬性的範本。</span><span class="sxs-lookup"><span data-stu-id="c889c-111">The connection type is a template that defines a set of properties.</span></span> <span data-ttu-id="c889c-112">連接會定義在其連接類型中定義的每一個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="c889c-112">The connection defines values for each property defined in its connection type.</span></span> <span data-ttu-id="c889c-113">如果整合模組包含連線類型，且已匯入您的自動化帳戶，連線類型是在整合模組中加入 Azure 自動化或使用 [Azure 自動化 API](http://msdn.microsoft.com/library/azure/mt163818.aspx)建立。</span><span class="sxs-lookup"><span data-stu-id="c889c-113">Connection types are added to Azure Automation in integration modules or created with the [Azure Automation API](http://msdn.microsoft.com/library/azure/mt163818.aspx) if the integration module includes a connection type and is imported into your Automation account.</span></span> <span data-ttu-id="c889c-114">否則，您必須建立中繼資料檔案來指定自動化連線類型。</span><span class="sxs-lookup"><span data-stu-id="c889c-114">Otherwise, you will need to create a metadata file to specify an Automation connection type.</span></span>  <span data-ttu-id="c889c-115">如需有關於此的進一步資訊，請參閱[整合模組](automation-integration-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="c889c-115">For further information regarding this, see [Integration Modules](automation-integration-modules.md).</span></span>  

>[!NOTE] 
><span data-ttu-id="c889c-116">Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。</span><span class="sxs-lookup"><span data-stu-id="c889c-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="c889c-117">這些資產都會經過加密，並使用為每個自動化帳戶產生的唯一索引鍵儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="c889c-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="c889c-118">這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="c889c-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="c889c-119">儲存安全資產之前，會使用主要憑證解密自動化帳戶的金鑰，然後用來加密資產。</span><span class="sxs-lookup"><span data-stu-id="c889c-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="c889c-120">Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="c889c-120">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="c889c-121">下表中的 Cmdlet 是用來使用 Windows PowerShell 建立和管理自動化連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-121">The cmdlets in the following table are used to create and manage Automation connections with Windows PowerShell.</span></span> <span data-ttu-id="c889c-122">它們是隨著 [Azure PowerShell 模組](/powershell/azure/overview) 的一部分推出，可供在自動化 Runbook 和 DSC 設定中使用。</span><span class="sxs-lookup"><span data-stu-id="c889c-122">They ship as part of the [Azure PowerShell module](/powershell/azure/overview) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="c889c-123">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="c889c-123">Cmdlet</span></span>|<span data-ttu-id="c889c-124">說明</span><span class="sxs-lookup"><span data-stu-id="c889c-124">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="c889c-125">Get-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="c889c-125">Get-AzureRmAutomationConnection</span></span>](/powershell/module/azurerm.automation/get-azurermautomationconnection)|<span data-ttu-id="c889c-126">擷取連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-126">Retrieves a connection.</span></span> <span data-ttu-id="c889c-127">包含具有連接欄位值的雜湊表。</span><span class="sxs-lookup"><span data-stu-id="c889c-127">Includes a hash table with the values of the connection’s fields.</span></span>|
|[<span data-ttu-id="c889c-128">New-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="c889c-128">New-AzureRmAutomationConnection</span></span>](/powershell/module/azurerm.automation/new-azurermautomationconnection)|<span data-ttu-id="c889c-129">建立新連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-129">Creates a new connection.</span></span>|
|[<span data-ttu-id="c889c-130">Remove-AzureRmAutomationConnection</span><span class="sxs-lookup"><span data-stu-id="c889c-130">Remove-AzureRmAutomationConnection</span></span>](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|<span data-ttu-id="c889c-131">移除現有的連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-131">Remove an existing connection.</span></span>|
|[<span data-ttu-id="c889c-132">Set-AzureRmAutomationConnectionFieldValue</span><span class="sxs-lookup"><span data-stu-id="c889c-132">Set-AzureRmAutomationConnectionFieldValue</span></span>](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|<span data-ttu-id="c889c-133">設定現有連接的特定欄位的值。</span><span class="sxs-lookup"><span data-stu-id="c889c-133">Sets the value of a particular field for an existing connection.</span></span>|

## <a name="activities"></a><span data-ttu-id="c889c-134">活動</span><span class="sxs-lookup"><span data-stu-id="c889c-134">Activities</span></span>

<span data-ttu-id="c889c-135">下表中的活動是用來存取 Runbook 或 DSC 設定中的連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-135">The activities in the following table are used to access connections in a runbook or DSC configuration.</span></span>

|<span data-ttu-id="c889c-136">活動</span><span class="sxs-lookup"><span data-stu-id="c889c-136">Activities</span></span>|<span data-ttu-id="c889c-137">說明</span><span class="sxs-lookup"><span data-stu-id="c889c-137">Description</span></span>|
|---|---|
|[<span data-ttu-id="c889c-138">Get-AutomationConnection</span><span class="sxs-lookup"><span data-stu-id="c889c-138">Get-AutomationConnection</span></span>](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|<span data-ttu-id="c889c-139">取得要使用的連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-139">Gets a connection to use.</span></span> <span data-ttu-id="c889c-140">傳回具有連線屬性的雜湊表。</span><span class="sxs-lookup"><span data-stu-id="c889c-140">Returns a hash table with the properties of the connection.</span></span>|

>[!NOTE] 
><span data-ttu-id="c889c-141">您應該避免在 **Get-AutomationConnection** 的 -Name 參數使用變數，因為這可能會使在設計階段中探索 Runbook 或 DSC 設定與連接資產之間的相依性變得複雜。</span><span class="sxs-lookup"><span data-stu-id="c889c-141">You should avoid using variables with the –Name parameter of **Get- AutomationConnection** since this can complicate discovering dependencies between runbooks or DSC configurations, and connection assets at design time.</span></span>

## <a name="creating-a-new-connection"></a><span data-ttu-id="c889c-142">建立新連接</span><span class="sxs-lookup"><span data-stu-id="c889c-142">Creating a New Connection</span></span>

### <a name="to-create-a-new-connection-with-the-azure-portal"></a><span data-ttu-id="c889c-143">使用 Azure 入口網站建立新的連接</span><span class="sxs-lookup"><span data-stu-id="c889c-143">To create a new connection with the Azure portal</span></span>

1. <span data-ttu-id="c889c-144">從您的自動化帳戶，按一下 [資產] 部分，以開啟 [資產] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c889c-144">From your automation account, click the **Assets** part to open the **Assets** blade.</span></span>
2. <span data-ttu-id="c889c-145">按一下 [連接] 部分，以開啟 [連接] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c889c-145">Click the **Connections** part to open the **Connections** blade.</span></span>
3. <span data-ttu-id="c889c-146">在分頁的頂端按一下 [ **加入連接** ]。</span><span class="sxs-lookup"><span data-stu-id="c889c-146">Click **Add a connection** at the top of the blade.</span></span>
4. <span data-ttu-id="c889c-147">在 [ **類型** ] 下拉式清單中，選取您想要建立的連接類型。</span><span class="sxs-lookup"><span data-stu-id="c889c-147">In the **Type** dropdown, select the type of connection you want to create.</span></span> <span data-ttu-id="c889c-148">表單會顯示該特定類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="c889c-148">The form will present the properties for that particular type.</span></span>
5. <span data-ttu-id="c889c-149">完成表單，然後按一下 [ **建立** ] 以儲存新連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-149">Complete the form and click **Create** to save the new connection.</span></span>

### <a name="to-create-a-new-connection-with-the-azure-classic-portal"></a><span data-ttu-id="c889c-150">使用 Azure 傳統入口網站建立新連接</span><span class="sxs-lookup"><span data-stu-id="c889c-150">To create a new connection with the Azure classic portal</span></span>

1. <span data-ttu-id="c889c-151">從您的自動化帳戶，在視窗的頂端按一下 [ **資產** ]。</span><span class="sxs-lookup"><span data-stu-id="c889c-151">From your automation account, click **Assets** at the top of the window.</span></span>
2. <span data-ttu-id="c889c-152">在視窗的底端按一下 [ **加入設定**]。</span><span class="sxs-lookup"><span data-stu-id="c889c-152">At the bottom of the window, click **Add Setting**.</span></span>
3. <span data-ttu-id="c889c-153">按一下 [ **加入連接**]。</span><span class="sxs-lookup"><span data-stu-id="c889c-153">Click **Add Connection**.</span></span>
4. <span data-ttu-id="c889c-154">在 [ **連接類型** ] 下拉式清單中，選取您想要建立的連接的類型。</span><span class="sxs-lookup"><span data-stu-id="c889c-154">In the **Connection Type** dropdown, select the type of connection you want to create.</span></span>  <span data-ttu-id="c889c-155">精靈會顯示該特定類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="c889c-155">The wizard will present the properties for that particular type.</span></span>
5. <span data-ttu-id="c889c-156">完成精靈，然後按一下核取方塊以儲存新連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-156">Complete the wizard and click the checkbox to save the new connection.</span></span>

### <a name="to-create-a-new-connection-with-windows-powershell"></a><span data-ttu-id="c889c-157">使用 Windows PowerShell 建立新連接</span><span class="sxs-lookup"><span data-stu-id="c889c-157">To create a new connection with Windows PowerShell</span></span>

<span data-ttu-id="c889c-158">透過 Windows PowerShell 使用 [New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) Cmdlet 建立新連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-158">Create a new connection with Windows PowerShell using the [New-AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet.</span></span> <span data-ttu-id="c889c-159">此 Cmdlet 具有名為 **ConnectionFieldValues** 的參數，對每個連接類型定義之屬性，預期會有 [雜湊表](http://technet.microsoft.com/library/hh847780.aspx) 定義值。</span><span class="sxs-lookup"><span data-stu-id="c889c-159">This cmdlet has a parameter named **ConnectionFieldValues** that expects a [hash table](http://technet.microsoft.com/library/hh847780.aspx) defining values for each of the properties defined by the connection type.</span></span>

<span data-ttu-id="c889c-160">如果您熟悉以自動化中的[執行身分帳戶](automation-sec-configure-azure-runas-account.md)向使用服務主體之 Runbook 驗證的方式，PowerShell 指令碼 (提供做為從入口網站建立執行身分帳戶的替代做法) 會使用下列範例命令建立新的連接資產。</span><span class="sxs-lookup"><span data-stu-id="c889c-160">If you are familiar with the Automation [Run As account](automation-sec-configure-azure-runas-account.md) to authenticate runbooks using the service principal, the PowerShell script, provided as an alternative to creating the the Run As account from the portal, creates a new connection asset using the following sample commands.</span></span>  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

<span data-ttu-id="c889c-161">您也可以使用此指令碼來建立連接資產，因為當您建立您的自動化帳戶時，它預設會自動包含數個全域模組以及 **AzurServicePrincipal** 連線類型，以建立**AzureRunAsConnection** 連線資產。</span><span class="sxs-lookup"><span data-stu-id="c889c-161">You are able to use the script to create the connection asset because when you create your Automation account, it automatically includes several global modules by default along with the connection type **AzurServicePrincipal** to create the **AzureRunAsConnection** connection asset.</span></span>  <span data-ttu-id="c889c-162">這很重要要牢記在心，因為如果您嘗試建立新的連接資產來連接到採用不同驗證方法的服務或應用程式，它會失敗，因為在您的自動化帳戶未定義該連接類型。</span><span class="sxs-lookup"><span data-stu-id="c889c-162">This is important to keep in mind, because if you attempt to create a new connection asset to connect to a service or application with a different authentication method, it will fail because the connection type is not already defined in your Automation account.</span></span>  <span data-ttu-id="c889c-163">有關如何從 [PowerShell 資源庫](https://www.powershellgallery.com)為您的自訂或模組建立您自己的連線類型，詳細資訊請參閱[整合模組](automation-integration-modules.md)</span><span class="sxs-lookup"><span data-stu-id="c889c-163">For further information on how to create your own connection type for your custom or module from the [PowerShell Gallery](https://www.powershellgallery.com), see [Integration Modules](automation-integration-modules.md)</span></span>
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="c889c-164">在 Runbook 或 DSC 設定中使用連接</span><span class="sxs-lookup"><span data-stu-id="c889c-164">Using a connection in a runbook or DSC configuration</span></span>

<span data-ttu-id="c889c-165">您會使用 **Get-AutomationConnection** Cmdlet 在 Runbook 或 DSC 設定中擷取連接。</span><span class="sxs-lookup"><span data-stu-id="c889c-165">You retrieve a connection in a runbook or DSC configuration with the **Get-AutomationConnection** cmdlet.</span></span>  <span data-ttu-id="c889c-166">您不能使用 [Get-AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) 活動。</span><span class="sxs-lookup"><span data-stu-id="c889c-166">You cannot use the [Get-AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) activity.</span></span>  <span data-ttu-id="c889c-167">這個活動會擷取連接中不同欄位的值，並傳回其作為 [雜湊表](http://go.microsoft.com/fwlink/?LinkID=324844) ，然後可以與 Runbook 或 DSC 設定中的適當命令搭配使用。</span><span class="sxs-lookup"><span data-stu-id="c889c-167">This activity retrieves the values of the different fields in the connection and returns them as a [hash table](http://go.microsoft.com/fwlink/?LinkID=324844) which can then be used with the appropriate commands in the runbook or DSC configuration.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="c889c-168">文字式 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="c889c-168">Textual runbook sample</span></span>

<span data-ttu-id="c889c-169">下列範例命令示範如何使用先前提及的執行身分帳戶，向您的 Runbook 中的 Azure Resource Manager 資源驗證。</span><span class="sxs-lookup"><span data-stu-id="c889c-169">The following sample commands show how to use the Run As account mentioned earlier, to authenticate with Azure Resource Manager resources in your runbook.</span></span>  <span data-ttu-id="c889c-170">它會使用代表執行身分帳戶的連接資產，亦即會參考憑證型服務主體而非認證型。</span><span class="sxs-lookup"><span data-stu-id="c889c-170">It uses the connection asset representing the Run As account, which references the certificate-based service principal, not credentials.</span></span>  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a><span data-ttu-id="c889c-171">圖形化 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="c889c-171">Graphical runbook samples</span></span>

<span data-ttu-id="c889c-172">透過在圖形化編輯器 [文件庫] 窗格的連接上按一下滑鼠右鍵，然後選取 [加入至畫布]，即可將 **Get-AutomationConnection** 活動加入至圖形化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="c889c-172">You add a **Get-AutomationConnection** activity to a graphical runbook by right-clicking on the connection in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![](media/automation-connections/connection-add-canvas.png)

<span data-ttu-id="c889c-173">下圖顯示在圖形化 Runbook 中使用連接的範例。</span><span class="sxs-lookup"><span data-stu-id="c889c-173">The following image shows an example of using a connection in a graphical runbook.</span></span>  <span data-ttu-id="c889c-174">這是如上所述，使用執行身分帳戶與文字 Runbook 進行驗證的相同範例。</span><span class="sxs-lookup"><span data-stu-id="c889c-174">This is the same example shown above for authenticating using the Run As account with a textual runbook.</span></span>  <span data-ttu-id="c889c-175">這個範例會對使用連接物件進行驗證的 **Get RunAs Connection** 活動使用 **Constant value** 資料集。</span><span class="sxs-lookup"><span data-stu-id="c889c-175">This example uses the **Constant value** data set for the **Get RunAs Connection** activity that uses a connection object for authentication.</span></span>  <span data-ttu-id="c889c-176">在此處使用[管線連結](automation-graphical-authoring-intro.md#links-and-workflow)，是因為 ServicePrincipalCertificate 參數集預期的是單一物件。</span><span class="sxs-lookup"><span data-stu-id="c889c-176">A [pipeline link](automation-graphical-authoring-intro.md#links-and-workflow) is used here since the ServicePrincipalCertificate parameter set is expecting a single object.</span></span>

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a><span data-ttu-id="c889c-177">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c889c-177">Next steps</span></span>

- <span data-ttu-id="c889c-178">閱讀[圖形化編寫中的連結](automation-graphical-authoring-intro.md#links-and-workflow)，以了解如何引導和控制您的 Runbook 中的邏輯流程。</span><span class="sxs-lookup"><span data-stu-id="c889c-178">Review [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow) to understand how to direct and control the flow of logic in your runbooks.</span></span>  

- <span data-ttu-id="c889c-179">若要進一步了解 Azure 自動化如何使用 PowerShell 模組，以及建立自有 PowerShell 模組來做為 Azure 自動化內整合模組的最佳做法，請參閱[整合模組](automation-integration-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="c889c-179">To learn more about Azure Automation's use of PowerShell modules and best practices for creating your own PowerShell modules to work as Integration Modules within Azure Automation, see [Integration Modules](automation-integration-modules.md).</span></span>  
