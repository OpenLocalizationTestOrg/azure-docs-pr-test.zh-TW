---
title: "aaaAzure 計費企業應用程式開發介面的使用方式詳細資料 |Microsoft 文件"
description: "深入了解 Azure 計費的使用量與 RateCard Api，也就是使用的 tooprovide 深入了解 Azure 資源耗用量和趨勢。"
services: 
documentationcenter: 
author: aedwin
manager: aedwin
editor: 
tags: billing
ms.assetid: 3e817b43-0696-400c-a02e-47b7817f9b77
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 04/25/2017
ms.author: aedwin
ms.openlocfilehash: def0805008261df5872f015db3d2b26e47d25569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-apis-for-enterprise-customers---usage-details"></a>適用於企業客戶的報告 API - 使用量詳細資料

hello 使用量詳細資料 API 提供已使用的數量和所註冊的估計的費用的每日明細。 hello 結果也會包含有關執行個體、 公尺和部門。 您可以查詢 hello API，計費週期或指定的開始和結束日期。 
## <a name="consumption-apis"></a>使用情況 API


##<a name="request"></a>要求 
指定需要 toobe 加入通用標頭屬性[這裡](billing-enterprise-api.md)。 如果未指定計費期間內，則資料 hello 目前計費週期內會傳回。 自訂時間範圍可以指定與 hello 開始和結束日期參數中 hello 格式為 yyyy-mm-dd hello 最大支援的時間範圍為 36 個月。  

|方法 | 要求 URI|
|-|-|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetails 
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/billingPeriods/{billingPeriod}/usagedetails|
|GET|https://consumption.azure.com/v2/enrollments/{enrollmentNumber}/usagedetailsbycustomdate?startTime=2017-01-01&endTime=2017-01-10|

> [!Note]
> toouse hello 預覽版 API，取代 v2 v1 hello 上述 URL 中。
>

## <a name="response"></a>Response

> 因為 toohello 可能的大型磁碟區資料 hello 結果的分頁集合。 hello nextLink 屬性，如果有的話，會指定 hello hello 下一頁資料的連結。 如果 hello 連結是空的它代表的是 hello 最後一頁。 
<br/>

    {
        "id": "string",
        "data": [
            {                       
            "accountId": 0,
            "productId": 0,
            "resourceLocationId": 0,
            "consumedServiceId": 0,
            "departmentId": 0,
            "accountOwnerEmail": "string",
            "accountName": "string",
            "serviceAdministratorId": "string",
            "subscriptionId": 0,
            "subscriptionGuid": "string",
            "subscriptionName": "string",
            "date": "2017-04-27T23:01:43.799Z",
            "product": "string",
            "meterId": "string",
            "meterCategory": "string",
            "meterSubCategory": "string",
            "meterRegion": "string",
            "meterName": "string",
            "consumedQuantity": 0,
            "resourceRate": 0,
            "Cost": 0,
            "resourceLocation": "string",
            "consumedService": "string",
            "instanceId": "string",
            "serviceInfo1": "string",
            "serviceInfo2": "string",
            "additionalInfo": "string",
            "tags": "string",
            "storeServiceIdentifier": "string",
            "departmentName": "string",
            "costCenter": "string",
            "unitOfMeasure": "string",
            "resourceGroup": "string"
            }
        ],
        "nextLink": "string"
    }

<br/>
**回應屬性定義**

|屬性名稱| 類型| 說明
|-|-|-|
|id| 字串| hello hello API 呼叫的唯一識別碼。 |
|data| JSON 陣列| hello 陣列的每個 instance\meter 每日使用量詳細資料。|
|nextLink| 字串| 當有更多頁面資料 hello nextLink 點 toohello URL tooreturn hello 下一頁資料。 |
|accountId| int| 已淘汰的欄位。 之所以顯示是為了提供回溯相容性。 |
|productId| int| 已淘汰的欄位。 之所以顯示是為了提供回溯相容性。 |
|resourceLocationId| int| 已淘汰的欄位。 之所以顯示是為了提供回溯相容性。 |
|consumedServiceID| int| 已淘汰的欄位。 之所以顯示是為了提供回溯相容性。 |
|departmentId| int| 已淘汰的欄位。 之所以顯示是為了提供回溯相容性。 |
|accountOwnerEmail| 字串| Hello 帳戶擁有者的電子郵件帳戶。 |
|accountName| 字串| 輸入客戶 hello 帳戶名稱。 |
|serviceAdministratorId| 字串| 服務系統管理員的電子郵件地址。 |
|subscriptionId| int| 已淘汰的欄位。 之所以顯示是為了提供回溯相容性。 |
|subscriptionGuid| 字串| Hello 訂用帳戶的全域唯一識別碼。 |
|subscriptionName| 字串| Hello 訂用帳戶的名稱。 |
|日期| 字串| hello 耗用量發生的日期。 |
|product| 字串| Hello 計量表上的其他詳細資料。 範例：A1(VM)Windows - 亞太地區東部|
|meterId| 字串| hello 發出使用量 hello 計量表的識別碼。 |
|meterCategory| 字串| hello Azure 平台使用的服務。 |
|meterSubCategory| 字串| 定義可能會影響 hello 速率的 hello Azure 服務類型。 範例：A1 VM (非 Windows)|
|meterRegion| 字串| 識別 hello 資料中心位置為基礎的價格特定服務的 hello 資料中心位置。 |
|meterName| 字串| Hello 計量表的名稱。 |
|consumedQuantity| double| hello hello 計量表已耗用的數量。 |
|resourceRate| double| hello 速率適用每個計費單位。 |
|cost| double| hello 具有已 hello 計量表所產生的費用。 |
|resourceLocation| 字串| 識別 hello hello 計量器執行所在的資料中心。 |
|consumedService| 字串| hello Azure 平台使用的服務。 |
|instanceId| 字串| 這個識別碼是 hello hello 資源名稱或 hello 完整資源 id。 如需詳細資訊，請參閱 [Azure Resource Manager API](https://docs.microsoft.com/rest/api/resources/resources) |
|serviceInfo1| 字串| 內部的 Azure 服務中繼資料。 |
|serviceInfo2| 字串| 例如，虛擬機器的映像類型和 ExpressRoute 的 ISP 名稱。 |
|additionalInfo| 字串| 服務專屬的中繼資料。 例如，虛擬機器的影像類型。 |
|tags| 字串| 客戶已新增的標記。 如需詳細資訊，請參閱[使用標記組織您的 Azure 資源](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-using-tags)。 |
|storeServiceIdentifier| 字串| 不會使用這個資料行。 之所以顯示是為了提供回溯相容性。 |
|departmentName| 字串| Hello 部門的名稱。 |
|costCenter| 字串| hello 使用量相關聯的 hello 成本中心。 |
|unitOfMeasure| 字串| 識別 hello 服務負責中的 hello 單位。 範例：GB、小時、10,000 秒。 |
|resourceGroup| 字串| hello 資源群組中的 hello 已部署的計量器正在執行中。 如需詳細資訊，請參閱 [Azure Resource Manager 概觀](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。 |
<br/>
## <a name="see-also"></a>另請參閱

* [計費週期 API](billing-enterprise-api-billing-periods.md)

* [餘額與摘要 API](billing-enterprise-api-balance-summary.md)

* [Marketplace 市集費用 API](billing-enterprise-api-marketplace-storecharge.md) 

* [價位表 API](billing-enterprise-api-pricesheet.md)
