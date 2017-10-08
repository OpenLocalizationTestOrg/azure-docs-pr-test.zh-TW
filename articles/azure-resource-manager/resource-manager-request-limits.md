---
title: "aaaAzure 資源管理員要求限制 |Microsoft 文件"
description: "描述如何 toouse 節流設定與 Azure 資源管理員要求到達訂用帳戶的限制。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>對 Resource Manager 要求進行節流
每個訂用帳戶和租用戶，資源管理員限制要求 too15，每小時 000 讀寫要求 too1，每小時 200。 這些限制適用於 tooeach Azure 資源管理員執行個體。在每個 Azure 區域中，有多個執行個體和 Azure 資源管理員是已部署的 tooall Azure 區域。  因此，實際上的限制比上面列出的還要高，因為通常是由多個不同的執行個體來服務使用者要求。

如果您的應用程式或指令碼已達到這些限制，您需要 toothrottle 您的要求。 本主題說明如何 toodetermine hello 剩餘要求您必須先到達 hello 限制以及如何 toorespond 時已達到 hello 上限。

當您到達 hello 限制時，您會收到 hello HTTP 狀態碼**429 太多要求**。

hello 的要求數目是限定範圍的 tooeither 訂用帳戶或您的租用戶。 如果您有多個，並行的應用程式提出要求，在您的訂用帳戶，來自這些應用程式的 hello 要求加在一起 toodetermine hello 數目其餘要求。

訂用帳戶範圍要求為 hello 牽涉到將您的訂用帳戶識別碼，例如擷取您的訂用帳戶中的 hello 資源群組。 受租用戶限制的要求則未包含訂用帳戶識別碼，例如擷取有效的 Azure 位置。

## <a name="remaining-requests"></a>剩餘的要求
您可以藉由檢查回應標頭判斷 hello 剩餘的要求數目。 每個要求包含 hello 剩餘的讀取和寫入要求數目的值。 hello 下表描述您可以檢查這些值為 hello 回應標頭：

| 回應標頭 | 說明 |
| --- | --- |
| x-ms-ratelimit-remaining-subscription-reads |受訂用帳戶限制的剩餘讀取 |
| x-ms-ratelimit-remaining-subscription-writes |受訂用帳戶限制的剩餘寫入 |
| x-ms-ratelimit-remaining-tenant-reads |受租用戶限制的剩餘讀取 |
| x-ms-ratelimit-remaining-tenant-writes |受租用戶限制的剩餘寫入 |
| x-ms-ratelimit-remaining-subscription-resource-requests |受訂用帳戶限制的剩餘資源類型要求。<br /><br />如果服務已覆寫 hello 預設限制，才會傳回此標頭值。 資源管理員會加入此值，而非 hello 訂用帳戶的讀取或寫入。 |
| x-ms-ratelimit-remaining-subscription-resource-entities-read |受訂用帳戶限制的剩餘資源類型集合要求。<br /><br />如果服務已覆寫 hello 預設限制，才會傳回此標頭值。 此值會提供其餘集合要求 （清單資源） 的 hello 數目。 |
| x-ms-ratelimit-remaining-tenant-resource-requests |受租用戶限制的剩餘資源類型要求。<br /><br />此標頭只會加入租用戶層級的要求，而且只有當服務已覆寫 hello 預設限制。 資源管理員會加入此值，而非 hello 租用戶讀取或寫入。 |
| x-ms-ratelimit-remaining-tenant-resource-entities-read |受租用戶限制的剩餘資源類型集合要求。<br /><br />此標頭只會加入租用戶層級的要求，而且只有當服務已覆寫 hello 預設限制。 |

## <a name="retrieving-hello-header-values"></a>擷取 hello 標頭值
在程式碼或指令碼中擷取這些標頭值與擷取任何標頭值並無不同。 

例如，在**C#**，擷取的 hello 標頭值**HttpWebResponse**名為物件**回應**以下列程式碼的 hello:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

在**PowerShell**，Invoke-webrequest 作業中擷取 hello 標頭值。

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

或者，如果想 toosee hello 剩餘要求進行偵錯，您可以提供 hello **-偵錯**參數上的您**PowerShell** cmdlet。

```powershell
Get-AzureRmResourceGroup -Debug
```

它會傳回許多值，包括下列回應值的 hello:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

在**Azure CLI**，您可以使用擷取 hello 標頭值 hello 更多詳細資料的選項。

```azurecli
azure group list -vv --json
```

它會傳回許多值，包括下列物件的 hello:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>在傳送下一個要求前先稍候
當您到達 hello 要求限制時，資源管理員會傳回 hello **429** HTTP 狀態碼和**後重試**hello 標頭中的值。 hello**後重試**值傳送嗨下一個要求之前，先指定您的應用程式應等待的秒 （或睡眠） 的 hello 數目。 如果經過 hello 重試值之前，您就會傳送要求，則不會處理您的要求，並傳回新的重試值。

## <a name="next-steps"></a>後續步驟

* 如需有關限制和配額的詳細資訊，請參閱 [Azure 訂用帳戶和服務限制、配額及條件約束](../azure-subscription-service-limits.md)。
* toolearn 需處理非同步 REST 要求，請參閱[追蹤非同步的 Azure 作業](resource-manager-async-operations.md)。
