---
title: "aaaCreating 管理解決方案中 Operations Management Suite (OMS) |Microsoft 文件"
description: "管理解決方案會擴充 hello 功能 Operations Management Suite (OMS) 藉由提供封裝的管理案例，客戶可以加入 tootheir OMS 工作區。  本文章提供有關如何建立管理方案 toobe 您自己的環境中使用，或進行可用 tooyour 客戶。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1915e204-ba7e-431b-9718-9eb6b4213ad8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/30/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f408df1b21f519fd1eb2cbeb19cca18f6c4161f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="35a7a-104">在 Operations Management Suite (OMS) 中建立管理解決方案檔 (預覽)</span><span class="sxs-lookup"><span data-stu-id="35a7a-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="35a7a-105">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="35a7a-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="35a7a-106">如下所述的任何結構描述是主體 toochange。</span><span class="sxs-lookup"><span data-stu-id="35a7a-106">Any schema described below is subject toochange.</span></span>  

<span data-ttu-id="35a7a-107">Operations Management Suite (OMS) 中的管理解決方案會實作為 [Resource Manager 範本](../azure-resource-manager/resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="35a7a-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="35a7a-108">學習如何 tooauthor 管理解決方案了解如何太 hello 主要工作[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="35a7a-108">hello main task in learning how tooauthor management solutions is learning how too[author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="35a7a-109">本文章提供唯一的方案使用的範本的詳細資料以及如何 tooconfigure 一般解決方案資源。</span><span class="sxs-lookup"><span data-stu-id="35a7a-109">This article provides unique details of templates used for solutions and how tooconfigure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="35a7a-110">工具</span><span class="sxs-lookup"><span data-stu-id="35a7a-110">Tools</span></span>

<span data-ttu-id="35a7a-111">您可以使用任何文字編輯器 toowork 方案檔，但我們建議您利用 hello hello 下列文章中所述，Visual Studio 或 Visual Studio 程式碼中所提供的功能。</span><span class="sxs-lookup"><span data-stu-id="35a7a-111">You can use any text editor toowork with solution files, but we recommend leveraging hello features provided in Visual Studio or Visual Studio Code as described in hello following articles.</span></span>

- [<span data-ttu-id="35a7a-112">透過 Visual Studio 建立與部署 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="35a7a-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="35a7a-113">在 Visual Studio Code 中使用 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="35a7a-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="35a7a-114">Structure</span><span class="sxs-lookup"><span data-stu-id="35a7a-114">Structure</span></span>
<span data-ttu-id="35a7a-115">hello 管理方案檔案的基本結構是 hello 與相同[Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md#template-format)即，如下所示。</span><span class="sxs-lookup"><span data-stu-id="35a7a-115">hello basic structure of a management solution file is hello same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="35a7a-116">每個 hello 的以下各節說明 hello 最上層項目和方案中及其內容。</span><span class="sxs-lookup"><span data-stu-id="35a7a-116">Each of hello sections below describes hello top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="35a7a-117">參數</span><span class="sxs-lookup"><span data-stu-id="35a7a-117">Parameters</span></span>
<span data-ttu-id="35a7a-118">[參數](../azure-resource-manager/resource-group-authoring-templates.md#parameters)是在安裝 hello 管理解決方案時，您需要從 hello 使用者的值。</span><span class="sxs-lookup"><span data-stu-id="35a7a-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from hello user when they install hello management solution.</span></span>  <span data-ttu-id="35a7a-119">所有解決方案都會有標準參數，而您可以視需要針對特定解決方案新增額外的參數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="35a7a-120">使用者如何提供使用者安裝方案的參數值將取決於 hello 特定參數，並安裝 hello 方案方式。</span><span class="sxs-lookup"><span data-stu-id="35a7a-120">How users will provide parameter values when they install your solution will depend on hello particular parameter and how hello solution is being installed.</span></span>

<span data-ttu-id="35a7a-121">當使用者安裝您的管理解決方案，透過 hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions)或[Azure 快速入門範本](operations-management-suite-solutions.md#finding-and-installing-management-solutions)它們是提示的 tooselect [OMS 工作區以及自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span><span class="sxs-lookup"><span data-stu-id="35a7a-121">When a user installs your management solution through hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted tooselect an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="35a7a-122">這些是使用的 toopopulate hello 值的每個 hello 標準參數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-122">These are used toopopulate hello values of each of hello standard parameters.</span></span>  <span data-ttu-id="35a7a-123">不會提示使用者 hello toodirectly hello 標準的參數提供值，但是可以提示的 tooprovide 值的任何其他參數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-123">hello user is not prompted toodirectly provide values for hello standard parameters, but they are prompted tooprovide values for any additional parameters.</span></span>

<span data-ttu-id="35a7a-124">Hello 使用者安裝方案時[另一種方法](operations-management-suite-solutions.md#finding-and-installing-management-solutions)，他們必須為所有標準的參數和所有其他參數提供值。</span><span class="sxs-lookup"><span data-stu-id="35a7a-124">When hello user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="35a7a-125">範例參數如下所示。</span><span class="sxs-lookup"><span data-stu-id="35a7a-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="35a7a-126">hello 下表描述 hello 參數屬性。</span><span class="sxs-lookup"><span data-stu-id="35a7a-126">hello following table describes hello attributes of a parameter.</span></span>

| <span data-ttu-id="35a7a-127">屬性</span><span class="sxs-lookup"><span data-stu-id="35a7a-127">Attribute</span></span> | <span data-ttu-id="35a7a-128">說明</span><span class="sxs-lookup"><span data-stu-id="35a7a-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="35a7a-129">類型</span><span class="sxs-lookup"><span data-stu-id="35a7a-129">type</span></span> |<span data-ttu-id="35a7a-130">Hello 參數的資料類型。</span><span class="sxs-lookup"><span data-stu-id="35a7a-130">Data type for hello parameter.</span></span> <span data-ttu-id="35a7a-131">hello 輸入的控制項顯示 hello 使用者 hello 資料類型而定。</span><span class="sxs-lookup"><span data-stu-id="35a7a-131">hello input control displayed for hello user depends on hello data type.</span></span><br><br><span data-ttu-id="35a7a-132">bool - 下拉式方塊</span><span class="sxs-lookup"><span data-stu-id="35a7a-132">bool - Drop down box</span></span><br><span data-ttu-id="35a7a-133">string - 文字方塊</span><span class="sxs-lookup"><span data-stu-id="35a7a-133">string - Text box</span></span><br><span data-ttu-id="35a7a-134">int - 文字方塊</span><span class="sxs-lookup"><span data-stu-id="35a7a-134">int - Text box</span></span><br><span data-ttu-id="35a7a-135">securestring - 密碼欄位</span><span class="sxs-lookup"><span data-stu-id="35a7a-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="35a7a-136">category</span><span class="sxs-lookup"><span data-stu-id="35a7a-136">category</span></span> |<span data-ttu-id="35a7a-137">Hello 參數的選擇性類別目錄。</span><span class="sxs-lookup"><span data-stu-id="35a7a-137">Optional category for hello parameter.</span></span>  <span data-ttu-id="35a7a-138">在相同類別目錄群組在一起的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-138">Parameters in hello same category are grouped together.</span></span> |
| <span data-ttu-id="35a7a-139">control</span><span class="sxs-lookup"><span data-stu-id="35a7a-139">control</span></span> |<span data-ttu-id="35a7a-140">string 參數的其他功能。</span><span class="sxs-lookup"><span data-stu-id="35a7a-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="35a7a-141">datetime - Datetime 控制項隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="35a7a-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="35a7a-142">自動產生的 guid-Guid 值，並不會顯示 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-142">guid - Guid value is automatically generated, and hello parameter is not displayed.</span></span> |
| <span data-ttu-id="35a7a-143">說明</span><span class="sxs-lookup"><span data-stu-id="35a7a-143">description</span></span> |<span data-ttu-id="35a7a-144">Hello 參數的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="35a7a-144">Optional description for hello parameter.</span></span>  <span data-ttu-id="35a7a-145">顯示資訊提示氣球下一步 toohello 參數中。</span><span class="sxs-lookup"><span data-stu-id="35a7a-145">Displayed in an information balloon next toohello parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="35a7a-146">標準參數</span><span class="sxs-lookup"><span data-stu-id="35a7a-146">Standard parameters</span></span>
<span data-ttu-id="35a7a-147">hello 下表列出所有的管理解決方案的 hello 標準參數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-147">hello following table lists hello standard parameters for all management solutions.</span></span>  <span data-ttu-id="35a7a-148">Hello 使用者，而不是提示認證從 hello Azure Marketplace 或快速入門範本安裝方案時，會填入這些值。</span><span class="sxs-lookup"><span data-stu-id="35a7a-148">These values are populated for hello user instead of prompting for them when your solution is installed from hello Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="35a7a-149">hello 使用者必須為它們提供值，如果 hello 方案已安裝另一個方法。</span><span class="sxs-lookup"><span data-stu-id="35a7a-149">hello user must provide values for them if hello solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="35a7a-150">hello hello Azure Marketplace] 和 [快速入門範本中的使用者介面 hello 資料表中預期 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="35a7a-150">hello user interface in hello Azure Marketplace and Quickstart templates is expecting hello parameter names in hello table.</span></span>  <span data-ttu-id="35a7a-151">如果您使用不同的參數名稱，然後將提示 hello 使用者，它們不會自動填入。</span><span class="sxs-lookup"><span data-stu-id="35a7a-151">If you use different parameter names then hello user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="35a7a-152">參數</span><span class="sxs-lookup"><span data-stu-id="35a7a-152">Parameter</span></span> | <span data-ttu-id="35a7a-153">類型</span><span class="sxs-lookup"><span data-stu-id="35a7a-153">Type</span></span> | <span data-ttu-id="35a7a-154">說明</span><span class="sxs-lookup"><span data-stu-id="35a7a-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="35a7a-155">accountName</span><span class="sxs-lookup"><span data-stu-id="35a7a-155">accountName</span></span> |<span data-ttu-id="35a7a-156">string</span><span class="sxs-lookup"><span data-stu-id="35a7a-156">string</span></span> |<span data-ttu-id="35a7a-157">Azure 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="35a7a-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="35a7a-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="35a7a-158">pricingTier</span></span> |<span data-ttu-id="35a7a-159">字串</span><span class="sxs-lookup"><span data-stu-id="35a7a-159">string</span></span> |<span data-ttu-id="35a7a-160">Log Analytics 工作區和 Azure 自動化帳戶的定價層。</span><span class="sxs-lookup"><span data-stu-id="35a7a-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="35a7a-161">regionId</span><span class="sxs-lookup"><span data-stu-id="35a7a-161">regionId</span></span> |<span data-ttu-id="35a7a-162">字串</span><span class="sxs-lookup"><span data-stu-id="35a7a-162">string</span></span> |<span data-ttu-id="35a7a-163">Hello Azure 自動化帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="35a7a-163">Region of hello Azure Automation account.</span></span> |
| <span data-ttu-id="35a7a-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="35a7a-164">solutionName</span></span> |<span data-ttu-id="35a7a-165">字串</span><span class="sxs-lookup"><span data-stu-id="35a7a-165">string</span></span> |<span data-ttu-id="35a7a-166">Hello 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="35a7a-166">Name of hello solution.</span></span>  <span data-ttu-id="35a7a-167">如果您要部署您的解決方案，透過快速入門範本，然後您應該定義 solutionName 做為參數讓您定義字串，而需要 hello 使用者 toospecify 其中一個。</span><span class="sxs-lookup"><span data-stu-id="35a7a-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring hello user toospecify one.</span></span> |
| <span data-ttu-id="35a7a-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="35a7a-168">workspaceName</span></span> |<span data-ttu-id="35a7a-169">字串</span><span class="sxs-lookup"><span data-stu-id="35a7a-169">string</span></span> |<span data-ttu-id="35a7a-170">Log Analytics 工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="35a7a-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="35a7a-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="35a7a-171">workspaceRegionId</span></span> |<span data-ttu-id="35a7a-172">字串</span><span class="sxs-lookup"><span data-stu-id="35a7a-172">string</span></span> |<span data-ttu-id="35a7a-173">Hello 記錄分析工作區的區域。</span><span class="sxs-lookup"><span data-stu-id="35a7a-173">Region of hello Log Analytics workspace.</span></span> |


<span data-ttu-id="35a7a-174">以下是 hello 結構 hello 標準參數，您可以複製並貼到您的方案檔。</span><span class="sxs-lookup"><span data-stu-id="35a7a-174">Following is hello structure of hello standard parameters that you can copy and paste into your solution file.</span></span>  

    "parameters": {
        "workspaceName": {
            "type": "string",
            "metadata": {
                "description": "A valid Log Analytics workspace name"
            }
        },
        "accountName": {
               "type": "string",
               "metadata": {
                   "description": "A valid Azure Automation account name"
               }
        },
        "workspaceRegionId": {
               "type": "string",
               "metadata": {
                   "description": "Region of hello Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of hello Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="35a7a-175">參照與 hello 語法 hello 解決方案的其他項目中的 tooparameter 值**參數 ('parameter name')**。</span><span class="sxs-lookup"><span data-stu-id="35a7a-175">You refer tooparameter values in other elements of hello solution with hello syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="35a7a-176">例如，tooaccess hello 工作區名稱，您會使用**parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="35a7a-176">For example, tooaccess hello workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="35a7a-177">變數</span><span class="sxs-lookup"><span data-stu-id="35a7a-177">Variables</span></span>
<span data-ttu-id="35a7a-178">[變數](../azure-resource-manager/resource-group-authoring-templates.md#variables)是您將使用中的 hello 管理解決方案的 hello 其餘部分的值。</span><span class="sxs-lookup"><span data-stu-id="35a7a-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in hello rest of hello management solution.</span></span>  <span data-ttu-id="35a7a-179">這些值不公開的 toohello 使用者安裝 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="35a7a-179">These values are not exposed toohello user installing hello solution.</span></span>  <span data-ttu-id="35a7a-180">它們是預定的 tooprovide hello 作者與單一位置，讓他們可以管理整個 hello 方案可能會重複使用的值。</span><span class="sxs-lookup"><span data-stu-id="35a7a-180">They are intended tooprovide hello author with a single location where they can manage values that may be used multiple times throughout hello solution.</span></span> <span data-ttu-id="35a7a-181">您應該將任何值的特定 tooyour 解決方案放在變數為相對於 toohard 加以 hello**資源**項目。</span><span class="sxs-lookup"><span data-stu-id="35a7a-181">You should put any values specific tooyour solution in variables as opposed toohard coding them in hello **resources** element.</span></span>  <span data-ttu-id="35a7a-182">這會使 hello 程式碼更容易閱讀，並可讓您 tooeasily 變更這些更新版本中的值。</span><span class="sxs-lookup"><span data-stu-id="35a7a-182">This makes hello code more readable and allows you tooeasily change these values in later versions.</span></span>

<span data-ttu-id="35a7a-183">下列範例為 **variables** 項目，包含解決方案中所使用的一般參數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="35a7a-184">參考透過 hello 解決方案與 hello 語法 toovariable 值**變數 ('variable name')**。</span><span class="sxs-lookup"><span data-stu-id="35a7a-184">You refer toovariable values through hello solution with hello syntax **variables('variable name')**.</span></span>  <span data-ttu-id="35a7a-185">例如，tooaccess hello SolutionName 變數，您會使用**variables('SolutionName')**。</span><span class="sxs-lookup"><span data-stu-id="35a7a-185">For example, tooaccess hello SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="35a7a-186">您也可以定義有多組值的複雜變數。</span><span class="sxs-lookup"><span data-stu-id="35a7a-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="35a7a-187">這在您會針對不同的資源類型定義多個屬性的管理解決方案中，這特別實用。</span><span class="sxs-lookup"><span data-stu-id="35a7a-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="35a7a-188">例如，您無法重建 hello 方案變數 toohello 下列如上所示。</span><span class="sxs-lookup"><span data-stu-id="35a7a-188">For example, you could restructure hello solution variables shown above toohello following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="35a7a-189">在此情況下，請參閱 toovariable 值透過 hello 解決方案與 hello 語法**variables('variable name').property**。</span><span class="sxs-lookup"><span data-stu-id="35a7a-189">In this case, you refer toovariable values through hello solution with hello syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="35a7a-190">例如，tooaccess hello 方案名稱變數，您會使用**variables('Solution')。名稱**。</span><span class="sxs-lookup"><span data-stu-id="35a7a-190">For example, tooaccess hello Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="35a7a-191">資源</span><span class="sxs-lookup"><span data-stu-id="35a7a-191">Resources</span></span>
<span data-ttu-id="35a7a-192">[資源](../azure-resource-manager/resource-group-authoring-templates.md#resources)hello 不同，定義資源管理解決方案將會安裝及設定。</span><span class="sxs-lookup"><span data-stu-id="35a7a-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define hello different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="35a7a-193">這會是最大的 hello 和 hello 範本最複雜部分。</span><span class="sxs-lookup"><span data-stu-id="35a7a-193">This will be hello largest and most complex portion of hello template.</span></span>  <span data-ttu-id="35a7a-194">您可以取得 hello 結構和資源項目中的完整描述[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md#resources)。</span><span class="sxs-lookup"><span data-stu-id="35a7a-194">You can get hello structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="35a7a-195">本文件中的其他文章會詳述您經常定義的其他資源。</span><span class="sxs-lookup"><span data-stu-id="35a7a-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="35a7a-196">相依項目</span><span class="sxs-lookup"><span data-stu-id="35a7a-196">Dependencies</span></span>
<span data-ttu-id="35a7a-197">hello **dependsOn**項目指定[相依性](../azure-resource-manager/resource-group-define-dependencies.md)於另一個資源。</span><span class="sxs-lookup"><span data-stu-id="35a7a-197">hello **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="35a7a-198">安裝 hello 方案時，在建立及其所有相依性之前，將不會建立資源。</span><span class="sxs-lookup"><span data-stu-id="35a7a-198">When hello solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="35a7a-199">例如，解決方案可能會在使用[作業資源](operations-management-suite-solutions-resources-automation.md#automation-jobs)安裝時[啟動 Runbook](operations-management-suite-solutions-resources-automation.md#runbooks)。</span><span class="sxs-lookup"><span data-stu-id="35a7a-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="35a7a-200">hello 作業資源會相依於 hello runbook 資源 toomake 確定建立 hello 作業之前，已建立該 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="35a7a-200">hello job resource would be dependent on hello runbook resource toomake sure that hello runbook is created before hello job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="35a7a-201">OMS 工作區和自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="35a7a-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="35a7a-202">管理解決方案需要[OMS 工作區](../log-analytics/log-analytics-manage-access.md)toocontain 檢視和[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)toocontain runbook 和相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="35a7a-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) toocontain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks and related resources.</span></span>  <span data-ttu-id="35a7a-203">這些都必須可用後再 hello hello 方案中的資源建立和不應在 hello 方案本身中定義。</span><span class="sxs-lookup"><span data-stu-id="35a7a-203">These must be available before hello resources in hello solution are created and should not be defined in hello solution itself.</span></span>  <span data-ttu-id="35a7a-204">hello 使用者將[指定工作區和帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)當他們部署您的方案，但身 hello 作者，您應該考慮下列點 hello。</span><span class="sxs-lookup"><span data-stu-id="35a7a-204">hello user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as hello author you should consider hello following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="35a7a-205">解決方案資源</span><span class="sxs-lookup"><span data-stu-id="35a7a-205">Solution resource</span></span>
<span data-ttu-id="35a7a-206">每個解決方案需要資源中的項目 hello**資源**定義本身 hello 方案項目。</span><span class="sxs-lookup"><span data-stu-id="35a7a-206">Each solution requires a resource entry in hello **resources** element that defines hello solution itself.</span></span>  <span data-ttu-id="35a7a-207">這會有一種**Microsoft.OperationsManagement/solutions**而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="35a7a-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have hello following structure.</span></span> <span data-ttu-id="35a7a-208">這包括[標準參數](#parameters)和[變數](#variables)所 hello 解決方案的常用的 toodefine 屬性。</span><span class="sxs-lookup"><span data-stu-id="35a7a-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used toodefine properties of hello solution.</span></span>


    {
      "name": "[concat(variables('Solution').Name, '[' ,parameters('workspacename'), ']')]",
      "location": "[parameters('workspaceRegionId')]",
      "tags": { },
      "type": "Microsoft.OperationsManagement/solutions",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
        <list-of-resources>
      ],
      "properties": {
        "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
        "referencedResources": [
            <list-of-referenced-resources>
        ],
        "containedResources": [
            <list-of-contained-resources>
        ]
      },
      "plan": {
        "name": "[concat(variables('Solution').Name, '[' ,parameters('workspaceName'), ']')]",
        "Version": "[variables('Solution').Version]",
        "product": "[variables('ProductName')]",
        "publisher": "[variables('Solution').Publisher]",
        "promotionCode": ""
      }
    }




### <a name="dependencies"></a><span data-ttu-id="35a7a-209">相依項目</span><span class="sxs-lookup"><span data-stu-id="35a7a-209">Dependencies</span></span>
<span data-ttu-id="35a7a-210">hello 方案資源必須[相依性](../azure-resource-manager/resource-group-define-dependencies.md)hello 方案，因為他們需要 tooexist 才能建立 hello 方案中的每個其他資源。</span><span class="sxs-lookup"><span data-stu-id="35a7a-210">hello solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in hello solution since they need tooexist before hello solution can be created.</span></span>  <span data-ttu-id="35a7a-211">您可以新增項目之每個資源 hello **dependsOn**項目。</span><span class="sxs-lookup"><span data-stu-id="35a7a-211">You do this by adding an entry for each resource in hello **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="35a7a-212">屬性</span><span class="sxs-lookup"><span data-stu-id="35a7a-212">Properties</span></span>
<span data-ttu-id="35a7a-213">hello 方案資源有下表中的 hello hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="35a7a-213">hello solution resource has hello properties in hello following table.</span></span>  <span data-ttu-id="35a7a-214">這包括 hello 參考，而且會定義安裝 hello 方案之後，如何管理 hello 資源 hello 方案所包含的資源。</span><span class="sxs-lookup"><span data-stu-id="35a7a-214">This includes hello resources referenced and contained by hello solution which defines how hello resource is managed after hello solution is installed.</span></span>  <span data-ttu-id="35a7a-215">Hello 方案中的每個資源應該會列在任一個 hello **referencedResources**或 hello **containedResources**屬性。</span><span class="sxs-lookup"><span data-stu-id="35a7a-215">Each resource in hello solution should be listed in either hello **referencedResources** or hello **containedResources** property.</span></span>

| <span data-ttu-id="35a7a-216">屬性</span><span class="sxs-lookup"><span data-stu-id="35a7a-216">Property</span></span> | <span data-ttu-id="35a7a-217">說明</span><span class="sxs-lookup"><span data-stu-id="35a7a-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="35a7a-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="35a7a-218">workspaceResourceId</span></span> |<span data-ttu-id="35a7a-219">Hello hello 表單中的記錄分析工作區的識別碼 *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<工作區名稱\>*。</span><span class="sxs-lookup"><span data-stu-id="35a7a-219">ID of hello Log Analytics workspace in hello form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="35a7a-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="35a7a-220">referencedResources</span></span> |<span data-ttu-id="35a7a-221">不應該移除 hello 方案中移除時的 hello 方案中的資源的清單。</span><span class="sxs-lookup"><span data-stu-id="35a7a-221">List of resources in hello solution that should not be removed when hello solution is removed.</span></span> |
| <span data-ttu-id="35a7a-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="35a7a-222">containedResources</span></span> |<span data-ttu-id="35a7a-223">移除 hello 方案時，應移除的 hello 方案中的資源的清單。</span><span class="sxs-lookup"><span data-stu-id="35a7a-223">List of resources in hello solution that should be removed when hello solution is removed.</span></span> |

<span data-ttu-id="35a7a-224">上述的 hello 範例適用於在方案中使用 runbook、 排程和檢視。</span><span class="sxs-lookup"><span data-stu-id="35a7a-224">hello example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="35a7a-225">hello 排程與 runbook*參考*在 hello**屬性**項目，因此不會移除 hello 方案中移除時。</span><span class="sxs-lookup"><span data-stu-id="35a7a-225">hello schedule and runbook are *referenced* in hello  **properties**  element so they are not removed when hello solution is removed.</span></span>  <span data-ttu-id="35a7a-226">hello 檢視是*包含*因此移除 hello 方案時，它會移除。</span><span class="sxs-lookup"><span data-stu-id="35a7a-226">hello view is *contained* so it is removed when hello solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="35a7a-227">規劃</span><span class="sxs-lookup"><span data-stu-id="35a7a-227">Plan</span></span>
<span data-ttu-id="35a7a-228">hello**計劃**hello 方案資源的實體有下表中的 hello hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="35a7a-228">hello **plan** entity of hello solution resource has hello properties in hello following table.</span></span>

| <span data-ttu-id="35a7a-229">屬性</span><span class="sxs-lookup"><span data-stu-id="35a7a-229">Property</span></span> | <span data-ttu-id="35a7a-230">說明</span><span class="sxs-lookup"><span data-stu-id="35a7a-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="35a7a-231">名稱</span><span class="sxs-lookup"><span data-stu-id="35a7a-231">name</span></span> |<span data-ttu-id="35a7a-232">Hello 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="35a7a-232">Name of hello solution.</span></span> |
| <span data-ttu-id="35a7a-233">版本</span><span class="sxs-lookup"><span data-stu-id="35a7a-233">version</span></span> |<span data-ttu-id="35a7a-234">Hello 方案由 hello 作者所決定的版本。</span><span class="sxs-lookup"><span data-stu-id="35a7a-234">Version of hello solution as determined by hello author.</span></span> |
| <span data-ttu-id="35a7a-235">product</span><span class="sxs-lookup"><span data-stu-id="35a7a-235">product</span></span> |<span data-ttu-id="35a7a-236">唯一字串 tooidentify hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="35a7a-236">Unique string tooidentify hello solution.</span></span> |
| <span data-ttu-id="35a7a-237">publisher</span><span class="sxs-lookup"><span data-stu-id="35a7a-237">publisher</span></span> |<span data-ttu-id="35a7a-238">Hello 方案的發行者。</span><span class="sxs-lookup"><span data-stu-id="35a7a-238">Publisher of hello solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="35a7a-239">範例</span><span class="sxs-lookup"><span data-stu-id="35a7a-239">Sample</span></span>
<span data-ttu-id="35a7a-240">您可以在下列位置的 hello 檢視與解決方案資源方案檔案的範例。</span><span class="sxs-lookup"><span data-stu-id="35a7a-240">You can view samples of solution files with a solution resource at hello following locations.</span></span>

- [<span data-ttu-id="35a7a-241">自動化資源</span><span class="sxs-lookup"><span data-stu-id="35a7a-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="35a7a-242">搜尋和警示資源</span><span class="sxs-lookup"><span data-stu-id="35a7a-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="35a7a-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35a7a-243">Next steps</span></span>
* <span data-ttu-id="35a7a-244">[新增已儲存的搜尋和警示](operations-management-suite-solutions-resources-searches-alerts.md)tooyour 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="35a7a-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) tooyour management solution.</span></span>
* <span data-ttu-id="35a7a-245">[加入檢視](operations-management-suite-solutions-resources-views.md)tooyour 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="35a7a-245">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="35a7a-246">[新增 runbook 與其他自動化資源](operations-management-suite-solutions-resources-automation.md)tooyour 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="35a7a-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>
* <span data-ttu-id="35a7a-247">瞭解 hello[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="35a7a-247">Learn hello details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="35a7a-248">搜尋 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates)不同 Resource Manager 範本的範例。</span><span class="sxs-lookup"><span data-stu-id="35a7a-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
