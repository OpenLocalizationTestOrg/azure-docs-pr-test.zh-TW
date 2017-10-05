---
title: "了解 Azure 部署錯誤 | Microsoft Docs"
description: "說明如何了解 Azure 部署錯誤。"
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "部署錯誤, azure 部署, 部署至 azure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: b67bb30fa259fa08e37e11afec724c8b8c3eb633
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="7ecf3-104">了解 Azure 部署錯誤</span><span class="sxs-lookup"><span data-stu-id="7ecf3-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="7ecf3-105">本主題說明部署錯誤，以及如何找出與錯誤相關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="7ecf3-106">如需常見部署錯誤的解決方案，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-106">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="7ecf3-107">兩種錯誤類型</span><span class="sxs-lookup"><span data-stu-id="7ecf3-107">Two types of errors</span></span>
<span data-ttu-id="7ecf3-108">您可能會收到兩種錯誤類型︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="7ecf3-109">驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="7ecf3-109">validation errors</span></span>
* <span data-ttu-id="7ecf3-110">部署錯誤</span><span class="sxs-lookup"><span data-stu-id="7ecf3-110">deployment errors</span></span>

<span data-ttu-id="7ecf3-111">下圖顯示訂用帳戶的活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-111">The following image shows the activity log for a subscription.</span></span> <span data-ttu-id="7ecf3-112">它代表兩個部署。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-112">It represents two deployments.</span></span> <span data-ttu-id="7ecf3-113">在其中一個部署中，範本驗證失敗 (**驗證**) 且無法繼續進行。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-113">In one deployment, the template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="7ecf3-114">在另一個部署中，範本已通過驗證，但在建立資源時失敗 (**寫入部署**)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-114">In the other deployment, the template passed validation but failed when creating the resources (**Write Deployments**).</span></span> 

![顯示錯誤碼](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="7ecf3-116">驗證錯誤來自可在部署之前判斷的情況。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="7ecf3-117">其中包含您範本中的語法錯誤，或者嘗試部署會超出您訂用帳戶配額的資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-117">They include syntax errors in your template, or trying to deploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="7ecf3-118">部署程序期間出現的情況下會發生驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-118">Deployment errors arise from conditions that occur during the deployment process.</span></span> <span data-ttu-id="7ecf3-119">其中包括嘗試存取以平行方式部署的資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-119">They include trying to access a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="7ecf3-120">這兩種錯誤類型都會傳回錯誤碼，以供您針對部署進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-120">Both types of errors return an error code that you use to troubleshoot the deployment.</span></span> <span data-ttu-id="7ecf3-121">這兩種錯誤類型都會出現在[活動記錄](resource-group-audit.md)中。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-121">Both types of errors appear in the [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="7ecf3-122">不過，驗證錯誤不會出現在部署歷程記錄中，因為部署永遠不會啟動。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-122">However, validation errors do not appear in your deployment history because the deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="7ecf3-123">判斷錯誤碼</span><span class="sxs-lookup"><span data-stu-id="7ecf3-123">Determine error code</span></span>

<span data-ttu-id="7ecf3-124">您可以藉由查看錯誤訊息和錯誤碼來了解錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-124">You can learn about an error by looking at the error message and the error code.</span></span> <span data-ttu-id="7ecf3-125">[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)一文會依錯誤碼列出解決方案。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-125">The [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="7ecf3-126">本主題說明如何使用 Azure 入口網站來探索錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-126">This topic shows how to use the Azure portal to discover the error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="7ecf3-127">驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="7ecf3-127">Validation errors</span></span>

<span data-ttu-id="7ecf3-128">透過入口網站進行部署時，您在提交值之後看到驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-128">When deploying through the portal, you see a validation error after submitting your values.</span></span>

![顯示入口網站驗證錯誤](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="7ecf3-130">選取訊息以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-130">Select the message for more details.</span></span> <span data-ttu-id="7ecf3-131">在下圖中，您會看到 **InvalidTemplateDeployment** 錯誤，以及指出某個原則封鎖了部署的訊息。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-131">In the following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![顯示驗證詳細資料](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="7ecf3-133">部署錯誤</span><span class="sxs-lookup"><span data-stu-id="7ecf3-133">Deployment errors</span></span>

<span data-ttu-id="7ecf3-134">當作業通過驗證，但在部署期間失敗時，您會在通知中看見錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-134">When the operation passes validation, but fails during deployment, you see the error in the notifications.</span></span> <span data-ttu-id="7ecf3-135">選取通知。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-135">Select the notification.</span></span>

![通知錯誤](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="7ecf3-137">您會看到更多與部署相關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-137">You see more details about the deployment.</span></span> <span data-ttu-id="7ecf3-138">選取選項來尋找與錯誤相關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-138">Select the option to find more information about the error.</span></span>

![部署失敗](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="7ecf3-140">您會看到錯誤訊息和錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-140">You see the error message and error codes.</span></span> <span data-ttu-id="7ecf3-141">請注意，有兩個錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-141">Notice there are two error codes.</span></span> <span data-ttu-id="7ecf3-142">第一個錯誤碼 (**DeploymentFailed**) 是一般錯誤，不會提供您解決錯誤所需的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-142">The first error code (**DeploymentFailed**) is a general error that does not provide the details you need to solve the error.</span></span> <span data-ttu-id="7ecf3-143">第二個錯誤碼 (**StorageAccountNotFound**) 會提供您需要的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-143">The second error code (**StorageAccountNotFound**) provides the details you need.</span></span> 

![錯誤詳細資料](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="7ecf3-145">啟用偵錯記錄</span><span class="sxs-lookup"><span data-stu-id="7ecf3-145">Enable debug logging</span></span>
<span data-ttu-id="7ecf3-146">有時您需要與要求和回應相關的詳細資訊，以探索哪裡出了錯。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-146">Sometimes you need more information about the request and response to discover what went wrong.</span></span> <span data-ttu-id="7ecf3-147">使用 PowerShell 或 Azure CLI，您可以要求在部署期間記錄其他資訊。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="7ecf3-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ecf3-148">PowerShell</span></span>

   <span data-ttu-id="7ecf3-149">在 PowerShell 中，將 **DeploymentDebugLogLevel** 參數設定為 [All]、[ResponseContent] 或 [RequestContent]。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-149">In PowerShell, set the **DeploymentDebugLogLevel** parameter to All, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="7ecf3-150">檢查具有下列 Cmdlet 的要求內容︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-150">Examine the request content with the following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="7ecf3-151">或者，具有下列項目的回應內容︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-151">Or, the response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="7ecf3-152">此資訊可協助您判斷範本中的值是否會正確設定。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-152">This information can help you determine whether a value in the template is being incorrectly set.</span></span>

- <span data-ttu-id="7ecf3-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7ecf3-153">Azure CLI</span></span>

   <span data-ttu-id="7ecf3-154">使用下列命令檢查部署作業︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-154">Examine the deployment operations with the following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="7ecf3-155">巢狀範本</span><span class="sxs-lookup"><span data-stu-id="7ecf3-155">Nested template</span></span>

   <span data-ttu-id="7ecf3-156">若要記錄巢狀範本的偵錯資訊，請使用 **debugSetting** 項目。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-156">To log debug information for a nested template, use the **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="7ecf3-157">建立疑難排解範本</span><span class="sxs-lookup"><span data-stu-id="7ecf3-157">Create a troubleshooting template</span></span>
<span data-ttu-id="7ecf3-158">在某些情況下，針對範本進行疑難排解的最簡單方式是測試其組件。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-158">In some cases, the easiest way to troubleshoot your template is to test parts of it.</span></span> <span data-ttu-id="7ecf3-159">您可以建立簡化範本，以便專注於您認為是錯誤成因的組件。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-159">You can create a simplified template that enables you to focus on the part that you believe is causing the error.</span></span> <span data-ttu-id="7ecf3-160">例如，假設您在參考資源時收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="7ecf3-161">不需要處理整個範本，而是建立一個會傳回可能造成問題之組件的範本。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-161">Rather than dealing with an entire template, create a template that returns the part that may be causing your problem.</span></span> <span data-ttu-id="7ecf3-162">它可協助您判斷是否傳入正確的參數、正確地使用範本函式，以及取得所預期的資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-162">It can help you determine whether you are passing in the right parameters, using template functions correctly, and getting the resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="7ecf3-163">或者，假設您遇到您認為與未正確設定之相依性有關的部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-163">Or, suppose you are encountering deployment errors that you believe are related to incorrectly set dependencies.</span></span> <span data-ttu-id="7ecf3-164">將其細分為簡化範本以測試您的範本。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="7ecf3-165">首先，建立可部署單一資源 (例如 SQL Server) 的範本。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="7ecf3-166">當您確定已正確定義該資源時，加入依存該資源的資源 (例如 SQL Database)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="7ecf3-167">當您正確定義這兩個資源時，加入其他相依的資源 (例如稽核原則)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="7ecf3-168">在每個測試部署之間，刪除資源群組以確保您充分測試相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-168">In between each test deployment, delete the resource group to make sure you adequately testing the dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="7ecf3-169">檢查部署順序</span><span class="sxs-lookup"><span data-stu-id="7ecf3-169">Check deployment sequence</span></span>

<span data-ttu-id="7ecf3-170">當資源是以非預期的順序部署時，會發生許多部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="7ecf3-171">相依性未正確設定時，就會發生這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="7ecf3-172">當您遺漏必要的相依性時，一個資源會嘗試使用另一個資源的值，但另一個資源還不存在。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-172">When you are missing a needed dependency, one resource attempts to use a value for another resource but the other does not yet exist.</span></span> <span data-ttu-id="7ecf3-173">您會收到錯誤表示找不到資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="7ecf3-174">您可能會不斷遇到這種錯誤類型，因為每個資源的部署時間可能有所不同。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-174">You may encounter this type of error intermittently because the deployment time for each resource can vary.</span></span> <span data-ttu-id="7ecf3-175">例如，您第一次部署資源成功，因為必要的資源恰好即時完成。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-175">For example, your first attempt to deploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="7ecf3-176">不過，您第二次嘗試失敗，因為必要的資源沒有即時完成。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-176">However, your second attempt fails because the required resource did not complete in time.</span></span> 

<span data-ttu-id="7ecf3-177">但是，您要避免設定不需要的相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-177">But, you want to avoid setting dependencies that are not needed.</span></span> <span data-ttu-id="7ecf3-178">當您有不必要的相依性時，您會阻止不互相相依的資源以平行方式部署，而延長部署的時間。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-178">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="7ecf3-179">此外，您可以建立封鎖部署的循環相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-179">In addition, you may create circular dependencies that block the deployment.</span></span> <span data-ttu-id="7ecf3-180">在同一個範本中部署參考的資源時，[reference](resource-group-template-functions-resource.md#reference) 函式會於該資源上建立隱含的相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-180">The [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on the referenced resource, when that resource is deployed in the same template.</span></span> <span data-ttu-id="7ecf3-181">因此，您的相依性可能會比 **dependsOn** 屬性中指定的相依性還多。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-181">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span></span> <span data-ttu-id="7ecf3-182">[resourceId](resource-group-template-functions-resource.md#resourceid) 函式不會建立隱含的相依性或驗證資源存在。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-182">The [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that the resource exists.</span></span>

<span data-ttu-id="7ecf3-183">當您遇到相依性問題時，您需要深入了解資源部署的順序。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-183">When you encounter dependency problems, you need to gain insight into the order of resource deployment.</span></span> <span data-ttu-id="7ecf3-184">若要檢視部署作業的順序︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-184">To view the order of deployment operations:</span></span>

1. <span data-ttu-id="7ecf3-185">選取資源群組的部署歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-185">Select the deployment history for your resource group.</span></span>

   ![選取部署歷程記錄](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="7ecf3-187">從歷程記錄中選取部署，然後選取 [事件]。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-187">Select a deployment from the history, and select **Events**.</span></span>

   ![選取部署事件](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="7ecf3-189">檢查每個資源的事件順序。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-189">Examine the sequence of events for each resource.</span></span> <span data-ttu-id="7ecf3-190">注意每個作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-190">Pay attention to the status of each operation.</span></span> <span data-ttu-id="7ecf3-191">例如，下列映像顯示平行部署的三個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-191">For example, the following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="7ecf3-192">請注意，三個儲存體帳戶會同時啟動。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-192">Notice that the three storage accounts are started at the same time.</span></span>

   ![平行部署](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="7ecf3-194">下一個映像顯示非平行部署的三個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-194">The next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="7ecf3-195">第二個儲存體帳戶相依於第一個儲存體帳戶，而第三個儲存體帳戶相依於第二個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-195">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span></span> <span data-ttu-id="7ecf3-196">因此，第一個儲存體帳戶會在下一個儲存體帳戶啟動之前啟動、接受及完成。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-196">Therefore, the first storage account is started, accepted, and completed before the next is started.</span></span>

   ![連續部署](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="7ecf3-198">即使針對更複雜的案例，您還是可以使用相同的技巧來探索每個資源的部署何時啟動及完成。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-198">Even for more complicated scenarios, you can use the same technique to discover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="7ecf3-199">請查閱您的部署事件以查看順序是否與您預期的不同。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-199">Look through your deployment events to see if the sequence is different than you would expect.</span></span> <span data-ttu-id="7ecf3-200">如果是，請重新評估此資源的相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-200">If so, reevaluate the dependencies for this resource.</span></span>

<span data-ttu-id="7ecf3-201">Resource Manager 範本會在驗證期間識別循環相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="7ecf3-202">它會傳回錯誤訊息，特別指出循環相依性存在。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="7ecf3-203">解決循環相依性︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-203">To solve a circular dependency:</span></span>

1. <span data-ttu-id="7ecf3-204">在範本中，找出循環相依性中所識別的資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-204">In your template, find the resource identified in the circular dependency.</span></span> 
2. <span data-ttu-id="7ecf3-205">針對該資源，檢查 **dependsOn** 屬性和任何使用的 **reference** 函式，查看相依於哪些資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-205">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span></span> 
3. <span data-ttu-id="7ecf3-206">檢查這些資源，查看所相依的資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-206">Examine those resources to see which resources they depend on.</span></span> <span data-ttu-id="7ecf3-207">跟隨相依性，直到您找出相依於原始資源的資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-207">Follow the dependencies until you notice a resource that depends on the original resource.</span></span>
5. <span data-ttu-id="7ecf3-208">針對參與循環相依性的資源，仔細檢查所有使用的 **dependsOn** 屬性，以識別不需要的任何相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-208">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span></span> <span data-ttu-id="7ecf3-209">移除這些相依性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-209">Remove those dependencies.</span></span> <span data-ttu-id="7ecf3-210">如果您不確定是否需要某個相依性，請嘗試移除它。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="7ecf3-211">重新部署範本。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-211">Redeploy the template.</span></span>

<span data-ttu-id="7ecf3-212">移除 **dependsOn** 屬性的值可能會在您部署範本時導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-212">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span></span> <span data-ttu-id="7ecf3-213">如果您遇到錯誤，請將相依性新增回範本。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-213">If you encounter an error, add the dependency back into the template.</span></span> 

<span data-ttu-id="7ecf3-214">如果該方法無法解決循環相依性，請考慮將一部分部署邏輯移到子資源 (例如擴充或設定值)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-214">If that approach does not solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="7ecf3-215">設定這些子資源在參與循環相依性的資源之後才進行部署。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-215">Configure those child resources to deploy after the resources involved in the circular dependency.</span></span> <span data-ttu-id="7ecf3-216">例如，假設您要部署兩部虛擬機器，但是您必須分別在上面設定互相參考的屬性。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="7ecf3-217">您可以採取下列順序部署︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-217">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="7ecf3-218">vm1</span><span class="sxs-lookup"><span data-stu-id="7ecf3-218">vm1</span></span>
2. <span data-ttu-id="7ecf3-219">vm2</span><span class="sxs-lookup"><span data-stu-id="7ecf3-219">vm2</span></span>
3. <span data-ttu-id="7ecf3-220">vm1 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="7ecf3-221">擴充在 vm1 上設定從 vm2 取得的值。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-221">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="7ecf3-222">vm2 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="7ecf3-223">擴充在 vm2 上設定從 vm1 取得的值。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-223">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="7ecf3-224">相同的方法也適用於 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-224">The same approach works for App Service apps.</span></span> <span data-ttu-id="7ecf3-225">請考慮將設定值移入應用程式資源的子資源。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-225">Consider moving configuration values into a child resource of the app resource.</span></span> <span data-ttu-id="7ecf3-226">您可以採取下列順序部署兩個 Web 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="7ecf3-226">You can deploy two web apps in the following order:</span></span>

1. <span data-ttu-id="7ecf3-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="7ecf3-227">webapp1</span></span>
2. <span data-ttu-id="7ecf3-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="7ecf3-228">webapp2</span></span>
3. <span data-ttu-id="7ecf3-229">webapp1 的設定相依於 webapp1 和 webapp2。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="7ecf3-230">它包含使用 webapp2 的值的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="7ecf3-231">webapp2 的設定相依於 webapp1 和 webapp2。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="7ecf3-232">它包含使用 webapp1 的值的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ecf3-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ecf3-233">Next steps</span></span>
* <span data-ttu-id="7ecf3-234">如需常見部署錯誤的解決方案，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-234">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="7ecf3-235">若要了解稽核動作，請參閱 [使用 Resource Manager 來稽核作業](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-235">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="7ecf3-236">若要了解部署期間可採取哪些動作來判斷錯誤，請參閱 [檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="7ecf3-236">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
