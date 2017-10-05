---
title: "針對常見的 Azure 部署錯誤進行疑難排解 | Microsoft Docs"
description: "說明如何解決使用 Azure Resource Manager 將資源部署至 Azure 時的常見錯誤。"
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "部署錯誤, azure 部署, 部署至 azure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="9c753-104">使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="9c753-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="9c753-105">本主題說明如何解決可能會遇到的一些常見 Azure 部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="9c753-106">本主題會說明下列錯誤碼︰</span><span class="sxs-lookup"><span data-stu-id="9c753-106">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="9c753-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="9c753-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="9c753-108">授權失敗</span><span class="sxs-lookup"><span data-stu-id="9c753-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="9c753-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="9c753-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="9c753-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="9c753-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="9c753-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="9c753-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="9c753-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="9c753-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="9c753-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="9c753-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="9c753-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="9c753-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="9c753-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="9c753-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="9c753-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="9c753-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="9c753-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="9c753-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="9c753-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="9c753-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="9c753-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="9c753-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="9c753-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="9c753-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="9c753-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="9c753-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="9c753-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="9c753-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="9c753-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="9c753-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="9c753-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="9c753-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="9c753-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="9c753-125">DeploymentFailed</span></span>

<span data-ttu-id="9c753-126">這個錯誤碼會指出一般部署錯誤，但不是您要開始進行疑難排解的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="9c753-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="9c753-127">實際上協助您解決問題的錯誤碼通常位於此錯誤的下一層。</span><span class="sxs-lookup"><span data-stu-id="9c753-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="9c753-128">例如，下圖顯示在部署錯誤底下的 **RequestDisallowedByPolicy** 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="9c753-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![顯示錯誤碼](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="9c753-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="9c753-130">SkuNotAvailable</span></span>

<span data-ttu-id="9c753-131">在部署資源 (通常是虛擬機器) 時，您可能會收到下列錯誤碼和錯誤訊息︰</span><span class="sxs-lookup"><span data-stu-id="9c753-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="9c753-132">當您選取的資源 SKU (例如 VM 大小) 不適用於您選取的位置時，您會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="9c753-133">若要解決此問題，您需要判斷區域中有哪些 SKU。</span><span class="sxs-lookup"><span data-stu-id="9c753-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="9c753-134">您可以使用 PowerShell、入口網站或 REST 作業來尋找可用的 SKU。</span><span class="sxs-lookup"><span data-stu-id="9c753-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="9c753-135">若是 PowerShell，請使用 [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) 並依位置篩選。</span><span class="sxs-lookup"><span data-stu-id="9c753-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="9c753-136">您必須擁有最新版 PowerShell 才能執行此命令。</span><span class="sxs-lookup"><span data-stu-id="9c753-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="9c753-137">結果包括該位置的 SKU 清單，以及該 SKU 的任何限制。</span><span class="sxs-lookup"><span data-stu-id="9c753-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="9c753-138">若要使用[入口網站](https://portal.azure.com)，請登入入口網站並透過介面加入資源。</span><span class="sxs-lookup"><span data-stu-id="9c753-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="9c753-139">當您設定值時，您會看到該資源可用的 SKU。</span><span class="sxs-lookup"><span data-stu-id="9c753-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="9c753-140">您不需要完成部署。</span><span class="sxs-lookup"><span data-stu-id="9c753-140">You do not need to complete the deployment.</span></span>

    ![可用的 SKU](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="9c753-142">若要為虛擬機器使用 REST API，請傳送下列要求︰</span><span class="sxs-lookup"><span data-stu-id="9c753-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="9c753-143">它會以下列格式傳回可用的 SKU 和區域︰</span><span class="sxs-lookup"><span data-stu-id="9c753-143">It returns available SKUs and regions in the following format:</span></span>

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

<span data-ttu-id="9c753-144">如果您在該區域或符合您業務需求的替代區域中找不到適當的 SKU，請向 Azure 支援服務提交 [SKU 要求](https://aka.ms/skurestriction)。</span><span class="sxs-lookup"><span data-stu-id="9c753-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="9c753-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="9c753-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="9c753-146">如果您收到此錯誤，表示您使用的訂用帳戶不被允許存取 Azure Active Directory 以外的任何 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="9c753-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="9c753-147">當您需要存取傳統入口網站，但不被允許部署資源時，就表示您擁有的訂用帳戶可能是這種類型。</span><span class="sxs-lookup"><span data-stu-id="9c753-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="9c753-148">若要解決此問題，您必須使用有權部署資源的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c753-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="9c753-149">若要使用 PowerShell 檢視您可用的訂用帳戶，請使用︰</span><span class="sxs-lookup"><span data-stu-id="9c753-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="9c753-150">若要設定目前的訂用帳戶，請使用︰</span><span class="sxs-lookup"><span data-stu-id="9c753-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="9c753-151">若要使用 Azure CLI 2.0 檢視您可用的訂用帳戶，請使用︰</span><span class="sxs-lookup"><span data-stu-id="9c753-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="9c753-152">若要設定目前的訂用帳戶，請使用︰</span><span class="sxs-lookup"><span data-stu-id="9c753-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="9c753-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="9c753-153">InvalidTemplate</span></span>
<span data-ttu-id="9c753-154">此錯誤可能起因於數個不同類型的錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="9c753-155">語法錯誤</span><span class="sxs-lookup"><span data-stu-id="9c753-155">Syntax error</span></span>

   <span data-ttu-id="9c753-156">如果您收到錯誤訊息指出無法驗證範本，則可能是範本中發生語法問題。</span><span class="sxs-lookup"><span data-stu-id="9c753-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="9c753-157">此錯誤很容易發生，因為範本運算式可能很複雜。</span><span class="sxs-lookup"><span data-stu-id="9c753-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="9c753-158">例如，儲存體帳戶的下列名稱指派包含一組方括號、三個函式、三組圓括號、一組單引號和一個屬性︰</span><span class="sxs-lookup"><span data-stu-id="9c753-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="9c753-159">如果您未提供相符的語法，範本會產生與您所要的值截然不同的值。</span><span class="sxs-lookup"><span data-stu-id="9c753-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="9c753-160">當您收到此類錯誤時，請仔細檢閱運算式語法。</span><span class="sxs-lookup"><span data-stu-id="9c753-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="9c753-161">請考慮使用 [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) 或 [Visual Studio Code](resource-manager-vs-code.md) 等 JSON 編輯器，它們可以警告您有語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="9c753-162">不正確的區段長度</span><span class="sxs-lookup"><span data-stu-id="9c753-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="9c753-163">資源名稱的格式不正確時，就會發生另一種無效範本錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="9c753-164">根層級資源的名稱必須比資源類型少一個區段。</span><span class="sxs-lookup"><span data-stu-id="9c753-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="9c753-165">每個區段是以斜線區分。</span><span class="sxs-lookup"><span data-stu-id="9c753-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="9c753-166">在下列範例中，類型具有 2 個區段，而名稱則有 1 個區段，因此是**有效名稱**。</span><span class="sxs-lookup"><span data-stu-id="9c753-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="9c753-167">但下一個範例則 **不是有效名稱** ，因為它的區段數目和類型相同。</span><span class="sxs-lookup"><span data-stu-id="9c753-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="9c753-168">對於子資源來說，類型和名稱具有相同的區段數目。</span><span class="sxs-lookup"><span data-stu-id="9c753-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="9c753-169">此區段數目很合理，因為子資源的完整名稱和類型包含父資源的名稱和類型。</span><span class="sxs-lookup"><span data-stu-id="9c753-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="9c753-170">因此，完整名稱較完整類型仍少一個區段。</span><span class="sxs-lookup"><span data-stu-id="9c753-170">Therefore, the full name still has one less segment than the full type.</span></span>

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

   <span data-ttu-id="9c753-171">對於跨資源提供者套用的 Resource Manager 類型而言，要讓區段保持正確可能很棘手。</span><span class="sxs-lookup"><span data-stu-id="9c753-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="9c753-172">例如，將資源鎖定套用至網站需要具有四個區段的類型。</span><span class="sxs-lookup"><span data-stu-id="9c753-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="9c753-173">因此，名稱會是三個區段：</span><span class="sxs-lookup"><span data-stu-id="9c753-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="9c753-174">不應該複製索引</span><span class="sxs-lookup"><span data-stu-id="9c753-174">Copy index is not expected</span></span>

   <span data-ttu-id="9c753-175">當您將 **copy** 元素套用到不支援此元素的範本時，您會遇到此 **InvalidTemplate** 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="9c753-176">您只可以將複製元素套用到資源類型。</span><span class="sxs-lookup"><span data-stu-id="9c753-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="9c753-177">您不能將複製套用到資源類型內的屬性。</span><span class="sxs-lookup"><span data-stu-id="9c753-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="9c753-178">例如，您將複製套用到虛擬機器，但無法將它套用到虛擬機器的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="9c753-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="9c753-179">在某些情況下，您可以將子資源轉換成父資源，以建立複製迴圈。</span><span class="sxs-lookup"><span data-stu-id="9c753-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="9c753-180">如需有關使用複製的詳細資訊，請參閱 [在 Azure Resource Manager 中建立資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="9c753-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="9c753-181">參數無效</span><span class="sxs-lookup"><span data-stu-id="9c753-181">Parameter is not valid</span></span>

   <span data-ttu-id="9c753-182">如果範本會指定參數允許的值，而您提供的值不是其中一個值，則會收到類似下列錯誤的訊息：</span><span class="sxs-lookup"><span data-stu-id="9c753-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="9c753-183">在範本中重複檢查允許的值，並在部署期間提供一個值。</span><span class="sxs-lookup"><span data-stu-id="9c753-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="9c753-184">偵測到循環相依性</span><span class="sxs-lookup"><span data-stu-id="9c753-184">Circular dependency detected</span></span>

   <span data-ttu-id="9c753-185">當資源以防止部署啟動的方式互相相依，您會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="9c753-186">只要有相互相依性的組合，就會讓兩個或多個資源等候其他也正在等候的資源。</span><span class="sxs-lookup"><span data-stu-id="9c753-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="9c753-187">例如，resource1 相依於 resource3、resource2 相依於 resource1，而 resource3 相依於 resource2。</span><span class="sxs-lookup"><span data-stu-id="9c753-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="9c753-188">您通常可以移除不必要的相依性來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="9c753-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="9c753-189">NotFound 和 ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="9c753-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="9c753-190">當您的範本包含的資源名稱無法解析時，您會收到類似以下的錯誤：</span><span class="sxs-lookup"><span data-stu-id="9c753-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="9c753-191">如果您嘗試在範本中部署遺漏的資源，請檢查是否需要新增相依性。</span><span class="sxs-lookup"><span data-stu-id="9c753-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="9c753-192">如果可能，Resource Manager 會以平行方式建立資源，將部署最佳化。</span><span class="sxs-lookup"><span data-stu-id="9c753-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="9c753-193">如果一個資源必須在另一個資源之後部署，您就必須在範本中使用 **dependsOn** 元素來建立與該另一個資源的相依性。</span><span class="sxs-lookup"><span data-stu-id="9c753-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="9c753-194">例如，在部署 Web 應用程式時，App Service 方案必須存在。</span><span class="sxs-lookup"><span data-stu-id="9c753-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="9c753-195">如果您沒有指定該 Web 應用程式相依於 App Service 方案，Resource Manager 會同時建立這兩個資源。</span><span class="sxs-lookup"><span data-stu-id="9c753-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="9c753-196">您收到錯誤訊息，指出找不到 App Service 方案的資源，因為嘗試在 Web 應用程式上設定屬性時它尚未存在。</span><span class="sxs-lookup"><span data-stu-id="9c753-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="9c753-197">您會設定 Web 應用程式的相依性，以避免此錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-197">You prevent this error by setting the dependency in the web app.</span></span>

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

<span data-ttu-id="9c753-198">如需針對相依性錯誤進行疑難排解的建議，請參閱[檢查部署順序](#check-deployment-sequence)。</span><span class="sxs-lookup"><span data-stu-id="9c753-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="9c753-199">當資源存在於所要部署不同的資源群組中，則也會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="9c753-200">在該情況下，請使用 [resourceId 函式](resource-group-template-functions-resource.md#resourceid)來取得資源的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="9c753-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="9c753-201">如果您嘗試對無法解析的資源使用 [reference](resource-group-template-functions-resource.md#reference) 或 [listKeys](resource-group-template-functions-resource.md#listkeys) 函式，您會收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="9c753-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="9c753-202">尋找包含 **reference** 函式的運算式。</span><span class="sxs-lookup"><span data-stu-id="9c753-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="9c753-203">重複檢查確定參數值正確。</span><span class="sxs-lookup"><span data-stu-id="9c753-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="9c753-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="9c753-204">ParentResourceNotFound</span></span>

<span data-ttu-id="9c753-205">當某資源為另一個資源的父資源時，父資源必須在建立子資源之前就存在。</span><span class="sxs-lookup"><span data-stu-id="9c753-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="9c753-206">如果尚未存在，您會收到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="9c753-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="9c753-207">子資源的名稱包含父系名稱。</span><span class="sxs-lookup"><span data-stu-id="9c753-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="9c753-208">例如，SQL Database 可能定義如下︰</span><span class="sxs-lookup"><span data-stu-id="9c753-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="9c753-209">但是，如果您尚未於父資源上指定相依性，子資源可能會在父資源之前進行部署。</span><span class="sxs-lookup"><span data-stu-id="9c753-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="9c753-210">若要解決這個錯誤，請包含相依性。</span><span class="sxs-lookup"><span data-stu-id="9c753-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="9c753-211">StorageAccountAlreadyExists 和 StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="9c753-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="9c753-212">對於儲存體帳戶，您必須提供在 Azure 中是唯一的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="9c753-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="9c753-213">如果您未提供唯一的名稱，您會收到類似下列的錯誤：</span><span class="sxs-lookup"><span data-stu-id="9c753-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="9c753-214">您可以將您的命名慣例與 [uniqueString](resource-group-template-functions-string.md#uniquestring) 函式的結果串連，以建立一個唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="9c753-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="9c753-215">如果您以與您的訂用帳戶中現有的儲存體帳戶相同的名稱部署儲存體帳戶，但提供不同的位置，您會遇到錯誤，指出儲存體帳戶已存在於不同的位置。</span><span class="sxs-lookup"><span data-stu-id="9c753-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="9c753-216">刪除現有的儲存體帳戶，或提供與現有儲存體帳戶相同的位置。</span><span class="sxs-lookup"><span data-stu-id="9c753-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="9c753-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="9c753-217">AccountNameInvalid</span></span>
<span data-ttu-id="9c753-218">嘗試提供的儲存體帳戶名稱中包含禁止的字元時，您會看到 **AccountNameInvalid** 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="9c753-219">儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能使用數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="9c753-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="9c753-220">[uniqueString](resource-group-template-functions-string.md#uniquestring) 函式會傳回 13 個字元。</span><span class="sxs-lookup"><span data-stu-id="9c753-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="9c753-221">如果您要對 **uniqueString** 結果串連前置詞，請提供 11 個字元以下的前置詞。</span><span class="sxs-lookup"><span data-stu-id="9c753-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="9c753-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="9c753-222">BadRequest</span></span>

<span data-ttu-id="9c753-223">提供的屬性值無效時，您可能會碰到 BadRequest 狀態。</span><span class="sxs-lookup"><span data-stu-id="9c753-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="9c753-224">例如，如果您針對儲存體帳戶提供不正確的 SKU 值，則部署會失敗。</span><span class="sxs-lookup"><span data-stu-id="9c753-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="9c753-225">若要判斷屬性的有效值，請查看 [REST API](/rest/api) 了解您要部署的資源類型。</span><span class="sxs-lookup"><span data-stu-id="9c753-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="9c753-226">NoRegisteredProviderFound 和 MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="9c753-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="9c753-227">在部署資源時，您可能會收到下列錯誤代碼和訊息︰</span><span class="sxs-lookup"><span data-stu-id="9c753-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="9c753-228">或者，您可能會收到類似訊息，指出︰</span><span class="sxs-lookup"><span data-stu-id="9c753-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="9c753-229">您會因為下列三個原因其中一個而收到此錯誤︰</span><span class="sxs-lookup"><span data-stu-id="9c753-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="9c753-230">尚未向您的訂用帳戶註冊此資源提供者</span><span class="sxs-lookup"><span data-stu-id="9c753-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="9c753-231">此資源類型不支援 API 版本</span><span class="sxs-lookup"><span data-stu-id="9c753-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="9c753-232">此資源類型不支援位置</span><span class="sxs-lookup"><span data-stu-id="9c753-232">Location not supported for the resource type</span></span>

<span data-ttu-id="9c753-233">錯誤訊息應可提供給您支援的位置和 API 版本建議。</span><span class="sxs-lookup"><span data-stu-id="9c753-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="9c753-234">您可以將您的範本變更為其中一個建議的值。</span><span class="sxs-lookup"><span data-stu-id="9c753-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="9c753-235">Azure 入口網站或正在使用的命令列介面會自動註冊大部分的提供者；但並非全部。</span><span class="sxs-lookup"><span data-stu-id="9c753-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="9c753-236">如果您未曾使用特定的資源提供者，您可能需要註冊該提供者。</span><span class="sxs-lookup"><span data-stu-id="9c753-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="9c753-237">您可以透過 PowerShell 或 Azure CLI，深入探索資源提供者。</span><span class="sxs-lookup"><span data-stu-id="9c753-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="9c753-238">**入口網站**</span><span class="sxs-lookup"><span data-stu-id="9c753-238">**Portal**</span></span>

<span data-ttu-id="9c753-239">您可以看到註冊狀態，並透過入口網站註冊資源提供者命名空間。</span><span class="sxs-lookup"><span data-stu-id="9c753-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="9c753-240">對於您的訂用帳戶，選取**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="9c753-240">For your subscription, select **Resource providers**.</span></span>

   ![選取資源提供者](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="9c753-242">查看資源提供者的清單，並視需要選取 [註冊] 連結以註冊您嘗試部署的資源提供者類型。</span><span class="sxs-lookup"><span data-stu-id="9c753-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![列出資源提供者](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="9c753-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9c753-244">**PowerShell**</span></span>

<span data-ttu-id="9c753-245">若要查看您的註冊狀態，請使用 **Get-AzureRmResourceProvider**。</span><span class="sxs-lookup"><span data-stu-id="9c753-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="9c753-246">若要註冊提供者，請使用 **Register-AzureRmResourceProvider** ，並提供您想要註冊的資源提供者名稱。</span><span class="sxs-lookup"><span data-stu-id="9c753-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="9c753-247">若要取得支援特定資源類型的位置，請使用︰</span><span class="sxs-lookup"><span data-stu-id="9c753-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="9c753-248">若要取得支援特定資源類型的 API 版本，請使用︰</span><span class="sxs-lookup"><span data-stu-id="9c753-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="9c753-249">**Azure CLI**</span><span class="sxs-lookup"><span data-stu-id="9c753-249">**Azure CLI**</span></span>

<span data-ttu-id="9c753-250">若要查看是否已註冊該提供者，請使用 `azure provider list` 命令。</span><span class="sxs-lookup"><span data-stu-id="9c753-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="9c753-251">若要註冊資源提供者，請使用 `azure provider register` 命令，然後指定要註冊的*命名空間*。</span><span class="sxs-lookup"><span data-stu-id="9c753-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="9c753-252">若要查看資源類型所支援的位置和 API 版本，請使用︰</span><span class="sxs-lookup"><span data-stu-id="9c753-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="9c753-253">QuotaExceeded 和 OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="9c753-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="9c753-254">當部署超過配額時 (也許是每個資源群組、訂用帳戶、帳戶及其他範圍的配額)，可能會發生問題。</span><span class="sxs-lookup"><span data-stu-id="9c753-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="9c753-255">例如，您的訂用帳戶可能設定為要限制區域的核心數目。</span><span class="sxs-lookup"><span data-stu-id="9c753-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="9c753-256">如果您嘗試部署超過允許核心數目的虛擬機器，您會收到錯誤訊息指出已超過配額。</span><span class="sxs-lookup"><span data-stu-id="9c753-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="9c753-257">如需完整的配額資訊，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="9c753-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="9c753-258">若要檢查您訂用帳戶的核心配額，可以在 Azure CLI 中使用 `azure vm list-usage` 命令。</span><span class="sxs-lookup"><span data-stu-id="9c753-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="9c753-259">以下範例示範核心配額為 4 的免費試用帳戶：</span><span class="sxs-lookup"><span data-stu-id="9c753-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="9c753-260">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="9c753-260">Which returns:</span></span>

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

<span data-ttu-id="9c753-261">如果您部署的範本會在美國西部區域中建立四個以上的核心，您會看到類似以下的部署錯誤：</span><span class="sxs-lookup"><span data-stu-id="9c753-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="9c753-262">或者，您可以在 PowerShell 中使用 **Get-AzureRmVMUsage** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9c753-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="9c753-263">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="9c753-263">Which returns:</span></span>

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

<span data-ttu-id="9c753-264">在這些情況下，您應該移至入口網站，並提出支援問題，以針對您想要部署的區域提高配額。</span><span class="sxs-lookup"><span data-stu-id="9c753-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="9c753-265">請記住，對於資源群組，配額適用於每個個別區域，而不是整個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c753-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="9c753-266">如果您需要在美國西部部署 30 個核心，就必須要求在美國西部擁有 30 個資源管理員核心。</span><span class="sxs-lookup"><span data-stu-id="9c753-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="9c753-267">如果您需要在任何具有存取權限的區域中部署 30 個核心，就應該要求在所有區域中擁有 30 個 Resource Manager 核心。</span><span class="sxs-lookup"><span data-stu-id="9c753-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="9c753-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="9c753-268">InvalidContentLink</span></span>
<span data-ttu-id="9c753-269">當您收到錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="9c753-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="9c753-270">您最有可能嘗試連結至無法使用的巢狀範本。</span><span class="sxs-lookup"><span data-stu-id="9c753-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="9c753-271">再次確認您為巢狀範本提供的 URI。</span><span class="sxs-lookup"><span data-stu-id="9c753-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="9c753-272">如果儲存體帳戶中已有範本，請確定 URI 可存取。</span><span class="sxs-lookup"><span data-stu-id="9c753-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="9c753-273">您可能需要傳送 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="9c753-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="9c753-274">如需詳細資訊，請參閱 [透過 Azure 資源管理員使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="9c753-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="9c753-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="9c753-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="9c753-276">當訂用帳戶包含會讓您無法在部署期間嘗試執行某個動作的資源原則時，您就會收到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="9c753-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="9c753-277">請在錯誤訊息中尋找原則識別碼。</span><span class="sxs-lookup"><span data-stu-id="9c753-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="9c753-278">在 **PowerShell** 中，提供該原則識別碼做為 **Id** 參數，以擷取有關封鎖了部署之原則的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9c753-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="9c753-279">在 **Azure CLI** 中，提供原則定義的名稱︰</span><span class="sxs-lookup"><span data-stu-id="9c753-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="9c753-280">如需詳細資訊，請參閱下列文章。</span><span class="sxs-lookup"><span data-stu-id="9c753-280">For more information, see the following articles:</span></span>

- [<span data-ttu-id="9c753-281">RequestDisallowedByPolicy 錯誤</span><span class="sxs-lookup"><span data-stu-id="9c753-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="9c753-282">[使用原則來管理資源和控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="9c753-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="9c753-283">授權失敗</span><span class="sxs-lookup"><span data-stu-id="9c753-283">Authorization failed</span></span>
<span data-ttu-id="9c753-284">您可能會在部署期間收到錯誤，因為嘗試部署資源的帳戶或服務主體並有執行這些動作的存取權。</span><span class="sxs-lookup"><span data-stu-id="9c753-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="9c753-285">Azure Active Directory 可讓您或您的系統管理員最精確地控制哪些身分識別可以存取哪些資源。</span><span class="sxs-lookup"><span data-stu-id="9c753-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="9c753-286">例如，如果您的帳戶被指派「讀取者」角色，您將無法建立資源。</span><span class="sxs-lookup"><span data-stu-id="9c753-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="9c753-287">在此情況下，您會看到錯誤訊息，指出授權失敗。</span><span class="sxs-lookup"><span data-stu-id="9c753-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="9c753-288">如需角色型存取控制的詳細資訊，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="9c753-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9c753-289">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c753-289">Next steps</span></span>
* <span data-ttu-id="9c753-290">若要了解稽核動作，請參閱 [使用 Resource Manager 來稽核作業](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="9c753-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="9c753-291">若要了解部署期間可採取哪些動作來判斷錯誤，請參閱 [檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="9c753-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
