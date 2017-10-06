---
title: "aaaRegister 在 Azure 資料目錄中的資料來源 |Microsoft 文件"
description: "本文章重點說明如何 tooregister 在 Azure 資料目錄，包括 hello 中繼資料欄位中的資料來源擷取登錄期間。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a><span data-ttu-id="f77bc-103">在 Azure 資料目錄中註冊資料來源</span><span class="sxs-lookup"><span data-stu-id="f77bc-103">Register data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="f77bc-104">簡介</span><span class="sxs-lookup"><span data-stu-id="f77bc-104">Introduction</span></span>
<span data-ttu-id="f77bc-105">Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料來源的註冊和探索系統。</span><span class="sxs-lookup"><span data-stu-id="f77bc-105">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and discovery for enterprise data sources.</span></span> <span data-ttu-id="f77bc-106">換句話說，資料目錄可於協助人們探索、了解和使用資料來源，並可協助組織從現有的資料獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="f77bc-106">In other words, Data Catalog helps people discover, understand, and use data sources, and it helps organizations get more value from their existing data.</span></span> <span data-ttu-id="f77bc-107">hello 第一個步驟 toomaking 資料來源可透過資料目錄探索是 tooregister 該資料來源。</span><span class="sxs-lookup"><span data-stu-id="f77bc-107">hello first step toomaking a data source discoverable via Data Catalog is tooregister that data source.</span></span>

## <a name="register-data-sources"></a><span data-ttu-id="f77bc-108">註冊資料來源</span><span class="sxs-lookup"><span data-stu-id="f77bc-108">Register data sources</span></span>
<span data-ttu-id="f77bc-109">註冊是 hello 資料來源擷取中繼資料，並複製該資料 toohello 資料目錄服務的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="f77bc-109">Registration is hello process of extracting metadata from hello data source and copying that data toohello Data Catalog service.</span></span> <span data-ttu-id="f77bc-110">hello 資料仍會保留它目前位於何處，而且仍在 hello hello 系統管理員控制與 hello 目前系統的原則。</span><span class="sxs-lookup"><span data-stu-id="f77bc-110">hello data remains where it currently resides, and it remains under hello control of hello administrators and policies of hello current system.</span></span>

<span data-ttu-id="f77bc-111">tooregister 資料來源，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="f77bc-111">tooregister a data source, do hello following:</span></span>
1. <span data-ttu-id="f77bc-112">在 hello Azure 資料目錄入口網站啟動 hello 資料目錄資料的來源註冊工具。</span><span class="sxs-lookup"><span data-stu-id="f77bc-112">In hello Azure Data Catalog portal, start hello Data Catalog data source registration tool.</span></span> 
2. <span data-ttu-id="f77bc-113">使用登入您的工作或學校帳戶，以 hello 相同 toosign 用於 toohello 入口網站的 Azure Active Directory 認證。</span><span class="sxs-lookup"><span data-stu-id="f77bc-113">Sign in with your work or school account with hello same Azure Active Directory credentials that you use toosign in toohello portal.</span></span>
3. <span data-ttu-id="f77bc-114">選取您想 tooregister hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="f77bc-114">Select hello data source you want tooregister.</span></span>

<span data-ttu-id="f77bc-115">如需逐步的詳細資訊，請參閱 hello[開始使用 Azure 資料目錄](data-catalog-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="f77bc-115">For more step-by-step details, see hello [Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial.</span></span>

<span data-ttu-id="f77bc-116">您已註冊 hello 資料來源之後，hello 目錄會追蹤其位置，而且它的中繼資料的索引。</span><span class="sxs-lookup"><span data-stu-id="f77bc-116">After you've registered hello data source, hello catalog tracks its location and indexes its metadata.</span></span> <span data-ttu-id="f77bc-117">使用者可以搜尋、 瀏覽，並探索 hello 資料來源，並使用 hello 應用程式或其選擇的工具，以使用其位置 tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="f77bc-117">Users can search, browse, and discover hello data source, and then use its location tooconnect tooit by using hello application or tool of their choice.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="f77bc-118">支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="f77bc-118">Supported data sources</span></span>
<span data-ttu-id="f77bc-119">請參閱[資料目錄 DSR](data-catalog-dsr.md) 以取得目前支援的資料來源清單。</span><span class="sxs-lookup"><span data-stu-id="f77bc-119">For a list of currently supported data sources, see [Data Catalog DSR](data-catalog-dsr.md).</span></span>

## <a name="structural-metadata"></a><span data-ttu-id="f77bc-120">結構化中繼資料</span><span class="sxs-lookup"><span data-stu-id="f77bc-120">Structural metadata</span></span>
<span data-ttu-id="f77bc-121">當您註冊的資料來源時，hello 註冊工具會擷取您所選取的 hello 物件 hello 結構的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f77bc-121">When you register a data source, hello registration tool extracts information about hello structure of hello objects you select.</span></span> <span data-ttu-id="f77bc-122">這項資訊是參照的 tooas 結構化中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f77bc-122">This information is referred tooas structural metadata.</span></span>

<span data-ttu-id="f77bc-123">所有物件，此結構的中繼資料包括 hello 物件的位置，以便探索 hello 資料的使用者可以使用自己選擇的 hello 用戶端工具中的該資訊 tooconnect toohello 物件。</span><span class="sxs-lookup"><span data-stu-id="f77bc-123">For all objects, this structural metadata includes hello object’s location, so that users who discover hello data can use that information tooconnect toohello object in hello client tools of their choice.</span></span> <span data-ttu-id="f77bc-124">其他的結構化中繼資料包含物件名稱和類型，以及屬性/資料行名稱和資料類型。</span><span class="sxs-lookup"><span data-stu-id="f77bc-124">Other structural metadata includes object name and type, and attribute/column name and data type.</span></span>

## <a name="descriptive-metadata"></a><span data-ttu-id="f77bc-125">描述性中繼資料</span><span class="sxs-lookup"><span data-stu-id="f77bc-125">Descriptive metadata</span></span>
<span data-ttu-id="f77bc-126">此外 toohello 核心 hello 資料來源擷取的結構化中繼資料、 hello 資料來源註冊工具會擷取具描述性的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f77bc-126">In addition toohello core structural metadata that's extracted from hello data source, hello data source registration tool extracts descriptive metadata.</span></span> <span data-ttu-id="f77bc-127">SQL Server Analysis Services 和 SQL Server Reporting Services，此中繼資料是來自這些服務所公開的 hello 描述屬性。</span><span class="sxs-lookup"><span data-stu-id="f77bc-127">For SQL Server Analysis Services and SQL Server Reporting Services, this metadata is taken from hello Description properties exposed by these services.</span></span> <span data-ttu-id="f77bc-128">針對 SQL Server，提供使用 hello ms 值\_擷取擴充屬性的描述。</span><span class="sxs-lookup"><span data-stu-id="f77bc-128">For SQL Server, values provided using hello ms\_description extended property is extracted.</span></span> <span data-ttu-id="f77bc-129">Oracle 資料庫的 hello 資料來源註冊工具擷取 hello 註解從資料行 hello 所有\_ 索引標籤\_註解的檢視。</span><span class="sxs-lookup"><span data-stu-id="f77bc-129">For Oracle Database, hello data-source registration tool extracts hello COMMENTS column from hello ALL\_TAB\_COMMENTS view.</span></span>

<span data-ttu-id="f77bc-130">加法 toohello 描述性中繼資料中擷取 hello 資料來源，使用者可以使用 hello 資料來源註冊工具輸入描述性的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f77bc-130">In addition toohello descriptive metadata that's extracted from hello data source, users can enter descriptive metadata by using hello data source registration tool.</span></span> <span data-ttu-id="f77bc-131">使用者可以加入標記，並可以識別 hello 物件所註冊的專家。</span><span class="sxs-lookup"><span data-stu-id="f77bc-131">Users can add tags, and they can identify experts for hello objects being registered.</span></span> <span data-ttu-id="f77bc-132">此描述性的中繼資料是所有複製 toohello 資料目錄服務，以及 hello 結構化中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f77bc-132">All this descriptive metadata is copied toohello Data Catalog service along with hello structural metadata.</span></span>

## <a name="include-previews"></a><span data-ttu-id="f77bc-133">包含預覽</span><span class="sxs-lookup"><span data-stu-id="f77bc-133">Include previews</span></span>
<span data-ttu-id="f77bc-134">根據預設，只有中繼資料會擷取從資料來源和複製的 toohello 資料目錄服務，但是了解資料來源通常更容易時您可以檢視它所包含的 hello 資料的範例。</span><span class="sxs-lookup"><span data-stu-id="f77bc-134">By default, only metadata is extracted from data sources and copied toohello Data Catalog service, but understanding a data source is often made easier when you can view a sample of hello data it contains.</span></span>

<span data-ttu-id="f77bc-135">使用 hello 資料來源的資料目錄註冊工具，您可以包含在每個資料表和檢視已註冊的 hello 資料的快照集預覽。</span><span class="sxs-lookup"><span data-stu-id="f77bc-135">By using hello Data Catalog data-source registration tool, you can include a snapshot preview of hello data in each table and view that is registered.</span></span> <span data-ttu-id="f77bc-136">如果您在註冊期間選擇 tooinclude 預覽，hello 註冊工具包括從每個資料表和檢視 too20 記錄。</span><span class="sxs-lookup"><span data-stu-id="f77bc-136">If you choose tooinclude previews during registration, hello registration tool includes up too20 records from each table and view.</span></span> <span data-ttu-id="f77bc-137">此快照集會然後複製 toohello 目錄以及 hello 結構化及描述性中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f77bc-137">This snapshot is then copied toohello catalog along with hello structural and descriptive metadata.</span></span>

> [!NOTE]
> <span data-ttu-id="f77bc-138">含有大量資料行的寬型資料表可能會在預覽中包含少於 20 筆的記錄。</span><span class="sxs-lookup"><span data-stu-id="f77bc-138">Wide tables with a large number of columns might have fewer than 20 records included in their preview.</span></span>
>
>

## <a name="include-data-profiles"></a><span data-ttu-id="f77bc-139">包含資料設定檔</span><span class="sxs-lookup"><span data-stu-id="f77bc-139">Include data profiles</span></span>
<span data-ttu-id="f77bc-140">就如同包括預覽可以搜尋資料目錄中的資料來源的使用者提供有價值的內容，包括資料設定檔可讓您更輕鬆 toounderstand 探索資料來源。</span><span class="sxs-lookup"><span data-stu-id="f77bc-140">Just as including previews can provide valuable context for users who search for data sources in Data Catalog, including a data profile can make it easier toounderstand discovered data sources.</span></span>

<span data-ttu-id="f77bc-141">您可以藉由使用 hello 資料來源的資料目錄註冊工具，包含每個資料表和檢視已註冊的資料設定檔。</span><span class="sxs-lookup"><span data-stu-id="f77bc-141">By using hello Data Catalog data-source registration tool, you can include a data profile for each table and view that is registered.</span></span> <span data-ttu-id="f77bc-142">如果您選擇 tooinclude 資料設定檔在註冊期間，hello 註冊工具包含有關 hello 資料彙總統計資料中每個資料表和檢視，包括：</span><span class="sxs-lookup"><span data-stu-id="f77bc-142">If you choose tooinclude a data profile during registration, hello registration tool includes aggregate statistics about hello data in each table and view, including:</span></span>

* <span data-ttu-id="f77bc-143">資料列的資料與大小 hello hello 物件中的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="f77bc-143">hello number of rows and size of hello data in hello object.</span></span>
* <span data-ttu-id="f77bc-144">hello hello hello 資料和 hello 物件結構描述的最新的更新日期。</span><span class="sxs-lookup"><span data-stu-id="f77bc-144">hello date for hello most recent update of hello data and hello object schema.</span></span>
* <span data-ttu-id="f77bc-145">null 的記錄和資料行的相異值的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="f77bc-145">hello number of null records and distinct values for columns.</span></span>
* <span data-ttu-id="f77bc-146">hello 最小值、 最大值、 平均和標準差資料行的值。</span><span class="sxs-lookup"><span data-stu-id="f77bc-146">hello minimum, maximum, average, and standard deviation values for columns.</span></span>

<span data-ttu-id="f77bc-147">這些統計資料會複製 toohello 目錄以及 hello 結構化及描述性中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f77bc-147">These statistics are then copied toohello catalog along with hello structural and descriptive metadata.</span></span>

> [!NOTE]
> <span data-ttu-id="f77bc-148">文字和日期資料行不會包含其資料設定檔中的平均值或標準差值統計資料。</span><span class="sxs-lookup"><span data-stu-id="f77bc-148">Text and date columns do not include average or standard deviation statistics in their data profile.</span></span>
>
>

## <a name="update-registrations"></a><span data-ttu-id="f77bc-149">更新註冊</span><span class="sxs-lookup"><span data-stu-id="f77bc-149">Update registrations</span></span>
<span data-ttu-id="f77bc-150">登錄資料來源可在資料目錄中可探索當您使用 hello 中繼資料及選擇性在註冊期間所擷取的預覽。</span><span class="sxs-lookup"><span data-stu-id="f77bc-150">Registering a data source makes it discoverable in Data Catalog when you use hello metadata and optional preview extracted during registration.</span></span> <span data-ttu-id="f77bc-151">如果 hello 資料來源必須在 hello 目錄中 （例如，如果 hello 物件結構描述已變更、 原本排除的資料表應該包含在內，或您想要包含在 hello 預覽 tooupdate hello 資料），更新 toobe hello 資料來源註冊工具可以重新執行。</span><span class="sxs-lookup"><span data-stu-id="f77bc-151">If hello data source needs toobe updated in hello catalog (for example, if hello schema of an object has changed, tables originally excluded should be included, or you want tooupdate hello data that's included in hello previews), hello data source registration tool can be re-run.</span></span>

<span data-ttu-id="f77bc-152">重新註冊已註冊的資料來源會執行合併 “upsert” 作業：將會更新現有的物件，同時建立新的物件。</span><span class="sxs-lookup"><span data-stu-id="f77bc-152">Re-registering an already-registered data source performs a merge “upsert” operation: existing objects are updated, and new objects are created.</span></span> <span data-ttu-id="f77bc-153">透過 hello 資料目錄入口網站的使用者提供的任何中繼資料會保留。</span><span class="sxs-lookup"><span data-stu-id="f77bc-153">Any metadata provided by users through hello Data Catalog portal are retained.</span></span>

## <a name="summary"></a><span data-ttu-id="f77bc-154">摘要</span><span class="sxs-lookup"><span data-stu-id="f77bc-154">Summary</span></span>
<span data-ttu-id="f77bc-155">因為它會複製結構化及描述性的中繼資料從資料來源 toohello 目錄服務，登錄在資料目錄中的 hello 資料來源可讓您更輕鬆 toodiscover 的 hello 資料，並了解。</span><span class="sxs-lookup"><span data-stu-id="f77bc-155">Because it copies structural and descriptive metadata from a data source toohello catalog service, registering hello data source in Data Catalog makes hello data easier toodiscover and understand.</span></span> <span data-ttu-id="f77bc-156">註冊 hello 資料來源之後，您可以加上註解、 管理及使用 hello 資料目錄入口網站探索。</span><span class="sxs-lookup"><span data-stu-id="f77bc-156">After you have registered hello data source, you can annotate, manage, and discover it by using hello Data Catalog portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f77bc-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f77bc-157">Next steps</span></span>
<span data-ttu-id="f77bc-158">如需註冊資料來源的詳細資訊，請參閱 hello[開始使用 Azure 資料目錄](data-catalog-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="f77bc-158">For more information about registering data sources, see hello [Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial.</span></span>
