---
title: "在 Azure 資料目錄中註冊資料來源 | Microsoft Docs"
description: "本文主要說明如何在 Azure 資料目錄中註冊資料來源，包括註冊期間擷取的中繼資料欄位。"
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
ms.openlocfilehash: 30166823b33669dda88b41a4aee2dfc34f01466f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a><span data-ttu-id="fd014-103">在 Azure 資料目錄中註冊資料來源</span><span class="sxs-lookup"><span data-stu-id="fd014-103">Register data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="fd014-104">簡介</span><span class="sxs-lookup"><span data-stu-id="fd014-104">Introduction</span></span>
<span data-ttu-id="fd014-105">Azure 資料目錄是受到完整管理的雲端服務，可作為企業資料來源的註冊和探索系統。</span><span class="sxs-lookup"><span data-stu-id="fd014-105">Azure Data Catalog is a fully managed cloud service that serves as a system of registration and discovery for enterprise data sources.</span></span> <span data-ttu-id="fd014-106">換句話說，資料目錄可於協助人們探索、了解和使用資料來源，並可協助組織從現有的資料獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="fd014-106">In other words, Data Catalog helps people discover, understand, and use data sources, and it helps organizations get more value from their existing data.</span></span> <span data-ttu-id="fd014-107">透過資料目錄讓資料來源得以被探索的第一步是註冊該資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-107">The first step to making a data source discoverable via Data Catalog is to register that data source.</span></span>

## <a name="register-data-sources"></a><span data-ttu-id="fd014-108">註冊資料來源</span><span class="sxs-lookup"><span data-stu-id="fd014-108">Register data sources</span></span>
<span data-ttu-id="fd014-109">註冊是指從資料來源擷取中繼資料並將該資料複製到資料目錄服務的程序。</span><span class="sxs-lookup"><span data-stu-id="fd014-109">Registration is the process of extracting metadata from the data source and copying that data to the Data Catalog service.</span></span> <span data-ttu-id="fd014-110">資料會保留在它目前的位置，並且仍然在目前系統的系統管理員及原則的控制之下。</span><span class="sxs-lookup"><span data-stu-id="fd014-110">The data remains where it currently resides, and it remains under the control of the administrators and policies of the current system.</span></span>

<span data-ttu-id="fd014-111">若要註冊資料來源，請執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="fd014-111">To register a data source, do the following:</span></span>
1. <span data-ttu-id="fd014-112">在 Azure 資料目錄入口網站中，啟動資料目錄的資料來源註冊工具。</span><span class="sxs-lookup"><span data-stu-id="fd014-112">In the Azure Data Catalog portal, start the Data Catalog data source registration tool.</span></span> 
2. <span data-ttu-id="fd014-113">使用您的工作或學校帳戶 (含有您用以登入入口網站的相同 Azure Active Directory 認證) 進行登入。</span><span class="sxs-lookup"><span data-stu-id="fd014-113">Sign in with your work or school account with the same Azure Active Directory credentials that you use to sign in to the portal.</span></span>
3. <span data-ttu-id="fd014-114">選取您要註冊的資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-114">Select the data source you want to register.</span></span>

<span data-ttu-id="fd014-115">如需更多的逐步詳細資料，請參閱[開始使用 Azure 資料目錄](data-catalog-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="fd014-115">For more step-by-step details, see the [Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial.</span></span>

<span data-ttu-id="fd014-116">在您註冊資料來源之後，目錄會追蹤其位置，並為其中繼資料編製索引。</span><span class="sxs-lookup"><span data-stu-id="fd014-116">After you've registered the data source, the catalog tracks its location and indexes its metadata.</span></span> <span data-ttu-id="fd014-117">使用者可以搜尋、瀏覽及探索資料來源，然後使用其選擇的應用程式或工具，透過資料來源的位置連線到該資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-117">Users can search, browse, and discover the data source, and then use its location to connect to it by using the application or tool of their choice.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="fd014-118">支援的資料來源</span><span class="sxs-lookup"><span data-stu-id="fd014-118">Supported data sources</span></span>
<span data-ttu-id="fd014-119">請參閱[資料目錄 DSR](data-catalog-dsr.md) 以取得目前支援的資料來源清單。</span><span class="sxs-lookup"><span data-stu-id="fd014-119">For a list of currently supported data sources, see [Data Catalog DSR](data-catalog-dsr.md).</span></span>

## <a name="structural-metadata"></a><span data-ttu-id="fd014-120">結構化中繼資料</span><span class="sxs-lookup"><span data-stu-id="fd014-120">Structural metadata</span></span>
<span data-ttu-id="fd014-121">當您註冊資料來源時，註冊工具會擷取您所選取之物件結構的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="fd014-121">When you register a data source, the registration tool extracts information about the structure of the objects you select.</span></span> <span data-ttu-id="fd014-122">這項資訊指的是結構化中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fd014-122">This information is referred to as structural metadata.</span></span>

<span data-ttu-id="fd014-123">對於所有物件而言，此結構化中繼資料將包含物件的位置，因此探索資料的使用者可以使用該資訊來連線至他們所選擇之用戶端工具中的物件。</span><span class="sxs-lookup"><span data-stu-id="fd014-123">For all objects, this structural metadata includes the object’s location, so that users who discover the data can use that information to connect to the object in the client tools of their choice.</span></span> <span data-ttu-id="fd014-124">其他的結構化中繼資料包含物件名稱和類型，以及屬性/資料行名稱和資料類型。</span><span class="sxs-lookup"><span data-stu-id="fd014-124">Other structural metadata includes object name and type, and attribute/column name and data type.</span></span>

## <a name="descriptive-metadata"></a><span data-ttu-id="fd014-125">描述性中繼資料</span><span class="sxs-lookup"><span data-stu-id="fd014-125">Descriptive metadata</span></span>
<span data-ttu-id="fd014-126">除了從資料來源擷取的核心結構化中繼資料之外，資料來源註冊工具也會擷取描述性中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fd014-126">In addition to the core structural metadata that's extracted from the data source, the data source registration tool extracts descriptive metadata.</span></span> <span data-ttu-id="fd014-127">針對 SQL Server Analysis Services 和 SQL Server Reporting Services，這項中繼資料是取自這些服務所公開的 Description 屬性。</span><span class="sxs-lookup"><span data-stu-id="fd014-127">For SQL Server Analysis Services and SQL Server Reporting Services, this metadata is taken from the Description properties exposed by these services.</span></span> <span data-ttu-id="fd014-128">針對 SQL Server，會擷取使用 ms\_description 擴充屬性所提供的值。</span><span class="sxs-lookup"><span data-stu-id="fd014-128">For SQL Server, values provided using the ms\_description extended property is extracted.</span></span> <span data-ttu-id="fd014-129">針對 Oracle Database，資料來源註冊工具會從 ALL\_TAB\_COMMENTS 檢視擷取 COMMENTS 資料行。</span><span class="sxs-lookup"><span data-stu-id="fd014-129">For Oracle Database, the data-source registration tool extracts the COMMENTS column from the ALL\_TAB\_COMMENTS view.</span></span>

<span data-ttu-id="fd014-130">除了從資料來源擷取的描述性中繼資料之外，使用者也可以使用資料來源註冊工具來輸入描述性中繼資料。</span><span class="sxs-lookup"><span data-stu-id="fd014-130">In addition to the descriptive metadata that's extracted from the data source, users can enter descriptive metadata by using the data source registration tool.</span></span> <span data-ttu-id="fd014-131">使用者可以新增標記，並且能夠識別所註冊之物件的專家。</span><span class="sxs-lookup"><span data-stu-id="fd014-131">Users can add tags, and they can identify experts for the objects being registered.</span></span> <span data-ttu-id="fd014-132">所有的描述性中繼資料會與結構化中繼資料一同複製到資料目錄服務。</span><span class="sxs-lookup"><span data-stu-id="fd014-132">All this descriptive metadata is copied to the Data Catalog service along with the structural metadata.</span></span>

## <a name="include-previews"></a><span data-ttu-id="fd014-133">包含預覽</span><span class="sxs-lookup"><span data-stu-id="fd014-133">Include previews</span></span>
<span data-ttu-id="fd014-134">根據預設，系統只會從資料來源擷取中繼資料，並複製到資料目錄服務，但如果您可以檢視其中所包含資料的範例，通常能更輕鬆地了解資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-134">By default, only metadata is extracted from data sources and copied to the Data Catalog service, but understanding a data source is often made easier when you can view a sample of the data it contains.</span></span>

<span data-ttu-id="fd014-135">透過使用資料目錄的資料來源註冊工具，您可以在每個已註冊的資料表和檢視中，加入資料的快照預覽。</span><span class="sxs-lookup"><span data-stu-id="fd014-135">By using the Data Catalog data-source registration tool, you can include a snapshot preview of the data in each table and view that is registered.</span></span> <span data-ttu-id="fd014-136">如果您選擇要在註冊期間包含預覽，註冊工具將包含每個資料表和檢視最多 20 筆記錄。</span><span class="sxs-lookup"><span data-stu-id="fd014-136">If you choose to include previews during registration, the registration tool includes up to 20 records from each table and view.</span></span> <span data-ttu-id="fd014-137">此快照之後會與結構化和描述性中繼資料一同複製到目錄。</span><span class="sxs-lookup"><span data-stu-id="fd014-137">This snapshot is then copied to the catalog along with the structural and descriptive metadata.</span></span>

> [!NOTE]
> <span data-ttu-id="fd014-138">含有大量資料行的寬型資料表可能會在預覽中包含少於 20 筆的記錄。</span><span class="sxs-lookup"><span data-stu-id="fd014-138">Wide tables with a large number of columns might have fewer than 20 records included in their preview.</span></span>
>
>

## <a name="include-data-profiles"></a><span data-ttu-id="fd014-139">包含資料設定檔</span><span class="sxs-lookup"><span data-stu-id="fd014-139">Include data profiles</span></span>
<span data-ttu-id="fd014-140">包含預覽可為在資料目錄中搜尋資料來源的使用者提供有用的內容；同樣地，包含資料設定檔也能讓使用者更輕鬆了解已探索的資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-140">Just as including previews can provide valuable context for users who search for data sources in Data Catalog, including a data profile can make it easier to understand discovered data sources.</span></span>

<span data-ttu-id="fd014-141">透過使用資料目錄的資料來源註冊工具，您可以為每個已註冊的資料表和檢視包含資料設定檔。</span><span class="sxs-lookup"><span data-stu-id="fd014-141">By using the Data Catalog data-source registration tool, you can include a data profile for each table and view that is registered.</span></span> <span data-ttu-id="fd014-142">如果您選擇在註冊期間包含資料設定檔，則註冊工具會在每個資料表和檢視中包含關於資料的彙總統計資料，包括：</span><span class="sxs-lookup"><span data-stu-id="fd014-142">If you choose to include a data profile during registration, the registration tool includes aggregate statistics about the data in each table and view, including:</span></span>

* <span data-ttu-id="fd014-143">物件中的資料列數和資料大小。</span><span class="sxs-lookup"><span data-stu-id="fd014-143">The number of rows and size of the data in the object.</span></span>
* <span data-ttu-id="fd014-144">資料和物件結構描述的最近更新日期。</span><span class="sxs-lookup"><span data-stu-id="fd014-144">The date for the most recent update of the data and the object schema.</span></span>
* <span data-ttu-id="fd014-145">Null 記錄與資料行相異值的數目。</span><span class="sxs-lookup"><span data-stu-id="fd014-145">The number of null records and distinct values for columns.</span></span>
* <span data-ttu-id="fd014-146">資料行的最小值、最大值、平均值和標準差值。</span><span class="sxs-lookup"><span data-stu-id="fd014-146">The minimum, maximum, average, and standard deviation values for columns.</span></span>

<span data-ttu-id="fd014-147">這些統計資料之後會與結構化和描述性中繼資料一同複製到目錄。</span><span class="sxs-lookup"><span data-stu-id="fd014-147">These statistics are then copied to the catalog along with the structural and descriptive metadata.</span></span>

> [!NOTE]
> <span data-ttu-id="fd014-148">文字和日期資料行不會包含其資料設定檔中的平均值或標準差值統計資料。</span><span class="sxs-lookup"><span data-stu-id="fd014-148">Text and date columns do not include average or standard deviation statistics in their data profile.</span></span>
>
>

## <a name="update-registrations"></a><span data-ttu-id="fd014-149">更新註冊</span><span class="sxs-lookup"><span data-stu-id="fd014-149">Update registrations</span></span>
<span data-ttu-id="fd014-150">註冊資料來源讓您得以使用註冊期間擷取的中繼資料和選擇性預覽，藉此在資料目錄中探索資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-150">Registering a data source makes it discoverable in Data Catalog when you use the metadata and optional preview extracted during registration.</span></span> <span data-ttu-id="fd014-151">如果在目錄中的資料來源需要更新 (例如，如果物件的結構描述已經變更、或應包含原先排除的資料表，或您想要更新在預覽中所包含的資料)，可以重新執行資料來源註冊工具。</span><span class="sxs-lookup"><span data-stu-id="fd014-151">If the data source needs to be updated in the catalog (for example, if the schema of an object has changed, tables originally excluded should be included, or you want to update the data that's included in the previews), the data source registration tool can be re-run.</span></span>

<span data-ttu-id="fd014-152">重新註冊已註冊的資料來源會執行合併 “upsert” 作業：將會更新現有的物件，同時建立新的物件。</span><span class="sxs-lookup"><span data-stu-id="fd014-152">Re-registering an already-registered data source performs a merge “upsert” operation: existing objects are updated, and new objects are created.</span></span> <span data-ttu-id="fd014-153">使用者透過資料目錄入口網站所提供的任何中繼資料都將保留。</span><span class="sxs-lookup"><span data-stu-id="fd014-153">Any metadata provided by users through the Data Catalog portal are retained.</span></span>

## <a name="summary"></a><span data-ttu-id="fd014-154">摘要</span><span class="sxs-lookup"><span data-stu-id="fd014-154">Summary</span></span>
<span data-ttu-id="fd014-155">因為在資料目錄註冊資料來源會將結構化和描述性中繼資料從資料來源複製到目錄服務，所以可讓您更容易地探索及了解資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-155">Because it copies structural and descriptive metadata from a data source to the catalog service, registering the data source in Data Catalog makes the data easier to discover and understand.</span></span> <span data-ttu-id="fd014-156">在您註冊資料來源之後，即可使用資料目錄入口網站來標註、管理及探索資料來源。</span><span class="sxs-lookup"><span data-stu-id="fd014-156">After you have registered the data source, you can annotate, manage, and discover it by using the Data Catalog portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd014-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd014-157">Next steps</span></span>
<span data-ttu-id="fd014-158">如需註冊資料來源的詳細資訊，請參閱[開始使用 Azure 資料目錄](data-catalog-get-started.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="fd014-158">For more information about registering data sources, see the [Get Started with Azure Data Catalog](data-catalog-get-started.md) tutorial.</span></span>
