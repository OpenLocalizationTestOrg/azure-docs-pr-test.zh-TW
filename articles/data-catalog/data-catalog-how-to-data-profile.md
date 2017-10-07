---
title: "aaaHow tooData 分析資料來源"
description: "如何 tooarticle 反白顯示 tooinclude 資料表和資料行層級資料設定檔註冊在 Azure 資料目錄中，資料來源時，以及如何 toouse 資料設定檔 toounderstand 資料來源。"
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="c24ae-103">對資料來源進行資料分析</span><span class="sxs-lookup"><span data-stu-id="c24ae-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="c24ae-104">簡介</span><span class="sxs-lookup"><span data-stu-id="c24ae-104">Introduction</span></span>
<span data-ttu-id="c24ae-105">**Microsoft Azure 資料目錄** 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。</span><span class="sxs-lookup"><span data-stu-id="c24ae-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="c24ae-106">換句話說， **Azure 資料目錄**是協助人員相關的所有探索、 了解，以及使用資料來源，以及協助組織 tooget 其現有的資料來自多個值。</span><span class="sxs-lookup"><span data-stu-id="c24ae-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="c24ae-107">資料來源已向當**Azure 資料目錄**，它的中繼資料會複製，並以 hello 服務編製索引但 hello 劇本那里未結束。</span><span class="sxs-lookup"><span data-stu-id="c24ae-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="c24ae-108">hello**資料分析**功能**Azure 資料目錄**會檢查您的類別目錄中支援的資料來源的 hello 資料並收集統計資料，以及該資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c24ae-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="c24ae-109">它是簡單 tooinclude 資料資產的設定檔。</span><span class="sxs-lookup"><span data-stu-id="c24ae-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="c24ae-110">當您註冊資料資產時，選擇 [**包含資料設定檔**hello 資料來源註冊工具中。</span><span class="sxs-lookup"><span data-stu-id="c24ae-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="c24ae-111">什麼是資料分析</span><span class="sxs-lookup"><span data-stu-id="c24ae-111">What is Data Profiling</span></span>
<span data-ttu-id="c24ae-112">資料分析會檢查 hello hello 所註冊的資料來源中的資料，並收集統計資料，以及該資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c24ae-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="c24ae-113">在資料來源探索，這些統計資料可協助您判斷 hello 資料 toosolve hello 適合其商務問題。</span><span class="sxs-lookup"><span data-stu-id="c24ae-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="c24ae-114">hello 下列資料來源都支援程式碼剖析資料：</span><span class="sxs-lookup"><span data-stu-id="c24ae-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="c24ae-115">SQL Server (包括 Azure SQL DB 和 Azure SQL 資料倉儲) 資料表和檢視</span><span class="sxs-lookup"><span data-stu-id="c24ae-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="c24ae-116">Oracle 資料表和檢視</span><span class="sxs-lookup"><span data-stu-id="c24ae-116">Oracle tables and views</span></span>
* <span data-ttu-id="c24ae-117">Teradata 資料表和檢視</span><span class="sxs-lookup"><span data-stu-id="c24ae-117">Teradata tables and views</span></span>
* <span data-ttu-id="c24ae-118">Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="c24ae-118">Hive tables</span></span>

<span data-ttu-id="c24ae-119">在註冊資料資產時包含資料設定檔可幫助使用者回答資料來源的相關問題，包括︰</span><span class="sxs-lookup"><span data-stu-id="c24ae-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="c24ae-120">它可以是使用的 toosolve 我商務問題嗎？</span><span class="sxs-lookup"><span data-stu-id="c24ae-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="c24ae-121">Hello 資料是否符合 tooparticular 標準或模式？</span><span class="sxs-lookup"><span data-stu-id="c24ae-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="c24ae-122">有哪些 hello 資料來源的 hello 異常狀況？</span><span class="sxs-lookup"><span data-stu-id="c24ae-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="c24ae-123">將此資料整合到應用程式時可能面臨哪些挑戰？</span><span class="sxs-lookup"><span data-stu-id="c24ae-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="c24ae-124">您也可以加入文件 tooan 資產 toodescribe 資料無法如何整合到應用程式。</span><span class="sxs-lookup"><span data-stu-id="c24ae-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="c24ae-125">請參閱[如何 toodocument 資料來源](data-catalog-how-to-documentation.md)。</span><span class="sxs-lookup"><span data-stu-id="c24ae-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="c24ae-126">Tooinclude 資料設定檔時登錄資料來源</span><span class="sxs-lookup"><span data-stu-id="c24ae-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="c24ae-127">它是簡單 tooinclude 您的資料來源的設定檔。</span><span class="sxs-lookup"><span data-stu-id="c24ae-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="c24ae-128">當您註冊資料來源，在 [hello**註冊物件 toobe**面板 hello 資料來源登錄的工具，請選擇**包含資料設定檔**。</span><span class="sxs-lookup"><span data-stu-id="c24ae-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="c24ae-129">toolearn 深入了解如何 tooregister 資料來源，請參閱[如何 tooregister 資料來源](data-catalog-how-to-register.md)和[開始使用 Azure 資料目錄](data-catalog-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c24ae-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="c24ae-130">篩選包含資料設定檔的資料資產</span><span class="sxs-lookup"><span data-stu-id="c24ae-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="c24ae-131">您可以加入包含資料設定檔的 toodiscover 資料資產，`has:tableDataProfiles`或`has:columnsDataProfiles`做為其中一個搜尋詞彙。</span><span class="sxs-lookup"><span data-stu-id="c24ae-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="c24ae-132">選取**包含資料設定檔**在 hello 資料來源註冊工具會包含資料表和資料行層級設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="c24ae-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="c24ae-133">不過，hello 資料目錄應用程式開發介面可讓資料資產 toobe 向只有一組所包含的設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="c24ae-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="c24ae-134">檢視資料設定檔資訊</span><span class="sxs-lookup"><span data-stu-id="c24ae-134">Viewing data profile information</span></span>
<span data-ttu-id="c24ae-135">一旦您找到適合的資料來源與設定檔，您可以檢視 hello 設定檔詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c24ae-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="c24ae-136">tooview hello 資料設定檔，選取的資料資產，並選擇**資料設定檔**hello 資料目錄入口網站視窗中。</span><span class="sxs-lookup"><span data-stu-id="c24ae-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="c24ae-137">[Azure 資料目錄]  中的資料設定檔會顯示資料表和資料行設定檔資訊，包括︰</span><span class="sxs-lookup"><span data-stu-id="c24ae-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="c24ae-138">物件資料設定檔</span><span class="sxs-lookup"><span data-stu-id="c24ae-138">Object data profile</span></span>
* <span data-ttu-id="c24ae-139">資料列數目</span><span class="sxs-lookup"><span data-stu-id="c24ae-139">Number of rows</span></span>
* <span data-ttu-id="c24ae-140">資料表大小</span><span class="sxs-lookup"><span data-stu-id="c24ae-140">Table size</span></span>
* <span data-ttu-id="c24ae-141">Hello 物件上次更新</span><span class="sxs-lookup"><span data-stu-id="c24ae-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="c24ae-142">資料行資料設定檔</span><span class="sxs-lookup"><span data-stu-id="c24ae-142">Column data profile</span></span>
* <span data-ttu-id="c24ae-143">資料行資料類型</span><span class="sxs-lookup"><span data-stu-id="c24ae-143">Column data type</span></span>
* <span data-ttu-id="c24ae-144">相異值數目</span><span class="sxs-lookup"><span data-stu-id="c24ae-144">Number of distinct values</span></span>
* <span data-ttu-id="c24ae-145">具有 NULL 值的資料列數目</span><span class="sxs-lookup"><span data-stu-id="c24ae-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="c24ae-146">資料行的最小值、最大值、平均值和標準差值</span><span class="sxs-lookup"><span data-stu-id="c24ae-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="c24ae-147">摘要</span><span class="sxs-lookup"><span data-stu-id="c24ae-147">Summary</span></span>
<span data-ttu-id="c24ae-148">資料分析提供統計資料，並註冊資料資產 toohelp 判斷 hello 適用性 hello 資料 toosolve 商務問題的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c24ae-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="c24ae-149">加上註解和記載資料來源後，資料設定檔可以讓使用者更深入了解資料。</span><span class="sxs-lookup"><span data-stu-id="c24ae-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="c24ae-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c24ae-150">See Also</span></span>
* [<span data-ttu-id="c24ae-151">如何 tooregister 資料來源</span><span class="sxs-lookup"><span data-stu-id="c24ae-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="c24ae-152">開始使用 Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="c24ae-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
