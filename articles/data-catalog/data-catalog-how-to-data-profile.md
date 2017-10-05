---
title: "如何對資料來源進行資料分析"
description: "專門說明如何在 Azure 資料目錄中註冊資料來源時包含資料表和資料行層級的資料設定檔以及如何使用資料設定檔來了解資料來源的操作說明文章。"
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
ms.openlocfilehash: 8f4174f0ed74706b8275c8b1f0a62753f2834fa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="57610-103">對資料來源進行資料分析</span><span class="sxs-lookup"><span data-stu-id="57610-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="57610-104">簡介</span><span class="sxs-lookup"><span data-stu-id="57610-104">Introduction</span></span>
<span data-ttu-id="57610-105"> 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。</span><span class="sxs-lookup"><span data-stu-id="57610-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="57610-106">換句話說，[Azure 資料目錄]  的重點在於協助人們探索、了解，以及使用資料來源，並可協助組織從現有的資料獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="57610-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="57610-107">當資料來源向 **Azure 資料目錄**註冊之後，該服務會複製其中繼資料並建立索引，但不僅止於此。</span><span class="sxs-lookup"><span data-stu-id="57610-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="57610-108">**Azure 資料目錄**的**資料分析**功能會檢查目錄中所支援資料來源的資料，並收集關於該資料的統計資料和資訊。</span><span class="sxs-lookup"><span data-stu-id="57610-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="57610-109">想要包含資料資產的設定檔很容易。</span><span class="sxs-lookup"><span data-stu-id="57610-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="57610-110">當您註冊資料資產時，請選擇資料來源註冊工具中的 [包含資料設定檔]  。</span><span class="sxs-lookup"><span data-stu-id="57610-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="57610-111">什麼是資料分析</span><span class="sxs-lookup"><span data-stu-id="57610-111">What is Data Profiling</span></span>
<span data-ttu-id="57610-112">資料分析會檢查所註冊資料來源中的資料，並收集關於該資料的統計資料和資訊。</span><span class="sxs-lookup"><span data-stu-id="57610-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="57610-113">在探索資料來源期間，這些統計資料可以協助您判斷資料是否適合用來解決他們的商務問題。</span><span class="sxs-lookup"><span data-stu-id="57610-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="57610-114">下列資料來源都支援資料分析︰</span><span class="sxs-lookup"><span data-stu-id="57610-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="57610-115">SQL Server (包括 Azure SQL DB 和 Azure SQL 資料倉儲) 資料表和檢視</span><span class="sxs-lookup"><span data-stu-id="57610-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="57610-116">Oracle 資料表和檢視</span><span class="sxs-lookup"><span data-stu-id="57610-116">Oracle tables and views</span></span>
* <span data-ttu-id="57610-117">Teradata 資料表和檢視</span><span class="sxs-lookup"><span data-stu-id="57610-117">Teradata tables and views</span></span>
* <span data-ttu-id="57610-118">Hive 資料表</span><span class="sxs-lookup"><span data-stu-id="57610-118">Hive tables</span></span>

<span data-ttu-id="57610-119">在註冊資料資產時包含資料設定檔可幫助使用者回答資料來源的相關問題，包括︰</span><span class="sxs-lookup"><span data-stu-id="57610-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="57610-120">是否可用來解決商務問題？</span><span class="sxs-lookup"><span data-stu-id="57610-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="57610-121">資料是否符合特定標準或模式？</span><span class="sxs-lookup"><span data-stu-id="57610-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="57610-122">資料來源有哪些異常之處？</span><span class="sxs-lookup"><span data-stu-id="57610-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="57610-123">將此資料整合到應用程式時可能面臨哪些挑戰？</span><span class="sxs-lookup"><span data-stu-id="57610-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="57610-124">您也可以對資產新增說明文件來描述如何將資料整合到應用程式。</span><span class="sxs-lookup"><span data-stu-id="57610-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="57610-125">請參閱 [如何記載資料來源](data-catalog-how-to-documentation.md)。</span><span class="sxs-lookup"><span data-stu-id="57610-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="57610-126">如何在註冊資料來源時包含資料設定檔</span><span class="sxs-lookup"><span data-stu-id="57610-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="57610-127">想要包含資料來源的設定檔很容易。</span><span class="sxs-lookup"><span data-stu-id="57610-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="57610-128">當您註冊資料來源時，在資料來源註冊工具的 [要註冊的物件] 面板中選擇 [包含資料設定檔]。</span><span class="sxs-lookup"><span data-stu-id="57610-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="57610-129">若要深入了解如何註冊資料來源，請參閱[如何註冊資料來源](data-catalog-how-to-register.md)和[開始使用 Azure 資料目錄](data-catalog-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="57610-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="57610-130">篩選包含資料設定檔的資料資產</span><span class="sxs-lookup"><span data-stu-id="57610-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="57610-131">若要探索包含資料設定檔的資料資產，您可以包含 `has:tableDataProfiles` 或 `has:columnsDataProfiles` 做為搜尋字詞之一。</span><span class="sxs-lookup"><span data-stu-id="57610-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="57610-132">在資料來源註冊工具中選取 [包含資料設定檔]，即會同時包含資料表和資料行層級的設定檔資訊。</span><span class="sxs-lookup"><span data-stu-id="57610-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="57610-133">不過，資料目錄 API 讓只含一組設定檔資訊的資料資產能夠加以註冊。</span><span class="sxs-lookup"><span data-stu-id="57610-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="57610-134">檢視資料設定檔資訊</span><span class="sxs-lookup"><span data-stu-id="57610-134">Viewing data profile information</span></span>
<span data-ttu-id="57610-135">一旦您找到含有設定檔的合適資料來源，您可以檢視資料設定檔的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="57610-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="57610-136">若要檢視資料設定檔，請在資料目錄入口網站視窗中選取資料資產並選擇 [資料設定檔]  。</span><span class="sxs-lookup"><span data-stu-id="57610-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="57610-137">[Azure 資料目錄]  中的資料設定檔會顯示資料表和資料行設定檔資訊，包括︰</span><span class="sxs-lookup"><span data-stu-id="57610-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="57610-138">物件資料設定檔</span><span class="sxs-lookup"><span data-stu-id="57610-138">Object data profile</span></span>
* <span data-ttu-id="57610-139">資料列數目</span><span class="sxs-lookup"><span data-stu-id="57610-139">Number of rows</span></span>
* <span data-ttu-id="57610-140">資料表大小</span><span class="sxs-lookup"><span data-stu-id="57610-140">Table size</span></span>
* <span data-ttu-id="57610-141">物件的上次更新時間</span><span class="sxs-lookup"><span data-stu-id="57610-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="57610-142">資料行資料設定檔</span><span class="sxs-lookup"><span data-stu-id="57610-142">Column data profile</span></span>
* <span data-ttu-id="57610-143">資料行資料類型</span><span class="sxs-lookup"><span data-stu-id="57610-143">Column data type</span></span>
* <span data-ttu-id="57610-144">相異值數目</span><span class="sxs-lookup"><span data-stu-id="57610-144">Number of distinct values</span></span>
* <span data-ttu-id="57610-145">具有 NULL 值的資料列數目</span><span class="sxs-lookup"><span data-stu-id="57610-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="57610-146">資料行的最小值、最大值、平均值和標準差值</span><span class="sxs-lookup"><span data-stu-id="57610-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="57610-147">摘要</span><span class="sxs-lookup"><span data-stu-id="57610-147">Summary</span></span>
<span data-ttu-id="57610-148">資料分析可提供關於註冊資料資產的統計資料和資訊，以協助您判斷資料是否適合用來解決商務問題。</span><span class="sxs-lookup"><span data-stu-id="57610-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="57610-149">加上註解和記載資料來源後，資料設定檔可以讓使用者更深入了解資料。</span><span class="sxs-lookup"><span data-stu-id="57610-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="57610-150">另請參閱</span><span class="sxs-lookup"><span data-stu-id="57610-150">See Also</span></span>
* [<span data-ttu-id="57610-151">如何註冊資料來源</span><span class="sxs-lookup"><span data-stu-id="57610-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="57610-152">開始使用 Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="57610-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
