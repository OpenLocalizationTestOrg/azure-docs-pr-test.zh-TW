---
title: "Azure CDN 規則引擎參考 | Microsoft Docs"
description: "Azure CDN 規則引擎比對條件和功能的參考文件。"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10145661a8c575381493c9aaa901c3ef92c2e81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine"></a>Azure CDN 規則引擎
本主題會針對 Azure 內容傳遞網路 (CDN) [規則引擎](cdn-rules-engine.md)列出可用比對條件和功能的詳細說明。

HTTP 規則引擎是設計為特定類型要求如何由 CDN 處理的最終授權。

**常見用途**：

- 覆寫或定義自訂快取原則。
- 保護或拒絕機密內容的要求。
- 將要求重新導向。
- 儲存自訂記錄檔資料。

## <a name="terminology"></a>術語
規則是透過使用[**條件運算式**](cdn-rules-engine-reference-conditional-expressions.md)、[**比對**](cdn-rules-engine-reference-match-conditions.md)和[**功能**](cdn-rules-engine-reference-features.md)定義。 這些元素會在下圖中反白顯示。

 ![CDN 相符條件](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>語法

處理特殊字元的方式會根據比對條件或功能如何處理文字值而異。 比對條件或功能可能會以下列其中一種方式解譯文字︰

1. [**常值**](#literal-values) 
2. [**萬用字元值**](#wildcard-values)
3. [**規則運算式**](#regular-expressions)

### <a name="literal-values"></a>常值
解譯為常值的文字會將所有特殊字元 (除了 % 符號之外)，視為必須符合值的一部分。 換句話說，常值比對條件設定為 `\'*'\`，只會在找到確切值時 (亦即，`\'*'\`) 獲得滿足。
 
百分比符號是用來表示 URL 編碼 (例如 `%20`)。

### <a name="wildcard-values"></a>萬用字元值
解譯為萬用字元值的文字會將額外意義指派給特殊字元。 下表描述如何解譯下列字元集。

Character | 說明
----------|------------
\ | 反斜線是用來逸出此資料表中指定的任何字元。 必須在逸出特殊字元之前指定反斜線。<br/>例如，下列語法逸出星號︰`\*`
% | 百分比符號是用來表示 URL 編碼 (例如 `%20`)。
* | 星號為萬用字元，表示一或多個字元。
空白字元 | 空白字元，表示比對條件可能藉由指定值或模式獲得滿足。
'value' | 單引號不具有特殊意義。 不過，單引號組是用來表示值應視為常值。 使用方式如下：<br><br/>- 它可讓比對條件在指定值符合比較值的任何部分時獲得滿足。  例如，`'ma'` 會比對下列任何字串︰ <br/><br/>/business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/business/template.**ma**p<br /><br />- 它可讓特殊字元指定為常值字元。 例如，您可以指定常值空白字元，方法是在單引號組內括住空白字元 (亦即，`' '` 或 `'sample value'`)。<br/>- 它可以指定空白值。 藉由指定單引號組來指定空白值 (亦即，'')。<br /><br/>**重要事項：**<br/>- 如果指定值不包含萬用字元，則它會自動被視為常值。 這表示不需要指定單引號組。<br/>- 如果反斜線不會逸出此資料表中的另一個字元，則它將會在於單引號組內指定時被忽略。<br/>- 另一種將特殊字元指定為常值字元的方式是使用反斜線逸出它 (亦即，`\`)。

### <a name="regular-expressions"></a>規則運算式

規則運算式會定義要在文字值中搜尋的模式。 規則運算式標記法會將特定意義定義為各種符號。 下表指出支援規則運算式的比對條件和功能如何處理特殊字元。

特殊字元 | 說明
------------------|------------
\ | 反斜線會逸出它後面接續的字元。 這會導致該字元被視為常值，而非採用它的規則運算式的意義。 例如，下列語法逸出星號︰`\*`
% | 百分比符號的意義取決於其使用方式。<br/><br/> `%{HTTPVariable}`︰這個語法會識別 HTTP 變數。<br/>`%{HTTPVariable%Pattern}`︰這個語法會使用百分比符號來識別 HTTP 變數，並做為分隔符號。<br />`\%`︰逸出百分比符號可以讓它可用來做為常值，或表示 URL 編碼 (例如 `\%20`)。
* | 星號可讓前置字元比對零或多次。 
空白字元 | 空白字元通常會被視為常值字元。 
'value' | 單引號會被視為常值字元。 單引號組不具有特殊意義。


## <a name="next-steps"></a>後續步驟
* [規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)
* [規則引擎條件運算式](cdn-rules-engine-reference-conditional-expressions.md)
* [規則引擎功能](cdn-rules-engine-reference-features.md)
* [使用規則引擎覆寫預設的 HTTP 行為](cdn-rules-engine.md)
* [Azure CDN 概觀](cdn-overview.md)
