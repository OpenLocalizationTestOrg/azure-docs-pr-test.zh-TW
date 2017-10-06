---
title: "aaaMicrosoft Power BI Embedded-連線 tooa 資料來源"
description: "Power BI Embedded，連接 toodata 來源"
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="6eeda-103">Tooa 資料來源連接</span><span class="sxs-lookup"><span data-stu-id="6eeda-103">Connect tooa data source</span></span>
<span data-ttu-id="6eeda-104">使用 **Power BI Embedded**可以將報表內嵌到您自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6eeda-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="6eeda-105">當您將 Power BI 報表內嵌到應用程式時，hello 報表連接基礎資料的 toohello**匯入**hello 資料，或是藉由複製**直接連接**toohello 資料來源使用**DirectQuery**。</span><span class="sxs-lookup"><span data-stu-id="6eeda-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="6eeda-106">以下是使用的 hello 差異**匯入**和**DirectQuery**。</span><span class="sxs-lookup"><span data-stu-id="6eeda-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="6eeda-107">Import</span><span class="sxs-lookup"><span data-stu-id="6eeda-107">Import</span></span> | <span data-ttu-id="6eeda-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="6eeda-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="6eeda-109">資料表、 資料行，*和資料*匯入或複製到 hello 報表資料集。</span><span class="sxs-lookup"><span data-stu-id="6eeda-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="6eeda-110">toosee 變更發生的 toohello 基礎資料，您必須重新整理，或匯入完成，目前資料集一次。</span><span class="sxs-lookup"><span data-stu-id="6eeda-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="6eeda-111">只有*資料表和資料行*匯入或複製到 hello 報表資料集。</span><span class="sxs-lookup"><span data-stu-id="6eeda-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="6eeda-112">您一律檢視 hello 最新的資料。</span><span class="sxs-lookup"><span data-stu-id="6eeda-112">You always view hello most current data.</span></span> |

<span data-ttu-id="6eeda-113">有了 Power BI Embedded，您就可以使用 DirectQuery 搭配雲端資料來源，但目前無法使用內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="6eeda-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="6eeda-114">hello 在內部部署資料閘道不支援使用 Power BI Embedded 這一次。</span><span class="sxs-lookup"><span data-stu-id="6eeda-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="6eeda-115">這表示您無法在 DirectQuery 使用內部部署資料來源。</span><span class="sxs-lookup"><span data-stu-id="6eeda-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="6eeda-116">支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="6eeda-116">Supported data sources</span></span>

<span data-ttu-id="6eeda-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="6eeda-117">**DirectQuery**</span></span>
* <span data-ttu-id="6eeda-118">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="6eeda-118">Azure SQL database</span></span>
* <span data-ttu-id="6eeda-119">Azure SQL 資料倉儲</span><span class="sxs-lookup"><span data-stu-id="6eeda-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="6eeda-120">**匯入**</span><span class="sxs-lookup"><span data-stu-id="6eeda-120">**Import**</span></span>

<span data-ttu-id="6eeda-121">您可以使用所有可用的 hello 在 Power BI Desktop 中的資料來源匯入。</span><span class="sxs-lookup"><span data-stu-id="6eeda-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="6eeda-122">您將**不**是無法 toorefresh 內嵌 Power BI 的資料。</span><span class="sxs-lookup"><span data-stu-id="6eeda-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="6eeda-123">您必須變更 tooupload tooyour PBIX 檔案 tooPower BI Embedded。</span><span class="sxs-lookup"><span data-stu-id="6eeda-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="6eeda-124">這是因為 toono 可用的閘道。</span><span class="sxs-lookup"><span data-stu-id="6eeda-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="6eeda-125">使用 DirectQuery 的優點</span><span class="sxs-lookup"><span data-stu-id="6eeda-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="6eeda-126">使用 **DirectQuery**有兩項主要優點：</span><span class="sxs-lookup"><span data-stu-id="6eeda-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="6eeda-127">**DirectQuery**可讓您透過建立視覺效果的地方，否則會有並不可行 toofirst 匯入的極大型資料集的所有 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="6eeda-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="6eeda-128">基礎資料變更可能需要重新整理資料，並針對某些報表，hello 需要 toodisplay 目前資料可能會需要大型資料傳輸，造成重新匯入資料並不可行。</span><span class="sxs-lookup"><span data-stu-id="6eeda-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="6eeda-129">相較之下， **DirectQuery** 報表一律使用目前的資料。</span><span class="sxs-lookup"><span data-stu-id="6eeda-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="6eeda-130">DirectQuery 的限制</span><span class="sxs-lookup"><span data-stu-id="6eeda-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="6eeda-131">有一些限制 toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="6eeda-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="6eeda-132">所有資料表必須全都來自單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="6eeda-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="6eeda-133">如果 hello 查詢過於複雜時，會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6eeda-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="6eeda-134">tooremedy hello 錯誤，您必須重構 hello 查詢是較不複雜。</span><span class="sxs-lookup"><span data-stu-id="6eeda-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="6eeda-135">如果 hello 查詢必須很複雜，您將需要 tooimport hello 資料，而不是使用**DirectQuery**。</span><span class="sxs-lookup"><span data-stu-id="6eeda-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="6eeda-136">關聯性篩選為有限的 tooa 單一方向，而不是兩個方向。</span><span class="sxs-lookup"><span data-stu-id="6eeda-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="6eeda-137">您無法變更資料行 hello 資料類型。</span><span class="sxs-lookup"><span data-stu-id="6eeda-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="6eeda-138">根據預設，限制是置於量值允許的 DAX 運算式中。</span><span class="sxs-lookup"><span data-stu-id="6eeda-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="6eeda-139">請參閱 [DirectQuery 和量值](#measures)。</span><span class="sxs-lookup"><span data-stu-id="6eeda-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="6eeda-140">DirectQuery 和量值</span><span class="sxs-lookup"><span data-stu-id="6eeda-140">DirectQuery and measures</span></span>
<span data-ttu-id="6eeda-141">傳送 toohello 基礎資料來源的 tooensure 查詢可接受的效能，限制加諸於量值。</span><span class="sxs-lookup"><span data-stu-id="6eeda-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="6eeda-142">當使用**Power BI Desktop**進階使用者可以選擇 toobypass 這項限制選擇**檔案 > 選項和設定 > 選項**。</span><span class="sxs-lookup"><span data-stu-id="6eeda-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="6eeda-143">在 [hello**選項**] 對話方塊中，選擇**DirectQuery**，並選取 hello 選項**允許在 DirectQuery 模式中使用不受限制的量值**。</span><span class="sxs-lookup"><span data-stu-id="6eeda-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="6eeda-144">選取該選項後，即可使用對量值有效的任何 DAX 運算式。</span><span class="sxs-lookup"><span data-stu-id="6eeda-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="6eeda-145">使用者必須知道;但是，某些運算式的效能很好匯入 hello 資料時可能會導致查詢速度緩慢 toohello 後端來源在**DirectQuery**模式。</span><span class="sxs-lookup"><span data-stu-id="6eeda-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="6eeda-146">另請參閱</span><span class="sxs-lookup"><span data-stu-id="6eeda-146">See Also</span></span>
* [<span data-ttu-id="6eeda-147">開始使用 Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="6eeda-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="6eeda-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="6eeda-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="6eeda-149">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="6eeda-149">More questions?</span></span> [<span data-ttu-id="6eeda-150">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="6eeda-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

