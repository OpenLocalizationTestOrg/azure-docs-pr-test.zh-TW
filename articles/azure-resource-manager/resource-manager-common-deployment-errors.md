---
title: "aaaTroubleshoot 常見的 Azure 部署錯誤 |Microsoft 文件"
description: "描述如何部署使用 Azure 資源管理員資源 tooAzure 時 tooresolve 常見錯誤。"
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "部署錯誤，azure 部署，部署 tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="604ca-104">使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="604ca-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="604ca-105">本主題說明如何解決可能會遇到的一些常見 Azure 部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="604ca-106">本主題將描述下列錯誤碼 hello:</span><span class="sxs-lookup"><span data-stu-id="604ca-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="604ca-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="604ca-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="604ca-108">授權失敗</span><span class="sxs-lookup"><span data-stu-id="604ca-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="604ca-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="604ca-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="604ca-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="604ca-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="604ca-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="604ca-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="604ca-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="604ca-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="604ca-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="604ca-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="604ca-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="604ca-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="604ca-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="604ca-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="604ca-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="604ca-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="604ca-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="604ca-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="604ca-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="604ca-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="604ca-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="604ca-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="604ca-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="604ca-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="604ca-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="604ca-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="604ca-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="604ca-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="604ca-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="604ca-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="604ca-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="604ca-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="604ca-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="604ca-125">DeploymentFailed</span></span>

<span data-ttu-id="604ca-126">此錯誤碼指出一般的部署錯誤，但它不是您需要疑難排解 toostart hello 的錯誤代碼。</span><span class="sxs-lookup"><span data-stu-id="604ca-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="604ca-127">hello 實際上可協助您解決 hello 問題錯誤碼通常是以下這個錯誤的一個層級。</span><span class="sxs-lookup"><span data-stu-id="604ca-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="604ca-128">例如，hello 下列影像顯示 hello **RequestDisallowedByPolicy**低於 hello 部署錯誤的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="604ca-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![顯示錯誤碼](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="604ca-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="604ca-130">SkuNotAvailable</span></span>

<span data-ttu-id="604ca-131">部署資源 （通常是虛擬機器），您可能會收到 hello 下錯誤程式碼和錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="604ca-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="604ca-132">Hello 資源 （例如 VM 大小），您已選取的 SKU 不適用於您所選取的 hello 位置時，您會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="604ca-133">tooresolve 此問題，您需要 toodetermine Sku 可用區域中。</span><span class="sxs-lookup"><span data-stu-id="604ca-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="604ca-134">您可以使用 PowerShell、 hello 入口網站或 REST 作業 toofind 可用的 Sku。</span><span class="sxs-lookup"><span data-stu-id="604ca-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="604ca-135">若是 PowerShell，請使用 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 並依位置篩選。</span><span class="sxs-lookup"><span data-stu-id="604ca-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="604ca-136">您必須擁有 hello 最新版的 PowerShell 此命令。</span><span class="sxs-lookup"><span data-stu-id="604ca-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="604ca-137">hello 結果包括 Sku hello 位置清單，以及適用於該 SKU 任何限制。</span><span class="sxs-lookup"><span data-stu-id="604ca-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="604ca-138">toouse hello[入口網站](https://portal.azure.com)、 登入 toohello 入口網站，並加入透過 hello 介面資源。</span><span class="sxs-lookup"><span data-stu-id="604ca-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="604ca-139">當您設定 hello 值，您會看到 hello 可用的 Sku，該資源。</span><span class="sxs-lookup"><span data-stu-id="604ca-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="604ca-140">您不需要 toocomplete hello 部署。</span><span class="sxs-lookup"><span data-stu-id="604ca-140">You do not need toocomplete hello deployment.</span></span>

    ![可用的 SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="604ca-142">虛擬機器的 toouse hello REST API 傳送 hello 下列要求：</span><span class="sxs-lookup"><span data-stu-id="604ca-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="604ca-143">它會傳回可用的 Sku 和區域中 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="604ca-143">It returns available SKUs and regions in hello following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="604ca-144">如果您無法 toofind 該地區或符合商務需求的其他區域中的適當 SKU，提交[SKU 要求](https://aka.ms/skurestriction)tooAzure 支援。</span><span class="sxs-lookup"><span data-stu-id="604ca-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="604ca-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="604ca-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="604ca-146">如果您收到這個錯誤，您使用的訂用帳戶不允許 tooaccess Azure Active Directory 以外的任何 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="604ca-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="604ca-147">需要 tooaccess hello 傳統入口網站，但不是允許 toodeploy 資源後，您可能會出現這種類型的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="604ca-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="604ca-148">tooresolve 此問題，您必須使用有權限 toodeploy 資源的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="604ca-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="604ca-149">tooview 您可用的訂用帳戶使用 PowerShell，使用：</span><span class="sxs-lookup"><span data-stu-id="604ca-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="604ca-150">此外，tooset hello 目前訂用帳戶，使用：</span><span class="sxs-lookup"><span data-stu-id="604ca-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="604ca-151">tooview 您可用的訂用帳戶使用 Azure CLI 2.0 中，使用：</span><span class="sxs-lookup"><span data-stu-id="604ca-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="604ca-152">此外，tooset hello 目前訂用帳戶，使用：</span><span class="sxs-lookup"><span data-stu-id="604ca-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="604ca-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="604ca-153">InvalidTemplate</span></span>
<span data-ttu-id="604ca-154">此錯誤可能起因於數個不同類型的錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="604ca-155">語法錯誤</span><span class="sxs-lookup"><span data-stu-id="604ca-155">Syntax error</span></span>

   <span data-ttu-id="604ca-156">如果您收到錯誤訊息，指出 hello 範本無法驗證時，您可能在範本中有語法問題。</span><span class="sxs-lookup"><span data-stu-id="604ca-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="604ca-157">這個錯誤，所以簡單 toomake 範本運算式可能很複雜。</span><span class="sxs-lookup"><span data-stu-id="604ca-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="604ca-158">例如，hello 下列名稱指派儲存體帳戶都包含一組括號、 三個函式、 三組括號、 一組的單引號和一個屬性：</span><span class="sxs-lookup"><span data-stu-id="604ca-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="604ca-159">如果您未提供 hello 比對語法，hello 範本會產生值將會不同於您的意圖。</span><span class="sxs-lookup"><span data-stu-id="604ca-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="604ca-160">當您收到這種類型的錯誤時，請仔細檢閱 hello 運算式語法。</span><span class="sxs-lookup"><span data-stu-id="604ca-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="604ca-161">請考慮使用 [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 或 [Visual Studio Code](resource-manager-vs-code.md) 等 JSON 編輯器，它們可以警告您有語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="604ca-162">不正確的區段長度</span><span class="sxs-lookup"><span data-stu-id="604ca-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="604ca-163">Hello 資源名稱不是處於 hello 正確的格式時，就會發生另一個無效的樣板錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="604ca-164">根層級的資源必須有一個較少的區段中 hello 名稱，而非在 hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="604ca-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="604ca-165">每個區段是以斜線區分。</span><span class="sxs-lookup"><span data-stu-id="604ca-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="604ca-166">在下列範例的 hello，hello 類型有兩個區段和 hello 名稱會有一個區段，所以**有效名稱**。</span><span class="sxs-lookup"><span data-stu-id="604ca-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="604ca-167">Hello 下一個範例，但是**不是有效的名稱**因為它有 hello 的區段數與 hello 型別一樣。</span><span class="sxs-lookup"><span data-stu-id="604ca-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="604ca-168">如需子資源，hello 類型和名稱有 hello 相同的區段數目。</span><span class="sxs-lookup"><span data-stu-id="604ca-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="604ca-169">因為 hello 完整名稱和 hello 子類型包括 hello 父系名稱和型別，這個區段數目才有意義。</span><span class="sxs-lookup"><span data-stu-id="604ca-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="604ca-170">因此，hello 完整名稱仍會有一個較少區段比 hello 完整型別。</span><span class="sxs-lookup"><span data-stu-id="604ca-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="604ca-171">取得正確的 hello 區段可能很困難會套用於資源提供者的資源管理員類型。</span><span class="sxs-lookup"><span data-stu-id="604ca-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="604ca-172">例如，套用資源鎖定 tooa 網站需要四個區段的類型。</span><span class="sxs-lookup"><span data-stu-id="604ca-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="604ca-173">因此，hello 名稱是三個區段：</span><span class="sxs-lookup"><span data-stu-id="604ca-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="604ca-174">不應該複製索引</span><span class="sxs-lookup"><span data-stu-id="604ca-174">Copy index is not expected</span></span>

   <span data-ttu-id="604ca-175">發生此錯誤的**InvalidTemplate**錯誤，當您套用 hello**複製**元素 tooa 範本之一部分的 hello 不支援這個項目。</span><span class="sxs-lookup"><span data-stu-id="604ca-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="604ca-176">您只可以套用 hello 複製項目 tooa 資源類型。</span><span class="sxs-lookup"><span data-stu-id="604ca-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="604ca-177">您無法套用複製 tooa 屬性內的資源類型。</span><span class="sxs-lookup"><span data-stu-id="604ca-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="604ca-178">例如，套用複製 tooa 虛擬機器，但您無法將它套用 toohello OS 磁碟的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="604ca-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="604ca-179">在某些情況下，您可以將轉換子資源 tooa 父資源 toocreate 在複製迴圈。</span><span class="sxs-lookup"><span data-stu-id="604ca-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="604ca-180">如需有關使用複製的詳細資訊，請參閱 [在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="604ca-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="604ca-181">參數無效</span><span class="sxs-lookup"><span data-stu-id="604ca-181">Parameter is not valid</span></span>

   <span data-ttu-id="604ca-182">如果 hello 範本指定的允許的值的參數，而且您提供的值不是其中一個值，您會收到下列錯誤訊息類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="604ca-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="604ca-183">檢查 hello hello 範本中允許的值，並提供在部署期間。</span><span class="sxs-lookup"><span data-stu-id="604ca-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="604ca-184">偵測到循環相依性</span><span class="sxs-lookup"><span data-stu-id="604ca-184">Circular dependency detected</span></span>

   <span data-ttu-id="604ca-185">當資源的相依性不會啟動 hello 部署中，您會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="604ca-186">只要有相互相依性的組合，就會讓兩個或多個資源等候其他也正在等候的資源。</span><span class="sxs-lookup"><span data-stu-id="604ca-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="604ca-187">例如，resource1 相依於 resource3、resource2 相依於 resource1，而 resource3 相依於 resource2。</span><span class="sxs-lookup"><span data-stu-id="604ca-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="604ca-188">您通常可以移除不必要的相依性來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="604ca-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="604ca-189">NotFound 和 ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="604ca-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="604ca-190">當您的範本包含無法解析資源 hello 名稱時，您會收到類似的錯誤：</span><span class="sxs-lookup"><span data-stu-id="604ca-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="604ca-191">如果您嘗試 toodeploy hello 遺漏 hello 範本中的資源，請檢查您是否需要 tooadd 相依性。</span><span class="sxs-lookup"><span data-stu-id="604ca-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="604ca-192">如果可能，Resource Manager 會以平行方式建立資源，將部署最佳化。</span><span class="sxs-lookup"><span data-stu-id="604ca-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="604ca-193">如果另一個資源之後，必須先部署一個資源，您需要 toouse hello **dependsOn**項目中的相依性，在您範本 toocreate hello 其他資源。</span><span class="sxs-lookup"><span data-stu-id="604ca-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="604ca-194">例如，在部署 web 應用程式時，必須存在 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="604ca-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="604ca-195">如果您未指定該 hello web 應用程式相依於 hello App Service 方案，資源管理員會在 hello 建立兩個資源相同的時間。</span><span class="sxs-lookup"><span data-stu-id="604ca-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="604ca-196">您收到錯誤訊息指出找不到應用程式服務計劃的資源，該 hello，因為它尚未存在時嘗試 tooset hello web 應用程式上的屬性。</span><span class="sxs-lookup"><span data-stu-id="604ca-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="604ca-197">您可以在 hello web 應用程式中設定 hello 相依性，以避免這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-197">You prevent this error by setting hello dependency in hello web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="604ca-198">如需針對相依性錯誤進行疑難排解的建議，請參閱[檢查部署順序](#check-deployment-sequence)。</span><span class="sxs-lookup"><span data-stu-id="604ca-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="604ca-199">Hello 資源位於不同的資源群組的其中一個要部署的 hello 存在時，也會看到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="604ca-200">在此情況下，使用 hello [resourceId 函數](resource-group-template-functions-resource.md#resourceid)tooget hello 完整的 hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="604ca-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="604ca-201">如果您嘗試 toouse hello[參考](resource-group-template-functions-resource.md#reference)或[Listkey](resource-group-template-functions-resource.md#listkeys)函式具有無法解析，您會收到下列錯誤 hello 資源：</span><span class="sxs-lookup"><span data-stu-id="604ca-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="604ca-202">查詢運算式包含 hello**參考**函式。</span><span class="sxs-lookup"><span data-stu-id="604ca-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="604ca-203">再次確認 hello 參數值正確。</span><span class="sxs-lookup"><span data-stu-id="604ca-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="604ca-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="604ca-204">ParentResourceNotFound</span></span>

<span data-ttu-id="604ca-205">父 tooanother 資源一個資源時，必須存在 hello 父資源，才能建立 hello 子資源。</span><span class="sxs-lookup"><span data-stu-id="604ca-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="604ca-206">如果尚未存在，您會收到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="604ca-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="604ca-207">hello hello 子資源名稱包含 hello 父系名稱。</span><span class="sxs-lookup"><span data-stu-id="604ca-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="604ca-208">例如，SQL Database 可能定義如下︰</span><span class="sxs-lookup"><span data-stu-id="604ca-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="604ca-209">但是，如果您未在 hello 父資源上指定相依性，可能會取得 hello 子資源，部署 hello 父系之前。</span><span class="sxs-lookup"><span data-stu-id="604ca-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="604ca-210">tooresolve 這個錯誤，包含相依性。</span><span class="sxs-lookup"><span data-stu-id="604ca-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="604ca-211">StorageAccountAlreadyExists 和 StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="604ca-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="604ca-212">儲存體帳戶，您必須提供 Azure 中是唯一的 hello 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="604ca-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="604ca-213">如果您未提供唯一的名稱，您會收到類似下列的錯誤：</span><span class="sxs-lookup"><span data-stu-id="604ca-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="604ca-214">您可以建立一個唯一的名稱，藉由串連 hello hello 結果與您命名慣例[uniqueString](resource-group-template-functions-string.md#uniquestring)函式。</span><span class="sxs-lookup"><span data-stu-id="604ca-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="604ca-215">如果您部署的 hello 的儲存體帳戶相同名稱與現有的儲存體帳戶訂用帳戶，但是提供不同的位置，您收到的錯誤指出 hello 儲存體帳戶已經存在於不同的位置。</span><span class="sxs-lookup"><span data-stu-id="604ca-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="604ca-216">請刪除現有儲存體帳戶 hello，或提供 hello 相同的位置，如 hello 現有儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="604ca-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="604ca-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="604ca-217">AccountNameInvalid</span></span>
<span data-ttu-id="604ca-218">您會看到 hello **AccountNameInvalid**錯誤時嘗試的 toogive 儲存體帳戶名稱包含禁止的字元。</span><span class="sxs-lookup"><span data-stu-id="604ca-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="604ca-219">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能使用數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="604ca-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="604ca-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring)函式會傳回 13 個字元。</span><span class="sxs-lookup"><span data-stu-id="604ca-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="604ca-221">如果您在串連前置詞 toohello **uniqueString**產生，提供 11 個字元前置詞或更少。</span><span class="sxs-lookup"><span data-stu-id="604ca-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="604ca-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="604ca-222">BadRequest</span></span>

<span data-ttu-id="604ca-223">提供的屬性值無效時，您可能會碰到 BadRequest 狀態。</span><span class="sxs-lookup"><span data-stu-id="604ca-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="604ca-224">例如，如果您提供儲存體帳戶 SKU 值不正確，hello 部署將會失敗。</span><span class="sxs-lookup"><span data-stu-id="604ca-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="604ca-225">toodetermine 有效的值屬性，查看 hello [REST API](/rest/api)您要部署的 hello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="604ca-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="604ca-226">NoRegisteredProviderFound 和 MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="604ca-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="604ca-227">在部署資源時，您可能會收到下列錯誤程式碼的 hello 和訊息：</span><span class="sxs-lookup"><span data-stu-id="604ca-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="604ca-228">或者，您可能會收到類似訊息，指出︰</span><span class="sxs-lookup"><span data-stu-id="604ca-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="604ca-229">您會因為下列三個原因其中一個而收到此錯誤︰</span><span class="sxs-lookup"><span data-stu-id="604ca-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="604ca-230">hello 資源提供者尚未註冊訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="604ca-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="604ca-231">Hello 資源類型不支援的 API 版本</span><span class="sxs-lookup"><span data-stu-id="604ca-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="604ca-232">Hello 資源類型不支援的位置</span><span class="sxs-lookup"><span data-stu-id="604ca-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="604ca-233">hello 錯誤訊息應該提供支援的 hello 位置和 API 版本的建議。</span><span class="sxs-lookup"><span data-stu-id="604ca-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="604ca-234">您可以變更您的範本 tooone hello 的建議值。</span><span class="sxs-lookup"><span data-stu-id="604ca-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="604ca-235">大部分的提供者會自動註冊 hello 您使用的 Azure 入口網站或 hello 命令列介面，但不是全部。</span><span class="sxs-lookup"><span data-stu-id="604ca-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="604ca-236">如果您沒有使用特定的資源提供者之前，您可能需要 tooregister 該提供者。</span><span class="sxs-lookup"><span data-stu-id="604ca-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="604ca-237">您可以透過 PowerShell 或 Azure CLI，深入探索資源提供者。</span><span class="sxs-lookup"><span data-stu-id="604ca-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="604ca-238">**入口網站**</span><span class="sxs-lookup"><span data-stu-id="604ca-238">**Portal**</span></span>

<span data-ttu-id="604ca-239">您可以看到 hello 登錄狀態並登錄資源提供者命名空間，透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="604ca-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="604ca-240">對於您的訂用帳戶，選取**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="604ca-240">For your subscription, select **Resource providers**.</span></span>

   ![選取資源提供者](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="604ca-242">查看 hello 資源提供者清單，並視需要選取 hello**註冊**連結 tooregister hello 資源提供者的 hello 類型嘗試 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="604ca-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![列出資源提供者](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="604ca-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="604ca-244">**PowerShell**</span></span>

<span data-ttu-id="604ca-245">toosee 您的註冊狀態，使用**Get AzureRmResourceProvider**。</span><span class="sxs-lookup"><span data-stu-id="604ca-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="604ca-246">tooregister 為提供者，使用**暫存器 AzureRmResourceProvider**並提供 hello 名稱想 tooregister hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="604ca-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="604ca-247">tooget hello 支援位置的特定類型的資源，請使用：</span><span class="sxs-lookup"><span data-stu-id="604ca-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="604ca-248">tooget hello 支援特定類型的資源，使用 API 版本：</span><span class="sxs-lookup"><span data-stu-id="604ca-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="604ca-249">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="604ca-249">**Azure CLI**</span></span>

<span data-ttu-id="604ca-250">toosee hello 提供者註冊時，是否使用 hello`azure provider list`命令。</span><span class="sxs-lookup"><span data-stu-id="604ca-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="604ca-251">tooregister 資源提供者，使用 hello`azure provider register`命令，並指定 hello*命名空間*tooregister。</span><span class="sxs-lookup"><span data-stu-id="604ca-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="604ca-252">toosee hello 支援位置和資源類型的 API 版本使用：</span><span class="sxs-lookup"><span data-stu-id="604ca-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="604ca-253">QuotaExceeded 和 OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="604ca-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="604ca-254">當部署超過配額時 (也許是每個資源群組、訂用帳戶、帳戶及其他範圍的配額)，可能會發生問題。</span><span class="sxs-lookup"><span data-stu-id="604ca-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="604ca-255">例如，您的訂用帳戶可能會設定區域的核心 toolimit hello 數目。</span><span class="sxs-lookup"><span data-stu-id="604ca-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="604ca-256">如果您嘗試 toodeploy 具有更多的核心數目超過允許數量的 hello 的虛擬機器，您會收到的錯誤指出 hello 配額超過。</span><span class="sxs-lookup"><span data-stu-id="604ca-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="604ca-257">如需完整的配額資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="604ca-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="604ca-258">tooexamine 您訂用帳戶配額的核心，您可以使用 hello `azure vm list-usage` hello Azure CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="604ca-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="604ca-259">hello 下列範例將說明該 hello 核心配額，免費試用帳戶是 4:</span><span class="sxs-lookup"><span data-stu-id="604ca-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="604ca-260">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="604ca-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="604ca-261">如果您部署的 hello 美國西部地區中建立四個以上的核心的範本，您會取得部署錯誤，看起來像：</span><span class="sxs-lookup"><span data-stu-id="604ca-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="604ca-262">在 PowerShell 中，您可以使用 hello 或者**Get AzureRmVMUsage** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="604ca-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="604ca-263">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="604ca-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="604ca-264">在這些情況下，您應該移 toohello 入口網站，而且檔案支援問題 tooraise hello 區域要 toodeploy 配額。</span><span class="sxs-lookup"><span data-stu-id="604ca-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="604ca-265">請記住，資源群組的 hello 配額是各地區，不適用於 hello 整個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="604ca-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="604ca-266">如果您需要在美國西部的 toodeploy 30 個核心，您必須在美國西部 30 資源管理員核心 tooask。</span><span class="sxs-lookup"><span data-stu-id="604ca-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="604ca-267">如果您需要在任何 hello 區域 toowhich toodeploy 30 核心可以存取，您應該會尋求 30 的所有區域中的資源管理員核心。</span><span class="sxs-lookup"><span data-stu-id="604ca-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="604ca-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="604ca-268">InvalidContentLink</span></span>
<span data-ttu-id="604ca-269">當您收到 hello 錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="604ca-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="604ca-270">您最有可能嘗試 toolink tooa 巢狀的樣板，無法使用。</span><span class="sxs-lookup"><span data-stu-id="604ca-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="604ca-271">檢查 hello hello 巢狀範本提供的 URI。</span><span class="sxs-lookup"><span data-stu-id="604ca-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="604ca-272">如果儲存體帳戶中已有 hello 範本，請確定 hello URI 可供存取。</span><span class="sxs-lookup"><span data-stu-id="604ca-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="604ca-273">您可能需要 toopass SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="604ca-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="604ca-274">如需詳細資訊，請參閱 [透過 Azure 資源管理員使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="604ca-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="604ca-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="604ca-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="604ca-276">當您的訂閱包含讓您在部署期間嘗試 tooperform 動作的資源原則，您會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="604ca-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="604ca-277">在 hello 錯誤訊息，尋找 hello 原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="604ca-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="604ca-278">在**PowerShell**，提供該原則識別碼，則為 hello**識別碼**封鎖部署的 hello 原則的相關參數 tooretrieve 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="604ca-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="604ca-279">在**Azure CLI**，提供 hello hello 原則定義名稱：</span><span class="sxs-lookup"><span data-stu-id="604ca-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="604ca-280">如需詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="604ca-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="604ca-281">RequestDisallowedByPolicy 錯誤</span><span class="sxs-lookup"><span data-stu-id="604ca-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="604ca-282">[使用原則 toomanage 資源，並控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="604ca-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="604ca-283">授權失敗</span><span class="sxs-lookup"><span data-stu-id="604ca-283">Authorization failed</span></span>
<span data-ttu-id="604ca-284">您可能會在部署期間收到錯誤，因為 hello 帳戶或服務主體嘗試 toodeploy hello 資源沒有存取 tooperform 那些動作。</span><span class="sxs-lookup"><span data-stu-id="604ca-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="604ca-285">Azure Active Directory 可讓您或您的系統管理員 toocontrol 哪些身分識別可以存取哪些資源以很大的有效位數。</span><span class="sxs-lookup"><span data-stu-id="604ca-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="604ca-286">例如，如果您的帳戶指派 toohello 讀取者角色，您不能 toocreate 資源。</span><span class="sxs-lookup"><span data-stu-id="604ca-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="604ca-287">在此情況下，您會看到錯誤訊息，指出授權失敗。</span><span class="sxs-lookup"><span data-stu-id="604ca-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="604ca-288">如需角色型存取控制的詳細資訊，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="604ca-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="604ca-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="604ca-289">Next steps</span></span>
* <span data-ttu-id="604ca-290">toolearn 有關稽核的動作，請參閱[稽核與資源管理員作業](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="604ca-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="604ca-291">toolearn 有關動作 toodetermine hello 錯誤，在部署期間，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="604ca-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
