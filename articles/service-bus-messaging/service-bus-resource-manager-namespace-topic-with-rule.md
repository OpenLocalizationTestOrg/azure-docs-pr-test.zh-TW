---
title: "aaaCreate Azure 服務匯流排主題訂用帳戶和規則使用 Azure Resource Manager 範本 |Microsoft 文件"
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
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="59c60-103">使用 Azure Resource Manager 範本建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="59c60-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="59c60-104">本文示範如何 toouse Azure Resource Manager 範本，建立服務匯流排命名空間使用主題、 訂用帳戶，以及規則 （篩選）。</span><span class="sxs-lookup"><span data-stu-id="59c60-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="59c60-105">您了解如何 toodefine 部署的資源，以及如何 toodefine 參數指定當 hello 執行部署。</span><span class="sxs-lookup"><span data-stu-id="59c60-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="59c60-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求</span><span class="sxs-lookup"><span data-stu-id="59c60-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="59c60-107">如需關於建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="59c60-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="59c60-108">如需 Azure 資源命名慣例相關實務和模式的詳細資訊，請參閱 [Azure 資源的建議命名慣例][Recommended naming conventions for Azure resources]。</span><span class="sxs-lookup"><span data-stu-id="59c60-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="59c60-109">Hello 完成範本，請參閱 hello[主題、 訂用帳戶，與規則的服務匯流排命名空間][ Service Bus namespace with topic, subscription, and rule]範本。</span><span class="sxs-lookup"><span data-stu-id="59c60-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="59c60-110">hello 下列 Azure 資源管理員範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="59c60-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="59c60-111">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="59c60-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="59c60-112">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="59c60-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="59c60-113">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="59c60-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="59c60-114">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59c60-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="59c60-115">toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="59c60-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="59c60-116">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="59c60-116">What will you deploy?</span></span>

<span data-ttu-id="59c60-117">使用此範本，您將部署具有主題、訂用帳戶和規則 (篩選器) 的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="59c60-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="59c60-118">[服務匯流排主題和訂用帳戶](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions)使用「發佈/訂閱」模式，提供一對多的通訊形式。</span><span class="sxs-lookup"><span data-stu-id="59c60-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="59c60-119">當使用主題和訂用帳戶，不直接的彼此通訊的分散式應用程式元件改為它們會交換訊息，透過可做為媒介的主題。訂用帳戶 tooa 主題類似於虛擬佇列，可接收訊息所送出 toohello 主題的複本。</span><span class="sxs-lookup"><span data-stu-id="59c60-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="59c60-120">訂用帳戶篩選器可讓您 toospecify tooa 主題應該會出現特定主題的訂用帳戶內傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="59c60-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="59c60-121">什麼是規則 (篩選器)？</span><span class="sxs-lookup"><span data-stu-id="59c60-121">What are rules (filters)?</span></span>

<span data-ttu-id="59c60-122">在許多情況下，必須以不同的方式處理具有特定特性的訊息。</span><span class="sxs-lookup"><span data-stu-id="59c60-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="59c60-123">tooenable，您可以設定訂閱 toofind 訊息，有特定的屬性，然後再執行修改 toothose 屬性。</span><span class="sxs-lookup"><span data-stu-id="59c60-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="59c60-124">雖然服務匯流排訂閱可看見所有傳送 toohello 主題的訊息，您僅能複製這些訊息 toohello 虛擬訂閱佇列的子集。</span><span class="sxs-lookup"><span data-stu-id="59c60-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="59c60-125">使用訂用帳戶篩選器即可達成。</span><span class="sxs-lookup"><span data-stu-id="59c60-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="59c60-126">toolearn 進一步了解規則 （篩選），請參閱[規則和動作](service-bus-queues-topics-subscriptions.md#rules-and-actions)。</span><span class="sxs-lookup"><span data-stu-id="59c60-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="59c60-127">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="59c60-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="59c60-128">[![部署 tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="59c60-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="59c60-129">參數</span><span class="sxs-lookup"><span data-stu-id="59c60-129">Parameters</span></span>

<span data-ttu-id="59c60-130">使用 Azure 資源管理員中，您應該定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="59c60-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="59c60-131">hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="59c60-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="59c60-132">您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境不同，這些值的參數。</span><span class="sxs-lookup"><span data-stu-id="59c60-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="59c60-133">不會定義參數的值一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="59c60-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="59c60-134">每個參數值用於 hello 範本 toodefine hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="59c60-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="59c60-135">hello 範本會定義下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="59c60-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="59c60-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="59c60-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="59c60-137">hello 服務匯流排命名空間 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="59c60-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="59c60-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="59c60-138">serviceBusTopicName</span></span>
<span data-ttu-id="59c60-139">hello hello hello 服務匯流排命名空間中建立的主題名稱。</span><span class="sxs-lookup"><span data-stu-id="59c60-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="59c60-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="59c60-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="59c60-141">hello 建立 hello 服務匯流排命名空間中的 hello 訂用帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="59c60-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="59c60-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="59c60-142">serviceBusRuleName</span></span>
<span data-ttu-id="59c60-143">hello hello rule(filter) hello 服務匯流排命名空間中建立名稱。</span><span class="sxs-lookup"><span data-stu-id="59c60-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="59c60-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="59c60-144">serviceBusApiVersion</span></span>
<span data-ttu-id="59c60-145">hello hello 範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="59c60-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="59c60-146">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="59c60-146">Resources toodeploy</span></span>
<span data-ttu-id="59c60-147">建立**訊息**類型的標準服務匯流排命名空間與主題、訂用帳戶和規則。</span><span class="sxs-lookup"><span data-stu-id="59c60-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="59c60-148">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="59c60-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="59c60-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="59c60-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="59c60-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="59c60-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="59c60-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59c60-151">Next steps</span></span>
<span data-ttu-id="59c60-152">既然您已經建立及部署使用 Azure 資源管理員的資源，了解如何 toomanage 檢視這些文件的下列資源：</span><span class="sxs-lookup"><span data-stu-id="59c60-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="59c60-153">管理 Azure 服務匯流排</span><span class="sxs-lookup"><span data-stu-id="59c60-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="59c60-154">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="59c60-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="59c60-155">管理 Service Bus Explorer hello 與服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="59c60-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

