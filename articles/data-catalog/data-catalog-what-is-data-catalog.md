---
title: "aaaIntroduction tooAzure 資料目錄 |Microsoft 文件"
description: "本文提供 Microsoft Azure 資料目錄，包括其功能和其定址 hello 問題的概觀。 資料類別目錄可讓任何使用者 tooregister、 探索、 了解及取用資料來源。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: cc733907-17ec-4153-9f0c-5b3754b2db19
ms.service: data-catalog
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 82144c440b5692d3608af08208f36ee8e6dfdc93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-data-catalog"></a><span data-ttu-id="defe0-104">什麼是 Azure 資料目錄？</span><span class="sxs-lookup"><span data-stu-id="defe0-104">What is Azure Data Catalog?</span></span>
<span data-ttu-id="defe0-105">Azure 資料目錄是完全受管理的雲端服務的使用者可以探索 hello 必要且了解 hello 資料來源，而是尋找資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-105">Azure Data Catalog is a fully managed cloud service whose users can discover hello data sources they need and understand hello data sources they find.</span></span> <span data-ttu-id="defe0-106">在 hello 相同的時間，現有的投資從多個值的資料目錄可協助組織 get。</span><span class="sxs-lookup"><span data-stu-id="defe0-106">At hello same time, Data Catalog helps organizations get more value from their existing investments.</span></span> 

<span data-ttu-id="defe0-107">任何使用者 (分析師、資料科學家或開發人員) 都能利用資料目錄來探索、了解及取用資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-107">With Data Catalog, any user (analyst, data scientist, or developer) can discover, understand, and consume data sources.</span></span> <span data-ttu-id="defe0-108">資料目錄包括中繼資料和附註的 crowdsourcing 模型。</span><span class="sxs-lookup"><span data-stu-id="defe0-108">Data Catalog includes a crowdsourcing model of metadata and annotations.</span></span> <span data-ttu-id="defe0-109">它是單一的中心位置，以讓所有組織的使用者 toocontribute 其專業知識，並建置社群和文化特性的資料。</span><span class="sxs-lookup"><span data-stu-id="defe0-109">It is a single, central place for all of an organization's users toocontribute their knowledge and build a community and culture of data.</span></span>

## <a name="discovery-challenges-for-data-consumers"></a><span data-ttu-id="defe0-110">探索資料取用者面臨的挑戰</span><span class="sxs-lookup"><span data-stu-id="defe0-110">Discovery challenges for data consumers</span></span>
<span data-ttu-id="defe0-111">傳統上，探索企業資料來源一向都是根據部落知識的一項有機程序。</span><span class="sxs-lookup"><span data-stu-id="defe0-111">Traditionally, discovering enterprise data sources has been an organic process based on tribal knowledge.</span></span> <span data-ttu-id="defe0-112">對於大部分的值，從其資訊資產想 tooget hello 的公司而言，這種方法會出現許多挑戰：</span><span class="sxs-lookup"><span data-stu-id="defe0-112">For companies that want tooget hello most value from their information assets, this approach presents numerous challenges:</span></span>

* <span data-ttu-id="defe0-113">使用者可能不知道，除非他們在另一個流程當中與資料來源有所接觸，否則資料來源會一直存在。</span><span class="sxs-lookup"><span data-stu-id="defe0-113">Users might not be aware that a data source exists unless they come into contact with it as part of another process.</span></span> <span data-ttu-id="defe0-114">並沒有任何已註冊資料來源的中央位置。</span><span class="sxs-lookup"><span data-stu-id="defe0-114">There is no central location where data sources are registered.</span></span>
* <span data-ttu-id="defe0-115">除非使用者知道的資料來源的 hello 位置，它們就無法使用用戶端應用程式來連線 toohello 資料。</span><span class="sxs-lookup"><span data-stu-id="defe0-115">Unless users know hello location of a data source, they cannot connect toohello data by using a client application.</span></span> <span data-ttu-id="defe0-116">資料消費體驗會需要使用者 tooknow hello 連接字串或路徑。</span><span class="sxs-lookup"><span data-stu-id="defe0-116">Data-consumption experiences require users tooknow hello connection string or path.</span></span>
* <span data-ttu-id="defe0-117">除非使用者知道的資料來源的文件的 hello 位置，否則他們無法了解 hello 適合使用的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="defe0-117">Unless users know hello location of a data source's documentation, they cannot understand hello intended uses of hello data.</span></span> <span data-ttu-id="defe0-118">資料來源和文件可能會存在於許多地方，且可透過各種不同的體驗來取用。</span><span class="sxs-lookup"><span data-stu-id="defe0-118">Data sources and documentation might live in a variety of places and be consumed through a variety of experiences.</span></span>
* <span data-ttu-id="defe0-119">如果使用者有疑問的資訊資產，必須找出 hello 專家或小組，負責 hello 資料，並讓它們參與離線。</span><span class="sxs-lookup"><span data-stu-id="defe0-119">If users have questions about an information asset, they must locate hello expert or team that's responsible for hello data and engage them offline.</span></span> <span data-ttu-id="defe0-120">資料和包含關於其使用方式之專家觀點的資料之間，沒有任何明確的連線。</span><span class="sxs-lookup"><span data-stu-id="defe0-120">There is no explicit connection between data and those with expert perspectives on its use.</span></span>
* <span data-ttu-id="defe0-121">除非使用者了解用來要求存取 toohello 資料來源的 hello 程序，探索 hello 資料來源和其文件仍無法解決它們存取 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="defe0-121">Unless users understand hello process for requesting access toohello data source, discovering hello data source and its documentation still does not help them access hello data.</span></span>

## <a name="discovery-challenges-for-data-producers"></a><span data-ttu-id="defe0-122">探索資料產生者面臨的挑戰</span><span class="sxs-lookup"><span data-stu-id="defe0-122">Discovery challenges for data producers</span></span>
<span data-ttu-id="defe0-123">雖然資料取用者朝 hello 先前所述的挑戰，使用者是負責產生和維護的資訊資產會面臨挑戰自己的：</span><span class="sxs-lookup"><span data-stu-id="defe0-123">Although data consumers face hello previously mentioned challenges, users who are responsible for producing and maintaining information assets face challenges of their own:</span></span>

* <span data-ttu-id="defe0-124">將具有描述性中繼資料的資料來源加以註釋，通常是徒勞無功的。</span><span class="sxs-lookup"><span data-stu-id="defe0-124">Annotating data sources with descriptive metadata is often a lost effort.</span></span> <span data-ttu-id="defe0-125">用戶端應用程式通常會忽略儲存在 hello 資料來源的描述。</span><span class="sxs-lookup"><span data-stu-id="defe0-125">Client applications typically ignore descriptions that are stored in hello data source.</span></span>
* <span data-ttu-id="defe0-126">建立資料來源的文件，通常是徒勞無功的。</span><span class="sxs-lookup"><span data-stu-id="defe0-126">Creating documentation for data sources is often a lost effort.</span></span> <span data-ttu-id="defe0-127">保持文件與資料來源同步處理是一項持續的責任，使用者可能會對於過期的文件缺乏信任。</span><span class="sxs-lookup"><span data-stu-id="defe0-127">Keeping documentation in sync with data sources is an ongoing responsibility, and users might lack trust in documentation that's perceived as being out of date.</span></span>
* <span data-ttu-id="defe0-128">建立和維護資料來源的文件既複雜又耗時。</span><span class="sxs-lookup"><span data-stu-id="defe0-128">Creating and maintaining documentation for data sources is complex and time-consuming.</span></span> <span data-ttu-id="defe0-129">讓使用 hello 資料來源的人員，文件集隨時可用 tooeveryone 可以更為。</span><span class="sxs-lookup"><span data-stu-id="defe0-129">Making that documentation readily available tooeveryone who uses hello data source can be even more so.</span></span>
* <span data-ttu-id="defe0-130">限制存取 toodata 來源，並確保資料取用者知道 toorequest 存取方式是進行中的挑戰。</span><span class="sxs-lookup"><span data-stu-id="defe0-130">Restricting access toodata sources and ensuring that data consumers know how toorequest access is an ongoing challenge.</span></span>

<span data-ttu-id="defe0-131">這類挑戰結合時，它們呈現一道重大障礙，公司想 tooencourage 及提升 hello 使用和了解企業資料。</span><span class="sxs-lookup"><span data-stu-id="defe0-131">When such challenges are combined, they present a significant barrier for companies who want tooencourage and promote hello use and understanding of enterprise data.</span></span>

## <a name="azure-data-catalog-can-help"></a><span data-ttu-id="defe0-132">Azure 資料目錄能提供協助</span><span class="sxs-lookup"><span data-stu-id="defe0-132">Azure Data Catalog can help</span></span>
<span data-ttu-id="defe0-133">資料目錄是設計的 tooaddress 這些問題和 toohelp 企業 get hello 最值從其現有的資訊資產。</span><span class="sxs-lookup"><span data-stu-id="defe0-133">Data Catalog is designed tooaddress these problems and toohelp enterprises get hello most value from their existing information assets.</span></span> <span data-ttu-id="defe0-134">資料目錄，讓資料來源輕鬆地探索及可了解 hello 使用者管理 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="defe0-134">Data Catalog makes data sources easily discoverable and understandable by hello users who manage hello data.</span></span>

<span data-ttu-id="defe0-135">資料目錄提供雲端型服務，其中可以註冊資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-135">Data Catalog provides a cloud-based service into which a data source can be registered.</span></span> <span data-ttu-id="defe0-136">hello 資料仍會保留在現有的位置，但它的中繼資料的副本加入 tooData 類別目錄，以及參考 toohello 資料來源位置。</span><span class="sxs-lookup"><span data-stu-id="defe0-136">hello data remains in its existing location, but a copy of its metadata is added tooData Catalog, along with a reference toohello data-source location.</span></span> <span data-ttu-id="defe0-137">hello 中繼資料也是索引的 toomake 輕易地找到透過搜尋和可了解 toohello 使用者探索每個資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-137">hello metadata is also indexed toomake each data source easily discoverable via search and understandable toohello users who discover it.</span></span>

<span data-ttu-id="defe0-138">已註冊的資料來源之後，它的中繼資料可以再被豐富，登錄它的 hello 使用者或是 hello 企業中其他使用者。</span><span class="sxs-lookup"><span data-stu-id="defe0-138">After a data source has been registered, its metadata can then be enriched, either by hello user who registered it or by other users in hello enterprise.</span></span> <span data-ttu-id="defe0-139">任何使用者都可以提供描述、標記或其他中繼資料 (例如要求資料來源存取的文件和程序) 來加註資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-139">Any user can annotate a data source by providing descriptions, tags, or other metadata, such as documentation and processes for requesting data source access.</span></span> <span data-ttu-id="defe0-140">此描述性的中繼資料補充 hello 結構化中繼資料 （例如資料行名稱和資料類型） 註冊 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-140">This descriptive metadata supplements hello structural metadata (such as column names and data types) that's registered from hello data source.</span></span>

<span data-ttu-id="defe0-141">探索及了解資料來源以及其用法是 hello 註冊 hello 來源的主要用途。</span><span class="sxs-lookup"><span data-stu-id="defe0-141">Discovering and understanding data sources and their use is hello primary purpose of registering hello sources.</span></span> <span data-ttu-id="defe0-142">企業使用者可能需要資料商業智慧、 應用程式開發、 資料科學中，或任何其他工作需要 hello 正確的資料的地方。</span><span class="sxs-lookup"><span data-stu-id="defe0-142">Enterprise users might need data for business intelligence, application development, data science, or any other task where hello right data is required.</span></span> <span data-ttu-id="defe0-143">他們可以使用 hello 資料目錄探索體驗 tooquickly 尋找資料符合其需求，其適合 hello 用途，了解 hello 資料 tooevaluate 和取用 hello 資料在其選擇的工具中開啟 hello 資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-143">They can use hello Data Catalog discovery experience tooquickly find data that matches their needs, understand hello data tooevaluate its fitness for hello purpose, and consume hello data by opening hello data source in their tool of choice.</span></span> 

<span data-ttu-id="defe0-144">在 hello 相同時，使用者可以參與 toohello 類別目錄的標記、 記錄及註解已註冊的資料來源。</span><span class="sxs-lookup"><span data-stu-id="defe0-144">At hello same time, users can contribute toohello catalog by tagging, documenting, and annotating data sources that have already been registered.</span></span> <span data-ttu-id="defe0-145">它們也可以登錄新資料來源，然後可探索、 了解，和由 hello 社群的目錄使用者。</span><span class="sxs-lookup"><span data-stu-id="defe0-145">They can also register new data sources, which can then be discovered, understood, and consumed by hello community of catalog users.</span></span>

![資料目錄功能](./media/data-catalog-what-is-data-catalog/data-catalog-capabilities.png)

## <a name="learn-more-about-data-catalog"></a><span data-ttu-id="defe0-147">深入了解資料目錄</span><span class="sxs-lookup"><span data-stu-id="defe0-147">Learn more about Data Catalog</span></span>
<span data-ttu-id="defe0-148">toolearn 進一步了解 hello 功能的資料目錄，請參閱：</span><span class="sxs-lookup"><span data-stu-id="defe0-148">toolearn more about hello capabilities of Data Catalog, see:</span></span>

* [<span data-ttu-id="defe0-149">如何 tooregister 資料來源</span><span class="sxs-lookup"><span data-stu-id="defe0-149">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="defe0-150">如何 toodiscover 資料來源</span><span class="sxs-lookup"><span data-stu-id="defe0-150">How toodiscover data sources</span></span>](data-catalog-how-to-discover.md)
* [<span data-ttu-id="defe0-151">如何 tooannotate 資料來源</span><span class="sxs-lookup"><span data-stu-id="defe0-151">How tooannotate data sources</span></span>](data-catalog-how-to-annotate.md)
* [<span data-ttu-id="defe0-152">如何 toodocument 資料來源</span><span class="sxs-lookup"><span data-stu-id="defe0-152">How toodocument data sources</span></span>](data-catalog-how-to-documentation.md)
* [<span data-ttu-id="defe0-153">如何 tooconnect toodata 來源</span><span class="sxs-lookup"><span data-stu-id="defe0-153">How tooconnect toodata sources</span></span>](data-catalog-how-to-connect.md)
* [<span data-ttu-id="defe0-154">如何 toowork 大型資料</span><span class="sxs-lookup"><span data-stu-id="defe0-154">How toowork with big data</span></span>](data-catalog-how-to-big-data.md)
* [<span data-ttu-id="defe0-155">如何 toomanage 資料資產</span><span class="sxs-lookup"><span data-stu-id="defe0-155">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
* [<span data-ttu-id="defe0-156">如何設定 tooset hello 商務字彙</span><span class="sxs-lookup"><span data-stu-id="defe0-156">How tooset up hello Business Glossary</span></span>](data-catalog-how-to-business-glossary.md)
* [<span data-ttu-id="defe0-157">常見問題集</span><span class="sxs-lookup"><span data-stu-id="defe0-157">Frequently asked questions</span></span>](data-catalog-frequently-asked-questions.md)

## <a name="next-steps"></a><span data-ttu-id="defe0-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="defe0-158">Next steps</span></span>
<span data-ttu-id="defe0-159">tooget 開始使用資料目錄，請移至：</span><span class="sxs-lookup"><span data-stu-id="defe0-159">tooget started with Data Catalog, go to:</span></span>
* [<span data-ttu-id="defe0-160">Microsoft Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="defe0-160">Microsoft Azure Data Catalog</span></span>](https://www.azuredatacatalog.com)
* [<span data-ttu-id="defe0-161">開始使用 Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="defe0-161">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
