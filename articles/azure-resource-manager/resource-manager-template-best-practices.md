---
title: "建立 Resource Manager 範本的最佳做法 | Microsoft Docs"
description: "簡化 Azure Resource Manager 範本的指導方針。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: a23301ba88279af3f7bf4d353ae808e9eeb0900d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="3807f-103">建立 Azure Resource Manager 範本的最佳做法</span><span class="sxs-lookup"><span data-stu-id="3807f-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="3807f-104">下列指導方針可協助您建立可靠又容易使用的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="3807f-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="3807f-105">指導方針僅為建議。</span><span class="sxs-lookup"><span data-stu-id="3807f-105">The guidelines are only suggestions.</span></span> <span data-ttu-id="3807f-106">除了另有註明外，它們並非必要項目。</span><span class="sxs-lookup"><span data-stu-id="3807f-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="3807f-107">您的案例可能需要下列其中一個方法或範例的變化。</span><span class="sxs-lookup"><span data-stu-id="3807f-107">Your scenario might require a variation of one of the following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="3807f-108">資源名稱</span><span class="sxs-lookup"><span data-stu-id="3807f-108">Resource names</span></span>
<span data-ttu-id="3807f-109">通常，您會使用 Resource Manager 中的三種資源名稱︰</span><span class="sxs-lookup"><span data-stu-id="3807f-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="3807f-110">必須是唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="3807f-111">不需要是唯一的資源名稱，但是您選擇提供的名稱可協助您根據內容識別資源。</span><span class="sxs-lookup"><span data-stu-id="3807f-111">Resource names that are not required to be unique, but you choose to provide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="3807f-112">可以是一般的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="3807f-113">如需有關資源名稱限制的詳細資訊，請參閱 [Recommended naming conventions for Azure resources (Azure 資源的建議命名慣例)](../guidance/guidance-naming-conventions.md)。</span><span class="sxs-lookup"><span data-stu-id="3807f-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="3807f-114">唯一的資源名稱</span><span class="sxs-lookup"><span data-stu-id="3807f-114">Unique resource names</span></span>
<span data-ttu-id="3807f-115">您必須為任何有資料存取端點的資源類型，提供唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="3807f-116">一些需要唯一名稱的常見資源類型包括︰</span><span class="sxs-lookup"><span data-stu-id="3807f-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="3807f-117">Azure 儲存體<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="3807f-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="3807f-118">Azure App Service 中的 Web Apps 功能</span><span class="sxs-lookup"><span data-stu-id="3807f-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="3807f-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3807f-119">SQL Server</span></span>
* <span data-ttu-id="3807f-120">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="3807f-120">Azure Key Vault</span></span>
* <span data-ttu-id="3807f-121">Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="3807f-121">Azure Redis Cache</span></span>
* <span data-ttu-id="3807f-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="3807f-122">Azure Batch</span></span>
* <span data-ttu-id="3807f-123">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="3807f-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="3807f-124">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="3807f-124">Azure Search</span></span>
* <span data-ttu-id="3807f-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3807f-125">Azure HDInsight</span></span>

<span data-ttu-id="3807f-126"><sup>1</sup> 儲存體帳戶名稱也必須是小寫、長度不超過 24 個字元，而且沒有任何連字號。</span><span class="sxs-lookup"><span data-stu-id="3807f-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="3807f-127">如果您提供資源名稱的參數，必須在部署資源時提供唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy the resource.</span></span> <span data-ttu-id="3807f-128">您可以選擇性地建立會使用 [uniqueString()](resource-group-template-functions-string.md#uniquestring) 函式來產生名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="3807f-128">Optionally, you can create a variable that uses the [uniqueString()](resource-group-template-functions-string.md#uniquestring) function to generate a name.</span></span> 

<span data-ttu-id="3807f-129">您也可能想要將首碼或尾碼新增至 **uniqueString** 結果。</span><span class="sxs-lookup"><span data-stu-id="3807f-129">You also might want to add a prefix or suffix to the **uniqueString** result.</span></span> <span data-ttu-id="3807f-130">修改唯一的名稱可協助您更輕鬆地識別名稱的資源類型。</span><span class="sxs-lookup"><span data-stu-id="3807f-130">Modifying the unique name can help you more easily identify the resource type from the name.</span></span> <span data-ttu-id="3807f-131">例如，您可以使用下列變數來產生儲存體帳戶的唯一名稱：</span><span class="sxs-lookup"><span data-stu-id="3807f-131">For example, you can generate a unique name for a storage account by using the following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="3807f-132">用於識別的資源名稱</span><span class="sxs-lookup"><span data-stu-id="3807f-132">Resource names for identification</span></span>
<span data-ttu-id="3807f-133">您可能想要將某些資源類型命名，但其名稱不必是唯一的。</span><span class="sxs-lookup"><span data-stu-id="3807f-133">Some resource types you might want to name, but their names do not have to be unique.</span></span> <span data-ttu-id="3807f-134">針對這些資源類型，您可以提供能識別資源內容和資源類型的名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-134">For these resource types, you can provide a name that identifies both the resource context and the resource type.</span></span> <span data-ttu-id="3807f-135">提供描述性的名稱可協助您識別資源清單中的資源。</span><span class="sxs-lookup"><span data-stu-id="3807f-135">Provide a descriptive name that helps you identify the resource in a list of resources.</span></span> <span data-ttu-id="3807f-136">如果您需要將不同的資源名稱用於不同的部署，可以使用名稱的參數︰</span><span class="sxs-lookup"><span data-stu-id="3807f-136">If you need to use a different resource name for different deployments, you can use a parameter for the name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "The name of the VM to create."
        }
    }
}
```

<span data-ttu-id="3807f-137">如果您不需要在部署期間傳遞名稱，可以使用變數︰</span><span class="sxs-lookup"><span data-stu-id="3807f-137">If you do not need to pass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="3807f-138">您也可以使用硬式編碼的值︰</span><span class="sxs-lookup"><span data-stu-id="3807f-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="3807f-139">一般資源名稱</span><span class="sxs-lookup"><span data-stu-id="3807f-139">Generic resource names</span></span>
<span data-ttu-id="3807f-140">若為主要透過不同資源來存取的資源類型，您可以使用在範本中硬式編碼的一般名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in the template.</span></span> <span data-ttu-id="3807f-141">例如，您可以在 SQL Server 上設定防火牆規則的標準、一般名稱︰</span><span class="sxs-lookup"><span data-stu-id="3807f-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="3807f-142">參數</span><span class="sxs-lookup"><span data-stu-id="3807f-142">Parameters</span></span>
<span data-ttu-id="3807f-143">當您使用參數時，下列資訊可能會很有幫助︰</span><span class="sxs-lookup"><span data-stu-id="3807f-143">The following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="3807f-144">將參數的使用最小化。</span><span class="sxs-lookup"><span data-stu-id="3807f-144">Minimize your use of parameters.</span></span> <span data-ttu-id="3807f-145">可能的話，使用變數或常值。</span><span class="sxs-lookup"><span data-stu-id="3807f-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="3807f-146">只針對這些案例使用參數︰</span><span class="sxs-lookup"><span data-stu-id="3807f-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="3807f-147">您想要根據環境 (SKU、大小、容量) 使用變化的設定。</span><span class="sxs-lookup"><span data-stu-id="3807f-147">Settings that you want to use variations of according to environment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="3807f-148">您希望能方便識別而指定的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-148">Resource names that you want to specify for easy identification.</span></span>
   * <span data-ttu-id="3807f-149">您經常用來完成其他工作 (例如，管理使用者名稱) 的值。</span><span class="sxs-lookup"><span data-stu-id="3807f-149">Values that you use frequently to complete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="3807f-150">機密資料 (例如密碼)。</span><span class="sxs-lookup"><span data-stu-id="3807f-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="3807f-151">建立多個資源類型執行個體時要使用的數字或值陣列。</span><span class="sxs-lookup"><span data-stu-id="3807f-151">The number or array of values to use when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="3807f-152">參數名稱使用駝峰式大小寫。</span><span class="sxs-lookup"><span data-stu-id="3807f-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="3807f-153">在中繼資料中提供每個參數的描述：</span><span class="sxs-lookup"><span data-stu-id="3807f-153">Provide a description of every parameter in the metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "The type of the new storage account created to store the VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="3807f-154">定義參數的預設值 (密碼和 SSH 金鑰除外)：</span><span class="sxs-lookup"><span data-stu-id="3807f-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "The type of the new storage account created to store the VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="3807f-155">所有密碼和祕密都要使用 **securestring**：</span><span class="sxs-lookup"><span data-stu-id="3807f-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "The value of the secret to store in the vault."
           }
       }
   }
   ```

* <span data-ttu-id="3807f-156">可能的話，請勿使用參數來指定位置。</span><span class="sxs-lookup"><span data-stu-id="3807f-156">Whenever possible, don't use a parameter to specify location.</span></span> <span data-ttu-id="3807f-157">請改為使用資源群組的 **location** 屬性。</span><span class="sxs-lookup"><span data-stu-id="3807f-157">Instead, use the **location** property of the resource group.</span></span> <span data-ttu-id="3807f-158">針對所有資源使用 **resourceGroup().location** 運算式，就會將範本中的資源作為資源群組部署在相同的位置：</span><span class="sxs-lookup"><span data-stu-id="3807f-158">By using the **resourceGroup().location** expression for all your resources, resources in the template are deployed in the same location as the resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="3807f-159">如果只在有限的位置支援某資源類型，您可能想要直接在範本中指定有效的位置。</span><span class="sxs-lookup"><span data-stu-id="3807f-159">If a resource type is supported in only a limited number of locations, you might want to specify a valid location directly in the template.</span></span> <span data-ttu-id="3807f-160">如果您必須使用 **location** 參數，請儘可能和可能位於相同位置的資源一起共用該參數值。</span><span class="sxs-lookup"><span data-stu-id="3807f-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely to be in the same location.</span></span> <span data-ttu-id="3807f-161">這樣可以降低系統要求使用者提供位置資訊的次數。</span><span class="sxs-lookup"><span data-stu-id="3807f-161">This minimizes the number of times users are asked to provide location information.</span></span>
* <span data-ttu-id="3807f-162">資源類型的 API 版本要避免使用參數或變數。</span><span class="sxs-lookup"><span data-stu-id="3807f-162">Avoid using a parameter or variable for the API version for a resource type.</span></span> <span data-ttu-id="3807f-163">資源屬性和值可能會隨版本號碼而不同。</span><span class="sxs-lookup"><span data-stu-id="3807f-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="3807f-164">將 API 版本設定為參數或變數時，程式碼編輯器中的 Intellisense 會無法判斷正確的結構描述。</span><span class="sxs-lookup"><span data-stu-id="3807f-164">IntelliSense in a code editor cannot determine the correct schema when the API version is set to a parameter or variable.</span></span> <span data-ttu-id="3807f-165">請改為將 API 版本硬式編碼在範本中。</span><span class="sxs-lookup"><span data-stu-id="3807f-165">Instead, hard-code the API version in the template.</span></span>

## <a name="variables"></a><span data-ttu-id="3807f-166">變數</span><span class="sxs-lookup"><span data-stu-id="3807f-166">Variables</span></span>
<span data-ttu-id="3807f-167">當您使用變數時，下列資訊可能會很有幫助︰</span><span class="sxs-lookup"><span data-stu-id="3807f-167">The following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="3807f-168">您需要在範本中使用一次以上的值，才使用變數。</span><span class="sxs-lookup"><span data-stu-id="3807f-168">Use variables for values that you need to use more than once in a template.</span></span> <span data-ttu-id="3807f-169">如果值只會使用一次，硬式編碼值會讓您的範本較容易看懂。</span><span class="sxs-lookup"><span data-stu-id="3807f-169">If a value is used only once, a hard-coded value makes your template easier to read.</span></span>
* <span data-ttu-id="3807f-170">您不能使用範本之 **variables** 區段中的 [reference](resource-group-template-functions-resource.md#reference) 函式。</span><span class="sxs-lookup"><span data-stu-id="3807f-170">You cannot use the [reference](resource-group-template-functions-resource.md#reference) function in the **variables** section of the template.</span></span> <span data-ttu-id="3807f-171">**reference** 函式的值是從資源的執行階段狀態所衍生。</span><span class="sxs-lookup"><span data-stu-id="3807f-171">The **reference** function derives its value from the resource's runtime state.</span></span> <span data-ttu-id="3807f-172">不過，將範本初始剖析時，會將變數加以解析。</span><span class="sxs-lookup"><span data-stu-id="3807f-172">However, variables are resolved during the initial parsing of the template.</span></span> <span data-ttu-id="3807f-173">請直接在範本的 **resources** 或 **outputs** 區段中，建構需要 **reference** 函式的值。</span><span class="sxs-lookup"><span data-stu-id="3807f-173">Construct values that need the **reference** function directly in the **resources** or **outputs** section of the template.</span></span>
* <span data-ttu-id="3807f-174">如[資源名稱](#resource-names)中所述，包含變數以用於必須是唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="3807f-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="3807f-175">您可以將變數組成複雜物件。</span><span class="sxs-lookup"><span data-stu-id="3807f-175">You can group variables into complex objects.</span></span> <span data-ttu-id="3807f-176">使用 **variable.subentry** 格式，參考來自複雜物件的值。</span><span class="sxs-lookup"><span data-stu-id="3807f-176">Use the **variable.subentry** format to reference a value from a complex object.</span></span> <span data-ttu-id="3807f-177">群組變數可協助您追蹤相關的變數。</span><span class="sxs-lookup"><span data-stu-id="3807f-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="3807f-178">它也可以改善範本的可讀性。</span><span class="sxs-lookup"><span data-stu-id="3807f-178">It also improves readability of the template.</span></span> <span data-ttu-id="3807f-179">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="3807f-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="3807f-180">複雜物件包含的運算式不可以參考來自複雜物件的值。</span><span class="sxs-lookup"><span data-stu-id="3807f-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="3807f-181">請針對此目的，定義個別的變數。</span><span class="sxs-lookup"><span data-stu-id="3807f-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="3807f-182">如需使用複雜物件作為變數的進階範例，請參閱 [Azure Resource Manager 範本中的共用狀態](best-practices-resource-manager-state.md)。</span><span class="sxs-lookup"><span data-stu-id="3807f-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="3807f-183">資源</span><span class="sxs-lookup"><span data-stu-id="3807f-183">Resources</span></span>
<span data-ttu-id="3807f-184">當您使用資源時，下列資訊可能會很有幫助︰</span><span class="sxs-lookup"><span data-stu-id="3807f-184">The following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="3807f-185">針對範本中的每個資源指定 **comments**，協助其他參與者了解資源的用途：</span><span class="sxs-lookup"><span data-stu-id="3807f-185">To help other contributors understand the purpose of the resource, specify **comments** for each resource in the template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used to store the VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="3807f-186">您可以使用標記，將中繼資料新增至資源。</span><span class="sxs-lookup"><span data-stu-id="3807f-186">You can use tags to add metadata to resources.</span></span> <span data-ttu-id="3807f-187">使用中繼資料來新增資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3807f-187">Use metadata to add information about your resources.</span></span> <span data-ttu-id="3807f-188">例如，您可以新增中繼資料，來記錄資源的帳單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3807f-188">For example, you can add metadata to record billing details for a resource.</span></span> <span data-ttu-id="3807f-189">如需詳細資訊，請參閱 [使用標記組織您的 Azure 資源](resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="3807f-189">For more information, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="3807f-190">如果您使用範本中的公用端點 (例如 Azure Blob 儲存體公用端點)，請勿將命名空間硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="3807f-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* the namespace.</span></span> <span data-ttu-id="3807f-191">使用 **reference** 函式，動態擷取命名空間。</span><span class="sxs-lookup"><span data-stu-id="3807f-191">Use the **reference** function to dynamically retrieve the namespace.</span></span> <span data-ttu-id="3807f-192">您可以使用此方法可將範本部署到不同的公用命名空間環境中，而不需要將範本中的端點手動變更。</span><span class="sxs-lookup"><span data-stu-id="3807f-192">You can use this approach to deploy the template to different public namespace environments without manually changing the endpoint in the template.</span></span> <span data-ttu-id="3807f-193">將 API 版本設定成與您在範本中用於儲存體帳戶相同的版本：</span><span class="sxs-lookup"><span data-stu-id="3807f-193">Set the API version to the same version that you are using for the storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="3807f-194">如果將該儲存體帳戶部署在您要建立的相同範本中，當您參考資源時，即不需要指定提供者命名空間。</span><span class="sxs-lookup"><span data-stu-id="3807f-194">If the storage account is deployed in the same template that you are creating, you do not need to specify the provider namespace when you reference the resource.</span></span> <span data-ttu-id="3807f-195">簡化的語法如下︰</span><span class="sxs-lookup"><span data-stu-id="3807f-195">This is the simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="3807f-196">如果您範本中其他的值是使用公用命名空間進行設定，請變更這些值以反映相同的 **reference** 函式。</span><span class="sxs-lookup"><span data-stu-id="3807f-196">If you have other values in your template that are configured to use a public namespace, change these values to reflect the same **reference** function.</span></span> <span data-ttu-id="3807f-197">例如，您可以設定虛擬機器診斷設定檔的 **storageUri** 屬性：</span><span class="sxs-lookup"><span data-stu-id="3807f-197">For example, you can set the **storageUri** property of the virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="3807f-198">您也可以參考不同資源群組中現有的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="3807f-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="3807f-199">只有在應用程式要求時，才將公用 IP 位址指派給虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3807f-199">Assign public IP addresses to a virtual machine only when an application requires it.</span></span> <span data-ttu-id="3807f-200">若要連線至虛擬機器 (VM) 進行偵錯，或要進行管理或系統管理，請使用輸入 NAT 規則、虛擬網路閘道或 Jumpbox。</span><span class="sxs-lookup"><span data-stu-id="3807f-200">To connect to a virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="3807f-201">如需有關如何連線至虛擬機器的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="3807f-201">For more information about connecting to virtual machines, see:</span></span>
   
   * [<span data-ttu-id="3807f-202">在 Azure 中執行多層式架構的 VM</span><span class="sxs-lookup"><span data-stu-id="3807f-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="3807f-203">在 Azure Resource Manager 中設定 VM 的 WinRM 存取</span><span class="sxs-lookup"><span data-stu-id="3807f-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="3807f-204">允許使用 Azure 入口網站從外部存取您的 VM</span><span class="sxs-lookup"><span data-stu-id="3807f-204">Allow external access to your VM by using the Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="3807f-205">允許使用 PowerShell 從外部存取您的 VM</span><span class="sxs-lookup"><span data-stu-id="3807f-205">Allow external access to your VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="3807f-206">允許使用 Azure CLI 從外部存取您的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="3807f-206">Allow external access to your Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="3807f-207">公用 IP 位址的 **domainNameLabel** 屬性必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="3807f-207">The **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="3807f-208">**domainNameLabel** 值的長度必須介於 3 到 63 個字元之間，還要遵循這個規則運算式指定的規則：`^[a-z][a-z0-9-]{1,61}[a-z0-9]$`。</span><span class="sxs-lookup"><span data-stu-id="3807f-208">The **domainNameLabel** value must be between 3 and 63 characters long, and follow the rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="3807f-209">**uniqueString** 函式會產生長度為 13 個字元的字串，因此 **dnsPrefixString** 參數會限制為 50 個字元：</span><span class="sxs-lookup"><span data-stu-id="3807f-209">Because the **uniqueString** function generates a string that is 13 characters long, the **dnsPrefixString** parameter is limited to 50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "The DNS label for the public IP address. It must be lowercase. It should match the following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="3807f-210">將密碼新增至自訂指令碼擴充功能時，使用 **protectedSettings** 屬性中的 **commandToExecute** 屬性。</span><span class="sxs-lookup"><span data-stu-id="3807f-210">When you add a password to a custom script extension, use the **commandToExecute** property in the **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="3807f-211">為了確保作為參數傳遞至 VM 和擴充功能的祕密會經過加密，請使用相關擴充功能的 **protectedSettings** 屬性。</span><span class="sxs-lookup"><span data-stu-id="3807f-211">To ensure that secrets are encrypted when they are passed as parameters to VMs and extensions, use the **protectedSettings** property of the relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="3807f-212">輸出</span><span class="sxs-lookup"><span data-stu-id="3807f-212">Outputs</span></span>
<span data-ttu-id="3807f-213">如果您使用範本建立公用 IP 位址，則請包含 **outputs** 區段以傳回 IP 位址和完整網域名稱的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3807f-213">If you use a template to create public IP addresses, include an **outputs** section that returns details of the IP address and the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="3807f-214">您可以使用輸出值，輕鬆在部署後擷取公用 IP 位址和 FQDN 的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3807f-214">You can use output values to easily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="3807f-215">參考資源時，請使用當時用來建立該資源的 API 版本：</span><span class="sxs-lookup"><span data-stu-id="3807f-215">When you reference the resource, use the API version that you used to create it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="3807f-216">單一範本與巢狀範本</span><span class="sxs-lookup"><span data-stu-id="3807f-216">Single template vs. nested templates</span></span>
<span data-ttu-id="3807f-217">若要部署解決方案，您可以使用單一範本或有多個巢狀範本的主要範本。</span><span class="sxs-lookup"><span data-stu-id="3807f-217">To deploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="3807f-218">巢狀範本常見於更進階的案例。</span><span class="sxs-lookup"><span data-stu-id="3807f-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="3807f-219">使用巢狀範本會提供您下列優點︰</span><span class="sxs-lookup"><span data-stu-id="3807f-219">Using a nested template gives you the following advantages:</span></span>

* <span data-ttu-id="3807f-220">您可以將解決方案分解為多個目標元件。</span><span class="sxs-lookup"><span data-stu-id="3807f-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="3807f-221">您可以搭配不同的主要範本重複使用巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="3807f-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="3807f-222">如果您選擇使用巢狀範本，下列指導方針可協助您將範本設計標準化。</span><span class="sxs-lookup"><span data-stu-id="3807f-222">If you choose to use nested templates, the following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="3807f-223">這些指導方針是以 [設計 Azure Resource Manager 範本模式](best-practices-resource-manager-design-templates.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="3807f-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="3807f-224">我們建議具有下列範本的設計︰</span><span class="sxs-lookup"><span data-stu-id="3807f-224">We recommend a design that has the following templates:</span></span>

* <span data-ttu-id="3807f-225">**主要範本** (azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="3807f-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="3807f-226">用於輸入參數。</span><span class="sxs-lookup"><span data-stu-id="3807f-226">Use for the input parameters.</span></span>
* <span data-ttu-id="3807f-227">**共用的資源範本**。</span><span class="sxs-lookup"><span data-stu-id="3807f-227">**Shared resources template**.</span></span> <span data-ttu-id="3807f-228">用於部署所有其他資源可以使用的共用資源 (例如虛擬網路和可用性設定組)。</span><span class="sxs-lookup"><span data-stu-id="3807f-228">Use to deploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="3807f-229">使用 **dependsOn** 運算式可確保在其他範本之前部署此範本。</span><span class="sxs-lookup"><span data-stu-id="3807f-229">Use the **dependsOn** expression to ensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="3807f-230">**選擇性資源範本**。</span><span class="sxs-lookup"><span data-stu-id="3807f-230">**Optional resources template**.</span></span> <span data-ttu-id="3807f-231">用於根據參數 (例如 jumpbox) 有條件地部署資源。</span><span class="sxs-lookup"><span data-stu-id="3807f-231">Use to conditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="3807f-232">**成員資源範本**。</span><span class="sxs-lookup"><span data-stu-id="3807f-232">**Member resources template**.</span></span> <span data-ttu-id="3807f-233">應用程式層內的每個執行個體類型都有自己的組態。</span><span class="sxs-lookup"><span data-stu-id="3807f-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="3807f-234">您可以在一個階層內定義不同的執行個體類型。</span><span class="sxs-lookup"><span data-stu-id="3807f-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="3807f-235">(例如，第一個執行個體會建立叢集，而其他執行個體會新增至現有的叢集。)每個執行個體類型有自己的部署範本。</span><span class="sxs-lookup"><span data-stu-id="3807f-235">(For example, the first instance creates a cluster, and additional instances are added to the existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="3807f-236">**指令碼**。</span><span class="sxs-lookup"><span data-stu-id="3807f-236">**Scripts**.</span></span> <span data-ttu-id="3807f-237">廣泛可重複使用的指令碼適用於各種個執行個體類型 (例如，將其他磁碟初始化和格式化)。</span><span class="sxs-lookup"><span data-stu-id="3807f-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="3807f-238">您針對特定自訂用途而建立的自訂指令碼，會根據各種執行個體類型而不同。</span><span class="sxs-lookup"><span data-stu-id="3807f-238">Custom scripts that you create for a specific customization purpose are different, based on the instance type.</span></span>

![巢狀範本](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="3807f-240">如需詳細資訊，請參閱 [透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3807f-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-to-nested-templates"></a><span data-ttu-id="3807f-241">有條件地連結到巢狀範本</span><span class="sxs-lookup"><span data-stu-id="3807f-241">Conditionally link to nested templates</span></span>
<span data-ttu-id="3807f-242">您可以使用參數，有條件地連結到巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="3807f-242">You can use a parameter to conditionally link to nested templates.</span></span> <span data-ttu-id="3807f-243">參數會變成範本 URI 的一部分︰</span><span class="sxs-lookup"><span data-stu-id="3807f-243">The parameter becomes part of the URI for the template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="3807f-244">範本格式</span><span class="sxs-lookup"><span data-stu-id="3807f-244">Template format</span></span>
<span data-ttu-id="3807f-245">最好將您的範本透過 JSON 驗證程式傳遞。</span><span class="sxs-lookup"><span data-stu-id="3807f-245">It's a good practice to pass your template through a JSON validator.</span></span> <span data-ttu-id="3807f-246">驗證程式可協助您移除在部署期間可能會造成錯誤的多餘逗號、括號及方括號。</span><span class="sxs-lookup"><span data-stu-id="3807f-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="3807f-247">請嘗試在您喜愛的編輯環境 (Visual Studio 程式碼、Atom、Sublime Text、Visual Studio) 中使用 [JSONLint](http://jsonlint.com/) 或 linter 套件。</span><span class="sxs-lookup"><span data-stu-id="3807f-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="3807f-248">也建議您將 JSON 格式化以更方便閱讀。</span><span class="sxs-lookup"><span data-stu-id="3807f-248">It's also a good idea to format your JSON for better readability.</span></span> <span data-ttu-id="3807f-249">您可以對本機的編輯器使用 JSON 格式器封裝。</span><span class="sxs-lookup"><span data-stu-id="3807f-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="3807f-250">在 Visual Studio 中，若要格式化文件，請按 **Ctrl+K、Ctrl+D**。</span><span class="sxs-lookup"><span data-stu-id="3807f-250">In Visual Studio, to format the document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="3807f-251">在 Visual Studio 程式碼中，請按 **Alt+Shift+F**。</span><span class="sxs-lookup"><span data-stu-id="3807f-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="3807f-252">如果您的本機編輯器並不會格式化文件，您可以使用 [線上格式器](https://www.bing.com/search?q=json+formatter)。</span><span class="sxs-lookup"><span data-stu-id="3807f-252">If your local editor doesn't format the document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3807f-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3807f-253">Next steps</span></span>
* <span data-ttu-id="3807f-254">如需設計虛擬機器解決方案架構的指引，請參閱[在 Azure 中執行 Windows VM](../guidance/guidance-compute-single-vm.md) 和[在 Azure 中執行 Linux VM](../guidance/guidance-compute-single-vm-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="3807f-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="3807f-255">如需有關設定儲存體帳戶的指引，請參閱 [Azure 儲存體效能與延展性檢查清單](../storage/common/storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="3807f-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="3807f-256">若要深入了解企業如何使用 Resource Manager 有效地管理訂閱，請參閱 [Azure 企業 Scaffold：規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="3807f-256">To learn about how an enterprise can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

