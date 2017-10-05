---
title: "在 Azure 中使用範本建立邏輯應用程式 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本部署邏輯應用程式以定義工作流程。"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 161adeacd6da2b15225c8a4ddae171e19e539967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="88a2d-103">使用範本建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="88a2d-103">Create a Logic App using a template</span></span>
<span data-ttu-id="88a2d-104">範本提供快速的方式，在邏輯應用程式中使用不同連接器。</span><span class="sxs-lookup"><span data-stu-id="88a2d-104">Templates provide a quick way to use different connectors within a logic app.</span></span> <span data-ttu-id="88a2d-105">邏輯應用程式包含 Azure Resource Manager 範本，供您用來建立可用於定義商務工作流程的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="88a2d-105">Logic apps includes Azure Resource Manager templates for you to create a logic app that can be used to define business workflows.</span></span> <span data-ttu-id="88a2d-106">您可以定義要部署的資源，以及部署邏輯應用程式時定義參數的方式。</span><span class="sxs-lookup"><span data-stu-id="88a2d-106">You can define which resources are deployed, and how to define parameters when you deploy your logic app.</span></span> <span data-ttu-id="88a2d-107">您可以直接在自己的商務案例中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="88a2d-107">You can use this template for your own business scenarios, or customize it to meet your requirements.</span></span>

<span data-ttu-id="88a2d-108">如需邏輯應用程式屬性的詳細資料，請參閱 [邏輯應用程式工作流程管理 API](https://msdn.microsoft.com/library/azure/mt643788.aspx)。</span><span class="sxs-lookup"><span data-stu-id="88a2d-108">For more details on the Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="88a2d-109">如需定義本身的範例，請參閱 [作者邏輯應用程式定義](logic-apps-author-definitions.md)。</span><span class="sxs-lookup"><span data-stu-id="88a2d-109">For examples of the definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="88a2d-110">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="88a2d-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="88a2d-111">如需完整範本，請參閱 [邏輯應用程式範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="88a2d-111">For the complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="88a2d-112">您會部署什麼</span><span class="sxs-lookup"><span data-stu-id="88a2d-112">What you deploy</span></span>
<span data-ttu-id="88a2d-113">使用此範本，您將部署邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="88a2d-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="88a2d-114">若要自動執行部署，請選取下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="88a2d-114">To run the deployment automatically, select the following button:</span></span>  

<span data-ttu-id="88a2d-115">[![部署至 Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="88a2d-115">[![Deploy to Azure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="88a2d-116">參數</span><span class="sxs-lookup"><span data-stu-id="88a2d-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="88a2d-117">testUri</span><span class="sxs-lookup"><span data-stu-id="88a2d-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-to-deploy"></a><span data-ttu-id="88a2d-118">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="88a2d-118">Resources to deploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="88a2d-119">邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="88a2d-119">Logic app</span></span>
<span data-ttu-id="88a2d-120">建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="88a2d-120">Creates the logic app.</span></span>

<span data-ttu-id="88a2d-121">範本會使用邏輯應用程式名稱的參數值。</span><span class="sxs-lookup"><span data-stu-id="88a2d-121">The templates uses a parameter value for the logic app name.</span></span> <span data-ttu-id="88a2d-122">它會將邏輯應用程式的位置設為與資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="88a2d-122">It sets the location of the logic app to the same location as the resource group.</span></span> 

<span data-ttu-id="88a2d-123">這個特定的定義每小時執行一次，並 Ping **testUri** 參數中所指定的位置。</span><span class="sxs-lookup"><span data-stu-id="88a2d-123">This particular definition runs once an hour, and pings the location specified in the **testUri** parameter.</span></span> 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-to-run-deployment"></a><span data-ttu-id="88a2d-124">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="88a2d-124">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="88a2d-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88a2d-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="88a2d-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="88a2d-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



