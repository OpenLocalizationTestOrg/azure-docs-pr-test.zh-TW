---
title: "使用 Azure Resource Manager 範本建立服務匯流排授權規則 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本建立命名空間和佇列的服務匯流排授權規則"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fbd2372829a1aefa2c080c0a8a72b9ff4375b16f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="4c597-103">使用 Azure Resource Manager 範本建立命名空間和佇列的服務匯流排授權規則</span><span class="sxs-lookup"><span data-stu-id="4c597-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="4c597-104">本文說明如何使用 Azure Resource Manager 範本，建立服務匯流排命名空間和佇列的[授權規則](service-bus-authentication-and-authorization.md#shared-access-signature-authentication)。</span><span class="sxs-lookup"><span data-stu-id="4c597-104">This article shows how to use an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="4c597-105">您將學習如何定義要部署哪些資源，以及如何定義執行部署時所指定的參數。</span><span class="sxs-lookup"><span data-stu-id="4c597-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="4c597-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="4c597-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="4c597-107">如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="4c597-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="4c597-108">如需完整的範本，請參閱 GitHub 上的[服務匯流排授權規則範本][Service Bus auth rule template]。</span><span class="sxs-lookup"><span data-stu-id="4c597-108">For the complete template, see the [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="4c597-109">下列 Azure Resource Manager 範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="4c597-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="4c597-110">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="4c597-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="4c597-111">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="4c597-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="4c597-112">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4c597-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="4c597-113">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="4c597-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="4c597-114">若要檢查最新的範本，請造訪 [Azure 快速入門範本][Azure Quickstart Templates]資源庫並搜尋「服務匯流排」。</span><span class="sxs-lookup"><span data-stu-id="4c597-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="4c597-115">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="4c597-115">What will you deploy?</span></span>
<span data-ttu-id="4c597-116">使用此範本，您將部署命名空間和訊息實體 (在此情況下為佇列) 的服務匯流排授權規則。</span><span class="sxs-lookup"><span data-stu-id="4c597-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="4c597-117">此範本使用[共用存取簽章 (SAS)](service-bus-sas.md) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4c597-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="4c597-118">SAS 可讓應用程式使用在命名空間或在與特定權限相關聯的訊息實體 (佇列或主題) 上設定的存取金鑰，向服務匯流排進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4c597-118">SAS enables applications to authenticate to Service Bus using an access key configured on the namespace, or on the messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="4c597-119">您可以接著使用此金鑰來產生 SAS 權杖，以便用戶端用來向服務匯流排進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4c597-119">You can then use this key to generate a SAS token that clients can in turn use to authenticate to Service Bus.</span></span>

<span data-ttu-id="4c597-120">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="4c597-120">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="4c597-121">[![部署至 Azure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="4c597-121">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="4c597-122">參數</span><span class="sxs-lookup"><span data-stu-id="4c597-122">Parameters</span></span>

<span data-ttu-id="4c597-123">透過 Azure 資源管理員，您可以定義在部署範本時想要指定之值的參數。</span><span class="sxs-lookup"><span data-stu-id="4c597-123">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="4c597-124">此範本有一個 `Parameters` 區段，內含所有參數值。</span><span class="sxs-lookup"><span data-stu-id="4c597-124">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="4c597-125">您應該為會隨著要部署的專案或要部署到的環境而變化的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="4c597-125">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="4c597-126">請不要為永遠保持不變的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="4c597-126">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="4c597-127">每個參數值都可在範本中用來定義所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="4c597-127">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="4c597-128">範本會定義下列參數。</span><span class="sxs-lookup"><span data-stu-id="4c597-128">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="4c597-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="4c597-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="4c597-130">要建立的服務匯流排命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="4c597-130">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="4c597-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="4c597-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="4c597-132">命名空間的授權規則名稱。</span><span class="sxs-lookup"><span data-stu-id="4c597-132">The name of the authorization rule for the namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="4c597-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="4c597-133">serviceBusQueueName</span></span>
<span data-ttu-id="4c597-134">服務匯流排命名空間中的佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="4c597-134">The name of the queue in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="4c597-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="4c597-135">serviceBusApiVersion</span></span>
<span data-ttu-id="4c597-136">範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="4c597-136">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="4c597-137">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="4c597-137">Resources to deploy</span></span>
<span data-ttu-id="4c597-138">建立 **訊息**類型的標準服務匯流排命名空間，以及命名空間和實體的服務匯流排授權規則。</span><span class="sxs-lookup"><span data-stu-id="4c597-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-to-run-deployment"></a><span data-ttu-id="4c597-139">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="4c597-139">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="4c597-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c597-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="4c597-141">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4c597-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="4c597-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c597-142">Next steps</span></span>
<span data-ttu-id="4c597-143">現在您已使用 Azure Resource Manager 建立並部署資源，請檢視這些文件，了解如何管理這些資源︰</span><span class="sxs-lookup"><span data-stu-id="4c597-143">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="4c597-144">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="4c597-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="4c597-145">使用服務匯流排總管管理服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="4c597-145">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="4c597-146">服務匯流排驗證和授權</span><span class="sxs-lookup"><span data-stu-id="4c597-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
