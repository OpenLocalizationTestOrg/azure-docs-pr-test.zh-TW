---
title: "aaaAzure 非同步作業 |Microsoft 文件"
description: "描述如何在 Azure 中的 tootrack 非同步作業。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>追蹤非同步 Azure 作業
某些 Azure REST 作業，以非同步方式執行，因為 hello 作業無法完成快速。 本主題描述如何 hello 回應中傳回 tootrack hello 非同步作業狀態的值。  

## <a name="status-codes-for-asynchronous-operations"></a>非同步作業的狀態碼
非同步作業最初會傳回下列其中一個 HTTP 狀態碼︰

* 201 (已建立)
* 202 (已接受) 

當 hello 作業成功完成時，它會傳回：

* 200 (確定)
* 204 (沒有內容) 

請參閱 toohello [REST API 文件](/rest/api/)toosee hello 回應 hello 作業正在執行。 

## <a name="monitor-status-of-operation"></a>監視作業的狀態
hello 非同步 REST 作業傳回的標頭的值，您使用 toodetermine hello 狀態 hello 作業。 可能有三個標頭值 tooexamine:

* `Azure-AsyncOperation`-URL 檢查 hello hello 作業進行中的狀態。 如果您的作業會傳回此值，請一律使用 hello 作業 （而不是位置） 的 it tootrack hello 狀態。
* `Location` - 用於判斷作業何時完成的 URL。 只在未傳回 Azure-AsyncOperation 時才使用此值。
* `Retry-After`-hello 檢查 hello hello 非同步作業的狀態之前的秒數 toowait 數目。

不過，並非每個非同步作業會傳回所有這些值。 例如，您可能需要 tooevaluate hello Azure AsyncOperation 標頭值的一項作業和另一個作業的 hello 位置標頭值。 

您會在擷取要求的任何標頭值，您可以擷取 hello 標頭值。 例如，在 C# 中，您要擷取的 hello 標頭值`HttpWebResponse`名為物件`response`以下列程式碼的 hello:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Azure-AsyncOperation 要求和回應

tooget hello 狀態 hello 非同步作業時，傳送 GET 要求 toohello URL Azure AsyncOperation 標頭值。

從這項作業的 hello 回應 hello 主體包含 hello 作業的相關資訊。 hello 下列範例顯示 hello hello 作業傳回的可能值：

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

所有回應只傳回 `status`。 當 hello 狀態為 Failed 或已取消，則會傳回 hello 物件時發生錯誤。 所有其他值均為選擇性;因此，您會收到 hello 回應可能看起來與 hello 範例不同。

## <a name="provisioningstate-values"></a>provisioningState 值

建立、更新或刪除資源的作業 (PUT、PATCH、DELETE) 通常會傳回 `provisioningState` 值。 當作業完成時會傳回下列三個值之一︰ 

* Succeeded
* Failed
* Canceled

所有其他值則表示 hello 作業仍在執行中。 hello 資源提供者可以傳回自訂的值，指出其狀態。 例如，您可能會收到**接受**hello 要求時接收並執行。

## <a name="example-requests-and-responses"></a>要求和回應範例

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>啟動虛擬機器 (202 與 Azure-AsyncOperation)
這個範例會示範如何 toodetermine hello 狀態**啟動**虛擬機器的作業。 hello 初始要求是下列格式的 hello:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

它傳回狀態碼 202。 在 hello 標頭值，您會看到：

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

toocheck hello hello 非同步作業，傳送另一個要求 toothat URL 的狀態。

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

hello 回應主體會包含 hello hello 作業狀態：

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>部署資源 (201 與 Azure-AsyncOperation)

這個範例會示範如何 toodetermine hello 狀態**部署**部署資源 tooAzure 的作業。 hello 初始要求是下列格式的 hello:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

它傳回狀態碼 201。 hello 回應 hello 主體包括：

```json
"provisioningState":"Accepted",
```

在 hello 標頭值，您會看到：

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

toocheck hello hello 非同步作業，傳送另一個要求 toothat URL 的狀態。

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

hello 回應主體會包含 hello hello 作業狀態：

```json
{"status":"Running"}
```

Hello 部署完成時，包含回應 hello:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>建立儲存體帳戶 (202 與 Location 和 Retry-After)

這個範例會示範如何 toodetermine hello 的 hello 狀態**建立**儲存體帳戶的作業。 hello 初始要求是下列格式的 hello:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

和 hello 要求主體包含 hello 儲存體帳戶屬性：

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

它傳回狀態碼 202。 在 hello 標頭值，您會看到下列兩個值的 hello:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

之後等候數秒指定在重試之後，傳送給另一個要求 toothat URL 檢查 hello hello 非同步作業的狀態。

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

如果 hello 要求仍在執行中，您會收到狀態碼 202。 如果 hello 要求已完成，您會收到狀態碼 200，並 hello 回應 hello 主體包含 hello 已建立的儲存體帳戶的 hello 屬性。

## <a name="next-steps"></a>後續步驟

* 如需每個 REST 作業的相關文件，請參閱 [REST API 文件](/rest/api/)。
* 管理透過 hello 資源管理員 REST API 資源的相關資訊，請參閱[使用 hello 資源管理員 REST API](resource-manager-rest-api.md)。
* 部署範本，透過 hello 資源管理員 REST API 的相關資訊，請參閱[部署具有資源管理員範本和資源管理員 REST API 資源](resource-group-template-deploy-rest.md)。
