---
title: "Runbook 輸入參數 | Microsoft Docs"
description: "Runbook 輸入參數可讓您將資料傳遞至剛啟動的 Runbook，以增加 Runbook 的彈性。 本文說明在 Runbook 中使用輸入參數的不同案例。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="105cd-104">Runbook 輸入參數</span><span class="sxs-lookup"><span data-stu-id="105cd-104">Runbook input parameters</span></span>
<span data-ttu-id="105cd-105">Runbook 輸入參數可讓您將資料傳遞至剛啟動的 Runbook，以增加 Runbook 的彈性。</span><span class="sxs-lookup"><span data-stu-id="105cd-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="105cd-106">這些參數可讓Runbook 動作以特定案例和環境做為目標。</span><span class="sxs-lookup"><span data-stu-id="105cd-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="105cd-107">在本文中，我們將逐步引導您了解在 Runbook 中使用輸入參數的不同案例。</span><span class="sxs-lookup"><span data-stu-id="105cd-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="105cd-108">設定輸入參數</span><span class="sxs-lookup"><span data-stu-id="105cd-108">Configure input parameters</span></span>
<span data-ttu-id="105cd-109">輸入參數可以在 PowerShell、PowerShell 工作流程和圖形化 Runbook 中設定。</span><span class="sxs-lookup"><span data-stu-id="105cd-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="105cd-110">一個 Runbook 可以使用具有不同資料類型的多個參數，或完全不使用參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="105cd-111">輸入參數可以是強制性或選擇性的，而且您可以為選擇性參數指派預設值。</span><span class="sxs-lookup"><span data-stu-id="105cd-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="105cd-112">您可以在透過其中一種可用方法啟動 Runbook 時，指派 Runbook 的輸入參數值。</span><span class="sxs-lookup"><span data-stu-id="105cd-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="105cd-113">可用方法包括從入口網站或 Web 服務啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="105cd-114">您也可以啟動一個 Runbook 做為在另一個 Runbook 中以內嵌方式呼叫的子 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="105cd-115">在 PowerShell 和 PowerShell 工作流程 Runbook 中設定輸入參數</span><span class="sxs-lookup"><span data-stu-id="105cd-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="105cd-116">Azure 自動化中的 PowerShell 和 [PowerShell 工作流程 Runbook](automation-first-runbook-textual.md) 支援透過下列屬性定義的輸入參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="105cd-117">**屬性**</span><span class="sxs-lookup"><span data-stu-id="105cd-117">**Property**</span></span> | <span data-ttu-id="105cd-118">**說明**</span><span class="sxs-lookup"><span data-stu-id="105cd-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="105cd-119">類型</span><span class="sxs-lookup"><span data-stu-id="105cd-119">Type</span></span> |<span data-ttu-id="105cd-120">必要。</span><span class="sxs-lookup"><span data-stu-id="105cd-120">Required.</span></span> <span data-ttu-id="105cd-121">對參數值預期的資料類型。</span><span class="sxs-lookup"><span data-stu-id="105cd-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="105cd-122">任何 .NET 類型皆有效。</span><span class="sxs-lookup"><span data-stu-id="105cd-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="105cd-123">名稱</span><span class="sxs-lookup"><span data-stu-id="105cd-123">Name</span></span> |<span data-ttu-id="105cd-124">必要。</span><span class="sxs-lookup"><span data-stu-id="105cd-124">Required.</span></span> <span data-ttu-id="105cd-125">參數名稱。</span><span class="sxs-lookup"><span data-stu-id="105cd-125">The name of the parameter.</span></span> <span data-ttu-id="105cd-126">這在 Runbook 中必須是唯一的，並且只能包含字母、數字或底線字元。</span><span class="sxs-lookup"><span data-stu-id="105cd-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="105cd-127">而且必須以字母開頭。</span><span class="sxs-lookup"><span data-stu-id="105cd-127">It must start with a letter.</span></span> |
| <span data-ttu-id="105cd-128">強制</span><span class="sxs-lookup"><span data-stu-id="105cd-128">Mandatory</span></span> |<span data-ttu-id="105cd-129">選用。</span><span class="sxs-lookup"><span data-stu-id="105cd-129">Optional.</span></span> <span data-ttu-id="105cd-130">指定是否必須提供參數的值。</span><span class="sxs-lookup"><span data-stu-id="105cd-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="105cd-131">如果您將此項目設定為 **$true**，則在 Runbook 啟動時必須提供其值。</span><span class="sxs-lookup"><span data-stu-id="105cd-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="105cd-132">如果您將此項目設定為 **$false**，則可以選擇提供值。</span><span class="sxs-lookup"><span data-stu-id="105cd-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="105cd-133">預設值</span><span class="sxs-lookup"><span data-stu-id="105cd-133">Default value</span></span> |<span data-ttu-id="105cd-134">選用。</span><span class="sxs-lookup"><span data-stu-id="105cd-134">Optional.</span></span>  <span data-ttu-id="105cd-135">指定在 Runbook 啟動時未傳遞值的情況下所將用於參數的值。</span><span class="sxs-lookup"><span data-stu-id="105cd-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="105cd-136">任何參數皆可設定為預設值，此值將會使參數自動成為選擇性，無論 [強制] 設定為何。</span><span class="sxs-lookup"><span data-stu-id="105cd-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="105cd-137">Windows PowerShell 所支援的輸入參數屬性比此處所列的多，例如驗證、別名和參數集。</span><span class="sxs-lookup"><span data-stu-id="105cd-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="105cd-138">不過，Azure 自動化目前僅支援以上所列的輸入參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="105cd-139">PowerShell 工作流程 Runbook 中的參數定義具有下列一般形式，其中，多個參數會以逗號分隔。</span><span class="sxs-lookup"><span data-stu-id="105cd-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="105cd-140">定義參數時，如果您未指定 **Mandatory** 屬性，依預設會將該參數視為選擇性。</span><span class="sxs-lookup"><span data-stu-id="105cd-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="105cd-141">此外，如果您在 PowerShell 工作流程 Runbook 中設定某個參數的預設值，則 Powershell 會將其視為選擇性參數，無論其 **Mandatory** 屬性值為何。</span><span class="sxs-lookup"><span data-stu-id="105cd-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="105cd-142">舉例來說，我們為輸出虛擬機器 (可以是單一 VM 或資源群組內的所有 VM) 相關詳細資料的 PowerShell 工作流程 Runbook 設定輸入參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="105cd-143">如以下螢幕擷取畫面所示，此 Runbook 有兩個參數：虛擬機器的名稱和資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="105cd-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![自動化 PowerShell 工作流程](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="105cd-145">在此參數定義中， **$VMName** 和 **$resourceGroupName** 參數是字串類型的簡單參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="105cd-146">不過，PowerShell 和 PowerShell 工作流程 Runbook 支援所有簡單類型和複雜類型，例如輸入參數的 **object** 或 **PSCredential**。</span><span class="sxs-lookup"><span data-stu-id="105cd-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="105cd-147">如果您的 Runbook 有 object 類型的輸入參數，則使用具有 (name,value) 配對的 PowerShell 雜湊表來傳入值。</span><span class="sxs-lookup"><span data-stu-id="105cd-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="105cd-148">例如，如果您在 Runbook 中有下列參數：</span><span class="sxs-lookup"><span data-stu-id="105cd-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="105cd-149">則您可以將下列值傳遞至參數：</span><span class="sxs-lookup"><span data-stu-id="105cd-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="105cd-150">在圖形化 Runbook 中設定輸入參數</span><span class="sxs-lookup"><span data-stu-id="105cd-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="105cd-151">為了使用輸入參數[設定圖形化 Runbook](automation-first-runbook-graphical.md)，我們將建立會輸出虛擬機器 (可以是單一 VM 或資源群組內的所有 VM) 相關詳細資料的圖形化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="105cd-152">設定 Runbook 包含兩個主要活動，如下所述。</span><span class="sxs-lookup"><span data-stu-id="105cd-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="105cd-153">[**使用 Azure 執行身分帳戶驗證 Runbook**](automation-sec-configure-azure-runas-account.md) 以 Azure 驗證。</span><span class="sxs-lookup"><span data-stu-id="105cd-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="105cd-154">以 [**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) 取得虛擬機器的屬性。</span><span class="sxs-lookup"><span data-stu-id="105cd-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="105cd-155">您可以使用 [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) 活動來輸出虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="105cd-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="105cd-156">**Get-AzureRmVm** 活動會接受兩個參數：**虛擬機器名稱**和**資源群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="105cd-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="105cd-157">由於這些參數在您每次啟動 Runbook 時可能需要不同的值，因此您可以將輸入參數新增至您的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="105cd-158">以下是新增輸入參數的步驟：</span><span class="sxs-lookup"><span data-stu-id="105cd-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="105cd-159">從 [Runbook]  刀鋒視窗中選取圖形化 Runbook，然後按一下 [編輯][](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="105cd-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="105cd-160">在 Runbook 編輯器中，按一下 [輸入和輸出] 以開啟 [輸入和輸出] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="105cd-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![自動化圖形化 Runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="105cd-162">[輸入和輸出]  刀鋒視窗會顯示為 Runbook 定義的輸入參數清單。</span><span class="sxs-lookup"><span data-stu-id="105cd-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="105cd-163">在此刀鋒視窗上，您可以新增輸入參數，或編輯現有輸入參數的組態。</span><span class="sxs-lookup"><span data-stu-id="105cd-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="105cd-164">若要為 Runbook 新增參數，請按一下 [新增輸入] 以開啟 [Runbook 輸入參數] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="105cd-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="105cd-165">您可以在其中設定下列連線參數：</span><span class="sxs-lookup"><span data-stu-id="105cd-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="105cd-166">**屬性**</span><span class="sxs-lookup"><span data-stu-id="105cd-166">**Property**</span></span> | <span data-ttu-id="105cd-167">**說明**</span><span class="sxs-lookup"><span data-stu-id="105cd-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="105cd-168">名稱</span><span class="sxs-lookup"><span data-stu-id="105cd-168">Name</span></span> |<span data-ttu-id="105cd-169">必要。</span><span class="sxs-lookup"><span data-stu-id="105cd-169">Required.</span></span>  <span data-ttu-id="105cd-170">參數名稱。</span><span class="sxs-lookup"><span data-stu-id="105cd-170">The name of the parameter.</span></span> <span data-ttu-id="105cd-171">這在 Runbook 中必須是唯一的，並且只能包含字母、數字或底線字元。</span><span class="sxs-lookup"><span data-stu-id="105cd-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="105cd-172">而且必須以字母開頭。</span><span class="sxs-lookup"><span data-stu-id="105cd-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="105cd-173">說明</span><span class="sxs-lookup"><span data-stu-id="105cd-173">Description</span></span> |<span data-ttu-id="105cd-174">選用。</span><span class="sxs-lookup"><span data-stu-id="105cd-174">Optional.</span></span> <span data-ttu-id="105cd-175">關於輸入參數用途的說明。</span><span class="sxs-lookup"><span data-stu-id="105cd-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="105cd-176">類型</span><span class="sxs-lookup"><span data-stu-id="105cd-176">Type</span></span> |<span data-ttu-id="105cd-177">選用。</span><span class="sxs-lookup"><span data-stu-id="105cd-177">Optional.</span></span> <span data-ttu-id="105cd-178">對參數值預期的資料類型。</span><span class="sxs-lookup"><span data-stu-id="105cd-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="105cd-179">支援的參數類型有：**String**、**Int32**、**Int64**、**Decimal**、**Boolean**、**DateTime**、**Object**。</span><span class="sxs-lookup"><span data-stu-id="105cd-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="105cd-180">若未選取資料類型，將預設為 **String**。</span><span class="sxs-lookup"><span data-stu-id="105cd-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="105cd-181">強制</span><span class="sxs-lookup"><span data-stu-id="105cd-181">Mandatory</span></span> |<span data-ttu-id="105cd-182">選用。</span><span class="sxs-lookup"><span data-stu-id="105cd-182">Optional.</span></span> <span data-ttu-id="105cd-183">指定是否必須提供參數的值。</span><span class="sxs-lookup"><span data-stu-id="105cd-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="105cd-184">如果您選擇 [是] ，則在 Runbook 啟動時必須提供其值。</span><span class="sxs-lookup"><span data-stu-id="105cd-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="105cd-185">如果您選擇 [否] ，則在 Runbook 啟動時不一定需要值，並且可設定預設值。</span><span class="sxs-lookup"><span data-stu-id="105cd-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="105cd-186">預設值</span><span class="sxs-lookup"><span data-stu-id="105cd-186">Default Value</span></span> |<span data-ttu-id="105cd-187">選用。</span><span class="sxs-lookup"><span data-stu-id="105cd-187">Optional.</span></span> <span data-ttu-id="105cd-188">指定在 Runbook 啟動時未傳遞值的情況下所將用於參數的值。</span><span class="sxs-lookup"><span data-stu-id="105cd-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="105cd-189">不是強制性的參數可以設定預設值。</span><span class="sxs-lookup"><span data-stu-id="105cd-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="105cd-190">若要設定預設值，請選擇 [自訂] 。</span><span class="sxs-lookup"><span data-stu-id="105cd-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="105cd-191">除非在 Runbook 啟動時提供了其他值，否則將會使用此值。</span><span class="sxs-lookup"><span data-stu-id="105cd-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="105cd-192">若不想提供任何預設值，請選擇 [無]  。</span><span class="sxs-lookup"><span data-stu-id="105cd-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![加入新的輸入](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="105cd-194">使用下列屬性，建立將由 **Get-AzureRmVm** 活動使用的兩個參數：</span><span class="sxs-lookup"><span data-stu-id="105cd-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="105cd-195">**參數1：**</span><span class="sxs-lookup"><span data-stu-id="105cd-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="105cd-196">Name - VMName</span><span class="sxs-lookup"><span data-stu-id="105cd-196">Name - VMName</span></span>
     * <span data-ttu-id="105cd-197">Type - String</span><span class="sxs-lookup"><span data-stu-id="105cd-197">Type - String</span></span>
     * <span data-ttu-id="105cd-198">Mandatory - No</span><span class="sxs-lookup"><span data-stu-id="105cd-198">Mandatory - No</span></span>
   * <span data-ttu-id="105cd-199">**參數 2：**</span><span class="sxs-lookup"><span data-stu-id="105cd-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="105cd-200">Name - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="105cd-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="105cd-201">Type - String</span><span class="sxs-lookup"><span data-stu-id="105cd-201">Type - String</span></span>
     * <span data-ttu-id="105cd-202">Mandatory - No</span><span class="sxs-lookup"><span data-stu-id="105cd-202">Mandatory - No</span></span>
     * <span data-ttu-id="105cd-203">Default value - Custom</span><span class="sxs-lookup"><span data-stu-id="105cd-203">Default value - Custom</span></span>
     * <span data-ttu-id="105cd-204">自訂預設值 - \<包含虛擬機器之資源群組的名稱></span><span class="sxs-lookup"><span data-stu-id="105cd-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="105cd-205">新增參數之後，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="105cd-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="105cd-206">現在，您可以在 [輸入和輸出] 刀鋒視窗中加以檢視。</span><span class="sxs-lookup"><span data-stu-id="105cd-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="105cd-207">再按一下 [確定]，然後按一下 [儲存] 並 [發佈] 您的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="105cd-208">將值指派給 Runbook 中的輸入參數</span><span class="sxs-lookup"><span data-stu-id="105cd-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="105cd-209">在下列情況下，您可以將值傳遞至 Runbook 中的輸入參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="105cd-210">啟動 Runbook 並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="105cd-211">Runbook 有多種啟動方式：透過 Azure 入口網站、透過 Webhook、透過 PowerShell Cmdlet、REST API 或 SDK。</span><span class="sxs-lookup"><span data-stu-id="105cd-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="105cd-212">以下我們將討論啟動 Runbook 並指派參數的不同方法。</span><span class="sxs-lookup"><span data-stu-id="105cd-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="105cd-213">使用 Azure 入口網站啟動已發佈的 Runbook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="105cd-214">當您[啟動 Runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) 時，[啟動 Runbook] 刀鋒視窗隨即開啟，而您可以為剛建立的參數設定值。</span><span class="sxs-lookup"><span data-stu-id="105cd-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![使用入口網站啟動](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="105cd-216">在輸入方塊下的標籤中，您可以查看為參數設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="105cd-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="105cd-217">這些屬性包括強制或選擇性、類型和預設值。</span><span class="sxs-lookup"><span data-stu-id="105cd-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="105cd-218">在參數名稱旁的球形文字說明中，您可以檢視您在進行參數輸入值相關決策時所需的所有金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="105cd-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="105cd-219">此資訊包括參數為強制或選擇性。</span><span class="sxs-lookup"><span data-stu-id="105cd-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="105cd-220">也包括類型和預設值 (如果有的話) 和其他有用的注意事項。</span><span class="sxs-lookup"><span data-stu-id="105cd-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![說明提示氣球](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="105cd-222">字串類型參數支援 **空** 字串值。</span><span class="sxs-lookup"><span data-stu-id="105cd-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="105cd-223">在輸入參數文字方塊中輸入 **[EmptyString]** ，將會傳遞空字串給參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="105cd-224">此外，字串類型參數不支援傳遞 **Null** 值。</span><span class="sxs-lookup"><span data-stu-id="105cd-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="105cd-225">若未傳遞任何值給字串參數，PowerShell 會將其解譯為 Null。</span><span class="sxs-lookup"><span data-stu-id="105cd-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="105cd-226">使用 PowerShell Cmdlet 啟動已發佈的 Runbook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="105cd-227">**Azure Resource Manager Cmdlet：** 您可以使用 [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)啟動在資源群組中建立的自動化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="105cd-228">**範例：**</span><span class="sxs-lookup"><span data-stu-id="105cd-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="105cd-229">**Azure 服務管理 Cmdlet：** 您可以使用 [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)啟動在預設資源群組中建立的自動化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="105cd-230">**範例：**</span><span class="sxs-lookup"><span data-stu-id="105cd-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="105cd-231">當您使用 PowerShell Cmdlet 啟動 Runbook 時，將建立值為 **PowerShell** 的預設參數 **MicrosoftApplicationManagementStartedBy**。</span><span class="sxs-lookup"><span data-stu-id="105cd-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="105cd-232">您可以在 [作業詳細資料]  刀鋒視窗中檢視此參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="105cd-233">使用 SDK 啟動 Runbook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="105cd-234">**Azure Resource Manager 方法：** 您可以使用程式設計語言的 SDK 來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="105cd-235">以下 C# 程式碼片段用於在您的自動化帳戶中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="105cd-236">您可以在我們的 [GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)中檢視完整的程式碼。</span><span class="sxs-lookup"><span data-stu-id="105cd-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="105cd-237">**Azure 服務管理方法：** 您可以使用程式設計語言的 SDK 來啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="105cd-238">以下 C# 程式碼片段用於在您的自動化帳戶中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="105cd-239">您可以在我們的 [GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)中檢視完整的程式碼。</span><span class="sxs-lookup"><span data-stu-id="105cd-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="105cd-240">若要啟動此方法，請建立字典來儲存 Runbook 參數、**VMName**、**resourceGroupName** 以及其值。</span><span class="sxs-lookup"><span data-stu-id="105cd-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="105cd-241">然後啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-241">Then start the runbook.</span></span> <span data-ttu-id="105cd-242">以下 C# 程式碼片段用於呼叫上面定義的方法。</span><span class="sxs-lookup"><span data-stu-id="105cd-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="105cd-243">使用 REST API 啟動 Runbook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="105cd-244">Runbook 作業可透過 Azure 自動化 REST API，使用 **PUT** 方法和下列要求 URI 來建立及啟動。</span><span class="sxs-lookup"><span data-stu-id="105cd-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="105cd-245">在要求 URI 中，取代下列參數：</span><span class="sxs-lookup"><span data-stu-id="105cd-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="105cd-246">**subscription-id：** 您的 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="105cd-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="105cd-247">**cloud-service-name：** 要求所要傳送到的雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="105cd-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="105cd-248">**automation-account-name：** 裝載在指定的雲端服務內的自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="105cd-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="105cd-249">**job-id：** 作業的 GUID。</span><span class="sxs-lookup"><span data-stu-id="105cd-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="105cd-250">您可以使用 **[GUID]::NewGuid().ToString()** 命令建立 PowerShell 中的 GUID。</span><span class="sxs-lookup"><span data-stu-id="105cd-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="105cd-251">若要將參數傳遞至 Runbook 作業，請使用要求本文。</span><span class="sxs-lookup"><span data-stu-id="105cd-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="105cd-252">它會採用兩個以 JSON 格式提供的屬性：</span><span class="sxs-lookup"><span data-stu-id="105cd-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="105cd-253">**Runbook 名稱：** 必要。</span><span class="sxs-lookup"><span data-stu-id="105cd-253">**Runbook name:** Required.</span></span> <span data-ttu-id="105cd-254">作業要啟動之 Runbook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="105cd-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="105cd-255">**Runbook 參數：** 選擇性。</span><span class="sxs-lookup"><span data-stu-id="105cd-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="105cd-256">參數清單的字典；清單必須採用 (名稱, 值) 格式，其中的名稱應為字串類型，而值可以是任何有效的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="105cd-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="105cd-257">如果您想要啟動先前以 **VMName** 和 **resourceGroupName** 做為參數建立的 **Get-AzureVMTextual** Runbook，請使用下列 JSON 格式的要求本文。</span><span class="sxs-lookup"><span data-stu-id="105cd-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="105cd-258">如果成功建立作業，則會傳回 HTTP 狀態碼 201。</span><span class="sxs-lookup"><span data-stu-id="105cd-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="105cd-259">如需關於回應標頭和回應本文的詳細資訊，請參閱有關如何 [使用 REST API 建立 Runbook 作業](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="105cd-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="105cd-260">測試 Runbook 並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="105cd-261">當您使用測試選項[測試 Runbook 的草稿版本](automation-testing-runbook.md)時，將會開啟 [測試] 刀鋒視窗，您可以在其中為剛建立的參數設定值。</span><span class="sxs-lookup"><span data-stu-id="105cd-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![測試並指派參數](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="105cd-263">將排程連結至 Runbook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="105cd-264">您可以[將排程連結](automation-schedules.md)至您的 Runbook，以在特定時間啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="105cd-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="105cd-265">您會在建立排程時指派輸入參數，且 Runbook 經由排程啟動時，將會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="105cd-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="105cd-266">必須提供所有必要參數值，才能儲存排程。</span><span class="sxs-lookup"><span data-stu-id="105cd-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![排程並指派參數](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="105cd-268">建立 Runbook 的 Webhook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="105cd-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="105cd-269">您可以為您的 Runbook 建立 [Webhook](automation-webhooks.md) ，並設定 Runbook 輸入參數。</span><span class="sxs-lookup"><span data-stu-id="105cd-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="105cd-270">必須提供所有必要參數值，才能儲存 Webhook。</span><span class="sxs-lookup"><span data-stu-id="105cd-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![建立 Webhook 並指派參數](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="105cd-272">當您使用 Webhook 執行 Runbook 時，會隨著您定義的輸入參數傳送預先定義的輸入參數 **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** 。</span><span class="sxs-lookup"><span data-stu-id="105cd-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="105cd-273">您可以按一下 **WebhookData** 參數加以展開，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="105cd-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![WebhookData 參數](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="105cd-275">後續步驟</span><span class="sxs-lookup"><span data-stu-id="105cd-275">Next steps</span></span>
* <span data-ttu-id="105cd-276">如需關於 Runbook 輸入和輸出的詳細資訊，請參閱 [Azure 自動化：Runbook 輸入、輸出和巢狀 Runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)。</span><span class="sxs-lookup"><span data-stu-id="105cd-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="105cd-277">如需以不同方式啟動 Runbook 的詳細資訊，請參閱 [啟動 Runbook](automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="105cd-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="105cd-278">若要編輯文字 Runbook，請參閱 [編輯文字 Runbook](automation-edit-textual-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="105cd-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="105cd-279">若要編輯圖形化 Runbook，請參閱 [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="105cd-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

