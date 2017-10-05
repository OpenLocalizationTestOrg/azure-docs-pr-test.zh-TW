---
title: "使用 PowerShell 將 Azure Application Insights 自動化 | Microsoft Docs"
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
ms.openlocfilehash: 88dbb9515300f847789bc889911cdeff5f5bdb53
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="0a590-103">使用 PowerShell 建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="0a590-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="0a590-104">本文說明如何使用 Azure 資源管理，自動將 [Application Insights](app-insights-overview.md) 資源的建立和更新自動化。</span><span class="sxs-lookup"><span data-stu-id="0a590-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="0a590-105">例如，您可能建置程序中這麼做。</span><span class="sxs-lookup"><span data-stu-id="0a590-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="0a590-106">除了基本的 Application Insights 資源外，您可以建立[可用性 Web 測試](app-insights-monitor-web-app-availability.md)、設定[警示](app-insights-alerts.md)、設定[價格配置](app-insights-pricing.md)和建立其他 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="0a590-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="0a590-107">建立這些資源的關鍵是 [Azure 資源管理員](../azure-resource-manager/powershell-azure-resource-manager.md)適用的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="0a590-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="0a590-108">簡單地說，此程序是：下載現有資源的 JSON 定義；參數化某些值 (例如名稱)；然後每當您想建立新的資源時再執行範本。</span><span class="sxs-lookup"><span data-stu-id="0a590-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="0a590-109">您可以一起封裝幾項資源一次全部建立，例如一個包含可用性測試、警示和連續匯出儲存體的應用程式監視器。</span><span class="sxs-lookup"><span data-stu-id="0a590-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="0a590-110">部分參數化有一些微妙之處，我們會在這裡說明。</span><span class="sxs-lookup"><span data-stu-id="0a590-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="0a590-111">單次設定</span><span class="sxs-lookup"><span data-stu-id="0a590-111">One-time setup</span></span>
<span data-ttu-id="0a590-112">若您未曾將 PowerShell 與 Azure 訂用帳戶搭配使用：</span><span class="sxs-lookup"><span data-stu-id="0a590-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="0a590-113">在您要執行指令碼的電腦上安裝 Azure Powershell 模組：</span><span class="sxs-lookup"><span data-stu-id="0a590-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="0a590-114">安裝 [Microsoft Web Platform Installer (v5 或更新版本)](http://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0a590-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="0a590-115">請使用它來安裝 Microsoft Azure Powershell。</span><span class="sxs-lookup"><span data-stu-id="0a590-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="0a590-116">建立 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="0a590-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="0a590-117">建立新的 .json 檔案 - 在此範例中稱為 `template1.json` 。</span><span class="sxs-lookup"><span data-stu-id="0a590-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="0a590-118">將此內容複製到其中：</span><span class="sxs-lookup"><span data-stu-id="0a590-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
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
                    "description": "Enter the application type."
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
                    "description": "Enter the application location."
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
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
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



## <a name="create-application-insights-resources"></a><span data-ttu-id="0a590-119">建立 Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="0a590-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="0a590-120">在 PowerShell 中，登入 Azure：</span><span class="sxs-lookup"><span data-stu-id="0a590-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="0a590-121">執行如下命令：</span><span class="sxs-lookup"><span data-stu-id="0a590-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="0a590-122">`-ResourceGroupName` 是您要在其中建立新資源的群組。</span><span class="sxs-lookup"><span data-stu-id="0a590-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="0a590-123">`-TemplateFile` 必須出現在自訂參數之前。</span><span class="sxs-lookup"><span data-stu-id="0a590-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="0a590-124">`-appName` 是要建立的資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="0a590-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="0a590-125">您可以新增其他參數 - 可在範本的參數區段中找到其描述。</span><span class="sxs-lookup"><span data-stu-id="0a590-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="0a590-126">取得檢測金鑰</span><span class="sxs-lookup"><span data-stu-id="0a590-126">To get the instrumentation key</span></span>
<span data-ttu-id="0a590-127">建立應用程式資源之後，您會想要檢測金鑰：</span><span class="sxs-lookup"><span data-stu-id="0a590-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="0a590-128">設定價格方案</span><span class="sxs-lookup"><span data-stu-id="0a590-128">Set the price plan</span></span>

<span data-ttu-id="0a590-129">您可以設定[價格方案](app-insights-pricing.md)。</span><span class="sxs-lookup"><span data-stu-id="0a590-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="0a590-130">若要使用企業價格計劃建立應用程式資源，請使用上述的範本︰</span><span class="sxs-lookup"><span data-stu-id="0a590-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="0a590-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="0a590-131">priceCode</span></span>|<span data-ttu-id="0a590-132">計劃</span><span class="sxs-lookup"><span data-stu-id="0a590-132">plan</span></span>|
|---|---|
|<span data-ttu-id="0a590-133">1</span><span class="sxs-lookup"><span data-stu-id="0a590-133">1</span></span>|<span data-ttu-id="0a590-134">基本</span><span class="sxs-lookup"><span data-stu-id="0a590-134">Basic</span></span>|
|<span data-ttu-id="0a590-135">2</span><span class="sxs-lookup"><span data-stu-id="0a590-135">2</span></span>|<span data-ttu-id="0a590-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="0a590-136">Enterprise</span></span>|

* <span data-ttu-id="0a590-137">如果您只想要使用預設基本價格方案，您可以從範本中省略 CurrentBillingFeatures 資源。</span><span class="sxs-lookup"><span data-stu-id="0a590-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="0a590-138">如果您想在建立元件資源之後變更價格方案，可以使用省略 "microsoft.insights/components" 資源的範本。</span><span class="sxs-lookup"><span data-stu-id="0a590-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="0a590-139">此外，也從計費資源省略 `dependsOn` 節點。</span><span class="sxs-lookup"><span data-stu-id="0a590-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="0a590-140">若要驗證更新的價格方案，請在瀏覽器中查看 [功能與定價] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0a590-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="0a590-141">「重新整理瀏覽器檢視」以確保您看到的是最新的狀態。</span><span class="sxs-lookup"><span data-stu-id="0a590-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="0a590-142">新增度量警示</span><span class="sxs-lookup"><span data-stu-id="0a590-142">Add a metric alert</span></span>

<span data-ttu-id="0a590-143">若要與您的應用程式資源同時設定度量警示，請將類似的程式碼合併至範本檔案︰</span><span class="sxs-lookup"><span data-stu-id="0a590-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

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
      // Ensure this resource is created after the app resource:
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

<span data-ttu-id="0a590-144">當您叫用範本時，您可以選擇性地新增此參數︰</span><span class="sxs-lookup"><span data-stu-id="0a590-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="0a590-145">您當然可以參數化其他欄位。</span><span class="sxs-lookup"><span data-stu-id="0a590-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="0a590-146">若要尋找其他警示規則的類型名稱和組態詳細資料，請以手動方式建立規則，然後在 [Azure Resource Manager](https://resources.azure.com/) 檢查。</span><span class="sxs-lookup"><span data-stu-id="0a590-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="0a590-147">新增可用性測試</span><span class="sxs-lookup"><span data-stu-id="0a590-147">Add an availability test</span></span>

<span data-ttu-id="0a590-148">這個範例是 ping 測試 (以測試單一網頁)。</span><span class="sxs-lookup"><span data-stu-id="0a590-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="0a590-149">可用性測試中**有兩個部分**︰測試本身，以及通知您失敗的警示。</span><span class="sxs-lookup"><span data-stu-id="0a590-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="0a590-150">將下列程式碼合併至建立應用程式的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="0a590-150">Merge the following code into the template file that creates the app.</span></span>

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
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
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
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
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

<span data-ttu-id="0a590-151">若要探索其他測試位置的程式碼，或自動建立更複雜的 web 測試，請手動建立範例，然後從 [Azure Resource Manager](https://resources.azure.com/) 參數化程式碼。</span><span class="sxs-lookup"><span data-stu-id="0a590-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="0a590-152">新增其他資源</span><span class="sxs-lookup"><span data-stu-id="0a590-152">Add more resources</span></span>

<span data-ttu-id="0a590-153">若要自動建立任何類型的任何其他資源，手動建立範例，然後從 [Azure Resource Manager](https://resources.azure.com/) 複製並參數化其程式碼。</span><span class="sxs-lookup"><span data-stu-id="0a590-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="0a590-154">開啟 [Azure 資源管理員](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0a590-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="0a590-155">向下導覽 `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components` 直到應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="0a590-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Azure 資源總管中的瀏覽](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="0a590-157">*元件* 是用來顯示應用程式的基本 Application Insights 資源。</span><span class="sxs-lookup"><span data-stu-id="0a590-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="0a590-158">相關聯的警示規則和可用性 Web 測試有個別的資源。</span><span class="sxs-lookup"><span data-stu-id="0a590-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="0a590-159">將元件的 JSON 複製到 `template1.json`的適當位置。</span><span class="sxs-lookup"><span data-stu-id="0a590-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="0a590-160">刪除這些屬性：</span><span class="sxs-lookup"><span data-stu-id="0a590-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="0a590-161">開啟 webtests 和 alertrules 區段，將個別項目的 JSON 複製到您的範本。</span><span class="sxs-lookup"><span data-stu-id="0a590-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="0a590-162">(請勿從 webtests 或 alertrules 節點複製：移到其下的項目。)</span><span class="sxs-lookup"><span data-stu-id="0a590-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="0a590-163">每個 Web 測試都有一個關聯的警示規則，您必須同時複製這兩者。</span><span class="sxs-lookup"><span data-stu-id="0a590-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="0a590-164">您也可以包含計量的警示。</span><span class="sxs-lookup"><span data-stu-id="0a590-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="0a590-165">[計量名稱](app-insights-powershell-alerts.md#metric-names)。</span><span class="sxs-lookup"><span data-stu-id="0a590-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="0a590-166">在每個資源中插入下面這行：</span><span class="sxs-lookup"><span data-stu-id="0a590-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="0a590-167">參數化範本</span><span class="sxs-lookup"><span data-stu-id="0a590-167">Parameterize the template</span></span>
<span data-ttu-id="0a590-168">現在您必須以參數取代特定的名稱。</span><span class="sxs-lookup"><span data-stu-id="0a590-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="0a590-169">若要[參數化範本](../azure-resource-manager/resource-group-authoring-templates.md)，您要使用[一組協助程式函式](../azure-resource-manager/resource-group-template-functions.md)撰寫表示式。</span><span class="sxs-lookup"><span data-stu-id="0a590-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="0a590-170">您無法將參數化字串的一部分，因此請使用 `concat()` 建置字串。</span><span class="sxs-lookup"><span data-stu-id="0a590-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="0a590-171">以下是您會想要進行的替換的範例。</span><span class="sxs-lookup"><span data-stu-id="0a590-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="0a590-172">每個替換各出現數次。</span><span class="sxs-lookup"><span data-stu-id="0a590-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="0a590-173">您的範本中可能需要其他替換。</span><span class="sxs-lookup"><span data-stu-id="0a590-173">You might need others in your template.</span></span> <span data-ttu-id="0a590-174">這些範例使用我們在範本頂端定義的參數和變數。</span><span class="sxs-lookup"><span data-stu-id="0a590-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="0a590-175">find</span><span class="sxs-lookup"><span data-stu-id="0a590-175">find</span></span> | <span data-ttu-id="0a590-176">取代為</span><span class="sxs-lookup"><span data-stu-id="0a590-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="0a590-177">`"myappname"` (小寫)</span><span class="sxs-lookup"><span data-stu-id="0a590-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="0a590-178">刪除 Guid 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="0a590-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="0a590-179">設定資源間的相依性</span><span class="sxs-lookup"><span data-stu-id="0a590-179">Set dependencies between the resources</span></span>
<span data-ttu-id="0a590-180">Azure 應以嚴格的順序設定資源。</span><span class="sxs-lookup"><span data-stu-id="0a590-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="0a590-181">為確保一項設定完成後再開始下一項設定，請加入相依性命令行：</span><span class="sxs-lookup"><span data-stu-id="0a590-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="0a590-182">在可用性測試資源中︰</span><span class="sxs-lookup"><span data-stu-id="0a590-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="0a590-183">可用性測試的警示資源中︰</span><span class="sxs-lookup"><span data-stu-id="0a590-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="0a590-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a590-184">Next steps</span></span>
<span data-ttu-id="0a590-185">其他自動化文件：</span><span class="sxs-lookup"><span data-stu-id="0a590-185">Other automation articles:</span></span>

* <span data-ttu-id="0a590-186">[建立 Application Insights 資源](app-insights-powershell-script-create-resource.md) - 快速方法 (不使用範本)</span><span class="sxs-lookup"><span data-stu-id="0a590-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="0a590-187">設定警示</span><span class="sxs-lookup"><span data-stu-id="0a590-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="0a590-188">建立 Web 測試</span><span class="sxs-lookup"><span data-stu-id="0a590-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="0a590-189">將 Azure 診斷傳送至 Application Insights</span><span class="sxs-lookup"><span data-stu-id="0a590-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="0a590-190">從 GitHub 部署至 Azure (英文)</span><span class="sxs-lookup"><span data-stu-id="0a590-190">Deploy to Azure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="0a590-191">建立版本附註</span><span class="sxs-lookup"><span data-stu-id="0a590-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

