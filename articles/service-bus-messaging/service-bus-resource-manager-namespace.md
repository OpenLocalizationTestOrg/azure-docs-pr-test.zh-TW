---
title: "使用 Azure Resource Manager 範本建立服務匯流排命名空間 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本來建立服務匯流排命名空間"
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
ms.openlocfilehash: 8fff390919a1807995646dab322b4cbe56dd0268
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a><span data-ttu-id="a8e32-103">使用 Azure Resource Manager 範本來建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="a8e32-103">Create a Service Bus namespace using an Azure Resource Manager template</span></span>

<span data-ttu-id="a8e32-104">本文說明如何使用 Azure Resource Manager 範本，建立**訊息**類型的服務匯流排命名空間與標準/基本 SKU。</span><span class="sxs-lookup"><span data-stu-id="a8e32-104">This article describes how to use an Azure Resource Manager template that creates a Service Bus namespace of type **Messaging** with a Standard/Basic SKU.</span></span> <span data-ttu-id="a8e32-105">本文也會定義針對部署執行而指定的參數。</span><span class="sxs-lookup"><span data-stu-id="a8e32-105">The article also defines the parameters that are specified for the execution of the deployment.</span></span> <span data-ttu-id="a8e32-106">您可以直接在自己的部署中使用此範本，或自訂此範本以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="a8e32-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="a8e32-107">如需建立範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本][Authoring Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="a8e32-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="a8e32-108">如需完整的範本，請參閱 GitHub 上的 [服務匯流排命名空間範本][Service Bus namespace template]。</span><span class="sxs-lookup"><span data-stu-id="a8e32-108">For the complete template, see the [Service Bus namespace template][Service Bus namespace template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="a8e32-109">下列 Azure Resource Manager 範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="a8e32-109">The following Azure Resource Manager templates are available for download and deployment.</span></span> 
> 
> * [<span data-ttu-id="a8e32-110">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="a8e32-110">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="a8e32-111">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a8e32-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="a8e32-112">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="a8e32-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="a8e32-113">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="a8e32-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="a8e32-114">若要檢查最新的範本，請造訪 [Azure 快速入門範本][Azure Quickstart Templates]資源庫並搜尋「服務匯流排」。</span><span class="sxs-lookup"><span data-stu-id="a8e32-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="a8e32-115">您將部署什麼？</span><span class="sxs-lookup"><span data-stu-id="a8e32-115">What will you deploy?</span></span>
<span data-ttu-id="a8e32-116">使用此範本時，您將部署具有[基本、標準或進階](https://azure.microsoft.com/pricing/details/service-bus/) SKU 的「服務匯流排」命名空間。</span><span class="sxs-lookup"><span data-stu-id="a8e32-116">With this template, you will deploy a Service Bus namespace with a [Basic, Standard, or Premium](https://azure.microsoft.com/pricing/details/service-bus/) SKU.</span></span>

<span data-ttu-id="a8e32-117">若要自動執行部署，請按一下下列按鈕：</span><span class="sxs-lookup"><span data-stu-id="a8e32-117">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="a8e32-118">[![部署至 Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="a8e32-118">[![Deploy to Azure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="a8e32-119">參數</span><span class="sxs-lookup"><span data-stu-id="a8e32-119">Parameters</span></span>
<span data-ttu-id="a8e32-120">透過 Azure 資源管理員，您可以定義在部署範本時想要指定之值的參數。</span><span class="sxs-lookup"><span data-stu-id="a8e32-120">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="a8e32-121">此範本有一個 `Parameters` 區段，內含所有參數值。</span><span class="sxs-lookup"><span data-stu-id="a8e32-121">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="a8e32-122">您應該為會隨著要部署的專案或要部署到的環境而變化的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="a8e32-122">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="a8e32-123">請不要為永遠保持不變的值定義參數。</span><span class="sxs-lookup"><span data-stu-id="a8e32-123">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="a8e32-124">每個參數值都可在範本中用來定義所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="a8e32-124">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="a8e32-125">此範本會定義下列參數。</span><span class="sxs-lookup"><span data-stu-id="a8e32-125">This template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="a8e32-126">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="a8e32-126">serviceBusNamespaceName</span></span>
<span data-ttu-id="a8e32-127">要建立的服務匯流排命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="a8e32-127">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebussku"></a><span data-ttu-id="a8e32-128">serviceBusSKU</span><span class="sxs-lookup"><span data-stu-id="a8e32-128">serviceBusSKU</span></span>
<span data-ttu-id="a8e32-129">要建立的服務匯流 [SKU](https://azure.microsoft.com/pricing/details/service-bus/) 名稱。</span><span class="sxs-lookup"><span data-stu-id="a8e32-129">The name of the Service Bus [SKU](https://azure.microsoft.com/pricing/details/service-bus/) to create.</span></span>

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
        "description": "The messaging tier for service Bus namespace" 
    } 

```

<span data-ttu-id="a8e32-130">此範本會定義此參數允許使用的值 (Basic、Standard 或 Premium)，並指派未指定任何值時的預設值 (Standard)。</span><span class="sxs-lookup"><span data-stu-id="a8e32-130">The template defines the values that are permitted for this parameter (Basic, Standard, or Premium) and assigns a default value (Standard) if no value is specified.</span></span>

<span data-ttu-id="a8e32-131">如需服務匯流排定價的詳細資訊，請參閱[服務匯流排定價與計費][Service Bus pricing and billing]。</span><span class="sxs-lookup"><span data-stu-id="a8e32-131">For more information about Service Bus pricing, see [Service Bus pricing and billing][Service Bus pricing and billing].</span></span>

### <a name="servicebusapiversion"></a><span data-ttu-id="a8e32-132">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="a8e32-132">serviceBusApiVersion</span></span>
<span data-ttu-id="a8e32-133">範本的服務匯流排 API 版本。</span><span class="sxs-lookup"><span data-stu-id="a8e32-133">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by the template" 
       } 
```

## <a name="resources-to-deploy"></a><span data-ttu-id="a8e32-134">要部署的資源</span><span class="sxs-lookup"><span data-stu-id="a8e32-134">Resources to deploy</span></span>
### <a name="service-bus-namespace"></a><span data-ttu-id="a8e32-135">服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="a8e32-135">Service Bus namespace</span></span>
<span data-ttu-id="a8e32-136">建立 **訊息**類型的標準服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="a8e32-136">Creates a standard Service Bus namespace of type **Messaging**.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="a8e32-137">執行部署的命令</span><span class="sxs-lookup"><span data-stu-id="a8e32-137">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="a8e32-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a8e32-138">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a><span data-ttu-id="a8e32-139">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8e32-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a><span data-ttu-id="a8e32-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8e32-140">Next steps</span></span>
<span data-ttu-id="a8e32-141">現在您已使用 Azure Resource Manager 建立並部署資源，請參閱這些文件，了解如何管理這些資源︰</span><span class="sxs-lookup"><span data-stu-id="a8e32-141">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by reading these articles:</span></span>

* [<span data-ttu-id="a8e32-142">使用 PowerShell 管理服務匯流排</span><span class="sxs-lookup"><span data-stu-id="a8e32-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="a8e32-143">使用服務匯流排總管管理服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="a8e32-143">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
