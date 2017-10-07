---
title: "SQL 資料倉儲與 Azure Machine Learning aaaUse |Microsoft 文件"
description: "搭配使用 Azure 機器學習服務與 SQL 資料倉儲以便開發解決方案的秘訣。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>搭配使用 Azure 機器學習服務與 SQL 資料倉儲
Azure Machine Learning 是完全受管理的預測分析服務，您可以對您的資料在 SQL 資料倉儲中，使用 toocreate 預測模型，並再發行為已備妥取用 web 服務。 您可以了解 hello 基本概念的預測分析和機器學習，藉由讀取[簡介 tooMachine 在 Azure 上學習][Introduction tooMachine Learning on Azure]。  您接著可以學 toocreate，如何訓練、 評分和測試使用 hello 的機器學習模型[教學課程中建立實驗][Create experiment tutorial]。

在本文中，您將學習如何遵循使用 hello toodo hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:

* 從資料庫 toocreate 讀取資料、 定型和計分的預測模型
* 寫入資料 tooyour 資料庫

## <a name="read-data-from-sql-data-warehouse"></a>從 SQL 資料倉儲讀取資料
我們將從 hello AdventureWorksDW 資料庫中的 Product 資料表讀取資料。

### <a name="step-1"></a>步驟 1
按一下以啟動新的實驗 + 新增在 hello hello Machine Learning Studio 視窗底部選取實驗，，然後選取 空白實驗。 選取 hello 預設試驗頂端 hello hello 畫布的名稱，以及將它重新命名 toosomething 有意義，例如，自行車的價格預測。

### <a name="step-2"></a>步驟 2
尋找資料集的 hello 調色盤中的 hello 讀取器模組和 hello 左邊 hello 實驗畫布上的模組。 拖曳 hello 模組 toohello 實驗畫布。
![][drag_reader]

### <a name="step-3"></a>步驟 3
選取 hello 讀取器模組，然後填寫 hello 屬性 窗格。

1. 選取 Azure SQL Database 做為 hello 資料來源。
2. 資料庫伺服器名稱： 類型 hello 伺服器名稱。 您可以使用 hello [Azure 入口網站][ Azure portal] toofind 這。

![][server_name]

1. 資料庫名稱： 類型 hello hello 您剛才指定的伺服器上的資料庫名稱。
2. 伺服器的使用者帳戶名稱： 輸入 hello 的使用者名稱擁有 hello 資料庫的存取權限的帳戶。
3. 伺服器使用者帳戶密碼： 提供 hello hello 密碼指定使用者帳戶。
4. 接受任何伺服器憑證： 如果您想 tooskip 讀取資料之前，檢閱 hello 站台憑證，請使用此選項 （較不安全）。
5. 資料庫查詢： 輸入 SQL 陳述式描述您想要 tooread hello 資料。 在此情況下，我們會使用下列查詢的 hello 產品資料表讀取資料。

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>步驟 4
1. 按一下下 hello 實驗畫布的執行執行 hello 實驗。
2. Hello 實驗完成時，hello 讀取器模組必須順利完成綠色核取記號 tooindicate。 請注意也 hello hello 右上角中執行狀態的已完成。

![][run]

1. toosee hello 匯入的資料，按一下底端 hello hello 汽車的資料集的 hello 輸出連接埠並選取視覺效果。

## <a name="create-train-and-score-a-model"></a>建立、定型和評分模型
現在您可以使用此資料集：

* 建立模型：處理資料並定義功能
* 定型 hello 模型： 選擇並套用的學習演算法
* 分數與測試 hello 模型： 預測新的自行車價格

![][model]

深入了解 toocreate，如何訓練、 評分和測試的機器學習模型使用 hello toolearn[教學課程中建立實驗][Create experiment tutorial]。

## <a name="write-data-tooazure-sql-data-warehouse"></a>寫入資料 tooAzure SQL 資料倉儲
我們會撰寫 hello 結果集 tooProductPriceForecast 資料表 hello AdventureWorksDW 資料庫中。

### <a name="step-1"></a>步驟 1
尋找資料集的 hello 調色盤中的 hello 編寫器模組和 hello 左邊 hello 實驗畫布上的模組。 拖曳 hello 模組 toohello 實驗畫布。

![][drag_writer]

### <a name="step-2"></a>步驟 2
選取 hello 編寫器模組，然後填寫 hello 屬性 窗格。

1. 選取 Azure SQL Database 做為資料目的地 hello。
2. 資料庫伺服器名稱： 類型 hello 伺服器名稱。 您可以使用 hello [Azure 入口網站][ Azure portal] toofind 這。
3. 資料庫名稱： 類型 hello hello 您剛才指定的伺服器上的資料庫名稱。
4. 伺服器的使用者帳戶名稱： 輸入 hello 的使用者名稱擁有 hello 資料庫的寫入權限的帳戶。
5. 伺服器使用者帳戶密碼： 提供 hello hello 密碼指定使用者帳戶。
6. 接受任何伺服器憑證 （不安全）： 選取此選項，如果您不想 tooview hello 憑證。
7. 以逗號分隔清單儲存的資料行 toobe： 提供要 toooutput hello 資料集或結果資料行的清單。
8. 資料表名稱： 指定 hello hello 資料的資料表名稱。
9. Datatable 資料行的逗號分隔的清單： 指定 hello 資料行名稱 toouse hello 新資料表中。 hello 資料行名稱可以不同於 hello 的 hello 來源資料集中，但您必須列出 hello 相同數目的資料行，您定義的 hello 輸出資料表。
10. 每個 SQL Azure 作業寫入的資料列數目： 您可以設定 hello 撰寫 tooa SQL 資料庫的一項作業的資料列數目。

![][writer_properties]

### <a name="step-3"></a>步驟 3
1. 按一下下 hello 實驗畫布的執行執行 hello 實驗。
2. Hello 實驗完成時，所有的模組必須已順利完成綠色核取記號 tooindicate。

## <a name="next-steps"></a>後續步驟
如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
