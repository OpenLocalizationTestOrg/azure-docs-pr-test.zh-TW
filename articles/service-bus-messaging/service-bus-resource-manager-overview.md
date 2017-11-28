---
title: "使用 Azure Resource Manager 範本 aaaCreate Azure 服務匯流排資源 |Microsoft 文件"
description: "使用 Azure Resource Manager 範本 tooautomate hello 建立服務匯流排資源"
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="1d3d9-103">使用 Azure Resource Manager 範本建立服務匯流排資源</span><span class="sxs-lookup"><span data-stu-id="1d3d9-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="1d3d9-104">本文說明如何 toocreate 及部署服務匯流排資源使用 Azure Resource Manager 範本、 PowerShell 和 hello 服務匯流排資源提供者。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="1d3d9-105">Azure 資源管理員範本可協助您定義 hello 資源 toodeploy 解決方案，及 toospecify 參數和變數可讓您針對不同的環境 tooinput 值。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="1d3d9-106">hello 範本包含 JSON 和您可以為您的部署使用 tooconstruct 值的運算式。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="1d3d9-107">如需撰寫 Azure 資源管理員範本，並討論 hello 範本格式的詳細資訊，請參閱[結構和語法的 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1d3d9-108">如何 hello 這個發行項的顯示中的範例 toouse Azure 資源管理員 toocreate 服務匯流排命名空間和傳訊實體 （佇列）。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="1d3d9-109">如需其他範本的範例，請瀏覽 hello [Azure 快速入門範本組件庫][ Azure Quickstart Templates gallery] ，並搜尋 「 Service Bus 」。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="1d3d9-110">服務匯流排 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="1d3d9-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="1d3d9-111">這些服務匯流排 Azure Resource Manager 範本可供下載和部署。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="1d3d9-112">按一下下列連結以取得有關每個，以在 GitHub 上的連結 toohello 範本的詳細資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="1d3d9-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="1d3d9-113">建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="1d3d9-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="1d3d9-114">建立服務匯流排命名空間與佇列</span><span class="sxs-lookup"><span data-stu-id="1d3d9-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="1d3d9-115">建立服務匯流排命名空間與主題和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1d3d9-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="1d3d9-116">建立服務匯流排命名空間與佇列和授權規則</span><span class="sxs-lookup"><span data-stu-id="1d3d9-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="1d3d9-117">建立服務匯流排命名空間與主題、訂用帳戶和規則</span><span class="sxs-lookup"><span data-stu-id="1d3d9-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="1d3d9-118">使用 PowerShell 部署</span><span class="sxs-lookup"><span data-stu-id="1d3d9-118">Deploy with PowerShell</span></span>

<span data-ttu-id="1d3d9-119">hello 下列程序描述如何 toouse PowerShell toodeploy Azure Resource Manager 範本，建立**標準**層服務匯流排命名空間，而該命名空間內的佇列。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="1d3d9-120">這個範例根據 hello[建立服務匯流排命名空間與佇列](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue)範本。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="1d3d9-121">hello 近似工作流程如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d3d9-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="1d3d9-122">安裝 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-122">Install PowerShell.</span></span>
2. <span data-ttu-id="1d3d9-123">建立 hello 範本以及 （選擇性） 參數檔案。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="1d3d9-124">在 PowerShell 中，登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="1d3d9-125">如果沒有資源群組，請建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="1d3d9-126">測試 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-126">Test hello deployment.</span></span>
6. <span data-ttu-id="1d3d9-127">如有需要，請將 hello 部署模式設定。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="1d3d9-128">部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-128">Deploy hello template.</span></span>

<span data-ttu-id="1d3d9-129">如需部署 Azure Resource Manager 範本的完整資訊，請參閱[使用 Azure Resource Manager 範本部署資源][Deploy resources with Azure Resource Manager templates]。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="1d3d9-130">安裝 PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d3d9-130">Install PowerShell</span></span>

<span data-ttu-id="1d3d9-131">安裝 Azure PowerShell 中的 hello 指示[開始使用 Azure PowerShell](/powershell/azure/get-started-azureps)。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="1d3d9-132">建立範本</span><span class="sxs-lookup"><span data-stu-id="1d3d9-132">Create a template</span></span>

<span data-ttu-id="1d3d9-133">再製或複製 hello [201 servicebus-建立-佇列](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json)從 GitHub 的範本：</span><span class="sxs-lookup"><span data-stu-id="1d3d9-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="1d3d9-134">建立參數檔案 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="1d3d9-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="1d3d9-135">toouse 是選擇性參數檔案，複製 hello [201 servicebus-建立-佇列](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json)檔案。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="1d3d9-136">取代 hello 值`serviceBusNamespaceName`hello hello 服務匯流排命名空間名稱與您想要此部署中 toocreate 值，取代成 hello`serviceBusQueueName`想 toocreate hello hello 佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="1d3d9-137">如需詳細資訊，請參閱 hello[參數](../azure-resource-manager/resource-group-template-deploy.md#parameter-files)主題。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="1d3d9-138">登入 tooAzure 並設定 hello Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1d3d9-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="1d3d9-139">從 PowerShell 提示中，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="1d3d9-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1d3d9-140">您必須提示的 toolog tooyour Azure 帳戶上。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="1d3d9-141">登入之後，執行下列命令 tooview hello 您可用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="1d3d9-142">這個命令會傳回可用的 Azure 訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="1d3d9-143">藉由執行下列命令的 hello 選擇訂閱 hello 目前工作階段。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="1d3d9-144">取代`<YourSubscriptionId>`想 toouse hello GUID hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="1d3d9-145">設定 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="1d3d9-145">Set hello resource group</span></span>

<span data-ttu-id="1d3d9-146">如果您沒有現有的資源群組中，建立新的資源群組以 hello * * 新增 AzureRmResourceGroup * * 命令。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="1d3d9-147">提供 hello 名稱 hello 資源群組及您想要 toouse 的位置。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="1d3d9-148">例如：</span><span class="sxs-lookup"><span data-stu-id="1d3d9-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="1d3d9-149">如果成功，則會顯示 hello 新資源群組的摘要。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="1d3d9-150">測試 hello 部署</span><span class="sxs-lookup"><span data-stu-id="1d3d9-150">Test hello deployment</span></span>

<span data-ttu-id="1d3d9-151">驗證您的部署執行 hello `Test-AzureRmResourceGroupDeployment` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="1d3d9-152">測試時部署 hello，請在相同的方式執行 hello 部署時提供參數。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="1d3d9-153">建立 hello 部署</span><span class="sxs-lookup"><span data-stu-id="1d3d9-153">Create hello deployment</span></span>

<span data-ttu-id="1d3d9-154">toocreate hello 新的部署，執行 hello `New-AzureRmResourceGroupDeployment` cmdlet，並提供出現提示時，即 hello 必要參數。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="1d3d9-155">hello 參數包括您的部署，您的資源群組和 hello 路徑或 URL toohello 範本檔案的 hello 名稱的名稱。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="1d3d9-156">如果 hello**模式**未指定參數，hello 預設值是**Incremental**用。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="1d3d9-157">如需詳細資訊，請參閱[累加部署與完整部署](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="1d3d9-158">hello 下列命令會提示您 hello PowerShell 視窗中的 hello 三個參數：</span><span class="sxs-lookup"><span data-stu-id="1d3d9-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="1d3d9-159">toospecify 參數檔案，請使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="1d3d9-160">當您執行 hello 部署 cmdlet 時，您也可以使用內嵌參數。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="1d3d9-161">hello 命令如下所示：</span><span class="sxs-lookup"><span data-stu-id="1d3d9-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="1d3d9-162">toorun[完成](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments)部署、 設定 hello**模式**參數太**完成**:</span><span class="sxs-lookup"><span data-stu-id="1d3d9-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="1d3d9-163">確認 hello 部署</span><span class="sxs-lookup"><span data-stu-id="1d3d9-163">Verify hello deployment</span></span>
<span data-ttu-id="1d3d9-164">如果已成功部署 hello 資源，hello 部署的摘要會顯示 hello PowerShell 視窗中：</span><span class="sxs-lookup"><span data-stu-id="1d3d9-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1d3d9-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d3d9-165">Next steps</span></span>
<span data-ttu-id="1d3d9-166">您現在已經瞭解 hello 基本工作流程和部署 Azure Resource Manager 範本的命令。</span><span class="sxs-lookup"><span data-stu-id="1d3d9-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="1d3d9-167">如需詳細資訊，請造訪下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="1d3d9-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="1d3d9-168">[Azure Resource Manager 概觀][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="1d3d9-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="1d3d9-169">[使用 Resource Manager 範本與 Azure PowerShell 來部署資源][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="1d3d9-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="1d3d9-170">編寫 Azure 資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="1d3d9-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
