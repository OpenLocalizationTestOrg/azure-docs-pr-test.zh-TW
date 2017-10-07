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
# <a name="view-deployment-operations-with-azure-resource-manager"></a>使用 Azure Resource Manager 來檢視部署作業


您可以檢視透過 hello Azure 入口網站部署的 hello 作業。 您可能會最想要檢視 hello 作業，當您具有在部署期間收到錯誤，所以本文會著重於檢視失敗的作業。 hello 入口網站提供的介面，可讓您找出 hello tooeasily 的錯誤，並判斷可能的修正方法。

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>入口網站
toosee hello 部署作業，請使用下列步驟的 hello:

1. Hello 資源群組參與 hello 部署，請注意 hello hello 最後一個部署狀態。 您可以選取此狀態 tooget 更多詳細資料。
   
    ![deployment status](./media/resource-manager-deployment-operations/deployment-status.png)
2. 您會看到 hello 最新的部署歷程記錄。 選取 hello 部署失敗。
   
    ![deployment status](./media/resource-manager-deployment-operations/select-deployment.png)
3. 選取 hello 連結 toosee 的原因描述 hello 部署失敗。 在下面的 hello 影像，hello DNS 記錄不是唯一的。  
   
    ![檢視失敗的部署](./media/resource-manager-deployment-operations/view-error.png)
   
    這則錯誤訊息應足以供您 toobegin 疑難排解。 不過，如果您需要更多詳細資料的已完成工作時，您可以檢視 hello 作業 hello 步驟中所示。
4. 您可以檢視所有 hello 部署作業中 hello**部署**刀鋒視窗。 選取任何作業 toosee 更多詳細資料。
   
    ![檢視作業](./media/resource-manager-deployment-operations/view-operations.png)
   
    在此情況下，您會看到 hello 儲存體帳戶、 虛擬網路和可用性設定組已成功建立。 hello 公用 IP 位址失敗時，和其他資源而未嘗試進行。
5. 您可以選取來檢視事件 hello 部署**事件**。
   
    ![檢視事件](./media/resource-manager-deployment-operations/view-events.png)
6. 您看到所有 hello 部署的 hello 事件，並選取任何一個，如需詳細資訊。 請注意太 hello 相互關聯識別碼。 使用技術支援人員 tootroubleshoot 部署時，這個值可以是很有幫助。
   
    ![查看事件](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget hello 整體狀態的部署時，使用 hello **Get AzureRmResourceGroupDeployment**命令。 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   或者，您可以篩選只在已失敗的部署的 hello 結果。

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. 每個部署都包括多個作業。 每一項作業代表 hello 部署程序中的步驟。 toodiscover 發生了什麼錯誤與部署，您通常需要 toosee hello 部署作業的詳細資料。 您可以查看 hello 狀態的 hello 作業**Get AzureRmResourceGroupDeploymentOperation**。

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    它會傳回多個作業具有下列格式的 hello 中的每一個：

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget 詳細失敗的作業，擷取作業與 hello 屬性**失敗**狀態。

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    它會傳回所有與 hello 遵循格式中的每一個 hello 失敗的作業：

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

    請注意 hello serviceRequestId hello trackingId hello 作業。 使用技術支援人員 tootroubleshoot 部署時，hello serviceRequestId 可能很有用。 您將使用 hello trackingId hello 下一個步驟 toofocus 上特定作業中。
4. 特定的失敗作業，下列命令使用 hello tooget hello 狀態訊息：

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    它會傳回：

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Azure 中的每個部署作業包含要求和回應內容。 hello 要求內容是什麼您傳送 tooAzure 在部署期間 (例如，建立的 VM，作業系統磁碟和其他資源)。 hello 回應內容是 Azure 傳送回從您的部署要求。 在部署期間，您可以使用**DeploymentDebugLogLevel** hello 要求和/或回應的參數 toospecify 會保留在 hello 記錄檔中。 

  您從 hello 記錄檔，取得這項資訊，並將它儲存在本機上使用下列 PowerShell 命令的 hello:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Azure CLI

1. 取得部署的整體狀態 hello 以 hello **azure 群組部署顯示**命令。

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  其中一個 hello 傳回值為 hello **correlationId**。 會使用此值 tootrack 相關的事件，而且可以很有幫助時使用的技術支援人員 tootroubleshoot 部署。

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. 針對部署中，使用 toosee hello 作業：

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. 取得以 hello 部署的相關資訊[取得範本部署的相關資訊](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)作業。

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    Hello 回應，請特別注意 hello **provisioningState**， **correlationId**，和**錯誤**項目。 hello **correlationId**用 tootrack 相關的事件，而且可以很有幫助時使用的技術支援人員 tootroubleshoot 部署。

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

2. 取得以 hello 的部署作業的相關資訊[列出所有範本部署作業](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List)作業。 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    hello 回應包含要求和/或回應的資訊，根據您指定在 hello **debugSetting**在部署期間的屬性。

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


## <a name="next-steps"></a>後續步驟
* 如需協助解決特定部署錯誤，請參閱[部署資源 tooAzure 與 Azure 資源管理員時，解決常見的錯誤](resource-manager-common-deployment-errors.md)。
* 有關使用 hello 活動 toolearn 記錄 toomonitor 其他類型的動作，請參閱[檢視活動記錄 toomanage Azure 資源](resource-group-audit.md)。
* toovalidate 您的部署，然後再執行它，請參閱[部署的資源群組與 Azure Resource Manager 範本](resource-group-template-deploy.md)。

