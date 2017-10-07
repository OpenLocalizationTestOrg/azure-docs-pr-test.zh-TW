---
title: "aaaAzure CDN 規則引擎的條件運算式 |Microsoft 文件"
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
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Azure CDN 規則引擎條件運算式
本主題列出的詳細的描述 hello 條件運算式的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。

規則 hello 第一個部分是 hello 條件運算式。

條件運算式 | 說明
-----------------------|-------------
IF | 如果運算式永遠是 hello 規則中的第一個陳述式的一部分。 像所有其他條件運算式一樣，此 IF 陳述式必須與符合項目相關聯。 如果不定義了任何額外的條件運算式，這個比對會決定一組功能可能會套用的 tooa 要求之前，必須符合的 hello 準則。
AND IF | 表示運算式只能加入下列類型的條件運算式： 如果，表示 hello 之後。 就表示另一個 hello 初始 IF 陳述式必須符合的條件。
ELSE IF| ELSE IF 運算式指定的替代進行一組功能特定 toothis ELSE 的 IF 陳述式之前必須符合的條件。 hello 存在 ELSE 的 IF 陳述式表示 hello hello 前一個陳述式結尾。 可能會放在 ELSE 的 IF 陳述式之後的 hello 只有條件式運算式是另一個 ELSE IF 陳述式。 這表示 ELSE 的 IF 陳述式只可以使用的 toospecify 單一具有 toobe 符合其他條件。

**範例**：![CDN 相符條件](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > 後續的規則可能會覆寫先前規則所指定的 hello 動作。 範例︰全面涵蓋規則會保護所有透過以權杖為基礎的驗證要求。 另一個規則可能會建立它的下方 toomake 某些類型的要求的例外狀況。

### <a name="next-steps"></a>後續步驟
* [Azure CDN 概觀](cdn-overview.md)
* [規則引擎參考](cdn-rules-engine-reference.md)
* [規則引擎比對條件](cdn-rules-engine-reference-match-conditions.md)
* [規則引擎功能](cdn-rules-engine-reference-features.md)
* [覆寫使用 hello 規則引擎的預設 HTTP 行為](cdn-rules-engine.md)
