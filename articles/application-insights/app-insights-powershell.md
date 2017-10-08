---
title: "使用 PowerShell 的 Azure Application Insights aaaAutomate |Microsoft 文件"
description: "在 PowerShell 中使用 Azure Resource Manager 範本自動建立資源、警示及可用性測試。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a>使用 PowerShell 建立 Application Insights 資源
本文將告訴您如何 tooautomate hello 建立和更新[Application Insights](app-insights-overview.md)使用 Azure 資源管理以自動執行的資源。 例如，您可能建置程序中這麼做。 Hello 基本的 Application Insights 資源，以及您可以建立[可用性 web 測試](app-insights-monitor-web-app-availability.md)、 安裝[警示](app-insights-alerts.md)，將的 hello[定價配置](app-insights-pricing.md)，並建立其他 Azure資源。

hello 這些資源是 JSON 範本的索引鍵 toocreating [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md)。 簡而言之，hello 程序是： 下載 hello JSON 定義現有的資源;某些值，例如名稱; 參數化然後再執行 hello 範本，每當您想要 toocreate 新的資源。 您可以封裝在一起的多項資源、 toocreate 中其中一個移-例如、 可用性測試、 警示與連續匯出的存放裝置的應用程式監視。 有的 hello 參數化，這裡，我們將說明一些微妙 toosome。

## <a name="one-time-setup"></a>單次設定
若您未曾將 PowerShell 與 Azure 訂用帳戶搭配使用：

Hello toorun hello 指令碼所在的電腦上安裝 hello Azure Powershell 模組：

1. 安裝 [Microsoft Web Platform Installer (v5 或更高版本)](http://www.microsoft.com/web/downloads/platform.aspx)。
2. 使用 tooinstall Microsoft Azure Powershell。

## <a name="create-an-azure-resource-manager-template"></a>建立 Azure Resource Manager 範本
建立新的 .json 檔案 - 在此範例中稱為 `template1.json` 。 將此內容複製到其中：

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a>建立 Application Insights 資源
1. 在 PowerShell 中，登入 tooAzure:
   
    `Login-AzureRmAccount`
2. 執行如下命令：
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * `-ResourceGroupName`是您想要 toocreate hello 新資源的 hello 群組。
   * `-TemplateFile`必須先 hello 自訂參數。
   * `-appName`hello 資源 toocreate hello 名稱。

您可以加入其他參數-hello 範本 hello 參數區段中找到其描述。

## <a name="tooget-hello-instrumentation-key"></a>tooget hello 檢測金鑰
建立應用程式資源之後, 您會想 hello 檢測金鑰： 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a>設定 hello 價格計劃

您可以設定 hello[價格計劃](app-insights-pricing.md)。

toocreate hello 企業價格計劃，使用上述的 hello 範本的應用程式資源：

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|priceCode|計劃|
|---|---|
|1|基本|
|2|Enterprise|

* 如果您只想 toouse hello 預設基本價格計劃，您可以省略 hello CurrentBillingFeatures 資源從 hello 範本。
* 如果在建立 hello 元件資源之後，您會想 toochange hello 價格計劃，您可以使用省略 hello"microsoft.insights/components"資源的範本。 此外，省略 hello`dependsOn`從 hello 計費資源節點。 

tooverify hello 更新的價格計劃，看看 hello 瀏覽器中的 hello [功能 + 定價] 刀鋒視窗。 **重新整理 hello 瀏覽器檢視**toomake 確定您看到 hello 最新狀態。



## <a name="add-a-metric-alert"></a>新增度量警示

總的度量的警示，在 hello tooset 相同時間為您的應用程式資源，類似到 hello 範本檔案的合併程式碼：

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

當您叫用 hello 範本時，您可以選擇性地加入這個參數：

    `-responseTime 2`

您當然可以參數化其他欄位。 

toofind 出 hello 型別名稱和組態詳細資料的其他警示的規則，以手動方式建立規則，然後檢查它在[Azure Resource Manager](https://resources.azure.com/)。 


## <a name="add-an-availability-test"></a>新增可用性測試

這個範例是 ping 測試 (tootest 單一頁面)。  

**有兩個部分**可用性測試中： hello 測試本身，並通知您失敗的 hello 警示。

合併 hello 成 hello 範本檔建立 hello 應用程式，下列程式碼。

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

toodiscover hello 代碼的其他測試的位置或 tooautomate hello 建立更複雜的 web 測試，手動建立範例，然後再參數化 hello 程式碼，從[Azure Resource Manager](https://resources.azure.com/)。

## <a name="add-more-resources"></a>新增其他資源

tooautomate hello 建立任何其他資源的任何範例手動建立，然後複製並從其程式碼的參數化[Azure Resource Manager](https://resources.azure.com/)。 

1. 開啟 [Azure 資源管理員](https://resources.azure.com/)。 向下導覽`subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`，tooyour 應用程式資源。 
   
    ![Azure 資源總管中的瀏覽](./media/app-insights-powershell/01.png)
   
    *元件*是 hello 基本的顯示應用程式的 Application Insights 資源。 Hello 相關警示的規則和可用性 web 測試有不同的資源。
2. 複製 hello JSON 的 hello 元件到 hello 適當位置中`template1.json`。
3. 刪除這些屬性：
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. 開啟 hello webtests 和 alertrules 區段，並將 hello JSON 的個別項目複製到您的範本。 (不要複製 hello webtests 或 alertrules 節點： 移至其下的 hello 項目。)
   
    每個 web 測試有相關聯的警示規則，因此您需要這些 toocopy。
   
    您也可以包含計量的警示。 [計量名稱](app-insights-powershell-alerts.md#metric-names)。
5. 在每個資源中插入下面這行：
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a>參數化 hello 範本
現在您有使用參數 tooreplace hello 特定名稱。 太[參數化的範本](../azure-resource-manager/resource-group-authoring-templates.md)，撰寫運算式使用[組協助程式函式](../azure-resource-manager/resource-group-template-functions.md)。 

您無法將參數化字串的部分，因此，使用`concat()`toobuild 字串。

以下是範例 hello 替代項目中，您會想 toomake。 每個替換各出現數次。 您的範本中可能需要其他替換。 這些範例會使用頂端的 hello 範本 hello hello 參數和我們所定義的變數。

| find | 取代為 |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| `"myappname"` (小寫) |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/>刪除 Guid 和識別碼。 |

### <a name="set-dependencies-between-hello-resources"></a>設定 hello 資源之間的相依性
Azure 應該設定嚴格的順序中的 hello 資源。 toomake 確定安裝程式完成之前 hello 接下來，新增相依性幾行：

* 在 hello 可用性測試資源：
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* 在可用性測試資源 hello 警示：
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a>後續步驟
其他自動化文件：

* [建立 Application Insights 資源](app-insights-powershell-script-create-resource.md) - 快速方法 (不使用範本)
* [設定警示](app-insights-powershell-alerts.md)
* [建立 Web 測試](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [傳送 Azure 診斷 tooApplication Insights](app-insights-powershell-azure-diagnostics.md)
* [部署從 GitHub tooAzure](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [建立版本附註](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

