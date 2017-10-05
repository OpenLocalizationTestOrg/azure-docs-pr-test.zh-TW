---
title: "Azure Data Factory 複製精靈 | Microsoft Docs"
description: "了解如何使用 Azure Data Factory 複製精靈，將資料從支援的資料來源複製到接收。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 53eaa650308979bc0953a6403baf1fd1b86f7420
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-factory-copy-wizard"></a><span data-ttu-id="5c50d-103">Azure Data Factory 複製精靈</span><span class="sxs-lookup"><span data-stu-id="5c50d-103">Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="5c50d-104">Azure Data Factory 複製精靈簡化內嵌資料的程序，這通常是端對端資料整合案例中的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="5c50d-104">The Azure Data Factory Copy Wizard eases the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="5c50d-105">逐步執行 Azure Data Factory 複製精靈時，您不需要了解任何用於連結服務、資料集和管線的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="5c50d-105">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, data sets, and pipelines.</span></span> <span data-ttu-id="5c50d-106">精靈會自動建立管線，將資料從選取的資料來源複製到選取的目的地。</span><span class="sxs-lookup"><span data-stu-id="5c50d-106">The wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span></span> <span data-ttu-id="5c50d-107">此外，複製精靈可協助您在撰寫時驗證內嵌的資料。</span><span class="sxs-lookup"><span data-stu-id="5c50d-107">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring.</span></span> <span data-ttu-id="5c50d-108">這樣可節省時間，尤其是當您第一次從資料來源內嵌資料時更是如此。</span><span class="sxs-lookup"><span data-stu-id="5c50d-108">This saves time, especially when you are ingesting data for the first time from the data source.</span></span> <span data-ttu-id="5c50d-109">若要啟動複製精靈，請在 Data Factory 首頁按一下 [複製資料]  圖格。</span><span class="sxs-lookup"><span data-stu-id="5c50d-109">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span></span>

![複製精靈](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a><span data-ttu-id="5c50d-111">針對巨量資料設計</span><span class="sxs-lookup"><span data-stu-id="5c50d-111">Designed for big data</span></span>
<span data-ttu-id="5c50d-112">此精靈可讓您在數分鐘內輕鬆地將資料從各種來源移至目的地。</span><span class="sxs-lookup"><span data-stu-id="5c50d-112">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span></span> <span data-ttu-id="5c50d-113">逐步執行精靈之後，即會自動建立具有複製活動的管線以及相依的 Data Factory 實體 (連結的服務和資料集)。</span><span class="sxs-lookup"><span data-stu-id="5c50d-113">After you go through the wizard, a pipeline with a copy activity is automatically created for you, along with dependent Data Factory entities (linked services and data sets).</span></span> <span data-ttu-id="5c50d-114">不需任何額外的步驟，即可建立管線。</span><span class="sxs-lookup"><span data-stu-id="5c50d-114">No additional steps are required to create the pipeline.</span></span>   

![選取資料來源](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="5c50d-116">如需取得建立範例管線以便將資料從 Azure Blob 複製到 Azure SQL Database 資料表的逐步指示，請參閱[複製精靈教學課程](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="5c50d-116">For step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table, see the [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md).</span></span>
>
>

<span data-ttu-id="5c50d-117">精靈從一開始就針對巨量資料而設計，並且支援多樣化資料和物件類型。</span><span class="sxs-lookup"><span data-stu-id="5c50d-117">The wizard is designed with big data in mind from the start, with support for diverse data and object types.</span></span> <span data-ttu-id="5c50d-118">您可以撰寫 Data Factory 管線，移動數百個資料夾、檔案或資料表。</span><span class="sxs-lookup"><span data-stu-id="5c50d-118">You can author Data Factory pipelines that move hundreds of folders, files, or tables.</span></span> <span data-ttu-id="5c50d-119">精靈支援自動資料預覽、結構描述擷取和對應，以及資料篩選。</span><span class="sxs-lookup"><span data-stu-id="5c50d-119">The wizard supports automatic data preview, schema capture and mapping, and data filtering.</span></span>

## <a name="automatic-data-preview"></a><span data-ttu-id="5c50d-120">自動資料預覽</span><span class="sxs-lookup"><span data-stu-id="5c50d-120">Automatic data preview</span></span>
<span data-ttu-id="5c50d-121">您可以預覽一部分選取的資料來源以驗證資料是否是您要複製的資料。</span><span class="sxs-lookup"><span data-stu-id="5c50d-121">You can preview part of the data from the selected data source in order to validate whether the data is what you want to copy.</span></span> <span data-ttu-id="5c50d-122">此外，如果來源資料位於文字檔案中，複製精靈會自動剖析該文字檔，以了解資料列和資料行的分隔符號，以及結構描述。</span><span class="sxs-lookup"><span data-stu-id="5c50d-122">In addition, if the source data is in a text file, the Copy Wizard parses the text file to learn the row and column delimiters and schema automatically.</span></span>

![檔案格式設定](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="5c50d-124">結構描述擷取和對應</span><span class="sxs-lookup"><span data-stu-id="5c50d-124">Schema capture and mapping</span></span>
<span data-ttu-id="5c50d-125">在某些情況下，輸入資料的結構描述可能不符合輸出資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="5c50d-125">The schema of input data may not match the schema of output data in some cases.</span></span> <span data-ttu-id="5c50d-126">在此案例中，您需要將來源結構描述的資料行對應到目的地結構描述的資料行。</span><span class="sxs-lookup"><span data-stu-id="5c50d-126">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span>

> [!TIP]
> <span data-ttu-id="5c50d-127">從 SQL Server 或 Azure SQL Database 中將資料複製到 Azure SQL 資料倉儲時，如果目的地存放區中沒有資料表，Data Factory 支援使用來源的結構描述來自動建立資料表。</span><span class="sxs-lookup"><span data-stu-id="5c50d-127">When copying data from SQL Server or Azure SQL Database into Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory support auto table creation using source's schema.</span></span> <span data-ttu-id="5c50d-128">深入了解[使用 Azure Data Factory 從 Azure SQL 資料倉儲來回移動資料](./data-factory-azure-sql-data-warehouse-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="5c50d-128">Learn more from [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).</span></span>
>

<span data-ttu-id="5c50d-129">請使用下拉式清單選取來源結構描述的資料行來對應至目的地結構描述中的資料行。</span><span class="sxs-lookup"><span data-stu-id="5c50d-129">Use a drop-down list to select a column from the source schema to map to a column in the destination schema.</span></span> <span data-ttu-id="5c50d-130">複製精靈會嘗試了解資料行對應的模式，</span><span class="sxs-lookup"><span data-stu-id="5c50d-130">The Copy Wizard tries to understand your pattern for column mapping.</span></span> <span data-ttu-id="5c50d-131">並且對其餘的資料行套用相同的模式，所以您不需要個別選取每個資料行就能完成結構描述對應。</span><span class="sxs-lookup"><span data-stu-id="5c50d-131">It applies the same pattern to the rest of the columns, so that you do not need to select each of the columns individually to complete the schema mapping.</span></span> <span data-ttu-id="5c50d-132">如果想要，還是可以使用下拉式清單逐一對應資料行來覆寫這些對應。</span><span class="sxs-lookup"><span data-stu-id="5c50d-132">If you prefer, you can override these mappings by using the drop-down lists to map the columns one by one.</span></span> <span data-ttu-id="5c50d-133">您對應越多資料行，模式就會變得越精確。</span><span class="sxs-lookup"><span data-stu-id="5c50d-133">The pattern becomes more accurate as you map more columns.</span></span> <span data-ttu-id="5c50d-134">複製精靈會持續更新模式，直到達到您想要達成的資料行對應的正確模式。</span><span class="sxs-lookup"><span data-stu-id="5c50d-134">The Copy Wizard constantly updates the pattern, and ultimately reaches the right pattern for the column mapping you want to achieve.</span></span>     

![結構描述對應](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="5c50d-136">篩選資料</span><span class="sxs-lookup"><span data-stu-id="5c50d-136">Filtering data</span></span>
<span data-ttu-id="5c50d-137">您可以篩選來源資料，只選取需要複製到接收資料存放區的資料。</span><span class="sxs-lookup"><span data-stu-id="5c50d-137">You can filter source data to select only the data that needs to be copied to the sink data store.</span></span> <span data-ttu-id="5c50d-138">篩選可減少要複製到接收資料存放區的資料，因此可增強複製作業的輸送量。</span><span class="sxs-lookup"><span data-stu-id="5c50d-138">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="5c50d-139">它提供一種彈性方式，藉由使用 SQL 查詢語言來篩選關聯式資料庫中的資料，或使用 [Data Factory 函式與變數](data-factory-functions-variables.md)來篩選 Azure Blob 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="5c50d-139">It provides a flexible way to filter data in a relational database by using the SQL query language, or files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="5c50d-140">篩選資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="5c50d-140">Filtering of data in a database</span></span>
<span data-ttu-id="5c50d-141">下列螢幕擷取畫面顯示使用 `Text.Format` 函式和 `WindowStart` 變數的 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="5c50d-141">The following screenshot shows a SQL query using the `Text.Format` function and `WindowStart` variable.</span></span>

![驗證運算式](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="5c50d-143">篩選 Azure Blob 資料夾中的資料</span><span class="sxs-lookup"><span data-stu-id="5c50d-143">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="5c50d-144">您可以在資料夾路徑中使用變數，以複製在執行階段根據[系統變數](data-factory-functions-variables.md#data-factory-system-variables)決定之資料夾內的資料。</span><span class="sxs-lookup"><span data-stu-id="5c50d-144">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="5c50d-145">支援的變數包括︰**{year}**、**{month}**、**{day}**、**{hour}**、**{minute}** 及 **{custom}**。</span><span class="sxs-lookup"><span data-stu-id="5c50d-145">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="5c50d-146">例如︰inputfolder/{year}/{month}/{day}。</span><span class="sxs-lookup"><span data-stu-id="5c50d-146">For example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="5c50d-147">假設您的輸入資料夾格式如下︰</span><span class="sxs-lookup"><span data-stu-id="5c50d-147">Suppose that you have input folders in the following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="5c50d-148">按一下 [檔案或資料夾] 的 [瀏覽] 按鈕、瀏覽至其中一個資料夾 (例如 2016->03->01->02)，然後按一下 [選擇]。</span><span class="sxs-lookup"><span data-stu-id="5c50d-148">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="5c50d-149">您應該會在文字方塊中看到 `2016/03/01/02`。</span><span class="sxs-lookup"><span data-stu-id="5c50d-149">You should see `2016/03/01/02` in the text box.</span></span> <span data-ttu-id="5c50d-150">現在，將 **2016** 取代為 **{year}**、**03** 取代為 **{month}**、**01** 取代為 **{day}**，以及 **02** 取代為 **{hour}**，然後按 **Tab** 鍵。</span><span class="sxs-lookup"><span data-stu-id="5c50d-150">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press the **Tab** key.</span></span> <span data-ttu-id="5c50d-151">您應該會看到選取這四個變數之格式的下拉式清單︰</span><span class="sxs-lookup"><span data-stu-id="5c50d-151">You should see drop-down lists to select the format for these four variables:</span></span>

![使用系統變數](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="5c50d-153">如下列螢幕擷取畫面所示，您也可以使用 **custom** 變數和任何[支援的格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5c50d-153">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="5c50d-154">若要選取具有該結構的資料夾，請先使用 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5c50d-154">To select a folder with that structure, use the **Browse** button first.</span></span> <span data-ttu-id="5c50d-155">然後將值取代為 **{custom}**，並按 **Tab** 鍵來查看可輸入格式字串的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5c50d-155">Then replace a value with **{custom}**, and press the **Tab** key to see the text box where you can type the format string.</span></span>     

![使用自訂變數](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a><span data-ttu-id="5c50d-157">排程選項</span><span class="sxs-lookup"><span data-stu-id="5c50d-157">Scheduling options</span></span>
<span data-ttu-id="5c50d-158">您可以執行複製作業一次，或按照排程 (每小時、每日等) 執行。</span><span class="sxs-lookup"><span data-stu-id="5c50d-158">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="5c50d-159">這兩個選項均適用於跨環境的廣闊連接器，包括內部部署、雲端和本機桌面複本。</span><span class="sxs-lookup"><span data-stu-id="5c50d-159">Both of these options can be used for the breadth of the connectors across environments, including on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="5c50d-160">一次性複製作業只能進行一次從來源到目的地的資料移動。</span><span class="sxs-lookup"><span data-stu-id="5c50d-160">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="5c50d-161">它適用於任何規模和任何支援格式的資料。</span><span class="sxs-lookup"><span data-stu-id="5c50d-161">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="5c50d-162">排程複製可讓您依照指定的週期複製資料。</span><span class="sxs-lookup"><span data-stu-id="5c50d-162">The scheduled copy allows you to copy data on a prescribed recurrence.</span></span> <span data-ttu-id="5c50d-163">在設定排程複製時，您可以使用豐富的設定 (如重試、逾時和警示)。</span><span class="sxs-lookup"><span data-stu-id="5c50d-163">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![排程屬性](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="5c50d-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5c50d-165">Next steps</span></span>
<span data-ttu-id="5c50d-166">如需使用 Data Factory 複製精靈建立含複製活動之管線的快速逐步解說，請參閱 [教學課程：使用 Data Factory 複製精靈建立具有複製活動的管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="5c50d-166">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>
