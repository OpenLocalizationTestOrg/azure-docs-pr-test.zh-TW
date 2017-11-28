---
title: "aaaCreate Azure 服務匯流排命名空間主題訂用帳戶使用 Azure Resource Manager 範本 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題和訂用帳戶"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="5d843-103">使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5d843-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="5d843-104">本文示範如何 toouse Azure Resource Manager 範本，建立服務匯流排命名空間的主題和訂用帳戶，該命名空間中。</span><span class="sxs-lookup"><span data-stu-id="5d843-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="5d843-105">您將學習如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="5d843-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="5d843-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求</span><span class="sxs-lookup"><span data-stu-id="5d843-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="5d843-107">如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="5d843-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="5d843-108">Hello 完成範本，請參閱 hello[主題和訂用帳戶的服務匯流排命名空間][ Service Bus namespace with topic and subscription]範本。</span><span class="sxs-lookup"><span data-stu-id="5d843-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="5d843-109">hello 下列 Azure 資源管理員範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="5d843-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="5d843-110">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="5d843-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="5d843-111">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="5d843-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="5d843-112">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="5d843-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="5d843-113">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="5d843-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="5d843-114">toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋 「 Service Bus 」。</span><span class="sxs-lookup"><span data-stu-id="5d843-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="5d843-115">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="5d843-115">What will you deploy?</span></span>

<span data-ttu-id="5d843-116">使用此範本，您將部署具有主題和訂用帳戶的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="5d843-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="5d843-117">[服務匯流排主題和訂用帳戶](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)使用「發佈/訂閱」模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="5d843-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="5d843-118">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="5d843-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="5d843-119">[![部署 tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5d843-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="5d843-120">參數</span><span class="sxs-lookup"><span data-stu-id="5d843-120">Parameters</span></span>

<span data-ttu-id="5d843-121">使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="5d843-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="5d843-122">hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="5d843-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="5d843-123">您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。</span><span class="sxs-lookup"><span data-stu-id="5d843-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="5d843-124">不會定義參數的值，會一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="5d843-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="5d843-125">每個參數值用於 hello 範本 toodefine hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="5d843-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="5d843-126">hello 範本會定義下列參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="5d843-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="5d843-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="5d843-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="5d843-128">hello 服務匯流排命名空間 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="5d843-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="5d843-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="5d843-129">serviceBusTopicName</span></span>
<span data-ttu-id="5d843-130">hello hello hello 服務匯流排命名空間中建立的主題名稱。</span><span class="sxs-lookup"><span data-stu-id="5d843-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="5d843-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="5d843-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="5d843-132">hello 建立 hello 服務匯流排命名空間中的 hello 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="5d843-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="5d843-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="5d843-133">serviceBusApiVersion</span></span>
<span data-ttu-id="5d843-134">hello hello 範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="5d843-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="5d843-135">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="5d843-135">Resources toodeploy</span></span>
<span data-ttu-id="5d843-136">建立 **訊息**類型的標準服務匯流排命名空間與主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d843-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="5d843-137">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="5d843-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="5d843-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d843-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="5d843-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5d843-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="5d843-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d843-140">Next steps</span></span>
<span data-ttu-id="5d843-141">既然您已經建立及部署使用 Azure 資源管理員的資源，了解如何 toomanage 檢視這些文件的下列資源：</span><span class="sxs-lookup"><span data-stu-id="5d843-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="5d843-142">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="5d843-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="5d843-143">管理 Service Bus Explorer hello 與服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="5d843-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
