---
title: "使用 REST API 和範本 aaaDeploy 資源 |Microsoft 文件"
description: "使用 Azure 資源管理員和資源管理員 REST API toodeploy 資源 tooAzure。 hello 資源的資源管理員範本中定義。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>使用 Resource Manager 範本和 Resource Manager REST API 部署資源
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [入口網站](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

本文說明如何 toouse hello 資源管理員 REST API 與資源管理員範本 toodeploy 資源 tooAzure。  

> [!TIP]
> 如需部署期間偵錯錯誤的說明，請參閱︰
> 
> * [檢視部署作業](resource-manager-deployment-operations.md)toolearn 有關取得資訊可協助您疑難排解您的錯誤
> * [部署資源 tooAzure 與 Azure 資源管理員時，針對常見錯誤進行疑難排解](resource-manager-common-deployment-errors.md)toolearn 如何 tooresolve 常見的部署錯誤
> 
> 

您的範本可以是本機檔案，或者是透過 URI 提供使用的外部檔案。 當您的範本位於儲存體帳戶時，就可以限制存取 toohello 範本，並在部署期間提供的共用的存取簽章 (SAS) token。

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>部署以 hello REST API
1. 設定[一般參數和標頭](https://docs.microsoft.com/rest/api/index) (包括驗證權杖)。
2. 如果您沒有現有資源群組，請建立新的資源群組。 提供您的訂用帳戶 ID、 hello 名稱 hello 新的資源群組，以及您需要為您的方案的位置。 如需詳細資訊，請參閱[建立資源群組](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate)。
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. 驗證您的部署之前先執行 hello[驗證範本部署](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate)作業。 在測試 hello 部署時，提供參數，相同的方式執行 hello 部署 （顯示 hello 下一個步驟中） 時。
4. 建立部署。 提供您的訂用帳戶 ID、 hello hello 資源群組名稱、 hello 部署的 hello 名稱和連結 tooyour 範本。 Hello 範本檔案的相關資訊，請參閱[參數檔](#parameter-file)。 如需 hello REST API toocreate 資源群組的詳細資訊，請參閱[建立範本部署](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate)。 請注意 hello**模式**設定得**Incremental**。 toorun 完整部署，設定**模式**太**完成**。 請小心使用 hello 完整模式，您可以不小心刪除不在範本中的資源時。
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      如果您想要 toolog 回應內容、 要求內容，或兩者，包含**debugSetting** hello 要求中。
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      您可以設定您的儲存體帳戶 toouse 共用的存取簽章 (SAS) token。 如需詳細資訊，請參閱[使用共用存取簽章委派存取](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature)。
5. 取得 hello 範本部署的 hello 狀態。 如需詳細資訊，請參閱[取得範本部署的相關資訊](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get)。
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>參數檔案

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>後續步驟
* toolearn 有關處理非同步 REST 作業，請參閱[追蹤非同步的 Azure 作業](resource-manager-async-operations.md)。
* 如需部署透過 hello.NET 用戶端程式庫資源的範例，請參閱[部署使用.NET 程式庫和範本的資源](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* toodefine 參數在範本中，請參閱[撰寫樣板](resource-group-authoring-templates.md#parameters)。
* 如需部署解決方案 toodifferent 環境需求的指引，請參閱[Microsoft Azure 中的開發和測試環境](solution-dev-test-environments.md)。
* 如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。

