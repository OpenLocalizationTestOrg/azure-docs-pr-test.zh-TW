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
# <a name="understand-azure-deployment-errors"></a>了解 Azure 部署錯誤
本主題說明部署錯誤，以及如何找出與錯誤相關的詳細資訊。 解決方式 toocommon 部署錯誤，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。

## <a name="two-types-of-errors"></a>兩種錯誤類型
您可能會收到兩種錯誤類型︰

* 驗證錯誤
* 部署錯誤

hello 下列影像顯示 hello 活動記錄檔以取得訂用帳戶。 它代表兩個部署。 在一個部署中，hello 範本驗證失敗 (**驗證**) 和尚未進行。 在 hello 其他部署，hello 範本已通過驗證，但無法建立 hello 資源時 (**寫入部署**)。 

![顯示錯誤碼](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

驗證錯誤來自可在部署之前判斷的情況。 它們是在您的範本或嘗試會超過您的訂用帳戶配額的 toodeploy 資源中包含語法錯誤。 部署錯誤會引起 hello 部署程序期間發生的狀況。 其中包括嘗試 tooaccess 以平行方式部署的資源。

這兩種類型的錯誤傳回您使用 tootroubleshoot hello 部署錯誤碼。 這兩種類型的錯誤會出現在 hello[活動記錄檔](resource-group-audit.md)。 不過，驗證錯誤不會出現在您的部署歷程記錄中因為 hello 部署永遠不會啟動。

## <a name="determine-error-code"></a>判斷錯誤碼

您可以藉由查看 hello 的錯誤訊息以及 hello 錯誤碼深入了解錯誤。 hello[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)文章錯誤碼所列出的解決方式。 本主題說明如何 toouse hello Azure 入口網站 toodiscover hello 錯誤碼。

### <a name="validation-errors"></a>驗證錯誤

部署時透過 hello 入口網站，您會看到驗證錯誤之後正在提交您的值。

![顯示入口網站驗證錯誤](./media/resource-manager-troubleshoot-tips/validation-error.png)

選取 hello 訊息，如需詳細資訊。 在下列映像的 hello，您會看到**InvalidTemplateDeployment**錯誤和訊息，指出某個原則封鎖部署。

![顯示驗證詳細資料](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a>部署錯誤

當 hello 作業通過驗證，但在部署期間發生失敗時，您會看到 hello 通知中的 hello 錯誤。 選取 hello 通知。

![通知錯誤](./media/resource-manager-troubleshoot-tips/notification.png)

您會看到更多詳細 hello 部署。 選取 hello 選項 toofind hello 錯誤的詳細資訊。

![部署失敗](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

您會看到 hello 訊息和錯誤的錯誤碼。 請注意，有兩個錯誤碼。 hello 第一個錯誤程式碼 (**DeploymentFailed**) 是一般的錯誤未提供 hello 詳細說明您需要 toosolve hello 錯誤。 hello 第二個錯誤碼 (**StorageAccountNotFound**) 提供您需要的 hello 詳細資料。 

![錯誤詳細資料](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a>啟用偵錯記錄
有時候您需要有關 hello 要求和回應 toodiscover 何者發生錯誤。 使用 PowerShell 或 Azure CLI，您可以要求在部署期間記錄其他資訊。

- PowerShell

   在 PowerShell 中，設定 hello **DeploymentDebugLogLevel**參數 tooAll、 ResponseContent 或 RequestContent。

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   使用下列 cmdlet 的 hello 檢查 hello 要求內容：

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   或者，hello 回應的內容：

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   此資訊可協助您判斷是否正在正確設定 hello 範本中的值。

- Azure CLI

   檢查 hello 部署作業以 hello 下列命令：

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- 巢狀範本

   巢狀範本，請使用 hello toolog 偵錯資訊**debugSetting**項目。

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


## <a name="create-a-troubleshooting-template"></a>建立疑難排解範本
在某些情況下，hello 最簡單的方式 tootroubleshoot 您的範本是 tootest 部分。 您可以建立可讓您簡化的範本 toofocus，您認為造成 hello 錯誤的 hello 組件上。 例如，假設您在參考資源時收到錯誤。 而不是處理整個的範本時，建立範本，可傳回 hello 一部分可能會造成您的問題。 它可協助您判斷是否您將傳入 hello 正確的參數，正確地使用樣板函式，而您收到 hello 資源預期。

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

或者，假設您遇到您認為 tooincorrectly 設定相依性相關的部署錯誤。 將其細分為簡化範本以測試您的範本。 首先，建立可部署單一資源 (例如 SQL Server) 的範本。 當您確定已正確定義該資源時，加入依存該資源的資源 (例如 SQL Database)。 當您正確定義這兩個資源時，加入其他相依的資源 (例如稽核原則)。 每個測試部署，之間刪除 hello 資源群組 toomake 確定您可以充分地測試 hello 相依性。 

## <a name="check-deployment-sequence"></a>檢查部署順序

當資源是以非預期的順序部署時，會發生許多部署錯誤。 相依性未正確設定時，就會發生這些錯誤。 當您遺漏所需的相依性時，一項資源會嘗試的 toouse 尚未存在另一個資源，但其他 hello 的值。 您會收到錯誤表示找不到資源。 可能會遇到這種類型的錯誤或間歇性因為 hello 部署時間，每個資源而有所不同。 例如，第一次的嘗試 toodeploy 資源成功，因為有項必要的資源隨機完成的時間。 不過，您的第二次嘗試會失敗，因為 hello 所需的資源未完成的時間。 

但是，您希望不需 tooavoid 設定相依性。 當您有不必要的相依性時，您便會延長 hello hello 部署期間，防止不以平行方式部署彼此相依的資源。 此外，您可以建立封鎖 hello 部署的循環相依性。 hello[參考](resource-group-template-functions-resource.md#reference)函式會建立隱含的相依性參考 hello 資源中 hello 部署該資源時相同的範本。 因此，您可能需要比 hello hello 中指定的相依性的多個相依性**dependsOn**屬性。 hello [resourceId](resource-group-template-functions-resource.md#resourceid)函式不會建立隱含的相依性或驗證 hello 資源已存在。

當您遇到相依性問題時，您會需要 toogain 深入了解資源部署的 hello 順序。 tooview hello 順序的部署作業：

1. 選取資源群組的 hello 部署歷程記錄。

   ![選取部署歷程記錄](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. 從 hello 歷程記錄中，選取任一部署，然後選取**事件**。

   ![選取部署事件](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. 檢查 hello 一連串的每個資源的事件。 請注意 toohello 狀態，每個作業。 例如，hello 下圖顯示三個部署的儲存體帳戶以平行方式。 請注意，hello 三個儲存體帳戶在 hello 啟動相同的時間。

   ![平行部署](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   hello 下一個影像會顯示尚未部署的三個儲存體帳戶，以平行方式。 hello 第二個儲存體帳戶取決於 hello 第一個儲存體帳戶，以及第三個儲存體帳戶 hello 取決於 hello 第二個儲存體帳戶。 因此，hello 第一個儲存體帳戶啟動、 接受，及接下來啟動 hello 之前完成。

   ![連續部署](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

即使對於更複雜的情況，您可以使用 hello 相同的技巧 toodiscover 時啟動及完成的每個資源部署。 如果 hello 順序不會比預期不同，請查看您的部署事件 toosee。 若是如此，重新評估 hello 這個資源的相依性。

Resource Manager 範本會在驗證期間識別循環相依性。 它會傳回錯誤訊息，特別指出循環相依性存在。 toosolve 循環相依性：

1. 在範本中，尋找 hello hello 循環相依性中所識別的資源。 
2. 該資源中，檢查 hello **dependsOn**屬性和任何使用 hello**參考**函式的 toosee 它相依於哪些資源。 
3. 檢查哪些資源它們依存這些資源 toosee。 您會注意到相依於 hello 原始資源的資源之前，請遵循 hello 相依性。
5. 如需 hello 資源參與 hello 循環相依性，仔細檢查所有使用 hello **dependsOn**屬性 tooidentify 不需要任何相依性。 移除這些相依性。 如果您不確定是否需要某個相依性，請嘗試移除它。 
6. 重新部署 hello 範本。

移除值從 hello **dependsOn**屬性可能會導致錯誤，當您部署的 hello 範本。 如果您遇到錯誤時，新增回 hello 範本 hello 相依性。 

如果該方法無法解決 hello 循環相依性，請考慮將您的部署邏輯的一部分移到子資源 （例如擴充功能或組態設定）。 設定這些子資源 toodeploy 之後所涉及的 hello 循環相依性的 hello 資源。 例如，假設您要部署兩部虛擬機器，但您必須設定，請參閱 toohello 其他每一個屬性。 您可以將它們部署在 hello 順序：

1. vm1
2. vm2
3. vm1 的擴充相依於 vm1 和 vm2。 hello 延伸模組設定 vm1 它 vm2 從取得的值。
4. vm2 的擴充相依於 vm1 和 vm2。 hello 延伸模組設定 vm2 它 vm1 從取得的值。

hello 相同的方法適用於 App Service 應用程式。 請考慮將組態值移到 hello 應用程式資源的子資源。 您可以部署在 hello 順序中的兩個 web 應用程式：

1. webapp1
2. webapp2
3. webapp1 的設定相依於 webapp1 和 webapp2。 它包含使用 webapp2 的值的應用程式設定。
4. webapp2 的設定相依於 webapp1 和 webapp2。 它包含使用 webapp1 的值的應用程式設定。


## <a name="next-steps"></a>後續步驟
* 解決方式 toocommon 部署錯誤，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。
* toolearn 有關稽核的動作，請參閱[稽核與資源管理員作業](resource-group-audit.md)。
* toolearn 有關動作 toodetermine hello 錯誤，在部署期間，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。
