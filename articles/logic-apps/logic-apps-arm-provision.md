---
title: "aaaCreate 邏輯應用程式使用 Azure 中的範本 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 toodeploy 邏輯應用程式定義工作流程。"
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
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a><span data-ttu-id="0bb77-103">使用範本建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0bb77-103">Create a Logic App using a template</span></span>
<span data-ttu-id="0bb77-104">範本會提供您快速 toouse 邏輯應用程式中的其他連接器。</span><span class="sxs-lookup"><span data-stu-id="0bb77-104">Templates provide a quick way toouse different connectors within a logic app.</span></span> <span data-ttu-id="0bb77-105">邏輯應用程式包括 toocreate 邏輯應用程式可以使用的 toodefine 商務工作流程的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="0bb77-105">Logic apps includes Azure Resource Manager templates for you toocreate a logic app that can be used toodefine business workflows.</span></span> <span data-ttu-id="0bb77-106">您可以定義部署的資源，以及如何 toodefine 參數，當您部署應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="0bb77-106">You can define which resources are deployed, and how toodefine parameters when you deploy your logic app.</span></span> <span data-ttu-id="0bb77-107">您可以針對您自己的商務案例，使用此範本，或自訂它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="0bb77-107">You can use this template for your own business scenarios, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="0bb77-108">如需有關 hello 邏輯應用程式屬性的詳細資訊，請參閱[邏輯應用程式工作流程管理 API](https://msdn.microsoft.com/library/azure/mt643788.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0bb77-108">For more details on hello Logic app properties, see [Logic App Workflow Management API](https://msdn.microsoft.com/library/azure/mt643788.aspx).</span></span> 

<span data-ttu-id="0bb77-109">如需 hello 定義本身的範例，請參閱[作者邏輯應用程式定義](logic-apps-author-definitions.md)。</span><span class="sxs-lookup"><span data-stu-id="0bb77-109">For examples of hello definition itself, see [Author Logic App definitions](logic-apps-author-definitions.md).</span></span> 

<span data-ttu-id="0bb77-110">如需關於建立範本的詳細資訊，請參閱 [編寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="0bb77-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="0bb77-111">Hello 完成範本，請參閱[邏輯應用程式範本](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="0bb77-111">For hello complete template, see [Logic App template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).</span></span>

## <a name="what-you-deploy"></a><span data-ttu-id="0bb77-112">您會部署什麼</span><span class="sxs-lookup"><span data-stu-id="0bb77-112">What you deploy</span></span>
<span data-ttu-id="0bb77-113">使用此範本，您將部署邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bb77-113">With this template, you deploy a logic app.</span></span>

<span data-ttu-id="0bb77-114">toorun hello 部署會自動選取 hello 下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="0bb77-114">toorun hello deployment automatically, select hello following button:</span></span>  

<span data-ttu-id="0bb77-115">[![部署 tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="0bb77-115">[![Deploy tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="0bb77-116">參數</span><span class="sxs-lookup"><span data-stu-id="0bb77-116">Parameters</span></span>
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a><span data-ttu-id="0bb77-117">testUri</span><span class="sxs-lookup"><span data-stu-id="0bb77-117">testUri</span></span>
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a><span data-ttu-id="0bb77-118">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="0bb77-118">Resources toodeploy</span></span>
### <a name="logic-app"></a><span data-ttu-id="0bb77-119">邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="0bb77-119">Logic app</span></span>
<span data-ttu-id="0bb77-120">建立 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bb77-120">Creates hello logic app.</span></span>

<span data-ttu-id="0bb77-121">hello 範本用於 hello 邏輯應用程式名稱的參數值。</span><span class="sxs-lookup"><span data-stu-id="0bb77-121">hello templates uses a parameter value for hello logic app name.</span></span> <span data-ttu-id="0bb77-122">它會設定 hello 邏輯應用程式 toohello hello 位置與 hello 資源群組相同的位置。</span><span class="sxs-lookup"><span data-stu-id="0bb77-122">It sets hello location of hello logic app toohello same location as hello resource group.</span></span> 

<span data-ttu-id="0bb77-123">這個特定的定義執行一次一小時，且 ping hello hello 中指定位置**testUri**參數。</span><span class="sxs-lookup"><span data-stu-id="0bb77-123">This particular definition runs once an hour, and pings hello location specified in hello **testUri** parameter.</span></span> 

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


## <a name="commands-toorun-deployment"></a><span data-ttu-id="0bb77-124">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="0bb77-124">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="0bb77-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bb77-125">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="0bb77-126">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0bb77-126">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



