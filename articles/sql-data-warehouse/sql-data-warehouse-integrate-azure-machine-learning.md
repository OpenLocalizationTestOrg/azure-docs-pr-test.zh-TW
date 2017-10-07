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
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="85843-103">搭配使用 Azure 機器學習服務與 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="85843-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="85843-104">Azure Machine Learning 是完全受管理的預測分析服務，您可以對您的資料在 SQL 資料倉儲中，使用 toocreate 預測模型，並再發行為已備妥取用 web 服務。</span><span class="sxs-lookup"><span data-stu-id="85843-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="85843-105">您可以了解 hello 基本概念的預測分析和機器學習，藉由讀取[簡介 tooMachine 在 Azure 上學習][Introduction tooMachine Learning on Azure]。</span><span class="sxs-lookup"><span data-stu-id="85843-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="85843-106">您接著可以學 toocreate，如何訓練、 評分和測試使用 hello 的機器學習模型[教學課程中建立實驗][Create experiment tutorial]。</span><span class="sxs-lookup"><span data-stu-id="85843-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="85843-107">在本文中，您將學習如何遵循使用 hello toodo hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="85843-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="85843-108">從資料庫 toocreate 讀取資料、 定型和計分的預測模型</span><span class="sxs-lookup"><span data-stu-id="85843-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="85843-109">寫入資料 tooyour 資料庫</span><span class="sxs-lookup"><span data-stu-id="85843-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="85843-110">從 SQL 資料倉儲讀取資料</span><span class="sxs-lookup"><span data-stu-id="85843-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="85843-111">我們將從 hello AdventureWorksDW 資料庫中的 Product 資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="85843-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="85843-112">步驟 1</span><span class="sxs-lookup"><span data-stu-id="85843-112">Step 1</span></span>
<span data-ttu-id="85843-113">按一下以啟動新的實驗 + 新增在 hello hello Machine Learning Studio 視窗底部選取實驗，，然後選取 空白實驗。</span><span class="sxs-lookup"><span data-stu-id="85843-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="85843-114">選取 hello 預設試驗頂端 hello hello 畫布的名稱，以及將它重新命名 toosomething 有意義，例如，自行車的價格預測。</span><span class="sxs-lookup"><span data-stu-id="85843-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="85843-115">步驟 2</span><span class="sxs-lookup"><span data-stu-id="85843-115">Step 2</span></span>
<span data-ttu-id="85843-116">尋找資料集的 hello 調色盤中的 hello 讀取器模組和 hello 左邊 hello 實驗畫布上的模組。</span><span class="sxs-lookup"><span data-stu-id="85843-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="85843-117">拖曳 hello 模組 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="85843-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="85843-118">步驟 3</span><span class="sxs-lookup"><span data-stu-id="85843-118">Step 3</span></span>
<span data-ttu-id="85843-119">選取 hello 讀取器模組，然後填寫 hello 屬性 窗格。</span><span class="sxs-lookup"><span data-stu-id="85843-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="85843-120">選取 Azure SQL Database 做為 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="85843-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="85843-121">資料庫伺服器名稱： 類型 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="85843-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="85843-122">您可以使用 hello [Azure 入口網站][ Azure portal] toofind 這。</span><span class="sxs-lookup"><span data-stu-id="85843-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="85843-123">資料庫名稱： 類型 hello hello 您剛才指定的伺服器上的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="85843-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="85843-124">伺服器的使用者帳戶名稱： 輸入 hello 的使用者名稱擁有 hello 資料庫的存取權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="85843-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="85843-125">伺服器使用者帳戶密碼： 提供 hello hello 密碼指定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="85843-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="85843-126">接受任何伺服器憑證： 如果您想 tooskip 讀取資料之前，檢閱 hello 站台憑證，請使用此選項 （較不安全）。</span><span class="sxs-lookup"><span data-stu-id="85843-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="85843-127">資料庫查詢： 輸入 SQL 陳述式描述您想要 tooread hello 資料。</span><span class="sxs-lookup"><span data-stu-id="85843-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="85843-128">在此情況下，我們會使用下列查詢的 hello 產品資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="85843-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="85843-129">步驟 4</span><span class="sxs-lookup"><span data-stu-id="85843-129">Step 4</span></span>
1. <span data-ttu-id="85843-130">按一下下 hello 實驗畫布的執行執行 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="85843-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="85843-131">Hello 實驗完成時，hello 讀取器模組必須順利完成綠色核取記號 tooindicate。</span><span class="sxs-lookup"><span data-stu-id="85843-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="85843-132">請注意也 hello hello 右上角中執行狀態的已完成。</span><span class="sxs-lookup"><span data-stu-id="85843-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="85843-133">toosee hello 匯入的資料，按一下底端 hello hello 汽車的資料集的 hello 輸出連接埠並選取視覺效果。</span><span class="sxs-lookup"><span data-stu-id="85843-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="85843-134">建立、定型和評分模型</span><span class="sxs-lookup"><span data-stu-id="85843-134">Create, train and score a model</span></span>
<span data-ttu-id="85843-135">現在您可以使用此資料集：</span><span class="sxs-lookup"><span data-stu-id="85843-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="85843-136">建立模型：處理資料並定義功能</span><span class="sxs-lookup"><span data-stu-id="85843-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="85843-137">定型 hello 模型： 選擇並套用的學習演算法</span><span class="sxs-lookup"><span data-stu-id="85843-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="85843-138">分數與測試 hello 模型： 預測新的自行車價格</span><span class="sxs-lookup"><span data-stu-id="85843-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="85843-139">深入了解 toocreate，如何訓練、 評分和測試的機器學習模型使用 hello toolearn[教學課程中建立實驗][Create experiment tutorial]。</span><span class="sxs-lookup"><span data-stu-id="85843-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="85843-140">寫入資料 tooAzure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="85843-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="85843-141">我們會撰寫 hello 結果集 tooProductPriceForecast 資料表 hello AdventureWorksDW 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="85843-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="85843-142">步驟 1</span><span class="sxs-lookup"><span data-stu-id="85843-142">Step 1</span></span>
<span data-ttu-id="85843-143">尋找資料集的 hello 調色盤中的 hello 編寫器模組和 hello 左邊 hello 實驗畫布上的模組。</span><span class="sxs-lookup"><span data-stu-id="85843-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="85843-144">拖曳 hello 模組 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="85843-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="85843-145">步驟 2</span><span class="sxs-lookup"><span data-stu-id="85843-145">Step 2</span></span>
<span data-ttu-id="85843-146">選取 hello 編寫器模組，然後填寫 hello 屬性 窗格。</span><span class="sxs-lookup"><span data-stu-id="85843-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="85843-147">選取 Azure SQL Database 做為資料目的地 hello。</span><span class="sxs-lookup"><span data-stu-id="85843-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="85843-148">資料庫伺服器名稱： 類型 hello 伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="85843-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="85843-149">您可以使用 hello [Azure 入口網站][ Azure portal] toofind 這。</span><span class="sxs-lookup"><span data-stu-id="85843-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="85843-150">資料庫名稱： 類型 hello hello 您剛才指定的伺服器上的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="85843-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="85843-151">伺服器的使用者帳戶名稱： 輸入 hello 的使用者名稱擁有 hello 資料庫的寫入權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="85843-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="85843-152">伺服器使用者帳戶密碼： 提供 hello hello 密碼指定使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="85843-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="85843-153">接受任何伺服器憑證 （不安全）： 選取此選項，如果您不想 tooview hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="85843-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="85843-154">以逗號分隔清單儲存的資料行 toobe： 提供要 toooutput hello 資料集或結果資料行的清單。</span><span class="sxs-lookup"><span data-stu-id="85843-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="85843-155">資料表名稱： 指定 hello hello 資料的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="85843-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="85843-156">Datatable 資料行的逗號分隔的清單： 指定 hello 資料行名稱 toouse hello 新資料表中。</span><span class="sxs-lookup"><span data-stu-id="85843-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="85843-157">hello 資料行名稱可以不同於 hello 的 hello 來源資料集中，但您必須列出 hello 相同數目的資料行，您定義的 hello 輸出資料表。</span><span class="sxs-lookup"><span data-stu-id="85843-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="85843-158">每個 SQL Azure 作業寫入的資料列數目： 您可以設定 hello 撰寫 tooa SQL 資料庫的一項作業的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="85843-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="85843-159">步驟 3</span><span class="sxs-lookup"><span data-stu-id="85843-159">Step 3</span></span>
1. <span data-ttu-id="85843-160">按一下下 hello 實驗畫布的執行執行 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="85843-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="85843-161">Hello 實驗完成時，所有的模組必須已順利完成綠色核取記號 tooindicate。</span><span class="sxs-lookup"><span data-stu-id="85843-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85843-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="85843-162">Next steps</span></span>
<span data-ttu-id="85843-163">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="85843-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
