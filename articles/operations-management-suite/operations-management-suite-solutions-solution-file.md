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
# <a name="creating-a-management-solution-file-in-operations-management-suite-oms-preview"></a>在 Operations Management Suite (OMS) 中建立管理解決方案檔 (預覽)
> [!NOTE]
> 這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。 如下所述的任何結構描述是主體 toochange。  

Operations Management Suite (OMS) 中的管理解決方案會實作為 [Resource Manager 範本](../azure-resource-manager/resource-manager-template-walkthrough.md)。  學習如何 tooauthor 管理解決方案了解如何太 hello 主要工作[撰寫範本](../azure-resource-manager/resource-group-authoring-templates.md)。  本文章提供唯一的方案使用的範本的詳細資料以及如何 tooconfigure 一般解決方案資源。


## <a name="tools"></a>工具

您可以使用任何文字編輯器 toowork 方案檔，但我們建議您利用 hello hello 下列文章中所述，Visual Studio 或 Visual Studio 程式碼中所提供的功能。

- [透過 Visual Studio 建立與部署 Azure 資源群組](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)
- [在 Visual Studio Code 中使用 Azure Resource Manager 範本](../azure-resource-manager/resource-manager-vs-code.md)




## <a name="structure"></a>Structure
hello 管理方案檔案的基本結構是 hello 與相同[Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md#template-format)即，如下所示。  每個 hello 的以下各節說明 hello 最上層項目和方案中及其內容。  

    {
       "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
       "contentVersion": "1.0",
       "parameters": {  },
       "variables": {  },
       "resources": [  ],
       "outputs": {  }
    }

## <a name="parameters"></a>參數
[參數](../azure-resource-manager/resource-group-authoring-templates.md#parameters)是在安裝 hello 管理解決方案時，您需要從 hello 使用者的值。  所有解決方案都會有標準參數，而您可以視需要針對特定解決方案新增額外的參數。  使用者如何提供使用者安裝方案的參數值將取決於 hello 特定參數，並安裝 hello 方案方式。

當使用者安裝您的管理解決方案，透過 hello [Azure Marketplace](operations-management-suite-solutions.md#finding-and-installing-management-solutions)或[Azure 快速入門範本](operations-management-suite-solutions.md#finding-and-installing-management-solutions)它們是提示的 tooselect [OMS 工作區以及自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account).  這些是使用的 toopopulate hello 值的每個 hello 標準參數。  不會提示使用者 hello toodirectly hello 標準的參數提供值，但是可以提示的 tooprovide 值的任何其他參數。

Hello 使用者安裝方案時[另一種方法](operations-management-suite-solutions.md#finding-and-installing-management-solutions)，他們必須為所有標準的參數和所有其他參數提供值。

範例參數如下所示。  

    "startTime": {
        "type": "string",
        "metadata": {
            "description": "Enter time for starting VMs by resource group.",
            "control": "datetime",
            "category": "Schedule"
        }

hello 下表描述 hello 參數屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |Hello 參數的資料類型。 hello 輸入的控制項顯示 hello 使用者 hello 資料類型而定。<br><br>bool - 下拉式方塊<br>string - 文字方塊<br>int - 文字方塊<br>securestring - 密碼欄位<br> |
| category |Hello 參數的選擇性類別目錄。  在相同類別目錄群組在一起的 hello 參數。 |
| control |string 參數的其他功能。<br><br>datetime - Datetime 控制項隨即顯示。<br>自動產生的 guid-Guid 值，並不會顯示 hello 參數。 |
| 說明 |Hello 參數的選擇性描述。  顯示資訊提示氣球下一步 toohello 參數中。 |

### <a name="standard-parameters"></a>標準參數
hello 下表列出所有的管理解決方案的 hello 標準參數。  Hello 使用者，而不是提示認證從 hello Azure Marketplace 或快速入門範本安裝方案時，會填入這些值。  hello 使用者必須為它們提供值，如果 hello 方案已安裝另一個方法。

> [!NOTE]
> hello hello Azure Marketplace] 和 [快速入門範本中的使用者介面 hello 資料表中預期 hello 參數名稱。  如果您使用不同的參數名稱，然後將提示 hello 使用者，它們不會自動填入。
>
>

| 參數 | 類型 | 說明 |
|:--- |:--- |:--- |
| accountName |string |Azure 自動化帳戶名稱。 |
| pricingTier |字串 |Log Analytics 工作區和 Azure 自動化帳戶的定價層。 |
| regionId |字串 |Hello Azure 自動化帳戶的區域。 |
| solutionName |字串 |Hello 方案的名稱。  如果您要部署您的解決方案，透過快速入門範本，然後您應該定義 solutionName 做為參數讓您定義字串，而需要 hello 使用者 toospecify 其中一個。 |
| workspaceName |字串 |Log Analytics 工作區名稱。 |
| workspaceRegionId |字串 |Hello 記錄分析工作區的區域。 |


以下是 hello 結構 hello 標準參數，您可以複製並貼到您的方案檔。  

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


參照與 hello 語法 hello 解決方案的其他項目中的 tooparameter 值**參數 ('parameter name')**。  例如，tooaccess hello 工作區名稱，您會使用**parameters('workspaceName')**

## <a name="variables"></a>變數
[變數](../azure-resource-manager/resource-group-authoring-templates.md#variables)是您將使用中的 hello 管理解決方案的 hello 其餘部分的值。  這些值不公開的 toohello 使用者安裝 hello 解決方案。  它們是預定的 tooprovide hello 作者與單一位置，讓他們可以管理整個 hello 方案可能會重複使用的值。 您應該將任何值的特定 tooyour 解決方案放在變數為相對於 toohard 加以 hello**資源**項目。  這會使 hello 程式碼更容易閱讀，並可讓您 tooeasily 變更這些更新版本中的值。

下列範例為 **variables** 項目，包含解決方案中所使用的一般參數。

    "variables": {
        "SolutionVersion": "1.1",
        "SolutionPublisher": "Contoso",
        "SolutionName": "My Solution",
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

參考透過 hello 解決方案與 hello 語法 toovariable 值**變數 ('variable name')**。  例如，tooaccess hello SolutionName 變數，您會使用**variables('SolutionName')**。

您也可以定義有多組值的複雜變數。  這在您會針對不同的資源類型定義多個屬性的管理解決方案中，這特別實用。  例如，您無法重建 hello 方案變數 toohello 下列如上所示。

    "variables": {
        "Solution": {
          "Version": "1.1",
          "Publisher": "Contoso",
          "Name": "My Solution"
        },
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31"
    },

在此情況下，請參閱 toovariable 值透過 hello 解決方案與 hello 語法**variables('variable name').property**。  例如，tooaccess hello 方案名稱變數，您會使用**variables('Solution')。名稱**。

## <a name="resources"></a>資源
[資源](../azure-resource-manager/resource-group-authoring-templates.md#resources)hello 不同，定義資源管理解決方案將會安裝及設定。  這會是最大的 hello 和 hello 範本最複雜部分。  您可以取得 hello 結構和資源項目中的完整描述[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md#resources)。  本文件中的其他文章會詳述您經常定義的其他資源。 


### <a name="dependencies"></a>相依項目
hello **dependsOn**項目指定[相依性](../azure-resource-manager/resource-group-define-dependencies.md)於另一個資源。  安裝 hello 方案時，在建立及其所有相依性之前，將不會建立資源。  例如，解決方案可能會在使用[作業資源](operations-management-suite-solutions-resources-automation.md#automation-jobs)安裝時[啟動 Runbook](operations-management-suite-solutions-resources-automation.md#runbooks)。  hello 作業資源會相依於 hello runbook 資源 toomake 確定建立 hello 作業之前，已建立該 hello runbook。

### <a name="oms-workspace-and-automation-account"></a>OMS 工作區和自動化帳戶
管理解決方案需要[OMS 工作區](../log-analytics/log-analytics-manage-access.md)toocontain 檢視和[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)toocontain runbook 和相關聯的資源。  這些都必須可用後再 hello hello 方案中的資源建立和不應在 hello 方案本身中定義。  hello 使用者將[指定工作區和帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)當他們部署您的方案，但身 hello 作者，您應該考慮下列點 hello。

## <a name="solution-resource"></a>解決方案資源
每個解決方案需要資源中的項目 hello**資源**定義本身 hello 方案項目。  這會有一種**Microsoft.OperationsManagement/solutions**而且具有下列結構的 hello。 這包括[標準參數](#parameters)和[變數](#variables)所 hello 解決方案的常用的 toodefine 屬性。


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




### <a name="dependencies"></a>相依項目
hello 方案資源必須[相依性](../azure-resource-manager/resource-group-define-dependencies.md)hello 方案，因為他們需要 tooexist 才能建立 hello 方案中的每個其他資源。  您可以新增項目之每個資源 hello **dependsOn**項目。

### <a name="properties"></a>屬性
hello 方案資源有下表中的 hello hello 屬性。  這包括 hello 參考，而且會定義安裝 hello 方案之後，如何管理 hello 資源 hello 方案所包含的資源。  Hello 方案中的每個資源應該會列在任一個 hello **referencedResources**或 hello **containedResources**屬性。

| 屬性 | 說明 |
|:--- |:--- |
| workspaceResourceId |Hello hello 表單中的記錄分析工作區的識別碼 *<Resource Group ID>/providers/Microsoft.OperationalInsights/workspaces/\<工作區名稱\>*。 |
| referencedResources |不應該移除 hello 方案中移除時的 hello 方案中的資源的清單。 |
| containedResources |移除 hello 方案時，應移除的 hello 方案中的資源的清單。 |

上述的 hello 範例適用於在方案中使用 runbook、 排程和檢視。  hello 排程與 runbook*參考*在 hello**屬性**項目，因此不會移除 hello 方案中移除時。  hello 檢視是*包含*因此移除 hello 方案時，它會移除。

### <a name="plan"></a>規劃
hello**計劃**hello 方案資源的實體有下表中的 hello hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 名稱 |Hello 方案的名稱。 |
| 版本 |Hello 方案由 hello 作者所決定的版本。 |
| product |唯一字串 tooidentify hello 解決方案。 |
| publisher |Hello 方案的發行者。 |



## <a name="sample"></a>範例
您可以在下列位置的 hello 檢視與解決方案資源方案檔案的範例。

- [自動化資源](operations-management-suite-solutions-resources-automation.md#sample)
- [搜尋和警示資源](operations-management-suite-solutions-resources-searches-alerts.md#sample)


## <a name="next-steps"></a>後續步驟
* [新增已儲存的搜尋和警示](operations-management-suite-solutions-resources-searches-alerts.md)tooyour 管理解決方案。
* [加入檢視](operations-management-suite-solutions-resources-views.md)tooyour 管理解決方案。
* [新增 runbook 與其他自動化資源](operations-management-suite-solutions-resources-automation.md)tooyour 管理解決方案。
* 瞭解 hello[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。
* 搜尋 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates)不同 Resource Manager 範本的範例。
