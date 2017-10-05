---
title: "Azure 資料目錄簡介 | Microsoft Docs"
description: "本文提供 Microsoft Azure 資料目錄的概觀，包括其具備的功能以及所解決的問題。 資料目錄可讓任何使用者註冊、探索、了解及取用資料來源。"
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
ms.openlocfilehash: a28a7679831201fcf3a9d1c15497ff706c2752a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-azure-data-catalog"></a><span data-ttu-id="5b76c-104">什麼是 Azure 資料目錄？</span><span class="sxs-lookup"><span data-stu-id="5b76c-104">What is Azure Data Catalog?</span></span>
<span data-ttu-id="5b76c-105">Azure 資料目錄是完全受管理的雲端服務，能讓其使用者探索它們需要的資料來源，並了解他們所尋找的資料來源。</span><span class="sxs-lookup"><span data-stu-id="5b76c-105">Azure Data Catalog is a fully managed cloud service whose users can discover the data sources they need and understand the data sources they find.</span></span> <span data-ttu-id="5b76c-106">同時，資料目錄可協助組織從現有的投資中獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="5b76c-106">At the same time, Data Catalog helps organizations get more value from their existing investments.</span></span> 

<span data-ttu-id="5b76c-107">任何使用者 (分析師、資料科學家或開發人員) 都能利用資料目錄來探索、了解及取用資料來源。</span><span class="sxs-lookup"><span data-stu-id="5b76c-107">With Data Catalog, any user (analyst, data scientist, or developer) can discover, understand, and consume data sources.</span></span> <span data-ttu-id="5b76c-108">資料目錄包括中繼資料和附註的 crowdsourcing 模型。</span><span class="sxs-lookup"><span data-stu-id="5b76c-108">Data Catalog includes a crowdsourcing model of metadata and annotations.</span></span> <span data-ttu-id="5b76c-109">它是單一的中心位置，能讓組織的所有使用者貢獻其專業知識，並建置資料的社群和文化特性。</span><span class="sxs-lookup"><span data-stu-id="5b76c-109">It is a single, central place for all of an organization's users to contribute their knowledge and build a community and culture of data.</span></span>

## <a name="discovery-challenges-for-data-consumers"></a><span data-ttu-id="5b76c-110">探索資料取用者面臨的挑戰</span><span class="sxs-lookup"><span data-stu-id="5b76c-110">Discovery challenges for data consumers</span></span>
<span data-ttu-id="5b76c-111">傳統上，探索企業資料來源一向都是根據部落知識的一項有機程序。</span><span class="sxs-lookup"><span data-stu-id="5b76c-111">Traditionally, discovering enterprise data sources has been an organic process based on tribal knowledge.</span></span> <span data-ttu-id="5b76c-112">對於想要充分利用其資訊資產的公司，這個方法會帶來許多挑戰：</span><span class="sxs-lookup"><span data-stu-id="5b76c-112">For companies that want to get the most value from their information assets, this approach presents numerous challenges:</span></span>

* <span data-ttu-id="5b76c-113">使用者可能不知道，除非他們在另一個流程當中與資料來源有所接觸，否則資料來源會一直存在。</span><span class="sxs-lookup"><span data-stu-id="5b76c-113">Users might not be aware that a data source exists unless they come into contact with it as part of another process.</span></span> <span data-ttu-id="5b76c-114">並沒有任何已註冊資料來源的中央位置。</span><span class="sxs-lookup"><span data-stu-id="5b76c-114">There is no central location where data sources are registered.</span></span>
* <span data-ttu-id="5b76c-115">除非使用者知道資料來源的位置，否則它們無法使用用戶端應用程式連線到資料。</span><span class="sxs-lookup"><span data-stu-id="5b76c-115">Unless users know the location of a data source, they cannot connect to the data by using a client application.</span></span> <span data-ttu-id="5b76c-116">資料取用體驗需要使用者知道連接字串或路徑。</span><span class="sxs-lookup"><span data-stu-id="5b76c-116">Data-consumption experiences require users to know the connection string or path.</span></span>
* <span data-ttu-id="5b76c-117">除非使用者知道資料來源文件的位置，否則無法了解資料的用途。</span><span class="sxs-lookup"><span data-stu-id="5b76c-117">Unless users know the location of a data source's documentation, they cannot understand the intended uses of the data.</span></span> <span data-ttu-id="5b76c-118">資料來源和文件可能會存在於許多地方，且可透過各種不同的體驗來取用。</span><span class="sxs-lookup"><span data-stu-id="5b76c-118">Data sources and documentation might live in a variety of places and be consumed through a variety of experiences.</span></span>
* <span data-ttu-id="5b76c-119">如果使用者有關於資訊資產的疑問，必須洽詢負責資料的專家或小組，並讓它們離線參與。</span><span class="sxs-lookup"><span data-stu-id="5b76c-119">If users have questions about an information asset, they must locate the expert or team that's responsible for the data and engage them offline.</span></span> <span data-ttu-id="5b76c-120">資料和包含關於其使用方式之專家觀點的資料之間，沒有任何明確的連線。</span><span class="sxs-lookup"><span data-stu-id="5b76c-120">There is no explicit connection between data and those with expert perspectives on its use.</span></span>
* <span data-ttu-id="5b76c-121">除非使用者了解要求存取資料來源的程序，否則，探索資料來源及其文件仍無法協助他們存取資料。</span><span class="sxs-lookup"><span data-stu-id="5b76c-121">Unless users understand the process for requesting access to the data source, discovering the data source and its documentation still does not help them access the data.</span></span>

## <a name="discovery-challenges-for-data-producers"></a><span data-ttu-id="5b76c-122">探索資料產生者面臨的挑戰</span><span class="sxs-lookup"><span data-stu-id="5b76c-122">Discovery challenges for data producers</span></span>
<span data-ttu-id="5b76c-123">雖然資料取用者面臨先前所述的挑戰，但負責產生和維護的資訊資產的使用者本身也面臨挑戰：</span><span class="sxs-lookup"><span data-stu-id="5b76c-123">Although data consumers face the previously mentioned challenges, users who are responsible for producing and maintaining information assets face challenges of their own:</span></span>

* <span data-ttu-id="5b76c-124">將具有描述性中繼資料的資料來源加以註釋，通常是徒勞無功的。</span><span class="sxs-lookup"><span data-stu-id="5b76c-124">Annotating data sources with descriptive metadata is often a lost effort.</span></span> <span data-ttu-id="5b76c-125">用戶端應用程式通常會忽略儲存在資料來源的描述。</span><span class="sxs-lookup"><span data-stu-id="5b76c-125">Client applications typically ignore descriptions that are stored in the data source.</span></span>
* <span data-ttu-id="5b76c-126">建立資料來源的文件，通常是徒勞無功的。</span><span class="sxs-lookup"><span data-stu-id="5b76c-126">Creating documentation for data sources is often a lost effort.</span></span> <span data-ttu-id="5b76c-127">保持文件與資料來源同步處理是一項持續的責任，使用者可能會對於過期的文件缺乏信任。</span><span class="sxs-lookup"><span data-stu-id="5b76c-127">Keeping documentation in sync with data sources is an ongoing responsibility, and users might lack trust in documentation that's perceived as being out of date.</span></span>
* <span data-ttu-id="5b76c-128">建立和維護資料來源的文件既複雜又耗時。</span><span class="sxs-lookup"><span data-stu-id="5b76c-128">Creating and maintaining documentation for data sources is complex and time-consuming.</span></span> <span data-ttu-id="5b76c-129">而要讓使用資料來源的每個使用者可隨時取得文件可能會更為艱鉅。</span><span class="sxs-lookup"><span data-stu-id="5b76c-129">Making that documentation readily available to everyone who uses the data source can be even more so.</span></span>
* <span data-ttu-id="5b76c-130">限制對資料來源的存取，並確保資料取用者知道如何要求存取是一項持續的挑戰。</span><span class="sxs-lookup"><span data-stu-id="5b76c-130">Restricting access to data sources and ensuring that data consumers know how to request access is an ongoing challenge.</span></span>

<span data-ttu-id="5b76c-131">這些挑戰結合起來，會形成更大的障礙，使得公司更難以鼓勵和推動使用企業資料並加以了解。</span><span class="sxs-lookup"><span data-stu-id="5b76c-131">When such challenges are combined, they present a significant barrier for companies who want to encourage and promote the use and understanding of enterprise data.</span></span>

## <a name="azure-data-catalog-can-help"></a><span data-ttu-id="5b76c-132">Azure 資料目錄能提供協助</span><span class="sxs-lookup"><span data-stu-id="5b76c-132">Azure Data Catalog can help</span></span>
<span data-ttu-id="5b76c-133">資料目錄旨在解決這些問題，有助於讓企業能夠充分利用現有的資訊資產。</span><span class="sxs-lookup"><span data-stu-id="5b76c-133">Data Catalog is designed to address these problems and to help enterprises get the most value from their existing information assets.</span></span> <span data-ttu-id="5b76c-134">資料目錄能讓管理資料的使用者輕鬆地探索和了解資料來源。</span><span class="sxs-lookup"><span data-stu-id="5b76c-134">Data Catalog makes data sources easily discoverable and understandable by the users who manage the data.</span></span>

<span data-ttu-id="5b76c-135">資料目錄提供雲端型服務，其中可以註冊資料來源。</span><span class="sxs-lookup"><span data-stu-id="5b76c-135">Data Catalog provides a cloud-based service into which a data source can be registered.</span></span> <span data-ttu-id="5b76c-136">資料會保留在現有的位置，但其中繼資料的複本會連同資料來源位置的參考，一起新增至資料目錄。</span><span class="sxs-lookup"><span data-stu-id="5b76c-136">The data remains in its existing location, but a copy of its metadata is added to Data Catalog, along with a reference to the data-source location.</span></span> <span data-ttu-id="5b76c-137">此中繼資料也會編製索引，透過搜尋輕鬆找到每個資料來源，並讓探索資料來源的使用者了解每個資料來源。</span><span class="sxs-lookup"><span data-stu-id="5b76c-137">The metadata is also indexed to make each data source easily discoverable via search and understandable to the users who discover it.</span></span>

<span data-ttu-id="5b76c-138">註冊資料來源之後，進行註冊的使用者或企業中的其他使用者即可充實其中繼資料。</span><span class="sxs-lookup"><span data-stu-id="5b76c-138">After a data source has been registered, its metadata can then be enriched, either by the user who registered it or by other users in the enterprise.</span></span> <span data-ttu-id="5b76c-139">任何使用者都可以提供描述、標記或其他中繼資料 (例如要求資料來源存取的文件和程序) 來加註資料來源。</span><span class="sxs-lookup"><span data-stu-id="5b76c-139">Any user can annotate a data source by providing descriptions, tags, or other metadata, such as documentation and processes for requesting data source access.</span></span> <span data-ttu-id="5b76c-140">此描述性中繼資料可補充資料來源中已註冊的結構化中繼資料 (例如資料行名稱和資料類型)。</span><span class="sxs-lookup"><span data-stu-id="5b76c-140">This descriptive metadata supplements the structural metadata (such as column names and data types) that's registered from the data source.</span></span>

<span data-ttu-id="5b76c-141">註冊來源的主要目的是為了探索和了解資料來源及其用途。</span><span class="sxs-lookup"><span data-stu-id="5b76c-141">Discovering and understanding data sources and their use is the primary purpose of registering the sources.</span></span> <span data-ttu-id="5b76c-142">企業使用者可能需要的資料，是需要正確資料的資料商業智慧、應用程式開發、資料科學，或任何其他工作。</span><span class="sxs-lookup"><span data-stu-id="5b76c-142">Enterprise users might need data for business intelligence, application development, data science, or any other task where the right data is required.</span></span> <span data-ttu-id="5b76c-143">他們可以使用資料目錄探索體驗，快速尋找符合其需求的資料、了解資料以評估其適合的用途，並在其選擇的工具中開啟資料來源來取用資料。</span><span class="sxs-lookup"><span data-stu-id="5b76c-143">They can use the Data Catalog discovery experience to quickly find data that matches their needs, understand the data to evaluate its fitness for the purpose, and consume the data by opening the data source in their tool of choice.</span></span> 

<span data-ttu-id="5b76c-144">同時，使用者可以參與目錄，方法是將已註冊的資料來源加以標記、記錄及註解。</span><span class="sxs-lookup"><span data-stu-id="5b76c-144">At the same time, users can contribute to the catalog by tagging, documenting, and annotating data sources that have already been registered.</span></span> <span data-ttu-id="5b76c-145">它們也可以註冊新的資料來源，接著使用者的社群便可加以探索、了解和取用。</span><span class="sxs-lookup"><span data-stu-id="5b76c-145">They can also register new data sources, which can then be discovered, understood, and consumed by the community of catalog users.</span></span>

![資料目錄功能](./media/data-catalog-what-is-data-catalog/data-catalog-capabilities.png)

## <a name="learn-more-about-data-catalog"></a><span data-ttu-id="5b76c-147">深入了解資料目錄</span><span class="sxs-lookup"><span data-stu-id="5b76c-147">Learn more about Data Catalog</span></span>
<span data-ttu-id="5b76c-148">若要深入了解資料目錄的功能，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="5b76c-148">To learn more about the capabilities of Data Catalog, see:</span></span>

* [<span data-ttu-id="5b76c-149">如何註冊資料來源</span><span class="sxs-lookup"><span data-stu-id="5b76c-149">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="5b76c-150">如何探索資料來源</span><span class="sxs-lookup"><span data-stu-id="5b76c-150">How to discover data sources</span></span>](data-catalog-how-to-discover.md)
* [<span data-ttu-id="5b76c-151">如何註解資料來源</span><span class="sxs-lookup"><span data-stu-id="5b76c-151">How to annotate data sources</span></span>](data-catalog-how-to-annotate.md)
* [<span data-ttu-id="5b76c-152">如何記載資料來源</span><span class="sxs-lookup"><span data-stu-id="5b76c-152">How to document data sources</span></span>](data-catalog-how-to-documentation.md)
* [<span data-ttu-id="5b76c-153">如何連接到資料來源</span><span class="sxs-lookup"><span data-stu-id="5b76c-153">How to connect to data sources</span></span>](data-catalog-how-to-connect.md)
* [<span data-ttu-id="5b76c-154">如何使用巨量資料</span><span class="sxs-lookup"><span data-stu-id="5b76c-154">How to work with big data</span></span>](data-catalog-how-to-big-data.md)
* [<span data-ttu-id="5b76c-155">如何管理資料資產</span><span class="sxs-lookup"><span data-stu-id="5b76c-155">How to manage data assets</span></span>](data-catalog-how-to-manage.md)
* [<span data-ttu-id="5b76c-156">如何設定商務詞彙</span><span class="sxs-lookup"><span data-stu-id="5b76c-156">How to set up the Business Glossary</span></span>](data-catalog-how-to-business-glossary.md)
* [<span data-ttu-id="5b76c-157">常見問題集</span><span class="sxs-lookup"><span data-stu-id="5b76c-157">Frequently asked questions</span></span>](data-catalog-frequently-asked-questions.md)

## <a name="next-steps"></a><span data-ttu-id="5b76c-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b76c-158">Next steps</span></span>
<span data-ttu-id="5b76c-159">如需開始使用資料目錄，請移至：</span><span class="sxs-lookup"><span data-stu-id="5b76c-159">To get started with Data Catalog, go to:</span></span>
* [<span data-ttu-id="5b76c-160">Microsoft Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="5b76c-160">Microsoft Azure Data Catalog</span></span>](https://www.azuredatacatalog.com)
* [<span data-ttu-id="5b76c-161">開始使用 Azure 資料目錄</span><span class="sxs-lookup"><span data-stu-id="5b76c-161">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
