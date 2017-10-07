---
title: "在 Azure 資料目錄中的 aaaHow toodiscover 資料來源 |Microsoft 文件"
description: "本文章重點說明 toodiscover Azure 資料目錄，包括搜尋和篩選所註冊的資料資產，並使用 hello 叫用的 hello Azure 資料目錄入口網站的反白顯示功能。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: f72ae3a3-6573-4710-89a7-f13555e1968c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 624834b8895dd50c8931c9d3e6f8dc217927c617
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodiscover-data-sources-in-azure-data-catalog"></a>在 Azure 資料目錄中 toodiscover 資料來源的方式
## <a name="introduction"></a>簡介
Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料來源的註冊和探索系統。 換句話說，資料目錄可於協助人們探索、了解和使用資料來源，並可協助組織從現有的資料獲得更多價值。 資料來源以資料目錄註冊之後，它的中繼資料編製索引 hello 服務，您可以輕鬆地搜尋所需的 toodiscover hello 資料。

## <a name="searching-and-filtering"></a>搜尋和篩選
在資料目錄進行探索會使用兩種主要機制：搜尋和篩選。

搜尋是設計的 toobe 直覺式且功能強大。 根據預設，搜尋詞彙會比對 hello 類別目錄，包括使用者提供的註解中的任何內容。

篩選設計 toocomplement 搜尋。 您可以選取特定的特性，例如專家、資料來源類型、物件類型和標記。 您可以檢視只比對的資料資產，並限制搜尋結果 toomatching 資產。

藉由使用搜尋和篩選的組合，您可以快速瀏覽 hello 已經向您所需要的資料目錄 toodiscover hello 資料來源的資料來源。

## <a name="search-syntax"></a>搜尋語法
雖然 hello 預設任意文字搜尋是既簡單又直接，但是您也可以使用資料目錄搜尋語法的 hello 搜尋結果中較大的控制權。 下列技術資料類別目錄搜尋支援 hello:

| 技巧 | 使用 | 範例 |
| --- | --- | --- |
| 基本搜尋 |使用一或多個搜尋字詞的基本搜尋。 結果不符合任何屬性與一個或多個指定的 hello 詞彙任何資產。 |`sales data` |
| 屬性範圍 |只會與 hello 比對 hello 搜尋詞彙的傳回資料來源指定的屬性。 |`name:finance` |
| 布林運算子 |使用布林值作業擴大或縮小搜尋。 |`finance NOT corporate` |
| 使用括弧分組 |使用括號 toogroup 組件的 hello 查詢 tooachieve 邏輯隔離，尤其是在配合布林運算子。 |`name:finance AND (tags:Q1 OR tags:Q2)` |
| 比較運算子 |針對具有數值和日期資料類型的屬性使用比較而非相等。 |`modifiedTime > "11/05/2014"` |

如需有關資料類別目錄搜尋的詳細資訊，請參閱 hello [Azure 資料目錄](https://msdn.microsoft.com/library/azure/mt267594.aspx)發行項。

## <a name="hit-highlighting"></a>搜尋結果醒目提示
當您檢視搜尋結果時，顯示任何符合指定的 hello 的屬性 （例如 hello 資料資產的名稱、 描述和標記） 的搜尋詞彙會反白顯示的 toomake 它更容易 tooidentify 為什麼給定的搜尋傳回指定的資料資產。

> [!NOTE]
> 關閉反白顯示，使用 hello 叫用 tooturn**反白顯示**切換 hello 資料目錄入口網站中。
>
>

當您檢視搜尋結果時，即使已啟用醒目提示，不一定能明顯看出為何某個資料資產會包含在其中。 因為預設會搜尋所有屬性，某個資料資產可能因為符合資料行層級的屬性而被傳回。 與多個使用者可以使用他們自己的標籤和描述的已註冊的資料資產加上註解，因為並非所有的中繼資料可能會顯示 hello 搜尋結果清單中。

在 hello 預設並排顯示檢視，包括在 hello 搜尋結果中顯示每個圖格**檢視搜尋術語符合**圖示，因此，如果您想要您可以快速檢視 hello 數目的相符項目和其位置，以及 toojump toothem。

 ![叫用反白顯示，而且在 hello Azure 資料目錄入口網站中的搜尋相符項目](./media/data-catalog-how-to-discover/search-matches.png)

## <a name="summary"></a>摘要
因為資料來源登錄至資料目錄複製結構，並將描述性中繼資料從 hello 資料來源 toohello 類別目錄服務，請 hello 資料來源變得更容易 toodiscover 並了解。 您已註冊的資料來源之後，您可以探索使用篩選，並從 hello 資料目錄入口網站中進行搜尋。

## <a name="next-steps"></a>後續步驟
* 如需如何逐步的詳細資訊 toodiscover 資料來源，請參閱[開始使用 Azure 資料目錄](data-catalog-get-started.md)。
