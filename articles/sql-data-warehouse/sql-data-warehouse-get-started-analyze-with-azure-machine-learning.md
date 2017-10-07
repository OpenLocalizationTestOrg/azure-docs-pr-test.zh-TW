---
title: "與 Azure Machine Learning aaaAnalyze 資料 |Microsoft 文件"
description: "使用 Azure 機器學習 toobuild 預測機器學習模型根據儲存在 Azure SQL 資料倉儲中的資料。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>使用 Azure Machine Learning 分析資料
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

本教學課程使用 Azure 機器學習 toobuild 預測機器學習模型根據儲存在 Azure SQL 資料倉儲中的資料。 具體而言，這會建置目標的行銷活動的 hello 自行車購買 Adventure Works，由預測如果客戶可能 toobuy 自行車。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>必要條件
在本教學課程 toostep，您需要：

* 預先載入 AdventureWorksDW 範例資料的 SQL 資料倉儲。 tooprovision，請參閱[建立 SQL 資料倉儲][ Create a SQL Data Warehouse]選擇 tooload hello 範例資料。 如果您已經有資料倉儲但沒有範例資料，您可以[手動載入範例資料][load sample data manually]。

## <a name="1-get-hello-data"></a>1.取得 hello 資料
hello 資料是在 hello AdventureWorksDW 資料庫中的 hello dbo.vTargetMail 檢視。 tooread 這項資料：

1. 登入 [Azure Machine Learning Studio][Azure Machine Learning studio] 並按一下我的實驗。
2. 按一下 [+ 新增] 並選取 [空白實驗]。
3. 輸入您的實驗名稱：目標行銷。
4. 拖曳 hello**讀取器**從 hello 模組窗格將 hello 畫布的模組。
5. Hello 屬性 窗格中指定 SQL 資料倉儲資料庫的 hello 詳細的資料。
6. 指定 hello 資料庫**查詢**感興趣的 tooread hello 資料。

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

按一下以執行 hello 實驗**執行**下 hello 實驗畫布。
![執行 hello 實驗][1]

Hello 實驗順利地完成執行之後，按一下 hello 底部 hello hello 讀取器模組的輸出連接埠，然後選取 **視覺化**toosee hello 匯入資料。
![檢視匯入的資料][3]

## <a name="2-clean-hello-data"></a>2.全新的 hello 資料
tooclean hello 資料、 卸除某些不相關的 hello 模型的資料行。 toodo 這樣：

1. 拖曳 hello**投射資料行**hello 畫布模組。
2. 按一下**啟動資料行選取器**hello 屬性窗格 toospecify 想 toodrop 哪些資料行中。
   ![][4]
3. 排除兩個資料行：CustomerAlternateKey 和 GeographyKey。
   ![移除不必要的資料行][5]

## <a name="3-build-hello-model"></a>3.建立 hello 模型
我們將會分割 hello 資料 80-20: 80 %tootrain 機器學習模型和 20%tootest hello 模型。 我們可以將這個二元分類問題的 hello 「 二級 」 演算法使用。

1. 拖曳 hello**分割**hello 畫布模組。
2. 輸入 0.8 hello 第一個輸出資料集在 hello 屬性 窗格中的資料列的分數。
   ![將資料分成訓練集和測試集][6]
3. 拖曳 hello**二級促進式決策樹**hello 畫布模組。
4. 拖曳 hello**定型模型**模組 hello 畫布，並指定 hello 輸入。 然後，按一下 [**啟動資料行選取器**hello 屬性] 窗格中。
   * 第一個輸入：ML 演算法。
   * 第二個輸入： 在資料 tootrain hello 演算法。
     ![連接 hello 定型模型 」 模組][7]
5. 選取 hello **BikeBuyer** hello toopredict 資料行資料行。
   ![選取資料行 toopredict][8]

## <a name="4-score-hello-model"></a>4.計分 hello 模型
現在，我們將測試 hello 模型測試資料上執行的方式。 我們將會比較 hello 演算法我們使用不同的演算法 toosee 的效能更好的選擇。

1. 拖曳**計分模型**hello 畫布模組。
    第一個輸入： 定型模型的第二個輸入： 測試資料![分數 hello 模型][9]
2. 拖曳 hello**二級貝氏點機器**到 hello 實驗畫布。 我們將會比較此演算法如何比較 toohello 二級促進式決策樹中執行。
3. 複製和貼上的 hello 定型模型及計分模型中模組 hello 畫布。
4. 拖曳 hello**評估模型**hello 畫布 toocompare hello 兩個演算法的模組。
5. **執行**hello 實驗。
   ![執行 hello 實驗][10]
6. 按一下底部 hello hello 評估模型 」 模組的 hello 輸出連接埠，然後按一下 視覺化。
   ![將評估結果視覺化][11]

提供的 hello 度量 hello ROC 曲線，有效位數回收圖表，提起曲線。 查看這些度量，我們可以看到 hello 第二個進一步執行該 hello 第一個模型。 在 hello 什麼 hello 第一個模型來預測，按一下輸出連接埠的 hello 計分模型，然後按一下 視覺化 toolook。
![將評分結果視覺化][12]

您會看到兩個的多個資料行加入 tooyour 測試資料集。

* 計分機率： hello 可能性客戶是自行車購買者。
* 計分標籤： hello 分類由 hello 模型-自行車買主 (1) 與否 (0)。 用於標示此機率臨界值設定 too50%，而且可加以調整。

比較 hello 資料行 BikeBuyer （實際） 與 hello 計分標籤 （預測），您可以查看呈現 hello 模型的執行。 做為下一個步驟，您可使用此模型 toomake 預測新客戶並發佈為 web 服務，此模型或寫入結果後 tooSQL 資料倉儲。

## <a name="next-steps"></a>後續步驟
toolearn 有關建立預測的機器學習模型的詳細資訊，請參閱太[簡介 tooMachine 在 Azure 上學習][Introduction tooMachine Learning on Azure]。

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
