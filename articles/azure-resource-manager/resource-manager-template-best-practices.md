---
title: "建立資源管理員範本 aaaBest 作法 |Microsoft 文件"
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
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="dd65e-103">建立 Azure Resource Manager 範本的最佳做法</span><span class="sxs-lookup"><span data-stu-id="dd65e-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="dd65e-104">這些指導方針可協助您建立可靠且容易 toouse Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="dd65e-105">hello 指導方針是只建議。</span><span class="sxs-lookup"><span data-stu-id="dd65e-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="dd65e-106">除了另有註明外，它們並非必要項目。</span><span class="sxs-lookup"><span data-stu-id="dd65e-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="dd65e-107">您的案例可能需要 hello 其中一種方法或範例。</span><span class="sxs-lookup"><span data-stu-id="dd65e-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="dd65e-108">資源名稱</span><span class="sxs-lookup"><span data-stu-id="dd65e-108">Resource names</span></span>
<span data-ttu-id="dd65e-109">通常，您會使用 Resource Manager 中的三種資源名稱︰</span><span class="sxs-lookup"><span data-stu-id="dd65e-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="dd65e-110">必須是唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="dd65e-111">資源名稱不需要 toobe 唯一的但您選擇的 tooprovide 的名稱，可協助您找出內容為基礎的資源。</span><span class="sxs-lookup"><span data-stu-id="dd65e-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="dd65e-112">可以是一般的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="dd65e-113">如需有關資源名稱限制的詳細資訊，請參閱 [Recommended naming conventions for Azure resources (Azure 資源的建議命名慣例)](../guidance/guidance-naming-conventions.md)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="dd65e-114">唯一的資源名稱</span><span class="sxs-lookup"><span data-stu-id="dd65e-114">Unique resource names</span></span>
<span data-ttu-id="dd65e-115">您必須為任何有資料存取端點的資源類型，提供唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="dd65e-116">一些需要唯一名稱的常見資源類型包括︰</span><span class="sxs-lookup"><span data-stu-id="dd65e-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="dd65e-117">Azure 儲存體<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="dd65e-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="dd65e-118">Azure App Service 中的 Web Apps 功能</span><span class="sxs-lookup"><span data-stu-id="dd65e-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="dd65e-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dd65e-119">SQL Server</span></span>
* <span data-ttu-id="dd65e-120">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="dd65e-120">Azure Key Vault</span></span>
* <span data-ttu-id="dd65e-121">Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="dd65e-121">Azure Redis Cache</span></span>
* <span data-ttu-id="dd65e-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="dd65e-122">Azure Batch</span></span>
* <span data-ttu-id="dd65e-123">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="dd65e-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="dd65e-124">Azure 搜尋服務</span><span class="sxs-lookup"><span data-stu-id="dd65e-124">Azure Search</span></span>
* <span data-ttu-id="dd65e-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="dd65e-125">Azure HDInsight</span></span>

<span data-ttu-id="dd65e-126"><sup>1</sup> 儲存體帳戶名稱也必須是小寫、長度不超過 24 個字元，而且沒有任何連字號。</span><span class="sxs-lookup"><span data-stu-id="dd65e-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="dd65e-127">如果您提供的資源名稱參數，您必須提供唯一的名稱，當您部署的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="dd65e-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="dd65e-128">（選擇性） 您可以建立的變數，會使用 hello [uniqueString()](resource-group-template-functions-string.md#uniquestring)函式 toogenerate 名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="dd65e-129">您也可能會想 tooadd 前置詞或後置詞 toohello **uniqueString**結果。</span><span class="sxs-lookup"><span data-stu-id="dd65e-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="dd65e-130">修改 hello 唯一名稱可協助您更輕鬆地識別 hello 名稱中的 hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="dd65e-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="dd65e-131">例如，您可以使用下列變數的 hello 產生儲存體帳戶的唯一名稱：</span><span class="sxs-lookup"><span data-stu-id="dd65e-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="dd65e-132">用於識別的資源名稱</span><span class="sxs-lookup"><span data-stu-id="dd65e-132">Resource names for identification</span></span>
<span data-ttu-id="dd65e-133">某些資源類型您可能想 tooname，但其名稱不一定唯一 toobe。</span><span class="sxs-lookup"><span data-stu-id="dd65e-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="dd65e-134">對於這些資源類型，您可以提供識別 hello 資源內容和 hello 資源類型的名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="dd65e-135">提供可協助您識別資源的清單中的 hello 資源的描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="dd65e-136">如果您需要 toouse 不同部署不同的資源名稱，您可以使用參數名稱 hello:</span><span class="sxs-lookup"><span data-stu-id="dd65e-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="dd65e-137">如果您不需要在名稱中的 toopass 在部署期間，您可以使用變數：</span><span class="sxs-lookup"><span data-stu-id="dd65e-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="dd65e-138">您也可以使用硬式編碼的值︰</span><span class="sxs-lookup"><span data-stu-id="dd65e-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="dd65e-139">一般資源名稱</span><span class="sxs-lookup"><span data-stu-id="dd65e-139">Generic resource names</span></span>
<span data-ttu-id="dd65e-140">您主要是透過不同的資源存取的資源類型，您可以使用硬式編碼 hello 範本中的泛型名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="dd65e-141">例如，您可以在 SQL Server 上設定防火牆規則的標準、一般名稱︰</span><span class="sxs-lookup"><span data-stu-id="dd65e-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="dd65e-142">參數</span><span class="sxs-lookup"><span data-stu-id="dd65e-142">Parameters</span></span>
<span data-ttu-id="dd65e-143">hello 下列資訊可能很有幫助您使用的參數：</span><span class="sxs-lookup"><span data-stu-id="dd65e-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="dd65e-144">將參數的使用最小化。</span><span class="sxs-lookup"><span data-stu-id="dd65e-144">Minimize your use of parameters.</span></span> <span data-ttu-id="dd65e-145">可能的話，使用變數或常值。</span><span class="sxs-lookup"><span data-stu-id="dd65e-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="dd65e-146">只針對這些案例使用參數︰</span><span class="sxs-lookup"><span data-stu-id="dd65e-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="dd65e-147">您要根據 tooenvironment SKU、 大小 (容量） toouse 變化的設定。</span><span class="sxs-lookup"><span data-stu-id="dd65e-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="dd65e-148">您想 toospecify 為了易於識別資源名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="dd65e-149">值，您經常使用 toocomplete 其他工作 （例如系統管理員使用者名稱）。</span><span class="sxs-lookup"><span data-stu-id="dd65e-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="dd65e-150">機密資料 (例如密碼)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="dd65e-151">當您建立的資源類型的多個執行個體的值 toouse 的陣列或 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="dd65e-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="dd65e-152">參數名稱使用駝峰式大小寫。</span><span class="sxs-lookup"><span data-stu-id="dd65e-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="dd65e-153">提供在 hello 中繼資料中的每個參數的描述：</span><span class="sxs-lookup"><span data-stu-id="dd65e-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="dd65e-154">定義參數的預設值 (密碼和 SSH 金鑰除外)：</span><span class="sxs-lookup"><span data-stu-id="dd65e-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="dd65e-155">所有密碼和祕密都要使用 **securestring**：</span><span class="sxs-lookup"><span data-stu-id="dd65e-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="dd65e-156">您應該盡可能不使用參數 toospecify 位置。</span><span class="sxs-lookup"><span data-stu-id="dd65e-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="dd65e-157">請改用 hello**位置**hello 資源群組的屬性。</span><span class="sxs-lookup"><span data-stu-id="dd65e-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="dd65e-158">使用 hello **resourceGroup （).location** hello 範本中的資源會部署在運算式中的所有資源，hello 與 hello 資源群組相同的位置：</span><span class="sxs-lookup"><span data-stu-id="dd65e-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
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
   
   <span data-ttu-id="dd65e-159">如果資源類型已支援有限數目的位置，您可能想 toospecify 直接在 hello 範本中的有效位置。</span><span class="sxs-lookup"><span data-stu-id="dd65e-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="dd65e-160">如果您必須使用**位置**參數，該參數值盡可能分享可能 toobe hello 中的資源相同的位置。</span><span class="sxs-lookup"><span data-stu-id="dd65e-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="dd65e-161">這會將系統會要求使用者 tooprovide 位置資訊的 hello 次數降到最低。</span><span class="sxs-lookup"><span data-stu-id="dd65e-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="dd65e-162">避免使用 hello API 版本的資源類型的參數或變數。</span><span class="sxs-lookup"><span data-stu-id="dd65e-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="dd65e-163">資源屬性和值可能會隨版本號碼而不同。</span><span class="sxs-lookup"><span data-stu-id="dd65e-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="dd65e-164">Hello API 版本設定 tooa 參數或變數時，程式碼編輯器中的 IntelliSense 無法判斷 hello 正確的結構描述。</span><span class="sxs-lookup"><span data-stu-id="dd65e-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="dd65e-165">相反地，硬式編碼 hello hello 範本中的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="dd65e-166">變數</span><span class="sxs-lookup"><span data-stu-id="dd65e-166">Variables</span></span>
<span data-ttu-id="dd65e-167">hello 下列資訊可能很有幫助您使用的變數：</span><span class="sxs-lookup"><span data-stu-id="dd65e-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="dd65e-168">使用變數，您需要 toouse 超過一次在範本中的值。</span><span class="sxs-lookup"><span data-stu-id="dd65e-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="dd65e-169">值，只有使用一次，如果硬式編碼值可讓您的範本容易 tooread。</span><span class="sxs-lookup"><span data-stu-id="dd65e-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="dd65e-170">您無法使用 hello[參考](resource-group-template-functions-resource.md#reference)函式在 hello**變數**hello 範本的區段。</span><span class="sxs-lookup"><span data-stu-id="dd65e-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="dd65e-171">hello**參考**函式衍生其值從 hello 資源的執行階段狀態。</span><span class="sxs-lookup"><span data-stu-id="dd65e-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="dd65e-172">不過，在 hello 初始 hello 範本的剖析期間解析變數。</span><span class="sxs-lookup"><span data-stu-id="dd65e-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="dd65e-173">建構需要 hello 值**參考**函式直接在 hello**資源**或**輸出**hello 範本的區段。</span><span class="sxs-lookup"><span data-stu-id="dd65e-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="dd65e-174">如[資源名稱](#resource-names)中所述，包含變數以用於必須是唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="dd65e-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="dd65e-175">您可以將變數組成複雜物件。</span><span class="sxs-lookup"><span data-stu-id="dd65e-175">You can group variables into complex objects.</span></span> <span data-ttu-id="dd65e-176">使用 hello **variable.subentry**格式化 tooreference 複雜物件中的值。</span><span class="sxs-lookup"><span data-stu-id="dd65e-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="dd65e-177">群組變數可協助您追蹤相關的變數。</span><span class="sxs-lookup"><span data-stu-id="dd65e-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="dd65e-178">它還可提升可讀性 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-178">It also improves readability of hello template.</span></span> <span data-ttu-id="dd65e-179">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="dd65e-179">Here's an example:</span></span>
   
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
   > <span data-ttu-id="dd65e-180">複雜物件包含的運算式不可以參考來自複雜物件的值。</span><span class="sxs-lookup"><span data-stu-id="dd65e-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="dd65e-181">請針對此目的，定義個別的變數。</span><span class="sxs-lookup"><span data-stu-id="dd65e-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="dd65e-182">如需使用複雜物件作為變數的進階範例，請參閱 [Azure Resource Manager 範本中的共用狀態](best-practices-resource-manager-state.md)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="dd65e-183">資源</span><span class="sxs-lookup"><span data-stu-id="dd65e-183">Resources</span></span>
<span data-ttu-id="dd65e-184">hello 下列資訊可能很有幫助您使用的資源：</span><span class="sxs-lookup"><span data-stu-id="dd65e-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="dd65e-185">toohelp 了解 hello 資源 hello 用途中，指定其他參與者**註解**hello 範本中的每個資源：</span><span class="sxs-lookup"><span data-stu-id="dd65e-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="dd65e-186">您可以使用標記 tooadd 中繼資料 tooresources。</span><span class="sxs-lookup"><span data-stu-id="dd65e-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="dd65e-187">使用資源的相關中繼資料 tooadd 資訊。</span><span class="sxs-lookup"><span data-stu-id="dd65e-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="dd65e-188">例如，您可以加入資源的中繼資料 toorecord 帳單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dd65e-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="dd65e-189">如需詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="dd65e-190">如果您使用*公用端點*（例如 Azure Blob 儲存體公用端點），在範本中*執行硬式編碼*hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="dd65e-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="dd65e-191">使用 hello**參考**函式 toodynamically 擷取 hello 命名空間。</span><span class="sxs-lookup"><span data-stu-id="dd65e-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="dd65e-192">您可以使用此方法 toodeploy hello 範本 toodifferent 公用命名空間的環境而不需要手動變更 hello 範本中的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="dd65e-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="dd65e-193">設定 hello API 版本 toohello hello 儲存體帳戶在範本中使用的相同版本：</span><span class="sxs-lookup"><span data-stu-id="dd65e-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="dd65e-194">如果 hello 的已部署的 hello 儲存體帳戶所建立的相同範本，您不需要 toospecify hello 提供者命名空間參照 hello 資源時。</span><span class="sxs-lookup"><span data-stu-id="dd65e-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="dd65e-195">這是簡化的 hello 語法：</span><span class="sxs-lookup"><span data-stu-id="dd65e-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="dd65e-196">如果您有在範本中設定的 toouse 公用命名空間的其他值，變更這些值 tooreflect hello 相同**參考**函式。</span><span class="sxs-lookup"><span data-stu-id="dd65e-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="dd65e-197">例如，您可以設定 hello **storageUri** hello 虛擬機器的診斷設定檔的屬性：</span><span class="sxs-lookup"><span data-stu-id="dd65e-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="dd65e-198">您也可以參考不同資源群組中現有的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="dd65e-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="dd65e-199">應用程式需要時才指派公用 IP 位址 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dd65e-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="dd65e-200">tooconnect tooa 虛擬機器 (VM) 針對偵錯，或管理或達成管理目的，使用輸入的 NAT 規則、 虛擬網路閘道或 jumpbox。</span><span class="sxs-lookup"><span data-stu-id="dd65e-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="dd65e-201">如需連接 toovirtual 機器的詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="dd65e-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="dd65e-202">在 Azure 中執行多層式架構的 VM</span><span class="sxs-lookup"><span data-stu-id="dd65e-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="dd65e-203">在 Azure Resource Manager 中設定 VM 的 WinRM 存取</span><span class="sxs-lookup"><span data-stu-id="dd65e-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="dd65e-204">允許外部存取 tooyour VM 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dd65e-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="dd65e-205">允許外部存取 tooyour VM 使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd65e-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="dd65e-206">使用 Azure CLI 允許外部存取 tooyour Linux VM</span><span class="sxs-lookup"><span data-stu-id="dd65e-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="dd65e-207">hello **domainNameLabel**屬性的公用 IP 位址必須是唯一。</span><span class="sxs-lookup"><span data-stu-id="dd65e-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="dd65e-208">hello **domainNameLabel**值必須介於 3 到 63 個字元，並遵循這個規則運算式所指定的 hello 規則： `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`。</span><span class="sxs-lookup"><span data-stu-id="dd65e-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="dd65e-209">因為 hello **uniqueString**函式會產生的字串 13 個字元長，hello **dnsPrefixString**參數是有限的 too50 字元：</span><span class="sxs-lookup"><span data-stu-id="dd65e-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="dd65e-210">當您新增密碼 tooa 自訂指令碼延伸模組時，使用 hello **commandToExecute**屬性在 hello **protectedSettings**屬性：</span><span class="sxs-lookup"><span data-stu-id="dd65e-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
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
   > <span data-ttu-id="dd65e-211">密碼的 tooensure 加密傳遞為參數 tooVMs 和擴充功能時，使用 hello **protectedSettings** hello 相關的延伸模組屬性。</span><span class="sxs-lookup"><span data-stu-id="dd65e-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="dd65e-212">輸出</span><span class="sxs-lookup"><span data-stu-id="dd65e-212">Outputs</span></span>
<span data-ttu-id="dd65e-213">如果您使用範本 toocreate 公用 IP 位址，包括**輸出**傳回 hello IP 位址和 hello 完整的網域名稱 (FQDN) 的詳細資料 > 一節。</span><span class="sxs-lookup"><span data-stu-id="dd65e-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="dd65e-214">在部署之後，您可以使用輸出值 tooeasily 擷取詳細公用 IP 位址和 Fqdn。</span><span class="sxs-lookup"><span data-stu-id="dd65e-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="dd65e-215">當您參考 hello 資源時，使用您用 toocreate hello API 版本它：</span><span class="sxs-lookup"><span data-stu-id="dd65e-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

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

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="dd65e-216">單一範本與巢狀範本</span><span class="sxs-lookup"><span data-stu-id="dd65e-216">Single template vs. nested templates</span></span>
<span data-ttu-id="dd65e-217">toodeploy 方案時，您可以使用單一範本或主要範本與多個巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="dd65e-218">巢狀範本常見於更進階的案例。</span><span class="sxs-lookup"><span data-stu-id="dd65e-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="dd65e-219">使用巢狀的樣板可讓您 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="dd65e-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="dd65e-220">您可以將解決方案分解為多個目標元件。</span><span class="sxs-lookup"><span data-stu-id="dd65e-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="dd65e-221">您可以搭配不同的主要範本重複使用巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="dd65e-222">如果您選擇 toouse 巢狀範本，hello 指導方針可協助您標準化範本設計。</span><span class="sxs-lookup"><span data-stu-id="dd65e-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="dd65e-223">這些指導方針是以 [設計 Azure Resource Manager 範本模式](best-practices-resource-manager-design-templates.md)為基礎。</span><span class="sxs-lookup"><span data-stu-id="dd65e-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="dd65e-224">我們建議您設計具有下列範本的 hello:</span><span class="sxs-lookup"><span data-stu-id="dd65e-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="dd65e-225">**主要範本** (azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="dd65e-226">Hello 輸入參數的使用。</span><span class="sxs-lookup"><span data-stu-id="dd65e-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="dd65e-227">**共用的資源範本**。</span><span class="sxs-lookup"><span data-stu-id="dd65e-227">**Shared resources template**.</span></span> <span data-ttu-id="dd65e-228">使用 toodeploy 共用的所有其他資源正在使用的資源 （例如，虛擬網路和可用性集）。</span><span class="sxs-lookup"><span data-stu-id="dd65e-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="dd65e-229">使用 hello **dependsOn**運算式 tooensure 此範本其他範本之前部署。</span><span class="sxs-lookup"><span data-stu-id="dd65e-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="dd65e-230">**選擇性資源範本**。</span><span class="sxs-lookup"><span data-stu-id="dd65e-230">**Optional resources template**.</span></span> <span data-ttu-id="dd65e-231">使用 tooconditionally 部署參數 (例如，jumpbox) 為基礎的資源。</span><span class="sxs-lookup"><span data-stu-id="dd65e-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="dd65e-232">**成員資源範本**。</span><span class="sxs-lookup"><span data-stu-id="dd65e-232">**Member resources template**.</span></span> <span data-ttu-id="dd65e-233">應用程式層內的每個執行個體類型都有自己的組態。</span><span class="sxs-lookup"><span data-stu-id="dd65e-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="dd65e-234">您可以在一個階層內定義不同的執行個體類型。</span><span class="sxs-lookup"><span data-stu-id="dd65e-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="dd65e-235">（例如，hello 第一個執行個體建立叢集，和 toohello 現有的叢集中加入其他執行個體）。每個執行個體類型有自己的部署範本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="dd65e-236">**指令碼**。</span><span class="sxs-lookup"><span data-stu-id="dd65e-236">**Scripts**.</span></span> <span data-ttu-id="dd65e-237">廣泛可重複使用的指令碼適用於各種個執行個體類型 (例如，將其他磁碟初始化和格式化)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="dd65e-238">針對特定的自訂用途所建立的自訂指令碼會不同，根據 hello 執行個體類型。</span><span class="sxs-lookup"><span data-stu-id="dd65e-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![巢狀範本](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="dd65e-240">如需詳細資訊，請參閱 [透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="dd65e-241">有條件地連結 toonested 範本</span><span class="sxs-lookup"><span data-stu-id="dd65e-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="dd65e-242">您可以使用參數 tooconditionally 連結 toonested 範本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="dd65e-243">hello 參數就會變成 hello URI hello 範本的一部分：</span><span class="sxs-lookup"><span data-stu-id="dd65e-243">hello parameter becomes part of hello URI for hello template:</span></span>

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

## <a name="template-format"></a><span data-ttu-id="dd65e-244">範本格式</span><span class="sxs-lookup"><span data-stu-id="dd65e-244">Template format</span></span>
<span data-ttu-id="dd65e-245">它是很好的作法 toopass 您透過 JSON 驗證程式的範本。</span><span class="sxs-lookup"><span data-stu-id="dd65e-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="dd65e-246">驗證程式可協助您移除在部署期間可能會造成錯誤的多餘逗號、括號及方括號。</span><span class="sxs-lookup"><span data-stu-id="dd65e-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="dd65e-247">請嘗試在您喜愛的編輯環境 (Visual Studio 程式碼、Atom、Sublime Text、Visual Studio) 中使用 [JSONLint](http://jsonlint.com/) 或 linter 套件。</span><span class="sxs-lookup"><span data-stu-id="dd65e-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="dd65e-248">它也是個不錯的主意 tooformat 您的 JSON，以增加可讀性。</span><span class="sxs-lookup"><span data-stu-id="dd65e-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="dd65e-249">您可以對本機的編輯器使用 JSON 格式器封裝。</span><span class="sxs-lookup"><span data-stu-id="dd65e-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="dd65e-250">在 Visual Studio，tooformat hello 文件中，按**Ctrl + K、 Ctrl + D**。</span><span class="sxs-lookup"><span data-stu-id="dd65e-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="dd65e-251">在 Visual Studio 程式碼中，請按 **Alt+Shift+F**。</span><span class="sxs-lookup"><span data-stu-id="dd65e-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="dd65e-252">如果您的本機編輯器並不會格式化 hello 文件，您可以使用[線上格式器](https://www.bing.com/search?q=json+formatter)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd65e-253">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd65e-253">Next steps</span></span>
* <span data-ttu-id="dd65e-254">如需設計虛擬機器解決方案架構的指引，請參閱[在 Azure 中執行 Windows VM](../guidance/guidance-compute-single-vm.md) 和[在 Azure 中執行 Linux VM](../guidance/guidance-compute-single-vm-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="dd65e-255">如需有關設定儲存體帳戶的指引，請參閱 [Azure 儲存體效能與延展性檢查清單](../storage/common/storage-performance-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="dd65e-256">企業可以如何使用資源管理員 tooeffectively toolearn 管理訂用帳戶，請參閱[Azure 企業版 scaffold： 精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="dd65e-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

