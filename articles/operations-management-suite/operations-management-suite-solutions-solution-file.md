---
title: "在 Operations Management Suite (OMS) 中建立管理解決方案 | Microsoft Docs"
description: "管理解決方案會藉由提供客戶可新增至他們 OMS 工作區的套件管理案例，以擴充 Operations Management Suite (OMS) 的功能。  這篇文章提供詳細資料，說明如何建立要用於自己的環境中或可供客戶使用的管理解決方案。"
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
ms.openlocfilehash: ee3462c13101d18921dc488b08c79e1e4e02ff3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a><span data-ttu-id="3c642-104">在 Operations Management Suite (OMS) 中建立管理解決方案檔 (預覽)</span><span class="sxs-lookup"><span data-stu-id="3c642-104">Creating a management solution file in Operations Management Suite (OMS) (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="3c642-105">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="3c642-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="3c642-106">以下所述的任何結構描述可能會有所變更。</span><span class="sxs-lookup"><span data-stu-id="3c642-106">Any schema described below is subject to change.</span></span>  

<span data-ttu-id="3c642-107">Operations Management Suite (OMS) 中的管理解決方案會實作為 [Resource Manager 範本](../azure-resource-manager/resource-manager-template-walkthrough.md)。</span><span class="sxs-lookup"><span data-stu-id="3c642-107">Management solutions in Operations Management Suite (OMS) are implemented as [Resource Manager templates](../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>  <span data-ttu-id="3c642-108">學習如何撰寫管理解決方案的主要工作，是學習如何[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3c642-108">The main task in learning how to author management solutions is learning how to [author a template](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>  <span data-ttu-id="3c642-109">本文提供用於解決方案的範本獨特詳細資料，以及設定一般解決方案資源的方式。</span><span class="sxs-lookup"><span data-stu-id="3c642-109">This article provides unique details of templates used for solutions and how to configure typical solution resources.</span></span>


## <a name="tools"></a><span data-ttu-id="3c642-110">工具</span><span class="sxs-lookup"><span data-stu-id="3c642-110">Tools</span></span>

<span data-ttu-id="3c642-111">您可以使用任何文字編輯器來處理解決方案檔，但建議您利用 Visual Studio 或 Visual Studio Code 中提供的功能，如下列文章所述。</span><span class="sxs-lookup"><span data-stu-id="3c642-111">You can use any text editor to work with solution files, but we recommend leveraging the features provided in Visual Studio or Visual Studio Code as described in the following articles.</span></span>

- [<span data-ttu-id="3c642-112">透過 Visual Studio 建立與部署 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="3c642-112">Creating and deploying Azure resource groups through Visual Studio</span></span>](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [<span data-ttu-id="3c642-113">在 Visual Studio Code 中使用 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3c642-113">Working with Azure Resource Manager Templates in Visual Studio Code</span></span>](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a><span data-ttu-id="3c642-114">Structure</span><span class="sxs-lookup"><span data-stu-id="3c642-114">Structure</span></span>
<span data-ttu-id="3c642-115">管理解決方案與 [Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md#template-format)的基本結構相同，如下所示。</span><span class="sxs-lookup"><span data-stu-id="3c642-115">The basic structure of a management solution file is the same as a [Resource Manager Template](../azure-resource-manager/resource-group-authoring-templates.md#template-format) which is as follows.</span></span>  <span data-ttu-id="3c642-116">下列各節說明最上層元素及其在解決方案中的內容。</span><span class="sxs-lookup"><span data-stu-id="3c642-116">Each of the sections below describes the top level elements and and their contents in a solution.</span></span>  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a><span data-ttu-id="3c642-117">參數</span><span class="sxs-lookup"><span data-stu-id="3c642-117">Parameters</span></span>
<span data-ttu-id="3c642-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) 是您在使用者安裝解決方案時向他們要求的值。</span><span class="sxs-lookup"><span data-stu-id="3c642-118">[Parameters](../azure-resource-manager/resource-group-authoring-templates.md#parameters) are values that you require from the user when they install the management solution.</span></span>  <span data-ttu-id="3c642-119">所有解決方案都會有標準參數，而您可以視需要針對特定解決方案新增額外的參數。</span><span class="sxs-lookup"><span data-stu-id="3c642-119">There are standard parameters that all solutions will have, and you can add additional parameters as required for your particular solution.</span></span>  <span data-ttu-id="3c642-120">使用者在安裝解決方案時提供參數值的方式，將取決於特定參數以及解決方案的安裝方式。</span><span class="sxs-lookup"><span data-stu-id="3c642-120">How users will provide parameter values when they install your solution will depend on the particular parameter and how the solution is being installed.</span></span>

<span data-ttu-id="3c642-121">當使用者透過 [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) 或 [Azure 快速入門範本](operations-management-suite-solutions.md#finding-and-installing-management-solutions)安裝管理解決方案時，系統會提示他們選取 [OMS 工作區和自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)。</span><span class="sxs-lookup"><span data-stu-id="3c642-121">When a user installs your management solution through the [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions) or [Azure QuickStart templates](operations-management-suite-solutions.md#finding-and-installing-management-solutions) they are prompted to select an [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account).</span></span>  <span data-ttu-id="3c642-122">這些用來填入每個標準參數的值。</span><span class="sxs-lookup"><span data-stu-id="3c642-122">These are used to populate the values of each of the standard parameters.</span></span>  <span data-ttu-id="3c642-123">系統不會提示使用者直接提供標準參數的值，但會提示他們提供任何其他參數的值。</span><span class="sxs-lookup"><span data-stu-id="3c642-123">The user is not prompted to directly provide values for the standard parameters, but they are prompted to provide values for any additional parameters.</span></span>

<span data-ttu-id="3c642-124">當使用者以[其他方法](operations-management-suite-solutions.md#finding-and-installing-management-solutions)安裝解決方案時，他們必須提供所有標準參數和所有其他參數的值。</span><span class="sxs-lookup"><span data-stu-id="3c642-124">When the user installs your solution [another method](operations-management-suite-solutions.md#finding-and-installing-management-solutions), they must provide a value for all standard parameters and all additional parameters.</span></span>

<span data-ttu-id="3c642-125">範例參數如下所示。</span><span class="sxs-lookup"><span data-stu-id="3c642-125">A sample parameter is shown below.</span></span>  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

<span data-ttu-id="3c642-126">下表說明參數的屬性。</span><span class="sxs-lookup"><span data-stu-id="3c642-126">The following table describes the attributes of a parameter.</span></span>

| <span data-ttu-id="3c642-127">屬性</span><span class="sxs-lookup"><span data-stu-id="3c642-127">Attribute</span></span> | <span data-ttu-id="3c642-128">說明</span><span class="sxs-lookup"><span data-stu-id="3c642-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3c642-129">類型</span><span class="sxs-lookup"><span data-stu-id="3c642-129">type</span></span> |<span data-ttu-id="3c642-130">變數的資料類型。</span><span class="sxs-lookup"><span data-stu-id="3c642-130">Data type for the parameter.</span></span> <span data-ttu-id="3c642-131">針對使用者顯示的輸入控制項視資料類型而定。</span><span class="sxs-lookup"><span data-stu-id="3c642-131">The input control displayed for the user depends on the data type.</span></span><br><br><span data-ttu-id="3c642-132">bool - 下拉式方塊</span><span class="sxs-lookup"><span data-stu-id="3c642-132">bool - Drop down box</span></span><br><span data-ttu-id="3c642-133">string - 文字方塊</span><span class="sxs-lookup"><span data-stu-id="3c642-133">string - Text box</span></span><br><span data-ttu-id="3c642-134">int - 文字方塊</span><span class="sxs-lookup"><span data-stu-id="3c642-134">int - Text box</span></span><br><span data-ttu-id="3c642-135">securestring - 密碼欄位</span><span class="sxs-lookup"><span data-stu-id="3c642-135">securestring - Password field</span></span><br> |
| <span data-ttu-id="3c642-136">category</span><span class="sxs-lookup"><span data-stu-id="3c642-136">category</span></span> |<span data-ttu-id="3c642-137">參數的選擇性類別。</span><span class="sxs-lookup"><span data-stu-id="3c642-137">Optional category for the parameter.</span></span>  <span data-ttu-id="3c642-138">相同類別中的參數會群組在一起。</span><span class="sxs-lookup"><span data-stu-id="3c642-138">Parameters in the same category are grouped together.</span></span> |
| <span data-ttu-id="3c642-139">control</span><span class="sxs-lookup"><span data-stu-id="3c642-139">control</span></span> |<span data-ttu-id="3c642-140">string 參數的其他功能。</span><span class="sxs-lookup"><span data-stu-id="3c642-140">Additional functionality for string parameters.</span></span><br><br><span data-ttu-id="3c642-141">datetime - Datetime 控制項隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="3c642-141">datetime - Datetime control is displayed.</span></span><br><span data-ttu-id="3c642-142">guid - 會自動產生 Guid 值，但未顯示此參數。</span><span class="sxs-lookup"><span data-stu-id="3c642-142">guid - Guid value is automatically generated, and the parameter is not displayed.</span></span> |
| <span data-ttu-id="3c642-143">說明</span><span class="sxs-lookup"><span data-stu-id="3c642-143">description</span></span> |<span data-ttu-id="3c642-144">參數的選擇性說明。</span><span class="sxs-lookup"><span data-stu-id="3c642-144">Optional description for the parameter.</span></span>  <span data-ttu-id="3c642-145">顯示於參數旁邊的資訊球形文字說明。</span><span class="sxs-lookup"><span data-stu-id="3c642-145">Displayed in an information balloon next to the parameter.</span></span> |

### <a name="standard-parameters"></a><span data-ttu-id="3c642-146">標準參數</span><span class="sxs-lookup"><span data-stu-id="3c642-146">Standard parameters</span></span>
<span data-ttu-id="3c642-147">下表列出所有管理解決方案的標準參數。</span><span class="sxs-lookup"><span data-stu-id="3c642-147">The following table lists the standard parameters for all management solutions.</span></span>  <span data-ttu-id="3c642-148">系統會為使用者填入這些值，而不會在他們從 Azure Marketplace 或快速入門範本安裝解決方案時提示他們輸入這些值。</span><span class="sxs-lookup"><span data-stu-id="3c642-148">These values are populated for the user instead of prompting for them when your solution is installed from the Azure Marketplace or Quickstart templates.</span></span>  <span data-ttu-id="3c642-149">如果以其他方法安裝解決方案，使用者必須提供這些值。</span><span class="sxs-lookup"><span data-stu-id="3c642-149">The user must provide values for them if the solution is installed with another method.</span></span>

> [!NOTE]
> <span data-ttu-id="3c642-150">Azure Marketplace 和快速入門範本中的使用者介面需有表格中的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="3c642-150">The user interface in the Azure Marketplace and Quickstart templates is expecting the parameter names in the table.</span></span>  <span data-ttu-id="3c642-151">如果您使用不同的參數名稱，則會提示使用者輸入其值，而不會自動填入。</span><span class="sxs-lookup"><span data-stu-id="3c642-151">If you use different parameter names then the user will be prompted for them, and they will not be automatically populated.</span></span>
>
>

| <span data-ttu-id="3c642-152">參數</span><span class="sxs-lookup"><span data-stu-id="3c642-152">Parameter</span></span> | <span data-ttu-id="3c642-153">類型</span><span class="sxs-lookup"><span data-stu-id="3c642-153">Type</span></span> | <span data-ttu-id="3c642-154">說明</span><span class="sxs-lookup"><span data-stu-id="3c642-154">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3c642-155">accountName</span><span class="sxs-lookup"><span data-stu-id="3c642-155">accountName</span></span> |<span data-ttu-id="3c642-156">string</span><span class="sxs-lookup"><span data-stu-id="3c642-156">string</span></span> |<span data-ttu-id="3c642-157">Azure 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="3c642-157">Azure Automation account name.</span></span> |
| <span data-ttu-id="3c642-158">pricingTier</span><span class="sxs-lookup"><span data-stu-id="3c642-158">pricingTier</span></span> |<span data-ttu-id="3c642-159">字串</span><span class="sxs-lookup"><span data-stu-id="3c642-159">string</span></span> |<span data-ttu-id="3c642-160">Log Analytics 工作區和 Azure 自動化帳戶的定價層。</span><span class="sxs-lookup"><span data-stu-id="3c642-160">Pricing tier of both Log Analytics workspace and Azure Automation account.</span></span> |
| <span data-ttu-id="3c642-161">regionId</span><span class="sxs-lookup"><span data-stu-id="3c642-161">regionId</span></span> |<span data-ttu-id="3c642-162">字串</span><span class="sxs-lookup"><span data-stu-id="3c642-162">string</span></span> |<span data-ttu-id="3c642-163">Azure 自動化帳戶的區域。</span><span class="sxs-lookup"><span data-stu-id="3c642-163">Region of the Azure Automation account.</span></span> |
| <span data-ttu-id="3c642-164">solutionName</span><span class="sxs-lookup"><span data-stu-id="3c642-164">solutionName</span></span> |<span data-ttu-id="3c642-165">字串</span><span class="sxs-lookup"><span data-stu-id="3c642-165">string</span></span> |<span data-ttu-id="3c642-166">解決方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="3c642-166">Name of the solution.</span></span>  <span data-ttu-id="3c642-167">如果您是透過快速入門範本部署解決方案，則您應該將 solutionName 定義為參數，如此您就可以定義字串，而不需要使用者來指定。</span><span class="sxs-lookup"><span data-stu-id="3c642-167">If you are deploying your solution through Quickstart templates, then you should define solutionName as a parameter so you can define a string instead requiring the user to specify one.</span></span> |
| <span data-ttu-id="3c642-168">workspaceName</span><span class="sxs-lookup"><span data-stu-id="3c642-168">workspaceName</span></span> |<span data-ttu-id="3c642-169">字串</span><span class="sxs-lookup"><span data-stu-id="3c642-169">string</span></span> |<span data-ttu-id="3c642-170">Log Analytics 工作區名稱。</span><span class="sxs-lookup"><span data-stu-id="3c642-170">Log Analytics workspace name.</span></span> |
| <span data-ttu-id="3c642-171">workspaceRegionId</span><span class="sxs-lookup"><span data-stu-id="3c642-171">workspaceRegionId</span></span> |<span data-ttu-id="3c642-172">字串</span><span class="sxs-lookup"><span data-stu-id="3c642-172">string</span></span> |<span data-ttu-id="3c642-173">Log Analytics 工作區的區域。</span><span class="sxs-lookup"><span data-stu-id="3c642-173">Region of the Log Analytics workspace.</span></span> |


<span data-ttu-id="3c642-174">以下是您可以複製並貼到您的方案檔案中的標準參數結構。</span><span class="sxs-lookup"><span data-stu-id="3c642-174">Following is the structure of the standard parameters that you can copy and paste into your solution file.</span></span>  

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
                   "description": "Region of the Log Analytics workspace"
            }
        },
        "regionId": {
            "type": "string",
            "metadata": {
                "description": "Region of the Azure Automation account"
            }
        },
        "pricingTier": {
            "type": "string",
            "metadata": {
                "description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
        }
    }


<span data-ttu-id="3c642-175">參考解決方案的其他項目中使用 **parameters('parameter name')** 語法的參數值。</span><span class="sxs-lookup"><span data-stu-id="3c642-175">You refer to parameter values in other elements of the solution with the syntax **parameters('parameter name')**.</span></span>  <span data-ttu-id="3c642-176">例如，若要存取工作區名稱，您會使用 **parameters('workspaceName')**</span><span class="sxs-lookup"><span data-stu-id="3c642-176">For example, to access the workspace name, you would use **parameters('workspaceName')**</span></span>

## <a name="variables"></a><span data-ttu-id="3c642-177">變數</span><span class="sxs-lookup"><span data-stu-id="3c642-177">Variables</span></span>
<span data-ttu-id="3c642-178">[變數](../azure-resource-manager/resource-group-authoring-templates.md#variables)是您會在管理解決方案的其餘部分中使用的值。</span><span class="sxs-lookup"><span data-stu-id="3c642-178">[Variables](../azure-resource-manager/resource-group-authoring-templates.md#variables) are values that you will use in the rest of the management solution.</span></span>  <span data-ttu-id="3c642-179">這些值不會公開給安裝解決方案的使用者。</span><span class="sxs-lookup"><span data-stu-id="3c642-179">These values are not exposed to the user installing the solution.</span></span>  <span data-ttu-id="3c642-180">它們旨在為作者提供單一位置，讓他們可以管理在整個解決方案可能會重複使用的值。</span><span class="sxs-lookup"><span data-stu-id="3c642-180">They are intended to provide the author with a single location where they can manage values that may be used multiple times throughout the solution.</span></span> <span data-ttu-id="3c642-181">您應該將解決方案特有的值放在變數中，而非將這些值硬式編碼在 **resources** 元素中。</span><span class="sxs-lookup"><span data-stu-id="3c642-181">You should put any values specific to your solution in variables as opposed to hard coding them in the **resources** element.</span></span>  <span data-ttu-id="3c642-182">這會讓程式碼更容易閱讀，並可讓您輕鬆地在後續的版本中變更這些值。</span><span class="sxs-lookup"><span data-stu-id="3c642-182">This makes the code more readable and allows you to easily change these values in later versions.</span></span>

<span data-ttu-id="3c642-183">下列範例為 **variables** 項目，包含解決方案中所使用的一般參數。</span><span class="sxs-lookup"><span data-stu-id="3c642-183">Following is an example of a **variables** element with typical parameters used in solutions.</span></span>

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="3c642-184">參考透過使用 **variables('variable name')** 語法的解決方案參數值。</span><span class="sxs-lookup"><span data-stu-id="3c642-184">You refer to variable values through the solution with the syntax **variables('variable name')**.</span></span>  <span data-ttu-id="3c642-185">例如，若要存取 SolutionName 變數，您會使用 **variables('SolutionName')**。</span><span class="sxs-lookup"><span data-stu-id="3c642-185">For example, to access the SolutionName variable, you would use **variables('SolutionName')**.</span></span>

<span data-ttu-id="3c642-186">您也可以定義有多組值的複雜變數。</span><span class="sxs-lookup"><span data-stu-id="3c642-186">You can also define complex variables that multiple sets of values.</span></span>  <span data-ttu-id="3c642-187">這在您會針對不同的資源類型定義多個屬性的管理解決方案中，這特別實用。</span><span class="sxs-lookup"><span data-stu-id="3c642-187">These are particularly useful in management solutions where you are defining multiple properties for different types of resources.</span></span>  <span data-ttu-id="3c642-188">例如，您可以將上述的解決方案變數重建為下列所示的狀態。</span><span class="sxs-lookup"><span data-stu-id="3c642-188">For example, you could restructure the solution variables shown above to the following.</span></span>

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

<span data-ttu-id="3c642-189">在此情況下，您會以 **variables('variable name').property** 語法透過解決方案參考變數。</span><span class="sxs-lookup"><span data-stu-id="3c642-189">In this case, you refer to variable values through the solution with the syntax **variables('variable name').property**.</span></span>  <span data-ttu-id="3c642-190">例如，若要存取 Solution Name 變數，您會使用 **variables('Solution').Name**。</span><span class="sxs-lookup"><span data-stu-id="3c642-190">For example, to access the Solution Name variable, you would use **variables('Solution').Name**.</span></span>

## <a name="resources"></a><span data-ttu-id="3c642-191">資源</span><span class="sxs-lookup"><span data-stu-id="3c642-191">Resources</span></span>
<span data-ttu-id="3c642-192">[資源](../azure-resource-manager/resource-group-authoring-templates.md#resources)會定義您的管理解決方案將會安裝並設定的不同資源。</span><span class="sxs-lookup"><span data-stu-id="3c642-192">[Resources](../azure-resource-manager/resource-group-authoring-templates.md#resources) define the different resources that your management solution will install and configure.</span></span>  <span data-ttu-id="3c642-193">這是範本最大且最複雜的部分。</span><span class="sxs-lookup"><span data-stu-id="3c642-193">This will be the largest and most complex portion of the template.</span></span>  <span data-ttu-id="3c642-194">您可以在[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md#resources)中取得 resource 元素的架構和完整描述。</span><span class="sxs-lookup"><span data-stu-id="3c642-194">You can get the structure and complete description of resource elements in [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md#resources).</span></span>  <span data-ttu-id="3c642-195">本文件中的其他文章會詳述您經常定義的其他資源。</span><span class="sxs-lookup"><span data-stu-id="3c642-195">Different resources that you will typically define are detailed in other articles in this documentation.</span></span> 


### <a name="dependencies"></a><span data-ttu-id="3c642-196">相依項目</span><span class="sxs-lookup"><span data-stu-id="3c642-196">Dependencies</span></span>
<span data-ttu-id="3c642-197">**dependsOn** 元素指定對另一個資源的[相依性](../azure-resource-manager/resource-group-define-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="3c642-197">The **dependsOn** elements specifies a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on another resource.</span></span>  <span data-ttu-id="3c642-198">安裝解決方案時，直到所有相依性建立後才會建立資源。</span><span class="sxs-lookup"><span data-stu-id="3c642-198">When the solution is installed, a resource is not created until all of its dependencies have been created.</span></span>  <span data-ttu-id="3c642-199">例如，解決方案可能會在使用[作業資源](operations-management-suite-solutions-resources-automation.md#automation-jobs)安裝時[啟動 Runbook](operations-management-suite-solutions-resources-automation.md#runbooks)。</span><span class="sxs-lookup"><span data-stu-id="3c642-199">For example, your solution might [start a runbook](operations-management-suite-solutions-resources-automation.md#runbooks) when it's installed using a [job resource](operations-management-suite-solutions-resources-automation.md#automation-jobs).</span></span>  <span data-ttu-id="3c642-200">作業資源會相依於 Runbook 資源，以確保在建立作業前建立 Runbook。</span><span class="sxs-lookup"><span data-stu-id="3c642-200">The job resource would be dependent on the runbook resource to make sure that the runbook is created before the job is created.</span></span>

### <a name="oms-workspace-and-automation-account"></a><span data-ttu-id="3c642-201">OMS 工作區和自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="3c642-201">OMS workspace and Automation account</span></span>
<span data-ttu-id="3c642-202">管理解決方案需要 [OMS 工作區](../log-analytics/log-analytics-manage-access.md)才可包含檢視，以及需要[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)才可包含 Runbook 和相關資源。</span><span class="sxs-lookup"><span data-stu-id="3c642-202">Management solutions require an [OMS workspace](../log-analytics/log-analytics-manage-access.md) to contain views and an [Automation account](../automation/automation-security-overview.md#automation-account-overview) to contain runbooks and related resources.</span></span>  <span data-ttu-id="3c642-203">這些項目必須在建立解決方案中的資源前取得，且不得定義於解決方案本身。</span><span class="sxs-lookup"><span data-stu-id="3c642-203">These must be available before the resources in the solution are created and should not be defined in the solution itself.</span></span>  <span data-ttu-id="3c642-204">使用者將會在部署解決方案時[指定工作區和帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)，但身為作者，您應該考慮下列幾點。</span><span class="sxs-lookup"><span data-stu-id="3c642-204">The user will [specify a workspace and account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) when they deploy your solution, but as the author you should consider the following points.</span></span>

## <a name="solution-resource"></a><span data-ttu-id="3c642-205">解決方案資源</span><span class="sxs-lookup"><span data-stu-id="3c642-205">Solution resource</span></span>
<span data-ttu-id="3c642-206">每個解決方案需要**資源**項目中定義解決方案本身的資源項目。</span><span class="sxs-lookup"><span data-stu-id="3c642-206">Each solution requires a resource entry in the **resources** element that defines the solution itself.</span></span>  <span data-ttu-id="3c642-207">這會有一種 **Microsoft.OperationsManagement/solutions** 並有下列結構。</span><span class="sxs-lookup"><span data-stu-id="3c642-207">This will have a type of **Microsoft.OperationsManagement/solutions** and have the following structure.</span></span> <span data-ttu-id="3c642-208">這包括經常用來定義解決方案屬性的[標準參數](#parameters)和[變數](#variables)。</span><span class="sxs-lookup"><span data-stu-id="3c642-208">This includes [standard parameters](#parameters) and [variables](#variables) that are typically used to define properties of the solution.</span></span>


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




### <a name="dependencies"></a><span data-ttu-id="3c642-209">相依項目</span><span class="sxs-lookup"><span data-stu-id="3c642-209">Dependencies</span></span>
<span data-ttu-id="3c642-210">解決方案資源在解決方案中的每隔一個資源上須有[相依性](../azure-resource-manager/resource-group-define-dependencies.md)，因為必須先存在相依性，才能建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="3c642-210">The solution resource must have a [dependency](../azure-resource-manager/resource-group-define-dependencies.md) on every other resource in the solution since they need to exist before the solution can be created.</span></span>  <span data-ttu-id="3c642-211">您可以在 **dependsOn** 項目中針對每個資源新增一個項目。</span><span class="sxs-lookup"><span data-stu-id="3c642-211">You do this by adding an entry for each resource in the **dependsOn** element.</span></span>

### <a name="properties"></a><span data-ttu-id="3c642-212">屬性</span><span class="sxs-lookup"><span data-stu-id="3c642-212">Properties</span></span>
<span data-ttu-id="3c642-213">解決方案資源具有下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="3c642-213">The solution resource has the properties in the following table.</span></span>  <span data-ttu-id="3c642-214">這包括由定義解決方案安裝後如何管理資源的解決方案所參考及包含的資源。</span><span class="sxs-lookup"><span data-stu-id="3c642-214">This includes the resources referenced and contained by the solution which defines how the resource is managed after the solution is installed.</span></span>  <span data-ttu-id="3c642-215">解決方案中的每個資源應列在 **referencedResources** 或 **containedResources** 屬性中。</span><span class="sxs-lookup"><span data-stu-id="3c642-215">Each resource in the solution should be listed in either the **referencedResources** or the **containedResources** property.</span></span>

| <span data-ttu-id="3c642-216">屬性</span><span class="sxs-lookup"><span data-stu-id="3c642-216">Property</span></span> | <span data-ttu-id="3c642-217">說明</span><span class="sxs-lookup"><span data-stu-id="3c642-217">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3c642-218">workspaceResourceId</span><span class="sxs-lookup"><span data-stu-id="3c642-218">workspaceResourceId</span></span> |<span data-ttu-id="3c642-219">具有以下形式的 Log Analytics 工作區識別碼：*<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<工作區名稱\>*。</span><span class="sxs-lookup"><span data-stu-id="3c642-219">ID of the Log Analytics workspace in the form *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<Workspace Name\>*.</span></span> |
| <span data-ttu-id="3c642-220">referencedResources</span><span class="sxs-lookup"><span data-stu-id="3c642-220">referencedResources</span></span> |<span data-ttu-id="3c642-221">解決方案移除時不應移除的解決方案資源清單。</span><span class="sxs-lookup"><span data-stu-id="3c642-221">List of resources in the solution that should not be removed when the solution is removed.</span></span> |
| <span data-ttu-id="3c642-222">containedResources</span><span class="sxs-lookup"><span data-stu-id="3c642-222">containedResources</span></span> |<span data-ttu-id="3c642-223">解決方案移除時應移除的解決方案資源清單。</span><span class="sxs-lookup"><span data-stu-id="3c642-223">List of resources in the solution that should be removed when the solution is removed.</span></span> |

<span data-ttu-id="3c642-224">上述範例適用於具有 Runbook、排程和檢視的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3c642-224">The example  above is for a solution with a runbook, a schedule, and view.</span></span>  <span data-ttu-id="3c642-225">**properties** 元素會「參考」排程和 Runbook，因此在移除解決方案時不會移除它們。</span><span class="sxs-lookup"><span data-stu-id="3c642-225">The schedule and runbook are *referenced* in the  **properties**  element so they are not removed when the solution is removed.</span></span>  <span data-ttu-id="3c642-226">會*包含*檢視，因此當移除解決方案時會移除它。</span><span class="sxs-lookup"><span data-stu-id="3c642-226">The view is *contained* so it is removed when the solution is removed.</span></span>

### <a name="plan"></a><span data-ttu-id="3c642-227">規劃</span><span class="sxs-lookup"><span data-stu-id="3c642-227">Plan</span></span>
<span data-ttu-id="3c642-228">解決方案資源的**計劃**實體具有下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="3c642-228">The **plan** entity of the solution resource has the properties in the following table.</span></span>

| <span data-ttu-id="3c642-229">屬性</span><span class="sxs-lookup"><span data-stu-id="3c642-229">Property</span></span> | <span data-ttu-id="3c642-230">說明</span><span class="sxs-lookup"><span data-stu-id="3c642-230">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3c642-231">名稱</span><span class="sxs-lookup"><span data-stu-id="3c642-231">name</span></span> |<span data-ttu-id="3c642-232">解決方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="3c642-232">Name of the solution.</span></span> |
| <span data-ttu-id="3c642-233">version</span><span class="sxs-lookup"><span data-stu-id="3c642-233">version</span></span> |<span data-ttu-id="3c642-234">作者所決定的解決方案版本。</span><span class="sxs-lookup"><span data-stu-id="3c642-234">Version of the solution as determined by the author.</span></span> |
| <span data-ttu-id="3c642-235">product</span><span class="sxs-lookup"><span data-stu-id="3c642-235">product</span></span> |<span data-ttu-id="3c642-236">識別解決方案的唯一字串。</span><span class="sxs-lookup"><span data-stu-id="3c642-236">Unique string to identify the solution.</span></span> |
| <span data-ttu-id="3c642-237">publisher</span><span class="sxs-lookup"><span data-stu-id="3c642-237">publisher</span></span> |<span data-ttu-id="3c642-238">解決方案的發佈者。</span><span class="sxs-lookup"><span data-stu-id="3c642-238">Publisher of the solution.</span></span> |



## <a name="sample"></a><span data-ttu-id="3c642-239">範例</span><span class="sxs-lookup"><span data-stu-id="3c642-239">Sample</span></span>
<span data-ttu-id="3c642-240">您可以在以下位置檢視具有解決方案資源的解決方案檔範例。</span><span class="sxs-lookup"><span data-stu-id="3c642-240">You can view samples of solution files with a solution resource at the following locations.</span></span>

- [<span data-ttu-id="3c642-241">自動化資源</span><span class="sxs-lookup"><span data-stu-id="3c642-241">Automation resources</span></span>](operations-management-suite-solutions-resources-automation.md#sample)
- [<span data-ttu-id="3c642-242">搜尋和警示資源</span><span class="sxs-lookup"><span data-stu-id="3c642-242">Search and alert resources</span></span>](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a><span data-ttu-id="3c642-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c642-243">Next steps</span></span>
* <span data-ttu-id="3c642-244">在您的管理解決方案中[新增儲存的搜尋和警示](operations-management-suite-solutions-resources-searches-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="3c642-244">[Add saved searches and alerts](operations-management-suite-solutions-resources-searches-alerts.md) to your management solution.</span></span>
* <span data-ttu-id="3c642-245">在您的管理解決方案中[新增檢視](operations-management-suite-solutions-resources-views.md)。</span><span class="sxs-lookup"><span data-stu-id="3c642-245">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="3c642-246">在您的管理解決方案中[新增 Runbook 及其他自動化資源](operations-management-suite-solutions-resources-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="3c642-246">[Add runbooks and other Automation resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>
* <span data-ttu-id="3c642-247">了解[編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3c642-247">Learn the details of [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3c642-248">搜尋 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates)不同 Resource Manager 範本的範例。</span><span class="sxs-lookup"><span data-stu-id="3c642-248">Search [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates) for samples of different Resource Manager templates.</span></span>
