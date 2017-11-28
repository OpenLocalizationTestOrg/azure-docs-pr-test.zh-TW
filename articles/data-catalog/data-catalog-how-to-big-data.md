---
title: "與 「 偉大資料 」 資料來源的 aaaHow toowork |Microsoft 文件"
description: "如何 tooarticle 反白顯示的 「 偉大資料 」 的資料來源，包括 Azure Blob 儲存體、 Azure 資料湖，Hadoop HDFS 搭配使用 Azure 資料目錄的模式。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="952ae-103">在 Azure 資料目錄中 toowork 大型資料來源的方式</span><span class="sxs-lookup"><span data-stu-id="952ae-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="952ae-104">簡介</span><span class="sxs-lookup"><span data-stu-id="952ae-104">Introduction</span></span>
<span data-ttu-id="952ae-105">**Microsoft Azure 資料目錄** 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。</span><span class="sxs-lookup"><span data-stu-id="952ae-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="952ae-106">它就是要協助大眾探索、 了解，以及使用資料來源，以及幫助組織 tooget 多個值，從其現有的資料來源，包括巨量資料。</span><span class="sxs-lookup"><span data-stu-id="952ae-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="952ae-107">**Azure 資料目錄**支援 hello 註冊的 Azure Blob 儲存體 blob 和目錄，以及 Hadoop HDFS 檔案及目錄。</span><span class="sxs-lookup"><span data-stu-id="952ae-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="952ae-108">hello 半結構化的本質，這些資料來源的提供很大的彈性。</span><span class="sxs-lookup"><span data-stu-id="952ae-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="952ae-109">不過，tooget hello 大部分的值從註冊它們與**Azure 資料目錄**，使用者必須考慮如何組織 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="952ae-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="952ae-110">將目錄視為邏輯資料集</span><span class="sxs-lookup"><span data-stu-id="952ae-110">Directories as logical data sets</span></span>
<span data-ttu-id="952ae-111">組織大型資料來源的常見模式為邏輯的資料集是 tootreat 目錄。</span><span class="sxs-lookup"><span data-stu-id="952ae-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="952ae-112">最上層目錄會使用的 toodefine 資料集，而子資料夾定義資料分割，及它們所包含的 hello 檔案儲存 hello 資料本身。</span><span class="sxs-lookup"><span data-stu-id="952ae-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="952ae-113">此模式的可能範例如下：</span><span class="sxs-lookup"><span data-stu-id="952ae-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="952ae-114">在此範例中，vehicle_maintenance_events 和 location_tracking_events 代表邏輯資料集。</span><span class="sxs-lookup"><span data-stu-id="952ae-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="952ae-115">上述每個資料夾包含資料檔案，依據年份和月份組織成子資料夾。</span><span class="sxs-lookup"><span data-stu-id="952ae-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="952ae-116">上述每個資料夾可能包含數百或數千個檔案。</span><span class="sxs-lookup"><span data-stu-id="952ae-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="952ae-117">在此模式中，向 **Azure 資料目錄** 註冊個別的檔案毫無意義。</span><span class="sxs-lookup"><span data-stu-id="952ae-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="952ae-118">相反地，註冊代表 hello 是有意義的 toohello 使用者使用 hello 資料的資料集的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="952ae-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="952ae-119">參考資料檔案</span><span class="sxs-lookup"><span data-stu-id="952ae-119">Reference data files</span></span>
<span data-ttu-id="952ae-120">互補的模式是 toostore 參考資料集，以個別檔案。</span><span class="sxs-lookup"><span data-stu-id="952ae-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="952ae-121">這些資料集可能會視為 hello '小' 端的巨量資料，而且通常會類似 toodimensions 分析資料模型中。</span><span class="sxs-lookup"><span data-stu-id="952ae-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="952ae-122">參考資料檔案包含的記錄，使用的 tooprovide hello 大量 hello 資料檔案儲存在 hello 巨量資料存放區中的其他位置的內容。</span><span class="sxs-lookup"><span data-stu-id="952ae-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="952ae-123">此模式的可能範例如下：</span><span class="sxs-lookup"><span data-stu-id="952ae-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="952ae-124">當分析師或資料科學家便可使用 hello 較大的目錄結構中所含的 hello 資料時，這些參考檔案中的 hello 資料可以是使用的 tooprovide 的詳細資訊的實體的參考 tooonly 依名稱或識別碼 hello 較大的資料設定。</span><span class="sxs-lookup"><span data-stu-id="952ae-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="952ae-125">在這種模式是合理 tooregister hello 個別參考的資料檔案與**Azure 資料目錄**。</span><span class="sxs-lookup"><span data-stu-id="952ae-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="952ae-126">每個檔案都代表資料集，且每個都可以加上附註和個別地探索。</span><span class="sxs-lookup"><span data-stu-id="952ae-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="952ae-127">替代模式</span><span class="sxs-lookup"><span data-stu-id="952ae-127">Alternate patterns</span></span>
<span data-ttu-id="952ae-128">hello hello 前面一節中所述的模式只有兩個可能的方式，可能會組織巨量資料存放區，但是每個實作不同。</span><span class="sxs-lookup"><span data-stu-id="952ae-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="952ae-129">不論您的資料來源的結構方式，註冊使用大型資料來源時**Azure 資料目錄**，專注於註冊 hello 檔案和目錄的代表 hello 資料集內的值 tooothers 的程式組織。</span><span class="sxs-lookup"><span data-stu-id="952ae-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="952ae-130">註冊的所有檔案和目錄可以干擾 hello 類別目錄，難度的使用者 toofind 他們的需要。</span><span class="sxs-lookup"><span data-stu-id="952ae-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="952ae-131">摘要</span><span class="sxs-lookup"><span data-stu-id="952ae-131">Summary</span></span>
<span data-ttu-id="952ae-132">註冊具有的資料來源**Azure 資料目錄**使其更容易 toodiscover 並了解。</span><span class="sxs-lookup"><span data-stu-id="952ae-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="952ae-133">登錄及註解 hello 巨量資料檔案和目錄的代表邏輯資料集，您可以協助使用者尋找並使用所需的 hello 巨量資料來源。</span><span class="sxs-lookup"><span data-stu-id="952ae-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
