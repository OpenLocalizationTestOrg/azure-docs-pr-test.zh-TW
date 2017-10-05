---
title: "Azure 自動化中的變數資產 | Microsoft Docs"
description: "變數資產是可用於 Azure 自動化中所有 Runbook 和 DSC 設定的值。  這篇文章說明變數的詳細資料，以及如何以文字式和圖形化編寫形式加以使用。"
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
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="bc5a9-104">Azure 自動化中的變數資產</span><span class="sxs-lookup"><span data-stu-id="bc5a9-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="bc5a9-105">變數資產是可用於自動化帳戶中所有 Runbook 和 DSC 設定的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="bc5a9-106">可以從 Azure 入口網站、Windows PowerShell、Runbook 或 DSC 設定建立修改並擷取。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="bc5a9-107">自動化變數對下列案例很實用：</span><span class="sxs-lookup"><span data-stu-id="bc5a9-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="bc5a9-108">在多個 Runbook 或 DSC 設定之間共用值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="bc5a9-109">在相同 Runbook 或 DSC 設定的多個作業之間共用值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="bc5a9-110">從入口網站，或者從 Runbook 或 DSC 設定 (例如一組像是特定的 VM 名稱清單、特定的資源群組、AD 網域名稱等常見設定項目) 所使用的 Windows PowerShell 命令列來管理值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="bc5a9-111">自動化變數會保存，即使 Runbook 或 DSC 設定失敗也可持續使用變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="bc5a9-112">這也可讓一個 Runbook 設定某個值，然後由另一個 Runbook 使用，或者由相同的 Runbook 或 DSC 設定於下次執行時使用該值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="bc5a9-113">建立變數時，您可以指定將其加密儲存。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="bc5a9-114">變數加密時，會安全地儲存在 Azure 自動化中，而且無法透過隨附於 Azure PowerShell 模組的 [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) Cmdlet 擷取其值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="bc5a9-115">可以擷取加密值的唯一方法是從 Runbook 或 DSC 設定中的 **Get-AutomationVariable** 活動。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="bc5a9-116">Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="bc5a9-117">這些資產都會經過加密，並使用為每個自動化帳戶產生的唯一索引鍵儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="bc5a9-118">這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="bc5a9-119">儲存安全資產之前，會使用主要憑證解密自動化帳戶的金鑰，然後用來加密資產。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="bc5a9-120">變數型別</span><span class="sxs-lookup"><span data-stu-id="bc5a9-120">Variable types</span></span>

<span data-ttu-id="bc5a9-121">使用 Azure 入口網站建立變數時，您必須從下拉式清單中指定資料類型，使得入口網站可以顯示適當的控制項來輸入變數值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="bc5a9-122">變數不會受限於這個資料型別，但如果您想要指定不同型別的值，您必須使用 Windows PowerShell 來設定變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="bc5a9-123">如果您指定 [未定義]，則變數的值會設為 **$null**，而且您必須使用 [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) Cmdlet 或 **Set-AutomationVariable** 活動來設定該值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="bc5a9-124">您無法在入口網站中建立或變更複雜變數型別的值，但是您可以使用 Windows PowerShell 提供任何型別的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="bc5a9-125">複雜型別會傳回為 [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="bc5a9-126">您可以藉由建立陣列或雜湊表，並將它儲存到變數中，來儲存多個值到單一變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="bc5a9-127">以下是可在自動化中使用的變數類型清單：</span><span class="sxs-lookup"><span data-stu-id="bc5a9-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="bc5a9-128">String</span><span class="sxs-lookup"><span data-stu-id="bc5a9-128">String</span></span>
* <span data-ttu-id="bc5a9-129">Integer</span><span class="sxs-lookup"><span data-stu-id="bc5a9-129">Integer</span></span>
* <span data-ttu-id="bc5a9-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="bc5a9-130">DateTime</span></span>
* <span data-ttu-id="bc5a9-131">Boolean</span><span class="sxs-lookup"><span data-stu-id="bc5a9-131">Boolean</span></span>
* <span data-ttu-id="bc5a9-132">Null</span><span class="sxs-lookup"><span data-stu-id="bc5a9-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="bc5a9-133">Cmdlet 和工作流程活動</span><span class="sxs-lookup"><span data-stu-id="bc5a9-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="bc5a9-134">下表中的 Cmdlet 是用來使用 Windows PowerShell 建立和管理自動化變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="bc5a9-135">它們是隨著 [Azure PowerShell 模組](../powershell-install-configure.md) 的一部分推出，可供在自動化 Runbook 和 DSC 設定中使用。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="bc5a9-136">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="bc5a9-136">Cmdlets</span></span>|<span data-ttu-id="bc5a9-137">說明</span><span class="sxs-lookup"><span data-stu-id="bc5a9-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="bc5a9-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bc5a9-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="bc5a9-139">擷取現有變數的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="bc5a9-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bc5a9-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="bc5a9-141">建立新的變數並設定其值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="bc5a9-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bc5a9-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="bc5a9-143">移除現有的變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="bc5a9-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bc5a9-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="bc5a9-145">設定現有的變數的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="bc5a9-146">下表中的工作流程活動可用來在 Runbook 中存取自動化變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="bc5a9-147">它們僅供在 Runbook 或 DSC 設定中使用，並且不會隨著 Azure PowerShell 模組的一部分推出。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="bc5a9-148">工作流程活動</span><span class="sxs-lookup"><span data-stu-id="bc5a9-148">Workflow Activities</span></span>|<span data-ttu-id="bc5a9-149">說明</span><span class="sxs-lookup"><span data-stu-id="bc5a9-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="bc5a9-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bc5a9-150">Get-AutomationVariable</span></span>|<span data-ttu-id="bc5a9-151">擷取現有變數的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="bc5a9-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="bc5a9-152">Set-AutomationVariable</span></span>|<span data-ttu-id="bc5a9-153">設定現有的變數的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="bc5a9-154">您應該避免在 Runbook 或 DSC 設定中 **Get-AutomationVariable** 的 -Name 參數中使用變數，因為這可能會使在設計階段中探索 Runbook 或 DSC 設定與自動化變數之間的相依性變得複雜。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="bc5a9-155">建立新自動化變數</span><span class="sxs-lookup"><span data-stu-id="bc5a9-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="bc5a9-156">使用 Azure 入口網站建立新的變數</span><span class="sxs-lookup"><span data-stu-id="bc5a9-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="bc5a9-157">從您的自動化帳戶，按一下 [資產] 圖格，然後在 [資產] 刀鋒視窗上選取 [變數]。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="bc5a9-158">在 [變數] 圖格上，選取 [新增變數]。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="bc5a9-159">完成 [新增變數] 刀鋒視窗上的選項，然後按一下 [建立] 並儲存新變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="bc5a9-160">使用 Windows PowerShell 建立新變數</span><span class="sxs-lookup"><span data-stu-id="bc5a9-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="bc5a9-161">[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) Cmdlet 會建立新變數，並設定其初始值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="bc5a9-162">您可以使用 [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) 來擷取值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="bc5a9-163">如果值為簡單型別，則會傳回該相同的型別。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="bc5a9-164">如果它是複雜型別，則會傳回 **PSCustomObject** 。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="bc5a9-165">下列範例命令顯示如何建立字串型別的變數，然後傳回它的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="bc5a9-166">下列範例命令顯示如何建立具有複雜型別的變數，然後傳回其屬性。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="bc5a9-167">在此情況下，會使用來自 **Get-AzureRmVm** 的虛擬機器物件。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="bc5a9-168">在 Runbook 或 DSC 設定中使用變數</span><span class="sxs-lookup"><span data-stu-id="bc5a9-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="bc5a9-169">使用 **Set-AutomationVariable** 活動來設定 Runbook 或 DSC 設定中自動化變數的值，並使用 **Get-AutomationVariable** 來擷取它。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="bc5a9-170">您不應該在 Runbook 或 DSC 設定中使用 **Set-AzureAutomationVariable** 或 **Get-AzureAutomationVariable** Cmdlet，因為它們都不如工作流程活動有效率。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="bc5a9-171">您也無法使用 **Get-AzureAutomationVariable**擷取安全變數的值。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="bc5a9-172">在 Runbook 或 DSC 設定中建立新變數的唯一方法是使用 [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="bc5a9-173">文字式 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="bc5a9-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="bc5a9-174">從變數設定和擷取簡單的值</span><span class="sxs-lookup"><span data-stu-id="bc5a9-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="bc5a9-175">下列範例命令顯示如何設定及擷取文字式 Runbook 中的變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="bc5a9-176">在此範例中，假設已經建立名稱為 *NumberOfIterations* 和 *NumberOfRunnings* 的整數類型變數，以及名稱為 *SampleMessage* 字串類型變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="bc5a9-177">設定和擷取變數中的複雜物件</span><span class="sxs-lookup"><span data-stu-id="bc5a9-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="bc5a9-178">下列範例程式碼顯示如何在文字式Runbook 中使用複雜值來更新變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="bc5a9-179">在此範例中，會使用 **Get-AzureVM** 擷取 Azure 虛擬機器並儲存至現有的自動化變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="bc5a9-180">如 [變數型別](#variable-types)中所述，這會儲存為 PSCustomObject。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="bc5a9-181">在下列程式碼中，值是從變數擷取，且用來啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="bc5a9-182">設定和擷取變數中的集合</span><span class="sxs-lookup"><span data-stu-id="bc5a9-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="bc5a9-183">下列範例程式碼顯示如何在文字式Runbook 中使用變數搭配複雜值的集合。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="bc5a9-184">在此範例中，會使用 **Get-AzureVM** 擷取多部 Azure 虛擬機器並儲存至現有的自動化變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="bc5a9-185">如 [變數型別](#variable-types)中所述，這會儲存為 PSCustomObject 的集合。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="bc5a9-186">在下列程式碼中，集合是從變數擷取，且用來啟動每部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="bc5a9-187">圖形化 Runbook 範例</span><span class="sxs-lookup"><span data-stu-id="bc5a9-187">Graphical runbook samples</span></span>

<span data-ttu-id="bc5a9-188">在圖形化 Runbook 中，您會加入 **Get-AutomationVariable** 或 **Set-AutomationVariable**，方法是在圖形化編輯器 [文件庫] 窗格中的變數上按一下滑鼠右鍵，然後選取您想要的活動。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![加入變數至畫布](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="bc5a9-190">變數中的設定值</span><span class="sxs-lookup"><span data-stu-id="bc5a9-190">Setting values in a variable</span></span>
<span data-ttu-id="bc5a9-191">下圖顯示的範例活動會在圖形化 Runbook 中使用簡單值更新變數。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="bc5a9-192">在此範例中，會使用 **Get-AzureRmVM** 擷取單一 Azure 虛擬機器，而電腦名稱會儲存至現有的自動化變數，其類型為字串。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="bc5a9-193">[連結是管線或順序](automation-graphical-authoring-intro.md#links-and-workflow) 都沒關係，因為我們在輸出中只預期單一物件。</span><span class="sxs-lookup"><span data-stu-id="bc5a9-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![設定簡單變數](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="bc5a9-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc5a9-195">Next Steps</span></span>

* <span data-ttu-id="bc5a9-196">若要深入了解如何在圖形化編寫中將活動連接在一起，請參閱 [圖形化編寫中的連結](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="bc5a9-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="bc5a9-197">若要開始使用圖形化 Runbook，請參閱 [我的第一個圖形化 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="bc5a9-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

