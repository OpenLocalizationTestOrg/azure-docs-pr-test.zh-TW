---
title: "使用範本來建立 Azure 事件中樞命名空間和取用者群組 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本來建立含有事件中樞和取用者群組的事件中樞命名空間"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="9bf1b-103">使用 Azure Resource Manager 範本，以事件中樞和取用者群組來建立事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="9bf1b-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="9bf1b-104">本文說明如何使用 Azure Resource Manager 範本來建立一個類型為「事件中樞」、含有一個事件中樞和一個取用者群組的的命名空間。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="9bf1b-105">本文說明如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="9bf1b-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求</span><span class="sxs-lookup"><span data-stu-id="9bf1b-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="9bf1b-107">如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="9bf1b-108">如需完整的範本，請參閱 GitHub 上的[事件中樞和取用者群組範本][Event Hub and consumer group template]。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="9bf1b-109">若要檢查最新的範本，請造訪 [Azure 快速入門範本][Azure Quickstart Templates] 資源庫並搜尋事件中樞。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="9bf1b-110">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="9bf1b-110">What will you deploy?</span></span>
<span data-ttu-id="9bf1b-111">藉由此範本，您將部署含有事件中樞和取用者群組的「事件中樞」命名空間。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="9bf1b-112">[事件中樞](event-hubs-what-is-event-hubs.md) 是事件處理服務，用於提供大規模進入 Azure 的事件和遙測入口，並具備低延遲和高可靠性等特性。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="9bf1b-113">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="9bf1b-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="9bf1b-114">[![部署至 Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="9bf1b-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="9bf1b-115">參數</span><span class="sxs-lookup"><span data-stu-id="9bf1b-115">Parameters</span></span>
<span data-ttu-id="9bf1b-116">透過 Azure 資源管理員，您可以定義在部署範本時想要指定之值的參數。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="9bf1b-117">此範本有一個 `Parameters` 區段，內含所有參數值。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="9bf1b-118">針對會隨著所要部署專案或部署環境而變化的值，您應該為這些值定義參數。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="9bf1b-119">請不要為永遠保持不變的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="9bf1b-120">範本中的每個參數值會定義所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="9bf1b-121">範本會定義下列參數：</span><span class="sxs-lookup"><span data-stu-id="9bf1b-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="9bf1b-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="9bf1b-122">eventHubNamespaceName</span></span>
<span data-ttu-id="9bf1b-123">要建立的事件中樞命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="9bf1b-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="9bf1b-124">eventHubName</span></span>
<span data-ttu-id="9bf1b-125">在「事件中樞」命名空間中建立的事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="9bf1b-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="9bf1b-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="9bf1b-127">為事件中樞建立的取用者群組名稱。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="9bf1b-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="9bf1b-128">apiVersion</span></span>
<span data-ttu-id="9bf1b-129">範本的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="9bf1b-130">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="9bf1b-130">Resources to deploy</span></span>
<span data-ttu-id="9bf1b-131">建立類型為 **EventHubs**、含有事件中樞和取用者群組的命名空間。</span><span class="sxs-lookup"><span data-stu-id="9bf1b-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="9bf1b-132">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="9bf1b-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="9bf1b-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bf1b-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="9bf1b-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9bf1b-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="9bf1b-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bf1b-135">Next steps</span></span>
<span data-ttu-id="9bf1b-136">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="9bf1b-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="9bf1b-137">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="9bf1b-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9bf1b-138">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="9bf1b-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="9bf1b-139">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="9bf1b-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
