---
title: "aaaConstructing 篩選字串 hello 資料表設計工具的 |Microsoft 文件"
description: "建構篩選字串 hello 資料表設計工具"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>建構篩選字串 hello 資料表設計工具
## <a name="overview"></a>概觀
在 Azure 資料表中所顯示的 toofilter 資料 hello Visual Studio**資料表設計工具**，建構篩選字串，並將其輸入 hello 篩選欄位。 hello 篩選條件字串語法由 hello WCF 資料服務所定義且類似 tooa SQL WHERE 子句，但會傳送 toohello 表格服務透過 HTTP 要求。 hello**資料表設計工具**控點 hello 適當編碼方式，為您在想要的屬性值，因此 toofilter，您只需要輸入 hello 屬性的名稱、 比較運算子準則值，而且 hello 中的布林運算子來篩選 （選擇性）欄位。 您不需要 tooinclude hello $filter 查詢選項時您所建構 URL tooquery hello 資料表透過 hello[儲存體服務 REST API 參考](http://go.microsoft.com/fwlink/p/?LinkId=400447)。

hello WCF Data Services 根據 hello[開放式資料通訊協定](http://go.microsoft.com/fwlink/p/?LinkId=214805)(OData)。 如需詳細資訊，在 hello 篩選系統查詢選項 (**$filter**)，請參閱 hello [OData URI 轉換規格](http://go.microsoft.com/fwlink/p/?LinkId=214806)。

## <a name="comparison-operators"></a>比較運算子
hello 邏輯支援下列運算子的所有屬性類型：

| 邏輯運算子 | 說明 | 篩選字串範例 |
| --- | --- | --- |
| eq |等於 |City eq 'Redmond' |
| gt |大於 |Price gt 20 |
| ge |大於或等於太|Price ge 10 |
| lt |小於 |Price lt 20 |
| le |小於或等於 |Price le 100 |
| ne |不等於 |City ne 'London' |
| 和 |和 |Price le 200 and Price gt 3.5 |
| 或 |或 |Price le 3.5 or Price gt 200 |
| 否 |否 |not isAvailable |

建構篩選字串時，hello 下列規則很重要：

* 使用 hello 邏輯運算子 toocompare 屬性 tooa 值。 請注意，它不可能 toocompare 屬性 tooa 動態值。hello 運算式的一端必須是常數。
* Hello 篩選字串的所有部分都都區分大小寫的。
* hello hello 常值必須是相同的資料類型作為 hello 篩選 tooreturn 有效結果的順序中的 hello 屬性。 如需支援的屬性類型的詳細資訊，請參閱[了解 hello 表格服務資料模型](http://go.microsoft.com/fwlink/p/?LinkId=400448)。

## <a name="filtering-on-string-properties"></a>篩選字串屬性
當您篩選字串屬性時，請使用單引號括住 hello 字串常數。

hello hello 在下列範例會篩選**PartitionKey**和**RowKey**屬性，其他的非索引鍵屬性也可以加入 toohello 篩選字串：

    PartitionKey eq 'Partition1' and RowKey eq '00001'

您可以用括號括住每個篩選運算式 (雖然並非必要)：

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

請注意，hello 表格服務不支援萬用字元查詢中，不支援在 hello 資料表設計工具是。 不過，您可以執行比對的方式在 hello 想要的首碼使用比較運算子的前置詞。 hello 下列範例會傳回包含以 hello 字母 'A' 開頭的姓氏屬性的實體：

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>篩選數值屬性
toofilter 整數或浮點數，指定不加引號的 hello 數字。

這個範例會傳回與 Age 屬性的值大於 30 的所有實體：

    Age gt 30

這個範例會傳回具有 AmountDue 屬性且屬性值的所有實體小於或等於 too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>篩選布林值屬性
toofilter 布林值，指定**true**或**false**不需要引號。

hello 下列範例會傳回所有實體 hello IsActive 屬性設定的位置太**true**:

    IsActive eq true

您也可以撰寫此篩選條件運算式，不含 hello 邏輯運算子。 在下列範例的 hello，hello 表格服務也會傳回所有實體所在 IsActive **true**:

    IsActive

IsActive 所在位置為 false，您可以使用的所有實體不都 hello 的 tooreturn 運算子：

    not IsActive

## <a name="filtering-on-datetime-properties"></a>篩選 DateTime 屬性
toofilter 針對 DateTime 值，指定 hello **datetime**關鍵字，後面接著以單引號 hello 日期/時間常數。 中所述，hello 日期/時間常數必須是 UTC 組合格式，[格式化 DateTime 屬性值](http://go.microsoft.com/fwlink/p/?LinkId=400449)。

下列範例中的 hello 傳回實體其中 hello CustomerSince 屬性等於 tooJuly 10，2008年:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
