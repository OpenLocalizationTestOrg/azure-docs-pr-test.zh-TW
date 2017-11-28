---
title: "aaaCreate Azure 服務匯流排命名空間，並佇列使用 Azure Resource Manager 範本 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本建立服務匯流排命名空間和佇列"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="dfba6-103">使用 Azure Resource Manager 範本建立服務匯流排命名空間和佇列</span><span class="sxs-lookup"><span data-stu-id="dfba6-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="dfba6-104">本文示範如何 toouse Azure Resource Manager 範本，建立服務匯流排命名空間，並對該命名空間中。</span><span class="sxs-lookup"><span data-stu-id="dfba6-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="dfba6-105">您將學習如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="dfba6-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="dfba6-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="dfba6-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="dfba6-107">如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="dfba6-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="dfba6-108">Hello 完成範本，請參閱 hello[服務匯流排命名空間和佇列範本][ Service Bus namespace and queue template] GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="dfba6-108">For hello complete template, see hello [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="dfba6-109">hello 下列 Azure 資源管理員範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="dfba6-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="dfba6-110">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="dfba6-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="dfba6-111">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dfba6-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="dfba6-112">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="dfba6-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="dfba6-113">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="dfba6-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="dfba6-114">toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋 「 Service Bus 」。</span><span class="sxs-lookup"><span data-stu-id="dfba6-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="dfba6-115">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="dfba6-115">What will you deploy?</span></span>

<span data-ttu-id="dfba6-116">使用此範本，您將部署具有佇列的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="dfba6-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="dfba6-117">[服務匯流排佇列](service-bus-queues-topics-subscriptions.md#queues)第一個方案中提供，第一次出 (FIFO) 訊息傳遞 tooone 或更多的競爭取用者。</span><span class="sxs-lookup"><span data-stu-id="dfba6-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery tooone or more competing consumers.</span></span>

<span data-ttu-id="dfba6-118">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="dfba6-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="dfba6-119">[![部署 tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="dfba6-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="dfba6-120">參數</span><span class="sxs-lookup"><span data-stu-id="dfba6-120">Parameters</span></span>

<span data-ttu-id="dfba6-121">使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="dfba6-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="dfba6-122">hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="dfba6-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="dfba6-123">您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。</span><span class="sxs-lookup"><span data-stu-id="dfba6-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="dfba6-124">不會定義參數的值，會一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="dfba6-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="dfba6-125">每個參數值用於 hello 範本 toodefine hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="dfba6-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="dfba6-126">hello 範本會定義下列參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="dfba6-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="dfba6-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="dfba6-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="dfba6-128">hello 服務匯流排命名空間 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="dfba6-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="dfba6-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="dfba6-129">serviceBusQueueName</span></span>
<span data-ttu-id="dfba6-130">hello hello hello 服務匯流排命名空間中建立的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="dfba6-130">hello name of hello queue created in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="dfba6-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="dfba6-131">serviceBusApiVersion</span></span>
<span data-ttu-id="dfba6-132">hello hello 範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="dfba6-132">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="dfba6-133">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="dfba6-133">Resources toodeploy</span></span>
<span data-ttu-id="dfba6-134">建立 **訊息**類型的標準服務匯流排命名空間和佇列。</span><span class="sxs-lookup"><span data-stu-id="dfba6-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="dfba6-135">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="dfba6-135">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="dfba6-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfba6-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="dfba6-137">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dfba6-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="dfba6-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfba6-138">Next steps</span></span>
<span data-ttu-id="dfba6-139">既然您已經建立及部署使用 Azure 資源管理員的資源，了解如何 toomanage 檢視這些文件的下列資源：</span><span class="sxs-lookup"><span data-stu-id="dfba6-139">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="dfba6-140">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="dfba6-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="dfba6-141">管理 Service Bus Explorer hello 與服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="dfba6-141">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
