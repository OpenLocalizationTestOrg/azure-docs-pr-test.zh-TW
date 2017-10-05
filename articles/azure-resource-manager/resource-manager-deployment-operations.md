---
title: "使用 Azure Resource Manager 進行的部署作業 | Microsoft Docs"
description: "說明如何使用入口網站、PowerShell、Azure CLI 及 REST API 來檢視 Azure Resource Manager 部署作業。"
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="6fdad-103">使用 Azure Resource Manager 來檢視部署作業</span><span class="sxs-lookup"><span data-stu-id="6fdad-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="6fdad-104">您可以透過 Azure 入口網站檢視部署的作業。</span><span class="sxs-lookup"><span data-stu-id="6fdad-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="6fdad-105">當您在部署期間收到錯誤時，您可能對於檢視作業最感興趣，所以本文著重於檢視失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="6fdad-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="6fdad-106">入口網站提供介面，讓您輕鬆地找到錯誤並判斷可能的修正方法。</span><span class="sxs-lookup"><span data-stu-id="6fdad-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="6fdad-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="6fdad-107">Portal</span></span>
<span data-ttu-id="6fdad-108">若要查看部署作業，請使用下列步驟 ︰</span><span class="sxs-lookup"><span data-stu-id="6fdad-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="6fdad-109">針對部署所含的資源群組，請注意最後一個部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="6fdad-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="6fdad-110">您可以選取此狀態，以取得更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6fdad-110">You can select this status to get more details.</span></span>
   
    ![deployment status](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="6fdad-112">您會看到最近的部署歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="6fdad-112">You see the recent deployment history.</span></span> <span data-ttu-id="6fdad-113">選取失敗的部署。</span><span class="sxs-lookup"><span data-stu-id="6fdad-113">Select the deployment that failed.</span></span>
   
    ![deployment status](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="6fdad-115">選取連結以查看部署失敗的原因描述。</span><span class="sxs-lookup"><span data-stu-id="6fdad-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="6fdad-116">在下圖中，DNS 記錄不是唯一的。</span><span class="sxs-lookup"><span data-stu-id="6fdad-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![檢視失敗的部署](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="6fdad-118">此錯誤訊息應足以讓您開始進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="6fdad-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="6fdad-119">不過，如果您需要有關哪些工作已完成的詳細資料，您可以檢視如下列步驟中所示的作業。</span><span class="sxs-lookup"><span data-stu-id="6fdad-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="6fdad-120">您可以在 [部署] 刀鋒視窗中檢視所有的部署作業。</span><span class="sxs-lookup"><span data-stu-id="6fdad-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="6fdad-121">選取任一作業以查看詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6fdad-121">Select any operation to see more details.</span></span>
   
    ![檢視作業](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="6fdad-123">在此情況下，您會看到儲存體帳戶、虛擬網路和可用性設定組都已成功建立。</span><span class="sxs-lookup"><span data-stu-id="6fdad-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="6fdad-124">公用 IP 位址失敗，並未嘗試其他資源。</span><span class="sxs-lookup"><span data-stu-id="6fdad-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="6fdad-125">您可以選取 [事件] ，以檢視部署的事件。</span><span class="sxs-lookup"><span data-stu-id="6fdad-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![檢視事件](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="6fdad-127">您會看見部署的所有事件，選取任何一個事件即可取得詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6fdad-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="6fdad-128">請一併注意相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="6fdad-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="6fdad-129">與技術支援人員合作來排解部署問題時，此值會相當有用。</span><span class="sxs-lookup"><span data-stu-id="6fdad-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![查看事件](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="6fdad-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fdad-131">PowerShell</span></span>
1. <span data-ttu-id="6fdad-132">若要取得部署的整體狀態，請使用 **Get-AzureRmResourceGroupDeployment** 命令。</span><span class="sxs-lookup"><span data-stu-id="6fdad-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="6fdad-133">或者，您也可以篩選結果，只找出失敗的部署。</span><span class="sxs-lookup"><span data-stu-id="6fdad-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="6fdad-134">每個部署都包括多個作業。</span><span class="sxs-lookup"><span data-stu-id="6fdad-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="6fdad-135">每個作業皆代表部署程序中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="6fdad-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="6fdad-136">若要探索部署有何問題，您通常需要查看有關部署作業的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6fdad-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="6fdad-137">您可以利用 **Get-AzureRmResourceGroupDeploymentOperation**查看作業的狀態。</span><span class="sxs-lookup"><span data-stu-id="6fdad-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="6fdad-138">以下列格式傳回多項作業︰</span><span class="sxs-lookup"><span data-stu-id="6fdad-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="6fdad-139">若要取得有關失敗作業的詳細資訊，請擷取具有 [失敗]  狀態的作業屬性。</span><span class="sxs-lookup"><span data-stu-id="6fdad-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="6fdad-140">這會以下列格式傳回所有失敗的作業︰</span><span class="sxs-lookup"><span data-stu-id="6fdad-140">Which returns all the failed operations with each one in the following format:</span></span>

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    <span data-ttu-id="6fdad-141">請記下此作業的 serviceRequestId 和 trackingId。</span><span class="sxs-lookup"><span data-stu-id="6fdad-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="6fdad-142">與技術支援人員合作來排解部署問題時，serviceRequestId 會相當有用。</span><span class="sxs-lookup"><span data-stu-id="6fdad-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="6fdad-143">您將在下一個步驟中運用 trackingId 將重點放在特定的作業。</span><span class="sxs-lookup"><span data-stu-id="6fdad-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="6fdad-144">若要取得特定失敗作業的狀態訊息，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="6fdad-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="6fdad-145">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="6fdad-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="6fdad-146">Azure 中的每個部署作業包含要求和回應內容。</span><span class="sxs-lookup"><span data-stu-id="6fdad-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="6fdad-147">要求內容是部署期間您傳送至 Azure 的內容 (例如，建立 VM、作業系統磁碟和其他資源)。</span><span class="sxs-lookup"><span data-stu-id="6fdad-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="6fdad-148">回應內容是 Azure 從您的部署要求傳送回來的內容。</span><span class="sxs-lookup"><span data-stu-id="6fdad-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="6fdad-149">部署期間，您可以使用 **DeploymentDebugLogLevel** 參數來指定要求和/或回應會保留在記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="6fdad-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="6fdad-150">您會使用下列 PowerShell 命令從記錄檔取得該資訊，並將它儲存在本機︰</span><span class="sxs-lookup"><span data-stu-id="6fdad-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="6fdad-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6fdad-151">Azure CLI</span></span>

1. <span data-ttu-id="6fdad-152">利用 **azure group deployment show** 命令取得部署的整體狀態。</span><span class="sxs-lookup"><span data-stu-id="6fdad-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="6fdad-153">其中一個傳回的值是 **correlationId**。</span><span class="sxs-lookup"><span data-stu-id="6fdad-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="6fdad-154">此值可用來追蹤相關的事件，並且在與技術支援人員合作來排解部署問題時會相當有用。</span><span class="sxs-lookup"><span data-stu-id="6fdad-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="6fdad-155">若要查看某個部署的作業，請使用：</span><span class="sxs-lookup"><span data-stu-id="6fdad-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="6fdad-156">REST</span><span class="sxs-lookup"><span data-stu-id="6fdad-156">REST</span></span>

1. <span data-ttu-id="6fdad-157">利用 [取得範本部署的相關資訊](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) 作業，來取得部署相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6fdad-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="6fdad-158">在回應中，請特別注意 **provisioningState**、**correlationId** 和 **error** 元素。</span><span class="sxs-lookup"><span data-stu-id="6fdad-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="6fdad-159">**correlationId** 可用來追蹤相關的事件，並且在與技術支援人員合作來排解部署問題時會相當有用。</span><span class="sxs-lookup"><span data-stu-id="6fdad-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. <span data-ttu-id="6fdad-160">使用 [列出所有範本部署作業](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) 的作業，來取得部署作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6fdad-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="6fdad-161">回應會根據您在部署期間於 **debugSetting** 屬性中指定的內容，來包含要求和 (或) 回應資訊。</span><span class="sxs-lookup"><span data-stu-id="6fdad-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a><span data-ttu-id="6fdad-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fdad-162">Next steps</span></span>
* <span data-ttu-id="6fdad-163">如需解決特定部署錯誤的說明，請參閱 [針對使用 Azure Resource Manager 將資源部署至 Azure 時常見的錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="6fdad-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="6fdad-164">若要了解如何使用活動記錄來監視其他類型的動作，請參閱[檢視活動記錄以管理 Azure 資源](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="6fdad-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="6fdad-165">若要在執行之前驗證您的部署，請參閱 [使用 Azure Resource Manager 範本部署資源群組](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="6fdad-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

