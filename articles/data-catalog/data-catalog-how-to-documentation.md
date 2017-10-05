---
title: "如何記載資料來源 | Microsoft Docs"
description: "專門說明如何在 Azure 資料目錄中記載資料資產的操作說明文章。"
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="575b8-103">記載資料來源</span><span class="sxs-lookup"><span data-stu-id="575b8-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="575b8-104">簡介</span><span class="sxs-lookup"><span data-stu-id="575b8-104">Introduction</span></span>
<span data-ttu-id="575b8-105"> 是全面管理的雲端服務，可作為企業資料來源的註冊系統和探索系統。</span><span class="sxs-lookup"><span data-stu-id="575b8-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="575b8-106">換句話說，**Azure 資料目錄**的重點在於協助人們探索、了解，以及使用資料來源，並可協助組織從現有的資料獲得更多價值。</span><span class="sxs-lookup"><span data-stu-id="575b8-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="575b8-107">當資料來源向 **Azure 資料目錄**註冊之後，該服務會複製其中繼資料並建立索引，但不僅止於此。</span><span class="sxs-lookup"><span data-stu-id="575b8-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="575b8-108">**Azure 資料目錄** 也可讓使用者提供自己的完整說明文件來描述資料來源的使用方式和常見案例。</span><span class="sxs-lookup"><span data-stu-id="575b8-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="575b8-109">在 [如何註解資料來源](data-catalog-how-to-annotate.md)中，您已了解知道資料來源的專家可以使用標記和描述來為資料來源加上註解。</span><span class="sxs-lookup"><span data-stu-id="575b8-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="575b8-110">**Azure 資料目錄** 入口網站含有 RTF 編輯器，因此使用者可以完整記載資料資產和容器。</span><span class="sxs-lookup"><span data-stu-id="575b8-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="575b8-111">該編輯器包括段落格式化，例如標題、文字格式化、項目符號清單、編號清單和資料表。</span><span class="sxs-lookup"><span data-stu-id="575b8-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="575b8-112">標記和描述非常適合用於簡單的註解。</span><span class="sxs-lookup"><span data-stu-id="575b8-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="575b8-113">不過，為了協助資料取用者深入了解資料來源的使用方式和資料來源的商務案例，專家可以提供完整而詳細的說明文件。</span><span class="sxs-lookup"><span data-stu-id="575b8-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="575b8-114">想要記載資料來源很容易。</span><span class="sxs-lookup"><span data-stu-id="575b8-114">It's easy to document a data source.</span></span> <span data-ttu-id="575b8-115">請選取資料資產或容器，然後選擇 [說明文件] 。</span><span class="sxs-lookup"><span data-stu-id="575b8-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="575b8-116">記載資料資產</span><span class="sxs-lookup"><span data-stu-id="575b8-116">Documenting data assets</span></span>
<span data-ttu-id="575b8-117">**Azure 資料目錄** 說明文件的優點可讓您使用資料目錄做為內容儲存機制，以建立完整的資料資產敘述。</span><span class="sxs-lookup"><span data-stu-id="575b8-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="575b8-118">您可以探索說明容器和資料表的詳細內容。</span><span class="sxs-lookup"><span data-stu-id="575b8-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="575b8-119">如果您在其他內容儲存機制 (例如 SharePoint 或檔案共用) 已有內容，您可以新增資產說明文件連結來參考此現有內容。</span><span class="sxs-lookup"><span data-stu-id="575b8-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="575b8-120">此功能可讓您更容易找到現有的說明文件。</span><span class="sxs-lookup"><span data-stu-id="575b8-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="575b8-121">說明文件不會包含在搜尋索引中。</span><span class="sxs-lookup"><span data-stu-id="575b8-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="575b8-122">說明文件層級的範圍可從描述資料資產容器的特性和值，到詳細描述容器內的資料表結構描述。</span><span class="sxs-lookup"><span data-stu-id="575b8-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="575b8-123">所提供的說明文件層級應以商務需求為準。</span><span class="sxs-lookup"><span data-stu-id="575b8-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="575b8-124">但一般來說，記載資料資產的優缺點如下︰</span><span class="sxs-lookup"><span data-stu-id="575b8-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="575b8-125">只記載容器︰所有內容集中放置，但可能缺少可供使用者做出明智決策的必要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="575b8-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="575b8-126">只記載資料表︰內容專用於該物件，但使用者會將文件放在多個地方。</span><span class="sxs-lookup"><span data-stu-id="575b8-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="575b8-127">記載容器和資料表︰最全面的方法，但可能需要花更多時間維護文件。</span><span class="sxs-lookup"><span data-stu-id="575b8-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="575b8-128">摘要</span><span class="sxs-lookup"><span data-stu-id="575b8-128">Summary</span></span>
<span data-ttu-id="575b8-129">在 **Azure 資料目錄** 中記載資料來源可依所需詳細程度建立資料資產的相關敘述。</span><span class="sxs-lookup"><span data-stu-id="575b8-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="575b8-130">藉由使用連結，您可以連結至現有內容儲存機制中儲存的內容，以結合您現有的文件和資料資產。</span><span class="sxs-lookup"><span data-stu-id="575b8-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="575b8-131">一旦使用者找到合適的資料資產，就能取得一組完整的說明文件。</span><span class="sxs-lookup"><span data-stu-id="575b8-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
