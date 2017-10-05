---
title: "搭配使用 Azure 機器學習服務與 SQL 資料倉儲 | Microsoft Docs"
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
ms.openlocfilehash: c19860c6b5b1c15d1e29ddc67f9cf9ad4618725b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="bc2ea-103">搭配使用 Azure 機器學習服務與 SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="bc2ea-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="bc2ea-104">Azure 機器學習服務是一項完全受管理的預測性分析服務，您可用來在 SQL 資料倉儲中針對您的資料建立預測模型，並發佈為可供取用 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="bc2ea-105">閱讀 [Azure 上的機器學習服務簡介][Introduction to Machine Learning on Azure]，即可了解預測性分析和機器學習的基本概念。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="bc2ea-106">然後，您可以使用[建立實驗教學課程][Create experiment tutorial]，了解如何建立、定型、評分和測試機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="bc2ea-107">在本文中，您將了解如何使用 [Azure Machine Learning Studio][Azure Machine Learning Studio]：</span><span class="sxs-lookup"><span data-stu-id="bc2ea-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="bc2ea-108">從您的資料庫讀取資料來建立、定型和評分預測模型</span><span class="sxs-lookup"><span data-stu-id="bc2ea-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="bc2ea-109">將資料寫入您的資料庫</span><span class="sxs-lookup"><span data-stu-id="bc2ea-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="bc2ea-110">從 SQL 資料倉儲讀取資料</span><span class="sxs-lookup"><span data-stu-id="bc2ea-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="bc2ea-111">我們將從 AdventureWorksDW 資料庫中的 Product 資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bc2ea-112">步驟 1</span><span class="sxs-lookup"><span data-stu-id="bc2ea-112">Step 1</span></span>
<span data-ttu-id="bc2ea-113">按一下 Machine Learning Studio 視窗底部的 [+新增]，選取 [實驗]，然後選取 [空白實驗] 以開始新的實驗。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="bc2ea-114">選取畫布頂端的預設實驗名稱，然後將它重新命名為有意義的名稱，例如，單車價格預測。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="bc2ea-115">步驟 2</span><span class="sxs-lookup"><span data-stu-id="bc2ea-115">Step 2</span></span>
<span data-ttu-id="bc2ea-116">在實驗畫布左邊的資料集和模組選擇區中尋找 [讀取器] 模組。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="bc2ea-117">將此模組拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="bc2ea-118">步驟 3</span><span class="sxs-lookup"><span data-stu-id="bc2ea-118">Step 3</span></span>
<span data-ttu-id="bc2ea-119">選取 [讀取器] 模組並填寫屬性窗格。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="bc2ea-120">選取 Azure SQL Database 做為資料來源。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="bc2ea-121">資料庫伺服器名稱：輸入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-121">Database server name: Type the server name.</span></span> <span data-ttu-id="bc2ea-122">您可以使用 [Azure 入口網站][Azure portal]進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="bc2ea-123">資料庫名稱：輸入您剛指定的伺服器上的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="bc2ea-124">伺服器使用者帳戶名稱：輸入具有資料庫存取權限的帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="bc2ea-125">伺服器使用者帳戶名稱：提供指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="bc2ea-126">接受任何伺服器憑證：如果您想要在讀取資料前跳過檢閱網站憑證，請使用這個選項 (較不安全)。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="bc2ea-127">資料庫查詢：輸入 SQL 陳述式，描述您要讀取的資料。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="bc2ea-128">在此情況下，我們將使用下列查詢從 Product 資料表讀取資料。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="bc2ea-129">步驟 4</span><span class="sxs-lookup"><span data-stu-id="bc2ea-129">Step 4</span></span>
1. <span data-ttu-id="bc2ea-130">按一下實驗畫布下方的 [執行]，以執行實驗。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="bc2ea-131">實驗完成時，[讀取器] 模組都會呈現綠色核取標記，表示該模組已順利完成。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="bc2ea-132">同時也請留意位於右上角的「執行完成」狀態。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="bc2ea-133">若要查看匯入的資料，請按一下汽車資料集底部的輸出連接埠，然後選取 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="bc2ea-134">建立、定型和評分模型</span><span class="sxs-lookup"><span data-stu-id="bc2ea-134">Create, train and score a model</span></span>
<span data-ttu-id="bc2ea-135">現在您可以使用此資料集：</span><span class="sxs-lookup"><span data-stu-id="bc2ea-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="bc2ea-136">建立模型：處理資料並定義功能</span><span class="sxs-lookup"><span data-stu-id="bc2ea-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="bc2ea-137">定型模型：選擇並套用學習演算法</span><span class="sxs-lookup"><span data-stu-id="bc2ea-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="bc2ea-138">對模型評分和測試：預測新的自行車價格</span><span class="sxs-lookup"><span data-stu-id="bc2ea-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="bc2ea-139">若要深入了解如何建立、定型、評分和測試機器學習模型，請使用 [建立實驗教學課程][Create experiment tutorial]。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="bc2ea-140">將資料寫入至 Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="bc2ea-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="bc2ea-141">我們會將結果集寫入至 AdventureWorksDW 資料庫中的 ProductPriceForecast 資料表。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="bc2ea-142">步驟 1</span><span class="sxs-lookup"><span data-stu-id="bc2ea-142">Step 1</span></span>
<span data-ttu-id="bc2ea-143">在實驗畫布左邊的資料集和模組選擇區中尋找 [寫入器] 模組。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="bc2ea-144">將此模組拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="bc2ea-145">步驟 2</span><span class="sxs-lookup"><span data-stu-id="bc2ea-145">Step 2</span></span>
<span data-ttu-id="bc2ea-146">選取 [寫入器] 模組並填寫屬性窗格。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="bc2ea-147">選取 Azure SQL Database 做為資料目的地。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="bc2ea-148">資料庫伺服器名稱：輸入伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-148">Database server name: Type the server name.</span></span> <span data-ttu-id="bc2ea-149">您可以使用 [Azure 入口網站][Azure portal]進行搜尋。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="bc2ea-150">資料庫名稱：輸入您剛指定的伺服器上的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="bc2ea-151">伺服器使用者帳戶名稱：輸入具有資料庫寫入權限的帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="bc2ea-152">伺服器使用者帳戶名稱：提供指定之使用者帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="bc2ea-153">接受任何伺服器憑證 (不安全)：如果您不想檢視憑證，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="bc2ea-154">要儲存之資料行的逗號分隔清單：提供您要輸出的資料集或結果資料行清單。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="bc2ea-155">資料表名稱：指定資料表的名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="bc2ea-156">以逗號分隔的資料表資料行清單：指定要用於新資料表中的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="bc2ea-157">資料行名稱可與來源資料集中的資料行名稱不同，但您必須在此列出您為輸出資料表定義的相同數目的資料行。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="bc2ea-158">每個 SQL Azure 作業寫入的資料列數目：您可以設定在單一作業中寫入至 SQL 資料庫的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="bc2ea-159">步驟 3</span><span class="sxs-lookup"><span data-stu-id="bc2ea-159">Step 3</span></span>
1. <span data-ttu-id="bc2ea-160">按一下實驗畫布下方的 [執行]，以執行實驗。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="bc2ea-161">實驗完成時，所有模組都會呈現綠色核取標記，表示它們已順利完成。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc2ea-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc2ea-162">Next steps</span></span>
<span data-ttu-id="bc2ea-163">如需更多開發秘訣，請參閱 [SQL 資料倉儲開發概觀][SQL Data Warehouse development overview]。</span><span class="sxs-lookup"><span data-stu-id="bc2ea-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
