---
title: "搭配使用 Power BI 與 SQL 資料倉儲 | Microsoft Docs"
description: "搭配使用 Power BI 與 Azure SQL 資料倉儲以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 4ea9a2ff0c95a73b348d3b48e9e62957d5cce31c
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>搭配使用 Power BI 與 SQL 資料倉儲
在 Azure SQL Database 中，SQL Data Warehouse Direct Connect 可讓使用者充分利用功能強大的邏輯下推，以及 Power BI 的分析功能。  透過 Direct Connect，查詢會在您瀏覽資料時即時傳送回到您的 Azure SQL 資料倉儲。  這項與 SQL 資料倉儲結合的功能，可讓使用者在數分鐘內針對數 TB 的資料建立動態報表。  此外，引入 [在 Power BI 中開啟] 按鈕可讓使用者直接將 Power BI 連接到其 SQL 資料倉儲，而不需從其他 Azure 部分收集資訊。

使用 Direct Connect 時，請注意：

* 在連接時指定完整的伺服器名稱 (請參閱以下內容以取得詳細資料)
* 確定資料庫的防火牆規則都設定為 [允許存取 Azure 服務]。
* 每個動作 (例如選取資料行或新增篩選器) 會直接查詢資料倉儲
* 大約每隔 15 分鐘重新整理一次動態磚 (重新整理不需要排程)
* 問答集不適用於 Direct Connect 資料集
* 不會自動挑選結構描述變更
* 所有「直接連接」查詢都將在 2 分鐘後逾時

隨著我們持續改善使用體驗，這些限制和助益事項可能會改變。 連接的步驟如下詳述。  

## <a name="using-the-open-in-power-bi-button"></a>使用 [在 Power BI 中開啟] 按鈕
使用 [在 Power BI 中開啟] 按鈕，是在 SQL 資料倉儲與 Power BI 之間移動的最簡單方式。 此按鈕可讓您順暢地開始在 Power BI 中建立新的儀表板。  

1. 若要開始瀏覽至您在 Azure 入口網站的 SQL 資料倉儲執行個體。
2. 按一下 [在 Power BI 中開啟] 按鈕。
3. 如果我們無法直接將您登入，或者您沒有 Power BI 帳戶，您必須登入。  
4. 您會被導向到 SQL 資料倉儲連線頁面，其中預先填入您的 SQL 資料倉儲中的資訊。
5. 輸入您的認證後，您將會完全連線到您的 SQL 資料倉儲。

## <a name="connecting-through-the-power-bi-portal"></a>透過 Power BI 入口網站連接
除了使用 [在 Power BI 中開啟] 按鈕，使用者也可以透過 Power BI 入口網站連接至其 SQL 資料倉儲。

1. 在導覽窗格的底部按一下 [取得資料]。
2. 選取 [資料庫]。
3. 一旦進入了 [資料庫] 頁面，請選取 [Azure SQL 資料倉儲]，然後按一下 [連線]。
4. 輸入必要的連線資訊。  在「Azure 入口網站」中可以找到您的伺服器名稱和資料庫名稱。
5. 會將您導向回到 Power BI 的主頁面，在您的連接已建立後，[資料集] 底下新的項目會出現，並具有執行個體的名稱。  
6. 您可以按一下新資料集，以瀏覽您資料庫中的所有資料表和檢視。 選取資料行會將查詢送回來源，並以動態方式建立視覺效果。 這些視覺效果可儲存在新的報表中，並釘選回您的儀表板。

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
