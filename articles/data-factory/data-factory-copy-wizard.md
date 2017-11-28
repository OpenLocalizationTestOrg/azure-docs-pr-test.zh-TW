---
title: "輕鬆地複製精靈-Azure aaaCopy 資料 |Microsoft 文件"
description: "深入了解如何 toouse hello 資料 Factory 複製精靈支援的資料來源 toosinks toocopy 資料。"
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
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a><span data-ttu-id="d08a8-103">使用 Azure Data Factory 複製精靈輕鬆地複製或移動資料</span><span class="sxs-lookup"><span data-stu-id="d08a8-103">Copy or move data easily with Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="d08a8-104">hello Azure 資料 Factory 複製精靈是 tooease hello 程序擷取資料，通常是在端對端資料整合案例中的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="d08a8-104">hello Azure Data Factory Copy Wizard is tooease hello process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="d08a8-105">當經過 hello Azure 資料 Factory 複製精靈，您不需要 toounderstand 任何 JSON 定義連結的服務、 資料集和管線。</span><span class="sxs-lookup"><span data-stu-id="d08a8-105">When going through hello Azure Data Factory Copy Wizard, you do not need toounderstand any JSON definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="d08a8-106">不過，完成所有 hello 精靈 中的 hello 步驟之後，hello 精靈會自動建立管線 toocopy 資料從 hello 選取的資料來源 toohello 選取目的地。</span><span class="sxs-lookup"><span data-stu-id="d08a8-106">However, after you complete all hello steps in hello wizard, hello wizard automatically creates a pipeline toocopy data from hello selected data source toohello selected destination.</span></span> <span data-ttu-id="d08a8-107">此外，hello 複製精靈可協助您 toovalidate hello 資料內嵌在 hello 階段撰寫，正在以節省許多時間，特別當您會擷取 hello 資料第一次 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="d08a8-107">In addition, hello Copy Wizard helps you toovalidate hello data being ingested at hello time of authoring, which saves much of your time, especially when you are ingesting data for hello first time from hello data source.</span></span> <span data-ttu-id="d08a8-108">toostart hello 複製精靈中，按一下 hello**將資料複製**的 data factory 的 hello 首頁上並排顯示。</span><span class="sxs-lookup"><span data-stu-id="d08a8-108">toostart hello Copy Wizard, click hello **Copy data** tile on hello home page of your data factory.</span></span>

![複製精靈](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a><span data-ttu-id="d08a8-110">直覺式的資料複製精靈</span><span class="sxs-lookup"><span data-stu-id="d08a8-110">An intuitive wizard for copying data</span></span>
<span data-ttu-id="d08a8-111">此精靈可讓您從各種來源 toodestinations tooeasily 移動資料以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="d08a8-111">This wizard allows you tooeasily move data from a wide variety of sources toodestinations in minutes.</span></span> <span data-ttu-id="d08a8-112">之後經過 hello 精靈，具有複製活動的管線會自動為您建立以及相依的 Data Factory 實體 （連結的服務和資料集）。</span><span class="sxs-lookup"><span data-stu-id="d08a8-112">After going through hello wizard, a pipeline with a copy activity is automatically created for you along with dependent Data Factory entities (linked services and datasets).</span></span> <span data-ttu-id="d08a8-113">不不需要的 toocreate hello 管線的任何額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="d08a8-113">No additional steps are required toocreate hello pipeline.</span></span>   

![選取資料來源](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="d08a8-115">請參閱[複製精靈教學課程](data-factory-copy-data-wizard-tutorial.md)文件的逐步指示 toocreate 範例管線 toocopy 資料從 Azure blob tooan Azure SQL Database 的資料表。</span><span class="sxs-lookup"><span data-stu-id="d08a8-115">See [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md) article for step-by-step instructions toocreate a sample pipeline toocopy data from an Azure blob tooan Azure SQL Database table.</span></span> 
> 
> 

<span data-ttu-id="d08a8-116">hello 精靈被設計大型的資料，請注意，從 hello 開始。</span><span class="sxs-lookup"><span data-stu-id="d08a8-116">hello wizard is designed with big data in mind from hello start.</span></span> <span data-ttu-id="d08a8-117">它是既簡單又有效率 tooauthor 移動數百個資料夾、 檔案或資料表使用 hello 複製資料精靈 」 的 Data Factory 管線。</span><span class="sxs-lookup"><span data-stu-id="d08a8-117">It is simple and efficient tooauthor Data Factory pipelines that move hundreds of folders, files, or tables using hello Copy Data wizard.</span></span> <span data-ttu-id="d08a8-118">hello 精靈支援下列三項功能的 hello： 自動資料預覽、 擷取結構描述和對應，以及篩選資料。</span><span class="sxs-lookup"><span data-stu-id="d08a8-118">hello wizard supports hello following three features: Automatic data preview, schema capture and mapping, and filtering data.</span></span> 

## <a name="automatic-data-preview"></a><span data-ttu-id="d08a8-119">自動資料預覽</span><span class="sxs-lookup"><span data-stu-id="d08a8-119">Automatic data preview</span></span>
<span data-ttu-id="d08a8-120">hello 複製精靈可讓您 tooreview 資料的一部分 hello hello 從資料來源為您選取 toovalidate 是否 hello 資料的 hello 以滑鼠右鍵想 toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="d08a8-120">hello copy wizard allows you tooreview part of hello data from hello selected data source for you toovalidate whether hello data it is hello right data you want toocopy.</span></span> <span data-ttu-id="d08a8-121">此外，如果 hello 來源資料是文字檔案中，hello 複製精靈剖析 hello 文字檔案 toolearn 資料列和資料行分隔符號和結構描述會自動。</span><span class="sxs-lookup"><span data-stu-id="d08a8-121">In addition, if hello source data is in a text file, hello copy wizard parses hello text file toolearn row and column delimiters, and schema automatically.</span></span> 

![檔案格式設定](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="d08a8-123">結構描述擷取和對應</span><span class="sxs-lookup"><span data-stu-id="d08a8-123">Schema capture and mapping</span></span>
<span data-ttu-id="d08a8-124">hello 結構描述的輸入資料可能不符合輸出資料，在某些情況下 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="d08a8-124">hello schema of input data may not match hello schema of output data in some cases.</span></span> <span data-ttu-id="d08a8-125">在此案例中，您需要 toomap hello 來源結構描述 toocolumns 從 hello 目的地結構描述中的資料行。</span><span class="sxs-lookup"><span data-stu-id="d08a8-125">In this scenario, you need toomap columns from hello source schema toocolumns from hello destination schema.</span></span> 

<span data-ttu-id="d08a8-126">hello 複製精靈會自動對應中 hello 來源結構描述 toocolumns hello 目的結構描述中的資料行。</span><span class="sxs-lookup"><span data-stu-id="d08a8-126">hello copy wizard automatically maps columns in hello source schema toocolumns in hello destination schema.</span></span> <span data-ttu-id="d08a8-127">您可以使用 hello 下拉式清單來覆寫 hello 對應 （或者） 指定資料行是否需要 toobe 複製 hello 資料時略過。</span><span class="sxs-lookup"><span data-stu-id="d08a8-127">You can override hello mappings by using hello drop-down lists (or) specify whether a column needs toobe skipped while copying hello data.</span></span>   

![結構描述對應](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="d08a8-129">篩選資料</span><span class="sxs-lookup"><span data-stu-id="d08a8-129">Filtering data</span></span>
<span data-ttu-id="d08a8-130">hello 精靈可讓您 toofilter 來源資料 tooselect 只有 hello 資料需要複製 toobe toohello 目的地/接收器資料存放區。</span><span class="sxs-lookup"><span data-stu-id="d08a8-130">hello wizard allows you toofilter source data tooselect only hello data that needs toobe copied toohello destination/sink data store.</span></span> <span data-ttu-id="d08a8-131">篩選可降低 hello hello 資料 toobe 複製的 toohello 接收的資料儲存和因此增強 hello 輸送量 hello 複製作業的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="d08a8-131">Filtering reduces hello volume of hello data toobe copied toohello sink data store and therefore enhances hello throughput of hello copy operation.</span></span> <span data-ttu-id="d08a8-132">它提供彈性的方式 toofilter 資料關聯式資料庫中使用 SQL 查詢語言 （或） 檔案中的 Azure blob 資料夾使用[Data Factory 函式和變數](data-factory-functions-variables.md)。</span><span class="sxs-lookup"><span data-stu-id="d08a8-132">It provides a flexible way toofilter data in a relational database by using SQL query language (or) files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="d08a8-133">篩選資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="d08a8-133">Filtering of data in a database</span></span>
<span data-ttu-id="d08a8-134">在 hello 範例 hello SQL 查詢會使用 hello`Text.Format`函式和`WindowStart`變數。</span><span class="sxs-lookup"><span data-stu-id="d08a8-134">In hello example, hello SQL query uses hello `Text.Format` function and `WindowStart` variable.</span></span> 

![驗證運算式](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="d08a8-136">篩選 Azure Blob 資料夾中的資料</span><span class="sxs-lookup"><span data-stu-id="d08a8-136">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="d08a8-137">您可以在 hello 資料夾路徑 toocopy 資料由決定在執行階段為基礎的資料夾中使用變數[系統變數](data-factory-functions-variables.md#data-factory-system-variables)。</span><span class="sxs-lookup"><span data-stu-id="d08a8-137">You can use variables in hello folder path toocopy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="d08a8-138">支援的 hello 變數是： **{year}**， **{month}**， **{day}**， **{小時}**， **{分鐘}**，和**{自訂}**。</span><span class="sxs-lookup"><span data-stu-id="d08a8-138">hello supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="d08a8-139">範例︰inputfolder/{year}/{month}/{day}。</span><span class="sxs-lookup"><span data-stu-id="d08a8-139">Example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="d08a8-140">假設您有輸入 hello 遵循格式中的資料夾：</span><span class="sxs-lookup"><span data-stu-id="d08a8-140">Suppose that you have input folders in hello following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="d08a8-141">按一下 hello**瀏覽**按鈕**檔案或資料夾**，瀏覽這些資料夾 tooone (比方說，2016年-> 03-> 01-> 02)，按一下**選擇**。</span><span class="sxs-lookup"><span data-stu-id="d08a8-141">Click hello **Browse** button for **File or folder**, browse tooone of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="d08a8-142">您應該會看到`2016/03/01/02`hello 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="d08a8-142">You should see `2016/03/01/02` in hello text box.</span></span> <span data-ttu-id="d08a8-143">現在，將 **2016** 取代為 **{year}**、**03** 取代為 **{month}**、**01** 取代為 **{day}**，以及 **02** 取代為 **{hour}**，然後按 Tab 鍵。您應該會看到這些四個變數的下拉式清單 tooselect hello 格式：</span><span class="sxs-lookup"><span data-stu-id="d08a8-143">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press Tab. You should see drop-down lists tooselect hello format for these four variables:</span></span>

![使用系統變數](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="d08a8-145">Hello 下列螢幕擷取畫面所示，您也可以使用**自訂**變數和任何[支援格式字串](https://msdn.microsoft.com/library/8kb3ddd4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d08a8-145">As shown in hello following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="d08a8-146">tooselect 資料夾與該結構中，使用 hello**瀏覽**按鈕第一次。</span><span class="sxs-lookup"><span data-stu-id="d08a8-146">tooselect a folder with that structure, use hello **Browse** button first.</span></span> <span data-ttu-id="d08a8-147">然後取代的值為**{自訂}**，然後按 Tab toosee hello 文字方塊可以在這裡輸入 hello 格式字串。</span><span class="sxs-lookup"><span data-stu-id="d08a8-147">Then replace a value with **{custom}**, and press Tab toosee hello text box where you can type hello format string.</span></span>     

![使用自訂變數](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a><span data-ttu-id="d08a8-149">支援多樣化資料和物件類型</span><span class="sxs-lookup"><span data-stu-id="d08a8-149">Support for diverse data and object types</span></span>
<span data-ttu-id="d08a8-150">藉由使用 hello 複製精靈，您可以有效地移動數百個資料夾、 檔案或資料表。</span><span class="sxs-lookup"><span data-stu-id="d08a8-150">By using hello Copy Wizard, you can efficiently move hundreds of folders, files, or tables.</span></span>

![選取從 toocopy 資料的資料表](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a><span data-ttu-id="d08a8-152">排程選項</span><span class="sxs-lookup"><span data-stu-id="d08a8-152">Scheduling options</span></span>
<span data-ttu-id="d08a8-153">您可以執行 hello 複製作業一次，或根據排程 （每小時、 每天，依此類推）。</span><span class="sxs-lookup"><span data-stu-id="d08a8-153">You can run hello copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="d08a8-154">這兩個選項可以用於 hello 廣度 hello 連接器的跨內部部署、 雲端和本機桌面的複本。</span><span class="sxs-lookup"><span data-stu-id="d08a8-154">Both of these options can be used for hello breadth of hello connectors across on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="d08a8-155">一次性複製作業可讓從來源 tooa 目的地的資料移動一次。</span><span class="sxs-lookup"><span data-stu-id="d08a8-155">A one-time copy operation enables data movement from a source tooa destination only once.</span></span> <span data-ttu-id="d08a8-156">它適用於 toodata 任何大小和任何支援的格式。</span><span class="sxs-lookup"><span data-stu-id="d08a8-156">It applies toodata of any size and any supported format.</span></span> <span data-ttu-id="d08a8-157">排程的 hello 複製可讓您 toocopy 資料上規定的循環。</span><span class="sxs-lookup"><span data-stu-id="d08a8-157">hello scheduled copy allows you toocopy data on a prescribed recurrence.</span></span> <span data-ttu-id="d08a8-158">您可以使用 （例如重試、 逾時和警示） 的豐富設定 tooconfigure hello 排程複製。</span><span class="sxs-lookup"><span data-stu-id="d08a8-158">You can use rich settings (like retry, timeout, and alerts) tooconfigure hello scheduled copy.</span></span>

![排程屬性](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="d08a8-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d08a8-160">Next steps</span></span>
<span data-ttu-id="d08a8-161">使用複製活動與 hello 資料 Factory 複製精靈 toocreate 管線快速逐步解說，請參閱[教學課程： 建立管線中使用 hello 複製精靈](data-factory-copy-data-wizard-tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="d08a8-161">For a quick walkthrough of using hello Data Factory Copy Wizard toocreate a pipeline with Copy Activity, see [Tutorial: Create a pipeline using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

