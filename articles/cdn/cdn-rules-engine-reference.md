---
title: "aaaAzure CDN 規則引擎參考 |Microsoft 文件"
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
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Azure CDN 規則引擎
本主題列出的詳細的描述 hello 可比對條件和功能的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。

hello HTTP 規則引擎已設計的 toobe hello 最終授權單位上如何特定類型的要求處理 hello CDN。

**常見用途**：

- 覆寫或定義自訂快取原則。
- 保護或拒絕機密內容的要求。
- 將要求重新導向。
- 儲存自訂記錄檔資料。

## <a name="terminology"></a>術語
藉由使用 hello 定義規則[**條件運算式**](cdn-rules-engine-reference-conditional-expressions.md)， [**符合**](cdn-rules-engine-reference-match-conditions.md)，和[ **功能**](cdn-rules-engine-reference-features.md)。 這些項目會在 hello 遵循圖中反白顯示。

 ![CDN 相符條件](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>語法

相應 toohow 相符或功能的控制代碼的文字值，會將用來處理特殊字元的 hello 方式各不相同。 比對條件或功能，可能會將解譯其中一種下列方法的 hello 文字：

1. [**常值**](#literal-values) 
2. [**萬用字元值**](#wildcard-values)
3. [**規則運算式**](#regular-expressions)

### <a name="literal-values"></a>常值
解譯為常值的文字會將所有的特殊字元，與 hello 例外狀況的 hello %符號，視為 hello 值必須符合的一部分。 換句話說，常值符合條件設定得`\'*'\`只而得以滿足時，確切的值 (亦即， `\'*'\`) 找到。
 
百分比符號是使用的 tooindicate URL 編碼方式 (例如`%20`)。

### <a name="wildcard-values"></a>萬用字元值
文字會解譯為萬用字元值，將會指派額外的意義 toospecial 字元。 hello 下表描述 hello 遵循一組字元解譯的方式。

Character | 說明
----------|------------
\ | 使用的 tooescape hello 字元指定此資料表中的反斜線。 Hello 應該逸出的特殊字元必須先指定直接反斜線。<br/>例如，請使用下列語法的 hello 逸出星號：`\*`
% | 百分比符號是使用的 tooindicate URL 編碼方式 (例如`%20`)。
* | 星號為萬用字元，表示一或多個字元。
空白字元 | 空格字元，表示可能會透過其中一種指定 hello 中滿足比對條件值或模式。
'value' | 單引號不具有特殊意義。 不過，會使用一組單引號 tooindicate 值應該被視為常值。 它可以用於下列方式 hello:<br><br/>-它可讓比對條件 toobe 滿足只要 hello 指定的值符合 hello 比較值的任何部分。  例如，`'ma'`會符合任何 hello 下列字串： <br/><br/>/business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/business/template.**ma**p<br /><br />-它可讓特殊字元 toobe 指定為常值字元。 例如，您可以指定常值空白字元，方法是在單引號組內括住空白字元 (亦即，`' '` 或 `'sample value'`)。<br/>-它可讓指定空白值 toobe。 藉由指定單引號組來指定空白值 (亦即，'')。<br /><br/>**重要事項：**<br/>-如果 hello 指定值不包含萬用字元，然後它會自動被視為常值。 這表示它不是必要的 toospecify 方以單引號包住一組。<br/>- 如果反斜線不會逸出此資料表中的另一個字元，則它將會在於單引號組內指定時被忽略。<br/>為另一個方式 toospecify 做常值字元的特殊字元是 tooescape 使用反斜線 (亦即， `\`)。

### <a name="regular-expressions"></a>規則運算式

規則運算式會定義要在文字值中搜尋的模式。 規則運算式標記法定義特定的意義 tooa 各種不同的符號。 hello 下表指出如何特殊字元都會被比對條件和支援規則運算式的功能。

特殊字元 | 說明
------------------|------------
\ | 反斜線逸出 hello 字元 hello 在它後面。 這會導致視為常值的值，而不會採取其規則運算式的意義上該字元 toobe。 例如，請使用下列語法的 hello 逸出星號：`\*`
% | 百分比符號的 hello 意義取決於其使用情形。<br/><br/> `%{HTTPVariable}`︰這個語法會識別 HTTP 變數。<br/>`%{HTTPVariable%Pattern}`： 這個語法會使用百分比符號 tooidentify HTTP 變數以及做為分隔符號。<br />`\%`： 逸出的百分比符號可讓它 toobe 做為常值或 tooindicate URL 編碼 (例如`\%20`)。
* | 星號允許 hello 前置字元 toobe 比對零或多次。 
空白字元 | 空白字元通常會被視為常值字元。 
'value' | 單引號會被視為常值字元。 單引號組不具有特殊意義。


## <a name="next-steps"></a>後續步驟
* [規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)
* [規則引擎條件運算式](cdn-rules-engine-reference-conditional-expressions.md)
* [規則引擎功能](cdn-rules-engine-reference-features.md)
* [覆寫使用 hello 規則引擎的預設 HTTP 行為](cdn-rules-engine.md)
* [Azure CDN 概觀](cdn-overview.md)
