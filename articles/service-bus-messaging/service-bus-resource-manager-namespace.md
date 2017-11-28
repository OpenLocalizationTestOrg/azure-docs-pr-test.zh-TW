---
title: "使用 Azure Resource Manager 範本 aaaCreate 服務匯流排命名空間 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 toocreate 服務匯流排命名空間"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="50103-103">使用 Azure Resource Manager 範本來建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="50103-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="50103-104">本文說明如何 toouse Azure Resource Manager 範本建立服務匯流排命名空間的型別**傳訊**與 Standard/Basic SKU。</span><span class="sxs-lookup"><span data-stu-id="50103-104">This article describes how toouse an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="50103-105">hello 發行項也會定義 hello 參數所指定的 hello 部署的 hello 執行。</span><span class="sxs-lookup"><span data-stu-id="50103-105">hello article also defines hello parameters that are specified for hello execution of hello deployment.</span></span> <span data-ttu-id="50103-106">您可以使用此範本為您自己的部署，或自訂它 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="50103-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="50103-107">如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="50103-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="50103-108">Hello 完成範本，請參閱 hello[服務匯流排命名空間範本][ Service Bus namespace template] GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="50103-108">For hello complete template, see hello [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="50103-109">hello 下列 Azure 資源管理員範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="50103-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="50103-110">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="50103-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="50103-111">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="50103-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="50103-112">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="50103-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="50103-113">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="50103-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="50103-114">toocheck hello 最新的範本，請瀏覽 hello [Azure 快速入門範本][ Azure Quickstart Templates]組件庫，並搜尋服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="50103-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="50103-115">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="50103-115">What will you deploy?</span></span>
<span data-ttu-id="50103-116">使用此範本時，您將部署具有[基本、標準或進階](https://azure.microsoft.com/pricing/details/service-bus/) SKU 的「服務匯流排」命名空間。</span><span class="sxs-lookup"><span data-stu-id="50103-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="50103-117">toorun 自動 hello 部署，請按一下下列按鈕 hello:</span><span class="sxs-lookup"><span data-stu-id="50103-117">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="50103-118">[![部署 tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="50103-118">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="50103-119">參數</span><span class="sxs-lookup"><span data-stu-id="50103-119">Parameters</span></span>
<span data-ttu-id="50103-120">使用 Azure 資源管理員中，您定義參數的值要 toospecify 部署 hello 範本時。</span><span class="sxs-lookup"><span data-stu-id="50103-120">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="50103-121">hello 範本包括的區段，稱為`Parameters`，其中包含所有 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="50103-121">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="50103-122">您應該定義依據您要部署的 hello 專案，或根據您要部署的 hello 環境而異的那些值的參數。</span><span class="sxs-lookup"><span data-stu-id="50103-122">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="50103-123">不會定義參數的值，會一律保持 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="50103-123">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="50103-124">每個參數值用於 hello 範本 toodefine hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="50103-124">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="50103-125">此範本會定義下列參數的 hello。</span><span class="sxs-lookup"><span data-stu-id="50103-125">This template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="50103-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="50103-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="50103-127">hello 服務匯流排命名空間 toocreate hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="50103-127">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="50103-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="50103-128">serviceBusSKU</span></span>
<span data-ttu-id="50103-129">服務匯流排 hello hello 名稱[SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate。</span><span class="sxs-lookup"><span data-stu-id="50103-129">hello name of hello Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.</span></span>

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="50103-130">hello 範本可定義 hello （Basic、 Standard 或 Premium），此參數允許的值，並指派的預設值 （標準），如果未不指定任何值。</span><span class="sxs-lookup"><span data-stu-id="50103-130">hello template defines hello values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="50103-131">如需服務匯流排定價的詳細資訊，請參閱[服務匯流排定價與計費][Service Bus pricing and billing]。</span><span class="sxs-lookup"><span data-stu-id="50103-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="50103-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="50103-132">serviceBusApiVersion</span></span>
<span data-ttu-id="50103-133">hello hello 範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="50103-133">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a><span data-ttu-id="50103-134">資源 toodeploy</span><span class="sxs-lookup"><span data-stu-id="50103-134">Resources toodeploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="50103-135">服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="50103-135">Service Bus namespace</span></span>
<span data-ttu-id="50103-136">建立 **訊息**類型的標準服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="50103-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="50103-137">命令 toorun 部署</span><span class="sxs-lookup"><span data-stu-id="50103-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="50103-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="50103-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="50103-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="50103-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="50103-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50103-140">Next steps</span></span>
<span data-ttu-id="50103-141">既然您已經建立及部署使用 Azure 資源管理員的資源，了解如何 toomanage 這些資源，藉由讀取這些文件：</span><span class="sxs-lookup"><span data-stu-id="50103-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by reading these articles:</span></span>

* [<span data-ttu-id="50103-142">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="50103-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="50103-143">管理 Service Bus Explorer hello 與服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="50103-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
