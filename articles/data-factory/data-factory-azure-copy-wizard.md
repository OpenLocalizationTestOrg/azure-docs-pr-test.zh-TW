---
title: "aaaData Factory Azure 複本精靈 |Microsoft 文件"
description: "深入了解如何 toouse hello 資料 Factory Azure 複本精靈支援的資料來源 toosinks toocopy 資料。"
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
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a><span data-ttu-id="d37e1-103">Azure Data Factory 複製精靈</span><span class="sxs-lookup"><span data-stu-id="d37e1-103">Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="d37e1-104">hello Azure 資料 Factory 複製精靈減輕 hello 的擷取資料，通常是在端對端資料整合案例中的第一個步驟的程序。</span><span class="sxs-lookup"><span data-stu-id="d37e1-104">hello Azure Data Factory Copy Wizard eases hello process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="d37e1-105">當經過 hello Azure 資料 Factory 複製精靈，您不需要 toounderstand 任何 JSON 定義連結的服務、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="d37e1-105">When going through hello Azure Data Factory Copy Wizard, you do not need toounderstand any JSON definitions for linked services, data sets, and pipelines.</span></span> <span data-ttu-id="d37e1-106">hello 精靈會自動建立管線 toocopy 資料，從 hello 選取的資料來源 toohello 選取目的地。</span><span class="sxs-lookup"><span data-stu-id="d37e1-106">hello wizard automatically creates a pipeline toocopy data from hello selected data source toohello selected destination.</span></span> <span data-ttu-id="d37e1-107">此外，hello 複製精靈可協助您 toovalidate hello 資料內嵌在 hello 階段撰寫的。</span><span class="sxs-lookup"><span data-stu-id="d37e1-107">In addition, hello Copy Wizard helps you toovalidate hello data being ingested at hello time of authoring.</span></span> <span data-ttu-id="d37e1-108">這可以節省時間，特別當您會擷取資料的 hello 第一次 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="d37e1-108">This saves time, especially when you are ingesting data for hello first time from hello data source.</span></span> <span data-ttu-id="d37e1-109">toostart hello 複製精靈中，按一下 hello**將資料複製**的 data factory 的 hello 首頁上並排顯示。</span><span class="sxs-lookup"><span data-stu-id="d37e1-109">toostart hello Copy Wizard, click hello **Copy data** tile on hello home page of your data factory.</span></span>

![複製精靈](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a><span data-ttu-id="d37e1-111">針對巨量資料設計</span><span class="sxs-lookup"><span data-stu-id="d37e1-111">Designed for big data</span></span>
<span data-ttu-id="d37e1-112">此精靈可讓您從各種來源 toodestinations tooeasily 移動資料以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="d37e1-112">This wizard allows you tooeasily move data from a wide variety of sources toodestinations in minutes.</span></span> <span data-ttu-id="d37e1-113">您瀏覽 hello 精靈之後，具有複製活動的管線會自動為您建立，以及相依的 Data Factory 實體 （連結的服務和資料集）。</span><span class="sxs-lookup"><span data-stu-id="d37e1-113">After you go through hello wizard, a pipeline with a copy activity is automatically created for you, along with dependent Data Factory entities (linked services and data sets).</span></span> <span data-ttu-id="d37e1-114">不不需要的 toocreate hello 管線的任何額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="d37e1-114">No additional steps are required toocreate hello pipeline.</span></span>   

![選取資料來源](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="d37e1-116">如需逐步指示 toocreate 範例管線 toocopy 資料從 Azure blob tooan Azure SQL Database 的資料表，請參閱 hello[複製精靈教學課程](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="d37e1-116">For step-by-step instructions toocreate a sample pipeline toocopy data from an Azure blob tooan Azure SQL Database table, see hello [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md).</span></span>
>
>

<span data-ttu-id="d37e1-117">hello 精靈被設計大型的資料，請注意，從 hello 開始，並且支援各種不同的資料和物件類型。</span><span class="sxs-lookup"><span data-stu-id="d37e1-117">hello wizard is designed with big data in mind from hello start, with support for diverse data and object types.</span></span> <span data-ttu-id="d37e1-118">您可以撰寫 Data Factory 管線，移動數百個資料夾、檔案或資料表。</span><span class="sxs-lookup"><span data-stu-id="d37e1-118">You can author Data Factory pipelines that move hundreds of folders, files, or tables.</span></span> <span data-ttu-id="d37e1-119">hello 精靈支援自動資料預覽、 擷取結構描述和對應，以及資料篩選。</span><span class="sxs-lookup"><span data-stu-id="d37e1-119">hello wizard supports automatic data preview, schema capture and mapping, and data filtering.</span></span>

## <a name="automatic-data-preview"></a><span data-ttu-id="d37e1-120">自動資料預覽</span><span class="sxs-lookup"><span data-stu-id="d37e1-120">Automatic data preview</span></span>
<span data-ttu-id="d37e1-121">您可以在 hello 資料是您想要預覽 hello 選取的資料來源中的順序 toovalidate hello 資料的一部分 toocopy。</span><span class="sxs-lookup"><span data-stu-id="d37e1-121">You can preview part of hello data from hello selected data source in order toovalidate whether hello data is what you want toocopy.</span></span> <span data-ttu-id="d37e1-122">此外，如果 hello 來源資料是文字檔案中，複製精靈 hello 剖析 hello 文字檔案 toolearn hello 資料列和資料行分隔符號和結構描述自動。</span><span class="sxs-lookup"><span data-stu-id="d37e1-122">In addition, if hello source data is in a text file, hello Copy Wizard parses hello text file toolearn hello row and column delimiters and schema automatically.</span></span>

![檔案格式設定](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="d37e1-124">結構描述擷取和對應</span><span class="sxs-lookup"><span data-stu-id="d37e1-124">Schema capture and mapping</span></span>
<span data-ttu-id="d37e1-125">hello 結構描述的輸入資料可能不符合輸出資料，在某些情況下 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="d37e1-125">hello schema of input data may not match hello schema of output data in some cases.</span></span> <span data-ttu-id="d37e1-126">在此案例中，您需要 toomap hello 來源結構描述 toocolumns 從 hello 目的地結構描述中的資料行。</span><span class="sxs-lookup"><span data-stu-id="d37e1-126">In this scenario, you need toomap columns from hello source schema toocolumns from hello destination schema.</span></span>

> [!TIP]
> <span data-ttu-id="d37e1-127">當複製資料的 SQL Server 或 Azure SQL Database 到 Azure SQL 資料倉儲，如果 hello 資料表不存在於 hello 目的地存放區，Data Factory 支援自動建立資料表使用來源的結構描述。</span><span class="sxs-lookup"><span data-stu-id="d37e1-127">When copying data from SQL Server or Azure SQL Database into Azure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory support auto table creation using source's schema.</span></span> <span data-ttu-id="d37e1-128">進一步了解從[從 Azure SQL 資料倉儲使用 Azure Data Factory 中移動資料 tooand](./data-factory-azure-sql-data-warehouse-connector.md)。</span><span class="sxs-lookup"><span data-stu-id="d37e1-128">Learn more from [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](./data-factory-azure-sql-data-warehouse-connector.md).</span></span>
>

<span data-ttu-id="d37e1-129">Hello 目的結構描述中，使用下拉式清單 tooselect hello 來源結構描述 toomap tooa 資料行中的資料行。</span><span class="sxs-lookup"><span data-stu-id="d37e1-129">Use a drop-down list tooselect a column from hello source schema toomap tooa column in hello destination schema.</span></span> <span data-ttu-id="d37e1-130">hello 複製精靈會嘗試 toounderstand 您的資料行對應的模式。</span><span class="sxs-lookup"><span data-stu-id="d37e1-130">hello Copy Wizard tries toounderstand your pattern for column mapping.</span></span> <span data-ttu-id="d37e1-131">它適用於的 hello 相同模式 toohello 其餘部分的 hello 資料行，因此，您不需要 tooselect 每個 hello 資料行個別 toocomplete hello 結構描述對應。</span><span class="sxs-lookup"><span data-stu-id="d37e1-131">It applies hello same pattern toohello rest of hello columns, so that you do not need tooselect each of hello columns individually toocomplete hello schema mapping.</span></span> <span data-ttu-id="d37e1-132">如果您想要的話，您可以使用 hello 下拉式清單 toomap hello 資料行一個覆寫這些對應。</span><span class="sxs-lookup"><span data-stu-id="d37e1-132">If you prefer, you can override these mappings by using hello drop-down lists toomap hello columns one by one.</span></span> <span data-ttu-id="d37e1-133">hello 模式會變成更精確，因為您將多個資料行的對應。</span><span class="sxs-lookup"><span data-stu-id="d37e1-133">hello pattern becomes more accurate as you map more columns.</span></span> <span data-ttu-id="d37e1-134">hello 複製精靈不斷地更新 hello 模式，最後到達 hello 右模式 hello 資料行對應您想要 tooachieve。</span><span class="sxs-lookup"><span data-stu-id="d37e1-134">hello Copy Wizard constantly updates hello pattern, and ultimately reaches hello right pattern for hello column mapping you want tooachieve.</span></span>     

![結構描述對應](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="d37e1-136">篩選資料</span><span class="sxs-lookup"><span data-stu-id="d37e1-136">Filtering data</span></span>
<span data-ttu-id="d37e1-137">您可以篩選來源資料 tooselect 只有 hello 資料需要複製 toobe toohello 接收資料存放區。</span><span class="sxs-lookup"><span data-stu-id="d37e1-137">You can filter source data tooselect only hello data that needs toobe copied toohello sink data store.</span></span> <span data-ttu-id="d37e1-138">篩選可降低 hello hello 資料 toobe 複製的 toohello 接收的資料儲存和因此增強 hello 輸送量 hello 複製作業的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="d37e1-138">Filtering reduces hello volume of hello data toobe copied toohello sink data store and therefore enhances hello throughput of hello copy operation.</span></span> <span data-ttu-id="d37e1-139">它提供彈性方式 toofilter 資料關聯式資料庫中的使用 hello SQL 查詢語言，或使用 Azure blob 資料夾中檔案[Data Factory 函式和變數](data-factory-functions-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="d37e1-139">It provides a flexible way toofilter data in a relational database by using hello SQL query language, or files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="d37e1-140">篩選資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="d37e1-140">Filtering of data in a database</span></span>
<span data-ttu-id="d37e1-141">hello 下列螢幕擷取畫面顯示 SQL 查詢使用 hello`Text.Format`函式和`WindowStart`變數。</span><span class="sxs-lookup"><span data-stu-id="d37e1-141">hello following screenshot shows a SQL query using hello `Text.Format` function and `WindowStart` variable.</span></span>

![驗證運算式](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="d37e1-143">篩選 Azure Blob 資料夾中的資料</span><span class="sxs-lookup"><span data-stu-id="d37e1-143">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="d37e1-144">您可以在 hello 資料夾路徑 toocopy 資料由決定在執行階段為基礎的資料夾中使用變數[系統變數](data-factory-functions-variables.md#data-factory-system-variables)。</span><span class="sxs-lookup"><span data-stu-id="d37e1-144">You can use variables in hello folder path toocopy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="d37e1-145">支援的 hello 變數是： **{year}**， **{month}**， **{day}**， **{小時}**， **{分鐘}**，和**{自訂}**。</span><span class="sxs-lookup"><span data-stu-id="d37e1-145">hello supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="d37e1-146">例如︰inputfolder/{year}/{month}/{day}。</span><span class="sxs-lookup"><span data-stu-id="d37e1-146">For example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="d37e1-147">假設您有輸入 hello 遵循格式中的資料夾：</span><span class="sxs-lookup"><span data-stu-id="d37e1-147">Suppose that you have input folders in hello following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="d37e1-148">按一下 hello**瀏覽**按鈕**檔案或資料夾**，瀏覽這些資料夾 tooone (比方說，2016年-> 03-> 01-> 02)，按一下**選擇**。</span><span class="sxs-lookup"><span data-stu-id="d37e1-148">Click hello **Browse** button for **File or folder**, browse tooone of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="d37e1-149">您應該會看到`2016/03/01/02`hello 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d37e1-149">You should see `2016/03/01/02` in hello text box.</span></span> <span data-ttu-id="d37e1-150">現在，取代**2016年**與**{year}**， **03**與**{month}**， **01**與**{day}**，和**02**與**{小時}**，並按 hello  **索引標籤**索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d37e1-150">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press hello **Tab** key.</span></span> <span data-ttu-id="d37e1-151">您應該會看到這些四個變數的下拉式清單 tooselect hello 格式：</span><span class="sxs-lookup"><span data-stu-id="d37e1-151">You should see drop-down lists tooselect hello format for these four variables:</span></span>

![使用系統變數](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="d37e1-153">Hello 下列螢幕擷取畫面所示，您也可以使用**自訂**變數和任何[支援格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d37e1-153">As shown in hello following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="d37e1-154">tooselect 資料夾與該結構中，使用 hello**瀏覽**按鈕第一次。</span><span class="sxs-lookup"><span data-stu-id="d37e1-154">tooselect a folder with that structure, use hello **Browse** button first.</span></span> <span data-ttu-id="d37e1-155">然後取代的值為**{自訂}**，並按 hello  **索引標籤**金鑰 toosee hello 文字方塊中，您可以在這裡輸入 hello 格式字串。</span><span class="sxs-lookup"><span data-stu-id="d37e1-155">Then replace a value with **{custom}**, and press hello **Tab** key toosee hello text box where you can type hello format string.</span></span>     

![使用自訂變數](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a><span data-ttu-id="d37e1-157">排程選項</span><span class="sxs-lookup"><span data-stu-id="d37e1-157">Scheduling options</span></span>
<span data-ttu-id="d37e1-158">您可以執行 hello 複製作業一次，或根據排程 （每小時、 每天，依此類推）。</span><span class="sxs-lookup"><span data-stu-id="d37e1-158">You can run hello copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="d37e1-159">這兩個選項可以用於 hello 範圍的環境，包括在內部部署、 雲端和本機桌面複製 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="d37e1-159">Both of these options can be used for hello breadth of hello connectors across environments, including on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="d37e1-160">一次性複製作業可讓從來源 tooa 目的地的資料移動一次。</span><span class="sxs-lookup"><span data-stu-id="d37e1-160">A one-time copy operation enables data movement from a source tooa destination only once.</span></span> <span data-ttu-id="d37e1-161">它適用於 toodata 任何大小和任何支援的格式。</span><span class="sxs-lookup"><span data-stu-id="d37e1-161">It applies toodata of any size and any supported format.</span></span> <span data-ttu-id="d37e1-162">排程的 hello 複製可讓您 toocopy 資料上規定的循環。</span><span class="sxs-lookup"><span data-stu-id="d37e1-162">hello scheduled copy allows you toocopy data on a prescribed recurrence.</span></span> <span data-ttu-id="d37e1-163">您可以使用 （例如重試、 逾時和警示） 的豐富設定 tooconfigure hello 排程複製。</span><span class="sxs-lookup"><span data-stu-id="d37e1-163">You can use rich settings (like retry, timeout, and alerts) tooconfigure hello scheduled copy.</span></span>

![排程屬性](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="d37e1-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d37e1-165">Next steps</span></span>
<span data-ttu-id="d37e1-166">使用複製活動與 hello 資料 Factory 複製精靈 toocreate 管線快速逐步解說，請參閱[教學課程： 建立管線中使用 hello 複製精靈](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="d37e1-166">For a quick walkthrough of using hello Data Factory Copy Wizard toocreate a pipeline with Copy Activity, see [Tutorial: Create a pipeline using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>
