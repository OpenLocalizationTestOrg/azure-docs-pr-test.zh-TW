---
title: "Microsoft Power BI Embedded - 連接到資料來源"
description: "Power BI Embedded，連接到資料來源"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="3adcb-103">連接到資料來源</span><span class="sxs-lookup"><span data-stu-id="3adcb-103">Connect to a data source</span></span>
<span data-ttu-id="3adcb-104">使用 **Power BI Embedded**可以將報表內嵌到您自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3adcb-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="3adcb-105">當您將 Power BI 報表內嵌到應用程式時，報告會以**匯入**資料複本的方式連接至基礎資料，或使用 **DirectQuery****直接連接**到資料來源。</span><span class="sxs-lookup"><span data-stu-id="3adcb-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="3adcb-106">以下是使用 **Import** 和 **DirectQuery** 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="3adcb-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="3adcb-107">Import</span><span class="sxs-lookup"><span data-stu-id="3adcb-107">Import</span></span> | <span data-ttu-id="3adcb-108">直接連接</span><span class="sxs-lookup"><span data-stu-id="3adcb-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="3adcb-109">資料表、資料行 *和資料* 匯入或複製到報表的資料集中。</span><span class="sxs-lookup"><span data-stu-id="3adcb-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="3adcb-110">若要查看基礎資料發生的變更，您必須重新整理或再次匯入完整的目前資料集。</span><span class="sxs-lookup"><span data-stu-id="3adcb-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="3adcb-111">只有 *資料表和資料行* 匯入或複製到報表的資料集中。</span><span class="sxs-lookup"><span data-stu-id="3adcb-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="3adcb-112">一律檢視最新的資料。</span><span class="sxs-lookup"><span data-stu-id="3adcb-112">You always view the most current data.</span></span> |

<span data-ttu-id="3adcb-113">有了 Power BI Embedded，您就可以使用 DirectQuery 搭配雲端資料來源，但目前無法使用內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="3adcb-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="3adcb-114">現階段 Power BI Embedded 不支援「內部部署資料閘道器」。</span><span class="sxs-lookup"><span data-stu-id="3adcb-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="3adcb-115">這表示您無法在 DirectQuery 使用內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="3adcb-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="3adcb-116">支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="3adcb-116">Supported data sources</span></span>

<span data-ttu-id="3adcb-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="3adcb-117">**DirectQuery**</span></span>
* <span data-ttu-id="3adcb-118">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3adcb-118">Azure SQL database</span></span>
* <span data-ttu-id="3adcb-119">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="3adcb-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="3adcb-120">**Import**</span><span class="sxs-lookup"><span data-stu-id="3adcb-120">**Import**</span></span>

<span data-ttu-id="3adcb-121">您可以使用 Power BI Desktop 中所有的可用資料來源進行匯入。</span><span class="sxs-lookup"><span data-stu-id="3adcb-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="3adcb-122">您將「不」能夠重新整理 Power BI Embedded 中的資料。</span><span class="sxs-lookup"><span data-stu-id="3adcb-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="3adcb-123">您必須將 PBIX 檔案的變更上傳到 Power BI Embedded。</span><span class="sxs-lookup"><span data-stu-id="3adcb-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="3adcb-124">這是因為沒有閘道器可用。</span><span class="sxs-lookup"><span data-stu-id="3adcb-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="3adcb-125">使用 DirectQuery 的優點</span><span class="sxs-lookup"><span data-stu-id="3adcb-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="3adcb-126">使用 **DirectQuery**有兩項主要優點：</span><span class="sxs-lookup"><span data-stu-id="3adcb-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="3adcb-127">**DirectQuery** 可讓您對非常大型的資料集建立視覺效果，否則不可能第一次就匯入所有資料。</span><span class="sxs-lookup"><span data-stu-id="3adcb-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="3adcb-128">基礎資料變更需要重新整理資料，而某些報表如果要顯示目前的資料，還需要大量的資料傳輸，這都使得重新匯入資料不可行。</span><span class="sxs-lookup"><span data-stu-id="3adcb-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="3adcb-129">相較之下， **DirectQuery** 報表一律使用目前的資料。</span><span class="sxs-lookup"><span data-stu-id="3adcb-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="3adcb-130">DirectQuery 的限制</span><span class="sxs-lookup"><span data-stu-id="3adcb-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="3adcb-131">使用 **DirectQuery**有一些限制：</span><span class="sxs-lookup"><span data-stu-id="3adcb-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="3adcb-132">所有資料表必須全都來自單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="3adcb-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="3adcb-133">如果查詢太複雜，就會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="3adcb-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="3adcb-134">若要補救錯誤，您必須重構以簡化查詢。</span><span class="sxs-lookup"><span data-stu-id="3adcb-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="3adcb-135">如果查詢一定要很複雜，就必須匯入資料，而不是使用 **DirectQuery**。</span><span class="sxs-lookup"><span data-stu-id="3adcb-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="3adcb-136">關聯性篩選限於單向，而非雙向。</span><span class="sxs-lookup"><span data-stu-id="3adcb-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="3adcb-137">您無法變更資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="3adcb-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="3adcb-138">根據預設，限制是置於量值允許的 DAX 運算式中。</span><span class="sxs-lookup"><span data-stu-id="3adcb-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="3adcb-139">請參閱 [DirectQuery 和量值](#measures)。</span><span class="sxs-lookup"><span data-stu-id="3adcb-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="3adcb-140">DirectQuery 和量值</span><span class="sxs-lookup"><span data-stu-id="3adcb-140">DirectQuery and measures</span></span>
<span data-ttu-id="3adcb-141">為確保傳送至基礎資料來源的查詢都有可接受的效能，所以將限制加諸於量值之上。</span><span class="sxs-lookup"><span data-stu-id="3adcb-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="3adcb-142">使用 **Power BI Desktop** 時，進階使用者可以選擇 [檔案] > [選項和設定] > [選項]，選擇略過這項限制。</span><span class="sxs-lookup"><span data-stu-id="3adcb-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="3adcb-143">在 [選項] 對話方塊中選擇 [DirectQuery]，並選取選項 [允許在 DirectQuery 模式中量值不受限制]。</span><span class="sxs-lookup"><span data-stu-id="3adcb-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="3adcb-144">選取該選項後，即可使用對量值有效的任何 DAX 運算式。</span><span class="sxs-lookup"><span data-stu-id="3adcb-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="3adcb-145">不過，使用者必須知道，當資料匯入時，某些執行得很好的運算式在 **DirectQuery** 模式中可能會造成後端來源的查詢非常慢。</span><span class="sxs-lookup"><span data-stu-id="3adcb-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="3adcb-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3adcb-146">See Also</span></span>
* [<span data-ttu-id="3adcb-147">開始使用 Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3adcb-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="3adcb-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3adcb-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="3adcb-149">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="3adcb-149">More questions?</span></span> [<span data-ttu-id="3adcb-150">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="3adcb-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

