---
title: "aaaDeployment 作業使用 Azure Resource Manager |Microsoft 文件"
description: "描述如何 tooview Azure Resource Manager 部署作業與 hello 入口網站、 PowerShell、 Azure CLI 和 REST API。"
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
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="52174-103">使用 Azure Resource Manager 來檢視部署作業</span><span class="sxs-lookup"><span data-stu-id="52174-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="52174-104">您可以檢視透過 hello Azure 入口網站部署的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="52174-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="52174-105">您可能會最想要檢視 hello 作業，當您具有在部署期間收到錯誤，所以本文會著重於檢視失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="52174-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="52174-106">hello 入口網站提供的介面，可讓您找出 hello tooeasily 的錯誤，並判斷可能的修正方法。</span><span class="sxs-lookup"><span data-stu-id="52174-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="52174-107">入口網站</span><span class="sxs-lookup"><span data-stu-id="52174-107">Portal</span></span>
<span data-ttu-id="52174-108">toosee hello 部署作業，請使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="52174-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="52174-109">Hello 資源群組參與 hello 部署，請注意 hello hello 最後一個部署狀態。</span><span class="sxs-lookup"><span data-stu-id="52174-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="52174-110">您可以選取此狀態 tooget 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52174-110">You can select this status tooget more details.</span></span>
   
    ![deployment status](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="52174-112">您會看到 hello 最新的部署歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="52174-112">You see hello recent deployment history.</span></span> <span data-ttu-id="52174-113">選取 hello 部署失敗。</span><span class="sxs-lookup"><span data-stu-id="52174-113">Select hello deployment that failed.</span></span>
   
    ![deployment status](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="52174-115">選取 hello 連結 toosee 的原因描述 hello 部署失敗。</span><span class="sxs-lookup"><span data-stu-id="52174-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="52174-116">在下面的 hello 影像，hello DNS 記錄不是唯一的。</span><span class="sxs-lookup"><span data-stu-id="52174-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![檢視失敗的部署](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="52174-118">這則錯誤訊息應足以供您 toobegin 疑難排解。</span><span class="sxs-lookup"><span data-stu-id="52174-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="52174-119">不過，如果您需要更多詳細資料的已完成工作時，您可以檢視 hello 作業 hello 步驟中所示。</span><span class="sxs-lookup"><span data-stu-id="52174-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="52174-120">您可以檢視所有 hello 部署作業中 hello**部署**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="52174-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="52174-121">選取任何作業 toosee 更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52174-121">Select any operation toosee more details.</span></span>
   
    ![檢視作業](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="52174-123">在此情況下，您會看到 hello 儲存體帳戶、 虛擬網路和可用性設定組已成功建立。</span><span class="sxs-lookup"><span data-stu-id="52174-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="52174-124">hello 公用 IP 位址失敗時，和其他資源而未嘗試進行。</span><span class="sxs-lookup"><span data-stu-id="52174-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="52174-125">您可以選取來檢視事件 hello 部署**事件**。</span><span class="sxs-lookup"><span data-stu-id="52174-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![檢視事件](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="52174-127">您看到所有 hello 部署的 hello 事件，並選取任何一個，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="52174-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="52174-128">請注意太 hello 相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="52174-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="52174-129">使用技術支援人員 tootroubleshoot 部署時，這個值可以是很有幫助。</span><span class="sxs-lookup"><span data-stu-id="52174-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![查看事件](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="52174-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="52174-131">PowerShell</span></span>
1. <span data-ttu-id="52174-132">tooget hello 整體狀態的部署時，使用 hello **Get AzureRmResourceGroupDeployment**命令。</span><span class="sxs-lookup"><span data-stu-id="52174-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="52174-133">或者，您可以篩選只在已失敗的部署的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="52174-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="52174-134">每個部署都包括多個作業。</span><span class="sxs-lookup"><span data-stu-id="52174-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="52174-135">每一項作業代表 hello 部署程序中的步驟。</span><span class="sxs-lookup"><span data-stu-id="52174-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="52174-136">toodiscover 發生了什麼錯誤與部署，您通常需要 toosee hello 部署作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="52174-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="52174-137">您可以查看 hello 狀態的 hello 作業**Get AzureRmResourceGroupDeploymentOperation**。</span><span class="sxs-lookup"><span data-stu-id="52174-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="52174-138">它會傳回多個作業具有下列格式的 hello 中的每一個：</span><span class="sxs-lookup"><span data-stu-id="52174-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="52174-139">tooget 詳細失敗的作業，擷取作業與 hello 屬性**失敗**狀態。</span><span class="sxs-lookup"><span data-stu-id="52174-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="52174-140">它會傳回所有與 hello 遵循格式中的每一個 hello 失敗的作業：</span><span class="sxs-lookup"><span data-stu-id="52174-140">Which returns all hello failed operations with each one in hello following format:</span></span>

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

    <span data-ttu-id="52174-141">請注意 hello serviceRequestId hello trackingId hello 作業。</span><span class="sxs-lookup"><span data-stu-id="52174-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="52174-142">使用技術支援人員 tootroubleshoot 部署時，hello serviceRequestId 可能很有用。</span><span class="sxs-lookup"><span data-stu-id="52174-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="52174-143">您將使用 hello trackingId hello 下一個步驟 toofocus 上特定作業中。</span><span class="sxs-lookup"><span data-stu-id="52174-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="52174-144">特定的失敗作業，下列命令使用 hello tooget hello 狀態訊息：</span><span class="sxs-lookup"><span data-stu-id="52174-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="52174-145">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="52174-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="52174-146">Azure 中的每個部署作業包含要求和回應內容。</span><span class="sxs-lookup"><span data-stu-id="52174-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="52174-147">hello 要求內容是什麼您傳送 tooAzure 在部署期間 (例如，建立的 VM，作業系統磁碟和其他資源)。</span><span class="sxs-lookup"><span data-stu-id="52174-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="52174-148">hello 回應內容是 Azure 傳送回從您的部署要求。</span><span class="sxs-lookup"><span data-stu-id="52174-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="52174-149">在部署期間，您可以使用**DeploymentDebugLogLevel** hello 要求和/或回應的參數 toospecify 會保留在 hello 記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="52174-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="52174-150">您從 hello 記錄檔，取得這項資訊，並將它儲存在本機上使用下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="52174-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="52174-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="52174-151">Azure CLI</span></span>

1. <span data-ttu-id="52174-152">取得部署的整體狀態 hello 以 hello **azure 群組部署顯示**命令。</span><span class="sxs-lookup"><span data-stu-id="52174-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="52174-153">其中一個 hello 傳回值為 hello **correlationId**。</span><span class="sxs-lookup"><span data-stu-id="52174-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="52174-154">會使用此值 tootrack 相關的事件，而且可以很有幫助時使用的技術支援人員 tootroubleshoot 部署。</span><span class="sxs-lookup"><span data-stu-id="52174-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="52174-155">針對部署中，使用 toosee hello 作業：</span><span class="sxs-lookup"><span data-stu-id="52174-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="52174-156">REST</span><span class="sxs-lookup"><span data-stu-id="52174-156">REST</span></span>

1. <span data-ttu-id="52174-157">取得以 hello 部署的相關資訊[取得範本部署的相關資訊](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)作業。</span><span class="sxs-lookup"><span data-stu-id="52174-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="52174-158">Hello 回應，請特別注意 hello **provisioningState**， **correlationId**，和**錯誤**項目。</span><span class="sxs-lookup"><span data-stu-id="52174-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="52174-159">hello **correlationId**用 tootrack 相關的事件，而且可以很有幫助時使用的技術支援人員 tootroubleshoot 部署。</span><span class="sxs-lookup"><span data-stu-id="52174-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="52174-160">取得以 hello 的部署作業的相關資訊[列出所有範本部署作業](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List)作業。</span><span class="sxs-lookup"><span data-stu-id="52174-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="52174-161">hello 回應包含要求和/或回應的資訊，根據您指定在 hello **debugSetting**在部署期間的屬性。</span><span class="sxs-lookup"><span data-stu-id="52174-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="52174-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52174-162">Next steps</span></span>
* <span data-ttu-id="52174-163">如需協助解決特定部署錯誤，請參閱[部署資源 tooAzure 與 Azure 資源管理員時，解決常見的錯誤](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="52174-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="52174-164">有關使用 hello 活動 toolearn 記錄 toomonitor 其他類型的動作，請參閱[檢視活動記錄 toomanage Azure 資源](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="52174-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="52174-165">toovalidate 您的部署，然後再執行它，請參閱[部署的資源群組與 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="52174-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

