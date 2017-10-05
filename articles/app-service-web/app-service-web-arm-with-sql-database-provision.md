---
title: "佈建使用 SQL Database 的 Web 應用程式"
description: "使用 Azure 資源管理員範本來部署 Web 應用程式，其中包含 SQL Database。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: fb9648e1-9bf2-4537-bc4a-ab8d4953168c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: cc34f684f8c50e95a62cb7b04fd2ddce5deb68d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="provision-a-web-app-with-a-sql-database"></a><span data-ttu-id="13f76-103">佈建 Web 應用程式與 SQL Database</span><span class="sxs-lookup"><span data-stu-id="13f76-103">Provision a web app with a SQL Database</span></span>
<span data-ttu-id="13f76-104">在本主題中，您將學習如何建立 Azure 資源管理員範本，以部署 Web 應用程式與 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="13f76-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app and SQL Database.</span></span> <span data-ttu-id="13f76-105">您將學習如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="13f76-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="13f76-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="13f76-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="13f76-107">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="13f76-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="13f76-108">如需有關部署應用程式的詳細資訊，請參閱 [透過可預測方式在 Azure 中部署複雜應用程式](app-service-deploy-complex-application-predictably.md)。</span><span class="sxs-lookup"><span data-stu-id="13f76-108">For more information about deploying apps, see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md).</span></span>

<span data-ttu-id="13f76-109">如需完整的範本，請參閱 [Web 應用程式與 SQL Database 範本](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="13f76-109">For the complete template, see [Web App With SQL Database template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="13f76-110">部署內容</span><span class="sxs-lookup"><span data-stu-id="13f76-110">What you will deploy</span></span>
<span data-ttu-id="13f76-111">在此範本中，您將部署：</span><span class="sxs-lookup"><span data-stu-id="13f76-111">In this template, you will deploy:</span></span>

* <span data-ttu-id="13f76-112">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="13f76-112">a web app</span></span>
* <span data-ttu-id="13f76-113">SQL Database 伺服器</span><span class="sxs-lookup"><span data-stu-id="13f76-113">SQL Database server</span></span>
* <span data-ttu-id="13f76-114">SQL Database</span><span class="sxs-lookup"><span data-stu-id="13f76-114">SQL Database</span></span>
* <span data-ttu-id="13f76-115">自動調整設定</span><span class="sxs-lookup"><span data-stu-id="13f76-115">AutoScale settings</span></span>
* <span data-ttu-id="13f76-116">警示規則</span><span class="sxs-lookup"><span data-stu-id="13f76-116">Alert rules</span></span>
* <span data-ttu-id="13f76-117">應用程式情資</span><span class="sxs-lookup"><span data-stu-id="13f76-117">App Insights</span></span>

<span data-ttu-id="13f76-118">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="13f76-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="13f76-119">[![部署至 Azure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="13f76-119">[![Deploy to Azure](./media/app-service-web-arm-with-sql-database-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-sql-database%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="13f76-120">要指定的參數</span><span class="sxs-lookup"><span data-stu-id="13f76-120">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="administratorlogin"></a><span data-ttu-id="13f76-121">administratorLogin</span><span class="sxs-lookup"><span data-stu-id="13f76-121">administratorLogin</span></span>
<span data-ttu-id="13f76-122">資料庫伺服器系統管理員要使用的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="13f76-122">The account name to use for the database server administrator.</span></span>

    "administratorLogin": {
      "type": "string"
    }

### <a name="administratorloginpassword"></a><span data-ttu-id="13f76-123">administratorLoginPassword</span><span class="sxs-lookup"><span data-stu-id="13f76-123">administratorLoginPassword</span></span>
<span data-ttu-id="13f76-124">資料庫伺服器系統管理員要使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="13f76-124">The password to use for the database server administrator.</span></span>

    "administratorLoginPassword": {
      "type": "securestring"
    }

### <a name="databasename"></a><span data-ttu-id="13f76-125">databaseName</span><span class="sxs-lookup"><span data-stu-id="13f76-125">databaseName</span></span>
<span data-ttu-id="13f76-126">要建立之新資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="13f76-126">The name of the new database to create.</span></span>

    "databaseName": {
      "type": "string",
      "defaultValue": "sampledb"
    }

### <a name="collation"></a><span data-ttu-id="13f76-127">collation</span><span class="sxs-lookup"><span data-stu-id="13f76-127">collation</span></span>
<span data-ttu-id="13f76-128">用來管理字元適當用法的資料庫定序。</span><span class="sxs-lookup"><span data-stu-id="13f76-128">The database collation to use for governing the proper use of characters.</span></span>

    "collation": {
      "type": "string",
      "defaultValue": "SQL_Latin1_General_CP1_CI_AS"
    }

### <a name="edition"></a><span data-ttu-id="13f76-129">edition</span><span class="sxs-lookup"><span data-stu-id="13f76-129">edition</span></span>
<span data-ttu-id="13f76-130">要建立的資料庫類型。</span><span class="sxs-lookup"><span data-stu-id="13f76-130">The type of database to create.</span></span>

    "edition": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "Standard",
        "Premium"
      ],
      "metadata": {
        "description": "The type of database to create."
      }
    }

### <a name="maxsizebytes"></a><span data-ttu-id="13f76-131">maxSizeBytes</span><span class="sxs-lookup"><span data-stu-id="13f76-131">maxSizeBytes</span></span>
<span data-ttu-id="13f76-132">資料庫的大小上限 (位元組)。</span><span class="sxs-lookup"><span data-stu-id="13f76-132">The maximum size, in bytes, for the database.</span></span>

    "maxSizeBytes": {
      "type": "string",
      "defaultValue": "1073741824"
    }

### <a name="requestedserviceobjectivename"></a><span data-ttu-id="13f76-133">requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="13f76-133">requestedServiceObjectiveName</span></span>
<span data-ttu-id="13f76-134">與版本的效能等級對應的名稱。</span><span class="sxs-lookup"><span data-stu-id="13f76-134">The name corresponding to the performance level for edition.</span></span> 

    "requestedServiceObjectiveName": {
      "type": "string",
      "defaultValue": "Basic",
      "allowedValues": [
        "Basic",
        "S0",
        "S1",
        "S2",
        "P1",
        "P2",
        "P3"
      ],
      "metadata": {
        "description": "Describes the performance level for Edition"
      }
    }

## <a name="variables-for-names"></a><span data-ttu-id="13f76-135">名稱的變數</span><span class="sxs-lookup"><span data-stu-id="13f76-135">Variables for names</span></span>
<span data-ttu-id="13f76-136">這個範本包括建構範本所用名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="13f76-136">This template includes variables that construct names used in the template.</span></span> <span data-ttu-id="13f76-137">變數值會使用 **uniqueString** 函式從資源群組識別碼產生名稱。</span><span class="sxs-lookup"><span data-stu-id="13f76-137">The variable values use the **uniqueString** function to generate a name from the resource group id.</span></span>

    "variables": {
        "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
        "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
        "sqlserverName": "[concat('sqlserver', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="13f76-138">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="13f76-138">Resources to deploy</span></span>
### <a name="sql-server-and-database"></a><span data-ttu-id="13f76-139">SQL Server 和資料庫</span><span class="sxs-lookup"><span data-stu-id="13f76-139">SQL Server and Database</span></span>
<span data-ttu-id="13f76-140">建立新的 SQL Server 和資料庫。</span><span class="sxs-lookup"><span data-stu-id="13f76-140">Creates a new SQL Server and database.</span></span> <span data-ttu-id="13f76-141">**serverName** 參數中指定伺服器名稱，**serverLocation** 參數中指定位置。</span><span class="sxs-lookup"><span data-stu-id="13f76-141">The name of the server is specified in the **serverName** parameter and the location specified in the **serverLocation** parameter.</span></span> <span data-ttu-id="13f76-142">在建立新的伺服器時，您必須提供資料庫伺服器系統管理員的登入名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="13f76-142">When creating the new server, you must provide a login name and password for the database server administrator.</span></span> 

    {
      "name": "[variables('sqlserverName')]",
      "type": "Microsoft.Sql/servers",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "SqlServer"
      },
      "apiVersion": "2014-04-01-preview",
      "properties": {
        "administratorLogin": "[parameters('administratorLogin')]",
        "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
      },
      "resources": [
        {
          "name": "[parameters('databaseName')]",
          "type": "databases",
          "location": "[resourceGroup().location]",
          "tags": {
            "displayName": "Database"
          },
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "properties": {
            "edition": "[parameters('edition')]",
            "collation": "[parameters('collation')]",
            "maxSizeBytes": "[parameters('maxSizeBytes')]",
            "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
          }
        },
        {
          "type": "firewallrules",
          "apiVersion": "2014-04-01-preview",
          "dependsOn": [
            "[variables('sqlserverName')]"
          ],
          "location": "[resourceGroup().location]",
          "name": "AllowAllAzureIps",
          "properties": {
            "endIpAddress": "0.0.0.0",
            "startIpAddress": "0.0.0.0"
          }
        }
      ]
    },

[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="13f76-143">Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="13f76-143">Web app</span></span>
    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "connectionstrings",
          "dependsOn": [
            "[variables('webSiteName')]"
          ],
          "properties": {
            "DefaultConnection": {
              "value": "[concat('Data Source=tcp:', reference(concat('Microsoft.Sql/servers/', variables('sqlserverName'))).fullyQualifiedDomainName, ',1433;Initial Catalog=', parameters('databaseName'), ';User Id=', parameters('administratorLogin'), '@', variables('sqlserverName'), ';Password=', parameters('administratorLoginPassword'), ';')]",
              "type": "SQLServer"
            }
          }
        }
      ]
    },


### <a name="autoscale"></a><span data-ttu-id="13f76-144">自動調整</span><span class="sxs-lookup"><span data-stu-id="13f76-144">AutoScale</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
      "type": "Microsoft.Insights/autoscalesettings",
      "location": "[resourceGroup().location]",
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "properties": {
        "profiles": [
          {
            "name": "Default",
            "capacity": {
              "minimum": 1,
              "maximum": 2,
              "default": 1
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT10M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 80.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT10M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "CpuPercentage",
                  "metricResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT1H",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60.0
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": 1,
                  "cooldown": "PT1H"
                }
              }
            ]
          }
        ],
        "enabled": false,
        "name": "[concat(variables('hostingPlanName'), '-', resourceGroup().name)]",
        "targetResourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      }
    },


### <a name="alert-rules-for-status-codes-403-and-500s-high-cpu-and-http-queue-length"></a><span data-ttu-id="13f76-145">狀態碼 403、狀態碼 500、高 CPU 和 HTTP 佇列長度的警示規則</span><span class="sxs-lookup"><span data-stu-id="13f76-145">Alert rules for status codes 403 and 500's, High CPU, and HTTP Queue Length</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ServerErrors ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ServerErrorsAlertRule"
      },
      "properties": {
        "name": "[concat('ServerErrors ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some server errors, status code 5xx.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http5xx"
          },
          "operator": "GreaterThan",
          "threshold": 0.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "ForbiddenRequestsAlertRule"
      },
      "properties": {
        "name": "[concat('ForbiddenRequests ', variables('webSiteName'))]",
        "description": "[concat(variables('webSiteName'), ' has some requests that are forbidden, status code 403.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/sites', variables('webSiteName'))]",
            "metricName": "Http403"
          },
          "operator": "GreaterThan",
          "threshold": 0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "CPUHighAlertRule"
      },
      "properties": {
        "name": "[concat('CPUHigh ', variables('hostingPlanName'))]",
        "description": "[concat('The average CPU is high across all the instances of ', variables('hostingPlanName'))]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
            "metricName": "CpuPercentage"
          },
          "operator": "GreaterThan",
          "threshold": 90,
          "windowSize": "PT15M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
      "type": "Microsoft.Insights/alertrules",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[variables('hostingPlanName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName')))]": "Resource",
        "displayName": "AutoScaleSettings"
      },
      "properties": {
        "name": "[concat('LongHttpQueue ', variables('hostingPlanName'))]",
        "description": "[concat('The HTTP queue for the instances of ', variables('hostingPlanName'), ' has a large number of pending requests.')]",
        "isEnabled": false,
        "condition": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]",
            "metricName": "HttpQueueLength"
          },
          "operator": "GreaterThan",
          "threshold": 100.0,
          "windowSize": "PT5M"
        },
        "action": {
          "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
          "sendToServiceOwners": true,
          "customEmails": [ ]
        }
      }
    },

### <a name="app-insights"></a><span data-ttu-id="13f76-146">應用程式情資</span><span class="sxs-lookup"><span data-stu-id="13f76-146">App Insights</span></span>
    {
      "apiVersion": "2014-04-01",
      "name": "[concat('AppInsights', variables('webSiteName'))]",
      "type": "Microsoft.Insights/components",
      "location": "Central US",
      "dependsOn": [
        "[variables('webSiteName')]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Web/sites', variables('webSiteName')))]": "Resource",
        "displayName": "AppInsightsComponent"
      },
      "properties": {
        "ApplicationId": "[variables('webSiteName')]"
      }
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="13f76-147">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="13f76-147">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="13f76-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="13f76-148">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli"></a><span data-ttu-id="13f76-149">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="13f76-149">Azure CLI</span></span>

    azure config mode arm
    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="13f76-150">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="13f76-150">Azure CLI 2.0</span></span>

    az resource deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-sql-database/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE]
> <span data-ttu-id="13f76-151">如需參數 JSON 檔案的內容，請參閱 [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json)。</span><span class="sxs-lookup"><span data-stu-id="13f76-151">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-sql-database/azuredeploy.parameters.json).</span></span>
>
>
