---
title: "使用複製精靈輕鬆地複製資料 - Azure |Microsoft Docs"
description: "了解如何使用 Data Factory 複製精靈，將資料從支援的資料來源複製到接收。"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 282cb4484f8209e6bb36f2a02d7a897f1ba0aa8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a><span data-ttu-id="a74d7-103">使用 Azure Data Factory 複製精靈輕鬆地複製或移動資料</span><span class="sxs-lookup"><span data-stu-id="a74d7-103">Copy or move data easily with Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="a74d7-104">Azure Data Factory 複製精靈會簡化內嵌資料的程序，這通常是端對端資料整合案例中的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a74d7-104">The Azure Data Factory Copy Wizard is to ease the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="a74d7-105">逐步執行 Azure Data Factory 複製精靈時，您不需要了解任何用於連結服務、資料集和管線的 JSON 定義。</span><span class="sxs-lookup"><span data-stu-id="a74d7-105">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="a74d7-106">不過，當您完成精靈中的所有步驟之後，精靈會自動建立管線，將資料從選取的資料來源複製到選取的目的地。</span><span class="sxs-lookup"><span data-stu-id="a74d7-106">However, after you complete all the steps in the wizard, the wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span></span> <span data-ttu-id="a74d7-107">此外，複製精靈可協助您驗證已在撰寫期間內嵌資料，這可節省您的許多時間，特別是當您第一次內嵌資料來源的資料時。</span><span class="sxs-lookup"><span data-stu-id="a74d7-107">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring, which saves much of your time, especially when you are ingesting data for the first time from the data source.</span></span> <span data-ttu-id="a74d7-108">若要啟動複製精靈，請在 Data Factory 首頁按一下 [複製資料]  圖格。</span><span class="sxs-lookup"><span data-stu-id="a74d7-108">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span></span>

![複製精靈](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a><span data-ttu-id="a74d7-110">直覺式的資料複製精靈</span><span class="sxs-lookup"><span data-stu-id="a74d7-110">An intuitive wizard for copying data</span></span>
<span data-ttu-id="a74d7-111">此精靈可讓您在數分鐘內輕鬆地將資料從各種來源移至目的地。</span><span class="sxs-lookup"><span data-stu-id="a74d7-111">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span></span> <span data-ttu-id="a74d7-112">逐步執行精靈之後，即會自動建立具有複製活動的管線以及相依的 Data Factory 實體 (連結的服務和資料集)。</span><span class="sxs-lookup"><span data-stu-id="a74d7-112">After going through the wizard, a pipeline with a copy activity is automatically created for you along with dependent Data Factory entities (linked services and datasets).</span></span> <span data-ttu-id="a74d7-113">不需任何額外的步驟，即可建立管線。</span><span class="sxs-lookup"><span data-stu-id="a74d7-113">No additional steps are required to create the pipeline.</span></span>   

![選取資料來源](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="a74d7-115">請參閱[複製精靈教學課程](data-factory-copy-data-wizard-tutorial.md)文章，來取得建立範例管線的逐步指示，以便將資料從 Azure Blob 複製到 Azure SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="a74d7-115">See [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md) article for step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table.</span></span> 
> 
> 

<span data-ttu-id="a74d7-116">精靈的設計之初即是以巨量資料為出發點。</span><span class="sxs-lookup"><span data-stu-id="a74d7-116">The wizard is designed with big data in mind from the start.</span></span> <span data-ttu-id="a74d7-117">它是撰寫 Data Factory 管線既簡單又有效率的方式，讓您得以使用複製資料精靈來移動數百個資料夾、檔案或資料表。</span><span class="sxs-lookup"><span data-stu-id="a74d7-117">It is simple and efficient to author Data Factory pipelines that move hundreds of folders, files, or tables using the Copy Data wizard.</span></span> <span data-ttu-id="a74d7-118">此精靈支援下列三項功能︰自動資料預覽、結構描述擷取和對應，以及篩選資料。</span><span class="sxs-lookup"><span data-stu-id="a74d7-118">The wizard supports the following three features: Automatic data preview, schema capture and mapping, and filtering data.</span></span> 

## <a name="automatic-data-preview"></a><span data-ttu-id="a74d7-119">自動資料預覽</span><span class="sxs-lookup"><span data-stu-id="a74d7-119">Automatic data preview</span></span>
<span data-ttu-id="a74d7-120">複製精靈可讓您檢閱來自所選取資料來源之資料的一部分，以驗證資料是否為您想要複製的正確資料。</span><span class="sxs-lookup"><span data-stu-id="a74d7-120">The copy wizard allows you to review part of the data from the selected data source for you to validate whether the data it is the right data you want to copy.</span></span> <span data-ttu-id="a74d7-121">此外，如果來源資料位於文字檔案中，複製精靈會自動剖析該文字檔，以了解資料列和資料行的分隔符號，以及結構描述。</span><span class="sxs-lookup"><span data-stu-id="a74d7-121">In addition, if the source data is in a text file, the copy wizard parses the text file to learn row and column delimiters, and schema automatically.</span></span> 

![檔案格式設定](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="a74d7-123">結構描述擷取和對應</span><span class="sxs-lookup"><span data-stu-id="a74d7-123">Schema capture and mapping</span></span>
<span data-ttu-id="a74d7-124">在某些情況下，輸入資料的結構描述可能不符合輸出資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="a74d7-124">The schema of input data may not match the schema of output data in some cases.</span></span> <span data-ttu-id="a74d7-125">在此案例中，您需要將來源結構描述的資料行對應到目的地結構描述的資料行。</span><span class="sxs-lookup"><span data-stu-id="a74d7-125">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span> 

<span data-ttu-id="a74d7-126">複製精靈會自動將來源結構描述中的資料行對應到目的地結構描述中的資料行。</span><span class="sxs-lookup"><span data-stu-id="a74d7-126">The copy wizard automatically maps columns in the source schema to columns in the destination schema.</span></span> <span data-ttu-id="a74d7-127">您可以使用下拉式清單來覆寫對應 (或) 指定在複製資料時是否必須略過資料行。</span><span class="sxs-lookup"><span data-stu-id="a74d7-127">You can override the mappings by using the drop-down lists (or) specify whether a column needs to be skipped while copying the data.</span></span>   

![結構描述對應](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="a74d7-129">篩選資料</span><span class="sxs-lookup"><span data-stu-id="a74d7-129">Filtering data</span></span>
<span data-ttu-id="a74d7-130">此精靈可讓您篩選來源資料，只選取需要複製到目的地/接收資料存放區的資料。</span><span class="sxs-lookup"><span data-stu-id="a74d7-130">The wizard allows you to filter source data to select only the data that needs to be copied to the destination/sink data store.</span></span> <span data-ttu-id="a74d7-131">篩選可減少要複製到接收資料存放區的資料，因此可增強複製作業的輸送量。</span><span class="sxs-lookup"><span data-stu-id="a74d7-131">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="a74d7-132">它提供一種彈性方式，藉由使用 SQL 查詢語言來篩選關聯式資料庫中的資料 (或) 使用 [Data Factory 函式與變數](data-factory-functions-variables.md)來篩選 Azure Blob 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a74d7-132">It provides a flexible way to filter data in a relational database by using SQL query language (or) files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="a74d7-133">篩選資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="a74d7-133">Filtering of data in a database</span></span>
<span data-ttu-id="a74d7-134">在此範例中，SQL 查詢會使用 `Text.Format` 函式與 `WindowStart` 變數。</span><span class="sxs-lookup"><span data-stu-id="a74d7-134">In the example, the SQL query uses the `Text.Format` function and `WindowStart` variable.</span></span> 

![驗證運算式](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="a74d7-136">篩選 Azure Blob 資料夾中的資料</span><span class="sxs-lookup"><span data-stu-id="a74d7-136">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="a74d7-137">您可以在資料夾路徑中使用變數，以複製在執行階段根據[系統變數](data-factory-functions-variables.md#data-factory-system-variables)決定之資料夾內的資料。</span><span class="sxs-lookup"><span data-stu-id="a74d7-137">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="a74d7-138">支援的變數包括︰**{year}**、**{month}**、**{day}**、**{hour}**、**{minute}** 及 **{custom}**。</span><span class="sxs-lookup"><span data-stu-id="a74d7-138">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="a74d7-139">範例︰inputfolder/{year}/{month}/{day}。</span><span class="sxs-lookup"><span data-stu-id="a74d7-139">Example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="a74d7-140">假設您的輸入資料夾格式如下︰</span><span class="sxs-lookup"><span data-stu-id="a74d7-140">Suppose that you have input folders in the following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="a74d7-141">按一下 [檔案或資料夾] 的 [瀏覽] 按鈕、瀏覽至其中一個資料夾 (例如 2016->03->01->02)，然後按一下 [選擇]。</span><span class="sxs-lookup"><span data-stu-id="a74d7-141">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="a74d7-142">您應該會在文字方塊中看到 `2016/03/01/02`。</span><span class="sxs-lookup"><span data-stu-id="a74d7-142">You should see `2016/03/01/02` in the text box.</span></span> <span data-ttu-id="a74d7-143">現在，將 **2016** 取代為 **{year}**、**03** 取代為 **{month}**、**01** 取代為 **{day}**，以及 **02** 取代為 **{hour}**，然後按 Tab 鍵。</span><span class="sxs-lookup"><span data-stu-id="a74d7-143">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press Tab.</span></span> <span data-ttu-id="a74d7-144">您應該會看到選取這四個變數之格式的下拉式清單︰</span><span class="sxs-lookup"><span data-stu-id="a74d7-144">You should see drop-down lists to select the format for these four variables:</span></span>

![使用系統變數](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="a74d7-146">如下列螢幕擷取畫面所示，您也可以使用 **custom** 變數和任何[支援的格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a74d7-146">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="a74d7-147">若要選取具有該結構的資料夾，請先使用 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a74d7-147">To select a folder with that structure, use the **Browse** button first.</span></span> <span data-ttu-id="a74d7-148">然後將值取代為 **{custom}**，並按 Tab 鍵來查看可輸入格式字串的文字方塊。</span><span class="sxs-lookup"><span data-stu-id="a74d7-148">Then replace a value with **{custom}**, and press Tab to see the text box where you can type the format string.</span></span>     

![使用自訂變數](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a><span data-ttu-id="a74d7-150">支援多樣化資料和物件類型</span><span class="sxs-lookup"><span data-stu-id="a74d7-150">Support for diverse data and object types</span></span>
<span data-ttu-id="a74d7-151">使用複製精靈，您可以有效率地移動數百個資料夾、檔案或資料表。</span><span class="sxs-lookup"><span data-stu-id="a74d7-151">By using the Copy Wizard, you can efficiently move hundreds of folders, files, or tables.</span></span>

![選取要從中複製資料的資料表](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a><span data-ttu-id="a74d7-153">排程選項</span><span class="sxs-lookup"><span data-stu-id="a74d7-153">Scheduling options</span></span>
<span data-ttu-id="a74d7-154">您可以執行複製作業一次，或按照排程 (每小時、每日等) 執行。</span><span class="sxs-lookup"><span data-stu-id="a74d7-154">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="a74d7-155">這兩個選項均適用於範圍跨越內部部署、雲端和本機桌面複本的廣闊連接器。</span><span class="sxs-lookup"><span data-stu-id="a74d7-155">Both of these options can be used for the breadth of the connectors across on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="a74d7-156">一次性複製作業只能進行一次從來源到目的地的資料移動。</span><span class="sxs-lookup"><span data-stu-id="a74d7-156">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="a74d7-157">它適用於任何規模和任何支援格式的資料。</span><span class="sxs-lookup"><span data-stu-id="a74d7-157">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="a74d7-158">排程複製可讓您依照指定的週期複製資料。</span><span class="sxs-lookup"><span data-stu-id="a74d7-158">The scheduled copy allows you to copy data on a prescribed recurrence.</span></span> <span data-ttu-id="a74d7-159">在設定排程複製時，您可以使用豐富的設定 (如重試、逾時和警示)。</span><span class="sxs-lookup"><span data-stu-id="a74d7-159">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![排程屬性](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="a74d7-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a74d7-161">Next steps</span></span>
<span data-ttu-id="a74d7-162">如需使用 Data Factory 複製精靈建立含複製活動之管線的快速逐步解說，請參閱 [教學課程：使用 Data Factory 複製精靈建立具有複製活動的管線](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="a74d7-162">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

