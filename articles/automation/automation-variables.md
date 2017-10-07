---
title: "在 Azure 自動化中的 aaaVariable 資產 |Microsoft 文件"
description: "變數資產是屬於可用 tooall runbook 在 Azure 自動化 DSC 設定的值。  這篇文章說明 hello 詳細資料的變數以及與它們的 toowork 文字及圖形化撰寫。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="8b661-104">Azure 自動化中的變數資產</span><span class="sxs-lookup"><span data-stu-id="8b661-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="8b661-105">變數資產是屬於可用 tooall runbook 以及自動化帳戶中的 DSC 設定的值。</span><span class="sxs-lookup"><span data-stu-id="8b661-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="8b661-106">他們可以建立、 修改，並將擷取從 hello Azure 入口網站中，Windows PowerShell，從 runbook 或 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="8b661-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="8b661-107">自動化變數適用於下列案例的 hello:</span><span class="sxs-lookup"><span data-stu-id="8b661-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="8b661-108">在多個 Runbook 或 DSC 設定之間共用值。</span><span class="sxs-lookup"><span data-stu-id="8b661-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="8b661-109">Hello 從多個工作之間共用一個值相同的 runbook 或 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="8b661-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="8b661-110">從 hello 入口網站或從 hello 所使用的 runbook 或 DSC 設定，例如一組常用設定項目特定清單類似的 VM 名稱、 特定的資源群組、 AD 網域名稱、 等的 Windows PowerShell 命令列管理值。</span><span class="sxs-lookup"><span data-stu-id="8b661-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="8b661-111">自動化變數會保存，以便繼續使用 toobe 即使 hello runbook 或 DSC 設定失敗。</span><span class="sxs-lookup"><span data-stu-id="8b661-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="8b661-112">這麼做也可以設定一個 runbook，然後由另一個，或由 hello 值 toobe 相同的 runbook 或 DSC 組態 hello 執行的下一次。</span><span class="sxs-lookup"><span data-stu-id="8b661-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="8b661-113">建立變數時，您可以指定將其加密儲存。</span><span class="sxs-lookup"><span data-stu-id="8b661-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="8b661-114">變數加密後，會安全地儲存在 Azure 自動化中，而且無法擷取其值，從 hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)隨附於 hello Azure PowerShell 模組的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8b661-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="8b661-115">hello，可以擷取加密的值的唯一方式是從 hello **Get-automationvariable**活動在 runbook 或 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="8b661-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="8b661-116">Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="8b661-117">這些資產都會經過加密並儲存在 hello 使用產生的唯一索引鍵，每個自動化帳戶的 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="8b661-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="8b661-118">這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="8b661-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="8b661-119">之前儲存安全資產，hello 自動化帳戶的 hello 金鑰會解密使用 hello 主要憑證，並接著使用 tooencrypt hello 資產。</span><span class="sxs-lookup"><span data-stu-id="8b661-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="8b661-120">變數型別</span><span class="sxs-lookup"><span data-stu-id="8b661-120">Variable types</span></span>

<span data-ttu-id="8b661-121">當您建立變數以 hello Azure 入口網站時，您必須指定 hello 下拉式清單中的資料類型，所以 hello 入口網站可以顯示 hello 適當的控制項輸入 hello 變數值。</span><span class="sxs-lookup"><span data-stu-id="8b661-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="8b661-122">hello 變數不是受限制的 toothis 資料類型，不過您必須設定使用 Windows PowerShell，如果您想 toospecify hello 變數不同類型的值。</span><span class="sxs-lookup"><span data-stu-id="8b661-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="8b661-123">如果您指定**未定義**，hello hello 變數值會設定得則**$null**，而且您必須將以 hello hello 值[Set-azureautomationvariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet 或**Set-automationvariable**活動。</span><span class="sxs-lookup"><span data-stu-id="8b661-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="8b661-124">您無法建立或變更複雜變數類型 hello 入口網站中的 hello 值，但是您可以提供使用 Windows PowerShell 的任何類型的值。</span><span class="sxs-lookup"><span data-stu-id="8b661-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="8b661-125">複雜型別會傳回為 [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8b661-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="8b661-126">您可以藉由建立陣列或雜湊表，並將它儲存 toohello 變數來儲存多個值 tooa 單一變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="8b661-127">hello 下面是可用在自動化中的變數類型的清單：</span><span class="sxs-lookup"><span data-stu-id="8b661-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="8b661-128">String</span><span class="sxs-lookup"><span data-stu-id="8b661-128">String</span></span>
* <span data-ttu-id="8b661-129">Integer</span><span class="sxs-lookup"><span data-stu-id="8b661-129">Integer</span></span>
* <span data-ttu-id="8b661-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="8b661-130">DateTime</span></span>
* <span data-ttu-id="8b661-131">Boolean</span><span class="sxs-lookup"><span data-stu-id="8b661-131">Boolean</span></span>
* <span data-ttu-id="8b661-132">Null</span><span class="sxs-lookup"><span data-stu-id="8b661-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="8b661-133">Cmdlet 和工作流程活動</span><span class="sxs-lookup"><span data-stu-id="8b661-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="8b661-134">hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 的自動化變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="8b661-135">這些 cmdlet 隨附 hello [Azure PowerShell 模組](../powershell-install-configure.md)可用於自動化 runbook 和 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="8b661-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="8b661-136">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="8b661-136">Cmdlets</span></span>|<span data-ttu-id="8b661-137">說明</span><span class="sxs-lookup"><span data-stu-id="8b661-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="8b661-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="8b661-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="8b661-139">擷取現有變數的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8b661-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="8b661-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="8b661-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="8b661-141">建立新的變數並設定其值。</span><span class="sxs-lookup"><span data-stu-id="8b661-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="8b661-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="8b661-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="8b661-143">移除現有的變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="8b661-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="8b661-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="8b661-145">設定現有變數的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8b661-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="8b661-146">在 hello 下表中的 hello 工作流程活動是使用的 tooaccess runbook 中的自動化變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="8b661-147">它們只可用於 runbook 或 DSC 設定，而且不要 hello Azure PowerShell 模組的一部分。</span><span class="sxs-lookup"><span data-stu-id="8b661-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="8b661-148">工作流程活動</span><span class="sxs-lookup"><span data-stu-id="8b661-148">Workflow Activities</span></span>|<span data-ttu-id="8b661-149">說明</span><span class="sxs-lookup"><span data-stu-id="8b661-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="8b661-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="8b661-150">Get-AutomationVariable</span></span>|<span data-ttu-id="8b661-151">擷取現有變數的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8b661-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="8b661-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="8b661-152">Set-AutomationVariable</span></span>|<span data-ttu-id="8b661-153">設定現有變數的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8b661-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="8b661-154">您應該避免使用中的變數 hello – Name 參數**Get-automationvariable**在 runbook 或 DSC 設定，因為這可以使得探索 runbook 或 DSC 設定和自動化之間的相依性在設計階段的變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="8b661-155">建立新自動化變數</span><span class="sxs-lookup"><span data-stu-id="8b661-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="8b661-156">toocreate hello Azure 入口網站的新變數</span><span class="sxs-lookup"><span data-stu-id="8b661-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="8b661-157">從您的自動化帳戶，按一下 hello**資產**磚，然後在 hello**資產**刀鋒視窗中，選取**變數**。</span><span class="sxs-lookup"><span data-stu-id="8b661-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="8b661-158">在 hello**變數**磚中，選取**加入變數**。</span><span class="sxs-lookup"><span data-stu-id="8b661-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="8b661-159">完成上 hello 的 hello 選項**新變數**刀鋒視窗，然後按一下**建立**儲存 hello 新變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="8b661-160">toocreate 使用 Windows PowerShell 的新變數</span><span class="sxs-lookup"><span data-stu-id="8b661-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="8b661-161">hello[新增 AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet 會建立新的變數，並設定其初始值。</span><span class="sxs-lookup"><span data-stu-id="8b661-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="8b661-162">您可以擷取 hello 值使用[Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8b661-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="8b661-163">如果 hello 值是簡單類型，則會傳回該相同的類型。</span><span class="sxs-lookup"><span data-stu-id="8b661-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="8b661-164">如果它是複雜型別，則會傳回 **PSCustomObject** 。</span><span class="sxs-lookup"><span data-stu-id="8b661-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="8b661-165">hello 下列範例命令顯示如何 toocreate 類型之變數的字串，然後傳回其值。</span><span class="sxs-lookup"><span data-stu-id="8b661-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="8b661-166">hello 下列範例命令顯示如何 toocreate 複雜變數類型與然後傳回其屬性。</span><span class="sxs-lookup"><span data-stu-id="8b661-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="8b661-167">在此情況下，會使用來自 **Get-AzureRmVm** 的虛擬機器物件。</span><span class="sxs-lookup"><span data-stu-id="8b661-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="8b661-168">在 Runbook 或 DSC 設定中使用變數</span><span class="sxs-lookup"><span data-stu-id="8b661-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="8b661-169">使用 hello **Set-automationvariable**活動 tooset hello 自動化中的變數值的 runbook 或 DSC 設定和 hello **Get-automationvariable** tooretrieve 它。</span><span class="sxs-lookup"><span data-stu-id="8b661-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="8b661-170">您不應該使用 hello **Set-azureautomationvariable**或**Get-azureautomationvariable** runbook 或 DSC 設定，因為它們都不如 hello 工作流程活動中的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8b661-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="8b661-171">您也無法擷取安全的變數與 hello 值**Get-azureautomationvariable**。</span><span class="sxs-lookup"><span data-stu-id="8b661-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="8b661-172">hello 只方式 toocreate 從 runbook 中的新變數，或在 DSC 設定為 toouse hello [New-azureautomationvariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8b661-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="8b661-173">文字式 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="8b661-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="8b661-174">從變數設定和擷取簡單的值</span><span class="sxs-lookup"><span data-stu-id="8b661-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="8b661-175">hello 下列範例命令顯示如何 tooset 及擷取文字的 runbook 中的變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="8b661-176">在此範例中，假設已經建立名稱為 *NumberOfIterations* 和 *NumberOfRunnings* 的整數類型變數，以及名稱為 *SampleMessage* 字串類型變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="8b661-177">設定和擷取變數中的複雜物件</span><span class="sxs-lookup"><span data-stu-id="8b661-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="8b661-178">hello 以下範例程式碼將示範如何 tooupdate 文字 runbook 中的複雜值的變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="8b661-179">在此範例中，Azure 虛擬機器會擷取與**Get-azurevm**和儲存的 tooan 現有的自動化變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="8b661-180">如 [變數型別](#variable-types)中所述，這會儲存為 PSCustomObject。</span><span class="sxs-lookup"><span data-stu-id="8b661-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="8b661-181">在下列程式碼的 hello，hello 值會擷取從 hello 變數和已使用 toostart hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8b661-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="8b661-182">設定和擷取變數中的集合</span><span class="sxs-lookup"><span data-stu-id="8b661-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="8b661-183">hello 以下範例程式碼將示範如何 toouse 文字 runbook 中的複雜值集合的變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="8b661-184">在此範例中，使用擷取多個 Azure 虛擬機器**Get-azurevm**和儲存的 tooan 現有的自動化變數。</span><span class="sxs-lookup"><span data-stu-id="8b661-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="8b661-185">如 [變數型別](#variable-types)中所述，這會儲存為 PSCustomObject 的集合。</span><span class="sxs-lookup"><span data-stu-id="8b661-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="8b661-186">在下列程式碼的 hello，hello 集合擷取自 hello 變數，且使用 toostart 每部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8b661-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="8b661-187">圖形化 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="8b661-187">Graphical runbook samples</span></span>

<span data-ttu-id="8b661-188">在圖形化 runbook，您會新增 hello **Get-automationvariable**或**Set-automationvariable** hello hello 圖形編輯器的程式庫 窗格中的 hello 變數上按一下滑鼠右鍵，然後選取 hello您想要的活動。</span><span class="sxs-lookup"><span data-stu-id="8b661-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![加入變數 toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="8b661-190">變數中的設定值</span><span class="sxs-lookup"><span data-stu-id="8b661-190">Setting values in a variable</span></span>
<span data-ttu-id="8b661-191">hello 下圖顯示範例活動 tooupdate 簡單的值的變數在圖形化 runbook。</span><span class="sxs-lookup"><span data-stu-id="8b661-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="8b661-192">在此範例中，單一 Azure 虛擬機器會擷取與**Get AzureRmVM**和 hello 電腦名稱會儲存 tooan 現有的自動化變數類型為字串。</span><span class="sxs-lookup"><span data-stu-id="8b661-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="8b661-193">無論是否 hello[連結是管線或順序](automation-graphical-authoring-intro.md#links-and-workflow)因為我們只預期有單一物件 hello 輸出中。</span><span class="sxs-lookup"><span data-stu-id="8b661-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![設定簡單變數](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="8b661-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8b661-195">Next Steps</span></span>

* <span data-ttu-id="8b661-196">toolearn 進一步了解一起連接活動，在圖形化撰寫，請參閱[中圖形化撰寫連結](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="8b661-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="8b661-197">tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="8b661-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

