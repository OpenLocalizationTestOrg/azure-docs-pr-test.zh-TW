---
title: "建立和編輯 Azure 記錄分析中的記錄檔查詢的 aaaPortals |Microsoft 文件"
description: "本文說明 hello 入口網站，您可以使用在 Azure Log Analytics toocreate 和編輯的記錄搜尋。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: 7a2657574a132b2c4298511bb31259e68113ac91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="portals-for-creating-and-editing-log-queries-in-azure-log-analytics"></a><span data-ttu-id="6fc79-103">Azure Log Analytics 中用於建立和編輯記錄查詢的入口網站</span><span class="sxs-lookup"><span data-stu-id="6fc79-103">Portals for creating and editing log queries in Azure Log Analytics</span></span>

> [!NOTE]
> <span data-ttu-id="6fc79-104">本文說明在使用新的查詢語言 hello Azure Log Analytics 入口網站。</span><span class="sxs-lookup"><span data-stu-id="6fc79-104">This article describes portals in Azure Log Analytics using hello new query language.</span></span>  <span data-ttu-id="6fc79-105">您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc79-105">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="6fc79-106">如果您的工作區尚未升級的 toohello 新的查詢語言，您應該參閱太[尋找資料記錄分析中使用記錄搜尋](log-analytics-log-searches.md)hello 最新版 hello 記錄搜尋入口網站上的資訊。</span><span class="sxs-lookup"><span data-stu-id="6fc79-106">If your workspace hasn't been upgraded toohello new query language, you should refer too[Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on hello current version of hello Log Search portal.</span></span>

<span data-ttu-id="6fc79-107">您可以使用記錄搜尋中的許多地方整個記錄分析 tooretrieve 資料從 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="6fc79-107">You use log searches in a variety of places throughout Log Analytics tooretrieve data from hello workspace.</span></span>  <span data-ttu-id="6fc79-108">實際建立和編輯查詢此外 tooworking 以互動方式與傳回資料不過，您必須是下面所述的兩個選項。</span><span class="sxs-lookup"><span data-stu-id="6fc79-108">For actually creating and editing queries in addition tooworking interactively with returned data though, you have two options that are described below.</span></span>  

## <a name="log-search-portal"></a><span data-ttu-id="6fc79-109">記錄搜尋入口網站</span><span class="sxs-lookup"><span data-stu-id="6fc79-109">Log search portal</span></span>
<span data-ttu-id="6fc79-110">從 hello Azure 入口網站或 hello OMS 入口網站存取 hello 記錄搜尋入口網站。</span><span class="sxs-lookup"><span data-stu-id="6fc79-110">hello Log Search portal is accessible from hello Azure portal or hello OMS portal.</span></span>  <span data-ttu-id="6fc79-111">它適合用來建立可在單行中建立的基本查詢。</span><span class="sxs-lookup"><span data-stu-id="6fc79-111">It's suitable for creating basic queries that can be created on a single line.</span></span>  <span data-ttu-id="6fc79-112">而不啟動外部的入口網站，可以使用 hello 記錄搜尋網站，您可以使用它 tooperform 各式各樣函式包括建立警示規則、 建立電腦群組，以及匯出 hello hello 查詢結果的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="6fc79-112">hello Log Search portal can be used without launching an external portal, and you can use it tooperform a variety of functions with log searches including creating alert rules, creating computer groups, and exporting hello results of hello query.</span></span>  

<span data-ttu-id="6fc79-113">hello 記錄搜尋入口網站會提供多項功能，而不需要 hello 查詢語言的完整知識編輯 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="6fc79-113">hello Log Search portal provides multiple features for editing hello query without having a full knowledge of hello query language.</span></span>  <span data-ttu-id="6fc79-114">您可以取得這些功能摘要[Azure Log Analytics 使用 hello 記錄搜尋入口網站中建立的記錄搜尋](log-analytics-log-search-log-search-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6fc79-114">You can get a summary of these features in [Create log searches in Azure Log Analytics using hello Log Search portal](log-analytics-log-search-log-search-portal.md).</span></span>


![記錄搜尋入口網站](media/log-analytics-log-search-portals/log-search-portal.png)

## <a name="advanced-analytics-portal"></a><span data-ttu-id="6fc79-116">進階 Analytics 入口網站</span><span class="sxs-lookup"><span data-stu-id="6fc79-116">Advanced Analytics portal</span></span>
<span data-ttu-id="6fc79-117">hello 進階分析入口網站是一個專用的入口網站，提供進階的功能不適用於 hello 記錄搜尋入口網站。</span><span class="sxs-lookup"><span data-stu-id="6fc79-117">hello Advanced Analytics portal is a dedicated portal that provides advanced functionality not available in hello Log Search portal.</span></span>  <span data-ttu-id="6fc79-118">功能包括 hello 能力 tooedit 查詢在多行上，選擇性地執行程式碼、 區分內容的 Intellisense 和智慧的分析。</span><span class="sxs-lookup"><span data-stu-id="6fc79-118">Features include hello ability tooedit a query on multiple lines, selectively execute code, context sensitive Intellisense, and Smart Analytics.</span></span>  <span data-ttu-id="6fc79-119">hello Advanced Analytics 入口網站是最適合在設計複雜的查詢，可能是儲存為記錄搜尋或複製並貼到其他的記錄分析項目。</span><span class="sxs-lookup"><span data-stu-id="6fc79-119">hello Advanced Analytics portal is most suitable for designing complex queries that are either saved as a log search or copied and pasted into other Log Analytics elements.</span></span>  <span data-ttu-id="6fc79-120">您啟動 hello Advanced Analytics 入口網站，從 hello 記錄搜尋入口網站中的連結。</span><span class="sxs-lookup"><span data-stu-id="6fc79-120">You launch hello Advanced Analytics portal from a link in hello Log Search portal.</span></span>

![進階 Analytics 入口網站](media/log-analytics-log-search-portals/advanced-analytics-portal.png)


<span data-ttu-id="6fc79-122">因為其進階的功能，您將通常用於 hello 進階分析入口網站為您主要的工具建立和編輯查詢。</span><span class="sxs-lookup"><span data-stu-id="6fc79-122">Because of its advanced features, you'll usually use hello Advanced Analytics portal as your primary tool for creating and editing queries.</span></span>  <span data-ttu-id="6fc79-123">一旦您判定 hello 查詢如預期般運作，然後複製並貼入例如 hello 記錄搜尋入口網站或檢視表設計工具的其他位置。</span><span class="sxs-lookup"><span data-stu-id="6fc79-123">Once you've determined that hello query works as expected, then you'll copy and paste it elsewhere such as hello Log Search portal or View Designer.</span></span>  <span data-ttu-id="6fc79-124">由於 hello Advanced Analytics 入口網站透過支援多行的查詢，從這個入口網站複製查詢時需要 tootake hello 下列事項。</span><span class="sxs-lookup"><span data-stu-id="6fc79-124">Because hello Advanced Analytics portal supports queries with multiple lines though, you need tootake hello following into consideration when copying a query from this portal.</span></span>

- <span data-ttu-id="6fc79-125">必須從 hello 查詢移除註解，才能有複製及貼到另一個位置。</span><span class="sxs-lookup"><span data-stu-id="6fc79-125">Comments must be removed from hello query before it's copied and pasted into another location.</span></span>  <span data-ttu-id="6fc79-126">您可以在一行前加上兩個斜線 (//) 以對該行進行註解。</span><span class="sxs-lookup"><span data-stu-id="6fc79-126">You can comment a line by preceding it with two slashes (//).</span></span>  <span data-ttu-id="6fc79-127">將多行查詢貼到單行時，會移除分行符號。</span><span class="sxs-lookup"><span data-stu-id="6fc79-127">When you paste a multiple line query into a single line, line breaks are removed.</span></span>  <span data-ttu-id="6fc79-128">如果包含了註解，hello 第一個註解後面的所有字元都視為 hello 註解的一部分。</span><span class="sxs-lookup"><span data-stu-id="6fc79-128">If comments are included, all characters after hello first comment are considered part of hello comment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6fc79-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fc79-129">Next steps</span></span>

- <span data-ttu-id="6fc79-130">逐步教學課程使用 hello[記錄搜尋入口網站](log-analytics-log-search-log-search-portal.md)或 hello [Advanced Analytics 入口網站](https://go.microsoft.com/fwlink/?linkid=856587)toocreate 查詢。</span><span class="sxs-lookup"><span data-stu-id="6fc79-130">Walk through a tutorial on using hello [Log Search portal](log-analytics-log-search-log-search-portal.md) or hello [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) toocreate queries.</span></span>
- <span data-ttu-id="6fc79-131">簽出[上撰寫查詢的教學課程](https://go.microsoft.com/fwlink/?linkid=856078)使用 hello 新的查詢語言。</span><span class="sxs-lookup"><span data-stu-id="6fc79-131">Check out a [tutorial on writing queries](https://go.microsoft.com/fwlink/?linkid=856078) using hello new query language.</span></span>
