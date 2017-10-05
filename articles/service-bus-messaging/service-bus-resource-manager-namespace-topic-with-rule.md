---
title: "使用 Azure Resource Manager 範本建立 Azure 服務匯流排主題、訂用帳戶和規則 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題、訂用帳戶和規則"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="39428-103">使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="39428-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="39428-104">本文說明如何使用 Azure Resource Manager 範本，建立服務匯流排命名空間與主題、訂用帳戶和規則 (篩選器)。</span><span class="sxs-lookup"><span data-stu-id="39428-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="39428-105">您將學習如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="39428-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="39428-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求</span><span class="sxs-lookup"><span data-stu-id="39428-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="39428-107">如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="39428-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="39428-108">如需 Azure 資源命名慣例相關實務和模式的詳細資訊，請參閱 [Azure 資源的建議命名慣例][Recommended naming conventions for Azure resources]。</span><span class="sxs-lookup"><span data-stu-id="39428-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="39428-109">如需完整的範本，請參閱[服務匯流排命名空間與主題、訂用帳戶和規則][Service Bus namespace with topic, subscription, and rule]範本。</span><span class="sxs-lookup"><span data-stu-id="39428-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="39428-110">下列 Azure Resource Manager 範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="39428-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="39428-111">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="39428-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="39428-112">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="39428-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="39428-113">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="39428-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="39428-114">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="39428-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="39428-115">若要檢查最新的範本，請造訪 [Azure 快速入門範本][Azure Quickstart Templates]資源庫並搜尋「服務匯流排」。</span><span class="sxs-lookup"><span data-stu-id="39428-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="39428-116">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="39428-116">What will you deploy?</span></span>

<span data-ttu-id="39428-117">使用此範本，您將部署具有主題、訂用帳戶和規則 (篩選器) 的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="39428-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="39428-118">[服務匯流排主題和訂用帳戶](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)使用「發佈/訂閱」模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="39428-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="39428-119">使用主題和訂用帳戶時，分散式應用程式的元件彼此不直接通訊，相反的，它們會透過扮演中繼角色的主題來交換訊息。主題的訂用帳戶類似於虛擬佇列，同樣可接收已傳送到主題的訊息複本。</span><span class="sxs-lookup"><span data-stu-id="39428-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="39428-120">訂用帳戶上的篩選器可讓您指定傳送至主題的哪些訊息應出現在特定主題訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="39428-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="39428-121">什麼是規則 (篩選器)？</span><span class="sxs-lookup"><span data-stu-id="39428-121">What are rules (filters)?</span></span>

<span data-ttu-id="39428-122">在許多情況下，必須以不同的方式處理具有特定特性的訊息。</span><span class="sxs-lookup"><span data-stu-id="39428-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="39428-123">若要這麼做，您可以設定訂用帳戶以尋找具有特定屬性的訊息，然後對這些屬性進行修改。</span><span class="sxs-lookup"><span data-stu-id="39428-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="39428-124">雖然服務匯流排訂用帳戶可看見所有傳送至主題的訊息，但您只可以將部分的訊息複製到虛擬訂用帳戶佇列。</span><span class="sxs-lookup"><span data-stu-id="39428-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="39428-125">使用訂用帳戶篩選器即可達成。</span><span class="sxs-lookup"><span data-stu-id="39428-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="39428-126">若要深入了解規則 (篩選條件)，請參閱 [規則和動作](service-bus-queues-topics-subscriptions.md#rules-and-actions)。</span><span class="sxs-lookup"><span data-stu-id="39428-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="39428-127">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="39428-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="39428-128">[![部署至 Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="39428-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="39428-129">參數</span><span class="sxs-lookup"><span data-stu-id="39428-129">Parameters</span></span>

<span data-ttu-id="39428-130">透過 Azure Resource Manager，您應該定義在部署範本時想要指定之值的參數。</span><span class="sxs-lookup"><span data-stu-id="39428-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="39428-131">此範本有一個 `Parameters` 區段，內含所有參數值。</span><span class="sxs-lookup"><span data-stu-id="39428-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="39428-132">您應該為會隨著要部署的專案或要部署到的環境而變化的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="39428-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="39428-133">請不要為永遠保持不變的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="39428-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="39428-134">每個參數值都可在範本中用來定義所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="39428-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="39428-135">範本會定義下列參數：</span><span class="sxs-lookup"><span data-stu-id="39428-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="39428-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="39428-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="39428-137">要建立的服務匯流排命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="39428-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="39428-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="39428-138">serviceBusTopicName</span></span>
<span data-ttu-id="39428-139">在服務匯流排命名空間中建立的主題名稱。</span><span class="sxs-lookup"><span data-stu-id="39428-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="39428-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="39428-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="39428-141">在服務匯流排命名空間中建立的訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="39428-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="39428-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="39428-142">serviceBusRuleName</span></span>
<span data-ttu-id="39428-143">在服務匯流排命名空間中建立的規則 (篩選器) 名稱。</span><span class="sxs-lookup"><span data-stu-id="39428-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="39428-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="39428-144">serviceBusApiVersion</span></span>
<span data-ttu-id="39428-145">範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="39428-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="39428-146">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="39428-146">Resources to deploy</span></span>
<span data-ttu-id="39428-147">建立**訊息**類型的標準服務匯流排命名空間與主題、訂用帳戶和規則。</span><span class="sxs-lookup"><span data-stu-id="39428-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
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
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="39428-148">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="39428-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="39428-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39428-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="39428-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="39428-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="39428-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39428-151">Next steps</span></span>
<span data-ttu-id="39428-152">現在您已使用 Azure Resource Manager 建立並部署資源，請檢視這些文件，了解如何管理這些資源︰</span><span class="sxs-lookup"><span data-stu-id="39428-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="39428-153">管理 Azure 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="39428-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="39428-154">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="39428-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="39428-155">使用服務匯流排總管管理服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="39428-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

