---
title: "使用範本的 Azure 事件中樞命名空間和取用者群組 aaaCreate |Microsoft 文件"
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
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="44500-103">使用 Azure Resource Manager 範本，以事件中樞和取用者群組來建立事件中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="44500-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="44500-104">本文將說明如何 toouse Azure Resource Manager 範本所建立的命名空間類型事件中心的一個事件中樞與一個取用者群組。</span><span class="sxs-lookup"><span data-stu-id="44500-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="44500-105">hello 文章顯示如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="44500-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="44500-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求</span><span class="sxs-lookup"><span data-stu-id="44500-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="44500-107">如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="44500-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="44500-108">Hello 完成範本，請參閱 hello[事件中樞與取用者群組範本][ Event Hub and consumer group template] GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="44500-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="44500-109">toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋事件中心。</span><span class="sxs-lookup"><span data-stu-id="44500-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="44500-110">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="44500-110">What will you deploy?</span></span>
<span data-ttu-id="44500-111">藉由此範本，您將部署含有事件中樞和取用者群組的「事件中樞」命名空間。</span><span class="sxs-lookup"><span data-stu-id="44500-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="44500-112">[事件中心](event-hubs-what-is-event-hubs.md)是處理用的服務 tooprovide 事件和遙測 ingress tooAzure 大規模、 可靠性高且延遲低的事件。</span><span class="sxs-lookup"><span data-stu-id="44500-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="44500-113">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="44500-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="44500-114">[![部署 tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="44500-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="44500-115">參數</span><span class="sxs-lookup"><span data-stu-id="44500-115">Parameters</span></span>
<span data-ttu-id="44500-116">使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="44500-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="44500-117">hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="44500-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="44500-118">您應該定義將會不同，根據您要部署的 hello 專案，或根據您要部署的 hello 環境 toowhich 這些值的參數。</span><span class="sxs-lookup"><span data-stu-id="44500-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="44500-119">不會定義參數的值一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="44500-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="44500-120">Hello 範本中的每個參數值定義部署的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="44500-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="44500-121">hello 範本會定義下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="44500-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="44500-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="44500-122">eventHubNamespaceName</span></span>
<span data-ttu-id="44500-123">hello 事件中樞命名空間 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="44500-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="44500-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="44500-124">eventHubName</span></span>
<span data-ttu-id="44500-125">hello hello hello 事件中樞命名空間中建立的事件中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="44500-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="44500-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="44500-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="44500-127">hello hello 事件中心建立的 hello 取用者群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="44500-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="44500-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="44500-128">apiVersion</span></span>
<span data-ttu-id="44500-129">hello 範本 hello API 版本。</span><span class="sxs-lookup"><span data-stu-id="44500-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="44500-130">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="44500-130">Resources toodeploy</span></span>
<span data-ttu-id="44500-131">建立類型為 **EventHubs**、含有事件中樞和取用者群組的命名空間。</span><span class="sxs-lookup"><span data-stu-id="44500-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="44500-132">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="44500-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="44500-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="44500-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="44500-134">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="44500-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="44500-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44500-135">Next steps</span></span>
<span data-ttu-id="44500-136">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="44500-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="44500-137">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="44500-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="44500-138">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="44500-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="44500-139">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="44500-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
