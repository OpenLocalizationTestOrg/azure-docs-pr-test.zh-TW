---
title: "使用 Azure Resource Manager 範本建立 Azure 服務匯流排命名空間、主題和訂用帳戶 | Microsoft Docs"
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
ms.openlocfilehash: 8dd48787e7b788d249085b3110484de1a2c1d265
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="4bf90-103">使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4bf90-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="4bf90-104">本文說明如何使用 Azure Resource Manager 範本，建立服務匯流排命名空間和該命名空間內的主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bf90-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="4bf90-105">您將學習如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="4bf90-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="4bf90-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求</span><span class="sxs-lookup"><span data-stu-id="4bf90-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="4bf90-107">如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="4bf90-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="4bf90-108">如需完整的範本，請參閱[服務匯流排命名空間與主題和訂用帳戶][Service Bus namespace with topic and subscription]範本。</span><span class="sxs-lookup"><span data-stu-id="4bf90-108">For the complete template, see the [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="4bf90-109">下列 Azure Resource Manager 範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="4bf90-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="4bf90-110">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="4bf90-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="4bf90-111">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="4bf90-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="4bf90-112">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="4bf90-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="4bf90-113">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="4bf90-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="4bf90-114">若要檢查最新的範本，請造訪 [Azure 快速入門範本][Azure Quickstart Templates]資源庫並搜尋「服務匯流排」。</span><span class="sxs-lookup"><span data-stu-id="4bf90-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="4bf90-115">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="4bf90-115">What will you deploy?</span></span>

<span data-ttu-id="4bf90-116">使用此範本，您將部署具有主題和訂用帳戶的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="4bf90-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="4bf90-117">[服務匯流排主題和訂用帳戶](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)使用「發佈/訂閱」模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="4bf90-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="4bf90-118">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="4bf90-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="4bf90-119">[![部署至 Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="4bf90-119">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="4bf90-120">參數</span><span class="sxs-lookup"><span data-stu-id="4bf90-120">Parameters</span></span>

<span data-ttu-id="4bf90-121">透過 Azure 資源管理員，您可以定義在部署範本時想要指定之值的參數。</span><span class="sxs-lookup"><span data-stu-id="4bf90-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="4bf90-122">此範本有一個 `Parameters` 區段，內含所有參數值。</span><span class="sxs-lookup"><span data-stu-id="4bf90-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="4bf90-123">您應該為會隨著要部署的專案或要部署到的環境而變化的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="4bf90-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="4bf90-124">請不要為永遠保持不變的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="4bf90-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="4bf90-125">每個參數值都可在範本中用來定義所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="4bf90-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="4bf90-126">範本會定義下列參數。</span><span class="sxs-lookup"><span data-stu-id="4bf90-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="4bf90-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="4bf90-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="4bf90-128">要建立的服務匯流排命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="4bf90-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="4bf90-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="4bf90-129">serviceBusTopicName</span></span>
<span data-ttu-id="4bf90-130">在服務匯流排命名空間中建立的主題名稱。</span><span class="sxs-lookup"><span data-stu-id="4bf90-130">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="4bf90-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="4bf90-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="4bf90-132">在服務匯流排命名空間中建立的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4bf90-132">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="4bf90-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="4bf90-133">serviceBusApiVersion</span></span>
<span data-ttu-id="4bf90-134">範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="4bf90-134">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="4bf90-135">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="4bf90-135">Resources to deploy</span></span>
<span data-ttu-id="4bf90-136">建立 **訊息**類型的標準服務匯流排命名空間與主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bf90-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="4bf90-137">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="4bf90-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="4bf90-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bf90-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="4bf90-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4bf90-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="4bf90-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bf90-140">Next steps</span></span>
<span data-ttu-id="4bf90-141">現在您已使用 Azure Resource Manager 建立並部署資源，請檢視這些文件，了解如何管理這些資源︰</span><span class="sxs-lookup"><span data-stu-id="4bf90-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="4bf90-142">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="4bf90-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="4bf90-143">使用服務匯流排總管管理服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="4bf90-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
