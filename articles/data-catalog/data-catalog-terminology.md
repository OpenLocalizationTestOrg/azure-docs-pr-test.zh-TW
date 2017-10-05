---
title: "Azure 資料目錄術語 | Microsoft Docs"
description: "本文提供 Azure 資料目錄文件所使用之概念與術語的簡介。"
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
ms.openlocfilehash: 557b529f45c7fbc286b7e1893d4b4688e088ed91
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-terminology"></a><span data-ttu-id="2677a-103">Azure 資料目錄術語</span><span class="sxs-lookup"><span data-stu-id="2677a-103">Azure Data Catalog terminology</span></span>
## <a name="catalog"></a><span data-ttu-id="2677a-104">目錄</span><span class="sxs-lookup"><span data-stu-id="2677a-104">Catalog</span></span>
<span data-ttu-id="2677a-105">Azure 資料目錄是以雲端為基礎的中繼資料儲存機制，其中可以註冊資料來源和資料資產。</span><span class="sxs-lookup"><span data-stu-id="2677a-105">The Azure Data Catalog is a cloud-based metadata repository in which data sources and data assets can be registered.</span></span> <span data-ttu-id="2677a-106">此目錄做為中央儲存位置，儲存從資料來源擷取的結構化中繼資料和使用者加入的描述性中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2677a-106">The catalog serves as a central storage location for structural metadata extracted from data sources and for descriptive metadata added by users.</span></span>

## <a name="data-source"></a><span data-ttu-id="2677a-107">資料來源</span><span class="sxs-lookup"><span data-stu-id="2677a-107">Data source</span></span>
<span data-ttu-id="2677a-108">資料來源是管理資料資產的系統或容器。</span><span class="sxs-lookup"><span data-stu-id="2677a-108">A data source is a system or container that manages data assets.</span></span> <span data-ttu-id="2677a-109">範例包括 SQL Server 資料庫、Oracle 資料庫、SQL Server Analysis Services 資料庫 (表格式或多維度) 和 SQL Server Reporting Services 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2677a-109">Examples include SQL Server databases, Oracle databases, SQL Server Analysis Services databases (tabular or multidimensional) and SQL Server Reporting Services servers.</span></span>

## <a name="data-asset"></a><span data-ttu-id="2677a-110">資料資產</span><span class="sxs-lookup"><span data-stu-id="2677a-110">Data asset</span></span>
<span data-ttu-id="2677a-111">資料資產是資料來源內可向目錄註冊的物件。</span><span class="sxs-lookup"><span data-stu-id="2677a-111">Data assets are objects contained within data sources that can be registered with the catalog.</span></span> <span data-ttu-id="2677a-112">範例包括 SQL Server 資料表和檢視、Oracle 資料表和檢視、SQL Server Analysis Services 量值、維度和 KPI，以及 SQL Server Reporting Services 報表。</span><span class="sxs-lookup"><span data-stu-id="2677a-112">Examples include SQL Server tables and views, Oracle tables and views, SQL Server Analysis Services measures, dimensions and KPIs, and SQL Server Reporting Services reports.</span></span>

## <a name="data-asset-location"></a><span data-ttu-id="2677a-113">資料資產位置</span><span class="sxs-lookup"><span data-stu-id="2677a-113">Data asset location</span></span>
<span data-ttu-id="2677a-114">目錄儲存資料來源或資料資產的位置，可供用戶端應用程式連接到來源。</span><span class="sxs-lookup"><span data-stu-id="2677a-114">The catalog stores the location of a data source or data asset, which can be used to connect to the source using a client application.</span></span> <span data-ttu-id="2677a-115">位置的格式和詳細資料隨資料來源類型而不同。</span><span class="sxs-lookup"><span data-stu-id="2677a-115">The format and details of the location vary based on the data source type.</span></span> <span data-ttu-id="2677a-116">比方說，SQL Server 資料表可以透過其四段名稱來識別 – 伺服器名稱、資料庫名稱、結構描述名稱、物件名稱 – 而 SQL Server Reporting Services 報表可以透過其 URL 來識別。</span><span class="sxs-lookup"><span data-stu-id="2677a-116">For example, a SQL Server table can be identified by its four part name – server name, database name, schema name, object name – while a SQL Server Reporting Services Report can be identified by its URL.</span></span>

## <a name="structural-metadata"></a><span data-ttu-id="2677a-117">結構化中繼資料</span><span class="sxs-lookup"><span data-stu-id="2677a-117">Structural metadata</span></span>
<span data-ttu-id="2677a-118">結構化中繼資料是從資料來源擷取的中繼資料，用來描述資料資產的結構。</span><span class="sxs-lookup"><span data-stu-id="2677a-118">Structural metadata is the metadata extracted from a data source that describes the structure of a data asset.</span></span> <span data-ttu-id="2677a-119">這包括資產位置、其物件名稱和類型，以及關於類型的其他特性。</span><span class="sxs-lookup"><span data-stu-id="2677a-119">This includes the assets location, its object name and type, and additional type-specific characteristics.</span></span> <span data-ttu-id="2677a-120">例如，資料表和檢視的結構化中繼資料包含物件資料行的名稱和資料類型。</span><span class="sxs-lookup"><span data-stu-id="2677a-120">For example, the structural metadata for tables and views includes the names and data types for the object’s columns.</span></span>

## <a name="descriptive-metadata"></a><span data-ttu-id="2677a-121">描述性中繼資料</span><span class="sxs-lookup"><span data-stu-id="2677a-121">Descriptive metadata</span></span>
<span data-ttu-id="2677a-122">描述性中繼資料是描述資料資產的用途或意圖的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2677a-122">Descriptive metadata is metadata that describes the purpose or intent of a data asset.</span></span> <span data-ttu-id="2677a-123">描述性中繼資料通常由目錄使用者利用 Azure 資料目錄入口網站來加入，但也可以在註冊期間從資料來源擷取。</span><span class="sxs-lookup"><span data-stu-id="2677a-123">Typically descriptive metadata is added by catalog users using the Azure Data Catalog portal, but it can also be extracted from the data source during registration.</span></span> <span data-ttu-id="2677a-124">例如，Azure 資料目錄註冊工具將會從 SQL Server Analysis Services 和 SQL Server Reporting Services 中的 Description 屬性擷取描述，以及從 SQL Server 資料庫中的 [ms_description 擴充屬性](https://technet.microsoft.com/library/ms190243.aspx)擷取描述 (如果這些屬性已填入值)。</span><span class="sxs-lookup"><span data-stu-id="2677a-124">For example, the Azure Data Catalog registration tool will extract descriptions from the Description property in SQL Server Analysis Services and SQL Server Reporting Services, and from the [ms_description extended property](https://technet.microsoft.com/library/ms190243.aspx) in SQL Server databases, if these properties have been populated with values.</span></span>

## <a name="request-access"></a><span data-ttu-id="2677a-125">要求存取</span><span class="sxs-lookup"><span data-stu-id="2677a-125">Request access</span></span>
<span data-ttu-id="2677a-126">資料資產的描述性中繼資料可以包含如何要求存取資料資產或資料來源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2677a-126">A data asset's descriptive metadata can include information on how to request access to the data asset or data source.</span></span> <span data-ttu-id="2677a-127">這項資訊會與資料資產位置一併顯示，且可包含一個或多個下列選項：</span><span class="sxs-lookup"><span data-stu-id="2677a-127">This information is presented with the data asset location, and can include one or more of the following options:</span></span>

* <span data-ttu-id="2677a-128">負責授與資料來源存取權之使用者或小組的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="2677a-128">The email address of the user or team responsible for granting access to the data source.</span></span>
* <span data-ttu-id="2677a-129">記載程序的 URL，使用者必須遵循才能取得資料來源的存取權。</span><span class="sxs-lookup"><span data-stu-id="2677a-129">The URL of the documented process that users must follow to gain access to the data source.</span></span>
* <span data-ttu-id="2677a-130">身分識別和存取管理工具 (例如 Microsoft Identity Manager) 的 URL，可以用來取得資料來源的存取權。</span><span class="sxs-lookup"><span data-stu-id="2677a-130">The URL of an identity and access management tool (such as Microsoft Identity Manager) that can be used to gain access to the data source.</span></span>
* <span data-ttu-id="2677a-131">任意文字項目，用來描述使用者如何取得資料來源的存取權。</span><span class="sxs-lookup"><span data-stu-id="2677a-131">A free-text entry that describes how users can gain access to the data source.</span></span>

## <a name="preview"></a><span data-ttu-id="2677a-132">預覽</span><span class="sxs-lookup"><span data-stu-id="2677a-132">Preview</span></span>
<span data-ttu-id="2677a-133">Azure 資料目錄中的預覽是最多 20 筆記錄的快照集，可以在註冊期間從資料來源中擷取，並與資料資產中繼資料一起儲存在目錄中。</span><span class="sxs-lookup"><span data-stu-id="2677a-133">A preview in Azure Data Catalog is a snapshot of up to 20 records that can be extracted from the data source during registration, and stored in the catalog with the data asset metadata.</span></span> <span data-ttu-id="2677a-134">預覽可協助使用者在探索資料資產時充分了解其功能和用途。</span><span class="sxs-lookup"><span data-stu-id="2677a-134">The preview can help users who discover a data asset better understand its function and purpose.</span></span> <span data-ttu-id="2677a-135">換句話說，查看範例資料比只看到資料行名稱和資料類型更有價值。</span><span class="sxs-lookup"><span data-stu-id="2677a-135">In other words, seeing sample data can be more valuable than seeing just the column names and data types.</span></span>
<span data-ttu-id="2677a-136">僅支援預覽資料表和檢視，而且必須由使用者在註冊期間明確選取。</span><span class="sxs-lookup"><span data-stu-id="2677a-136">Previews are only supported for tables and views, and must be explicitly selected by the user during registration.</span></span>

## <a name="data-profile"></a><span data-ttu-id="2677a-137">資料設定檔</span><span class="sxs-lookup"><span data-stu-id="2677a-137">Data Profile</span></span>
<span data-ttu-id="2677a-138">Azure 資料目錄中的資料設定檔是資料表層級的快照集和及資料行層級的中繼資料，已註冊的資料資產在註冊期間可從資料來源中擷取，並與資料資產中繼資料一起儲存在目錄中。</span><span class="sxs-lookup"><span data-stu-id="2677a-138">A data profile in Azure Data Catalog is a snapshot of table-level and column-level metadata about a registered data asset that can be extracted from the data source during registration, and stored in the catalog with the data asset metadata.</span></span> <span data-ttu-id="2677a-139">資料設定檔可協助使用者在探索資料資產時充分了解其功能和用途。</span><span class="sxs-lookup"><span data-stu-id="2677a-139">The data profile can help users who discover a data asset better understand its function and purpose.</span></span> <span data-ttu-id="2677a-140">和預覽相同，資料設定檔必須是使用者在註冊期間明確選取的資料。</span><span class="sxs-lookup"><span data-stu-id="2677a-140">Similar to previews, data profiles must be explicitly selected by the user during registration.</span></span>

> [!NOTE]
> <span data-ttu-id="2677a-141">為大型資料表和檢視擷取資料設定檔，作業成本會很高，而且可能會大幅增加註冊資料來源所需的時間。</span><span class="sxs-lookup"><span data-stu-id="2677a-141">Extracting a data profile can be a costly operation for large tables and views, and may significantly increase the time required to register a data source.</span></span>
>
>

## <a name="user-perspective"></a><span data-ttu-id="2677a-142">使用者觀點</span><span class="sxs-lookup"><span data-stu-id="2677a-142">User perspective</span></span>
<span data-ttu-id="2677a-143">在 Azure 資料目錄中，任何使用者都可以為已註冊的資料資產提供描述性中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2677a-143">In Azure Data Catalog, any user can provide descriptive metadata for a registered data asset.</span></span> <span data-ttu-id="2677a-144">每個使用者對資料及其用途各有不同的觀點。</span><span class="sxs-lookup"><span data-stu-id="2677a-144">Each user has a distinct perspective on the data and its use.</span></span> <span data-ttu-id="2677a-145">例如，負責伺服器的系統管理員可能提供其服務等級協定 (SLA) 或備份時段的詳細資料。資料負責人可能針對資料所支援的商務程序提供文件連結。分析師可能以最適合的詞彙提供描述給其他分析師，而且對於需要探索及了解資料的使用者來說，可能非常有價值。</span><span class="sxs-lookup"><span data-stu-id="2677a-145">For example, the administrator responsible for a server may provide the details of its service level agreement (SLA) or backup windows; a data steward may provide links to documentation for the business processes the data supports; and an analyst may provide a description in the terms that are most relevant to other analysts, and which can be most valuable to those users who need to discover and understand the data.</span></span>

<span data-ttu-id="2677a-146">每一種觀點基本上都很有價值，透過 Azure 資料目錄，每個使用者可以提供對他們有意義的資訊，而所有使用者都可以使用該資訊來了解資料及其用途。</span><span class="sxs-lookup"><span data-stu-id="2677a-146">Each of these perspectives are inherently valuable, and with Azure Data Catalog each user can provide the information that is meaningful to them, while all users can use that information to understand the data and its purpose.</span></span>

## <a name="expert"></a><span data-ttu-id="2677a-147">專家</span><span class="sxs-lookup"><span data-stu-id="2677a-147">Expert</span></span>
<span data-ttu-id="2677a-148">專家是指公認對資料資產有其獨特「專家」觀點的使用者。</span><span class="sxs-lookup"><span data-stu-id="2677a-148">An expert is a user who has been identified as having an informed “expert” perspective for a data asset.</span></span> <span data-ttu-id="2677a-149">任何使用者都可以將自己或其他使用者加入成為資產的專家。</span><span class="sxs-lookup"><span data-stu-id="2677a-149">Any user can add themselves or another user as an expert for an asset.</span></span> <span data-ttu-id="2677a-150">成為專家並不表示在 Azure 資料目錄具有任何額外的權限。它可讓使用者在檢閱資產的描述性中繼資料時，輕鬆找到最可能有用的觀點。</span><span class="sxs-lookup"><span data-stu-id="2677a-150">Being listed as an expert does not convey any additional privileges in Azure Data Catalog; it allows users to easily locate those perspectives that are most likely to be useful when reviewing an asset’s descriptive metadata.</span></span>

## <a name="owner"></a><span data-ttu-id="2677a-151">擁有者</span><span class="sxs-lookup"><span data-stu-id="2677a-151">Owner</span></span>
<span data-ttu-id="2677a-152">擁有者是具有額外權限來管理 Azure 資料目錄中的資料資產的使用者。</span><span class="sxs-lookup"><span data-stu-id="2677a-152">An owner is a user who has additional privileges for managing a data asset in Azure Data Catalog.</span></span> <span data-ttu-id="2677a-153">使用者可以取得已註冊的資料資產的擁有權，而擁有者可以加入其他使用者成為共同擁有者。</span><span class="sxs-lookup"><span data-stu-id="2677a-153">Users can take ownership of registered data assets, and owners can add other users as co-owners.</span></span> <span data-ttu-id="2677a-154">如需詳細資訊，請參閱[如何管理資料資產](data-catalog-how-to-manage.md)</span><span class="sxs-lookup"><span data-stu-id="2677a-154">For more information see  [How to manage data assets](data-catalog-how-to-manage.md)</span></span>  

> [!NOTE]
> <span data-ttu-id="2677a-155">只有標準版 Azure 資料目錄中支援擁有權和管理。</span><span class="sxs-lookup"><span data-stu-id="2677a-155">Ownership and management are available only in the Standard Edition of Azure Data Catalog.</span></span>
>
>

## <a name="registration"></a><span data-ttu-id="2677a-156">註冊</span><span class="sxs-lookup"><span data-stu-id="2677a-156">Registration</span></span>
<span data-ttu-id="2677a-157">註冊是指從資料來源擷取資料資產中繼資料並複製到 Azure 資料目錄服務的動作。</span><span class="sxs-lookup"><span data-stu-id="2677a-157">Registration is the act of extracting data asset metadata from a data source and copying it to the Azure Data Catalog service.</span></span> <span data-ttu-id="2677a-158">然後就可以加註和探索已註冊的資料資產。</span><span class="sxs-lookup"><span data-stu-id="2677a-158">Data assets that have been registered can then be annotated and discovered.</span></span>

## <a name="see-also"></a><span data-ttu-id="2677a-159">另請參閱</span><span class="sxs-lookup"><span data-stu-id="2677a-159">See also</span></span>
* [<span data-ttu-id="2677a-160">什麼是 Azure 資料目錄？</span><span class="sxs-lookup"><span data-stu-id="2677a-160">What is Azure Data Catalog?</span></span>](data-catalog-what-is-data-catalog.md) <span data-ttu-id="2677a-161">〉 - 這篇文章提供 Azure 資料目錄服務的概觀、所提供的價值和所支援的案例。</span><span class="sxs-lookup"><span data-stu-id="2677a-161">- This article provides an overview of the Azure Data Catalog service, the value it provides, and the scenarios it supports.</span></span>
* <span data-ttu-id="2677a-162">[開始使用 Azure 資料目錄](data-catalog-get-started.md) 〉 - 這篇文章提供端對端教學課程，示範如何使用 Azure 資料目錄來探索資料來源。</span><span class="sxs-lookup"><span data-stu-id="2677a-162">[Get started with Azure Data Catalog](data-catalog-get-started.md) - This article provides an end-to-end tutorial that shows you how to use Azure Data Catalog for data source discovery.</span></span>  
