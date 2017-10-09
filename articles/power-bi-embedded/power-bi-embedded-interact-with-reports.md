---
title: "搭配報表使用 hello JavaScript API 的 aaaInteract |Microsoft 文件"
description: "Power BI Embedded，與使用 hello JavaScript API 的報表互動"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>使用 hello JavaScript API 的 Power BI 報表與互動
hello Power BI JavaScript API 可讓您 tooeasily Power BI 報表內嵌到應用程式。 以 hello API，您的應用程式以程式設計的方式可以與不同的報表元素，例如分頁和篩選互動。 此互動功能可讓 Power BI 報告更能夠融合到您的應用程式中。

應用程式中內嵌 Power BI 報表時，您使用 iframe 裝載 hello 應用的一部分。 hello iframe 做為您的應用程式與 hello 報表之間的界限，為您可以在下列映像的 hello 中看到。 

![不具 JavaScript API 的 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

hello iframe hello 內嵌程序中來得簡單許多，但是沒有 hello JavaScript API hello 報表和應用程式無法彼此互動。 這種欠缺的互動功能，可讓覺得 hello 報表不全然 hello 應用程式的一部分。 hello 報表和應用程式真的需要 toocommunicate 來回，如 hello 下列影像所示。

![具有 JavaScript API 的 Power BI Embedded iframe](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

hello Power BI JavaScript API，可讓您可以安全地通過 hello iframe 界限 toowrite 程式碼。 這樣做可讓您的應用程式 tooprogrammatically 報表和來自使用者 hello 報表內進行的動作事件 toolisten 中執行的動作。

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>您可以使用 Power BI JavaScript API hello 做什麼？
以 hello JavaScript API 可以管理報表、 瀏覽報表中的 toopages、 篩選報表，和處理內嵌事件。 hello 下列圖表顯示 hello API hello 結構。

![Power BI JavaScript API 圖表](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>管理報告
hello Javascript 應用程式開發介面可讓您在 hello 報表和頁面層級 toomanage 行為：

* 安全地將特定的 Power BI 報表內嵌在您的應用程式-請嘗試 hello[內嵌示範應用程式](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * 設定存取權杖
* Hello 報表設定
  * 啟用和停用 hello 篩選 窗格和頁面導覽窗格-重試 hello[更新示範應用程式中設定](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * 設定網頁及篩選器的預設值-重試 hello[組預設值示範](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* 進入或離開全螢幕模式

[深入了解內嵌報告](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>瀏覽報表中的 toopages
hello JavaScript API enbales 所有的您 toodiscover 報表和 tooset hello 目前頁面中的分頁。 再試一次 hello[示範應用程式中瀏覽](http://azure-samples.github.io/powerbi-angular-client/#/scenario3)。

[深入了解頁面瀏覽](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>篩選報告
hello JavaScript 應用程式開發介面會提供基本和進階篩選的內嵌的報表和報表頁面的功能。 再試一次 hello[篩選示範應用程式](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)，並檢閱一些基本的程式碼。  

#### <a name="basic-filters"></a>基本篩選器
基本篩選放置在資料行或階層層級，並包含的值 tooinclude 」 或 「 排除清單。

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>進階篩選器
進階篩選器使用 hello 邏輯運算子或 OR，而且接受一個或兩個條件，每個都有自己的運算子和值。 支援的條件如下︰

* None
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contains
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[深入了解篩選](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>錯誤事件
此外 hello iframe toosending 資訊，您的應用程式也可以接收 hello 下列來自 hello iframe 的事件的詳細資訊：

* 內嵌
  * 已載入
  * 錯誤
* 報告
  * pageChanged
  * dataSelected (敬請期待)

[深入了解處理事件](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>後續步驟
如需 hello Power BI JavaScript API 的詳細資訊，請參閱下列連結查看 hello:

* [JavaScript API Wiki](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [物件模型參考](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* 範例
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [實況示範](https://microsoft.github.io/PowerBI-JavaScript/demo/)

