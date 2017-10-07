---
title: "Azure SQL database aaaQuery 效能深入資訊 |Microsoft 文件"
description: "效能監視識別的 hello 大部分的 CPU 耗用查詢 Azure SQL database 的查詢。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Azure SQL Database 查詢效能深入解析
管理和調整 hello 關聯式資料庫效能是富有挑戰性的工作需要重要的專業知識和需要投入時間。 查詢效能深入解析可讓您 toospend 藉由提供 hello 下列疑難排解資料庫效能較少的時間：

* 更深入的資料庫資源 (DTU) 取用分析。 
* hello 排名最前面查詢依 CPU/期間執行計數，可能會改善效能進行微調。
* 向下的能力 toodrill hello 到 hello 詳細資料的查詢、 檢視其文字和資源使用量的歷程記錄。 
* 效能微調註解，可顯示 [SQL Azure Database 建議程式](sql-database-advisor.md)  



## <a name="prerequisites"></a>必要條件
* 「查詢效能深入解析」要求 [查詢存放區](https://msdn.microsoft.com/library/dn817826.aspx) 在您的資料庫上為作用中狀態。 如果未執行查詢存放區，hello 入口網站會提示您 tooturn 其上。

## <a name="permissions"></a>權限
hello 下列[角色型存取控制](../active-directory/role-based-access-control-what-is.md)權限是必要的 toouse 查詢效能深入解析： 

* **讀取器**，**擁有者**，**參與者**， **SQL DB 參與者**，或**SQL Server 參與者**權限需要 tooview hello 熱門資源取用查詢和圖表。 
* **擁有者**，**參與者**， **SQL DB 參與者**，或**SQL Server 參與者**權限是必要的 tooview 查詢文字。

## <a name="using-query-performance-insight"></a>使用查詢效能深入解析
查詢效能深入解析為簡單 toouse:

* 開啟[Azure 入口網站](https://portal.azure.com/)和尋找您想 tooexamine 的資料庫。 
  * 從左側功能表中，[支援和疑難排解] 下方，選取 [查詢效能深入解析]。
* Hello 第一個索引標籤上，檢閱 熱門資源取用查詢的 hello 清單。
* 選取個別查詢 tooview 其詳細資料。
* 開啟 [SQL Azure Database 建議程式](sql-database-advisor.md) ，並查看是否有任何可用的建議。
* 使用滑桿或縮放圖示 toochange 觀察到的間隔。
  
    ![效能儀表板](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> 幾個小時的資料需要 toobe 查詢存放區所擷取的 SQL Database tooprovide 查詢效能深入資訊。 如果 hello 資料庫有任何活動或查詢存放區期間，未作用一段時間，顯示該時間週期時，將為空白 hello 圖表。 如果查詢存放區不在執行中，您可隨時加以啟用。   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>檢閱排名最前面的 CPU 取用查詢
在 hello[入口網站](http://portal.azure.com)不要遵循 hello:

1. 瀏覽 tooa SQL 資料庫，然後按一下 **所有設定** > **支援 + 疑難排解** > **查詢效能深入解析**。 
   
    ![查詢效能深入解析][1]
   
    hello 排名最前面查詢檢視隨即開啟，並列出 hello 前 CPU 取用查詢。
2. 按一下 詳細資料的 hello 圖表周圍。<br>hello 第一行會顯示 hello 資料庫的整體 DTU %hello 橫條圖會顯示在 hello 選間隔期間 hello 選取查詢所使用的 CPU %時 (例如，如果**上週**選取每個橫條都代表一天)。
   
    ![排名最前面的查詢][2]
   
    hello 下方的方格代表 hello 顯示查詢的彙總的資訊。
   
   * 查詢識別碼 - 資料庫內部查詢的唯一識別碼。
   * 在可觀察時間間隔期間每個查詢的 CPU (取決於彙總函式)。
   * 每個查詢的持續時間 (取決於彙總函式)。
   * 特定查詢的總執行次數。
     
     選取或清除個別查詢 tooinclude 或排除 hello 圖表使用核取方塊。
3. 如果您的資料就會成為過時，請按一下 hello**重新整理** 按鈕。
4. 您可以使用滑桿和顯示比例按鈕 toochange 的觀測間隔，並調查尖峰：![設定](./media/sql-database-query-performance/zoom.png)
5. (選擇性) 如果您想要不同的檢視，您可以選取 [自訂]  索引標籤，然後設定：
   
   * 度量 (CPU、持續時間、執行計數)
   * 時間間隔 (過去 24 小時、過去一週、過去一個月)。 
   * 查詢數目。
   * 彙總函式。
     
     ![settings](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>檢視個別查詢詳細資料
tooview 查詢詳細資料：

1. 按一下 hello 清單的最上層查詢中的任何查詢。
   
    ![詳細資料](./media/sql-database-query-performance/details.png)
2. hello 詳細資料檢視會開啟，並 hello 查詢 CPU 耗用量/期間執行計數細分經過一段時間。
3. 按一下 詳細資料的 hello 圖表周圍。
   
   * 上方圖表可顯示行整體資料庫的 DTU %，而且 hello 列 hello 選取的查詢所耗用的 CPU %。
   * 第二個圖表可顯示總持續時間由 hello 選取的查詢。
   * 下方圖表可顯示 hello 選取查詢所執行的總次數。
     
     ![查詢詳細資料][3]
4. （選擇性） 使用滑桿、 顯示比例按鈕或按**設定**toocustomize 查詢資料的顯示方式或 toopick 不同的時間期間。

## <a name="review-top-queries-per-duration"></a>針對每段持續時間檢閱排名最前面的查詢
在 hello 最近更新中的查詢效能深入解析，我們引進了兩個新的計量，可協助您找出潛在的瓶頸： 持續時間和執行計數。<br>

長時間執行的查詢有 hello 的鎖定較長的資源、 封鎖其他使用者，以及限制延展性的最大可能性。 它們也是 hello 最佳化的最佳候選項目。<br>

tooidentify 長時間執行的查詢：

1. 針對選取的資料庫，在 [查詢效能深入解析] 中開啟 [自訂]  索引標籤
2. 變更計量 toobe**持續時間**
3. 選取查詢數目和觀測間隔
4. 選取彙總函式
   
   * **Sum** 會加總整個觀測間隔內的所有查詢執行時間。
   * **Max** 會尋找在整個觀測間隔內執行時間最大的查詢。
   * **Avg**平均執行時間，所有的查詢執行並顯示您會發現 hello 超出這些平均值的頂端。 
     
     ![查詢持續時間][4]

## <a name="review-top-queries-per-execution-count"></a>針對每個執行計數檢閱排名最前面的查詢
執行數目很高可能不會影響資料庫本身且資源使用量可能很低，但整體應用程式可能會變慢。

在某些情況下，極高的執行計數可能會導致 tooincrease 的網路往返。 往返次數會大幅影響效能。 它們是主體 toonetwork 延遲和 toodownstream 伺服器延遲。 

比方說，許多資料導向網站經常存取 hello 資料庫針對每個使用者要求。 雖然連接共用有幫助，hello 增加網路流量和 hello 資料庫伺服器上的處理負載可能會影響效能。  一般建議是 tookeep round 往返 tooan 絕對最小值。

tooidentify 經常執行的查詢 （「 多對話 」） 的查詢：

1. 針對選取的資料庫，在 [查詢效能深入解析] 中開啟 [自訂]  索引標籤
2. 變更計量 toobe**執行計數**
3. 選取查詢數目和觀測間隔
   
    ![查詢執行計數][5]

## <a name="understanding-performance-tuning-annotations"></a>了解效能微調註解
同時瀏覽您的工作負載中查詢效能深入解析，您可能會注意到具有垂直線 hello 圖表上方的圖示。<br>

這些圖示是註解。它們代表 [SQL Azure Database 建議程式](sql-database-advisor.md)所執行會影響效能的動作。 由暫留註釋，您可以取得 hello 動作的基本資訊：

![查詢註解][6]

如果您想要更多的 tooknow，或將 advisor 建議，套用，請按一下 [hello] 圖示。 隨即會開啟動作的詳細資料。 如果是有效的建議，您就能使用命令立即套用動作。

![查詢註解詳細資料][7]

### <a name="multiple-annotations"></a>多個註解。
它是可能的縮放層級，因為會關閉 tooeach 其他的註釋，將取得摺疊成一個。 這將會利用特殊的圖示來表示，按一下該圖示就會開啟新的刀鋒視窗，其中顯示已分組的註解清單。
建立查詢和效能調整動作的關聯可協助 toobetter 了解您的工作負載。 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>最佳化查詢效能深入解析的 hello 查詢存放區組態
在您使用的查詢效能深入解析，您可能會遇到 hello 遵循查詢存放區的訊息：

* 「此資料庫的查詢存放區未正確設定。 按一下這裡 toolearn 詳細。 」
* 「此資料庫的查詢存放區未正確設定。 按一下這裡 toochange 設定。 」 

查詢存放區不能 toocollect 新資料時，通常會出現這些訊息。 

當查詢存放區處於唯讀狀態且以最佳方式設定參數時，就會發生第一種狀況。 您可以藉由增加查詢存放區的大小，或清除查詢存放區來修正此問題。

![qds 按鈕][8]

當查詢存放區已關閉或參數並不是以最佳方式所設定時，就會發生第二種狀況。 <br>藉由執行下列命令，或直接從入口網站，您可以變更 hello 保留和擷取原則，並啟用查詢存放區：

![qds 按鈕][9]

### <a name="recommended-retention-and-capture-policy"></a>建議使用的保留期和擷取原則
保留期原則有兩種：

* 大小基礎-如果已到達組 tooAUTO 它將會清除資料自動當接近大小上限。
* 以時間為基礎-根據預設，我們會將它設定 too30 天，也就是說，如果查詢存放區就會用完空間，將會刪除查詢超過 30 天的資訊

擷取原則可以設定為：

* **All**：擷取所有的查詢。
* **Auto**：會忽略不常執行的查詢，以及編譯和執行持續時間微不足道的查詢。 執行次數、編譯及執行階段持續時間的臨界值是由內部決定的。 這是 hello 預設選項。
* **None**：「查詢存放區」會停止擷取新的查詢，不過仍然會收集已擷取查詢的執行階段統計資料。

我們建議您設定的所有原則 tooAUTO 和全新的原則 too30 天：

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

增加查詢存放區的大小， 這可能是由連接 tooa 資料庫執行和發行下列查詢：

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

不過，如果您不想 toowait 您可以清除查詢存放區，套用這些設定會最後會讓收集新的查詢，查詢存放區。 

> [!NOTE]
> 執行下列查詢將會刪除 hello 查詢存放區中的所有目前資訊。 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>摘要
查詢效能深入解析，可協助您了解 hello 的查詢工作負載的影響，以及它與 toodatabase 資源耗用量。 利用此功能，您將深入了解 hello 頂端取用查詢，並輕鬆地在問題之前就識別出 hello 的 toofix。

## <a name="next-steps"></a>後續步驟
如需有關改善您的 SQL database 的 hello 效能的其他建議，請按一下[建議](sql-database-advisor.md)上 hello**查詢效能深入解析**刀鋒視窗。

![效能建議程式](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

