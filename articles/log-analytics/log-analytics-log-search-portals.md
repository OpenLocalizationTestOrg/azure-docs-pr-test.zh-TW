---
title: "建立和編輯 Azure 記錄分析中的記錄檔查詢的 aaaPortals |Microsoft 文件"
description: "本文說明 hello 入口網站，您可以使用在 Azure Log Analytics toocreate 和編輯的記錄搜尋。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a>Azure Log Analytics 中用於建立和編輯記錄查詢的入口網站

> [!NOTE]
> 本文說明在使用新的查詢語言 hello Azure Log Analytics 入口網站。  您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。  
>
> 如果您的工作區尚未升級的 toohello 新的查詢語言，您應該參閱太[尋找資料記錄分析中使用記錄搜尋](log-analytics-log-searches.md)hello 最新版 hello 記錄搜尋入口網站上的資訊。

您可以使用記錄搜尋中的許多地方整個記錄分析 tooretrieve 資料從 hello 工作區。  實際建立和編輯查詢此外 tooworking 以互動方式與傳回資料不過，您必須是下面所述的兩個選項。  

## <a name="log-search-portal"></a>記錄搜尋入口網站
從 hello Azure 入口網站或 hello OMS 入口網站存取 hello 記錄搜尋入口網站。  它適合用來建立可在單行中建立的基本查詢。  而不啟動外部的入口網站，可以使用 hello 記錄搜尋網站，您可以使用它 tooperform 各式各樣函式包括建立警示規則、 建立電腦群組，以及匯出 hello hello 查詢結果的記錄搜尋。  

hello 記錄搜尋入口網站會提供多項功能，而不需要 hello 查詢語言的完整知識編輯 hello 查詢。  您可以取得這些功能摘要[Azure Log Analytics 使用 hello 記錄搜尋入口網站中建立的記錄搜尋](log-analytics-log-search-log-search-portal.md)。


![記錄搜尋入口網站](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a>進階 Analytics 入口網站
hello 進階分析入口網站是一個專用的入口網站，提供進階的功能不適用於 hello 記錄搜尋入口網站。  功能包括 hello 能力 tooedit 查詢在多行上，選擇性地執行程式碼、 區分內容的 Intellisense 和智慧的分析。  hello Advanced Analytics 入口網站是最適合在設計複雜的查詢，可能是儲存為記錄搜尋或複製並貼到其他的記錄分析項目。  您啟動 hello Advanced Analytics 入口網站，從 hello 記錄搜尋入口網站中的連結。

![進階 Analytics 入口網站](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


因為其進階的功能，您將通常用於 hello 進階分析入口網站為您主要的工具建立和編輯查詢。  一旦您判定 hello 查詢如預期般運作，然後複製並貼入例如 hello 記錄搜尋入口網站或檢視表設計工具的其他位置。  由於 hello Advanced Analytics 入口網站透過支援多行的查詢，從這個入口網站複製查詢時需要 tootake hello 下列事項。

- 必須從 hello 查詢移除註解，才能有複製及貼到另一個位置。  您可以在一行前加上兩個斜線 (//) 以對該行進行註解。  將多行查詢貼到單行時，會移除分行符號。  如果包含了註解，hello 第一個註解後面的所有字元都視為 hello 註解的一部分。


## <a name="next-steps"></a>後續步驟

- 逐步教學課程使用 hello[記錄搜尋入口網站](log-analytics-log-search-log-search-portal.md)或 hello [Advanced Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)toocreate 查詢。
- 簽出[上撰寫查詢的教學課程](https://go.microsoft.com/fwlink/?linkid=856078)使用 hello 新的查詢語言。
