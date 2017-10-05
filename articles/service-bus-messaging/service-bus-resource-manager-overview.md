---
title: "使用 Azure Resource Manager 範本建立 Azure 服務匯流排資源 | Microsoft Docs"
description: "使用 Azure Resource Manager 範本自動建立服務匯流排資源"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="59efb-103">使用 Azure Resource Manager 範本建立服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="59efb-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="59efb-104">本文說明如何使用 Azure Resource Manager 範本、PowerShell 和服務匯流排資源提供者來建立和部署服務匯流排資源。</span><span class="sxs-lookup"><span data-stu-id="59efb-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="59efb-105">Azure Resource Manager 範本會協助您定義要部署給解決方案的資源，以及指定參數和變數，讓您可以針對不同的環境來輸入值。</span><span class="sxs-lookup"><span data-stu-id="59efb-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="59efb-106">範本由 JSON 與運算式所組成，可讓您用來為部署建構值。</span><span class="sxs-lookup"><span data-stu-id="59efb-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="59efb-107">如需撰寫 Azure Resource Manager 範本和討論範本格式的詳細資訊，請參閱 [Azure Resource Manager 範本的結構和語法](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="59efb-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="59efb-108">本文中的範例會示範如何使用 Azure Resource Manager 來建立服務匯流排命名空間和訊息實體 (佇列)。</span><span class="sxs-lookup"><span data-stu-id="59efb-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="59efb-109">如需其他範本範例，請造訪 [Azure 快速入門範本資源庫][Azure Quickstart Templates gallery]並搜尋「服務匯流排」。</span><span class="sxs-lookup"><span data-stu-id="59efb-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="59efb-110">服務匯流排 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="59efb-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="59efb-111">這些服務匯流排 Azure Resource Manager 範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="59efb-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="59efb-112">按一下下列連結可取得各自的詳細資料，並附有 GitHub 上的範本連結：</span><span class="sxs-lookup"><span data-stu-id="59efb-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="59efb-113">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="59efb-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="59efb-114">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="59efb-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="59efb-115">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59efb-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="59efb-116">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="59efb-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="59efb-117">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="59efb-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="59efb-118">使用 PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="59efb-118">Deploy with PowerShell</span></span>

<span data-ttu-id="59efb-119">下列程序描述如何使用 PowerShell 部署建立了**標準**層服務匯流排命名空間的 Azure Resource Manager 範本，以及如何在該命名空間內部署佇列。</span><span class="sxs-lookup"><span data-stu-id="59efb-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="59efb-120">這個範例是以[建立有佇列的服務匯流排命名空間](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue)範本為基礎。</span><span class="sxs-lookup"><span data-stu-id="59efb-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="59efb-121">近似的工作流程如下︰</span><span class="sxs-lookup"><span data-stu-id="59efb-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="59efb-122">安裝 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="59efb-122">Install PowerShell.</span></span>
2. <span data-ttu-id="59efb-123">建立範本和 (選擇性) 參數檔案。</span><span class="sxs-lookup"><span data-stu-id="59efb-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="59efb-124">在 PowerShell 中登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59efb-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="59efb-125">如果沒有資源群組，請建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="59efb-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="59efb-126">測試部署。</span><span class="sxs-lookup"><span data-stu-id="59efb-126">Test the deployment.</span></span>
6. <span data-ttu-id="59efb-127">如有需要，請設定部署模式。</span><span class="sxs-lookup"><span data-stu-id="59efb-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="59efb-128">部署範本。</span><span class="sxs-lookup"><span data-stu-id="59efb-128">Deploy the template.</span></span>

<span data-ttu-id="59efb-129">如需部署 Azure Resource Manager 範本的完整資訊，請參閱[使用 Azure Resource Manager 範本部署資源][Deploy resources with Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="59efb-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="59efb-130">安裝 PowerShell</span><span class="sxs-lookup"><span data-stu-id="59efb-130">Install PowerShell</span></span>

<span data-ttu-id="59efb-131">依照下列指示安裝 Azure PowerShell：[開始使用 Azure PowerShell](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="59efb-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="59efb-132">建立範本</span><span class="sxs-lookup"><span data-stu-id="59efb-132">Create a template</span></span>

<span data-ttu-id="59efb-133">從 GitHub 複製 [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) 範本：</span><span class="sxs-lookup"><span data-stu-id="59efb-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="59efb-134">建立參數檔案 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="59efb-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="59efb-135">若要使用選擇性的參數檔案，請複製 [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) 檔案。</span><span class="sxs-lookup"><span data-stu-id="59efb-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="59efb-136">以您要在這個部署中建立的服務匯流排命名空間名稱取代 `serviceBusNamespaceName` 值，並以您要建立的佇列名稱取代 `serviceBusQueueName` 值。</span><span class="sxs-lookup"><span data-stu-id="59efb-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="59efb-137">如需詳細資訊，請參閱[參數](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)主題。</span><span class="sxs-lookup"><span data-stu-id="59efb-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="59efb-138">登入 Azure 並設定 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59efb-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="59efb-139">從 PowerShell 提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="59efb-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="59efb-140">系統會提示您登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="59efb-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="59efb-141">登入之後，執行下列命令以檢視可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="59efb-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="59efb-142">這個命令會傳回可用的 Azure 訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="59efb-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="59efb-143">執行下列命令為目前的工作階段選擇訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="59efb-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="59efb-144">以您要使用的 Azure 訂用帳戶 GUID取代 `<YourSubscriptionId>`。</span><span class="sxs-lookup"><span data-stu-id="59efb-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="59efb-145">設定資源群組</span><span class="sxs-lookup"><span data-stu-id="59efb-145">Set the resource group</span></span>

<span data-ttu-id="59efb-146">如果沒有現成的資源群組，請使用 **New-AzureRmResourceGroup ** 命令建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="59efb-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="59efb-147">提供您要使用的資源群組名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="59efb-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="59efb-148">例如：</span><span class="sxs-lookup"><span data-stu-id="59efb-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="59efb-149">如果成功，就會顯示新資源群組的摘要。</span><span class="sxs-lookup"><span data-stu-id="59efb-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="59efb-150">測試部署</span><span class="sxs-lookup"><span data-stu-id="59efb-150">Test the deployment</span></span>

<span data-ttu-id="59efb-151">執行 `Test-AzureRmResourceGroupDeployment` Cmdlet 驗證部署。</span><span class="sxs-lookup"><span data-stu-id="59efb-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="59efb-152">測試部署時，請提供與執行部署時完全一致的參數。</span><span class="sxs-lookup"><span data-stu-id="59efb-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="59efb-153">建立部署</span><span class="sxs-lookup"><span data-stu-id="59efb-153">Create the deployment</span></span>

<span data-ttu-id="59efb-154">若要建立新的部署，請執行 `New-AzureRmResourceGroupDeployment` Cmdlet，並於提示出現時提供必要的參數。</span><span class="sxs-lookup"><span data-stu-id="59efb-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="59efb-155">參數會包含部署的名稱、資源群組的名稱，以及範本檔案的路徑或 URL。</span><span class="sxs-lookup"><span data-stu-id="59efb-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="59efb-156">如未指定 **Mode** 參數，即會使用預設值 **Incremental**。</span><span class="sxs-lookup"><span data-stu-id="59efb-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="59efb-157">如需詳細資訊，請參閱[累加部署與完整部署](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)。</span><span class="sxs-lookup"><span data-stu-id="59efb-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="59efb-158">下列命令會提示您在 PowerShell 視窗中輸入三個參數︰</span><span class="sxs-lookup"><span data-stu-id="59efb-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="59efb-159">若要改為指定參數檔案，請使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="59efb-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="59efb-160">執行部署 Cmdlet 時，您也可以使用內嵌參數。</span><span class="sxs-lookup"><span data-stu-id="59efb-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="59efb-161">命令如下所示︰</span><span class="sxs-lookup"><span data-stu-id="59efb-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="59efb-162">若要執行[完整](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)部署，請將 **Mode** 參數設為 **Complete**：</span><span class="sxs-lookup"><span data-stu-id="59efb-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="59efb-163">驗證部署</span><span class="sxs-lookup"><span data-stu-id="59efb-163">Verify the deployment</span></span>
<span data-ttu-id="59efb-164">如果資源成功部署，PowerShell 視窗中就會顯示部署的摘要︰</span><span class="sxs-lookup"><span data-stu-id="59efb-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="59efb-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59efb-165">Next steps</span></span>
<span data-ttu-id="59efb-166">您現在已了解部署 Azure Resource Manager 範本的基本工作流程和命令。</span><span class="sxs-lookup"><span data-stu-id="59efb-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="59efb-167">如需更多的詳細資訊，請瀏覽下列連結內容：</span><span class="sxs-lookup"><span data-stu-id="59efb-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="59efb-168">[Azure Resource Manager 概觀][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="59efb-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="59efb-169">[使用 Resource Manager 範本與 Azure PowerShell 來部署資源][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="59efb-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="59efb-170">編寫 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="59efb-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
