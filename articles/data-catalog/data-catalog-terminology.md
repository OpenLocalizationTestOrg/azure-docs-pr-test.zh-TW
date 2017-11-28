---
title: "aaaAzure 資料目錄術語 |Microsoft 文件"
description: "本文章提供簡介 tooconcepts 和使用 Azure 資料目錄文件中的詞彙。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a><span data-ttu-id="230c2-103">Azure 資料目錄術語</span><span class="sxs-lookup"><span data-stu-id="230c2-103">Azure Data Catalog terminology</span></span>
## <a name="catalog"></a><span data-ttu-id="230c2-104">目錄</span><span class="sxs-lookup"><span data-stu-id="230c2-104">Catalog</span></span>
<span data-ttu-id="230c2-105">hello Azure 資料目錄是以雲端為基礎的中繼資料儲存機制中的資料來源和資料資產都可以註冊。</span><span class="sxs-lookup"><span data-stu-id="230c2-105">hello Azure Data Catalog is a cloud-based metadata repository in which data sources and data assets can be registered.</span></span> <span data-ttu-id="230c2-106">hello 類別目錄做為擷取自資料來源的結構化中繼資料和使用者所加入的描述性中繼資料的中央存放位置。</span><span class="sxs-lookup"><span data-stu-id="230c2-106">hello catalog serves as a central storage location for structural metadata extracted from data sources and for descriptive metadata added by users.</span></span>

## <a name="data-source"></a><span data-ttu-id="230c2-107">資料來源</span><span class="sxs-lookup"><span data-stu-id="230c2-107">Data source</span></span>
<span data-ttu-id="230c2-108">資料來源是管理資料資產的系統或容器。</span><span class="sxs-lookup"><span data-stu-id="230c2-108">A data source is a system or container that manages data assets.</span></span> <span data-ttu-id="230c2-109">範例包括 SQL Server 資料庫、Oracle 資料庫、SQL Server Analysis Services 資料庫 (表格式或多維度) 和 SQL Server Reporting Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="230c2-109">Examples include SQL Server databases, Oracle databases, SQL Server Analysis Services databases (tabular or multidimensional) and SQL Server Reporting Services servers.</span></span>

## <a name="data-asset"></a><span data-ttu-id="230c2-110">資料資產</span><span class="sxs-lookup"><span data-stu-id="230c2-110">Data asset</span></span>
<span data-ttu-id="230c2-111">資料資產是內含的資料來源，可以向 hello 目錄物件。</span><span class="sxs-lookup"><span data-stu-id="230c2-111">Data assets are objects contained within data sources that can be registered with hello catalog.</span></span> <span data-ttu-id="230c2-112">範例包括 SQL Server 資料表和檢視、Oracle 資料表和檢視、SQL Server Analysis Services 量值、維度和 KPI，以及 SQL Server Reporting Services 報表。</span><span class="sxs-lookup"><span data-stu-id="230c2-112">Examples include SQL Server tables and views, Oracle tables and views, SQL Server Analysis Services measures, dimensions and KPIs, and SQL Server Reporting Services reports.</span></span>

## <a name="data-asset-location"></a><span data-ttu-id="230c2-113">資料資產位置</span><span class="sxs-lookup"><span data-stu-id="230c2-113">Data asset location</span></span>
<span data-ttu-id="230c2-114">hello 目錄會將儲存的資料來源或資料資產，可以使用的 tooconnect toohello hello 位置來源使用的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="230c2-114">hello catalog stores hello location of a data source or data asset, which can be used tooconnect toohello source using a client application.</span></span> <span data-ttu-id="230c2-115">hello 格式和 hello 位置的詳細資料隨著 hello 資料來源類型。</span><span class="sxs-lookup"><span data-stu-id="230c2-115">hello format and details of hello location vary based on hello data source type.</span></span> <span data-ttu-id="230c2-116">比方說，SQL Server 資料表可以透過其四段名稱來識別 – 伺服器名稱、資料庫名稱、結構描述名稱、物件名稱 – 而 SQL Server Reporting Services 報表可以透過其 URL 來識別。</span><span class="sxs-lookup"><span data-stu-id="230c2-116">For example, a SQL Server table can be identified by its four part name – server name, database name, schema name, object name – while a SQL Server Reporting Services Report can be identified by its URL.</span></span>

## <a name="structural-metadata"></a><span data-ttu-id="230c2-117">結構化中繼資料</span><span class="sxs-lookup"><span data-stu-id="230c2-117">Structural metadata</span></span>
<span data-ttu-id="230c2-118">結構化中繼資料是從說明 hello 結構的資料資產的資料來源擷取的 hello 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="230c2-118">Structural metadata is hello metadata extracted from a data source that describes hello structure of a data asset.</span></span> <span data-ttu-id="230c2-119">這包括 hello 資產位置、 其物件名稱和類型，以及其他特定類型的特性。</span><span class="sxs-lookup"><span data-stu-id="230c2-119">This includes hello assets location, its object name and type, and additional type-specific characteristics.</span></span> <span data-ttu-id="230c2-120">例如，hello 結構化中繼資料資料表和檢視表包含 hello 名稱和 hello 物件資料行的資料類型。</span><span class="sxs-lookup"><span data-stu-id="230c2-120">For example, hello structural metadata for tables and views includes hello names and data types for hello object’s columns.</span></span>

## <a name="descriptive-metadata"></a><span data-ttu-id="230c2-121">描述性中繼資料</span><span class="sxs-lookup"><span data-stu-id="230c2-121">Descriptive metadata</span></span>
<span data-ttu-id="230c2-122">描述性的中繼資料是描述 hello 用途或目的資料資產的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="230c2-122">Descriptive metadata is metadata that describes hello purpose or intent of a data asset.</span></span> <span data-ttu-id="230c2-123">通常描述性的中繼資料已加入之目錄的使用者使用 hello Azure 資料目錄入口網站，但它也可從擷取 hello 資料來源登錄期間。</span><span class="sxs-lookup"><span data-stu-id="230c2-123">Typically descriptive metadata is added by catalog users using hello Azure Data Catalog portal, but it can also be extracted from hello data source during registration.</span></span> <span data-ttu-id="230c2-124">例如，hello Azure 資料目錄註冊工具將會擷取描述從 hello 描述屬性在 SQL Server Analysis Services 和 SQL Server Reporting Services，以及從 hello [ms_description 擴充屬性](https://technet.microsoft.com/library/ms190243.aspx)在 SQL Server 資料庫中，如果這些屬性已填入值。</span><span class="sxs-lookup"><span data-stu-id="230c2-124">For example, hello Azure Data Catalog registration tool will extract descriptions from hello Description property in SQL Server Analysis Services and SQL Server Reporting Services, and from hello [ms_description extended property](https://technet.microsoft.com/library/ms190243.aspx) in SQL Server databases, if these properties have been populated with values.</span></span>

## <a name="request-access"></a><span data-ttu-id="230c2-125">要求存取</span><span class="sxs-lookup"><span data-stu-id="230c2-125">Request access</span></span>
<span data-ttu-id="230c2-126">資料資產的描述性中繼資料可以包含 toorequest toohello 資料資產或資料來源的存取方式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="230c2-126">A data asset's descriptive metadata can include information on how toorequest access toohello data asset or data source.</span></span> <span data-ttu-id="230c2-127">這項資訊會看見 hello 資料資產的位置，並可以包含一或多個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="230c2-127">This information is presented with hello data asset location, and can include one or more of hello following options:</span></span>

* <span data-ttu-id="230c2-128">hello hello 使用者或小組負責授與存取 toohello 資料來源的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="230c2-128">hello email address of hello user or team responsible for granting access toohello data source.</span></span>
* <span data-ttu-id="230c2-129">hello hello URL 記載的使用者必須遵循 toogain access toohello 資料來源的程序。</span><span class="sxs-lookup"><span data-stu-id="230c2-129">hello URL of hello documented process that users must follow toogain access toohello data source.</span></span>
* <span data-ttu-id="230c2-130">hello 的身分識別和存取管理工具 (例如 Microsoft Identity Manager) 可以使用的 toogain access toohello 資料來源的 URL。</span><span class="sxs-lookup"><span data-stu-id="230c2-130">hello URL of an identity and access management tool (such as Microsoft Identity Manager) that can be used toogain access toohello data source.</span></span>
* <span data-ttu-id="230c2-131">任意文字項目，描述使用者可以獲得存取 toohello 資料來源的方式。</span><span class="sxs-lookup"><span data-stu-id="230c2-131">A free-text entry that describes how users can gain access toohello data source.</span></span>

## <a name="preview"></a><span data-ttu-id="230c2-132">預覽</span><span class="sxs-lookup"><span data-stu-id="230c2-132">Preview</span></span>
<span data-ttu-id="230c2-133">在 Azure 資料目錄中的預覽是 too20 記錄可以在註冊期間，從 hello 資料來源中擷取和儲存在 hello 與 hello 資料資產中繼資料的目錄中的快照。</span><span class="sxs-lookup"><span data-stu-id="230c2-133">A preview in Azure Data Catalog is a snapshot of up too20 records that can be extracted from hello data source during registration, and stored in hello catalog with hello data asset metadata.</span></span> <span data-ttu-id="230c2-134">hello 預覽可協助使用者探索資料資產深入了解其功能與用途。</span><span class="sxs-lookup"><span data-stu-id="230c2-134">hello preview can help users who discover a data asset better understand its function and purpose.</span></span> <span data-ttu-id="230c2-135">換句話說，查看範例資料可以比看到剛才 hello 資料行名稱和資料類型更有價值。</span><span class="sxs-lookup"><span data-stu-id="230c2-135">In other words, seeing sample data can be more valuable than seeing just hello column names and data types.</span></span>
<span data-ttu-id="230c2-136">預覽只支援資料表和檢視表，而必須明確選取的 hello 使用者在註冊期間。</span><span class="sxs-lookup"><span data-stu-id="230c2-136">Previews are only supported for tables and views, and must be explicitly selected by hello user during registration.</span></span>

## <a name="data-profile"></a><span data-ttu-id="230c2-137">資料設定檔</span><span class="sxs-lookup"><span data-stu-id="230c2-137">Data Profile</span></span>
<span data-ttu-id="230c2-138">在 Azure 資料目錄中的資料設定檔是有關已註冊的資料資產可以在註冊期間，從 hello 資料來源中擷取和儲存在 hello 與 hello 資料資產中繼資料的類別目錄資料表層級和資料行層級中繼資料的快照集。</span><span class="sxs-lookup"><span data-stu-id="230c2-138">A data profile in Azure Data Catalog is a snapshot of table-level and column-level metadata about a registered data asset that can be extracted from hello data source during registration, and stored in hello catalog with hello data asset metadata.</span></span> <span data-ttu-id="230c2-139">hello 資料設定檔可協助使用者探索資料資產深入了解其功能與用途。</span><span class="sxs-lookup"><span data-stu-id="230c2-139">hello data profile can help users who discover a data asset better understand its function and purpose.</span></span> <span data-ttu-id="230c2-140">類似 toopreviews，資料設定檔必須明確選取的 hello 使用者在註冊期間。</span><span class="sxs-lookup"><span data-stu-id="230c2-140">Similar toopreviews, data profiles must be explicitly selected by hello user during registration.</span></span>

> [!NOTE]
> <span data-ttu-id="230c2-141">擷取的資料設定檔可以是昂貴的作業，大型資料表和檢視表，而且可能會大幅增加 hello 所需時間 tooregister 資料來源。</span><span class="sxs-lookup"><span data-stu-id="230c2-141">Extracting a data profile can be a costly operation for large tables and views, and may significantly increase hello time required tooregister a data source.</span></span>
>
>

## <a name="user-perspective"></a><span data-ttu-id="230c2-142">使用者觀點</span><span class="sxs-lookup"><span data-stu-id="230c2-142">User perspective</span></span>
<span data-ttu-id="230c2-143">在 Azure 資料目錄中，任何使用者都可以為已註冊的資料資產提供描述性中繼資料。</span><span class="sxs-lookup"><span data-stu-id="230c2-143">In Azure Data Catalog, any user can provide descriptive metadata for a registered data asset.</span></span> <span data-ttu-id="230c2-144">每個使用者擁有 hello 資料和其使用不同的檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="230c2-144">Each user has a distinct perspective on hello data and its use.</span></span> <span data-ttu-id="230c2-145">例如，hello 負責在伺服器的系統管理員可能會提供其服務等級協定 (SLA) 的備份時間範圍; hello 詳細資料資料管理人可能提供連結 toodocumentation hello 的商務處理 hello 資料支援。而且分析師可能提供 hello 條款最相關的 tooother 分析師，而且它可以是最有價值 toothose 使用者需要 toodiscover 及了解 hello 資料中的描述。</span><span class="sxs-lookup"><span data-stu-id="230c2-145">For example, hello administrator responsible for a server may provide hello details of its service level agreement (SLA) or backup windows; a data steward may provide links toodocumentation for hello business processes hello data supports; and an analyst may provide a description in hello terms that are most relevant tooother analysts, and which can be most valuable toothose users who need toodiscover and understand hello data.</span></span>

<span data-ttu-id="230c2-146">每個這些檢視方塊是原本就相當重要，而且與 Azure 資料目錄每一位使用者可以提供是有意義的 toothem，而所有的使用者可以使用該資訊 toounderstand hello 資料和其用途的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="230c2-146">Each of these perspectives are inherently valuable, and with Azure Data Catalog each user can provide hello information that is meaningful toothem, while all users can use that information toounderstand hello data and its purpose.</span></span>

## <a name="expert"></a><span data-ttu-id="230c2-147">專家</span><span class="sxs-lookup"><span data-stu-id="230c2-147">Expert</span></span>
<span data-ttu-id="230c2-148">專家是指公認對資料資產有其獨特「專家」觀點的使用者。</span><span class="sxs-lookup"><span data-stu-id="230c2-148">An expert is a user who has been identified as having an informed “expert” perspective for a data asset.</span></span> <span data-ttu-id="230c2-149">任何使用者都可以將自己或其他使用者加入成為資產的專家。</span><span class="sxs-lookup"><span data-stu-id="230c2-149">Any user can add themselves or another user as an expert for an asset.</span></span> <span data-ttu-id="230c2-150">被列為專家並未傳達任何額外的權限，在 Azure 資料目錄。它可讓使用者 tooeasily 找出這些檢閱資產的描述性中繼資料時是最有可能 toobe 有用的檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="230c2-150">Being listed as an expert does not convey any additional privileges in Azure Data Catalog; it allows users tooeasily locate those perspectives that are most likely toobe useful when reviewing an asset’s descriptive metadata.</span></span>

## <a name="owner"></a><span data-ttu-id="230c2-151">擁有者</span><span class="sxs-lookup"><span data-stu-id="230c2-151">Owner</span></span>
<span data-ttu-id="230c2-152">擁有者是具有額外權限來管理 Azure 資料目錄中的資料資產的使用者。</span><span class="sxs-lookup"><span data-stu-id="230c2-152">An owner is a user who has additional privileges for managing a data asset in Azure Data Catalog.</span></span> <span data-ttu-id="230c2-153">使用者可以取得已註冊的資料資產的擁有權，而擁有者可以加入其他使用者成為共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="230c2-153">Users can take ownership of registered data assets, and owners can add other users as co-owners.</span></span> <span data-ttu-id="230c2-154">如需詳細資訊，請參閱[如何 toomanage 資料資產](data-catalog-how-to-manage.md)</span><span class="sxs-lookup"><span data-stu-id="230c2-154">For more information see  [How toomanage data assets](data-catalog-how-to-manage.md)</span></span>  

> [!NOTE]
> <span data-ttu-id="230c2-155">擁有權和管理都只能在 hello 標準版本的 Azure 資料目錄。</span><span class="sxs-lookup"><span data-stu-id="230c2-155">Ownership and management are available only in hello Standard Edition of Azure Data Catalog.</span></span>
>
>

## <a name="registration"></a><span data-ttu-id="230c2-156">註冊</span><span class="sxs-lookup"><span data-stu-id="230c2-156">Registration</span></span>
<span data-ttu-id="230c2-157">註冊是從資料來源擷取資料資產中繼資料，並複製它 toohello Azure 資料目錄服務的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="230c2-157">Registration is hello act of extracting data asset metadata from a data source and copying it toohello Azure Data Catalog service.</span></span> <span data-ttu-id="230c2-158">然後就可以加註和探索已註冊的資料資產。</span><span class="sxs-lookup"><span data-stu-id="230c2-158">Data assets that have been registered can then be annotated and discovered.</span></span>

## <a name="see-also"></a><span data-ttu-id="230c2-159">另請參閱</span><span class="sxs-lookup"><span data-stu-id="230c2-159">See also</span></span>
* [<span data-ttu-id="230c2-160">什麼是 Azure 資料目錄？</span><span class="sxs-lookup"><span data-stu-id="230c2-160">What is Azure Data Catalog?</span></span>](data-catalog-what-is-data-catalog.md) <span data-ttu-id="230c2-161">-這篇文章提供 hello Azure 資料目錄服務、 hello 值提供，以及它所支援的 hello 案例的概觀。</span><span class="sxs-lookup"><span data-stu-id="230c2-161">- This article provides an overview of hello Azure Data Catalog service, hello value it provides, and hello scenarios it supports.</span></span>
* <span data-ttu-id="230c2-162">[開始使用 Azure 資料目錄](data-catalog-get-started.md)-本文章提供端對端教學課程中，為您示範如何 toouse Azure 資料目錄的資料來源搜索。</span><span class="sxs-lookup"><span data-stu-id="230c2-162">[Get started with Azure Data Catalog](data-catalog-get-started.md) - This article provides an end-to-end tutorial that shows you how toouse Azure Data Catalog for data source discovery.</span></span>  
