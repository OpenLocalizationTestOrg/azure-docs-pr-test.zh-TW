---
title: "SQL 資料倉儲與 Power BI aaaUse |Microsoft 文件"
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
ms.openlocfilehash: a3a347493d07af6824a561567f05894cfe3c0471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-with-sql-data-warehouse"></a>搭配使用 Power BI 與 SQL 資料倉儲
如同 Azure SQL Database，SQL 資料倉儲直接連線可讓使用者 tooleverage 強大邏輯下推連同 hello 的 Power BI 的分析功能。  使用直接連接，查詢會傳送後 tooyour Azure SQL 資料倉儲即時當您瀏覽 hello 資料。  此特性加 hello 小數位數 SQL 資料倉儲，可讓使用者 toocreate 動態報表以分鐘為單位依據數 tb 的資料。  此外，hello hello 開啟 Power BI 按鈕中導入可讓使用者 toodirectly 連接 Power BI tootheir SQL 資料倉儲，而不會收集 Azure 的其他部分的資訊。

使用 Direct Connect 時，請注意：

* 連接 （請參閱以下以取得詳細資料） 時，指定 hello 完整的伺服器名稱
* 確定防火牆規則的 hello 資料庫設定太 「 允許存取 tooAzure 服務 」。
* 選取資料行或加入篩選等每一個動作，都會直接查詢 hello 資料倉儲
* 磚重新整理大約每隔 15 分鐘 （重新整理不需要 toobe 排程）
* 問答集不適用於 Direct Connect 資料集
* 不會自動挑選結構描述變更
* 所有「直接連接」查詢都將在 2 分鐘後逾時

這些限制和備註可能會隨著我們持續 tooimprove hello 體驗變更。 hello 步驟 tooconnect 如下所述。  

## <a name="using-hello-open-in-power-bi-button"></a>使用 hello 'Power BI 中開啟 按鈕
您的 SQL 資料倉儲與 Power BI 之間 hello 最簡單方式 toomove 是以 hello 開啟中 Power BI 按鈕。 這個按鈕可讓您 tooseamlessly 開始在 Power BI 中建立新的儀表板。  

1. 啟動 tooget 瀏覽 tooyour hello Azure 傳統入口網站中的 SQL 資料倉儲執行個體。
2. 按一下 hello 'Power BI 中開啟 按鈕。
3. 如果我們不能 toosign 您在直接管理，或如果您沒有 Power BI 帳戶，您必須 toosign 中。  
4. 會將您導向 toohello SQL 資料倉儲連接頁面，您的 SQL 資料倉儲中的 hello 資訊預先填入。
5. 輸入您的認證之後，您會完全連接的 tooyour SQL 資料倉儲。

## <a name="connecting-through-hello-power-bi-portal"></a>透過 hello Power BI 入口網站連接
加法 toousing hello 開啟 Power BI 按鈕中，使用者可以也 tootheir SQL 資料倉儲連線透過 hello Power BI 入口網站。

1. 按一下 在 hello hello 瀏覽窗格底部的 「 取得資料 」。
2. 選取 [資料庫]。
3. 一次在 hello 資料庫頁面上，選取 [Azure SQL 資料倉儲 '，然後按一下連線]。
4. 輸入 hello 必要的連接資訊。  Hello Azure 入口網站中可以找到您的伺服器名稱和資料庫名稱。
5. 您將會導向回到 Power bi 和您的連線建立新的項目底下 '資料集' 之後 toohello 主頁面會顯示 hello 執行個體名稱。  
6. 您可以按一下新資料集 tooexplore hello hello 資料表和檢視您的資料庫中的所有。 選取資料行，將會傳送查詢後 toohello 來源，以動態方式建立視覺效果。 這些視覺效果可儲存為新的報表，並釘選回 tooyour 儀表板。

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
