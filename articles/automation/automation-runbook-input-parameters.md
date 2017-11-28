---
title: "輸入參數的 aaaRunbook |Microsoft 文件"
description: "Runbook 的輸入的參數可以讓您 toopass 資料 tooa runbook 啟動時增加 hello 彈性的 runbook。 本文說明在 Runbook 中使用輸入參數的不同案例。"
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
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="2042f-104">Runbook 輸入參數</span><span class="sxs-lookup"><span data-stu-id="2042f-104">Runbook input parameters</span></span>
<span data-ttu-id="2042f-105">Runbook 的輸入的參數可以讓您 toopass 資料 tooit 啟動時增加 hello 彈性的 runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="2042f-106">hello 參數可讓目標為特定案例和環境的 hello runbook 動作 toobe。</span><span class="sxs-lookup"><span data-stu-id="2042f-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="2042f-107">在本文中，我們將逐步引導您了解在 Runbook 中使用輸入參數的不同案例。</span><span class="sxs-lookup"><span data-stu-id="2042f-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="2042f-108">設定輸入參數</span><span class="sxs-lookup"><span data-stu-id="2042f-108">Configure input parameters</span></span>
<span data-ttu-id="2042f-109">輸入參數可以在 PowerShell、PowerShell 工作流程和圖形化 Runbook 中設定。</span><span class="sxs-lookup"><span data-stu-id="2042f-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="2042f-110">一個 Runbook 可以使用具有不同資料類型的多個參數，或完全不使用參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="2042f-111">輸入參數可以是強制性或選擇性的，而且您可以為選擇性參數指派預設值。</span><span class="sxs-lookup"><span data-stu-id="2042f-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="2042f-112">您可以將值指派 toohello runbook 的輸入的參數，當您透過 hello 可用方法之一啟動。</span><span class="sxs-lookup"><span data-stu-id="2042f-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="2042f-113">這些方法包括從 hello 入口網站或 web 服務正在啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="2042f-114">您也可以啟動一個 Runbook 做為在另一個 Runbook 中以內嵌方式呼叫的子 Runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="2042f-115">在 PowerShell 和 PowerShell 工作流程 Runbook 中設定輸入參數</span><span class="sxs-lookup"><span data-stu-id="2042f-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="2042f-116">PowerShell 和[PowerShell 工作流程 runbook](automation-first-runbook-textual.md) Azure 自動化中支援透過 hello 下列屬性定義的輸入的參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="2042f-117">**屬性**</span><span class="sxs-lookup"><span data-stu-id="2042f-117">**Property**</span></span> | <span data-ttu-id="2042f-118">**說明**</span><span class="sxs-lookup"><span data-stu-id="2042f-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="2042f-119">類型</span><span class="sxs-lookup"><span data-stu-id="2042f-119">Type</span></span> |<span data-ttu-id="2042f-120">必要。</span><span class="sxs-lookup"><span data-stu-id="2042f-120">Required.</span></span> <span data-ttu-id="2042f-121">hello hello 參數值所預期的資料型別。</span><span class="sxs-lookup"><span data-stu-id="2042f-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="2042f-122">任何 .NET 類型皆有效。</span><span class="sxs-lookup"><span data-stu-id="2042f-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="2042f-123">名稱</span><span class="sxs-lookup"><span data-stu-id="2042f-123">Name</span></span> |<span data-ttu-id="2042f-124">必要。</span><span class="sxs-lookup"><span data-stu-id="2042f-124">Required.</span></span> <span data-ttu-id="2042f-125">hello hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="2042f-125">hello name of hello parameter.</span></span> <span data-ttu-id="2042f-126">這必須 hello runbook 內是唯一的可包含字母、 數字或底線字元。</span><span class="sxs-lookup"><span data-stu-id="2042f-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="2042f-127">而且必須以字母開頭。</span><span class="sxs-lookup"><span data-stu-id="2042f-127">It must start with a letter.</span></span> |
| <span data-ttu-id="2042f-128">強制</span><span class="sxs-lookup"><span data-stu-id="2042f-128">Mandatory</span></span> |<span data-ttu-id="2042f-129">選用。</span><span class="sxs-lookup"><span data-stu-id="2042f-129">Optional.</span></span> <span data-ttu-id="2042f-130">指定是否必須提供 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="2042f-131">如果設定太**$true**，然後 hello runbook 啟動時，就必須提供值。</span><span class="sxs-lookup"><span data-stu-id="2042f-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="2042f-132">如果設定太**$false**，則為選擇性的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="2042f-133">預設值</span><span class="sxs-lookup"><span data-stu-id="2042f-133">Default value</span></span> |<span data-ttu-id="2042f-134">選用。</span><span class="sxs-lookup"><span data-stu-id="2042f-134">Optional.</span></span>  <span data-ttu-id="2042f-135">指定如果傳入的值不是 hello runbook 啟動時將用於 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="2042f-136">預設值可以設定任何參數，以及將自動進行 hello 參數選擇性不論 hello 強制設定。</span><span class="sxs-lookup"><span data-stu-id="2042f-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="2042f-137">Windows PowerShell 所支援的輸入參數屬性比此處所列的多，例如驗證、別名和參數集。</span><span class="sxs-lookup"><span data-stu-id="2042f-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="2042f-138">不過，Azure 自動化目前只支援 hello 輸入的參數上面所列。</span><span class="sxs-lookup"><span data-stu-id="2042f-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="2042f-139">在 PowerShell 工作流程 runbook 中的參數定義具有下列一般形式，多個參數會以逗號分隔的 hello。</span><span class="sxs-lookup"><span data-stu-id="2042f-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="2042f-140">當您正在定義的參數，如果您未指定 hello**強制**屬性，則會根據預設，hello 參數視為選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="2042f-141">此外，如果您在 PowerShell 工作流程 runbook 中設定參數的預設值，它將會被視為 powershell 選擇性參數，不論 hello**強制**屬性值。</span><span class="sxs-lookup"><span data-stu-id="2042f-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="2042f-142">例如，讓我們設定 hello 輸出詳細虛擬機器之單一 VM 或資源群組內的所有 Vm 的 PowerShell 工作流程 runbook 的輸入的參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="2042f-143">此 runbook hello 下列螢幕擷取畫面所示，有兩個參數： hello 的虛擬機器和 hello hello 資源群組名稱的名稱。</span><span class="sxs-lookup"><span data-stu-id="2042f-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![自動化 PowerShell 工作流程](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="2042f-145">在此參數定義中，hello 參數**$VMName**和**$resourceGroupName**是簡單字串類型的參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="2042f-146">不過，PowerShell 和 PowerShell 工作流程 Runbook 支援所有簡單類型和複雜類型，例如輸入參數的 **object** 或 **PSCredential**。</span><span class="sxs-lookup"><span data-stu-id="2042f-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="2042f-147">如果您的 runbook 具有物件類型的輸入的參數，然後使用 PowerShell 雜湊表 （名稱、 值） 與組 toopass 值中。</span><span class="sxs-lookup"><span data-stu-id="2042f-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="2042f-148">例如，如果您有下列參數在 runbook 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="2042f-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="2042f-149">然後您可以傳遞值 toohello 參數後面的 hello:</span><span class="sxs-lookup"><span data-stu-id="2042f-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="2042f-150">在圖形化 Runbook 中設定輸入參數</span><span class="sxs-lookup"><span data-stu-id="2042f-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="2042f-151">太[設定圖形化 runbook](automation-first-runbook-graphical.md)具有輸入參數，讓我們來建立圖形化 runbook 會輸出可能是虛擬機器的相關詳細資料之單一 VM 或資源群組內的所有 Vm。</span><span class="sxs-lookup"><span data-stu-id="2042f-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="2042f-152">設定 Runbook 包含兩個主要活動，如下所述。</span><span class="sxs-lookup"><span data-stu-id="2042f-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="2042f-153">[**向 Azure 執行身分帳戶的 Runbook** ](automation-sec-configure-azure-runas-account.md) tooauthenticate 與 Azure。</span><span class="sxs-lookup"><span data-stu-id="2042f-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="2042f-154">[**Get AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello 屬性的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2042f-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="2042f-155">您可以使用 hello [ **Write-output** ](https://technet.microsoft.com/library/hh849921.aspx)活動 toooutput hello 虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="2042f-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="2042f-156">hello 活動**Get AzureRmVm**接受兩個參數，hello**虛擬機器名稱**和 hello**資源群組名稱**。</span><span class="sxs-lookup"><span data-stu-id="2042f-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="2042f-157">由於每次啟動 hello runbook 時，這些參數可能需要不同的值，您可以加入輸入的參數 tooyour runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="2042f-158">以下是 hello 步驟 tooadd 輸入的參數：</span><span class="sxs-lookup"><span data-stu-id="2042f-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="2042f-159">選取 hello hello 從圖形化 runbook **Runbook**刀鋒視窗，然後按一下[**編輯**](automation-graphical-authoring-intro.md)它。</span><span class="sxs-lookup"><span data-stu-id="2042f-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="2042f-160">從 hello runbook 編輯器中，按一下 **輸入和輸出**tooopen hello**輸入和輸出**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2042f-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![自動化圖形化 Runbook](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="2042f-162">hello**輸入和輸出**刀鋒視窗會顯示 hello runbook 所定義的輸入參數的清單。</span><span class="sxs-lookup"><span data-stu-id="2042f-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="2042f-163">在這個刀鋒視窗中，您可以加入新的輸入的參數，或編輯現有輸入參數的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="2042f-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="2042f-164">按一下 tooadd hello runbook 的新參數**加入輸入**tooopen hello **Runbook 輸入的參數**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2042f-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="2042f-165">您可以設定下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="2042f-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="2042f-166">**屬性**</span><span class="sxs-lookup"><span data-stu-id="2042f-166">**Property**</span></span> | <span data-ttu-id="2042f-167">**說明**</span><span class="sxs-lookup"><span data-stu-id="2042f-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2042f-168">名稱</span><span class="sxs-lookup"><span data-stu-id="2042f-168">Name</span></span> |<span data-ttu-id="2042f-169">必要。</span><span class="sxs-lookup"><span data-stu-id="2042f-169">Required.</span></span>  <span data-ttu-id="2042f-170">hello hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="2042f-170">hello name of hello parameter.</span></span> <span data-ttu-id="2042f-171">這必須 hello runbook 內是唯一的可包含字母、 數字或底線字元。</span><span class="sxs-lookup"><span data-stu-id="2042f-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="2042f-172">而且必須以字母開頭。</span><span class="sxs-lookup"><span data-stu-id="2042f-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="2042f-173">說明</span><span class="sxs-lookup"><span data-stu-id="2042f-173">Description</span></span> |<span data-ttu-id="2042f-174">選用。</span><span class="sxs-lookup"><span data-stu-id="2042f-174">Optional.</span></span> <span data-ttu-id="2042f-175">關於 hello 目的輸入參數的描述。</span><span class="sxs-lookup"><span data-stu-id="2042f-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="2042f-176">類型</span><span class="sxs-lookup"><span data-stu-id="2042f-176">Type</span></span> |<span data-ttu-id="2042f-177">選用。</span><span class="sxs-lookup"><span data-stu-id="2042f-177">Optional.</span></span> <span data-ttu-id="2042f-178">hello 應有 hello 參數值的資料類型。</span><span class="sxs-lookup"><span data-stu-id="2042f-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="2042f-179">支援的參數類型有：**String**、**Int32**、**Int64**、**Decimal**、**Boolean**、**DateTime**、**Object**。</span><span class="sxs-lookup"><span data-stu-id="2042f-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="2042f-180">如果未選取的資料類型，則預設太**字串**。</span><span class="sxs-lookup"><span data-stu-id="2042f-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="2042f-181">強制</span><span class="sxs-lookup"><span data-stu-id="2042f-181">Mandatory</span></span> |<span data-ttu-id="2042f-182">選用。</span><span class="sxs-lookup"><span data-stu-id="2042f-182">Optional.</span></span> <span data-ttu-id="2042f-183">指定是否必須提供 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="2042f-184">如果您選擇**是**，然後 hello runbook 啟動時，就必須提供值。</span><span class="sxs-lookup"><span data-stu-id="2042f-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="2042f-185">如果您選擇**沒有**，然後 hello runbook 已啟動，且可能會設定預設值時，不需要值。</span><span class="sxs-lookup"><span data-stu-id="2042f-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="2042f-186">預設值</span><span class="sxs-lookup"><span data-stu-id="2042f-186">Default Value</span></span> |<span data-ttu-id="2042f-187">選用。</span><span class="sxs-lookup"><span data-stu-id="2042f-187">Optional.</span></span> <span data-ttu-id="2042f-188">指定如果傳入的值不是 hello runbook 啟動時將用於 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="2042f-189">不是強制性的參數可以設定預設值。</span><span class="sxs-lookup"><span data-stu-id="2042f-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="2042f-190">預設值，tooset 選擇**自訂**。</span><span class="sxs-lookup"><span data-stu-id="2042f-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="2042f-191">除非另一個值中有提供 hello runbook 啟動時，會使用此值。</span><span class="sxs-lookup"><span data-stu-id="2042f-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="2042f-192">選擇**無**如果您不想 tooprovide 任何預設值。</span><span class="sxs-lookup"><span data-stu-id="2042f-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![加入新的輸入](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="2042f-194">建立兩個參數具有下列屬性，將由 hello hello **Get AzureRmVm**活動：</span><span class="sxs-lookup"><span data-stu-id="2042f-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="2042f-195">**參數1：**</span><span class="sxs-lookup"><span data-stu-id="2042f-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="2042f-196">Name - VMName</span><span class="sxs-lookup"><span data-stu-id="2042f-196">Name - VMName</span></span>
     * <span data-ttu-id="2042f-197">Type - String</span><span class="sxs-lookup"><span data-stu-id="2042f-197">Type - String</span></span>
     * <span data-ttu-id="2042f-198">Mandatory - No</span><span class="sxs-lookup"><span data-stu-id="2042f-198">Mandatory - No</span></span>
   * <span data-ttu-id="2042f-199">**參數 2：**</span><span class="sxs-lookup"><span data-stu-id="2042f-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="2042f-200">Name - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2042f-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="2042f-201">Type - String</span><span class="sxs-lookup"><span data-stu-id="2042f-201">Type - String</span></span>
     * <span data-ttu-id="2042f-202">Mandatory - No</span><span class="sxs-lookup"><span data-stu-id="2042f-202">Mandatory - No</span></span>
     * <span data-ttu-id="2042f-203">Default value - Custom</span><span class="sxs-lookup"><span data-stu-id="2042f-203">Default value - Custom</span></span>
     * <span data-ttu-id="2042f-204">自訂的預設值- \<hello 包含 hello 虛擬機器的資源群組名稱 ></span><span class="sxs-lookup"><span data-stu-id="2042f-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="2042f-205">一旦您加入 hello 參數，請按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="2042f-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="2042f-206">您現在可以檢視它們在 hello**輸入和輸出刀鋒視窗**。</span><span class="sxs-lookup"><span data-stu-id="2042f-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="2042f-207">再按一下 確定，然後按一下儲存 並 發佈 您的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="2042f-208">在 runbook 中的 tooinput 參數指派值</span><span class="sxs-lookup"><span data-stu-id="2042f-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="2042f-209">您可以在 hello 下列案例中的 runbook 中傳遞值 tooinput 參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="2042f-210">啟動 Runbook 並指派參數</span><span class="sxs-lookup"><span data-stu-id="2042f-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="2042f-211">Runbook 可以啟動許多方法： 透過 Azure 入口網站，使用 webhook、 PowerShell cmdlet，以 hello REST API 或 hello SDK hello。</span><span class="sxs-lookup"><span data-stu-id="2042f-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="2042f-212">以下我們將討論啟動 Runbook 並指派參數的不同方法。</span><span class="sxs-lookup"><span data-stu-id="2042f-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="2042f-213">開始使用 hello Azure 入口網站已發佈的 runbook 和指派的參數</span><span class="sxs-lookup"><span data-stu-id="2042f-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="2042f-214">當您[啟動 hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal)，hello**啟動 Runbook**刀鋒視窗隨即開啟，而且您可以設定您剛才建立的 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![開始使用 hello 入口網站](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="2042f-216">在 hello hello 輸入方塊下方的標籤，您可以看到 hello hello 參數已設定的屬性。</span><span class="sxs-lookup"><span data-stu-id="2042f-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="2042f-217">這些屬性包括強制或選擇性、類型和預設值。</span><span class="sxs-lookup"><span data-stu-id="2042f-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="2042f-218">在 hello 說明提示氣球下一步 toohello 參數名稱，您可以看到所有您需要 toomake 參數輸入值來判斷 hello 金鑰資訊。</span><span class="sxs-lookup"><span data-stu-id="2042f-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="2042f-219">此資訊包括參數為強制或選擇性。</span><span class="sxs-lookup"><span data-stu-id="2042f-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="2042f-220">它也包含 hello 類型和預設值 （如果有的話） 和其他有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="2042f-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![說明提示氣球](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="2042f-222">字串類型參數支援 **空** 字串值。</span><span class="sxs-lookup"><span data-stu-id="2042f-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="2042f-223">輸入**[EmptyString]**在 hello 輸入參數 方塊中會傳遞空字串 toohello 參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="2042f-224">此外，字串類型參數不支援傳遞 **Null** 值。</span><span class="sxs-lookup"><span data-stu-id="2042f-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="2042f-225">如果您沒有傳遞任何值 toohello 字串參數，然後 PowerShell 會解譯為 null。</span><span class="sxs-lookup"><span data-stu-id="2042f-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="2042f-226">使用 PowerShell Cmdlet 啟動已發佈的 Runbook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="2042f-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="2042f-227">**Azure Resource Manager Cmdlet：** 您可以使用 [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)啟動在資源群組中建立的自動化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="2042f-228">**範例：**</span><span class="sxs-lookup"><span data-stu-id="2042f-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="2042f-229">**Azure 服務管理 Cmdlet：** 您可以使用 [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx)啟動在預設資源群組中建立的自動化 Runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="2042f-230">**範例：**</span><span class="sxs-lookup"><span data-stu-id="2042f-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="2042f-231">當您使用 PowerShell cmdlet，預設參數，來啟動 runbook **MicrosoftApplicationManagementStartedBy**使用 hello 值建立**PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="2042f-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="2042f-232">您可以檢視此參數在 hello**作業詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2042f-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="2042f-233">使用 SDK 啟動 Runbook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="2042f-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="2042f-234">**Azure 資源管理員的方法：**您可以使用 hello SDK 的程式設計語言來啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="2042f-235">以下 C# 程式碼片段用於在您的自動化帳戶中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="2042f-236">您可以檢視所有 hello 程式碼，在我們[GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)。</span><span class="sxs-lookup"><span data-stu-id="2042f-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="2042f-237">**Azure 服務管理方法：**您可以使用 hello SDK 的程式設計語言來啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="2042f-238">以下 C# 程式碼片段用於在您的自動化帳戶中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="2042f-239">您可以檢視所有 hello 程式碼，在我們[GitHub 儲存機制](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs)。</span><span class="sxs-lookup"><span data-stu-id="2042f-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="2042f-240">toostart 這種方法，建立 runbook 參數的字典 toostore hello **VMName**和**resourceGroupName**，和它們的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="2042f-241">然後啟動 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="2042f-241">Then start hello runbook.</span></span> <span data-ttu-id="2042f-242">以下是呼叫 hello 方法，定義於上方的 hello C# 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="2042f-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="2042f-243">啟動 runbook 使用 hello REST API 和指派的參數</span><span class="sxs-lookup"><span data-stu-id="2042f-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="2042f-244">Runbook 作業可建立及啟動以 hello Azure 自動化 REST API 使用 hello**放**以 hello 遵循方法要求 URI。</span><span class="sxs-lookup"><span data-stu-id="2042f-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="2042f-245">Hello 要求 URI 中取代 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="2042f-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="2042f-246">**subscription-id：** 您的 Azure 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="2042f-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="2042f-247">**雲端服務名稱：**應該傳送嗨雲端服務 toowhich hello 要求 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2042f-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="2042f-248">**自動化帳戶名稱：** hello 您裝載於 hello 的自動化帳戶名稱指定雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2042f-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="2042f-249">**作業識別碼：** hello hello 工作的 GUID。</span><span class="sxs-lookup"><span data-stu-id="2042f-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="2042f-250">在 PowerShell 中的 Guid 可以建立使用 hello **[GUID]::NewGuid()。Tostring （)**命令。</span><span class="sxs-lookup"><span data-stu-id="2042f-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="2042f-251">在訂單 toopass 參數 toohello runbook 工作，使用 hello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="2042f-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="2042f-252">它會採用下列 JSON 格式中提供的兩個屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="2042f-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="2042f-253">**Runbook 名稱：** 必要。</span><span class="sxs-lookup"><span data-stu-id="2042f-253">**Runbook name:** Required.</span></span> <span data-ttu-id="2042f-254">hello 作業 toostart hello hello runbook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="2042f-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="2042f-255">**Runbook 參數：** 選擇性。</span><span class="sxs-lookup"><span data-stu-id="2042f-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="2042f-256">字典 （名稱、 值） 中的 hello 參數清單的格式，其中名稱必須是字串型別和值可以是任何有效的 JSON 值。</span><span class="sxs-lookup"><span data-stu-id="2042f-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="2042f-257">如果您想 toostart hello **Get AzureVMTextual**稍早建立的 runbook **VMName**和**resourceGroupName**做為參數，使用下列 JSON 格式的 hellohello 要求主體。</span><span class="sxs-lookup"><span data-stu-id="2042f-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

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

<span data-ttu-id="2042f-258">如果 hello 工作成功建立，則會傳回 HTTP 狀態碼 「 201。</span><span class="sxs-lookup"><span data-stu-id="2042f-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="2042f-259">如需有關回應標頭和 hello 回應主體的詳細資訊，請參閱有關 toohello 文章太[使用 hello REST API 來建立 runbook 作業。](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="2042f-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="2042f-260">測試 Runbook 並指派參數</span><span class="sxs-lookup"><span data-stu-id="2042f-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="2042f-261">當您[測試 hello 草稿版本，您的 runbook 的](automation-testing-runbook.md)使用 hello 測試選項，hello**測試**刀鋒視窗隨即開啟，而且您可以設定您剛才建立的 hello 參數的值。</span><span class="sxs-lookup"><span data-stu-id="2042f-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![測試並指派參數](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="2042f-263">排程 tooa runbook 連結和指派的參數</span><span class="sxs-lookup"><span data-stu-id="2042f-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="2042f-264">您可以[將排程連結](automation-schedules.md)tooyour runbook 讓該 hello runbook 在特定時間啟動。</span><span class="sxs-lookup"><span data-stu-id="2042f-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="2042f-265">當您建立 hello 排程並 hello runbook 將會使用這些值，hello 排程啟動時，您會指定輸入的參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="2042f-266">提供所有必要的參數值之前，您無法儲存 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="2042f-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![排程並指派參數](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="2042f-268">建立 Runbook 的 Webhook，並指派參數</span><span class="sxs-lookup"><span data-stu-id="2042f-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="2042f-269">您可以為您的 Runbook 建立 [Webhook](automation-webhooks.md) ，並設定 Runbook 輸入參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="2042f-270">提供所有必要的參數值之前，您無法儲存 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="2042f-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![建立 Webhook 並指派參數](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="2042f-272">當您使用 webhook 執行 runbook 時，hello 預先定義的輸入的參數 **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** 傳送，以及您定義的 hello 輸入參數。</span><span class="sxs-lookup"><span data-stu-id="2042f-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="2042f-273">您可以按一下 tooexpand hello **WebhookData**參數，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="2042f-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![WebhookData 參數](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="2042f-275">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2042f-275">Next steps</span></span>
* <span data-ttu-id="2042f-276">如需關於 Runbook 輸入和輸出的詳細資訊，請參閱 [Azure 自動化：Runbook 輸入、輸出和巢狀 Runbook](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)。</span><span class="sxs-lookup"><span data-stu-id="2042f-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="2042f-277">如需不同的方式 toostart runbook 的詳細資訊，請參閱[啟動 runbook](automation-starting-a-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="2042f-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="2042f-278">tooedit 文字的 runbook，請參閱太[編輯文字的 runbook](automation-edit-textual-runbook.md)。</span><span class="sxs-lookup"><span data-stu-id="2042f-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="2042f-279">tooedit 圖形化 runbook，請參閱太[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="2042f-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

