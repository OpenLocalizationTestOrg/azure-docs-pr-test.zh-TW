---
title: "aaaUnderstand Azure 的部署錯誤 |Microsoft 文件"
description: "描述如何 toolearn 關於 Azure 部署錯誤。"
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "部署錯誤，azure 部署，部署 tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="3e429-104">了解 Azure 部署錯誤</span><span class="sxs-lookup"><span data-stu-id="3e429-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="3e429-105">本主題說明部署錯誤，以及如何找出與錯誤相關的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3e429-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="3e429-106">解決方式 toocommon 部署錯誤，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="3e429-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="3e429-107">兩種錯誤類型</span><span class="sxs-lookup"><span data-stu-id="3e429-107">Two types of errors</span></span>
<span data-ttu-id="3e429-108">您可能會收到兩種錯誤類型︰</span><span class="sxs-lookup"><span data-stu-id="3e429-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="3e429-109">驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="3e429-109">validation errors</span></span>
* <span data-ttu-id="3e429-110">部署錯誤</span><span class="sxs-lookup"><span data-stu-id="3e429-110">deployment errors</span></span>

<span data-ttu-id="3e429-111">hello 下列影像顯示 hello 活動記錄檔以取得訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e429-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="3e429-112">它代表兩個部署。</span><span class="sxs-lookup"><span data-stu-id="3e429-112">It represents two deployments.</span></span> <span data-ttu-id="3e429-113">在一個部署中，hello 範本驗證失敗 (**驗證**) 和尚未進行。</span><span class="sxs-lookup"><span data-stu-id="3e429-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="3e429-114">在 hello 其他部署，hello 範本已通過驗證，但無法建立 hello 資源時 (**寫入部署**)。</span><span class="sxs-lookup"><span data-stu-id="3e429-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![顯示錯誤碼](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="3e429-116">驗證錯誤來自可在部署之前判斷的情況。</span><span class="sxs-lookup"><span data-stu-id="3e429-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="3e429-117">它們是在您的範本或嘗試會超過您的訂用帳戶配額的 toodeploy 資源中包含語法錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="3e429-118">部署錯誤會引起 hello 部署程序期間發生的狀況。</span><span class="sxs-lookup"><span data-stu-id="3e429-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="3e429-119">其中包括嘗試 tooaccess 以平行方式部署的資源。</span><span class="sxs-lookup"><span data-stu-id="3e429-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="3e429-120">這兩種類型的錯誤傳回您使用 tootroubleshoot hello 部署錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="3e429-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="3e429-121">這兩種類型的錯誤會出現在 hello[活動記錄檔](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="3e429-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="3e429-122">不過，驗證錯誤不會出現在您的部署歷程記錄中因為 hello 部署永遠不會啟動。</span><span class="sxs-lookup"><span data-stu-id="3e429-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="3e429-123">判斷錯誤碼</span><span class="sxs-lookup"><span data-stu-id="3e429-123">Determine error code</span></span>

<span data-ttu-id="3e429-124">您可以藉由查看 hello 的錯誤訊息以及 hello 錯誤碼深入了解錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="3e429-125">hello[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)文章錯誤碼所列出的解決方式。</span><span class="sxs-lookup"><span data-stu-id="3e429-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="3e429-126">本主題說明如何 toouse hello Azure 入口網站 toodiscover hello 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="3e429-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="3e429-127">驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="3e429-127">Validation errors</span></span>

<span data-ttu-id="3e429-128">部署時透過 hello 入口網站，您會看到驗證錯誤之後正在提交您的值。</span><span class="sxs-lookup"><span data-stu-id="3e429-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![顯示入口網站驗證錯誤](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="3e429-130">選取 hello 訊息，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3e429-130">Select hello message for more details.</span></span> <span data-ttu-id="3e429-131">在下列映像的 hello，您會看到**InvalidTemplateDeployment**錯誤和訊息，指出某個原則封鎖部署。</span><span class="sxs-lookup"><span data-stu-id="3e429-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![顯示驗證詳細資料](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="3e429-133">部署錯誤</span><span class="sxs-lookup"><span data-stu-id="3e429-133">Deployment errors</span></span>

<span data-ttu-id="3e429-134">當 hello 作業通過驗證，但在部署期間發生失敗時，您會看到 hello 通知中的 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="3e429-135">選取 hello 通知。</span><span class="sxs-lookup"><span data-stu-id="3e429-135">Select hello notification.</span></span>

![通知錯誤](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="3e429-137">您會看到更多詳細 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="3e429-137">You see more details about hello deployment.</span></span> <span data-ttu-id="3e429-138">選取 hello 選項 toofind hello 錯誤的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3e429-138">Select hello option toofind more information about hello error.</span></span>

![部署失敗](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="3e429-140">您會看到 hello 訊息和錯誤的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="3e429-140">You see hello error message and error codes.</span></span> <span data-ttu-id="3e429-141">請注意，有兩個錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="3e429-141">Notice there are two error codes.</span></span> <span data-ttu-id="3e429-142">hello 第一個錯誤程式碼 (**DeploymentFailed**) 是一般的錯誤未提供 hello 詳細說明您需要 toosolve hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="3e429-143">hello 第二個錯誤碼 (**StorageAccountNotFound**) 提供您需要的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3e429-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![錯誤詳細資料](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="3e429-145">啟用偵錯記錄</span><span class="sxs-lookup"><span data-stu-id="3e429-145">Enable debug logging</span></span>
<span data-ttu-id="3e429-146">有時候您需要有關 hello 要求和回應 toodiscover 何者發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="3e429-147">使用 PowerShell 或 Azure CLI，您可以要求在部署期間記錄其他資訊。</span><span class="sxs-lookup"><span data-stu-id="3e429-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="3e429-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e429-148">PowerShell</span></span>

   <span data-ttu-id="3e429-149">在 PowerShell 中，設定 hello **DeploymentDebugLogLevel**參數 tooAll、 ResponseContent 或 RequestContent。</span><span class="sxs-lookup"><span data-stu-id="3e429-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="3e429-150">使用下列 cmdlet 的 hello 檢查 hello 要求內容：</span><span class="sxs-lookup"><span data-stu-id="3e429-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="3e429-151">或者，hello 回應的內容：</span><span class="sxs-lookup"><span data-stu-id="3e429-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="3e429-152">此資訊可協助您判斷是否正在正確設定 hello 範本中的值。</span><span class="sxs-lookup"><span data-stu-id="3e429-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="3e429-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3e429-153">Azure CLI</span></span>

   <span data-ttu-id="3e429-154">檢查 hello 部署作業以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="3e429-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="3e429-155">巢狀範本</span><span class="sxs-lookup"><span data-stu-id="3e429-155">Nested template</span></span>

   <span data-ttu-id="3e429-156">巢狀範本，請使用 hello toolog 偵錯資訊**debugSetting**項目。</span><span class="sxs-lookup"><span data-stu-id="3e429-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

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


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="3e429-157">建立疑難排解範本</span><span class="sxs-lookup"><span data-stu-id="3e429-157">Create a troubleshooting template</span></span>
<span data-ttu-id="3e429-158">在某些情況下，hello 最簡單的方式 tootroubleshoot 您的範本是 tootest 部分。</span><span class="sxs-lookup"><span data-stu-id="3e429-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="3e429-159">您可以建立可讓您簡化的範本 toofocus，您認為造成 hello 錯誤的 hello 組件上。</span><span class="sxs-lookup"><span data-stu-id="3e429-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="3e429-160">例如，假設您在參考資源時收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="3e429-161">而不是處理整個的範本時，建立範本，可傳回 hello 一部分可能會造成您的問題。</span><span class="sxs-lookup"><span data-stu-id="3e429-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="3e429-162">它可協助您判斷是否您將傳入 hello 正確的參數，正確地使用樣板函式，而您收到 hello 資源預期。</span><span class="sxs-lookup"><span data-stu-id="3e429-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

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

<span data-ttu-id="3e429-163">或者，假設您遇到您認為 tooincorrectly 設定相依性相關的部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="3e429-164">將其細分為簡化範本以測試您的範本。</span><span class="sxs-lookup"><span data-stu-id="3e429-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="3e429-165">首先，建立可部署單一資源 (例如 SQL Server) 的範本。</span><span class="sxs-lookup"><span data-stu-id="3e429-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="3e429-166">當您確定已正確定義該資源時，加入依存該資源的資源 (例如 SQL Database)。</span><span class="sxs-lookup"><span data-stu-id="3e429-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="3e429-167">當您正確定義這兩個資源時，加入其他相依的資源 (例如稽核原則)。</span><span class="sxs-lookup"><span data-stu-id="3e429-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="3e429-168">每個測試部署，之間刪除 hello 資源群組 toomake 確定您可以充分地測試 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="3e429-169">檢查部署順序</span><span class="sxs-lookup"><span data-stu-id="3e429-169">Check deployment sequence</span></span>

<span data-ttu-id="3e429-170">當資源是以非預期的順序部署時，會發生許多部署錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="3e429-171">相依性未正確設定時，就會發生這些錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e429-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="3e429-172">當您遺漏所需的相依性時，一項資源會嘗試的 toouse 尚未存在另一個資源，但其他 hello 的值。</span><span class="sxs-lookup"><span data-stu-id="3e429-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="3e429-173">您會收到錯誤表示找不到資源。</span><span class="sxs-lookup"><span data-stu-id="3e429-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="3e429-174">可能會遇到這種類型的錯誤或間歇性因為 hello 部署時間，每個資源而有所不同。</span><span class="sxs-lookup"><span data-stu-id="3e429-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="3e429-175">例如，第一次的嘗試 toodeploy 資源成功，因為有項必要的資源隨機完成的時間。</span><span class="sxs-lookup"><span data-stu-id="3e429-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="3e429-176">不過，您的第二次嘗試會失敗，因為 hello 所需的資源未完成的時間。</span><span class="sxs-lookup"><span data-stu-id="3e429-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="3e429-177">但是，您希望不需 tooavoid 設定相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="3e429-178">當您有不必要的相依性時，您便會延長 hello hello 部署期間，防止不以平行方式部署彼此相依的資源。</span><span class="sxs-lookup"><span data-stu-id="3e429-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="3e429-179">此外，您可以建立封鎖 hello 部署的循環相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="3e429-180">hello[參考](resource-group-template-functions-resource.md#reference)函式會建立隱含的相依性參考 hello 資源中 hello 部署該資源時相同的範本。</span><span class="sxs-lookup"><span data-stu-id="3e429-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="3e429-181">因此，您可能需要比 hello hello 中指定的相依性的多個相依性**dependsOn**屬性。</span><span class="sxs-lookup"><span data-stu-id="3e429-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="3e429-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid)函式不會建立隱含的相依性或驗證 hello 資源已存在。</span><span class="sxs-lookup"><span data-stu-id="3e429-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="3e429-183">當您遇到相依性問題時，您會需要 toogain 深入了解資源部署的 hello 順序。</span><span class="sxs-lookup"><span data-stu-id="3e429-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="3e429-184">tooview hello 順序的部署作業：</span><span class="sxs-lookup"><span data-stu-id="3e429-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="3e429-185">選取資源群組的 hello 部署歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="3e429-185">Select hello deployment history for your resource group.</span></span>

   ![選取部署歷程記錄](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="3e429-187">從 hello 歷程記錄中，選取任一部署，然後選取**事件**。</span><span class="sxs-lookup"><span data-stu-id="3e429-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![選取部署事件](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="3e429-189">檢查 hello 一連串的每個資源的事件。</span><span class="sxs-lookup"><span data-stu-id="3e429-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="3e429-190">請注意 toohello 狀態，每個作業。</span><span class="sxs-lookup"><span data-stu-id="3e429-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="3e429-191">例如，hello 下圖顯示三個部署的儲存體帳戶以平行方式。</span><span class="sxs-lookup"><span data-stu-id="3e429-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="3e429-192">請注意，hello 三個儲存體帳戶在 hello 啟動相同的時間。</span><span class="sxs-lookup"><span data-stu-id="3e429-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![平行部署](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="3e429-194">hello 下一個影像會顯示尚未部署的三個儲存體帳戶，以平行方式。</span><span class="sxs-lookup"><span data-stu-id="3e429-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="3e429-195">hello 第二個儲存體帳戶取決於 hello 第一個儲存體帳戶，以及第三個儲存體帳戶 hello 取決於 hello 第二個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e429-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="3e429-196">因此，hello 第一個儲存體帳戶啟動、 接受，及接下來啟動 hello 之前完成。</span><span class="sxs-lookup"><span data-stu-id="3e429-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![連續部署](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="3e429-198">即使對於更複雜的情況，您可以使用 hello 相同的技巧 toodiscover 時啟動及完成的每個資源部署。</span><span class="sxs-lookup"><span data-stu-id="3e429-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="3e429-199">如果 hello 順序不會比預期不同，請查看您的部署事件 toosee。</span><span class="sxs-lookup"><span data-stu-id="3e429-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="3e429-200">若是如此，重新評估 hello 這個資源的相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="3e429-201">Resource Manager 範本會在驗證期間識別循環相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="3e429-202">它會傳回錯誤訊息，特別指出循環相依性存在。</span><span class="sxs-lookup"><span data-stu-id="3e429-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="3e429-203">toosolve 循環相依性：</span><span class="sxs-lookup"><span data-stu-id="3e429-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="3e429-204">在範本中，尋找 hello hello 循環相依性中所識別的資源。</span><span class="sxs-lookup"><span data-stu-id="3e429-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="3e429-205">該資源中，檢查 hello **dependsOn**屬性和任何使用 hello**參考**函式的 toosee 它相依於哪些資源。</span><span class="sxs-lookup"><span data-stu-id="3e429-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="3e429-206">檢查哪些資源它們依存這些資源 toosee。</span><span class="sxs-lookup"><span data-stu-id="3e429-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="3e429-207">您會注意到相依於 hello 原始資源的資源之前，請遵循 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="3e429-208">如需 hello 資源參與 hello 循環相依性，仔細檢查所有使用 hello **dependsOn**屬性 tooidentify 不需要任何相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="3e429-209">移除這些相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-209">Remove those dependencies.</span></span> <span data-ttu-id="3e429-210">如果您不確定是否需要某個相依性，請嘗試移除它。</span><span class="sxs-lookup"><span data-stu-id="3e429-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="3e429-211">重新部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3e429-211">Redeploy hello template.</span></span>

<span data-ttu-id="3e429-212">移除值從 hello **dependsOn**屬性可能會導致錯誤，當您部署的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="3e429-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="3e429-213">如果您遇到錯誤時，新增回 hello 範本 hello 相依性。</span><span class="sxs-lookup"><span data-stu-id="3e429-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="3e429-214">如果該方法無法解決 hello 循環相依性，請考慮將您的部署邏輯的一部分移到子資源 （例如擴充功能或組態設定）。</span><span class="sxs-lookup"><span data-stu-id="3e429-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="3e429-215">設定這些子資源 toodeploy 之後所涉及的 hello 循環相依性的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="3e429-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="3e429-216">例如，假設您要部署兩部虛擬機器，但您必須設定，請參閱 toohello 其他每一個屬性。</span><span class="sxs-lookup"><span data-stu-id="3e429-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="3e429-217">您可以將它們部署在 hello 順序：</span><span class="sxs-lookup"><span data-stu-id="3e429-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="3e429-218">vm1</span><span class="sxs-lookup"><span data-stu-id="3e429-218">vm1</span></span>
2. <span data-ttu-id="3e429-219">vm2</span><span class="sxs-lookup"><span data-stu-id="3e429-219">vm2</span></span>
3. <span data-ttu-id="3e429-220">vm1 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="3e429-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="3e429-221">hello 延伸模組設定 vm1 它 vm2 從取得的值。</span><span class="sxs-lookup"><span data-stu-id="3e429-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="3e429-222">vm2 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="3e429-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="3e429-223">hello 延伸模組設定 vm2 它 vm1 從取得的值。</span><span class="sxs-lookup"><span data-stu-id="3e429-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="3e429-224">hello 相同的方法適用於 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3e429-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="3e429-225">請考慮將組態值移到 hello 應用程式資源的子資源。</span><span class="sxs-lookup"><span data-stu-id="3e429-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="3e429-226">您可以部署在 hello 順序中的兩個 web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="3e429-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="3e429-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="3e429-227">webapp1</span></span>
2. <span data-ttu-id="3e429-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="3e429-228">webapp2</span></span>
3. <span data-ttu-id="3e429-229">webapp1 的設定相依於 webapp1 和 webapp2。</span><span class="sxs-lookup"><span data-stu-id="3e429-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="3e429-230">它包含使用 webapp2 的值的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="3e429-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="3e429-231">webapp2 的設定相依於 webapp1 和 webapp2。</span><span class="sxs-lookup"><span data-stu-id="3e429-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="3e429-232">它包含使用 webapp1 的值的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="3e429-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3e429-233">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e429-233">Next steps</span></span>
* <span data-ttu-id="3e429-234">解決方式 toocommon 部署錯誤，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="3e429-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="3e429-235">toolearn 有關稽核的動作，請參閱[稽核與資源管理員作業](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="3e429-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="3e429-236">toolearn 有關動作 toodetermine hello 錯誤，在部署期間，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="3e429-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
