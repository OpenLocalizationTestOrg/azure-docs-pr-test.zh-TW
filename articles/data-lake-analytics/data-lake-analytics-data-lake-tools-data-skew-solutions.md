---
title: "使用 Azure 資料湖 Tools for Visual Studio aaaResolve 資料扭曲問題 |Microsoft 文件"
description: "使用 Azure Data Lake Tools for Visual Studio 針對資料扭曲問題的可能解決方案進行疑難排解。"
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>使用 Azure Data Lake Tools for Visual Studio 解決資料扭曲問題

## <a name="what-is-data-skew"></a>什麼是資料扭曲？

簡單來說，資料扭曲就是被過度代表的值。 假設您已經指派 50 稅 examiners tooaudit 稅傳回美國州一個檢查程式。 hello 我們在此將檢查程式，因為 hello 母體擴展有很小，有一些 toodo。 California，不過，hello 檢查程式都會保持忙碌因為 hello 狀態大型母體擴展。
    ![資料扭曲問題範例](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

在我們的案例中，hello 資料是平均地分散到所有稅額 examiners，這表示某些 examiners 必須比其他多運作。 在您自己的工作，您經常遇到 hello 稅檢查程式範例的情況。 在更多技術詞彙中，一個頂點取得更多的資料比其對等，可讓多個其他項目，最後會變慢整項作業的 hello 運作的 hello 頂點的情況。 更糟的是，hello 作業可能會失敗，因為端點可能會讓，例如，5 小時執行階段限制和 6 GB 的記憶體限制。

## <a name="resolving-data-skew-problems"></a>解決資料扭曲問題

Azure Data Lake Tools for Visual Studio 可協助偵測出您的作業是否有資料扭曲問題。 如果有問題存在，您可以嘗試本節中的 hello 解決方案來解決。

## <a name="solution-1-improve-table-partitioning"></a>解決方案 1：改善資料表分割

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>選項 1： 篩選 hello 扭曲索引鍵值事先

如果它不會影響您的商務邏輯，您可以事先篩選 hello 更高頻率的值。 例如，如果有大量 000-000-000 GUID 資料行中，您可能不想 tooaggregate 該值。 您之前彙總，您可以撰寫"WHERE GUID ！ ="000-000 000 的""toofilter hello 高頻率的值。

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>選項 2：選擇不同的分割區或散發索引鍵

在 hello 前面範例中，如果您想要只 toocheck hello 稅稽核工作負載所有透過 hello 國家/地區，您可以改善 hello 資料散發索引鍵選取 hello ID 編號。 挑選不同的磁碟分割或散發索引鍵可以有時 hello 平均分散資料更，但您需要確定此選項並不會影響您的商務邏輯 toomake。 比方說，toocalculate hello 稅加總每個狀態，您可能會想 toodesignate_狀態_hello 資料分割索引鍵。 如果您繼續 tooexperience 這個問題，請嘗試使用選項 3。

### <a name="option-3-add-more-partition-or-distribution-keys"></a>選項 3：新增更多分割區或散發索引鍵

您可以不只使用_州別_做為資料分割索引鍵，而使用多個資料分割索引鍵。 例如，請考慮加入_郵遞區號_做為額外的資料分割索引鍵 tooreduce 資料分割大小及更平均散發 hello 資料。

### <a name="option-4-use-round-robin-distribution"></a>選項 4：使用循環配置資源散發

如果磁碟分割及散發找不到適當的索引鍵，您可以嘗試 toouse 循環配置資源發佈。 循環配置資源散發會平等對待所有資料列，並將資料列隨機放到對應的貯體。 hello 資料取得平均分佈，但它遺失位置資訊，也會降低某些作業的作業效能的缺點。 此外，如果您仍執行彙總 hello 扭曲索引鍵，將會保存 hello 資料扭曲問題。 toolearn 有關循環配置資源發佈的詳細資訊，請參閱 「 hello U-SQL 資料表發佈一節中[CREATE TABLE (SQL U): 使用結構描述中建立資料表](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch)。

## <a name="solution-2-improve-hello-query-plan"></a>解決方案 2： 改善 hello 查詢計劃

### <a name="option-1-use-hello-create-statistics-statement"></a>選項 1： 使用 hello CREATE STATISTICS 陳述式

U-SQL 資料表提供 hello CREATE STATISTICS 陳述式。 此陳述式可讓多個資訊 toohello 查詢最佳化工具有關 hello 資料特性，例如值的分佈，儲存在資料表中。 對於大部分查詢而言 hello 查詢最佳化工具已經產生高品質查詢計劃 hello 必要的統計資料。 有時候，您可能需要 tooimprove 查詢效能，藉由建立其他統計資料建立的統計資料或修改 hello 查詢設計。 如需詳細資訊，請參閱 hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx)頁面。

程式碼範例：

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>統計資料的資訊不會自動更新。 如果您不需要重新建立 hello 統計資料更新資料表中的 hello 資料，可能會下降 hello 查詢效能。

### <a name="option-2-use-skewfactor"></a>選項 2：使用 SKEWFACTOR

如果您想 toosum hello 稅每個狀態，您必須使用 GROUP BY 狀態，不會避免 hello 資料扭曲問題的方法。 不過，您可以提供資料提示資料會扭曲索引鍵中，以便 hello 最佳化工具可以為您準備執行計劃您查詢 tooidentify 中。

通常，您可以設定 hello 參數做為 0.5 和 1，表示不太誤差和 1 意義大量誤差 0.5。 因為 hello 提示會影響 hello 目前的陳述式和所有下游的陳述式的執行計畫最佳化，請先確定 tooadd hello 提示 hello 潛在扭曲 key-wise 彙總。

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

程式碼範例：

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>選項 3：使用 ROWCOUNT  
此外 tooSKEWFACTOR，特定的扭曲金鑰聯結案例中，如果您知道該 hello 其他聯結的資料列集很小，就可以判斷 hello 最佳化工具在聯結之前的 hello U-SQL 陳述式中加入的資料列計數的提示。 如此一來，最佳化工具可以選擇廣播的聯結策略 toohelp 改善效能。 請注意，資料列計數無法解決 hello 資料扭曲問題，但可提供一些其他的說明。

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

程式碼範例：

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>解決方案 3： 改善 hello 使用者定義減壓器和結合子

有時候，您可以撰寫使用者定義運算子 toodeal 具有複雜的程序邏輯和編寫完善的減壓器和結合子可能會降低資料扭曲問題，在某些情況下。

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>選項 1：在情況允許時使用遞迴歸納器

根據預設，使用者定義的歸納器會以非遞迴模式執行，這代表某個索引鍵所減少的工作會被散發至單一頂點。 但如果您的資料有所偏差，可能會在單一的端點處理，長時間執行的 hello 龐大資料集。

tooimprove 效能，您可以在您的程式碼 toodefine 減壓器 toorun 的遞迴模式中加入屬性。 然後，可以是分散式的 toomultiple 頂點 hello 龐大資料集，並平行執行，因此可加快您的工作。

toochange 非遞迴減壓器 toorecursive，您必須確定您的演算法是關聯 toomake。 例如，hello 總和是關聯，而 hello 中間值不是。 您也需要確定輸入的 hello 和減壓器的輸出，保留 hello toomake 相同的結構描述。

遞迴歸納器的屬性：

    [SqlUserDefinedReducer(IsRecursive = true)]

程式碼範例：

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>選項 2：在情況允許時使用資料列層級結合器模式

特定扭曲索引鍵聯結案例類似 ROWCOUNT 提示 toohello，結合子模式會嘗試 toodistribute 龐大扭曲機碼值組 toomultiple 頂點以便 hello 工作可以同時執行。 結合器模式無法解決資料扭曲問題，但能夠為大型扭曲索引鍵值集提供一些額外的協助。

根據預設，hello 的結合子模式為 「 完整 」，這表示 hello 剩餘的資料列集，而且不能分隔正確的資料列集。 設定為左/右/內部的 hello 模式可讓資料列層級聯結。 hello 系統分隔 hello 對應的資料列集，並將它們散發到平行執行的多個頂點。 不過，您要設定 hello 的結合子模式之前，請小心 tooensure hello 對應的資料列集，可以區隔。

接下來的 hello 範例顯示分隔左邊的資料列集。 單一輸入資料列從 hello 左取決於每個輸出資料列同時可能會取決於權限與 hello hello 的所有資料列相同機碼值。 如果您為 left 設定 hello 的結合子模式，hello 系統分隔 hello 龐大左邊的資料列集為小型的並將它們指派 toomultiple 頂點。

![結合器模式圖例](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>如果您將 hello 錯誤結合子模式，hello 組合比較沒有效率，且 hello 結果可能有問題。

結合器模式的屬性︰

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left)： 取決於從 hello 左單一輸入資料列的每個輸出資料列 (和所有可能列 hello hello 權限與從相同機碼值)。

- qlUserDefinedCombiner(Mode=CombinerMode.Right)： 每個輸出資料列而定右 hello 的單一輸入資料列 (和所有可能列 hello 左 hello 與從相同機碼值)。

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner)： 每個輸出資料列取決於 hello 向左和右的 hello hello 的單一輸入資料列相同值。

程式碼範例：

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
