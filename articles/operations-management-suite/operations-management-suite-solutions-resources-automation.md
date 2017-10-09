---
title: "在 OMS 解決方案 aaaAzure 自動化資源 |Microsoft 文件"
description: "OMS 中的解決方案通常會包含在 Azure 自動化 tooautomate 程序，例如收集及處理監視資料中的 runbook。  本文說明如何 tooinclude runbook 及其相關的資源，在方案中。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a>新增 Azure 自動化資源 tooan OMS 管理解決方案 （預覽）
> [!NOTE]
> 這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。 如下所述的任何結構描述是主體 toochange。   


[在 OMS 中的管理解決方案](operations-management-suite-solutions.md)通常會包含在 Azure 自動化 tooautomate 程序，例如收集及處理監視資料中的 runbook。  此外 toorunbooks，自動化帳戶包含資產，例如變數和支援 hello 方案中的 hello runbook 使用的排程。  本文說明如何 tooinclude runbook 及其相關的資源，在方案中。

> [!NOTE]
> hello 這篇文章中的範例使用參數和變數，都是必要或常見 toomanagement 解決方案中所述[Operations Management Suite (OMS) 中建立管理方案](operations-management-suite-solutions-creating.md) 


## <a name="prerequisites"></a>必要條件
本文假設您已經熟悉 hello 下列資訊。

- 如何太[建立管理方案](operations-management-suite-solutions-creating.md)。
- hello 結構[方案檔](operations-management-suite-solutions-solution-file.md)。
- 如何太[撰寫資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)

## <a name="automation-account"></a>自動化帳戶
Azure 自動化中的所有資源都會包含在[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)中。  中所述[OMS 工作區以及自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)hello 自動化帳戶不包含在 hello 管理解決方案，但必須先安裝 hello 解決方案。  如果它無法使用，hello 方案安裝將會失敗。

每個自動化資源 hello 名稱包括 hello 其自動化帳戶名稱。  這是以 hello hello 方案**accountName**參數，如下列範例 runbook 資源的 hello 所示。

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a>Runbook
您應該包含由 hello 方案檔中的 hello 方案使用，因此安裝 hello 方案時，他們所建立的任何 runbook。  您不能包含 hello 範本中的 hello runbook hello 主體，因此您應發佈 hello runbook tooa 公共場所位置存取它的任何使用者安裝方案。

[Azure 自動化 runbook](../automation/automation-runbook-types.md)資源有一種**Microsoft.Automation/automationAccounts/runbooks**而且具有下列結構的 hello。 這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


hello 下表描述的 runbook hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| runbookType |指定 hello hello runbook 類型。 <br><br> Script - PowerShell 指令碼 <br>PowerShell - PowerShell 工作流程 <br> GraphPowerShell - 圖形化 PowerShell 指令碼 Runbook <br> GraphPowerShellWorkflow - 圖形化 PowerShell 工作流程 Runbook |
| logProgress |指定是否[進度記錄](../automation/automation-runbook-output-and-messages.md)應產生的 hello runbook。 |
| logVerbose |指定是否[詳細資訊記錄](../automation/automation-runbook-output-and-messages.md)應產生的 hello runbook。 |
| 說明 |Hello runbook 的選擇性描述。 |
| publishContentLink |指定 hello hello runbook 內容。 <br><br>uri 的 Uri toohello hello runbook 內容。  這會是 PowerShell 和 Script Runbook 的 .ps1 檔案，以及 Graph Runbook 的已匯出圖形化 Runbook 檔案。  <br> 版本-您自己的追蹤的 hello runbook 的版本。 |


## <a name="automation-jobs"></a>自動化作業
當您在 Azure 自動化中啟動 Runbook 時，此 Runbook 便會建立自動化作業。  您可以將自動化工作資源 tooyour 方案 tooautomatically 開始 runbook 安裝時，將 hello 管理解決方案。  這個方法是常用的 toostart runbook 所使用的 hello 解決方案的初始組態。  toostart runbook，以固定間隔建立[排程](#schedules)和[作業排程](#job-schedules)

工作資源的類型是**Microsoft.Automation/automationAccounts/jobs**而且具有下列結構的 hello。  這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

自動化工作的 hello 屬性詳述於下表中的 hello。

| 屬性 | 說明 |
|:--- |:--- |
| Runbook |單一名稱同名的 hello runbook toostart hello 的實體。 |
| 參數 |每個參數值 hello runbook 所需的實體。 |

hello 作業會包括 hello runbook 名稱和任何參數值 toobe 傳送 toohello runbook。  hello 作業應該[相依於](operations-management-suite-solutions-solution-file.md#resources)hello 作業之前，必須建立 hello 自 hello runbook 啟動的 runbook。  如果您有多個應該啟動的 Runbook，您可以藉由讓作業相依於其他任何應該先執行的作業，以定義這些 Runbook 的順序。

工作資源的 hello 名稱必須包含通常由參數指派的 GUID。  [在 Operations Management Suite (OMS) 中建立解決方案](operations-management-suite-solutions-solution-file.md#parameters)可讓您深入了解 GUID 參數。  


## <a name="certificates"></a>憑證
[Azure 自動化憑證](../automation/automation-certificates.md)型別為**Microsoft.Automation/automationAccounts/certificates**而且具有下列結構的 hello。 這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



憑證資源的 hello 內容詳述於下表中的 hello。

| 屬性 | 說明 |
|:--- |:--- |
| base64Value |Base 64 hello 憑證值。 |
| thumbprint |Hello 憑證指模。 |



## <a name="credentials"></a>認證
[Azure 自動化認證](../automation/automation-credentials.md)型別為**Microsoft.Automation/automationAccounts/credentials**而且具有下列結構的 hello。  這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

認證資源的 hello 內容詳述於下表中的 hello。

| 屬性 | 說明 |
|:--- |:--- |
| userName |Hello 認證的使用者名稱。 |
| password |Hello 認證的密碼。 |


## <a name="schedules"></a>排程
[Azure 自動化排程](../automation/automation-schedules.md)型別為**Microsoft.Automation/automationAccounts/schedules**而且具有下列結構的 hello hello。 這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

排程資源的 hello 內容詳述於下表中的 hello。

| 屬性 | 說明 |
|:--- |:--- |
| 說明 |Hello 排程的選擇性描述。 |
| startTime |排程 hello 開始時間指定為 DateTime 物件。 如果可以轉換的 tooa 可提供字串有效的日期時間。 |
| isEnabled |指定是否啟用 hello 排程。 |
| interval |hello hello 排程的間隔類型。<br><br>day<br>hour |
| frequency |Hello 排程的頻率應該引發天數或小時。 |

排程必須具有開始時間大於 hello 的值與目前的時間。  因為您會有無從得知進行 toobe 安裝時，您無法提供此值的變數。

使用其中一個方案中使用排程的資源時，下列兩種策略的 hello。

- 使用參數進行 hello hello 排程開始時間。  在安裝 hello 方案時，這會提示 hello 使用者 tooprovide 值。  如果您有多個排程，您可以對它們使用單一參數值。
- 建立 hello 排程使用 runbook 啟動時安裝 hello 解決方案。  這會移除 hello 需求的時間，但是您不能包含 hello 使用者 toospecify hello 排程，因此移除 hello 方案時將會移除您方案中的。


### <a name="job-schedules"></a>作業排程
作業排程資源會連結 Runbook 與排程。  它們有一種**Microsoft.Automation/automationAccounts/jobSchedules**而且具有下列結構的 hello hello。  這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


作業排程的 hello 屬性詳述於下表中的 hello。

| 屬性 | 說明 |
|:--- |:--- |
| 排程名稱 |單一**名稱**實體與 hello hello 排程名稱。 |
| Runbook 名稱  |單一**名稱**實體與 hello hello runbook 名稱。  |



## <a name="variables"></a>變數
[Azure 自動化變數](../automation/automation-variables.md)型別為**Microsoft.Automation/automationAccounts/variables**而且具有下列結構的 hello。  這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

hello 下表描述 hello 變數資源的屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 說明 | Hello 變數的選擇性描述。 |
| isEncrypted | 指定是否應該加密 hello 變數。 |
| 類型 | 這個屬性目前沒有任何作用。  hello hello 變數資料類型將決定由 hello 初始值。 |
| value | Hello 變數的值。 |

> [!NOTE]
> hello**類型** 內容目前沒有正在建立 hello 變數上的沒有作用。  hello hello 變數的資料類型將決定 hello 值。  

如果您設定 hello 初始 hello 變數值，它必須設定為 hello 正確的資料類型。  hello 下表提供可允許的 hello 不同的資料類型，以及其語法。  請注意，在 JSON 中的值是預期的 tooalways 括以引號括住含有 hello 括在引號內的任何特殊字元。  例如，字串值會指定以引號括住 hello 字串 (使用 hello 逸出字元 (\\)) 時可以使用引號括住的一組指定的數字的值。

| 資料類型 | 說明 | 範例 | 太解析|
|:--|:--|:--|:--|
| 字串   | 以雙引號括住值。  | "\"Hello world\"" | "Hello world" |
| numeric  | 以單引號括住數值。| "64" | 64 |
| 布林值  | 以引號括住 **true** 或 **false**。  請注意，此值必須是小寫。 | "true" | true |
| datetime | 序列化的日期值。<br>您可以使用 PowerShell toogenerate 中的 hello Convertto-json cmdlet 此值，在特定日期。<br>範例：get-date "5/24/2017 13:14:57" \| ConvertTo-Json | "\\/Date(1495656897378)\\/" | 2017-05-24 13:14:57 |

## <a name="modules"></a>模組
您的管理解決方案不需要 toodefine[全域模組](../automation/automation-integration-modules.md)使用您的 runbook，因為它們永遠都可以在您的自動化帳戶。  您將 runbook 所使用的任何其他模組需要 tooinclude 資源。

[整合模組](../automation/automation-integration-modules.md)型別為**Microsoft.Automation/automationAccounts/modules**而且具有下列結構的 hello。  這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


模組資源的 hello 內容詳述於下表中的 hello。

| 屬性 | 說明 |
|:--- |:--- |
| contentLink |指定 hello hello 模組內容。 <br><br>uri 的 Uri toohello hello 模組內容。  這會是 PowerShell 和 Script Runbook 的 .ps1 檔案，以及 Graph Runbook 的已匯出圖形化 Runbook 檔案。  <br> 版本-您自己的追蹤的 hello 模組版本。 |

一旦建立 hello runbook 之前的 hello 模組資源 tooensure 需要具備 hello runbook。

### <a name="updating-modules"></a>更新模組
如果您更新的管理解決方案，包括 runbook 所使用的排程，而且 hello 新版本，您的方案有使用該 runbook 的新模組，hello runbook 可能會使用 hello 模組 hello 舊版本。  您應該包含 hello 遵循您的方案中的 runbook，並建立工作 toorun 它們之前的任何其他 runbook。  這可確保任何模組，會更新為所需的 hello runbook 會載入。

* [更新 ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript)可確保所有的方案中的 runbook 所使用的 hello 模組都 hello 最新版本。  
* [個 MS ReRegisterAutomationSchedule 管理](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript)重新註冊所有 hello 排程資源 tooensure hello runbook 連結 toothem 與使用 hello 最新的模組。




## <a name="sample"></a>範例
以下是方案的範例，包括所包含的 hello 下列資源：

- Runbook。  這是儲存在公用 GitHub 儲存機制的 Runbook 範例。
- 啟動時安裝 hello 解決方案的 hello runbook 的自動化作業。
- 排程與工作排程 toostart hello runbook 的固定間隔。
- 憑證。
- 認證。
- 變數。
- 模組。  這是 hello [OMSIngestionAPI 模組](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5)撰寫資料 tooLog 分析。 

hello 範例會使用[標準方案參數](operations-management-suite-solutions-solution-file.md#parameters)通常做為方案中使用變數相對於 toohardcoding hello 資源定義中的值。


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a>後續步驟
* [將檢視 tooyour 方案](operations-management-suite-solutions-resources-views.md)toovisualize 收集資料。
